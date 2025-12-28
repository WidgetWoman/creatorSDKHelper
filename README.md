# pgCreator.js — Zoho Creator Utility

`pgCreator.js` provides the `AppRec` class and utility functions for interacting with Zoho Creator forms and reports. It supports CRUD operations, record counting, local record filtering, and widget integration helpers.

## Features

- Create, read, update, and delete records in Zoho Creator
- Count records matching criteria
- Filter and find records locally by ID or field
- Utility functions for Zoho Creator widget initialization and parent window navigation
- Phone number formatting helper
- Comprehensive JSDoc documentation for all methods

## Usage

### Import

```js
import AppRec, { initZoho, redirect, formatPhone } from "./app/pgCreator.js";
```

### Creating an Instance

```js
const appRec = new AppRec({
  form: "MyForm",
  report: "MyReport",
  criteria: '(Field1 == "Value")', // optional
});
```

### Creating a Record

```js
await appRec.create({ Field1: "Value", Field2: 123 });
```

### Reading Records

```js
// Reads with optional field_config and fields
const records = await appRec.read("custom", ["Field1", "Field2"]);
// Uses the criteria set in the constructor
```

### Updating a Record

```js
await appRec.updateById("RECORD_ID", { Field1: "New Value" });
```

### Deleting a Record

```js
await appRec.deleteById("RECORD_ID");
```

### Counting Records

```js
const count = await appRec.countRecords('(Field1 == "Value")');
```

### Local Filtering

```js
const record = appRec.viewById("RECORD_ID");
const matches = appRec.viewByField("Field1", "Value");
```

### Zoho Creator Widget Initialization

```js
// Pass the widget key (e.g., 'appointments') to extract user settings from query params
const zohoParams = await initZoho("appointments");
// zohoParams will include Zoho init params, user settings from query, and parentDomain if available
```

### Redirect Parent Window

```js
await redirect("redirect", "https://example.com", "same");
```

### Phone Number Formatting

```js
import { formatPhone } from "./app/pgCreator.js";
const formatted = formatPhone("+12345678900"); // (234) 567-8900
```

## API Reference

### `AppRec` Class

See JSDoc comments in `pgCreator.js` for detailed method documentation.

#### Constructor

- `new AppRec({ form, report, criteria })`

#### Methods

- `create(data)`
- `read(field_config, fields)`
- `updateById(recordId, data)`
- `deleteById(recordId)`
- `countRecords(criteria)`
- `viewById(id)`
- `viewByField(fieldName, value)`

### Utility Functions

- `initZoho(widgetkey)` — Initializes Zoho Creator widget and returns merged params for the given widget key
- `redirect(action, url, window)` — Redirects parent window using Zoho Creator UTIL API
- `formatPhone(phone)` — Formats a phone number string

## Requirements

- Zoho Creator Widget SDK loaded in your environment
- ES6 module support

## License

MIT

## License

MIT
