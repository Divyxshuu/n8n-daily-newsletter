# 🗞️ AI Daily Newsletter Bot (n8n) - Built By Div ❤️

This project is an automated AI-powered newsletter generator using **n8n**, designed to deliver **daily world news** in both HTML email (via Gmail) and Discord (Markdown format). 

It fetches news from **RSS feeds** and **NewsAPI**, processes them, filters and deduplicates, summarizes key headlines, and sends beautifully formatted updates every morning.

---

## 📌 Features

- ⏰ Automated daily schedule (e.g., every day at 8 AM)
- 📰 Combines sources: RSS feeds + NewsAPI
- 🧠 AI-generated summaries via ChatGPT-4o
- 📤 Outputs to Gmail (HTML) & Discord (Markdown)
- 🧹 Filters, deduplicates, and limits to latest 25 headlines
- 💡 Fully modular and no-code/low-code friendly via n8n

---

## 🔁 Workflow Overview

```
Schedule Trigger
   ├── RSS Read
   └── HTTP Request (NewsAPI)
           ↓
        Split Out (articles array)
           ↓
        Merge (append both sources)
           ↓
        Sort (by publishedAt and pubDate, descending)
           ↓
        Limit (to latest 25 items)
           ↓
        Edit Fields (normalize title to lowercase)
           ↓
        Remove Duplicates (based on normalized title)
           ↓
        Summarize (code node combining titles/content)
           ↓
        AI Agent (GPT-4o for dual output)
               ├── Gmail Tool (HTML)
               └── Discord Tool (Markdown)
```

---

## ⚙️ Setup Guide

### 1. 🧠 Requirements
- [n8n](https://n8n.io/)
- NewsAPI Key
- OpenAI API Key
- Gmail + Discord credentials

### 2. 🔑 Environment Variables
Set in n8n credentials:
- `NEWSAPI_KEY`
- `OPENAI_API_KEY`
- Gmail Auth (via OAuth2)
- Discord Webhook or legacy integration

### 3. 📬 AI Agent Prompt

The AI agent prompt formats two outputs:

**Gmail Output (HTML Email)**  
Includes a subject line and up to 12 styled items with emojis and formatting.

**Discord Output (Markdown)**  
Includes bold titles, emoji bullets, and spacing for Discord delivery.

---

## 🔍 Output Sample

### Gmail (HTML)

```html
<h2>📰 Today’s Top Headlines</h2>
<p>Hello! Here's a quick look at today’s most important global stories:</p>

<p>🌍 <b>India Hosts G20 Summit</b>: Global leaders discuss digital economy policies.</p>
<p>🧠 <b>Meta Unveils New AI Tools</b>: Meta rolls out AI to boost user personalization.</p>
<!-- ... -->

<p>Thank you for tuning in. Have a great day ahead!<br>Built by Div ❤️</p>
```

---

### Discord (Markdown)

```
📰 **Today’s Top Headlines** – India G20, Meta AI, Stock Slide

🌍 **India Hosts G20 Summit**: Leaders discuss digital innovations and global tech policies.

🧠 **Meta Rolls Out AI Tools**: New AI tools announced for improving content curation.

💼 **Merck Acquires Biotech Firm**: $10B deal finalizes for Promed Bio.

---
*Built by Div ❤️*
```

---

## 🧪 Output Quality

The workflow ensures:
- ✅ Latest news (via sort + time)
- ✅ Deduplicated headlines (case-insensitive)
- ✅ Clean summaries
- ✅ Formatted and validated email/markdown

---

## 📂 File Structure

```
Daily-Newsletter/
├── README.md
├── Daily-Newsletter.json       # Main n8n workflow
├── errorHandler.json           # Optional: Error handling workflow
├── assets/                     # Folder with screenshots of the project
│   └── error-example.png
│   └── error-workflow.png
│   └── main-workflowpng
```

---

## 💡 Future Improvements

- Telegram & Slack integrations
- Daily analytics/logs
- Multi-language news
- Web dashboard

---

## 👨‍💻 Author

Built by **Div** ❤️  
🔗 [LinkedIn](https://www.linkedin.com/in/notdiv)  
🔗 [GitHub](https://github.com/divyxshuu)

If this helps, drop a ⭐ on the repo or share your use case!

---

