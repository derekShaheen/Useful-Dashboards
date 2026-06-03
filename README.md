# Useful Dashboards

A small collection of self-contained, browser-based tools for warehouse / WMS work. Each one is a single HTML file with no build step and no server — open it locally, or use the hosted version on GitHub Pages.

## Tools

| Tool | What it does | Live page |
|------|--------------|-----------|
| **Exacta Packout Test Builder** | Builds `ITEMSTATUS` packout messages for the Exacta packout pipeline. Output as a Postman body, SQL `INSERT`, or raw JSON. | [Open](https://derekshaheen.github.io/Useful-Dashboards/Bastian-Packout-Msg-Generator/exacta-packout.html) |
| **Serial Barcode Generator** | Generates print-ready barcode sheets (Code 128 / Code 39) from a serial number range and exports to PDF. | [Open](https://derekshaheen.github.io/Useful-Dashboards/Batch-Serial-Barcode-Generator/index.html) |

## Exacta Packout Test Builder

A card-based UI for assembling one or more `ITEMSTATUS` records. Set the container SSCC, location, packed quantity, and serial numbers per message, then export all messages as a single payload.

Three output modes:

- **Postman** — full request body wrapped as `{ "params": { "json": { "records": [ ... ] } } }`.
- **SQL INSERT** — one `INSERT INTO t_alr_import_message` per message, each with its own GUID `host_group_id`.
- **JSON Only** — raw record JSON without the Postman envelope.

See [the tool README](Bastian-Packout-Msg-Generator/README.md) for field mappings and example output.

## Serial Barcode Generator

Enter a start and end serial sharing a `prefix + numeric suffix` pattern (e.g. `WHF1180286` → `WHF1180325`); the tool validates the range, generates a preview, and exports a print-ready Letter-size PDF. Layout (columns/rows), barcode type, serial text, and cell borders are all configurable. Up to 5,000 serials per run. Everything renders in-browser via [JsBarcode](https://github.com/lindell/JsBarcode) and [jsPDF](https://github.com/parallax/jsPDF) — nothing is uploaded.

See [the tool README](Batch-Serial-Barcode-Generator/README.md) for layout options and supported serial formats.

## License

[GPL-2.0](LICENSE)
