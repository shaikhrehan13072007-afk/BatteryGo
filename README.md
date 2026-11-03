# BatteryGo — React + Express + MongoDB

A Vercel-ready full-stack starter for a battery ecommerce and delivery platform.

## Stack
- React + Vite + React Router
- Express API (Vercel serverless entry at `api/index.js`)
- MongoDB Atlas + Mongoose
- JWT authentication, password login, email OTP flow
- Razorpay order creation / verification (COD is also supported)
- Cloudinary-ready product image URL field
- Customer, Admin and Delivery dashboards

## Local setup

### 1. Install
```bash
npm install
npm install --prefix client
npm install --prefix server
```

### 2. Configure environment
Copy `server/.env.example` to `server/.env` and fill in values.
For local development, run the API from `server` and the React app from `client`.

```bash
cd server
npm run dev
```
In another terminal:
```bash
cd client
npm run dev
```
Vite proxies `/api` to `http://localhost:5000`.

### 3. Create the first admin
Register a user normally, then promote that account in MongoDB Atlas:
```js
db.users.updateOne({ email: "admin@example.com" }, { $set: { role: "admin" } })
```
Do not expose admin registration publicly.

## Vercel deployment
1. Push this folder to GitHub.
2. Import the repository in Vercel.
3. Add the environment variables from `server/.env.example` in Vercel Project Settings.
4. Set Root Directory to the repository root.
5. Build command: `npm run build`
6. Output directory: `client/dist`
7. Deploy. `vercel.json` routes `/api/*` to `api/index.js` and all other routes to the SPA.
8. Add your deployed domain to `CLIENT_URL` and configure Razorpay/Cloudinary provider settings.

## Important integrations
- **Razorpay:** set `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET`. Online checkout is disabled until configured. COD works without keys.
- **Email OTP:** configure SMTP variables. Without SMTP, OTP is logged only in development; never use that mode in production.
- **SMS OTP:** mobile OTP is not activated in this starter because it requires your SMS provider account, sender/template approval and credentials. Connect MSG91 or Twilio before enabling mobile OTP in production. Email OTP API is included; password login/registration is active.
- **Images:** upload product images to Cloudinary or another image host and store the resulting HTTPS URL in `imageUrl`.
- Add rate limiting, CAPTCHA, email verification, privacy policy, terms, refund policy, tax/shipping rules and production monitoring before public launch.

This is a deployable foundation, not a substitute for configuring and testing your real payment, SMS, email and business credentials.
"# BatteryGo" 
