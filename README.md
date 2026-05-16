# Automated ATS-Optimized Resume Pipeline 🚀

An end-to-end automation pipeline built with **n8n** that autonomously scrapes targeted LinkedIn job postings, rewrites resume bullet points to match job descriptions using **Google Gemini**, and compiles a customized **LaTeX** PDF ready for application.

## 🏗️ System Architecture

1. **Trigger:** Runs daily at 7:00 AM via n8n Schedule node.
2. **Data Scraping:** Uses **Apify** to scrape the top 10 most recent job postings from LinkedIn based on specified keywords (e.g., "Machine Learning Engineer").
3. **Deduplication:** Queries a **Supabase** PostgreSQL database to ensure jobs haven't been processed in previous runs, saving API credits.
4. **LLM Optimization:** Fetches my master resume from Google Drive, and uses the **Google Gemini API** (LangChain Agent) to map my existing experience to the specific ATS keywords in the scraped Job Description.
5. **PDF Compilation:** Injects the optimized text into a custom, highly-formatted **LaTeX** template and compiles it into a PDF via a REST API.
6. **Delivery:** Uploads the final PDFs to Google Drive, generates shareable links, and emails a daily summary directly to my inbox via **Gmail API**.

## 🛠️ Tech Stack

* **Orchestration:** n8n (Dockerized)
* **Web Scraping:** Apify
* **Database / State Management:** Supabase (PostgreSQL)
* **AI / LLM:** Google Gemini 1.5 Pro
* **Document Processing:** LaTeX, Google Drive API
* **Notifications:** Gmail API

## 📂 Repository Structure

* `n8n-workflow.json` - The exported n8n workflow file containing all nodes and routing logic.
* `latex-compiler-node.js` - The custom JavaScript code injected into n8n to preserve my exact LaTeX formatting and styling during dynamic generation.

## 🚀 How to Run Locally

1. Import `n8n-workflow.json` into your local or self-hosted n8n instance.
2. Setup the following credentials in n8n:
   * Google Drive OAuth2
   * Gmail OAuth2
   * Supabase API Key
   * Apify API Token
   * Google Gemini API Key
3. Replace the `resumeFileId` in the "Workflow Configuration" node with your master resume Google Doc ID.
4. Activate the workflow!
