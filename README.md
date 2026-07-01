# ResumeAI — Personalized Resume Generator

Full-stack AI resume generator. Upload skill bank + master resume + JD → get ATS-optimized LaTeX.

## Stack
- **Backend**: FastAPI + Python
- **AI**: Groq API → llama-3.3-70b-versatile (free tier)
- **File parsing**: python-docx (DOCX) + PyMuPDF (PDF)
- **Frontend**: Vanilla HTML/CSS/JS (served by FastAPI)

## Setup

### 1. Install dependencies
```bash
pip install -r requirements.txt
```

### 2. Set Groq API Key (two options)

**Option A** — via .env file:
```bash
cp .env.example .env
# Edit .env and paste your key
GROQ_API_KEY=gsk_your_actual_key_here
```

**Option B** — Enter it directly in the web UI (no .env needed)

Get your free key at: https://console.groq.com

### 3. Run the server
```bash
python main.py
```

Or with uvicorn directly:
```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

### 4. Open browser
```
http://localhost:8000
```

## API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| GET | `/` | Web UI |
| GET | `/health` | Health check |
| POST | `/generate-resume` | Generate LaTeX resume |

### POST /generate-resume

**Form fields:**
| Field | Type | Required |
|-------|------|----------|
| `skill_bank` | File (.docx/.pdf) | ✅ |
| `master_resume` | File (.docx/.pdf) | ✅ |
| `job_description` | Text | ✅ |
| `groq_api_key` | Text | Optional (if set in .env) |

**Response:**
```json
{
  "success": true,
  "latex_code": "\\documentclass[letterpaper,11pt]{article}...",
  "stats": {
    "skill_bank_chars": 2500,
    "resume_chars": 3200,
    "latex_chars": 4800
  }
}
```

## Usage Flow

1. Upload your **Skill Bank** (.docx or .pdf) — list of all your skills/experience
2. Upload your **Master Resume** (.docx or .pdf) — reference for personal details
3. Paste the **Job Description** — full JD text
4. Enter your **Groq API key** (or set in .env)
5. Click **Generate Resume**
6. Copy the LaTeX code
7. Paste into [Overleaf](https://overleaf.com) → Compile → Download PDF

## File Structure

```
resume-generator/
├── main.py          # FastAPI backend
├── frontend.html    # Web UI (served at /)
├── requirements.txt
├── .env.example
└── README.md
```
