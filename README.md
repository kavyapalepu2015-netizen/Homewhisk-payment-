# HomeWhisk 🍰

**Homemade Treats, Made with Love**

A full-stack Home Bakery Order Management System built with:

- Java 17+
- Spring Boot
- Spring Web / REST
- Spring Data JPA + Hibernate
- MySQL
- React + Vite
- Git + GitHub

## Features

### Customer
- Browse homemade bakery products
- Search/filter products
- Customize cake orders
- Add products to cart
- Select quantity and delivery date
- Place an order
- View order confirmation and total
- Track delivery status

### Baker
- View all orders
- See customer and customization details
- Update order status
- Dashboard statistics

## Project structure

```text
HomeWhisk/
├── frontend/       # React + Vite
├── backend/        # Spring Boot REST API
├── database/       # MySQL schema
└── docs/           # API notes
```

## Run locally

### 1. Database

Create a MySQL database:

```sql
CREATE DATABASE homewhisk;
```

Or import `database/schema.sql`.

### 2. Backend

Requirements: Java 17+ and Maven.

Edit `backend/src/main/resources/application.properties` if your MySQL username/password differ.

```bash
cd backend
mvn spring-boot:run
```

Backend:
`http://localhost:8080`

### 3. Frontend

Requirements: Node.js 18+.

```bash
cd frontend
npm install
npm run dev
```

Frontend:
`http://localhost:5173`

The Vite development server proxies `/api` requests to Spring Boot.

## GitHub Pages note

GitHub Pages can host the **React frontend**, but it cannot run the Spring Boot server or MySQL database.

For a full deployed application:
- Frontend: GitHub Pages / Vercel / Netlify
- Backend: Render / Railway / another Java-capable host
- Database: MySQL-compatible hosted database

After deploying the backend, set:

```text
frontend/.env.production
VITE_API_BASE_URL=https://YOUR-BACKEND-URL
```

Then build the frontend:

```bash
npm run build
```

## API

See `docs/API.md`.

## Assignment mapping

| Requirement | Implementation |
|---|---|
| Java 17+ | Spring Boot backend |
| React | `frontend/` |
| REST API | `/api/...` |
| JPA/Hibernate | Entities + repositories |
| MySQL | `application.properties` + schema |
| Validation | Jakarta Bean Validation |
| HTTP status codes | `ResponseEntity` + exception handler |
| Responsive UI | CSS responsive layout |
| Order confirmation | Customer confirmation screen |
| Customization summary | Order details |
| Delivery status | Order status endpoint |
| Baker management | Baker dashboard |
| GitHub | Repository-ready structure |

## Suggested meaningful commits

```text
feat: create React bakery storefront
feat: add product customization and cart
feat: add Spring Boot order APIs
feat: add JPA entities and MySQL persistence
feat: add baker order management
docs: add setup and API documentation
```

## Payment setup (Razorpay)

The checkout now uses Razorpay Checkout with server-side payment-order creation and HMAC signature verification.

1. Create a Razorpay account and use **Test Mode** keys while developing.
2. Set these backend environment variables:
   - `RAZORPAY_KEY_ID=rzp_test_...`
   - `RAZORPAY_KEY_SECRET=...`
3. Start the Spring Boot API on port 8080 and the Vite frontend.
4. Add items to the cart and click **Pay & Place Order**.
5. The backend creates a Razorpay order; the browser opens Razorpay Checkout; the backend verifies the returned signature before the HomeWhisk order is created.

Never commit `RAZORPAY_KEY_SECRET` to GitHub. Use GitHub Actions/hosting environment secrets for deployment.
