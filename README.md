# Serial Barcode Generator

A self-contained HTML tool for generating printable barcode sheets from a serial number range. No installation, no server — just open the file in a browser.

## Usage

1. Open `barcode-generator.html` in any modern browser
2. Enter a **Start Serial** and **End Serial** (e.g. `WHF1180286` → `WHF1180325`)
3. The tool previews the count and validates the range as you type
4. Click **Load Range** to populate the serial list
5. Adjust layout options if needed, then click **Generate Preview**
6. Click **Download PDF** to save the print-ready file

## Layout Options

| Option | Description |
|---|---|
| Columns / Rows | Controls how many labels fit per page |
| Barcode Type | Code 128 (default) or Code 39 |
| Show Serial Text | Prints the serial number below each barcode |
| Cell Borders | Adds light guide lines between labels |

## Serial Format

Serials must follow a **prefix + numeric suffix** pattern. Zero-padding is preserved automatically.

- ✅ `WHF1180286` → `WHF1180325` (40 serials)
- ✅ `ABC001` → `ABC050` (50 serials)
- ❌ Mismatched prefixes (`ABC001` → `XYZ010`)

Maximum range: 5,000 serials per run.

## Output

- **Letter size** (8.5 × 11 in), portrait orientation
- Barcodes rendered as **Code 128** or **Code 39** — scannable by standard warehouse and retail scanners
- PDF is generated entirely in-browser; nothing is uploaded or transmitted

## Dependencies (CDN)

- [JsBarcode](https://github.com/lindell/JsBarcode) — barcode rendering
- [jsPDF](https://github.com/parallax/jsPDF) — PDF generation
