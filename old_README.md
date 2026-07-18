# ResumeEvaluator

ResumeEvaluator is an AI‑powered tool designed to automatically analyze a collection of resumes and determine how well each candidate aligns with a specific job description. It uses a Large Language Model (LLM) to extract relevant skills, experience, and keywords from both the resumes and the job posting, then ranks the candidates based on overall fit. 

## 🔍 What This Project Does

* **Directory Reading**: Scans all resumes stored in the project’s `resumes/` directory.
* **LLM Processing**: Analyzes a given job description using an advanced language model.
* **Candidate Evaluation**: Assesses each resume for relevance, skill match, and experience alignment.
* **Match Ranking**: Generates a sorted list of candidates based on overall qualification scores.
* **Extreme Filtering**: Automatically isolates the **top 2 resumes** and the **bottom 2 resumes** for quick screening.

## 🧠 How It Works

### 1. Resume Parsing
Each resume is loaded from the source folder and converted into structured, clean text for analysis.

### 2. Job Description Understanding
The LLM extracts core requirements, preferred skills, required years of experience, and role expectations from the posting.

### 3. Semantic Matching
Using embeddings or custom LLM scoring rules, each parsed resume is compared directly against the job requirements.

### 4. Ranking & Output
Resumes are scored, sorted, and a final evaluation report highlights the highest and lowest matching profiles.

## 🛠️ Tech Stack

* **Language**: Python 3.10+
* **Validation**: Pydantic v2 (for structured LLM outputs and config)
* **LLM Providers Supported**: OpenAI, Anthropic, Groq, OpenRouter

## 📦 Installation

Clone the repository and install the required dependencies:

```bash
# Clone the repository
git clone https://github.com
cd ResumeEvaluator

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate

# Install dependencies
pip install pydantic openai anthropic groq python-dotenv
```

## ⚙️ Configuration

Create a `.env` file in the root directory and add the API keys for the providers you plan to use:

```env
# Provider API Keys
OPENAI_API_KEY=your_openai_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here
GROQ_API_KEY=your_groq_key_here
OPENROUTER_API_KEY=your_openrouter_key_here

# Default Provider Settings
DEFAULT_LLM_PROVIDER=openai  # Options: openai, anthropic, groq, openrouter
DEFAULT_MODEL=gpt-4o
```

## 🚀 Usage

1. Place your target candidate resumes (PDF or TXT formats) into the `resumes/` directory.
2. Run the main evaluation script:

```bash
python main.py --provider groq --model llama3-70b-8192
```

### Example Implementation Snippet

```python
from pydantic import BaseModel, Field
from typing import List

class CandidateEvaluation(BaseModel):
    candidate_name: str
    overall_score: float = Field(..., description="Score from 0.0 to 10.0")
    matched_skills: List[str]
    missing_skills: List[str]
    fit_summary: str

# Your script will process resumes/ folder and yield structured Pydantic data
```
