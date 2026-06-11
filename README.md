
# PulseCopy | High-Performance Forex Terminal (Self-Hosted Edition)

This is a Next.js application designed for ultra-low latency trade mirroring. It is fully "Hostinger-ready" and configured for self-hosting on your own domain.

## Deployment to Hostinger VPS (Ubuntu/Node.js)

To run this on your Hostinger server with your own domain:

1. **Server Setup:**
   - Log into your Hostinger VPS via SSH.
   - Install Node.js: `curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - && sudo apt-get install -y nodejs`
   - Install PM2: `npm install -g pm2`

2. **Upload & Build:**
   - Upload your project files to the server.
   - Create a `.env.local` file with your Firebase credentials (for the underlying persistence).
   - Run `npm install`
   - Run `npm run build`

3. **Launch with PM2:**
   - `pm2 start npm --name "pulsecopy" -- start`

4. **Self-Hosted API Bridge:**
   - Your MT5 terminal now connects directly to your domain via `https://your-domain.com/api/signals`.
   - This removes the need for MT5 to talk directly to Google, providing a professional, branded experience.

## Hostinger + MySQL Setup

1. Create the MySQL database in Hostinger Cloudpanel:
   - Go to Databases > MySQL Databases.
   - Create database `igrowdb`.
   - Create user `igrowdb1` with the password you configured in Hostinger.
   - Assign the user to the database with full privileges.

2. Import the SQL schema:
   - Open phpMyAdmin for the `igrowdb` database.
   - Import `sql/signals-schema.sql`.
   - This creates tables for `signals`, `master_connections`, `followers`, `bridges`, and `ledger_entries`.

3. Configure your app environment:
   - Either set environment variables in Hostinger Node.js app configuration or upload a `.env.local` file to the project root.
   - Use `.env.local.example` as a template.
   - Example values:
     - `NEXT_PUBLIC_APP_DOMAIN=https://www.igrowlearningsociety.in`
     - `DB_HOST=localhost`
     - `DB_PORT=3306`
     - `DB_USER=igrow`
     - `DB_PASSWORD=vwq49HDW9GrgF1wOYqn6`
     - `DB_NAME=igrowdb`

4. Install and build on Hostinger:
   - `npm install`
   - `npm run build`

5. Start the app:
   - `npm start`
   - Or use PM2: `pm2 start npm --name "tradinggrow" -- start`

6. Set your domain and SSL:
   - Configure your Hostinger domain to point at the Node.js app.
   - Enable HTTPS so `https://www.igrowlearningsociety.in/api/signals` is available.

7. MT5 setup:
   - In MT5, add `https://www.igrowlearningsociety.in` to WebRequest allowed URLs.
   - Use the bridge endpoint `https://www.igrowlearningsociety.in/api/signals` in your MQL5 Bridge code.

## Database & Persistence

- **Why Firestore?** We use Firestore as the underlying persistence engine because it handles real-time syncing and concurrency far better than a standard MySQL setup for high-frequency trading.
- **Migration to MySQL:** If you wish to use your **phpMyAdmin** database for account ledger data, you can extend the `src/app/api/signals/route.ts` to log orders into your MySQL database using the `mysql2` package.

## MT5 Setup Checklist

1. Open MT5 -> Tools -> Options -> Expert Advisors.
2. Check "Allow WebRequest for listed URL".
3. Add **YOUR DOMAIN URL** (e.g., `https://your-domain.com`) to the list.
4. Copy the MQL5 code from the "Bridge" tab in your terminal.
