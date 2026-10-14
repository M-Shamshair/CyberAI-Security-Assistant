# CyberAI Security Assistant

## Local Offline Cybersecurity AI Assistant - V1 Stable

**Release Date:** 2026-10-14  
**Version:** V1.0 Stable  
**Architecture:** Security Reasoning Engine V7  

---
![Status](https://img.shields.io/badge/Status-V1.0%20Stable-blue)
![Privacy](https://img.shields.io/badge/Privacy-100%25%20Offline-green)


## 📖 Overview

CyberAI is a **private, offline, local AI security assistant** designed specifically for cybersecurity professionals, penetration testers, and application security engineers. It operates entirely on your local machine with no cloud dependencies, ensuring complete privacy for sensitive security assessments, source code reviews, and vulnerability research.

Unlike generic AI chatbots, CyberAI is engineered with an **Offensive Security Mindset**, thinking like a Senior Penetration Tester and Application Security Consultant.

---

## 🏆 Benefits Over Generic / Open-Source AI Models

| Feature | CyberAI (Local) | Generic Cloud AI (Chat-GPT, etc.) |
|---------|-----------------|----------------------------------|
| **Data Privacy** | ✅ 100% local, no data leaves your machine | ❌ Data sent to cloud servers |
| **Source Code Review** | ✅ Completely private, safe for proprietary code | ❌ Risk of code and sensitive information exposure |
| **Offline Operation** | ✅ Works without internet (Air-gapped ready) | ❌ Requires internet connection |
| **Custom Knowledge** | ✅ 850+ curated security documents (OWASP, OSCP, MITRE) | ❌ Limited to general training data |
| **Security Focus** | ✅ Specialized for offensive security & VAPT | ❌ General purpose, lacks pentest depth |
| **Model Control** | ✅ Choose and switch between local models | ❌ Fixed model, no control |
| **Cost & Limits** | ✅ One-time setup, no subscription, no rate limits | ❌ Monthly fees, strict rate limits |
| **Tool Integration** | ✅ Direct access to local Kali Linux tools (Nmap, etc.) | ❌ No local tool execution |
| **Keyword Flexibility** | ✅ Unrestricted offensive/defensive security terminology | ❌ Heavy censorship on offensive keywords |

---

## 💻 System Requirements
- **OS:** Kali Linux, Ubuntu, or Debian-based distributions
- **Python:** 3.10 or higher
- **RAM:** 8GB minimum (16GB recommended for smoother DeepSeek 6.7B inference)
- **Storage:** ~10GB free space (for models and vector database)
- **CPU:** Multi-core processor (4+ cores recommended)
- **GPU:** Optional (CPU inference is supported, but GPU significantly speeds up generation)

---

## 🏗️ Current Architecture

CyberAI V1 uses a modular, multi-engine architecture designed for professional security reasoning:

```text

User Query
   ↓
[1] Intent Router & Decision Engine
   ↓
[2] Security Brain V7 ────→ Tool Executor (if Nmap/Tool request)
   ↓
[3] Prompt Engine (Combines: RAG Context + Memory + Tool Output + Consultant Persona)
   ↓
[4] Ollama Local LLM (Qwen2.5-Coder:3b / DeepSeek-Coder:6.7b)
   ↓
[5] Response Engine (Validates pentest structure, evidence, and quality)
   ↓
Final Professional Security Assessment

```

## Core Components
- Ollama Runtime: Local LLM management (No cloud API).
- ChromaDB Vector Database: Stores 850+ cybersecurity documents as semantic embeddings.
- nomic-embed-text: Local embedding model for RAG retrieval.
- Security Reasoning Engine V7: Modular Python engine handling intent, brain, RAG, tools, and response validation.


## 📂 Current Project Structure
```text
CyberAI/
├── modules/                    # Core AI engine
│   ├── config.py               # Central configuration
│   ├── decision_engine.py      # Decision making logic
│   ├── intent_router.py        # Query classification
│   ├── memory_manager.py       # Conversation memory
│   ├── model_selector.py       # LLM model selection
│   ├── ollama_client.py        # Ollama API interface
│   ├── prompt_engine_v7.py     # Prompt construction
│   ├── rag_engine.py           # RAG retrieval
│   ├── response_engine.py      # Response formatting & QA
│   ├── security_brain_v7.py    # Security reasoning core
│   ├── tool_advisor.py         # Tool recommendations
│   ├── tool_executor.py        # Safe tool execution
│   └── tool_output_analyzer.py # Output analysis
│
├── scripts/                    # Execution scripts
│   ├── cyberai_offensive_v7_updated.py  # Main launcher
│   ├── start-ai.sh             # Start Ollama manually
│   ├── status-ai.sh            # Check Ollama status
│   └── stop-ai.sh              # Stop Ollama
│
├── tools/                      # Maintenance utilities
│   └── rag/
│       ├── build_vector_db.py  # Rebuild RAG index
│       ├── prepare_documents.py # Process documents
│       └── query_rag.py        # Test RAG retrieval
│
├── prompts/                    # AI behavior control
│   └── security_consultant.txt # Security consultant persona
│
├── rag_index/                  # ChromaDB vector database
│   └── chroma.sqlite3          # 850+ indexed security docs
│
├── memory/                     # AI memory storage
├── requirements.txt            # Production dependencies
├── requirements_dev.txt        # Development dependencies
├── install.sh                  # Automated installer
├── VERSION                     # Release information
└── README.md                   # This file
```

# 🛠️ Installation

Option 1: Automated Installation (Recommended)
If you are moving this to a new high-specification machine, simply run the installer:
1. chmod +x install.sh
2. ./install.sh

The installer will automatically:
1. Check Python/pip availability.
2. Create an isolated virtual environment.
3. Install required Python dependencies (chromadb, requests, tqdm, etc.).
4. Install Ollama (if missing).
5. Pull required models (qwen2.5-coder:3b, deepseek-coder:6.7b, nomic-embed-text).
6. Validate that the RAG database and modules load correctly.

Option 2: Manual Installation
If you prefer to set up the environment manually:

1. Create virtual environment:
- python3 -m venv ~/CyberAI_env
- source ~/CyberAI_env/bin/activate

2. Install Python dependencies
- pip install -r requirements.txt

3. Install Ollama (if not already installed)
- curl -fsSL https://ollama.com/install.sh | sh

4. Pull required models
- ollama pull qwen2.5-coder:3b
- ollama pull deepseek-coder:6.7b
- ollama pull nomic-embed-text

# 🚀 Usage & Starting the Program
Important: Ollama is configured to NOT start automatically on boot to save system resources. You must start it manually when needed.

Step 1: Start the AI Engine
- ./scripts/start-ai.sh
(Or manually: sudo systemctl start ollama)

Step 2: Run CyberAI
Activate virtual environment (if using manual install)
- source ~/CyberAI_env/bin/activate

Launch CyberAI
- python scripts/cyberai_offensive_v7_updated.py --debug

Step 3: Model Selection
Upon startup, CyberAI will prompt you to select a model:
Available Local Models

1. nomic-embed-text:latest
2. deepseek-coder:6.7b
3. qwen2.5-coder:3b

Select model number: 

- Qwen2.5-Coder:3b (Recommended): Faster, excellent for structured VAPT reports and API/Mobile security.
- DeepSeek-Coder:6.7b: Slower, deeper reasoning for complex code review and architecture analysis

# 🔮 Next Version Vision (Roadmap)
# CyberAI V2 (Intelligence & RAG Upgrade)
- Hybrid Search: Combine semantic vector search with keyword/BM25 matching.
- Reranking: Implement cross-encoders to rank RAG chunks for higher accuracy.
- Advanced Memory: Long-term pattern recognition and context-aware conversation.
- Security Benchmarking: Automated quality scoring and false-positive reduction metrics.

# CyberAI V3 (Automation & Integration)
- Fine-Tuned Security Model: Custom-trained on security datasets to reduce hallucinations.
- SAST Integration: Direct integration with local SAST tools for automated triage.
- Vulnerability Verification: Automated PoC generation and safe exploitation testing.
- Report Generation: Automated PDF/HTML VAPT report generation.

# 🔒 Privacy & Security Note
CyberAI is built with a Privacy-First architecture.
- No Telemetry: The application does not collect or transmit any data.
- No Cloud API: All LLM inference and embedding generation happen locally via Ollama.
- Air-Gap Ready: Once models are downloaded, CyberAI can operate on completely isolated, offline networks.
- Safe Execution: The Tool Executor framework restricts automated commands to a safe allow-list (e.g., Nmap, Whois) to prevent accidental system damage.

# 🛠️ Troubleshooting
* Ollama Connection Failed: Ensure Ollama is running (sudo systemctl status ollama). If not, start it (sudo systemctl start ollama).
* ModuleNotFoundError: Ensure your virtual environment is activated (source ~/CyberAI_env/bin/activate).
* ChromaDB / Embedding Errors: Ensure nomic-embed-text is installed (ollama list). If missing, run ollama pull nomic-embed-text.
* Slow Response Times: DeepSeek 6.7B requires more CPU/RAM. Switch to qwen2.5-coder:3b for faster responses, or consider moving to a machine with a dedicated GPU.

# 📜 License & Disclaimer
This project is for educational, research, and authorized professional security testing purposes.
Always obtain proper authorization before performing security assessments on systems you do not own.

Maintained by: 
- Muhammad Shamshair
- Last Updated: 2026-10-14

---

## 🔒 Source Code Access
The core CyberAI source code, security prompts, and RAG knowledge base are maintained in a **private repository** to ensure controlled distribution and security integrity.
This public repository contains **architecture and documentation only**.

**Authorized researchers, developers, and partners** may request source access:
1. Email: `your-email@yourdomain.com`
2. Subject: `CyberAI Source Code Access Request`
3. Include: Your GitHub username and intended use case

Approved requesters are added as collaborators to the private repository.
