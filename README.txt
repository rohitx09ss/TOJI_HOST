TOJI HOST — Render deployment bundle

1) Upload this folder/repository to GitHub.
2) In Render choose New + > Blueprint and select the repository (render.yaml),
   OR create a Web Service manually with:
   Build Command: pip install -r requirements.txt
   Start Command: python TOJI_HOST.py
3) Add Environment Variables in Render:
   BOT_TOKEN = your Telegram bot token
   OWNER_ID = your Telegram numeric user ID
   ADMIN_ID = admin Telegram numeric ID (if different)
   FAMWAY_API_KEY = your FamWay API key (optional if auto-pay is disabled)
   FAMWAY_BASE = https://famway.onrender.com
   BOT_URL = https://YOUR-SERVICE-NAME.onrender.com
   MANUAL_UPI_ID = rohit.hacrr@fam
4) Deploy and open https://YOUR-SERVICE-NAME.onrender.com/health
   Expected response: {"service":"toji-host-bot","status":"ok"}
5) UptimeRobot:
   - Create an HTTP(s) monitor
   - URL: https://YOUR-SERVICE-NAME.onrender.com/health
   - Monitoring interval: 5 minutes (if available on your plan)

Important:
- Render Free web services may spin down after inactivity. External pings can
  keep activity flowing but are not a guarantee of permanent 24/7 uptime.
- Local SQLite database and uploaded files are on the service filesystem. On
  Render Free, filesystem data is ephemeral and can be lost on redeploy/restart.
  Use a paid persistent disk or move database/files to managed persistent storage
  before relying on this for real users/payments.
- Never put secrets in GitHub. Set them only in Render Environment settings.
- Manual UPI QR payments require admin verification; this does not auto-credit.
- Running arbitrary customer Python/JS code on the same host is unsafe without
  OS/container isolation, resource limits and strict sandboxing.
