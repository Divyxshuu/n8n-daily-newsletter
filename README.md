# 📰 AI-Powered Daily News Digest with Error Monitoring (n8n) *Built by Div ❤️*

This project is an automated, multi-agent **AI-powered daily newsletter system** built in [n8n](https://n8n.io). It scrapes top news, deduplicates & formats the data, runs it through GPT-4o using OpenAI's Assistants and LangChain Agents, and sends both **email** and **Discord** versions of the digest.

It also includes a **full error-handling mechanism** that logs any failure and sends an error alert to Discord.

---

## 🚀 Key Features

- 🕗 **Scheduled Trigger**: Runs daily at 8:00 AM IST
- 🌐 **Data Sources**:
  - NewsAPI (US headlines)
  - BBC RSS Feed
- 🧹 **Data Processing**:
  - Normalize headlines
  - Remove duplicates
  - Summarize all headlines into one combined string
- 🧠 **AI Agent**:
  - Generates 2 versions: HTML Email and Markdown Discord message
  - GPT-4o with strict formatting rules
- 📤 **Multichannel Delivery**:
  - Email via Gmail
  - Message to Discord channel
- ⚠️ **Error Handling**:
  - Connected to an `Error Workflow` that sends detailed logs to Discord if anything fails

---

## 🧼 Data Preprocessing Nodes

### ✏️ Normalize Title

This node ensures consistency across all titles by:
- Lowercasing all titles to prevent case-sensitive mismatches.
- Removing unwanted characters like brackets or excessive spacing.
- Cleaning for deduplication and summarization stability.

---

### 🧹 Remove Duplicates

This custom node eliminates repeated stories across multiple feeds. It:
- Compares normalized titles using a hash or text match.
- Keeps only one unique entry per headline.
- Prevents spammy or duplicate stories in the final digest.

**Result**: From 35+ items, often reduces to 15–20 clean, unique articles.

---

### 📋 Summarize (Combiner)

This node does **not summarize** text in the AI sense, but:
- Combines all remaining news items into a single Markdown-style block.
- Preserves title + content per item using bullet formatting.

**Example Output**:
```
• US Tech Stocks Rally
The NASDAQ gained 2.3% after earnings reports beat expectations.

• UN Holds Emergency Meeting
Tensions rise in Eastern Europe as diplomats gather for crisis talks.
```

This text is then passed to the **AI Agent** for true summarization and reformatting.

---

## 🔧 Technologies Used

| Tool | Purpose |
|------|---------|
| n8n | Orchestration & automation |
| OpenAI (GPT-4o) | AI agent that creates newsletters |
| LangChain Agents | Used via n8n's AI Agent node |
| Discord Webhook | Sends the Discord version |
| Gmail API | Sends the Email version |
| NewsAPI + RSS | Scraping headline sources |

---

## 🛠️ How to Use

1. **Import the workflow** into your n8n instance.
2. Set environment variables / credentials:
   - OpenAI API Key
   - NewsAPI Key
   - Gmail account OAuth2
   - Discord Webhook URL
3. Connect an **error handler workflow** named exactly as:  
   `c7p7X0X8RZtYvgaB` or rename accordingly in the `errorWorkflow` settings.
4. **Enable scheduling** at 8:00 AM IST (adjust in Schedule Trigger if needed).

---

## 💡 Agent Prompt Design (System Message)

- Generates **exactly two** versions:  
  1. 📨 HTML version for Email  
  2. 💬 Markdown version for Discord  
- Validates formatting, no placeholders, no markdown in emails, and properly structured responses for both platforms.

---

## 🧠 Why This Matters

This project demonstrates:
- Real-world **multi-agent orchestration**
- **AI content generation** across formats
- **Robust error handling**
- Integration of **LLMs into low-code automation**

---

## 📸 Optional Screenshot Suggestion

> In assests\ Folder

---

## 📬 Example Output

**Discord Version**  
```
📰 **Today’s Top Headlines** – Tech, politics, and AI lead the day

🌍 **China Expands AI Regulation**: New rules tighten oversight on open-source models.

📉 **US Job Market Cools Slightly**: July reports show a slowdown in hiring.

...

---
*Built by Div ❤️*
```

**Email Version**  
Sent via Gmail as an HTML digest.

---

## 👤 Author

Built by **Div** as part of AI Internship Projects  
🔗 [LinkedIn](https://www.linkedin.com/in/notdiv)  
🔗 [GitHub](https://github.com/divyxshuu)
