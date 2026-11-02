# json-renderers-build-table-options

> Decorate and enhance JSON table specifications with options (serial numbering `#`, action buttons, search, and row utilities) — purely declarative and DOM-free.

---

## Why this exists

The core table builder (`json-renderers-build-table`) is designed to remain lean and focused exclusively on mapping columns and data rows into `colgroup`, `thead`, `tbody`, and `tfoot`.

However, real-world tables often require extra UI features:
- **Serial numbering (`#`)** prepended to headers, body rows, colgroup, and footer.
- **Row-level action buttons** (Edit / Delete / View / Save).
- **Search inputs** or toolbar components above the table.

This repository decouples those table extensions into clean, reusable instruction sets. It takes an existing table JSON specification and applies decorating instructions without touching the DOM.

---

## Installation

```bash
npm install json-renderers-build-table-options
```

---

## How It Works

`json-renderers-build-table-options` follows the **Pipeline / Decorator** pattern:

```
  Existing Table JSON Specification (base)
                  │
                  ▼
     json-renderers-build-table-options
        ├── Guards ({ base, options, showLog, returnLog })
        ├── Serial Instructions (prepends # column)
        ├── Options Instructions (appends action button column)
        └── Search Instructions (prepends toolbar/search)
                  │
                  ▼
       Updated Table JSON Specification
```

---

## Usage

### Clean & Natural API

```javascript
import buildOptions from "json-renderers-build-table-options";

const decoratedSpec = buildOptions({
    options: {
        showSerial: true,
        showOptions: true
    },
    base: tableBaseSpec
});
```

---

## API Reference

### `buildOptions({ options, base, showLog, returnLog })`

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `options` | `Object` | No | `{}` | Configuration object controlling which options to apply. |
| `base` | `Object` | **Yes** | — | The JSON table specification to decorate. Must be a valid object. |
| `showLog` | `boolean` | No | `false` | When `true`, outputs execution steps and guard evaluations to console. |
| `returnLog` | `Array` | No | `[]` | Array that captures execution logs and guard messages. |

### Supported `options` flags

- **`showSerial`** (`boolean`): Prepends a serial numbering (`#`) column into `colgroup`, `thead`, and `tbody` (and `tfoot` if present).
- **`showOptions`** (`boolean`): Appends an options/action buttons column into the table.
- **`showSearch`** (`boolean`): Injects search toolbar specifications.

### Version 6

The package entry point uses `src/v6`. It applies each serial/options instruction only when its target `data-role` exists in the supplied base. This allows body-only specifications to receive serial and options cells without requiring header, footer, or colgroup nodes. Version 5 remains available at `src/v5` with its original behavior.

---

## Architecture & Guard System (`v3`)

`v3` adopts a dedicated `guards/` subsystem where each parameter is validated independently:

```
src/v3/
├── index.js                     <-- Clean public entry
├── guards/
│   ├── index.js                 <-- Coordinator aggregating checks
│   ├── base/                    <-- Validates base is a valid object
│   ├── options/                 <-- Validates options object
│   ├── showLog/                 <-- Validates boolean
│   └── returnLog/               <-- Validates Array
├── instructionsForSerial.json
├── instructionsForOptions.json
└── insertSearch/
```
