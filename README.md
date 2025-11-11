# CVLab - AI-Powered CV Tailoring

An intelligent CV optimization platform that uses GPT-4 to analyze job descriptions and tailor resumes with evidence-based precision.


https://cvlab.up.railway.app/



## What It Does

CVLab solves a common problem: matching your experience to job requirements without fabricating skills. It analyzes your CV, compares it to the job posting, and rewrites your resume to emphasize relevant experience using industry-standard terminology.

**Key Features:**
- 🎯 Evidence-based skill matching (never claims skills you don't have)
- 📄 Professional LaTeX PDF generation
- 📝 AI-generated cover letters tailored to each job
- 🔐 User authentication and credit system
- ⚡ Rate limiting and production-ready security

## How It Works

```
1. Upload CV (PDF) → Extract text
2. Paste job description → Parse requirements
3. AI analyzes skill gaps → Maps evidence
4. Rewrites CV → Emphasizes relevant experience
5. Compiles LaTeX → Professional PDF
```

## Tech Stack

- **Backend:** FastAPI, Python 3.9+
- **AI:** OpenAI GPT-4 (multi-stage pipeline)
- **Document Processing:** LaTeX/pdflatex, PyPDF2
- **Security:** JWT auth, SlowAPI rate limiting
- **Deployment:** Railway

## Installation

```bash
# Clone and install
git clone https://github.com/yourusername/cvlab.git
cd cvlab
pip install -r requirements.txt

# Set up environment
echo "OPENAI_API_KEY=your_key_here" > .env

# Install LaTeX (Ubuntu/Debian)
sudo apt-get install texlive-full

# Run
uvicorn main:app --reload --port 8000
```

## API Endpoints

### `POST /generate-cv`
Tailors CV to job description
- **Rate limit:** 25/minute
- **Input:** `job_description`, `user_cv`
- **Output:** LaTeX code + skills analysis report

### `POST /compile-latex`
Compiles LaTeX to PDF
- **Input:** `latex_code`
- **Output:** Base64-encoded PDF

### `POST /generate-cover-letter`
Creates tailored cover letter
- **Rate limit:** 20/minute
- **Input:** `job_description`, `user_cv`
- **Output:** Formatted cover letter text

### `POST /upload-cv`
Extracts text from PDF CV
- **Input:** PDF file
- **Output:** Extracted text

## The AI Pipeline

**3-Stage Processing:**

1. **Parse & Extract** - Converts CV and job description to structured JSON
2. **Skill Analysis** - Maps job requirements to CV evidence with confidence scores:
   - Explicit (keyword appears verbatim)
   - Implicit (demonstrated through experience)
   - Transferable (related skill)
   - Absent (no evidence)
3. **Intelligent Rewrite** - Integrates keywords naturally without fabrication

**Example:**
```
Job requires: "Agile methodology"
CV shows: "Weekly sprint reviews" + "iterative improvements"
Result: Rewrites as "Conducted weekly Agile sprint reviews..."
```

## Why This Approach Works

Traditional CV tools either:
- Use templates that don't match job requirements
- Keyword-stuff in obvious ways that ATS systems flag
- Fabricate skills the candidate doesn't have

CVLab only promotes real experience, just reframed using job-specific language.

## Deployment

```bash
# Railway configuration
uvicorn main:app --host 0.0.0.0 --port $PORT

# Required environment variables
OPENAI_API_KEY=<your_key>
DATABASE_URL=<postgresql_url>
JWT_SECRET=<random_secret>
```



---

Built to help job seekers present their best authentic selves.
