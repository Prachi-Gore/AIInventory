# Complete Setup Guide - Inventra AI System

## Quick Start (5 Minutes)

This project comes with a **pre-seeded database**, so you can start immediately after setting up API keys!

### Step 1: Extract/Clone Project

```bash

# GitHub
git clone <repo-url>
cd inventra
```

### Step 2: Create Virtual Environment

```bash
# Create virtual environment
python3 -m venv venv

# Activate it
source venv/bin/activate          # macOS/Linux
# OR
venv\Scripts\activate              # Windows
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure API Keys

```bash
# Copy environment template
cp .env.example .env

# Edit .env with your API keys
nano .env  # or use any text editor
```

Required API keys in `.env`:

```bash
# 1. OpenAI API (Required)
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_MODEL=gpt-4o-mini

# 2. OpenWeather API (Required)
OPENWEATHER_API_KEY=your_openweather_api_key_here

# 3. Hugging Face API (Optional - for MCP sentiment analysis)
HUGGINGFACE_API_TOKEN=your_huggingface_token_here
```

### Step 5: Run the Application!

```bash
# Option 1: Web Interface (Recommended)
python main.py web

# Option 2: Command Line Interface
python main.py cli

# Option 3: View Statistics
python main.py stats
```

**That's it!** The database is already included with sample data. 🎉

---

## What's Included

### ✅ Pre-Configured Database

The `database/inventra.db` file (936 KB) comes pre-loaded with:

- **100 inventory items** across 5 regions
- **9,157 sales transactions** (2019-2024)
- **5,000 financial records**
- **20 vendor profiles**
- **0 pending tickets** (clean slate)
- **0 forecasts** (clean slate)

**You don't need to run any database setup!**

### ✅ Sample Data Overview

```
Regions: North, South, East, West, Central
Categories: Electronics, Kitchen Appliances, Home Appliances, Lighting, Home Care
Vendors: 20 suppliers with quality scores and reliability ratings
Date Range: January 2019 - October 2024
```

### ✅ Application Features

1. **Multi-Agent AI System** (LangGraph orchestration)
2. **Natural Language Queries** (ask questions in plain English)
3. **Financial Analysis** (profit/loss, revenue trends)
4. **Inventory Management** (stock tracking, reorder alerts)
5. **Weather Forecasting** (demand prediction)
6. **Ticket Management** (automated vendor tickets)
7. **Interactive Dashboard** (Streamlit web interface)
8. **Conversation Memory** (context across queries)

---

## Usage Examples

### Web Interface

```bash
python main.py web
```

Opens at `http://localhost:8501`

**Try these queries:**
- "Show me the financial summary"
- "What items are low in stock?"
- "Give me sales analysis for North region"
- "What should I reorder for monsoon season?"
- "Show pending tickets"

### CLI Mode

```bash
python main.py cli
```

Interactive command-line interface with the same capabilities.

### Statistics

```bash
python main.py stats
```

Quick overview of:
- Inventory levels and low-stock count
- Sales summary (last 30 days)
- Financial metrics (last 90 days)
- Pending tickets

---

## Optional: ML MCP Server

The ML MCP Server provides sentiment analysis using Hugging Face models.

### Setup

1. Get Hugging Face token (see above)
2. Add to `.env`: `HUGGINGFACE_API_TOKEN=hf_...`
3. Run the server:

```bash
python integrations/mcp_server.py
```

### Features

- Sentiment analysis of text
- Uses DistilBERT model
- MCP protocol compatible

See [integrations/README_MCP.md](integrations/README_MCP.md) for detailed documentation.

---

## Troubleshooting

### Issue: Module not found errors

### Issue: Streamlit won't start

**Solution:**
```bash
# Clear Streamlit cache
rm -rf ~/.streamlit/cache

# Try direct command
streamlit run ui/streamlit_app.py
```

### Issue: No data returned from queries

**Cause:** Database has historical data (2019-2024), default queries look at recent dates.

**Solution:** The system automatically falls back to all-time data if no recent data found. Default range is 365 days.

---

## Project Structure

```
inventra/
├── agents/                   # AI Agents
│   ├── coordinator.py        # LangGraph orchestrator
│   ├── decision_agent.py     # Business decisions
│   └── report_agent.py       # Data reports
│
├── services/                 # Business logic
│   ├── data_pipeline.py      # Data aggregation
│   ├── forecast_updater.py   # Weather forecasting
│   └── ticket_manager.py     # Ticket management
│
├── tools/                    # Utilities
│   ├── finance.py            # Financial calculations
│   ├── weather.py            # Weather API
│   └── export.py             # Data export
│
├── database/                 # Database layer
│   ├── inventra.db          # ⭐ Pre-seeded SQLite DB
│   ├── db_manager.py         # Database operations
│   ├── memory_manager.py     # Conversation history
│   ├── schema.sql            # Schema definition
│   └── data/*.csv            # Seed data (reference)
│
├── integrations/             # External integrations
│   ├── mcp_server.py         # ML MCP Server
│   └── README_MCP.md         # MCP documentation
│
├── config/                   # Configuration
│   ├── settings.py           # Settings management
│   └── logger.py             # Logging
│
├── ui/                       # User interface
│   └── streamlit_app.py      # Streamlit web app
│
├── main.py                   # Entry point
├── requirements.txt          # Dependencies
├── .env.example              # Environment template
├── README.md                 # Main documentation
└── SETUP_GUIDE.md           # This file
```

---

### Minimum Requirements

- **Python:** 3.10 or higher
- **RAM:** 2 GB
- **Storage:** 100 MB (excluding venv)
- **OS:** macOS, Linux, or Windows

### Recommended

- **Python:** 3.11 or 3.12
- **RAM:** 4 GB
- **Storage:** 500 MB
- **Internet:** For API calls

---

## Technology Stack

- **AI/ML:** LangGraph, LangChain, OpenAI, Hugging Face
- **Backend:** Python 3.12, SQLite, Pandas
- **Frontend:** Streamlit
- **APIs:** OpenWeather, Hugging Face Inference
- **Protocol:** MCP (Model Context Protocol)

---

## Support & Resources

- **Main README:** [README.md](README.md)
- **MCP Server Guide:** [integrations/README_MCP.md](integrations/README_MCP.md)
- **API Documentation:**
  - [OpenAI](https://platform.openai.com/docs)
  - [OpenWeather](https://openweathermap.org/api)
  - [Hugging Face](https://huggingface.co/docs/api-inference/index)

---

## What's Next?

After setup, try:

1. **Explore the Web Interface:**
   ```bash
   python main.py web
   ```
   Ask natural language questions!

2. **Check Statistics:**
   ```bash
   python main.py stats
   ```

3. **Try CLI Mode:**
   ```bash
   python main.py cli
   ```

4. **Optional: Run MCP Server:**
   ```bash
   python integrations/mcp_server.py
   ```

Enjoy using Inventra! 🎉

---

**Version:** 2.1
**Last Updated:** 2026-05-30
**Database:** Pre-seeded and ready to use
