# Software (edge processor)

Python code that runs on the laptop acting as the turnstile's edge processor.

Planned modules:

| File | Purpose |
|---|---|
| `enroll.py` | Capture a face, build the 128-value SFace template, quantize to 8 bits, encrypt and write it to a card via the Arduino |
| `verify.py` | Compare a live face with a card template and return a similarity score |
| `gate_bridge.py` | Serial link with the Arduino: receive card data, send `OPEN` / `DENY` |
| `log_store.py` | SQLite travel log (card ID, station, time, decision, score, latency) |
| `alert_screen.py` | Minimal security-staff screen for repeated mismatches |

## Setup

```bash
pip install -r requirements.txt
```

Download the face models into `software/models/` (see that folder's README).
