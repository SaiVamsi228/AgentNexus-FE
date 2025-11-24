# 🌐 Live Demo  
👉 **Deployed Project:** https://proud-sea-0f270e41e.3.azurestaticapps.net/

# Agent Nexus: AI Interview Practice Partner

> **Eightfold.ai AI Agent Building Assignment Submission**  
> *Problem Statement 2: Interview Practice Partner*

**Agent Nexus** is an autonomous, voice-enabled AI agent designed to conduct realistic mock interviews for technical and non-technical roles. Acting as "Nexus," a Senior Technical Recruiter, the agent conducts structured interviews, adapts to candidate personas, and provides actionable feedback.

---

## 📋 Table of Contents
- [Project Overview](#-project-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Design Decisions](#-design-decisions)
- [Tech Stack](#-tech-stack)
- [Setup & Installation](#-setup--installation)
- [Demo Scenarios](#-demo-scenarios)
- [Project Structure](#-project-structure)

---

## 🎯 Project Overview

This project implements a voice-first AI agent capable of:
1. **Conducting Role-Specific Interviews:** Tailored scenarios for Software Engineers, Sales Development Reps (SDR), and Retail Associates.  
2. **Adaptive Conversation Management:** The agent actively detects user intent (e.g., confusion, distraction) and modifies its responses dynamically rather than following a rigid script.  
3. **Deep-Dive Evaluation:** Unlike simple chatbots, Nexus challenges good answers with follow-up questions ("Why did you choose X over Y?") to test depth of knowledge.  
4. **Post-Interview Analysis:** Generates a comprehensive performance report including scoring, strengths, and areas for improvement.

---

## ✨ Key Features

- **🗣️ Low-Latency Voice Interaction:** Powered by **Vapi** for natural, interruptible voice conversations.  
- **🧠 Persona-Aware Logic:** The backend analyzes not just *what* is said, but *how* it is said, handling:
  - **Confused User:** Rephrases and simplifies.
  - **Chatty User:** Keeps the interview focused.
  - **Efficient User:** Speeds up the flow.
  - **Distracted User:** Shows empathy, then refocuses.
- **🔄 State-Machine Driven Flow:** Interview is handled via **LangGraph** (Intro → Technical → Behavioral → Closing).  
- **📊 Automated Feedback Generation:** Produces a structured JSON/Markdown report evaluating communication and technical accuracy.

---

## 🏗 System Architecture

A decoupled **Client–Server** design:

1. **User → Voice/Web Input**  
2. **Vapi (STT/TTS + Interruptible Voice)**  
3. **FastAPI Backend → LangGraph Brain**  
4. **State Machine** analyzes user input, persona, and evaluation  
5. **SQLite Persistence**  
6. **Response → Vapi → User**

---

## 🧠 Design Decisions

### 1. LangGraph Instead of Chains  
Interviews are **cyclic**, not linear. LangGraph enables loops, branches, persona handlers, and deep dives.

### 2. SQLite Persistence  
Avoids state loss due to server restarts on cloud (Render/Vercel).

### 3. Deep-Dive Mechanic  
Good answers trigger follow-ups instead of proceeding to next question.

### 4. Explicit Persona Detection  
Ensures conversational quality and realistic behavior.

---

## 🛠 Tech Stack

### Backend  
- FastAPI  
- LangGraph  
- LangChain  
- Gemini 2.0 Flash  
- SQLite  

### Frontend  
- React (Vite + TS)  
- Tailwind + Shadcn UI  
- Vapi Web SDK  

---

## 🚀 Setup & Installation

### Prerequisites  
- Node.js 18+  
- Python 3.12+  
- Vapi Public Key  
- Gemini API Key  

---

## 1️⃣ Backend Setup

```bash
git clone https://github.com/YOUR_USERNAME/agent-nexus.git
cd agent-nexus
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Create .env file
# GOOGLE_API_KEY=your_gemini_key

uvicorn app.main:app --reload
```

---

## 2️⃣ Frontend Setup

```bash
cd src
npm install

# Create .env file
# VITE_VAPI_PUBLIC_KEY=your_key_here

npm run dev
```

---

## 🎭 Demo Scenarios (For Evaluation)

| Scenario | Input | Expected Behavior |
| :------- | :---- | :---------------- |
| **Confused User** | "I don’t understand." | Simplifies, rephrases without leaking answers |
| **Chatty User** | "That reminds me of…" | Politely refocuses |
| **Efficient User** | "Skip" | Moves to next question immediately |
| **Distracted User** | "Sorry, noise here" | Shows empathy, repeats the question |
| **Strong Candidate** | Detailed answer | Deep-dive follow-up |

---

## 📂 Project Structure

```text
├── app/                   
│   ├── graph.py           
│   ├── main.py            
│   ├── store.py           
│   └── questions.json     
├── src/                   
│   ├── pages/
│   │   ├── InterviewRoom.tsx
│   │   └── Report.tsx
│   ├── lib/vapi.ts        
├── requirements.txt        
└── README.md              
```

---

## 📝 License

MIT License — Built for Eightfold.ai Hackathon 2025.

