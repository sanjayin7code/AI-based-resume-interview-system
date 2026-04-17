# 🤖 AI Resume Interview System
 
A multi-stage AI-powered interview simulator built with **Streamlit** and a **local LLM (Ollama + Phi-3)**. Upload your resume and a job description to go through a complete mock interview — Aptitude, Technical, and HR rounds — all generated dynamically based on your profile.
 
---
 
## ✨ Features
 
- 📄 **Resume + JD Upload** — Paste a job description and upload your resume to personalize the interview
- 🧠 **Aptitude Round** — 10 AI-generated MCQs covering logical reasoning, quantitative aptitude, verbal ability, and data interpretation
- 💻 **Technical Round** — 10 role-specific technical MCQs based on your resume and the job description (programming, CS concepts, databases)
- 🤝 **HR Round** — Behavioural questions to test your communication and soft skills
- ✅ **Automatic Evaluation** — Scores your MCQ answers and advances you through rounds
- 🔁 **Restart Anytime** — Reset and start a fresh interview session
---
 
## 🗂️ Project Structure
 
```
resume_reviewer_upmeta/
│
├── app.py                     # Main Streamlit app — controls all interview stages
├── demo.py                    # Quick test script for the LLM connection
├── requirements.txt           # Python dependencies
│
├── services/
│   ├── llm_service.py         # Calls local Ollama API (Phi-3 model)
│   ├── question_generator.py  # Generates MCQs via LLM prompts
│   └── evaluator.py           # Scores user answers against correct answers
│
├── pages/                     # (Reserved for future multi-page Streamlit expansion)
│   ├── aptitude.py
│   ├── technical.py
│   ├── hr.py
│   ├── review.py
│   └── result.py
│
├── prompts/                   # Prompt templates
│   ├── aptitude_prompt.txt
│   ├── technical_prompt.txt
│   ├── hr_prompt.txt
│   └── review_prompt.txt
│
└── utils/
    ├── resume_parser.py       # Resume parsing utilities
    ├── jd_parser.py           # Job description parsing utilities
    └── session_manager.py     # Streamlit session state helpers
```
 
---
 
## 🛠️ Tech Stack
 
| Layer        | Technology                  |
|--------------|-----------------------------|
| Frontend UI  | Streamlit                   |
| LLM Backend  | Ollama (local) + Phi-3 model |
| Language     | Python 3.10+                |
| API          | Ollama REST API (`localhost:11434`) |
 
---
 
## ⚙️ Prerequisites
 
1. **Python 3.10+**
2. **[Ollama](https://ollama.com/)** installed and running locally
3. **Phi-3 model** pulled in Ollama
---
 
## 🚀 Getting Started
 
### 1. Clone the repository
 
```bash
git clone https://github.com/your-username/resume-interview-system.git
cd resume-interview-system
```
 
### 2. Install dependencies
 
```bash
pip install -r requirements.txt
```
 
> If `requirements.txt` is empty, install manually:
> ```bash
> pip install streamlit requests
> ```
 
### 3. Start Ollama and pull the Phi-3 model
 
```bash
ollama serve
ollama pull phi3
```
 
### 4. Run the app
 
```bash
streamlit run app.py
```
 
Open your browser at `http://localhost:8501`
 
---
 
## 🧪 Test the LLM Connection
 
Before running the full app, you can verify your Ollama setup:
 
```bash
python demo.py
```
 
This sends a quick prompt to the LLM and prints the response to the console.
 
---
 
## 🎮 How It Works
 
```
Home → Upload Resume + JD
        ↓
  Aptitude Round (10 MCQs)
        ↓ pass (score ≥ 1)
  Technical Round (10 MCQs, resume-aware)
        ↓ pass (score ≥ 1)
  HR Round (3 open-ended questions)
        ↓ all answered
  🎉 Selected!   (or ❌ Better luck next time!)
```
 
- Each MCQ round is **dynamically generated** by the LLM based on the current context.
- Failing either the Aptitude or Technical round ends the session immediately.
- The HR round passes as long as all three fields are filled in.
---
 
## 🔧 Configuration
 
The LLM model and settings are configured in `services/llm_service.py`:
 
```python
{
    "model": "phi3",         # Change to any Ollama-supported model
    "stream": False,
    "options": {
        "temperature": 0.1   # Lower = more deterministic outputs
    }
}
```
 
To switch models (e.g., to `llama3` or `mistral`), pull the model via Ollama and update this file.
 
---
 
## 📌 Known Limitations
 
- Resume upload reads the file as plain text — works best with `.txt` resumes; PDF/DOCX parsing is not yet implemented.
- The passing threshold is set to `score >= 1`, meaning a single correct answer advances the candidate. Adjust in `app.py` as needed.
- Requires a locally running Ollama instance; no cloud LLM is used by default.
---
 
## 🤝 Contributing
 
Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.
 
---
 
## 📄 License
 
[MIT](LICENSE)
