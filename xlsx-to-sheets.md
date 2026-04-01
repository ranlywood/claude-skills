---
name: xlsx-to-sheets
description: Загрузка Excel-файла в Google Sheets с сохранением форматирования, формул и дизайна через googleworkspace-cli. Активируется когда нужно перенести xlsx в Google Sheets.
---

# Скилл: xlsx → Google Sheets

## Когда активировать

- «Загрузи в Google Sheets»
- «Перенеси Excel в Sheets»
- «Создай таблицу из xlsx»
- «Залей смету / файл в гугл»

---

## Критическое правило

**НИКОГДА не читать xlsx через openpyxl и заливать через `values batchUpdate`.**

Причины:
- В `ru_RU` локали (дефолт для RU-аккаунтов) формулы с `,` ломаются → `#ERROR!` (нужны `;`)
- Форматирование (цвета, шрифты, числовые форматы) не переносится совсем
- Межлистовые ссылки работают, но % формулы с IF падают

**Правильный способ — конвертация через Drive API.**

---

## Предварительные требования

### Установить gws CLI
```bash
brew install gws
```
`gws` — сторонний Google Workspace CLI (не официальный продукт Google).
Другие способы установки: https://github.com/nicholasgasior/gws

### Авторизоваться
```bash
gws auth login
```
Откроется браузер → войди в нужный Google-аккаунт → разреши доступ к Drive и Sheets.

---

## Алгоритм

### 1. Проверить авторизацию
```bash
gws auth status
```
Должно быть: `token_valid: true`

### 2. Загрузить с конвертацией
```bash
gws drive files create \
  --json '{"name": "Название таблицы", "mimeType": "application/vnd.google-apps.spreadsheet"}' \
  --upload '/путь/к/файлу.xlsx' \
  --upload-content-type 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'
```
Сохранить `id` из ответа.

### 3. Открыть доступ по ссылке
```bash
gws drive permissions create \
  --params '{"fileId": "SPREADSHEET_ID", "sendNotificationEmail": false}' \
  --json '{"role": "writer", "type": "anyone"}'
```
Варианты role: `writer` (редактирование), `reader` (просмотр), `commenter` (комментарии)

### 4. Дать ссылку
```
https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit
```

---

## Дополнительные операции

### Расшарить конкретному человеку по email
```bash
gws drive permissions create \
  --params '{"fileId": "ID", "sendNotificationEmail": true}' \
  --json '{"role": "writer", "type": "user", "emailAddress": "email@example.com"}'
```

### Удалить файл
```bash
gws drive files delete --params '{"fileId": "ID"}'
```

### Обновить данные в ячейках после загрузки
```bash
gws sheets spreadsheets values update \
  --params '{"spreadsheetId": "ID", "range": "Лист!A1", "valueInputOption": "USER_ENTERED"}' \
  --json '{"values": [["значение1", "значение2"]]}'
```

### Batch update нескольких диапазонов
```bash
gws sheets spreadsheets values batchUpdate \
  --params '{"spreadsheetId": "ID"}' \
  --json '{"valueInputOption": "USER_ENTERED", "data": [{"range": "Лист!A1", "values": [["val"]]}]}'
```

---

## Антипаттерны

| Что НЕ делать | Почему |
|---|---|
| `openpyxl` → `values batchUpdate` | Ломаются IF/TEXT формулы в ru_RU локали |
| Не указывать `mimeType: spreadsheet` в json | Загрузится как xlsx-файл, не как Sheets |
| Забыть `--upload-content-type` | Может неправильно определить формат |
| Не открыть доступ после создания | Файл доступен только владельцу |
