# SpamShield Email Classifier

Login-based spam/fraud email classifier with:
- local rule + Naive Bayes model
- optional external AI classification (Gemini/OpenAI)
- Gmail OAuth inbox scanner
- demo proxy email and sample inbox data

## Run locally

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/python app.py
```

Open `http://127.0.0.1:5000`.

## Demo credentials

- Username: `demo_user`
- Password: `Demo@12345`

## Enable Gemini or OpenAI

1. Copy `.env.example` to `.env`
2. Fill keys
3. Set:
   - `USE_EXTERNAL_AI=true`
   - `AI_PROVIDER=gemini` or `openai`

If external API fails or key is missing, app automatically falls back to local model.

## Connect real Gmail inbox

Create Google OAuth Web credentials and set:
- `GMAIL_CLIENT_ID`
- `GMAIL_CLIENT_SECRET`
- `GMAIL_REDIRECT_URI` (example: `https://your-app.onrender.com/gmail/callback`)

In Google Cloud OAuth settings, add the same redirect URI.
Then use **Connect Gmail** from the dashboard and run **Scan Latest Gmail Emails**.

## Deploy online (Render)

This repo includes `render.yaml` for one-click Blueprint deploy.

1. Open [Render Blueprint](https://dashboard.render.com/blueprint/new)
2. Connect your GitHub and select this repo
3. Add `GEMINI_API_KEY` when prompted
4. Deploy

Service will use:
- Build: `pip install -r requirements.txt`
- Start: `gunicorn app:app --bind 0.0.0.0:$PORT`

Note: free instances can sleep. Add a persistent disk if you want `emails.db` kept across restarts.
