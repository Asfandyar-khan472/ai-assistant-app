# ai-assistant-app# 📄 ATS Resume Checker

A Streamlit app that scores a resume for **ATS (Applicant Tracking System) compatibility** and gives concrete, prioritised suggestions to improve it. Powered by **Google Gemini Flash**.

## Features

- Upload a resume as **PDF, DOCX or TXT**
- **ATS score (0-100)** with a 5-category breakdown
- Prioritised improvements (High / Medium / Low) with exact fixes
- Missing keywords, optionally matched against a **pasted job description**
- Before/after **rewrite examples** taken from your own resume
- Instant rule-based checks (email, phone, links, section headings, length, metrics)
- Downloadable Markdown report

## How the score works

The AI rates five categories from 0-100, and the **overall score is calculated in code** using fixed weights, so it is consistent and cannot be arbitrarily inflated by the model.

| Category | Weight |
|---|---|
| Contact Information | 10% |
| Structure & Formatting | 20% |
| Keywords & Skills | 25% |
| Experience & Impact | 30% |
| Readability & Language | 15% |

> The score is an **estimate**. Real ATS products (Workday, Greenhouse, Lever, Taleo...) differ, so treat it as guidance, not a guarantee.

## Project structure

```
.
├── app.py             # Streamlit app
├── requirements.txt   # Python dependencies
└── README.md
```

## Run locally

1. **Get a free Gemini API key:** https://aistudio.google.com/apikey
2. **Clone and install**
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. **Provide your API key** (pick one):
   - Environment variable:
     ```bash
     export GEMINI_API_KEY="your-key"      # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
     ```
   - Or create `.streamlit/secrets.toml`:
     ```toml
     GEMINI_API_KEY = "your-key"
     ```
   - Or just paste it into the sidebar when the app opens.
4. **Start the app**
   ```bash
   streamlit run app.py
   ```

## Configuration

| Setting | Where | Default |
|---|---|---|
| `GEMINI_API_KEY` | secrets / env var / sidebar | – |
| `GEMINI_MODEL` | secrets / env var / sidebar | `gemini-flash-latest` |

`gemini-flash-latest` is a Google alias that always points to the newest Flash model. If you prefer a pinned version, set `GEMINI_MODEL` to e.g. `gemini-2.5-flash`. The app automatically falls back to `gemini-2.5-flash` if the chosen model name is not found.

## Deploy on Streamlit Community Cloud

1. Push this project to a **GitHub** repository (never commit `.streamlit/secrets.toml`).
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app** → select your repo, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**. Your app will be live at `https://<your-app-name>.streamlit.app`.

## Troubleshooting

| Problem | Fix |
|---|---|
| "Very little text could be extracted" | The PDF is a scanned image or design-heavy. Export a text-based PDF/DOCX (an ATS can't read images either). |
| "API key was rejected" | Re-check the key and that the Gemini API is enabled for it. |
| Rate limit / quota message | Free tier has per-minute and per-day limits. Wait a minute or enable billing. |
| Model not found | Change the model in the sidebar to `gemini-flash-latest`. |

## Privacy

Resume text is sent to the Gemini API for analysis. The app does not store files or results on disk. Don't upload documents you aren't comfortable sending to a third-party API.

## License

MIT
