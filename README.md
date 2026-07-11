# 🚀 AI Resume Scorer & Analyzer (ATS)

🔗 **Live Project Link:** [https://streamlit.app](https://streamlit.app)

This is a web application that acts like an Applicant Tracking System (ATS). It helps users upload their resume (as a PDF or Word document), paste a job description, and get an instant match score. The app uses AI to find gaps in the resume, suggest improvements, and let the user download the final feedback as a clean PDF report.

The project is split into two main parts:
1. **Backend (FastAPI):** Handles the heavy lifting—extracting text from files, talking to the AI, and generating PDF reports.
2. **Frontend (Streamlit):** The user interface where people log in, upload files, and see their dashboard metrics.

---

## 🛠️ Tools & Technologies Used

- **Frontend Interface:** [Streamlit](https://streamlit.io) — Used for building the interactive web pages and upload forms quickly.
- **Backend API:** [FastAPI](https://tiangolo.com) + [Uvicorn](https://uvicorn.org) — Keeps the server running fast and handles requests.
- **Database & Authentication:** [Supabase](https://supabase.com) — Handles user accounts, Gmail sign-in, and saves user history.
- **AI Engine:** [Groq API](https://groq.com) (Llama 3.3 model) — Reads the text and gives smart feedback instantly.
- **File Readers:** `pypdf` and `python-docx` — Reads text from PDF and Word files.
- **PDF Creator:** [WeasyPrint](https://weasyprint.org) — Converts HTML layouts into downloadable PDF files.

---

## 📂 Project Structure

```text
ATS_scorer/
├── backend/                  # The server side (FastAPI)
│   ├── api/                  # Login and routing code
│   ├── core/                 # App configurations and settings
│   ├── database/             # Connecting to Supabase
│   ├── models/               # Data structure templates
│   ├── services/             # Code for parsing files, Groq AI, and PDF making
│   ├── templates/            # HTML templates for the PDF layout
│   ├── utils/                # Helper functions for handling files
│   └── main.py               # The main file that starts the server
│
├── frontend/                 # The website side (Streamlit)
│   ├── .streamlit/           # App themes and secret keys settings
│   ├── assets/               # Custom CSS styles
│   ├── components/           # UI pieces (score bars, feedback grids)
│   ├── services/             # Code that talks to the backend API and Supabase
│   ├── views/                # Individual dashboard pages
│   └── streamlit_app.py      # The main file that starts the frontend website
│
└── .gitignore                # Tells Git to hide password files from GitHub
```

---

## 🚀 How to Setup and Run This Project Locally

### 1. Clone the project from GitHub
```bash
git clone https://github.com
cd ATS_SCORER
```

### 2. Setup the Backend Server
Go inside the backend folder, create a virtual environment to keep packages isolated, and install the requirements:
```bash
cd backend
python -m venv myenv

# Turn on the virtual environment (Windows):
.\myenv\Scripts\activate
# Turn on the virtual environment (Mac/Linux): source myenv/bin/activate

pip install -r requirements.txt
```

Create a file named `.env` inside the `backend/` folder and add your secret keys:
```env
SUPABASE_URL="https://supabase.co"
SUPABASE_ANON_KEY="your_supabase_public_anon_key"
SUPABASE_JWT_SECRET="your_supabase_jwt_secret"
GROQ_API_KEY="your_groq_api_key"
GROQ_MODEL="llama-3.3-70b-versatile"
HF_TOKEN="your_huggingface_read_token"
```
*(Note: Make sure your computer has `libmagic` and `GTK3 Runtime` installed for file reading and PDF generation to work on Windows/Mac).*

Start the backend server:
```bash
uvicorn main:app --reload
```

### 3. Setup the Frontend Website
Open a second terminal window, navigate to the frontend folder, and configure it:
```bash
cd ../frontend
```

Make sure your configuration is saved inside `.streamlit/secrets.toml`:
```toml
[connections.supabase]
SUPABASE_URL = "https://supabase.co"
SUPABASE_KEY = "your_supabase_public_anon_key"
```

Start the frontend website:
```bash
streamlit run streamlit_app.py
```

---

## 🔒 Security Note

Your secret database keys, API codes, and local virtual folders (`myenv/`) are written down in the `.gitignore` file. This ensures they stay safely on your computer and are never uploaded publicly to GitHub.
