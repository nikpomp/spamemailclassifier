# SpamShield Email Classifier

Login-based spam/fraud email classifier with:
- local rule + Naive Bayes model
- optional external AI classification (Gemini/OpenAI)
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

## Deploy online (Render/Railway)

- Use start command: `python app.py`
- Set environment variables from `.env.example`
- Add a persistent disk if you want `emails.db` saved across restarts
