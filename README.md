# AI Recruiting System

An intelligent, multi-agent recruitment system where AI agents (Jack & Jill) collaborate to match candidates with jobs.

## 🤖 The Agents

### 1. **JACK** (Candidate Agent)
- **Role:** Talent Advocate
- **Action:** Voice interviews with candidates to build comprehensive profiles
- **Output:** Candidate Profile (saved to database)

### 2. **JILL** (Hiring Manager Agent)
- **Role:** Talent Acquisition Partner
- **Action:** Voice interviews with hiring managers to understand roles
- **Output:** Job Specification (saved to database)

---

## 🚀 Setup

1. **Install dependencies:**
```bash
pip install -r requirements.txt
```

2. **Get your FREE Groq API key:**
   - Visit https://console.groq.com/
   - Sign up (free)
   - Create an API key
   
3. **Create `.env` file:**
```
GROQ_API_KEY=your_groq_api_key_here
```

---

## 📋 Scripts & Execution Order

### **STEP 1: Data Collection**
Run these scripts to populate your database with candidates and jobs.

#### Option A: Interview a Candidate
```bash
python jack_agent.py
```
- **What it does:** Voice interview with a candidate
- **Questions asked:** Background, education, work history, skills, location, salary expectations
- **Output:** Candidate profile saved to `candidates/` and database
- **When to run:** When you have a new candidate to interview

#### Option B: Brief a Hiring Manager
```bash
python jill_agent.py
```
- **What it does:** Voice interview with a hiring manager
- **Questions asked:** Company, team, role, requirements, culture, location, salary budget
- **Output:** Job specification saved to `jobs/` and database
- **When to run:** When you have a new job opening to fill

---

### **STEP 2: The Agent Boardroom (Matching & Negotiation)**
Once you have candidates AND jobs in the database, run this:

```bash
python jack_jill_negotiation.py
```
- **What it does:** Orchestrates Jack and Jill's negotiation to match candidates with jobs
- **The Flow:**
  1. Jill pitches the role and requirements
  2. Jack evaluates his candidates (scores 0-10 based on potential)
  3. Jack pitches suitable candidates to Jill
  4. Jill independently scores each candidate (0-10 based on requirements)
  5. System calculates average score
  6. **IF average > 8:** ✅ Interview scheduled, match saved
  7. **IF average ≤ 8:** ❌ Candidate rejected with reasoning
- **Output:** Full conversation transcript in `jack_jill_conversation.md`
- **When to run:** After collecting candidates and jobs

---

## 📂 Core Files

| File | Purpose |
|------|---------|
| `jack_agent.py` | Candidate interview agent (voice + AI) |
| `jill_agent.py` | Hiring manager interview agent (voice + AI) |
| `jack_jill_negotiation.py` | **Jack & Jill negotiation** (matching & scoring) |
| `database.py` | SQLite database functions |
| `verify_persistence.py` | Database verification tool |

---

## 📁 Directory Structure

```
AI Recruiter/
├── data/
│   └── recruiter.db          # SQLite database
├── candidates/               # Generated candidate profiles (.md)
├── jobs/                     # Generated job specs (.md)
├── prompts/
│   ├── jack_persona.md       # Jack's behavioral instructions
│   └── jill_persona.md       # Jill's behavioral instructions
├── jack_jill_conversation.md # Latest agent conversation transcript
└── [scripts listed above]
```

