# LLM_Comparison_report
# ⚡ LLM Nexus - Enterprise Comparison Dashboard

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Streamlit](https://img.shields.io/badge/Streamlit-1.28+-red.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

**An intelligent platform for optimizing AI model selection across ChatGPT, Gemini, and LLaMA.**

[Features](#-features) • [Demo](#-demo) • [Installation](#-installation) • [Usage](#-usage) • [Configuration](#-configuration)

</div>

---

## 📋 Overview

LLM Nexus is an enterprise-grade comparison dashboard that helps teams make data-driven decisions when selecting AI models. Compare ChatGPT, Gemini, and LLaMA responses in real-time with automated performance tracking, cost analysis, and quality metrics.

### Why LLM Nexus?

- **⚡ Parallel Execution** - Query multiple models simultaneously, saving time
- **📊 Performance Metrics** - Track latency, cost, and response quality
- **🎯 Smart Routing** - Automatic model selection based on task type
- **🔄 Fallback System** - Automatic failover if primary model fails
- **📈 Analytics** - Comprehensive CSV reports for analysis
- **🔐 Secure** - User authentication and session management

---

## ✨ Features

### 🚀 Core Capabilities

| Feature | Description |
|---------|-------------|
| **Multi-Model Comparison** | Compare ChatGPT (GPT-4o-mini), Google Gemini, and Meta LLaMA side-by-side |
| **Concurrent Execution** | ThreadPoolExecutor for parallel API calls |
| **Intelligent Routing** | Auto-select optimal models based on task type (coding, speed, cost) |
| **Performance Tracking** | Real-time latency and response length metrics |
| **Automated Reporting** | Generate CSV reports with timestamps and model comparisons |
| **Fallback Mechanism** | Automatic failover: ChatGPT → Gemini → LLaMA |
| **User Authentication** | Secure login/register system with password hashing |
| **Modern UI** | Dark-themed, responsive Streamlit interface |

### 🎯 Task-Based Model Selection

```python
Task Type          →  Recommended Models
─────────────────────────────────────────
Coding             →  ChatGPT, LLaMA
Fast Response      →  Gemini, ChatGPT
Cost Saving        →  LLaMA, Gemini
General Purpose    →  All three models
```

---

## 🎥 Demo

![LLM Nexus Interface](https://via.placeholder.com/800x400?text=LLM+Nexus+Dashboard)

*Screenshot showing side-by-side comparison of model responses with performance metrics*

---

## 🛠️ Installation

### Prerequisites

- Python 3.8 or higher
- API Keys for:
  - OpenAI (ChatGPT)
  - Google Gemini
  - Hugging Face (LLaMA)

### Step 1: Clone the Repository

```bash
git clone https://github.com/Tejsai05/LLM_Comparison_report.git
cd LLM_Comparison_report
```

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

**Required packages:**
```txt
streamlit
openai
google-generativeai
huggingface_hub
python-dotenv
pandas
```

### Step 3: Configure Environment Variables

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here
HF_API_KEY=your_huggingface_api_key_here
```

### Step 4: Run the Application

```bash
streamlit run app.py
```

The app will open automatically at `http://localhost:8501`

---

## 📖 Usage

### 1. Authentication

First-time users need to register:
- Click the **Register** tab
- Choose a username and password (min 4 characters)
- Login with your credentials

### 2. Select Models

Choose which models to compare:
- **All Models** - ChatGPT, Gemini, LLaMA
- **Task-Specific** - Let the system recommend models based on task type

### 3. Enter Your Prompt

Type or paste your question/prompt in the text area.

### 4. Compare Results

Click **🚀 Run Comparison** to get:
- Side-by-side responses from each model
- Response time metrics
- Response length statistics
- Quality indicators

### 5. Export Reports

Download comparison results as CSV for further analysis.

---

## ⚙️ Configuration

### Model Settings (`config.py`)

Customize model parameters:

```python
MODEL_CONFIG = {
    "Chatgpt": {
        "cost": 0.002,      # Cost per request
        "speed": "medium",   # Expected speed
        "quality": "high"    # Output quality
    },
    "Gemini": {
        "cost": 0.0005,
        "speed": "fast",
        "quality": "medium"
    },
    "Llama": {
        "cost": 0.0,         # Free via HuggingFace
        "speed": "slow",
        "quality": "medium"
    }
}
```

### Fallback Order (`utils/fallback.py`)

Modify the fallback sequence:

```python
FALLBACK_ORDER = {
    "ChatGPT": ["Gemini", "llaMA"],  # If ChatGPT fails, try Gemini, then LLaMA
    "Gemini": ["llaMA"],              # If Gemini fails, try LLaMA
    "llaMA": []                       # No fallback for LLaMA
}
```

---

## 📁 Project Structure

```
LLM_Comparison_report/
│
├── app.py                      # Main Streamlit application
├── auth.py                     # User authentication system
├── config.py                   # Model configuration
│
├── models/                     # Model integration modules
│   ├── chatgpt_model.py       # OpenAI GPT integration
│   ├── gemini_model.py        # Google Gemini integration
│   └── llama_model.py         # HuggingFace LLaMA integration
│
├── utils/                      # Utility functions
│   ├── parallel.py            # Parallel execution logic
│   ├── router.py              # Task-based model routing
│   ├── fallback.py            # Fallback mechanism
│   ├── metrics.py             # Performance tracking
│   ├── report.py              # Report generation
│   └── rate_limiter.py        # API rate limiting
│
├── data/                       # Data storage
│   ├── users.csv              # User credentials
│   ├── metrics/               # Performance logs
│   └── comparision_reports/   # Generated reports
│
├── .env                        # Environment variables (not in repo)
├── requirements.txt            # Python dependencies
└── README.md                   # This file
```

---

## 🔧 API Integration Details

### ChatGPT (OpenAI)
```python
Model: gpt-4o-mini
Temperature: 0.7
Max Tokens: Default
```

### Gemini (Google)
```python
Model: gemini-pro
Temperature: 0.7
Max Output Tokens: 300
```

### LLaMA (HuggingFace)
```python
Model: meta-llama/Meta-Llama-3-8B-Instruct
Temperature: 0.7
Max Tokens: 300
```

---

## 📊 Performance Metrics

The system tracks the following metrics for each model:

| Metric | Description | Storage |
|--------|-------------|---------|
| **Latency** | Time taken to generate response (seconds) | `data/metrics/metrics.csv` |
| **Response Length** | Character count of the output | Logged per request |
| **Timestamp** | When the request was made | ISO format |
| **Model Name** | Which model generated the response | Stored with each entry |

### Viewing Metrics

Metrics are stored in `data/metrics/metrics.csv`:

```csv
model,latency,response_length,timestamp
ChatGPT,1.234,450,1708123456.789
Gemini,0.856,380,1708123457.234
LLaMA,2.145,420,1708123458.901
```

---

## 🔐 Security Features

- **Password Hashing**: SHA-256 encryption for user passwords
- **Session Management**: Streamlit session state for user sessions
- **API Key Protection**: Environment variables for sensitive credentials
- **File Locking**: Thread-safe CSV operations

---

## 🚀 Advanced Usage

### Custom Model Addition

To add a new model:

1. Create a new file in `models/` (e.g., `claude_model.py`)
2. Implement the response function:

```python
def claude_response(prompt: str) -> str:
    # Your implementation
    return response
```

3. Update `utils/parallel.py`:

```python
MODEL_FUNCTIONS = {
    "chatgpt": chatgpt_response,
    "gemini": gemini_response,
    "llama": llama_response,
    "claude": claude_response  # Add your model
}
```

4. Update `config.py` with model parameters

---

## 🐛 Troubleshooting

### Common Issues

**Issue**: `API Key not found`
```bash
Solution: Ensure .env file exists with correct API keys
```

**Issue**: `ModuleNotFoundError`
```bash
Solution: pip install -r requirements.txt
```

**Issue**: `Rate limit exceeded`
```bash
Solution: Implement rate limiting or upgrade API plan
```

**Issue**: `Model timeout`
```bash
Solution: Check internet connection and API service status
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guide
- Add docstrings to all functions
- Update README for new features
- Test thoroughly before submitting PR

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [OpenAI](https://openai.com/) for ChatGPT API
- [Google](https://ai.google.dev/) for Gemini API
- [Meta](https://ai.meta.com/) & [HuggingFace](https://huggingface.co/) for LLaMA access
- [Streamlit](https://streamlit.io/) for the amazing web framework

---

## 📧 Contact

**Tejsai05** - [@Tejsai05](https://github.com/Tejsai05)

Project Link: [https://github.com/Tejsai05/LLM_Comparison_report](https://github.com/Tejsai05/LLM_Comparison_report)

---

## 🗺️ Roadmap

- [ ] Add Claude and other LLM support
- [ ] Implement real-time cost tracking
- [ ] Add response quality scoring (BLEU, ROUGE)
- [ ] Create visualization dashboard for metrics
- [ ] Support for batch processing
- [ ] API endpoint for programmatic access
- [ ] Docker containerization
- [ ] Multi-language support

---

<div align="center">

**⭐ Star this repo if you find it useful!**

Made with ❤️ by [Tejsai05](https://github.com/Tejsai05)

</div>
