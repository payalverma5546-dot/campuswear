# CampusWear — Backend Setup

## Stack
- React + Vite (frontend)
- Node.js + Express (REST API)
- MySQL + MySQL Workbench
- JWT + bcryptjs authentication

## 1. MySQL
1. Open MySQL Workbench and connect to your local MySQL server.
2. Open `backend/sql/schema.sql`.
3. Run the complete script. It creates the `campuswear` database and tables.

## 2. Backend environment
Inside `backend`, copy `.env.example` to `.env` and put your MySQL password in `DB_PASSWORD`. Keep `JWT_SECRET` as a long random value.

## 3. Backend install + seed
Open a terminal in `college-fashion-store/backend`:

```bash
npm install
npm run seed
npm run dev
```

The API runs at `http://localhost:5000`. Test `http://localhost:5000/api/health`.

Demo admin account:
- Admin email: the value used by your seed configuration
- Password: the value of `ADMIN_PASSWORD` in backend `.env`

## 4. Frontend
Open another terminal in `college-fashion-store`:

```bash
npm install
npm run dev
```

Optional: copy `.env.example` to `.env` if you want to change the API URL.

## 5. What is connected
- Register / Login / JWT
- User profile
- Products from MySQL API
- Cart
- Wishlist
- Saved for later
- Addresses
- Orders + order tracking
- Admin order status updates
- Product reviews
- Feedback

Card numbers/CVV are **not stored** by this demo backend. Payment is represented as a demo payment method/status only.

## Important
Run MySQL first, then backend, then frontend. You need two terminals open while developing.
