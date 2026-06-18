# Finance AI Agent

A conversational finance assistant built with **LangChain** and **OpenAI**. The agent uses one stock lookup tool, remembers conversation history for follow-up questions, and only responds to finance-related queries.

## Features

- OpenAI LLM (`gpt-4o-mini`) for understanding and responding to user questions
- Single `get_stock_info` tool powered by the Yahoo Finance chart API via `requests` (no extra API key required)
- **Conversation memory** — follow-up questions like *"What about Microsoft?"* work in context
- **Finance-only guard** — non-finance questions are politely rejected before the agent runs
- Interactive **chat window** (Gradio) embedded in the notebook output
- API key loaded securely from a local `.env` file

## Project Structure

```
finance_agent/
├── .env                      # Your OpenAI API key (not committed to git)
├── finance_agent.ipynb       # Main notebook — run this
├── requirements.txt          # Python dependencies
└── README.md                 # This file
```

## Setup

### 1. Create a virtual environment (recommended)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure your OpenAI API key

Create or edit `.env` in the project root:

```
OPENAI_API_KEY=your_openai_api_key_here
```

> **Note:** Never commit `.env` to version control.

### 4. Open the notebook

Open `finance_agent.ipynb` in **Cursor/VS Code** (with the Python extension), or launch Jupyter:

```bash
python -m notebook finance_agent.ipynb
```

Run all cells in order, then ask finance questions when prompted.

## Example Questions

- "What is Apple's current stock price?"
- "Show me key info for MSFT"
- "Compare that with Google" *(follow-up — uses chat memory)*

Type `quit` or `exit` to stop the chat loop.

## How It Works

1. **Environment** — `python-dotenv` loads `OPENAI_API_KEY` from `.env`.
2. **Finance guard** — Each question is checked; only finance-related topics proceed to the agent.
3. **Stock tool** — Fetches live price, day range, and 52-week metrics via the Yahoo Finance chart API.
4. **Agent + memory** — LangChain's `create_agent` with an in-memory checkpointer keeps conversation context across turns.
5. **Chat window** — Gradio UI embedded in the notebook; type `quit` to stop.

## Requirements

- Python 3.10+
- OpenAI API key with access to chat models
- Internet connection (for OpenAI and Yahoo Finance data)

## Disclaimer

This agent provides general market data for educational purposes only. It is **not** financial advice. Always consult a qualified professional before making investment decisions.
