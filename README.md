# firmware-test-farm-mcp

An [MCP](https://modelcontextprotocol.io) server that lets an AI agent flash a compiled firmware binary onto a
**real, physical** embedded dev board, run it, and get back structured pass/fail results — serial output, crash
info, reset reason, timing — instead of a simulator or a description of what should happen.

This repo hosts the `server.json` manifest for the [MCP Registry](https://registry.modelcontextprotocol.io). The
server itself runs as a hosted, always-on remote endpoint — there's no package to install.

## Connecting

Sign up and create an API key from the dashboard, then point any MCP client that supports Streamable HTTP + a
bearer token at:

https://test-farm-17d99.web.app/mcp
Authorization: Bearer <your API key>



## Tools

- **`run_firmware_test`** — flashes the given firmware artifact onto a real board of the requested `board_type`
  and waits for a structured result (pass/fail, serial log excerpt, crash/reset info, timing). Every response
  includes live queue info (position, boards available, estimated wait) so an agent can decide whether to wait
  or come back later.
- **`get_upload_url`** — returns a short-lived signed URL to upload a firmware binary to before calling
  `run_firmware_test`.
- **`search_firmware_examples`** — searches a curated knowledge base of reference examples, known issues, and
  pinout/datasheet links for a given board type.

## Currently available boards

`heltec_wireless_tracker`, `arduino_giga_r1`, `xiao_nrf52840_plus`, `arduino_nicla_voice`,
`arduino_nano_33_ble`, `adafruit_feather_esp32_v2`, `seeed_grove_vision_ai_v2`, `raspberrypi_pico`

More board types are defined in the schema for future hardware; a submission for a `board_type` with no
physical board currently registered is rejected up front rather than left queued forever.

## Pricing

Every account starts on a free tier (50 firmware runs/month). Paid and Enterprise tiers are unlimited —
Enterprise additionally covers custom board types and custom motors/controllers/sensors outside the standard
fleet. See the dashboard for current usage and to request a tier change.
