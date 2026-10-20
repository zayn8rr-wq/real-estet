# LeadFlow Real Estate Website

Responsive landing page, enquiry form, Express backend, configurable WhatsApp button and optional Google Sheets receiver.

## Important before sending to a client
- Featured listings, names and prices are placeholders; replace with verified properties.
- Set the real business WhatsApp number.
- For production lead retention, connect Google Sheets or a database. Without a webhook, leads append to `data/leads.jsonl`, which may not persist on cloud hosts.
- Do not claim live testing is complete until deployed and tested with dummy data.

## Run locally
Requires Node.js 18+. Copy `.env.example` to `.env`, set `WHATSAPP_NUMBER` to international digits only (India example `919876543210`), then run `npm install` and `npm start`. Open http://localhost:3000.

## Google Sheets setup (recommended)
1. Create a Google Sheet and copy the ID from its URL (`/spreadsheets/d/ID/edit`).
2. Extensions → Apps Script; paste `google-apps-script.gs`; replace `SHEET_ID`.
3. Deploy → New deployment → Web app; Execute as **Me**, access **Anyone**. Treat the deployed URL as a secret.
4. Copy the `/exec` URL to hosting env var `GOOGLE_SHEETS_WEBHOOK_URL`. Also set `WHATSAPP_NUMBER`. Redeploy.
5. Submit a dummy enquiry and verify a row appears in the `Leads` tab. If webhook delivery fails, the form shows an error, not success.

## Deploy to Render
1. Push this folder to a GitHub repository.
2. Render → New → Web Service → connect repo. Root directory is folder containing `package.json`.
3. Build command: `npm install`; Start command: `npm start`.
4. Add environment variables `WHATSAPP_NUMBER` and (recommended) `GOOGLE_SHEETS_WEBHOOK_URL`. Deploy.
5. Test the live form, verify the Sheet row, and click WhatsApp to confirm the right chat and prefilled message.

## Files
- `public/index.html`: landing page and sample properties
- `public/styles.css`: responsive styling
- `public/app.js`: form, validation, WhatsApp flow
- `server.js`: API and server-side lead handling
- `google-apps-script.gs`: optional Google Sheets webhook
- `.env.example`: environment settings

Production hardening: add rate limiting/spam protection, privacy policy/consent text, monitoring and appropriate access controls. Apps Script URL is a secret; rotate it if exposed.
