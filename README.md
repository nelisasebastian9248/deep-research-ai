🧠 Deep Research AI Agent System

A fully automated AI-powered multi-agent research system that plans, searches, writes, and emails detailed research reports.
Built with Python, LangGraph-style agent orchestration, Gradio UI, and SendGrid API for automated email delivery.

🚀 Overview

The Deep Research Agent System conducts autonomous end-to-end research:

Takes a user query via Gradio web UI

Plans multiple targeted searches using an intelligent Planner Agent

Performs web searches via an integrated Search Agent

Synthesizes findings into a long-form Markdown report 

Emails the final report using SendGrid API

All operations are traced and logged for debugging and transparency.

🧩 Architecture
🔹 1. Gradio Interface (main.py)

Collects the research topic.

Streams progress updates (“Planning…”, “Searching…”, “Writing report…”).

Displays the Markdown report.

Launches in the browser automatically.

🔹 2. Research Manager (research_manager.py)

The central orchestrator that:

Generates a unique trace ID for tracking.

Calls agents in sequence:

Planner Agent → generates search queries.

Search Agent → executes and summarizes web searches.

Writer Agent → compiles a detailed Markdown report.

Email Agent → formats and sends the report as HTML.

🔹 3. Agents

Each agent uses an LLM model (gpt-4o-mini) and runs asynchronously for scalability.

Agent/Function/OutputType
planner_agent-Generates structured search queries-WebSearchPlan
search_agent-Summarizes web pages into concise notes-str
writer_agent-Synthesizes long, detailed report-ReportData
email_agent	-Sends formatted email report-dict

📬 Email Integration (SendGrid)

The Email Agent uses SendGrid API
 to send formatted HTML reports.

You must set your SendGrid API key in .env:

SENDGRID_API_KEY=your_api_key_here


Make sure your sender email is verified in SendGrid before running.

⚙️ Environment Setup
1️⃣ Clone the repository
git clone https://github.com/<your-username>/deep-research-ai.git
cd deep-research-ai

2️⃣ Create a virtual environment
python -m venv venv
source venv/bin/activate   # or venv\Scripts\activate on Windows

3️⃣ Install dependencies
pip install -r requirements.txt

4️⃣ Add .env file
OPENAI_API_KEY=your_openai_key
SENDGRID_API_KEY=your_sendgrid_key

5️⃣ Run the app
uv run deep_research.py

This will launch Gradio in your browser automatically.

🧠 Example Workflow

Enter a research topic in the Gradio UI (e.g., “Impact of renewable energy on global economy”).

The system will:

Plan relevant searches.

Summarize results.

Write a multi-page Markdown report.

Email you the full formatted version.

View progress logs directly in the interface or terminal.

🪶 Example Output

Short Summary

Renewable energy has shown exponential growth globally, driven by policy incentives and cost reduction. However, disparities persist in adoption between developed and developing nations.

Report

(Full 5–10 page Markdown report generated dynamically by the Writer Agent)

Follow-up Questions

How do subsidies affect renewable investment by region?

What role does AI play in optimizing energy grids?

🧰 Tech Stack

Python 3.10+

Gradio — interactive front-end

Pydantic — typed model validation

SendGrid API — email delivery

OpenAI GPT-4o-mini — reasoning and writing

🧾 Folder Structure
deep-research-ai/
├── main.py                 # Gradio UI
├── research_manager.py     # Core research pipeline
├── planner_agent.py        # Plans search queries
├── search_agent.py         # Executes and summarizes searches
├── writer_agent.py         # Writes final report
├── email_agent.py          # Sends formatted report
├── agents.py               # Base agent utilities
├── requirements.txt
├── .env
└── README.md

🛠️ Future Enhancements

Add vector-based search with Chroma or FAISS

Integrate Google Search API for higher fidelity results

Support multiple recipients and report templates

Add RAG pipeline for citation-grounded summaries

