# 🍯 HoneyTrap.AI

**A SOC dashboard that lures attackers into a Cowrie honeypot and uses a Mistral LLM to analyze their behavior in real time.**

## Overview

Traditional honeypots capture raw logs, and analysts still have to dig through them by hand. HoneyTrap.AI adds an AI layer on top. Attackers interact with a realistic SSH/Telnet honeypot (Cowrie), every session is captured, and a Mistral LLM interprets what the attacker is trying to do. The results appear on a live SOC dashboard.

## Features

- **Cowrie honeypot**: emulates an SSH/Telnet server and records login attempts, commands, and file downloads
- **Real-time LLM analysis**: Mistral classifies attacker behavior, intent, and severity from session activity
- **SOC dashboard**: live view of sessions, commands, attacker IPs, and AI-generated insights
- **Threat summaries**: plain-language explanation of what each attacker did and why it matters
- **`<add: MITRE ATT&CK mapping / alerting / geo-IP, if implemented>`**

## Architecture

```
Attacker ──► Cowrie Honeypot ──► Session Logs (JSON)
                                      │
                                      ▼
                              Flask Backend ──► Mistral LLM
                                      │            (behavior analysis)
                                      ▼
                               SOC Dashboard
```

## Tech Stack

| Layer | Technology |
|-------|------------|
| Honeypot | Cowrie |
| Backend | Python, Flask |
| AI Analysis | Mistral LLM |
| Frontend | `<HTML/CSS/JS or framework>` |

## Project Structure

```
HoneyTrap.AI/
├── Hackathon AI/     # <describe>
├── MirrorTrap/       # <describe>
├── .env.example      # Environment variable template
├── .gitignore
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.10+
- Cowrie installed and running (see the [Cowrie docs](https://docs.cowrie.org))
- A Mistral API key

### Installation

```bash
git clone https://github.com/Shrak-24/HoneyTrap.AI.git
cd HoneyTrap.AI
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Configuration

Copy the example env file and add your credentials:

```bash
cp .env.example .env
```

```env
MISTRAL_API_KEY=your_key_here
COWRIE_LOG_PATH=/path/to/cowrie/var/log/cowrie/cowrie.json
```

### Run

```bash
python app.py
```

Open `http://localhost:5000` to view the dashboard.

## Usage

1. Start Cowrie and expose it on the port you want attackers to hit.
2. Launch the Flask app.
3. Watch sessions appear on the dashboard as attackers connect.
4. Review the AI-generated analysis for each session.

## Security Notice

⚠️ Run the honeypot in an **isolated environment** (VM or separate VLAN). Never deploy it on a machine that holds real data or credentials, and never commit API keys.

## Team

**Team SecureX**
- Shraddha S Kurakuri ([@Shrak-24](https://github.com/Shrak-24))
- Sagarika
- Aditya

## License

`<MIT / other>`
