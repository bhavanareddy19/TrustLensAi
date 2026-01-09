# 🛡️ TrustLens AI - Intelligent Reddit Toxicity Analyzer

<div align="center">

![Version](https://img.shields.io/badge/version-0.2.0-blue.svg)
![Python](https://img.shields.io/badge/python-3.8+-green.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.115.0-009688.svg)
![Chrome](https://img.shields.io/badge/Chrome-Extension-yellow.svg)
![License](https://img.shields.io/badge/license-MIT-purple.svg)

**A privacy-first, AI-powered Chrome extension that analyzes Reddit comments in real-time to detect toxic content and verify evidence-based claims.**

[Features](#-key-features) • [Tech Stack](#-tech-stack) • [Installation](#-installation) • [Architecture](#-architecture) • [Development](#-for-developers)

</div>

---

## 📋 Overview

TrustLens AI is a full-stack application that combines machine learning, web scraping, and browser extension development to create a safer, more informed Reddit browsing experience. The system analyzes comments for toxicity levels and verifies URL-based evidence in real-time, providing users with visual indicators (color-coded badges) and detailed insights.

### 🎯 The Problem

Online discussions, especially on platforms like Reddit, often contain:
- **Toxic language** that can harm community discourse
- **Unverified claims** presented as facts
- **Misleading sources** without proper verification

### ✅ The Solution

TrustLens AI provides:
- **Real-time toxicity detection** using transformer-based ML models
- **Automated evidence verification** through DNS, HTTP, and content validation
- **Privacy-first architecture** - all analysis happens locally on your machine
- **Intuitive visual feedback** with color-coded badges and detailed tooltips

---

## ✨ Key Features

### 🔍 **Intelligent Toxicity Detection**
- Utilizes transformer-based neural networks for accurate toxicity classification
- Multi-dimensional analysis: toxic, severe_toxic, obscene, threat, insult, identity_hate
- Three-tier classification system:
  - 🔴 **Red** - Strong language (score ≥ 0.5)
  - 🟡 **Yellow** - Slightly strong language (score 0.3-0.5)
  - 🟢 **Green** - Positive tone (score < 0.3)

### 📊 **Evidence Verification System**
- Automatic URL extraction and validation from comments
- Multi-stage verification process:
  - DNS resolution checks
  - HTTP/HTTPS accessibility testing
  - Content-type validation
  - Domain authority assessment (.gov, .edu prioritization)
- Comprehensive evidence status: Verified, Unverified, Mixed, or None

### 🎨 **Smart Badge System**
- Visual color-coded indicators on Reddit comments
- Dynamic tooltips with detailed breakdown:
  - Content tone analysis
  - Evidence verification status
  - Source credibility information
- Non-intrusive UI that integrates seamlessly with Reddit

### 🔒 **Privacy & Security**
- **100% local processing** - no data sent to external servers
- Standalone backend server runs on `localhost`
- No personal information collection or storage
- Open-source and transparent

---

## 🛠️ Tech Stack

### **Frontend**
- **Chrome Extension** (Manifest V3)
- **JavaScript** (ES6+) - Content scripts, background workers
- **CSS3** - Custom styling for badges and tooltips
- **Chrome APIs** - Storage, Active Tab permissions

### **Backend**
- **Python 3.8+**
- **FastAPI** - High-performance async web framework
- **Uvicorn** - ASGI server
- **Transformers** (Hugging Face) - Pre-trained toxicity detection models
- **PyTorch** - Deep learning inference
- **HTTPX & Requests** - HTTP client for URL verification
- **BeautifulSoup4** - HTML parsing
- **TLDExtract** - Domain extraction and analysis

### **Machine Learning**
- **Transformer Models** - Fine-tuned toxicity classifiers
- **Multi-label Classification** - Simultaneous detection of multiple toxicity types
- **Confidence Scoring** - Probabilistic outputs for nuanced analysis

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         User's Browser                       │
│  ┌───────────────────────────────────────────────────────┐  │
│  │           TrustLens Chrome Extension                  │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌────────────┐  │  │
│  │  │ Content      │  │ Background   │  │  Popup UI  │  │  │
│  │  │ Scripts      │  │ Worker       │  │            │  │  │
│  │  └──────┬───────┘  └──────────────┘  └────────────┘  │  │
│  └─────────┼──────────────────────────────────────────────┘  │
└────────────┼──────────────────────────────────────────────────┘
             │ HTTP Requests (localhost:8000)
             ▼
┌─────────────────────────────────────────────────────────────┐
│                    FastAPI Backend Server                    │
│  ┌───────────────────────────────────────────────────────┐  │
│  │                    API Endpoints                       │  │
│  │  • /analyze-evidence - Main analysis endpoint         │  │
│  │  • /health - Server health check                      │  │
│  └───────────┬───────────────────────────────────────────┘  │
│              ▼                                               │
│  ┌───────────────────────┐  ┌─────────────────────────┐    │
│  │  Toxicity Analysis    │  │  Evidence Verification  │    │
│  │                       │  │                         │    │
│  │  • Transformer Model  │  │  • URL Extraction       │    │
│  │  • Score Calculation  │  │  • DNS Validation       │    │
│  │  • Color Mapping      │  │  • HTTP Checks          │    │
│  │                       │  │  • Domain Authority     │    │
│  └───────────────────────┘  └─────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

1. **Detection**: Extension monitors Reddit pages for comments
2. **Extraction**: Comment text extracted via DOM parsing
3. **Analysis**: Sent to local API endpoint `/analyze-evidence`
4. **ML Processing**: Toxicity model generates multi-dimensional scores
5. **Verification**: URLs extracted and verified through multi-stage validation
6. **Badge Assignment**: Combined toxicity + evidence analysis determines badge color
7. **Rendering**: Visual badges injected into Reddit UI with hover tooltips
8. **User Interaction**: Detailed statistics available via extension popup

---

## 🚀 Installation

### Prerequisites

- **Python 3.8+** ([Download here](https://www.python.org/downloads/))
  - ⚠️ During installation, check **"Add Python to PATH"**
- **Google Chrome** browser
- **Git** (optional, for cloning)

### Quick Start (3 Steps)

#### Step 1: Clone/Download the Repository

```bash
git clone https://github.com/YOUR_USERNAME/TrustLensAi.git
cd TrustLensAi
```

Or download as ZIP and extract.

#### Step 2: Start the Backend Server

**Windows:**
```bash
# Double-click START_TRUSTLENS.bat
# OR run in terminal:
START_TRUSTLENS.bat
```

**Mac/Linux:**
```bash
pip install -r requirements.txt
python launcher.py
```

Wait until you see: `Server will be available at: http://127.0.0.1:8000`

✅ Keep this terminal window open while using TrustLens

#### Step 3: Install Chrome Extension

1. Open Chrome and navigate to `chrome://extensions/`
2. Enable **Developer mode** (toggle in top-right)
3. Click **"Load unpacked"**
4. Select the `chrome-extension` folder from this project
5. TrustLens icon should appear in your extensions toolbar

### Verification

Visit any Reddit post (e.g., [r/AskReddit](https://www.reddit.com/r/AskReddit/)) and you should see colored badges appearing next to comments!

---

## 💡 Usage

### Basic Usage

1. **Browse Reddit** - Navigate to any Reddit post
2. **Observe Badges** - Comments automatically receive color-coded badges:
   - 🔴 Red = Toxic content
   - 🟡 Yellow = Mild toxicity or unverified claims
   - 🟢 Green = Positive tone with verified sources
3. **Hover for Details** - Mouse over badges to see:
   - Tone analysis
   - Evidence verification status
   - Source credibility
4. **View Statistics** - Click the TrustLens extension icon for aggregate stats

### Advanced Features

#### Custom Toxicity Thresholds
Modify `api/toxicity_model/app.py` lines 42-58 to adjust sensitivity:
```python
def _badge_color_for_row(row_probs: np.ndarray) -> str:
    toxic_score = float(row_probs[0])
    if toxic_score >= 0.5:  # Adjust this threshold
        return "red"
    elif toxic_score >= 0.3:  # And this one
        return "yellow"
    else:
        return "green"
```

#### Evidence Verification Rules
Configure trusted domains in `api/evidence.py` to prioritize specific sources.

---

## 🧪 Testing

### Automated Tests

```bash
# Run comprehensive test suite
python test_badge_logic.py

# Test specific scenarios
python test_single_word.py
```

### Test Coverage

- **20+ test scenarios** covering all toxicity × evidence combinations
- Automated validation of badge color logic
- URL verification edge cases (localhost, invalid domains, PDFs, etc.)

---

## 📁 Project Structure

```
TrustLensAi/
├── api/                          # Backend API server
│   ├── main.py                  # FastAPI application & endpoints
│   ├── evidence.py              # URL verification logic
│   ├── toxicity_model/          # ML model integration
│   │   └── app.py              # Toxicity classification
│   └── performance_logs/        # Performance monitoring
├── chrome-extension/            # Chrome extension files
│   ├── manifest.json           # Extension configuration (V3)
│   ├── content.js              # Reddit page injection
│   ├── trustlens-badges.js     # Badge rendering logic
│   ├── popup.html              # Extension popup UI
│   └── popup.js                # Popup statistics
├── artifacts/                   # Runtime data storage
├── launcher.py                  # Backend server launcher
├── requirements.txt             # Python dependencies
├── START_TRUSTLENS.bat         # Windows quick-start script
├── test_badge_logic.py         # Automated test suite
└── README.md                    # This file
```

---

## 👨‍💻 For Developers

### Development Setup

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run in development mode
cd api
uvicorn main:app --reload --port 8000
```

### API Documentation

Once the server is running, visit:
- **Interactive docs**: http://127.0.0.1:8000/docs
- **Alternative docs**: http://127.0.0.1:8000/redoc

### Key Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Server health check |
| `/analyze-evidence` | POST | Analyze comment for toxicity & evidence |

### API Request Example

```bash
curl -X POST "http://127.0.0.1:8000/analyze-evidence" \
  -H "Content-Type: application/json" \
  -d '{
    "comment_id": "test123",
    "text": "This is a sample comment with https://www.cdc.gov/ source"
  }'
```

### Response Format

```json
{
  "status": "Verified",
  "badge_color": "green",
  "toxicity_color": "green",
  "toxicity_scores": {
    "toxic": 0.12,
    "severe_toxic": 0.01,
    "obscene": 0.02,
    "threat": 0.00,
    "insult": 0.05,
    "identity_hate": 0.01
  },
  "evidence": {
    "urls": ["https://www.cdc.gov/"],
    "status": "Verified",
    "results": [...]
  }
}
```

---

## 🎓 Technical Highlights

### What Makes This Project Stand Out

1. **Full-Stack Development**
   - Seamless integration between Chrome extension frontend and Python backend
   - RESTful API design with FastAPI
   - Asynchronous processing for performance

2. **Machine Learning Integration**
   - Real-world application of transformer models
   - Multi-label text classification
   - Efficient model inference optimization

3. **Advanced Web Scraping & Validation**
   - Intelligent URL extraction with regex patterns
   - Multi-stage verification pipeline
   - Domain authority assessment

4. **Chrome Extension Expertise**
   - Manifest V3 compliance (latest standard)
   - Content script injection and DOM manipulation
   - Cross-origin resource handling

5. **Software Engineering Best Practices**
   - Comprehensive test coverage
   - Clear documentation and code comments
   - Modular architecture with separation of concerns
   - Error handling and logging

6. **Privacy-First Design**
   - Local-only processing
   - No external data transmission
   - Transparent and auditable code

---

## 🗺️ Future Roadmap

- [ ] **Multi-Platform Support** - Firefox and Edge extensions
- [ ] **Enhanced ML Models** - Fine-tuned models for Reddit-specific language
- [ ] **User Customization** - Adjustable sensitivity and filtering preferences
- [ ] **Comment Context Analysis** - Thread-aware toxicity detection
- [ ] **Reporting Dashboard** - Detailed analytics and trends
- [ ] **Community Features** - Shared blocklists and trusted source databases
- [ ] **Performance Optimization** - Caching and batch processing
- [ ] **Mobile Support** - React Native app for mobile Reddit

---

## 🐛 Troubleshooting

### Common Issues

**Backend won't start:**
- Ensure Python 3.8+ is installed and in PATH
- Check if port 8000 is available (close other applications using it)
- Try: `python -m pip install --upgrade pip` then reinstall requirements

**Extension not working:**
- Verify backend server is running (`http://127.0.0.1:8000/health`)
- Reload the extension in `chrome://extensions/`
- Check browser console for errors (F12 → Console tab)

**Badges not appearing:**
- Ensure you're on a Reddit post page (not homepage)
- Wait a few seconds for initial analysis
- Refresh the page

**CORS errors:**
- Restart the backend server
- Clear browser cache
- Check that API requests are going to `http://127.0.0.1:8000` (not `localhost`)

---

## 📊 Performance

- **Analysis Speed**: ~200-500ms per comment (including ML inference)
- **Memory Usage**: ~500MB (model loaded in memory)
- **Concurrent Processing**: Handles multiple comments in parallel
- **Cache Strategy**: Evidence verification results cached for 15 minutes

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Development Guidelines

- Follow PEP 8 style guide for Python code
- Use ESLint for JavaScript code
- Write tests for new features
- Update documentation as needed

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Your Name**

- GitHub: [@YOUR_USERNAME](https://github.com/YOUR_USERNAME)
- LinkedIn: [Your LinkedIn](https://linkedin.com/in/YOUR_PROFILE)
- Email: your.email@example.com

---

## 🙏 Acknowledgments

- **Hugging Face** - Pre-trained transformer models
- **FastAPI** - Modern, fast web framework
- **PyTorch** - Deep learning framework
- Reddit community for inspiration

---

## 📈 Project Stats

![GitHub stars](https://img.shields.io/github/stars/YOUR_USERNAME/TrustLensAi?style=social)
![GitHub forks](https://img.shields.io/github/forks/YOUR_USERNAME/TrustLensAi?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/YOUR_USERNAME/TrustLensAi?style=social)

---

<div align="center">

**Made with ❤️ for a safer internet**

[⬆ Back to Top](#️-trustlens-ai---intelligent-reddit-toxicity-analyzer)

</div>
