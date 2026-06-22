
# CyberSentinel — Hybrid Intrusion Detection System

An offline hybrid network forensic and threat detection system designed to maximize classification accuracy and minimize false positives by combining **deterministic rule-based detection** with **statistical machine learning**.

---

## How It Works

CyberSentinel runs two detection layers in parallel. A threat is flagged if **either** layer catches it — maximizing recall and minimizing missed attacks.

### Layer 1 : Signature-Based (Deterministic)
Acts as a classic IDS. Instantly flags known malicious patterns from NSL-KDD attributes with manually defined thresholds:

| Rule | Attack Type |
|------|-------------|
| `src_bytes > 99th percentile` | DDoS / data exfiltration |
| `dst_host_count > 250` | Port sweep (Probe) |
| `serror_rate > 0.8` | SYN flood (DoS) |
| `root_shell = 1` | Root access gained (U2R) |
| `num_failed_logins > 0` | Brute force attempt (R2L) |

Minimal compute required — deterministic and instant.

### Layer 2 : Anomaly-Based (Isolation Forest / ML)
Trains only on **normal traffic** to learn what "normal" looks like. Any packet that deviates from that profile is flagged — catching zero-day attacks and novel patterns that rules alone would miss.

### Combined Result
```
Flagged by Layer 1 OR Layer 2 → Threat
Both layers clear → Normal
```
Two independent layers = higher recall, fewer missed attacks.

---

## Dataset

Trained and evaluated on the **NSL-KDD benchmark dataset** (KDDTrain+ / KDDTest+) — an industry-standard dataset for network intrusion detection research covering DoS, Probe, R2L, and U2R attack categories.

---

## Use Cases

**Live log monitoring** — connect to a live data stream to flag malicious behaviour and send real-time alerts.

**Static log forensics** — process historical traffic logs in batch to uncover advanced persistent threats (APTs), hidden data exfiltration, or breaches that bypassed initial defenses.

**Digital forensics & incident response** — reconstruct full attack timelines, isolate attacker behaviour, preserve digital evidence, and give IR teams visibility far beyond basic alerts.

**Web application security** — maps directly onto HTTP/SMTP/FTP environments to detect backend DoS flooding or reconnaissance scripts probing web APIs.

---

## Tech Stack

- **Language:** Python
- **ML Model:** Isolation Forest (scikit-learn)
- **Dataset:** NSL-KDD (KDDTrain+ / KDDTest+)

---

## Getting Started

```bash
git clone https://github.com/AaminaBinteArif/CyberSentinel.git
cd CyberSentinel
pip install -r requirements.txt
python main.py
```

---

## Author

**Aamina Binte Arif**  
