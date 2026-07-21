# 🚗 Insurance Claim AI Agent

An AI-powered Insurance Claim Agent that analyzes vehicle damage images, estimates repair costs, retrieves policy information, and generates insurance claim reports using Generative AI.

---

## Features

- 🔍 Vehicle damage detection using Google Gemini Vision
- 🤖 Multi-Agent workflow
- 📄 Insurance policy retrieval using RAG
- 💰 Repair cost estimation
- 📋 Automated insurance claim report generation
- 💬 Intelligent decision-making using LLMs

---

## Tech Stack

- Python
- Google Gemini
- LangChain
- FAISS
- Streamlit
- RAG (Retrieval-Augmented Generation)

---

## Project Architecture

Vision Agent
↓
Damage Analysis
↓
Policy Retrieval (RAG)
↓
Cost Estimation
↓
Decision Agent
↓
Claim Report Generation

---

## Project Structure

```
Insurance_claim_agent/
│── vision_agent.py
│── policy_agent.py
│── cost_agent.py
│── decision_agent.py
│── graph.py
│── state.py
│── insurance_policy.pdf
│── parts.csv
│── index.faiss
│── index.pkl
```

---

## Future Improvements

- Multi-company insurance support
- OCR for vehicle documents
- Real-time repair cost API
- Web deployment
- Voice-enabled claim assistant

---

## Author

**Mohanraj P**

AI Engineer | Generative AI | AI Agents

LinkedIn:
:https://www.linkedin.com/in/mohanraj-p-2bb994217/
GitHub:
https://github.com/mohanraj-Ai
