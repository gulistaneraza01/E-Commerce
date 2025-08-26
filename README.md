## E‑Commerce MERN App

Modern full‑stack e‑commerce application built with the MERN stack and Vite + React on the frontend. Includes authentication, product browsing, cart/checkout, orders, payments, and admin management.

### Tech Stack

- **Client**: React, Vite, Redux Toolkit, RTK Query, React Router, Tailwind CSS
- **Server**: Node.js, Express, MongoDB (Mongoose)
- **Auth**: JWT (access tokens via HTTP‑only cookies), optional OAuth (passport scaffolded)
- **Payments**: Stripe
- **Email**: Nodemailer (via SMTP)

### Monorepo Structure

```
.
├── client/   # React + Vite frontend
└── server/   # Express + MongoDB backend
```

### Key Features

- **User**: Register, login, profile, update profile, reset password
- **Catalog**: Product listing, details, search, pagination
- **Cart**: Add/remove items, persist cart, shipping & payment selection
- **Checkout**: Place order, Stripe payment, order success screen
- **Orders**: View order details, mark paid/delivered (admin)
- **Admin**: Manage users, products (CRUD), and orders

---

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- MongoDB (local or hosted e.g. MongoDB Atlas)
- Stripe account + API keys
- SMTP credentials for outgoing email (optional but recommended)

### 1) Clone and install

```bash
git clone <your-repo-url> sparktech-youtube
cd sparktech-youtube

# Install client deps
cd client && npm install

# Install server deps
cd ../server && npm install
```

### 2) Configure environment variables

Create `server/.env` based on `server/.env.example`:

```bash
cp server/.env.example server/.env
```

Fill in values:

- **Database**: `MONGO_URI`
- **JWT**: `JWT_SECRET`
- **Stripe**: `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET` (if using webhooks)
- **Email (SMTP)**: `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASS`, `SMTP_FROM`
- **Client/Server URLs**: `CLIENT_URL`, `SERVER_URL`

Optional client variables (create `client/.env`):

```
VITE_API_URL=http://localhost:5000
```

### 3) Seed sample data (optional)

From `server/`:

```bash
# Import seed users/products
npm run data:import

# Destroy all data
npm run data:destroy
```

### 4) Run in development

Open two terminals or run concurrently.

Server (port 5000 by default):

```bash
cd server
npm run dev
```

Client (port 5173 by default):

```bash
cd client
npm run dev
```

Visit the app at `http://localhost:5173` (client) and API at `http://localhost:5000/api` (server).

---

## Scripts

### Client (`client/`)

- `npm run dev` – start Vite dev server
- `npm run build` – production build
- `npm run preview` – preview built app

### Server (`server/`)

- `npm run dev` – start server with nodemon
- `npm start` – start server (production)
- `npm run data:import` – seed DB with sample data
- `npm run data:destroy` – clear DB collections

---

## API Overview

Base URL: `/api`

- **Auth**

  - `POST /api/users/login` – login
  - `POST /api/users` – register
  - `POST /api/users/logout` – logout
  - `GET /api/users/profile` – get profile (auth)
  - `PUT /api/users/profile` – update profile (auth)

- **Users (Admin)**

  - `GET /api/users` – list users
  - `GET /api/users/:id` – get user
  - `PUT /api/users/:id` – update user
  - `DELETE /api/users/:id` – delete user

- **Products**

  - `GET /api/products` – list products (supports search & pagination)
  - `GET /api/products/:id` – product details
  - `POST /api/products` – create (admin)
  - `PUT /api/products/:id` – update (admin)
  - `DELETE /api/products/:id` – delete (admin)

- **Orders**

  - `POST /api/orders` – create order
  - `GET /api/orders/:id` – get order
  - `GET /api/orders/myorders` – my orders
  - `PUT /api/orders/:id/pay` – mark paid
  - `PUT /api/orders/:id/deliver` – mark delivered (admin)

- **Uploads**
  - `POST /api/upload` – upload product image (admin)

---

## Project Notes

- Images uploaded by admins are stored under `server/uploads/` and served statically.
- Frontend API base comes from `VITE_API_URL` or defaults to same origin proxy if configured.
- Error handling and auth middlewares live in `server/middleware/`.

---

## Production Build & Deploy

1. Build client: `cd client && npm run build`
2. Serve client build with your preferred host (e.g., Nginx, Vercel, Netlify)
3. Deploy server separately (e.g., Render, Railway, Heroku, VPS) with `server/.env` set
4. Ensure `CLIENT_URL` and CORS settings allow the deployed client domain

---
