# znayka
Reliable WS→SQLite pipeline: collector, parser, analyzer, gold extractor, verification, OCR, predictions.
# Znayka

**Reliable WS → SQLite pipeline** for collecting, parsing, analyzing and forecasting events.  
End-to-end workflow with verification and OCR.

## Components
- **01_collect.py** — WebSocket collector (4 streams, tokens via `.env`).
- **02_parse.py** — Parser: extracts ticks, detects rounds (T1/T2/pause/max).
- **03_analyze.py** — Analyzer: canonical rounds (quorum ≥2 sources).
- **04_extract_golds.py** — Gold extractor: coef ≥ 10, context 2h/5h/10h.
- **05_verify_external.py** — Verification via CSV/JSON or screenshots.
- **06_ocr_coef.py** — OCR (Tesseract) to extract coefficients from ROI.
- **07_predict.py** — Forecast engine: windows, digits, top-10, 6-minutes.
- **tail_all.py** — All coefficients in real-time.
- **tail_min_ru.py** — Minimal forecasts (minutes only, with history).

## Database
SQLite (WAL) with full schema:
- `raw_streams`, `ticks`, `rounds_raw`, `rounds`
- `golds`, `gold_context`
- `external_ref`, `verification`
- `predictions`, `outcomes`

## Quick start
```bash
sudo bash scripts/install.sh
cp .env.example .env
cp sources.json.example sources.json
bash scripts/demo.sh
