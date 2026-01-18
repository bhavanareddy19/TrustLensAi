<div align="center">

# 🔍 TrustLens AI

### Real-Time Toxicity Detection & Source Credibility Analysis System

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org)
[![Hugging Face](https://img.shields.io/badge/HuggingFace-Transformers-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co)
[![Chrome Extension](https://img.shields.io/badge/Chrome-Extension%20V3-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white)](https://developer.chrome.com/docs/extensions/mv3/)

<p align="center">
  <img src="https://img.shields.io/badge/NLP-BERT%20Model-blue?style=flat-square" alt="NLP"/>
  <img src="https://img.shields.io/badge/API-RESTful-green?style=flat-square" alt="API"/>
  <img src="https://img.shields.io/badge/Processing-Real%20Time-orange?style=flat-square" alt="Real-time"/>
  <img src="https://img.shields.io/badge/Privacy-Local%20Only-purple?style=flat-square" alt="Privacy"/>
</p>

---

**An end-to-end ML pipeline that analyzes Reddit comments in real-time, detecting toxic content using BERT-based NLP and verifying source credibility through automated web scraping & DNS validation.**

[Features](#-key-features) • [Tech Stack](#-tech-stack) • [Architecture](#-system-architecture) • [Installation](#-quick-start) • [API Reference](#-api-endpoints)

</div>

---

## 🎯 Project Highlights

<table>
<tr>
<td width="50%">

### 🤖 AI/ML Engineering
- **BERT-based toxicity classification** using HuggingFace Transformers
- Multi-label classification (6 toxicity categories)
- GPU-accelerated inference with CUDA support
- Thread-safe lazy model loading
- Real-time prediction pipeline

</td>
<td width="50%">

### 📊 Data Engineering
- **ETL pipeline** for Reddit JSON data extraction
- Async API with FastAPI + Uvicorn (ASGI)
- Concurrent request handling (5 workers)
- Performance monitoring & metrics logging
- Automated data persistence to JSON artifacts

</td>
</tr>
<tr>
<td width="50%">

### 🔬 Data Science
- **NLP preprocessing** with tokenization & encoding
- Probability score analysis & threshold tuning
- Pattern recognition for evidence detection
- Statistical metrics tracking
- Model output interpretation

</td>
<td width="50%">

### 📈 Data Analysis
- **Real-time analytics dashboard**
- Latency tracking & throughput metrics
- Success rate calculations
- Session-based performance reports
- Structured JSON logging for analysis

</td>
</tr>
</table>

---

## 🛠 Tech Stack

<div align="center">

### Backend & AI/ML

| Technology | Purpose | Why It Matters |
|:----------:|:--------|:---------------|
| ![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white) | Core Language | Industry standard for ML/Data Engineering |
| ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) | API Framework | Modern async, auto-docs, type hints |
| ![PyTorch](https://img.shields.io/badge/-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) | Deep Learning | GPU acceleration, production-ready |
| ![HuggingFace](https://img.shields.io/badge/-Transformers-FFD21E?style=flat-square&logo=huggingface&logoColor=black) | NLP Models | Pre-trained BERT, easy deployment |
| ![Pydantic](https://img.shields.io/badge/-Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white) | Data Validation | Type-safe request/response handling |

### Data Processing & Web

| Technology | Purpose | Why It Matters |
|:----------:|:--------|:---------------|
| ![BeautifulSoup](https://img.shields.io/badge/-BeautifulSoup-43B02A?style=flat-square&logo=python&logoColor=white) | Web Scraping | HTML parsing for credibility checks |
| ![HTTPX](https://img.shields.io/badge/-HTTPX-2D3748?style=flat-square&logo=python&logoColor=white) | Async HTTP | Non-blocking API requests |
| ![Uvicorn](https://img.shields.io/badge/-Uvicorn-499848?style=flat-square&logo=gunicorn&logoColor=white) | ASGI Server | High-performance async serving |
| ![JSON](https://img.shields.io/badge/-JSON-000000?style=flat-square&logo=json&logoColor=white) | Data Format | Structured logging & artifacts |

### Frontend & Extension

| Technology | Purpose | Why It Matters |
|:----------:|:--------|:---------------|
| ![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) | Extension Logic | Chrome Extension development |
| ![Chrome](https://img.shields.io/badge/-Manifest%20V3-4285F4?style=flat-square&logo=googlechrome&logoColor=white) | Extension Format | Latest security standards |
| ![HTML5](https://img.shields.io/badge/-HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) | Popup UI | Extension interface |
| ![CSS3](https://img.shields.io/badge/-CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) | Styling | Badge & sidebar design |

</div>

---

## ⚡ Key Features

### 🔴🟡🟢 Three-Tier Badge System

```
┌─────────────────────────────────────────────────────────────────────┐
│                    BADGE CLASSIFICATION LOGIC                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   🔴 RED (Toxic)     →  Toxicity Score ≥ 0.7 (any category)        │
│   🟡 YELLOW (Mild)   →  Toxicity Score 0.3-0.7 OR unverified src   │
│   🟢 GREEN (Safe)    →  Toxicity Score < 0.3 AND verified sources  │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### 🧠 Multi-Label Toxicity Detection

The BERT model (`unitary/toxic-bert`) classifies comments across **6 categories**:

```python
categories = [
    "toxic",          # General toxicity
    "severe_toxic",   # Extreme harmful content
    "obscene",        # Profanity & vulgarity
    "threat",         # Threatening language
    "insult",         # Personal attacks
    "identity_hate"   # Discrimination
]
```

### 🔗 Source Credibility Verification

```
Comment with URL → Extract URLs → DNS Resolution → Public IP Validation
                                        ↓
                   Page Classification ← HTTP Reachability Check
                          ↓
        [news | government | education | blog | docs | social]
                          ↓
                  Credibility Score
```

**Verification Pipeline:**
- **DNS Resolution** with IDNA encoding support
- **Public IP Validation** (blocks private/loopback IPs)
- **SSL/TLS Certificate** verification
- **Content-Type** detection
- **Page Classification** via JSON-LD, OpenGraph, TLD analysis

---

## 🏗 System Architecture

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                              TRUSTLENS ARCHITECTURE                           │
└──────────────────────────────────────────────────────────────────────────────┘

┌─────────────────┐     ┌─────────────────┐     ┌─────────────────────────────┐
│   REDDIT.COM    │────▶│ CHROME EXTENSION│────▶│     FASTAPI BACKEND         │
│                 │     │   (Manifest V3)  │     │    http://127.0.0.1:8000    │
└─────────────────┘     └─────────────────┘     └─────────────────────────────┘
                               │                              │
                               │  POST /ingest                │
                               │  POST /analyze-evidence      │
                               ▼                              ▼
                        ┌─────────────────────────────────────────────────────┐
                        │                  PROCESSING PIPELINE                 │
                        ├─────────────────────────────────────────────────────┤
                        │                                                      │
                        │  ┌──────────────┐    ┌──────────────────────────┐   │
                        │  │   EXTRACT    │───▶│   TOXICITY PREDICTION    │   │
                        │  │   COMMENTS   │    │   (toxic-bert model)     │   │
                        │  └──────────────┘    └──────────────────────────┘   │
                        │         │                       │                    │
                        │         ▼                       ▼                    │
                        │  ┌──────────────┐    ┌──────────────────────────┐   │
                        │  │   EVIDENCE   │───▶│    BADGE FUSION LOGIC    │   │
                        │  │   ANALYSIS   │    │   (TL1 + TL2 + TL3)      │   │
                        │  └──────────────┘    └──────────────────────────┘   │
                        │                                 │                    │
                        │                                 ▼                    │
                        │                      ┌──────────────────────┐       │
                        │                      │   OUTPUT FORMATTER   │       │
                        │                      │   (JSON artifacts)   │       │
                        │                      └──────────────────────┘       │
                        │                                                      │
                        └─────────────────────────────────────────────────────┘
                                               │
                                               ▼
                        ┌─────────────────────────────────────────────────────┐
                        │              PERFORMANCE MONITORING                  │
                        ├─────────────────────────────────────────────────────┤
                        │  • Latency tracking (pattern, URL, verification)    │
                        │  • Throughput metrics (comments/sec)                │
                        │  • Success rate calculations                        │
                        │  • JSON logging to /performance_logs                │
                        └─────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
TrustLens_AI/
│
├── 🐍 api/                           # Backend Server
│   ├── main.py                       # FastAPI app & endpoints
│   ├── toxicity_model/
│   │   ├── app.py                    # Prediction endpoint & badge logic
│   │   ├── base.py                   # Abstract BaseAdapter class
│   │   └── toxicity_adapter.py       # BERT model inference
│   ├── evidence.py                   # URL extraction & verification
│   ├── evidence_monitored.py         # Performance-wrapped evidence
│   ├── extract_pure_comments.py      # Recursive comment parser
│   ├── output_formatter.py           # Structured output (TL1/TL2/TL3)
│   ├── performance_monitor.py        # Metrics tracking system
│   └── performance_logs/             # Auto-generated metrics
│
├── 🌐 chrome-extension/              # Chrome Extension (Manifest V3)
│   ├── manifest.json                 # Extension configuration
│   ├── content.js                    # Reddit detection & analysis
│   ├── trustlens-badges.js           # Badge rendering & UI
│   ├── popup.html/js                 # Extension popup
│   └── background.js                 # Service worker
│
├── 📊 artifacts/                     # Analysis output files
│   └── toxicity_output_*.json        # Per-post analysis results
│
├── 🚀 START_TRUSTLENS.bat            # One-click Windows launcher
├── 📋 requirements.txt               # Python dependencies
└── 📖 README.md                      # Documentation
```

---

## 📡 API Endpoints

<div align="center">

| Endpoint | Method | Description |
|:---------|:------:|:------------|
| `/health` | `GET` | Server health check |
| `/ingest` | `POST` | Analyze entire Reddit post |
| `/predict` | `POST` | Toxicity prediction only |
| `/analyze-evidence` | `POST` | Evidence + toxicity fusion |
| `/performance` | `GET` | Real-time metrics |
| `/performance/reset` | `POST` | Reset session metrics |

</div>

### Example Request

```bash
# Analyze a comment for toxicity and evidence
curl -X POST "http://127.0.0.1:8000/analyze-evidence" \
     -H "Content-Type: application/json" \
     -d '{"text": "According to this study https://nature.com/article, the results show..."}'
```

### Example Response

```json
{
  "status": "verified",
  "badge_color": "green",
  "toxicity_color": "green",
  "evidence": {
    "has_evidence": true,
    "verified_sources": ["nature.com"],
    "page_type": "academic"
  },
  "TL2_tooltip": "Balanced tone with verified academic source",
  "TL3_detail": {
    "urls_found": 1,
    "urls_verified": 1,
    "credibility_score": 0.95
  }
}
```

---

## 📊 Performance Metrics

The system tracks real-time performance metrics:

```
┌─────────────────────────────────────────────────────────────────┐
│                    PERFORMANCE DASHBOARD                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  📈 Throughput:           2.73 comments/sec                     │
│  ⏱️  Avg Latency:          45.2ms per comment                    │
│  ✅ Verification Rate:    65.7% URLs reachable                  │
│  🔄 Total Processed:      342 comments                          │
│                                                                  │
│  Operation Breakdown:                                            │
│  ├── Pattern Detection:   2.3ms avg                             │
│  ├── URL Extraction:      5.1ms avg                             │
│  ├── URL Verification:    38.2ms avg                            │
│  └── Badge Fusion:        1.2ms avg                             │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites

- **Python 3.8+** ([Download](https://www.python.org/downloads/))
- **Google Chrome** browser
- ~2GB RAM (for ML model)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/TrustLens_AI.git
cd TrustLens_AI

# 2. Install dependencies
pip install -r requirements.txt

# 3. Start the backend server
python launcher.py
# OR double-click START_TRUSTLENS.bat (Windows)
```

### Chrome Extension Setup

1. Open `chrome://extensions/`
2. Enable **Developer mode** (top-right toggle)
3. Click **Load unpacked**
4. Select the `chrome-extension/` folder
5. Visit any Reddit post to see TrustLens in action!

---

## 🧪 Model Details

### Toxic-BERT Architecture

```
Input Text
    │
    ▼
┌─────────────────────────────────────┐
│         BERT TOKENIZER              │
│   (max_length=128, truncation)      │
└─────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────┐
│      BERT ENCODER (12 layers)       │
│   Hidden Size: 768                  │
│   Attention Heads: 12               │
└─────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────┐
│      CLASSIFICATION HEAD            │
│   Output: 6 sigmoid probabilities   │
└─────────────────────────────────────┘
    │
    ▼
[toxic, severe_toxic, obscene, threat, insult, identity_hate]
```

**Device Support:**
- Auto-detects CUDA GPU for acceleration
- Fallback to CPU if GPU unavailable
- Thread-safe lazy loading with mutex locks

---

## 🔒 Privacy & Security

| Feature | Implementation |
|:--------|:---------------|
| **Local Processing** | All analysis runs on your machine |
| **No External APIs** | No data sent to third-party servers |
| **No Data Collection** | Zero telemetry or tracking |
| **Localhost Only** | Server binds to 127.0.0.1 |
| **Private IP Blocking** | Prevents SSRF attacks |

---

## 🎓 Skills Demonstrated

<div align="center">

### For Data Analyst Roles
`Data Processing` `Metrics Analysis` `JSON/ETL Pipelines` `Performance Dashboards` `Statistical Analysis`

### For Data Scientist Roles
`NLP/Text Classification` `BERT/Transformers` `Model Inference` `Feature Engineering` `Probability Analysis`

### For Data Engineer Roles
`FastAPI/REST APIs` `Async Programming` `ETL Pipelines` `Performance Monitoring` `Data Validation`

### For AI Engineer Roles
`PyTorch/Deep Learning` `HuggingFace Transformers` `Model Deployment` `GPU Optimization` `Real-time ML Systems`

</div>

---

## 📫 Connect With Me

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/bhavanareddy19/)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-000000?style=for-the-badge&logo=vercel)](https://bhavana19portfolio.netlify.app/)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail)](mailto:Bhavana.Vippala@colorado.edu)

</div>

---

<div align="center">

### ⭐ Star this repository if you found it helpful!

**Built with passion for AI/ML and Data Engineering**

</div>

---

<div align="center">
<sub>Made with ❤️ using Python, FastAPI, PyTorch & HuggingFace Transformers</sub>
</div>
