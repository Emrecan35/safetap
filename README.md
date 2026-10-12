# SafeTap

**Privacy-preserving facial verification for public transport turnstiles.**
The passenger's face template is stored on their own RFID card, not in a central database.
A bench-scale prototype built with Arduino and OpenCV for the İzmirim Kart use case.

> Course project — System Analysis and Design, Management Information Systems, İzmir Democracy University (2026–2027 Fall).
> Project code: **SAFE-TAP-26** · Author: **Emrecan Karaslan**

---

## How it works

1. **Enrollment:** the passenger looks at the camera once. A 128-value face template is extracted (OpenCV YuNet + SFace), compressed to 8-bit values, encrypted with AES and written to a MIFARE Classic 1K card. No photo is stored.
2. **Tap:** the card is tapped on the RC522 reader. The Arduino reads the encrypted template and sends it to the edge processor (laptop) over USB serial.
3. **Verify:** the edge processor captures the live face, compares it with the card template and returns `OPEN` or `DENY`.
4. **Gate:** on a match, the servo opens the gate, the green LED lights and the LCD greets the passenger. On a mismatch, the passenger gets a second attempt.
5. **Log and alert:** every decision is logged (card ID, station, time, decision, score, latency). A repeated mismatch sends a silent alert to the security screen.

```
 RFID card ──► RC522 ──► Arduino Uno ──USB serial──► Edge processor (laptop)
                         │  servo gate              │  camera + OpenCV
                         │  LCD, LEDs, buzzer       │  SQLite travel log
                         ◄────── OPEN / DENY ───────┘  security alert screen
```

In this prototype the comparison runs on the edge processor (**store-on-card**). In the target production design, the comparison moves into the card's secure element (**match-on-card**), so the template never leaves the card.

## Objectives

| ID | Objective | Target |
|---|---|---|
| OBJ-01 | Fast on-turnstile verification | Median < 500 ms, 95th percentile < 1 s |
| OBJ-02 | Reliable detection of mismatched card use | False acceptance < 1%, false rejection < 3% |

## Hardware

| Part | Role |
|---|---|
| Arduino Uno R3 (compatible) | Gate controller |
| RC522 RFID reader + MIFARE Classic 1K cards | Card reading and writing |
| SG90 micro servo | Gate arm |
| 16x2 LCD with I2C module | Passenger messages |
| Green/red LEDs, buzzer | Feedback |
| Laptop with webcam | Edge processor |

Wiring: see [`hardware/wiring.md`](hardware/wiring.md).

## Repository structure

```
safetap/
├── firmware/gate_controller/   Arduino sketch for the turnstile
├── software/                   Python: enrollment, verification, logging, alert screen
│   └── models/                 OpenCV face models (downloaded, not committed)
├── hardware/                   Wiring and parts list
├── tests/                      Benchmarks for OBJ-01 and OBJ-02
├── docs/
│   ├── report/                 Cumulative project report versions
│   └── diagrams/               UML, ERD, BPMN and architecture diagrams
└── data/                       Local test data (never committed)
```

## Roadmap

- [x] W02 – Problem definition and objectives (Section 1)
- [x] W03 – Project charter, feasibility, work plan and budget (Sections 2–3)
- [ ] W04 – Hardware ordered, consent form drafted
- [ ] W06 – Technical spike: template on card, end-to-end latency
- [ ] W07 – Analysis package completed
- [ ] W10 – Design package approved
- [ ] W12 – Working prototype demo (4 scenarios)
- [ ] W13 – Test results (LFW benchmark + volunteer sessions)
- [ ] W14 – Final report and presentation

## Privacy

- No raw face images are stored after enrollment; only encrypted templates on the cards.
- No central biometric database is created.
- Volunteer data is collected only with explicit written consent (KVKK) and deleted at the end of the semester.
- Nothing under `data/` is ever committed to this repository.

## Status

Analysis phase. Code will be added as the work packages progress.

## License

MIT — see [LICENSE](LICENSE).
