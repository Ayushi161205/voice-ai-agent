# 🤖 AI Voice Agent

An AI-powered outbound calling system that makes intelligent voice calls, answers questions using a custom knowledge base, and automatically captures call data — built using **Vapi AI**, **Twilio**, and **n8n**.

---

## 📌 Project Overview

This system enables you to:
- Make automated outbound calls to multiple numbers via CSV
- Answer caller questions using an AI-powered knowledge base
- Capture and store call data automatically via webhooks
- Scale outreach easily with bulk calling support

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| [Vapi AI](https://vapi.ai) | AI voice agent & call management |
| [Twilio](https://twilio.com) | Phone number & telephony provider |
| [n8n](https://n8n.io) | Workflow automation & webhook capture |
| [ngrok](https://ngrok.com) | Tunnel for local n8n webhook exposure |
| Claude Haiku 4.5 (Anthropic) | LLM powering the AI agent |
| Deepgram | Speech transcription |
| ElevenLabs | Voice synthesis |

---

## 📂 Repository Structure

```
ai-voice-agent/
├── vapi-agent.json          # Vapi AI assistant configuration
├── n8n-workflow.json        # n8n workflow for call data capture
├── knowledge-base.docx      # Knowledge base for the AI agent
├── calls.csv                # Sample CSV for bulk outbound calling
└── README.md                # Project documentation
```

---

## 🚀 How It Works

1. **Outbound Calls** — A CSV file with phone numbers is uploaded to Vapi, triggering bulk outbound calls via Twilio
2. **AI Agent** — The Vapi assistant (powered by Claude Haiku) answers questions using the knowledge base
3. **Webhook Capture** — After each call, Vapi sends an `end-of-call-report` to the n8n webhook
4. **Data Storage** — n8n processes and stores the call payload for analysis

---

## ⚙️ Setup Instructions

### Prerequisites
- Vapi account → [vapi.ai](https://vapi.ai)
- Twilio account with a phone number
- n8n (self-hosted via Docker or cloud)
- ngrok (for local webhook exposure)

### 1. Clone this repository
```bash
git clone https://github.com/your-username/ai-voice-agent.git
cd ai-voice-agent
```

### 2. Set up n8n via Docker
```bash
docker run -it --rm --name n8n -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```
- Import `n8n-workflow.json` into your n8n instance
- Activate the workflow

### 3. Expose n8n via ngrok
```bash
ngrok http --url=your-static-domain.ngrok-free.app 5678
```

### 4. Import Vapi Agent
- Go to [dashboard.vapi.ai](https://dashboard.vapi.ai)
- Create a new assistant and import `vapi-agent.json`
- Upload `knowledge-base.docx` to the knowledge base
- Set Server URL to: `https://your-ngrok-url/webhook/vapi`

### 5. Make Calls
- Go to Vapi → Phone Numbers → Test → Multiple Numbers
- Upload `calls.csv`
- Select your assistant and hit Call!

---

## 📊 Features

- ✅ Bulk outbound calling via CSV upload
- ✅ AI-powered voice agent with custom knowledge base
- ✅ Automatic call data capture via n8n webhook
- ✅ End-of-call reports with transcript and analysis
- ✅ Self-hosted n8n with persistent Docker volume storage
- ✅ Scalable to hundreds of numbers

---

## 📄 License

This project is for internal use. All rights reserved.
