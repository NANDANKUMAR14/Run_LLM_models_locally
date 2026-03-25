# Local LLM Setup Guide using Ollama and LM Studio

## Table of Contents
1. Introduction
2. What is a Local LLM?
3. System Requirements
4. Installing Ollama
5. Running Models with Ollama
6. Installing LM Studio
7. Running Models with LM Studio
8. Ollama vs LM Studio
9. Folder Structure for Projects
10. Using Local LLM with Python
11. Using Local LLM with LangChain
12. Using Local LLM with n8n
13. Troubleshooting
14. Recommended Models
15. Conclusion

---

## 1. Introduction
This guide explains how to run Large Language Models (LLMs) locally on your computer using **Ollama** and **LM Studio**. Running LLMs locally allows you to build AI agents, chatbots, automation tools, and offline AI applications without paying for API usage.

---

## 2. What is a Local LLM?
A Local LLM is a Large Language Model that runs on your own computer instead of the cloud.

### Advantages
- No API cost
- Works offline
- Full privacy
- Can be integrated into your own apps

### Disadvantages
- Requires good RAM
- Slower than cloud models

---

## 3. System Requirements
Minimum Requirements:
- RAM: 8GB (16GB recommended)
- Storage: 20GB free space
- CPU: i5 / Ryzen 5 or better
- GPU: Optional but recommended

---

## 4. Installing Ollama

### Step 1: Install Ollama
Visit: https://ollama.com
Download and install Ollama.

### Step 2: Start Ollama
Open terminal and run:

```bash
ollama serve
```

### Step 3: Download a Model

```bash
ollama pull llama3
```

Other models:

```bash
ollama pull mistral
ollama pull codellama
ollama pull phi
ollama pull gemma
```

### Step 4: Run the Model

```bash
ollama run llama3
```

Now you can chat with the model locally.

---

## 5. Running Models with Ollama API
Ollama runs on:

```
http://localhost:11434
```

You can use it in Python.

### Python Example

```python
import requests

url = "http://localhost:11434/api/generate"

data = {
    "model": "llama3",
    "prompt": "Explain AI in simple words"
}

response = requests.post(url, json=data)
print(response.json()["response"])
```

---

## 6. Installing LM Studio

### Step 1: Download LM Studio
Visit: https://lmstudio.ai
Download and install.

### Step 2: Download Model
Open LM Studio → Search model → Download:
- Llama 3
- Mistral
- Phi
- Gemma
- DeepSeek

### Step 3: Start Local Server
Go to:

```
Local Server → Start Server
```

Server runs on:

```
http://localhost:1234
```

---

## 7. Using LM Studio API

### Python Example

```python
import requests

url = "http://localhost:1234/v1/chat/completions"

headers = {
    "Content-Type": "application/json"
}

data = {
    "model": "local-model",
    "messages": [
        {"role": "user", "content": "Explain machine learning"}
    ]
}

response = requests.post(url, headers=headers, json=data)
print(response.json())
```

---

## 8. Ollama vs LM Studio

| Feature | Ollama | LM Studio |
|--------|--------|-----------|
| CLI | Yes | No |
| GUI | No | Yes |
| API | Yes | Yes |
| Easy for Beginners | Medium | Easy |
| Best For | Automation | Chat UI |

---

## 9. Folder Structure for AI Project

```
ai-project/
│
├── app.py
├── requirements.txt
├── .env
├── models/
├── agents/
├── workflows/
└── README.md
```

---

## 10. Using Local LLM with LangChain

Install:

```bash
pip install langchain ollama
```

Python Code:

```python
from langchain_community.llms import Ollama

llm = Ollama(model="llama3")

print(llm.invoke("Explain Docker in simple words"))
```

---

## 11. Using Local LLM with n8n

Steps:
1. Install n8n using Docker
2. Start Ollama
3. In n8n use HTTP Request node
4. Connect to:

```
http://host.docker.internal:11434/api/generate
```

Method: POST

Body:

```json
{
  "model": "llama3",
  "prompt": "Write an email about AI",
  "stream": false
}
```

---

## 12. Troubleshooting

### Error: Port already in use

```bash
sudo lsof -i :11434
kill -9 <PID>
ollama serve
```

### Error: Model not found

```bash
ollama list
```

### Error: Slow Model
Use smaller models:
- phi
- gemma
- mistral

---

## 13. Recommended Models

| Model | Size | Use |
|------|------|-----|
| Phi | Small | Low RAM |
| Mistral | Medium | Chat |
| Llama 3 | Large | Best Quality |
| CodeLlama | Medium | Coding |
| DeepSeek | Medium | Coding |

---

## 14. Conclusion

You can now run LLMs locally using:
- Ollama (best for automation and API)
- LM Studio (best GUI interface)

You can connect these to:
- Python apps
- Web apps
- AI Agents
- n8n automation
- Telegram bots

This is the foundation for building your own AI assistant locally.

