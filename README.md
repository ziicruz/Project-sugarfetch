# Project-sugarfetch

# Project Sugar Frontend

Frontend application for Sugar Cafe. This app serves three user flows:

- Customer ordering and tracking
- Admin operations (orders, menu, analytics)
- Super admin operations (admin management and reports)

## Stack

- React + Vite
- React Router
- React Query (`@tanstack/react-query`)
- Zod validation
- UI components (Radix + MUI)

## Prerequisites

- Node.js 20+
- npm
- Running Sugar API backend

## Environment Variables

Create `.env` in the frontend root:

```env
VITE_API_BASE_URL=http://localhost:3000
```

If not provided, hooks default to `http://localhost:3000`.

## Run Locally

Install dependencies:

```bash
npm install
```

Start dev server:

```bash
npm run dev
```

Default URL:

- `http://localhost:5173`

## Available Scripts

- `npm run dev` - start development server
- `npm run build` - production build

## Route Map

### Customer

- `/` - QR landing page
- `/menu` - menu browsing
- `/cart` - cart page
- `/order-confirmation` - order confirmation summary
- `/payment` - payment form and proof upload
- `/tracking` - payment/order status tracking

### Admin

- `/admin` - admin login
- `/admin/dashboard` - dashboard overview
- `/admin/orders` - order management
- `/admin/menu-management` - menu CRUD
- `/admin/analytics` - sales analytics and export

### Super Admin

- `/super-admin` - super admin login
- `/super-admin/dashboard` - super admin dashboard
- `/super-admin/admins` - admin account management
- `/super-admin/z-read` - Z-read/report page

## API Integration

This frontend consumes the Sugar API endpoints:

- Auth: `/admins/login`, `/super-admins/login`, `/admins` (register admin)
- Menu: `/menus`, `/menus/:id`
- Payments: `/payments`, `/payments/track/:id`, `/payments/:id/status`, `/payments/:id/confirm`
- Orders: `/orders`, `/orders/:id/status`, `/orders/:id/confirm`
- Analytics: `/analytics/dashboard`, `/analytics/sales`, `/analytics/export`

## Auth Behavior

- Admin login stores JWT in cookie: `admin_token`
- Super admin login stores JWT in cookie: `super_admin_token`
- Protected requests include `Authorization: Bearer <token>` from those cookies

## Core Frontend Modules

- `src/app/routes.ts` - browser routing config
- `src/hooks/useAuth.ts` - login and admin creation flows
- `src/hooks/useMenu.ts` - menu queries and mutations
- `src/hooks/usePayment.ts` - payment creation/tracking/admin payment actions
- `src/hooks/useOrderManagement.ts` - order listing, filtering, status updates
- `src/hooks/useAnalytics.ts` - dashboard/sales analytics and export
- `src/app/context/CartContext.tsx` - customer cart state

## Notes

- Payment creation uses multipart upload and sends field `paymentImage`.
- Menu create/update can include image upload and availability scheduling.
- Analytics export supports CSV and PDF download via backend.

## Deployment

For production deployment, set:

- `VITE_API_BASE_URL` to your deployed API URL (for example, Cloud Run URL).

Then run:

```bash
npm run build
```
  
