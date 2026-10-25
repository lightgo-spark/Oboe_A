# Oboe_A

<img width="1789" height="1041" alt="00 Oboe_A Dashboard" src="https://github.com/user-attachments/assets/f472ac4b-fe35-4258-b0ec-617bb8115db8" />

# 🚀 Oboe_A — Core Feature Guide (Quick Start)

> **A high-speed native runner to automate AI & data pipelines with just a simple JSON file — zero complex setup.**

---

## ⚡ 5 Essential Features

### 1. 🚀 One-Click Blazing-Fast Parallel Execution
- **Drag & Run**: Load your workflow JSON file and hit `▶ Run` or `⚡ Run All (Parallel)`.
- **16x Turbo Speed**: Independent tasks execute concurrently across up to 16 threads for dramatic speedups.
- **Simulation (Dry-run)**: Test and verify your workflow logic safely without calling real APIs or commands.

### 2. ⏰ 4 Smart Scheduling & Repeat Modes
- **🎯 Once at Time**: Waits until a specified clock time (e.g. `20:00:00`) and triggers automatically once.
- **🔄 Interval Repeat**: Runs repeatedly at your chosen cadence (every 10s, 1m, 5m, 1h, etc.) for N runs or infinitely.
- **📅 Daily at Time**: Runs every day at target times (e.g., market open `09:00`, close `15:30`, night report `20:00`), with Monday–Sunday weekday filters.
- **⚙ Cron Expression**: Supports standard 5-field Cron syntax (`0 20 * * *`) with a live 1-second countdown display.

### 3. 🔍 Intuitive Interactive Inspector
- **Instant Result Inspection**: Check task output data (XCom) instantly, with **one-click opening for generated PDF / CSV / JSON files**.
- **Single-Node Run (`▶`)**: Re-run and debug only a specific step while preserving existing upstream data.
- **Live In-Place Editing**: Modify Python code, prompts, or JSON parameters directly on screen and apply changes on the fly.
- **Terminal Logs & Profiler**: Search live console logs, copy errors, and view latency breakdown progress bars.

### 4. 🔔 Real-Time Telegram Phone Alerts
- Enter your Telegram Bot Token and Chat ID to receive instant pipeline completion reports directly on your phone.
- Easily choose whether to be notified only on failures or on every successful execution.

### 5. 🐍 Python (Airflow XCom Compatible) & REST APIs
- **Python**: Run scripts using familiar Airflow syntax like `ti.xcom_pull()` and `ti.xcom_push()`.
- **HTTP**: Fetch external REST API data with persistent connection pooling and feed it to downstream tasks.
- **LLM**: Connect AI prompts for summarization, data extraction, and report writing.
- **Silent Background Execution**: Runs cleanly in the background on Windows without annoying command prompt windows flashing.

---

## 💻 Quick Usage Guide

### 1) Desktop GUI Studio
Double-click the **`Oboe_A Studio`** shortcut on your Desktop to open the luxury frosted-glass studio.
- Easily toggle languages (`🌐 한국어 / ENG`) and luxury background themes (`🌌 Aurora / 💎 Obsidian / 🏛 Titanium`) at the top right.

### 2) Handy CLI Commands
```powershell
# 1. Run a workflow immediately
aiflow run my_flow.json

# 2. Schedule execution daily at 20:00:00
aiflow schedule my_flow.json --at "20:00:00"

# 3. Repeat 5 times at 10-minute intervals
aiflow schedule my_flow.json --interval 10m --repeat 5

# 4. View workflow DAG diagram
aiflow graph my_flow.json
```

---

## 📋 Supported Task Operators

| Operator (`op`) | Description | Example Configuration |
| :--- | :--- | :--- |
| **`python`** | Python script execution with XCom exchange | `"code": "data = ti.xcom_pull('step1')"` |
| **`http`** | REST API calls & web data collection | `"url": "https://api.site.com/data", "method": "GET"` |
| **`llm`** | Generative AI prompt reasoning & completion | `"prompt": "Summarize this data: {{ xcom.step1 }}"` |
| **`command`** | System shell command (runs silently) | `"command": "curl -O https://..."` |
| **`file_write`** | Saves generated text / reports to disk | `"path": "report.txt", "content": "{{ xcom.ai.text }}"` |
| **`branch`** | Conditional routing and task skipping | `"condition": "{{ status }} == 200"` |

---

## 📝 1-Minute Simple JSON Template

```json
{
  "name": "daily_briefing",
  "nodes": [
    {
      "id": "get_data",
      "op": "http",
      "params": {
        "url": "https://api.sample.com/today",
        "method": "GET"
      }
    },
    {
      "id": "ai_summary",
      "op": "llm",
      "depends_on": ["get_data"],
      "prompt": "Summarize the collected data: {{ xcom.get_data }}"
    },
    {
      "id": "save_file",
      "op": "file_write",
      "depends_on": ["ai_summary"],
      "params": {
        "path": "today_summary.txt",
        "content": "{{ xcom.ai_summary.text }}"
      }
    }
  ]
}
```

---
**Oboe_A Engine** — Lightweight, Fast, and Reliable Native AI Orchestration
