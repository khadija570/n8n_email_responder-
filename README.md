# n8n_email_responder-
Automated Gmail assistant built in n8n with AI-generated replies, urgency detection, Slack notifications, and optional Sheets logging.

## What it does
1. Watches **unread Gmail emails**
2. Filters/flags obvious spam or low-priority emails (optional logic)
3. Uses an **AI agent** to summarize the email and extract intent
4. Detects **urgent** messages → sends a **Slack alert**
5. Detects **meeting requests** → generates a scheduling reply
6. Generates a normal reply for other emails
7. Sends the reply via Gmail
8. *(Optional)* Logs metadata/summary/response to **Google Sheets**

## Repository content
- `workflows/email_responder.SANITIZED.json` – exported workflow (no secrets)
- `.env.example` – template (no secrets)
- `.gitignore`
- `README.md`

## Import in n8n
1. Open n8n → **Workflows**
2. Click **Import from File**
3. Select `workflows/email_responder.SANITIZED.json`
4. Open the workflow and reconnect the missing credentials (see below)

## Required credentials (configure inside n8n)
> This repository does **not** include any API keys, OAuth tokens, or credentials.

Create and attach credentials to the relevant nodes:
- **Gmail OAuth2** (trigger + send/reply)
- **OpenAI / LLM credential** (AI agent nodes)
- **Slack OAuth2** (urgent alert notifications)
- **Google Sheets OAuth2** *(optional)* (logging)

## Placeholders to configure
Because this is a public export, some values are placeholders:
- `__SLACK_CHANNEL_ID__` → set your Slack channel ID
- `__GOOGLE_SHEET_DOC_ID__` → set your Google Sheet document ID (if logging is enabled)

Update them directly inside n8n after importing.

## How to run
- Activate the workflow
- Send a test email to your Gmail inbox
- Check:
  - Slack for urgent alerts
  - Drafted/sent replies in Gmail
  - Google Sheets logs (if enabled)

## Security notes
- No secrets are committed in this repository.
- Do **not** commit your real `.env` file.
- If you ever committed secrets in Git history, rotate them before making the repo public.

## License
MIT
