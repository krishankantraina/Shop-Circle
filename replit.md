# Shop Circle

## Overview

Shop Circle is a full-stack service marketplace web application with three user roles: User, Vendor, and Admin. It supports browsing services (Rentals, Stays, Shopping), booking, mock payment processing, and role-based dashboards.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite + Tailwind CSS (artifacts/shop-circle)
- **API framework**: Express 5 (artifacts/api-server)
- **Database**: PostgreSQL + Drizzle ORM
- **Auth**: JWT (jsonwebtoken + bcryptjs)
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Demo Accounts

| Role   | Email                   | Password   |
|--------|-------------------------|------------|
| Admin  | admin@shopcircle.com    | admin123   |
| Vendor | vendor@shopcircle.com   | vendor123  |
| User   | user@shopcircle.com     | user123    |

## Key Features

### User Panel
- Signup/Login with JWT auth
- Browse services (Rentals, Stays, Shopping) with search & filter
- View service details + booking form
- Mock payment flow (simulate payment)
- View booking history and status

### Vendor Panel
- Manage service listings (create, edit, delete)
- View incoming bookings (accept/reject/complete)
- Dashboard with revenue and booking stats

### Admin Panel
- Dashboard with total users, vendors, bookings, revenue
- Manage users (activate/deactivate/delete)
- Approve/reject vendor service listings
- Monitor all transactions

## Project Structure

```
artifacts/
  api-server/          # Express 5 backend
    src/
      routes/          # Route handlers (auth, services, bookings, payments, vendor, admin)
      middlewares/     # Auth middleware (JWT)
      lib/             # Logger
  shop-circle/         # React + Vite frontend
    src/
      pages/           # All page components
      components/      # Shared UI components
lib/
  api-spec/            # OpenAPI spec
  api-client-react/    # Generated React Query hooks
  api-zod/             # Generated Zod schemas
  db/                  # Drizzle ORM + PostgreSQL schema
```

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas
- `pnpm --filter @workspace/db run push` — push DB schema changes
- `pnpm --filter @workspace/api-server run dev` — run API server
- `pnpm --filter @workspace/shop-circle run dev` — run frontend

## API Endpoints

- `POST /api/auth/register` — Register (role: user/vendor)
- `POST /api/auth/login` — Login, returns JWT
- `GET /api/auth/me` — Get current user
- `GET /api/services` — List approved services (supports ?category, search, minPrice, maxPrice)
- `GET /api/services/featured` — Featured services
- `GET /api/services/:id` — Service details
- `POST /api/services` — Create service (vendor)
- `PUT /api/services/:id` — Update service
- `DELETE /api/services/:id` — Delete service
- `GET /api/bookings` — List bookings (role-filtered)
- `POST /api/bookings` — Create booking (user)
- `GET /api/bookings/:id` — Booking detail
- `PUT /api/bookings/:id/status` — Update booking status
- `POST /api/payments/initiate` — Start payment
- `POST /api/payments/confirm` — Confirm/simulate payment
- `GET /api/payments` — List payments
- `GET /api/vendor/services` — Vendor's services
- `GET /api/vendor/bookings` — Vendor's bookings
- `GET /api/vendor/dashboard` — Vendor stats
- `GET /api/admin/dashboard` — Admin stats
- `GET /api/admin/users` — All users
- `PUT /api/admin/users/:id` — Update user
- `DELETE /api/admin/users/:id` — Delete user
- `GET /api/admin/services` — All services
- `PUT /api/admin/services/:id/approve` — Approve/reject service
- `GET /api/admin/transactions` — All transactions
