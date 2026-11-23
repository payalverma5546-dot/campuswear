# CampusWear — Gen-Z Ecommerce Demo

CampusWear is a React + Node/Express + MySQL ecommerce project for a college-fashion storefront.

## Included in this build

- Gen-Z responsive storefront with light/dark mode
- Dynamic hero, trending, new arrivals, top-rated, budget rail and recently viewed
- Category and gift discovery pages
- Case-insensitive advanced product search with live suggestions
- Server-side filters, sorting and pagination
- Product details with size/colour variants, variant stock/SKU and variant images
- Size guide, reviews and approved-review moderation flow
- Guest cart + guest wishlist with login synchronization
- Cart quantity controls, save for later and free-delivery progress
- Checkout with demo payment methods and coupon/discount validation (no real payment gateway)
- Order tracking timeline
- Account dashboard and secure logout experience
- Admin dashboard with inventory, variants, coupons, review moderation, orders, feedback and analytics
- Local upload fallback + S3-compatible production image storage
- MySQL backup download + scheduled backup support
- Helmet, rate limiting, JWT expiry and upload limits
- Docker/NGINX production deployment files

## Run locally

### Backend

```bash
cd backend
npm install
# copy .env.example to .env and set DB credentials
npm run seed
npm run dev
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Frontend defaults to `http://localhost:5173` and backend to `http://localhost:5000`.

## Demo admin

- Admin email: the value used by your seed configuration
- Password: the value of `ADMIN_PASSWORD` in backend `.env`

Change this credential before any real deployment.

## Production notes

- Set a strong `JWT_SECRET` (32+ characters).
- Configure MySQL credentials and a restricted database user.
- For production images, configure the S3-compatible variables in `backend/.env`.
- Put the frontend/backend behind HTTPS.
- Configure `BACKUP_INTERVAL_HOURS` and keep backup files off the application server as an additional backup strategy.
- This project intentionally does not include a real payment gateway.

## Recent CampusWear UI updates

- Replaced the old home-page marquee with a **Campus Offers** section for Hisar student audiences.
- Added college-specific demo coupon cards for GJUST, CCS HAU, LUVAS, Polytechnic, CRM Jat College and Government College.
- Added **Room Reset** as a new Gen-Z category for room/hostel decoration.
- Added Room Reset products to the backend seed catalogue.
- Enlarged category hero/banner imagery so each category section has a stronger, more complete visual.
- Kept the main project folder name exactly **campuswear**.

> Coupon codes in the UI are demo/project offers and should be connected to your actual coupon rules before production use.


## Student coupon verification
CampusWear now supports college-specific student coupons. Email-verifiable colleges use an official institutional email-domain OTP; colleges without a verifiable student-email domain can use manual admin review. Student-only coupons are blocked by the backend until verification succeeds. For real email delivery, configure `RESEND_API_KEY` and `EMAIL_FROM` in `backend/.env`. For local-only testing, `ALLOW_DEV_OTP=true` shows the OTP in development responses; never enable that in production.

### Database organization
The project uses separate relational tables for users, addresses, categories, subcategories, products, product images, variants, carts, wishlists, orders, reviews, colleges, student verification, coupons, homepage content and gift collections. The `products` table stores product master data; merchandising content is not mixed into it.


## Final production-readiness additions
- independently scrollable Categories filter on desktop/mobile
- product comparison (up to 4 items)
- fuzzy/synonym-aware product search
- recently-viewed API for signed-in users
- price-drop and back-in-stock alerts
- production Docker Compose with health checks and reverse-proxied API
- production security headers and disabled development OTP/email behavior
- deployment and environment templates

## COD + Shiprocket courier workflow

CampusWear enforces Cash on Delivery at the backend and provides an optional Shiprocket integration for admins to create shipments, check serviceable couriers, assign an AWB and sync tracking events. Configure credentials and the exact pickup location in `backend/.env`; see [`SHIPROCKET_SETUP.md`](./SHIPROCKET_SETUP.md) for setup steps, endpoints and operational limitations. No Shiprocket credentials are bundled with this project, so the live account/API workflow must be verified after configuration.

## Latest COD + Shiprocket work (21 October 2026)

- COD remains the only enabled checkout payment method.
- Shiprocket admin workflow now supports creating the courier order, fetching serviceable courier options, assigning an AWB, requesting pickup, and synchronizing tracking events.
- Pickup requests are guarded against accidental repeat submissions once CampusWear has saved a successful request. Verify actual pickup acceptance in the Shiprocket dashboard.
- Added database migrations for Shiprocket pickup status and request timestamp.
- Fixed a JSX syntax error in the product review photo gallery.

### Verification status

- Backend syntax checks: passed.
- Backend automated tests: 6 passed.
- Frontend JSX syntax parsing: 49 JSX files parsed without syntax errors using the installed TypeScript parser.
- Vite production build: not run successfully because frontend dependencies could not be installed in this environment (`vite` unavailable; npm registry/cache unavailable). Run `npm ci` and `npm run build` from `frontend/` on a machine with registry access before deployment.
- Live Shiprocket API, credentials, database migration, pickup booking and delivery remain unverified until configured with a real merchant account.
