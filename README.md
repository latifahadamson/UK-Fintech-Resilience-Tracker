# 🇬🇧 UK Economic Resilience & FinTech Tracker

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://uk-fintech-resilience-tracker-kq3kvduv8xipdrgvddfwfq.streamlit.app/)
![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-Deployed-FF4B4B?logo=streamlit&logoColor=white)
![Data Source](https://img.shields.io/badge/Data%20Source-ONS%20API-004B87)
![Status](https://img.shields.io/badge/Status-Live-brightgreen)

A high-availability Python dashboard that tracks UK inflation (CPIH) data from the Office for National Statistics (ONS) and presents it as a real-time FinTech analytics interface. Built with resilience at its core, the system guarantees 100% uptime through an automated triple-tier data fallback architecture.

---

## 🔴 Live Demo

👉 **[View the Live Dashboard](https://uk-fintech-resilience-tracker-kq3kvduv8xipdrgvddfwfq.streamlit.app/)**

---

## 📌 Project Overview

This project bridges the gap between raw government economic data and actionable FinTech insights. It was designed to give analysts, policymakers, and FinTech professionals real-time visibility into UK inflation trends — while remaining fully operational even when external APIs are unstable or unavailable.

### Key Metrics Tracked
- **Current CPIH Inflation Rate** (Index)
- **Historical Peak Rate**
- **36-month Trend Analysis**
- **Data Source Status** (Live API vs Offline Cache)

---

## ⚙️ The Engineering Challenge

During development, two critical real-world obstacles were encountered and solved:

| Challenge | Solution |
|-----------|----------|
| ONS Beta API returning intermittent 500-series server errors | Automated fallback to stable, version-pinned API shards |
| SSL/TLS certificate verification failures on secure environments | Certifi-verified SSL handshakes integrated into all requests |

---

## 🏗️ Architecture: Triple-Tier Fallback Strategy

To guarantee 100% dashboard uptime, the pipeline implements a three-layer resilience model:

```
┌─────────────────────────────────────┐
│         Tier 1: Live API            │
│  ONS Beta API – Latest Observations │
│  (Real-time CPIH stream)            │
└────────────────┬────────────────────┘
                 │ FAILS?
                 ▼
┌─────────────────────────────────────┐
│       Tier 2: Versioned Shards      │
│  ONS Version-Pinned Stable API      │
│  (Version 104 – reliable fallback)  │
└────────────────┬────────────────────┘
                 │ FAILS?
                 ▼
┌─────────────────────────────────────┐
│       Tier 3: Offline Cache         │
│  Local Pandas-based static dataset  │
│  (Dashboard stays functional)       │
└─────────────────────────────────────┘
```

The active tier is displayed in the dashboard header, giving users full transparency on data source status.

---

## 🛠️ Technical Stack

| Component | Technology |
|-----------|------------|
| Language | Python 3.12 |
| Dashboard Framework | Streamlit |
| Data Handling | Pandas |
| HTTP Requests | Requests |
| SSL Security | Certifi |
| Data Source | ONS (Office for National Statistics) Beta API |
| Deployment | Streamlit Community Cloud |

---

## 🚀 Getting Started

### Prerequisites
- Python 3.8 or higher
- pip

### Installation & Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/latifahadamson/UK-Fintech-Resilience-Tracker.git
   cd UK-Fintech-Resilience-Tracker
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the app**
   ```bash
   streamlit run app.py
   ```

4. Open your browser and navigate to `http://localhost:8501`

---

## 📁 Project Structure

```
UK-Fintech-Resilience-Tracker/
│
├── app.py               # Main application — dashboard logic & fallback pipeline
├── requirements.txt     # Python dependencies
└── README.md            # Project documentation
```

---

## 📊 How It Works

1. On launch, the app attempts to fetch the latest CPIH observations from the **ONS Live API**
2. If the live stream returns an error, it automatically pivots to a **stable versioned endpoint** (Version 104)
3. If both API tiers fail, the dashboard renders from a **local Pandas cache** — ensuring the UI is never blank
4. The dashboard displays the current inflation index, historical peak, and a 36-month trend line chart
5. A status indicator informs the user whether they are viewing live or cached data

---

## 🔍 Data Source

All inflation data is sourced from the **[Office for National Statistics (ONS)](https://www.ons.gov.uk/)** — the UK's largest independent producer of official statistics.

- **Dataset:** CPIH (Consumer Prices Index including owner occupiers' Housing costs)
- **Geography:** United Kingdom (`K02000001`)
- **Aggregate:** `cpih1dim1A0` (All items)

---

## 🤝 Contributing

Contributions, suggestions, and feedback are welcome! Feel free to:
- Open an [Issue](https://github.com/latifahadamson/UK-Fintech-Resilience-Tracker/issues) to report bugs or suggest features
- Submit a Pull Request with improvements

---

## 👩‍💻 Author

**Latifah Adamson**
Business Analyst | Data & Digital Transformation Specialist


##License

This project is open source and available under the [MIT License](LICENSE).
