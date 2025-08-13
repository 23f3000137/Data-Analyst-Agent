# 📊 Data Analyst Agent API

**Data Analyst Agent** is a Flask-based API that uses Python, Pandas, Matplotlib, and (optionally) an LLM to **source, prepare, analyze, and visualize any data** — from local files or scraped from the web.  
It is designed to work with automated evaluation systems where **`questions.txt`** and 0+ attached files are uploaded via a `POST` request, and the API returns answers **in the exact JSON format** specified in the question.

---

## 🚀 Features
- Accepts `questions.txt` and **any type of supporting data files** (CSV, Excel, JSON, Parquet, PNG, PDF, etc.)
- Reads and interprets questions to decide:
  - Whether to **scrape** data (e.g., Wikipedia highest-grossing films)
  - Whether to **analyze** uploaded datasets (e.g., correlation, regression)
  - Whether to **generate** visualizations (scatterplots, regression lines)
- Returns results **within 3 minutes** in valid JSON (array or object)
- Includes a **minimal HTML/CSS upload interface** for manual testing

---

## 📂 Project Structure
```
data_analyst_agent/
│
├── app.py              # Flask app (API + UI)
├── agent.py            # Core analysis engine
├── requirements.txt    # Python dependencies
├── templates/
│   └── index.html      # Upload UI
├── static/
│   └── style.css       # CSS styling
└── LICENSE             # MIT License
```

---

## ⚙️ Installation

1. **Clone this repository**
```bash
git clone https://github.com/23f3000137/Data-Analyst-Agent.git
cd data-analyst-agent
```

2. **Create a virtual environment**
```bash
python3 -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

---

## ▶️ Running Locally

### **Start the Flask app**
```bash
python app.py
```

By default, the app runs on:
```
http://127.0.0.1:5000/
```

---

## 📡 API Usage

### **Endpoint**
```
POST /api/
```

### **Request Example**
```bash
curl "http://127.0.0.1:5000/api/" \
  -F "questions.txt=@question.txt" \
  -F "data.csv=@data.csv" \
  -F "image.png=@chart.png"
```

- `questions.txt` (required) — contains one or more questions or a JSON template.
- Additional files are optional.

---

### **Response Example**
For array mode:
```json
[1, "Titanic", 0.485782, "data:image/png;base64,iVBORw0KG..."]
```

For object mode:
```json
{
  "Which high court disposed the most cases from 2019 - 2022?": "XYZ High Court",
  "What's the regression slope...": 3.21,
  "Plot the year...": "data:image/png;base64,..."
}
```

---

## 🌐 Web UI
You can manually test via the built-in upload form:
```
GET /
```
Upload `questions.txt` and other files, click **Submit**, and get JSON output in your browser or API client.

---

## 📦 Deployment
You can deploy this API anywhere:
- **Heroku**
- **Render**
- **Railway**
- **AWS / Azure / GCP**
- **ngrok** (for quick public testing)

Example (with gunicorn):
```bash
gunicorn app:app --bind 0.0.0.0:$PORT --timeout 300
```

---

## 📝 License
This project is licensed under the **MIT License** — you can use it freely for personal or commercial purposes.

---

## 📌 Notes
- Always return **valid JSON** within 3 minutes, even if you can't answer fully (partial credit).
- Keep base64 image responses **under 100 KB**.
- Use Pandas, DuckDB, and requests for efficient data analysis & web scraping.

---

## 💡 Next Steps
- Integrate with **Gemini or GPT** for natural language parsing of questions.
- Add support for **more visualization types**.
- Extend agent logic for **domain-specific datasets**.

---
