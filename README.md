# Streamly Telegram Bot

## Deploy with GitHub + Render

1. Upload these files to a GitHub repository.
2. In Render, create a new **Blueprint** from that repository (or create a Python Web Service manually).
3. Set these Environment Variables in Render:
   - `TOKEN` = your Telegram bot token
   - `ADMIN_ID` = your Telegram numeric user ID (multiple IDs may be comma-separated)
   - `BOT_USERNAME` = your bot username without `@` (optional)
4. Deploy. Render uses `render.yaml`; the health endpoint is `/healthz`.

## Notes

- The bot uses only Python's standard library; no third-party packages are required.
- User data is stored in `streamly_data.json`. A free Render service may lose local files when its instance is replaced/restarted; use persistent storage or external database storage for durable production data.
- Telegram Bot API 9.4 supports native `primary` (blue), `success` (green), and `danger` (red) button styles. Older Telegram clients may show default button colors.
- Telegram URL buttons must be inline buttons. The existing Owner reply-keyboard button is retained; tapping it displays a direct green URL button. Telegram does not allow a reply-keyboard button itself to open a URL.


## Video download fallback
The bot keeps its existing TikWM/SnapTik fast resolver path. If that path fails, it
falls back to yt-dlp for public TikTok posts and uploads the MP4 through Telegram.
The dependency is installed from `requirements.txt` during the Render build. Private,
restricted, deleted, or otherwise unavailable posts may still fail.
