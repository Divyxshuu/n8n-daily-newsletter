# 🗞️ AI Daily Newsletter Bot (n8n) – Built by Div ❤️

This project is a fully automated AI-powered newsletter generator using **n8n**, designed to deliver **daily world news summaries** in **HTML email** (via Gmail) and **Discord** (Markdown). It now includes error handling with **Discord alerts** if critical services (like APIs or AI models) fail.

---

## 📌 Features

- ⏰ **Daily Scheduled Trigger** (e.g., 8 AM IST)
- 📰 Combines sources from:
  - Trusted **RSS feeds**
  - Verified **NewsAPI** headlines
- 🧠 **AI-generated summaries** via GPT-4o (OpenAI)
- 📤 Delivers to **Gmail (HTML)** and **Discord (Markdown)**
- 🧹 Automatically:
  - Sorts by freshness
  - Limits to 25 headlines
  - Deduplicates by lowercase titles
- ❗ **Error notifications sent to Discord**
- 💡 Built low-code with **n8n** – fully customizable and modular

---

## 🔁 Workflow Overview

```plaintext
Schedule Trigger (Daily 8 AM)
   ├── RSS Read
   └── HTTP Request (NewsAPI) 
        ├── 🔁 On Error → Discord_Error1 (sends API error notice to Discord)
           ↓
        Split Out (extracts articles array)
           ↓
        Merge (append articles from both sources)
           ↓
        Sort (by pubDate & publishedAt descending)
           ↓
        Limit (top 25 items)
           ↓
        Normalize (manually extract titles)
           ↓
        Remove Duplicates (based on lowercase title)
           ↓
        Summarize (combine titles + content into one string)
           ↓
        AI Agent (ChatGPT-4o)
            ├── Gmail Tool (HTML email)
            ├── Discord Tool (Markdown message)
            └── 🔁 On Error → Discord_Error2 (sends OpenAI/Agent fail notice to Discord)
```

---

## ⚙️ Setup Guide

### 1. 🔧 Requirements

- [n8n](https://n8n.io) (self-hosted or desktop)
- NewsAPI Key (get from [https://newsapi.org](https://newsapi.org))
- OpenAI API Key (ChatGPT-4o supported)
- Gmail credentials (OAuth2)
- Discord webhook (or legacy integration)

---

### 2. 🔑 Credentials & API Safety

- **✅ Your API keys are NOT hardcoded** in the workflow
- **NewsAPI** is used via **HTTP Node** using:
  - Auth: `Generic Auth → Bearer Token`
- **OpenAI** used via **ChatGPT Tool Node** (no .env file required)
- Email and webhook fields are **manually entered**, but editable:
  - Set `"enter-your-email"` in the `.json` before uploading
- To avoid exposing your email/API key on GitHub:
  - ✅ Remove sensitive values before commit
  - ✅ Use `Credentials` in n8n to manage tokens securely

---

### 3. 📬 Agent Prompt (Built-in)

- Generates **2 separate outputs** every run:

#### ✅ Gmail Output (HTML)
- Full HTML email with emojis, subject line, greeting, and 12–15 real headlines

#### ✅ Discord Output (Markdown)
- Discord-friendly formatting with **bolded headlines**, emojis, and one-liner summaries

---

## 🧪 Output Quality

The workflow ensures:

- ✅ **Real-time freshness** (via time-based sort)
- ✅ **Deduplicated** headlines (case-insensitive)
- ✅ **Fallback logic** (if summary is missing)
- ✅ **Graceful failover** with Discord alerts if:
  - NewsAPI fails (invalid/missing key or quota limit)
  - OpenAI node fails (invalid key, timeout, etc.)

---

## 📂 Project Structure

```bash
Daily-Newsletter/
├── README.md                    # This file
├── Daily-Newsletter.json        # Main newsletter workflow
├── errorHandler.json            # Optional error-only workflow
├── assets/                      # Screenshots and visuals
│   ├── main-workflow.png
│   ├── error-example.png
│   └── error-workflow.png
```

---

## 🧠 Example Output

### Gmail (HTML):
```html
<h2>📰 Today’s Top Headlines</h2>
<p>Hello! Here's a quick look at today’s most important global stories:</p>

<p>🌍 <b>India Hosts G20 Summit</b>: Global leaders discuss digital economy policies.</p>
<p>🧠 <b>Meta Unveils New AI Tools</b>: Meta rolls out AI to boost personalization.</p>

<p>Thank you for tuning in. Have a great day ahead!<br>Built by Div ❤️</p>
```

### Discord (Markdown):

```
📰 **Today’s Top Headlines** – G20 Summit, Meta AI, Bitcoin Surge

🌍 **India Hosts G20**: Global leaders discuss economic and tech policy.

🧠 **Meta Unveils AI Tools**: New tools for personalization announced at event.

💼 **Bitcoin Hits $110k**: Crypto surges amid global ETF demand.

---
*Built by Div ❤️*
```

---

## 🚨 Error Handling (NEW)

If any of these fail:
- ❌ NewsAPI fails (401, 429, network) → Triggers `Discord_Error1` 
- ❌ OpenAI/Agent fails → Triggers `Discord_Error2`
- ❌ Any Other Error in workflow -> Error Workflow Triggered -> Discord Alert  
> You'll receive an error message via Discord webhook instantly.

---

## 💡 Future Upgrades

- 🔄 Telegram or Slack delivery
- 🌐 Web dashboard or archive
- 🧭 Multi-language news
- 📊 Newsletter analytics

---

## 👨‍💻 Author

**Built by Div ❤️**

- [🔗 LinkedIn](https://www.linkedin.com/in/notdiv/)
- [🔗 GitHub](https://github.com/divcreates)

---

If this helps, drop a ⭐ on the repo!

