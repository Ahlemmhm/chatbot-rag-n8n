# Chatbot RAG (n8n + Pinecone + OpenAI)

Single-file **web chat UI** that talks to an **n8n** RAG workflow (Pinecone vector store + OpenAI).  
Repo: https://github.com/Ahlemmhm/chatbot-rag-n8n

---

## ✨ What’s inside
- `index.html` – the chat UI (no build, just open it)
- `Chatbot RAG.json` – exported n8n workflow (no credentials inside)

---

## 🚀 Quick start (local)

1. **Import the workflow into n8n**  
   In n8n, open **… (top-right) → Import from File…** and select the JSON.

2. **Set credentials inside n8n**  
   - OpenAI API key  
   - Pinecone API key / index / namespace  
   *(Use the same embeddings model for ingest & query, e.g. `text-embedding-3-small` → dim 1536.)*

3. **Activate the workflow & copy the Production Webhook URL**  
   In **Webhook** node, use the **Production URL** (e.g. `http://localhost:5678/webhook/zit-chat`).  
   The Webhook must be set to **Respond = Using Respond to Webhook node**.

4. **Make sure the Respond node returns JSON**  
   In **Respond to Webhook**:
   - **Respond With:** `Text`
   - **Body** (Expression **ON**):
     ```js
     {{ JSON.stringify({ reply: $json.output || $json.response || $json.data || 'No reply' }) }}
     ```
   - **Headers:**
     - `Content-Type: application/json`
     - `Access-Control-Allow-Origin: *`
     - `Access-Control-Allow-Headers: Content-Type, X-Session-Id`
     - `Access-Control
