# 🇬🇧 UK Economic Resilience & FinTech Tracker

### **Project Overview**
This project is a high-availability data dashboard built to track United Kingdom inflation (CPIH) metrics. It bridges the gap between raw government data and actionable FinTech insights, providing real-time visibility into economic resilience.

### **The Challenge: Engineering for Reliability**
During development, the project faced two critical real-world engineering obstacles:
1. **Server Instability:** The primary ONS (Office for National Statistics) Beta API endpoint experienced intermittent 500-series internal server errors.
2. **Security Handshakes:** Navigating SSL/TLS certificate verification barriers common in secure macOS environments.

### **The Solution: A Hybrid Data Architecture**
To ensure 100% dashboard uptime, I implemented a **Triple-Tier Fallback Strategy**:
* **Tier 1 (Live API):** Attempts to fetch the absolute latest observations from the ONS live stream.
* **Tier 2 (Versioned Shards):** If the live stream fails, the pipeline automatically pivots to stable, version-pinned shards (Version 104).
* **Tier 3 (Offline Cache):** As a final fail-safe, the system utilizes a local Pandas-based data cache to ensure the UI remains functional regardless of external server status.

### **Technical Stack**
* **Language:** Python 3.12
* **Interface:** Streamlit
* **Data Handling:** Pandas & Requests
* **Security:** Certifi-verified SSL handshakes

### **How to Run**
1. Clone the repository: `git clone https://github.com/latifahadamson/uk-fintech-resilience-tracker.git`
2. Install dependencies: `pip install streamlit pandas requests certifi`
3. Launch the app: `streamlit run app.py`
