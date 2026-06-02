# Exacta Packout Test Builder

A single-file, browser-based tool for building **ITEMSTATUS** packout messages for the Exacta packout pipeline. Configure one or more messages through a simple UI and copy the result straight into Postman, run it as a SQL insert, or grab the raw JSON.

**Live page:** [Exacta Packout Test Builder](https://derekshaheen.github.io/Useful-Dashboards/Bastian-Packout-Msg-Generator/exacta-packout.html)

## What it does

Each message card represents one ITEMSTATUS record. You set the container SSCC, location, packed quantity, and a list of serial numbers, and the tool assembles a correctly-shaped message. Add as many messages as you need; they're all combined into a single output payload.

## Output modes

The output panel has three tabs:

- **Postman** *(default)* — the full request body, wrapped as `{ "params": { "json": { "records": [ ... ] } } }`. All messages are combined into one `records` array, ready to paste into the request body in Postman.
- **SQL INSERT** — one `INSERT INTO t_alr_import_message` statement per message, each with its own GUID `host_group_id` and the JSON payload embedded in the `json` column.
- **JSON Only** — the raw record JSON for each message, without the Postman envelope.

The **Copy** button copies whatever the active tab shows.

## Fields

| Field | Description |
|-------|-------------|
| Outbound Container SSCC | The container SSCC. Used for **both** `order_id` and `outbound_container_id` — they are always identical. |
| Location | Maps to `location_id`. Defaults to `X`. |
| Packed Qty | Maps to `packed_qty`. Auto-syncs to the number of serials, or can be set manually. |
| Serial Numbers | One entry per serial; emitted as the `serial_numbers` array. |

Each record is emitted with fixed values `message_type: "ITEMSTATUS"`, `mode: "1"`, `line_item_id: 1`, and `state: "COMPLETED"`. The `timestamp` is generated at build time in `MMDDYYYYHHMMSS` format.

## Controls

- **+ Add Order Message** — add another message card.
- **Duplicate** — copy a message (with a fresh GUID).
- **Remove** — delete a message.
- **Sample Data** — load a couple of example messages.
- **Clear All** — reset to a single empty message.

## Usage

No build step or dependencies — it's a self-contained HTML file. Open it in a browser locally, or use the live page linked above. Fill in your messages, pick the Postman tab, and copy the body into your Postman request.

## Example output (Postman)

```json
{
    "params": {
        "json": {
            "records": [
                {
                    "message_type": "ITEMSTATUS",
                    "mode": "1",
                    "order_id": "00000509460507138549",
                    "line_item_id": 1,
                    "state": "COMPLETED",
                    "location_id": "X",
                    "outbound_container_id": "00000509460507138549",
                    "packed_qty": 2,
                    "timestamp": "05182026104413",
                    "serial_numbers": [
                        { "serial_number": "WF1234567" },
                        { "serial_number": "WF1234568" }
                    ]
                }
            ]
        }
    }
}
```