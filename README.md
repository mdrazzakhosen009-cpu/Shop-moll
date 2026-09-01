# SAREE Premium — Turso Production Rebuild

Node.js + Express + Turso + Groq. The browser, admin panel and backend use the same API and the same Turso database.

## Repository root
```text
.env.example
package.json
server.js
render.yaml
README.md
public/index.html
public/style.css
public/app.js
admin/index.html
admin/admin.css
admin/admin.js
```

## Render
Root Directory: **blank**
Build Command: `npm install`
Start Command: `npm start`

## Environment Variables
- `TURSO_DATABASE_URL` — your `libsql://...` URL
- `TURSO_AUTH_TOKEN` — a fresh Turso auth token
- `ADMIN_PASSWORD` — initial admin password on first database setup
- `GROQ_API_KEY` — Groq key
- `GROQ_MODEL` — optional; defaults to a Groq model configured in the server
- `SESSION_SECRET` — optional; a random value is recommended

## Persistent data
Products, product images, agents, orders, order tracking data, store/payment/delivery settings, chatbot quick options, logo data and the admin password hash are persisted in Turso. Product and logo images are stored as base64 data URLs in Turso, so the app does not depend on Render's ephemeral filesystem for these assets.

## Working admin flows
- Product add/edit/delete
- Product image upload
- Agent add/edit/delete
- Order status updates
- Store/payment/delivery settings
- Chatbot quick options
- Logo upload
- Theme selection
- Password change
- Live dashboard counts/revenue

## AI
Groq powers the shopping assistant and catalog-aware responses. The customer image matching endpoint sends the uploaded image to the configured Groq vision-capable model and validates returned product IDs against the live Turso catalog. If your Groq account/model does not support vision, the endpoint returns a safe error instead of pretending matching succeeded.

## Security
Never commit real Turso tokens, Groq keys or passwords to GitHub. Set them only in Render Environment Variables.
