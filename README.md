# ResumeEvaluator

ResumeEvaluator is an automated system that analyzes multiple resumes against a specific job description to rank candidates based on their role compatibility. The project uses Large Language Models (LLMs) to parse unstructured data, extract relevant professional criteria, and score candidates to identify the top two and bottom two matches.

## Overview

This project streamlines the initial resume screening process through a multi-step programmatic workflow:

1. Translates a raw job description into structured, predictable data fields.
2. Extracts key qualifications from various resume formats into a unified JSON schema.
3. Scores each resume directly against the job requirements.
4. Ranks the entire applicant pool to surface the strongest and weakest matches.

The primary objective is to eliminate manual review bottlenecks and establish a consistent baseline for candidate evaluation.

## How It Works

### 1. Job Description Parsing
The system processes the target job description using an LLM to generate a structured model. This model isolates critical hiring parameters, including:
* Job title and core role
* Required technical and soft skills
* Preferred or bonus qualifications
* Minimum years of experience
* Minimum education requirements
* Primary responsibilities

This structural baseline ensures that every resume is evaluated against identical criteria.

### 2. Resume Parsing
The application reads input files in PDF or DOCX formats and converts them to raw text. The LLM then extracts and normalizes the following data into a standardized schema:
* Contact details (Name, email, phone number)
* Total years of professional experience
* Documented technical skills
* Chronological work history (including internships)
* Educational background
* Academic or personal projects
* Certifications and licenses

### 3. Resume Scoring
The system compares each normalized resume against the structured job criteria. The evaluation model generates a specific match result containing:
* Overlapping skills that match the job profile
* Missing skills or noticeable qualification gaps
* Alignment between candidate experience level and job requirements
* An overall compatibility score from 0 to 100
* A brief qualitative summary justifying the score

### 4. Ranking Candidates
After evaluating all inputs, the system sorts the candidates by their numerical score and outputs:
* The top two highest-scoring candidates
* The bottom two lowest-scoring candidates
* Detailed match data and reasoning for both groups

## Project Structure

```text
ResumeEvaluator/
│
├── resumes/                 # Directory containing input PDF and DOCX resumes
├── evaluator.py             # Main execution script for parsing, scoring, and ranking
├── README.md                # Project documentation
└── job_description.txt      # Text file containing the target job description
```

## Technologies Used

* **Python**: Core programming language for application logic.
* **Groq LLM API**: Inference engine used for data extraction and candidate evaluation.
* **Pydantic**: Data validation library used to enforce structured schemas on LLM outputs.
* **PyPDF**: Library used to extract text from PDF files.
* **python-docx**: Library used to extract text from Word documents.
* **python-dotenv**: Configuration tool used to securely manage API keys.

## Output Example

The script executes via the terminal and prints the structured results in the following format:

```text
TOP 2 CANDIDATES

John Doe - 87%
{
  "matching_skills": ["Python", "Pydantic"],
  "missing_skills": ["Groq"],
  "verdict": "Strong technical alignment with required experience."
}

Jane Smith - 82%
{
  "matching_skills": ["Python", "PDF Extraction"],
  "missing_skills": ["Cloud Architecture"],
  "verdict": "Solid foundational experience, missing preferred qualifications."
}

LOWEST 2 CANDIDATES

Alex Kumar - 41%
{
  "matching_skills": ["Python"],
  "missing_skills": ["Data Modeling", "LLM Integration"],
  "verdict": "Candidate lacks the minimum required years of experience."
}

Ravi Patel - 38%
{
  "matching_skills": [],
  "missing_skills": ["Python", "Data Extraction"],
  "verdict": "Background does not align with the core requirements of this role."
}
```
