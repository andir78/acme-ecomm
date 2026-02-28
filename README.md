# Full stack application for ACME inc.

This repo is a demonstrator purely to acquire some practical experience in:-
- Domain driven design
- React/Node front end

The end user (ACME inc.) is completely fictional.

## MVP Requirements - Feature List

This file lists the MVP features for the Acme Widgets e‑commerce app. Each feature includes short acceptance criteria, related entities, and primary API endpoints.

## 1) User accounts & auth (high)
- Features: sign up, login (JWT), logout, profile read/update, password reset (email stub).
- Acceptance: register -> receive token; protected endpoints require valid token.
- Entities: User
- Endpoints:
  - POST /api/auth/register
  - POST /api/auth/login
  - POST /api/auth/logout
  - GET /api/users/me
  - PATCH /api/users/me
  - POST /api/auth/password-reset (stub)

## 2) Product catalog (high)
- Features: list products, product detail, search/filter (category, price), pagination, image URLs.
- Acceptance: public paginated list and single product view.
- Entities: Product
- Endpoints:
  - GET /api/products
  - GET /api/products/:id
  - GET /api/products?search=&category=&min=&max=&page=&limit=
  - POST /api/products (admin)
  - PATCH /api/products/:id (admin)
  - DELETE /api/products/:id (admin)

## 3) Shopping cart (high)
- Features: add/remove/update cart items, view cart; persist cart for authenticated users.
- Acceptance: client can manage cart and see item totals.
- Entities: Order (cart state), OrderItem
- Endpoints:
  - GET /api/cart
  - POST /api/cart/items
  - PATCH /api/cart/items/:itemId
  - DELETE /api/cart/items/:itemId
  - POST /api/cart/merge (optional for guest->user)

## 4) Checkout & Orders (high)
- Features: create order from cart, order summary, order history, order status (pending, paid, shipped, cancelled). Payment = stub.
- Acceptance: orders persisted, totals computed, items stored.
- Entities: Order, OrderItem, User, Product
- Endpoints:
  - POST /api/orders
  - GET /api/orders/:id
  - GET /api/orders (user)
  - PATCH /api/orders/:id (admin: update status)

## 5) Inventory basics (medium)
- Features: product stock quantity, prevent checkout if out of stock, decrement stock on successful order.
- Acceptance: checkout fails when quantity > stock; stock updated after order.
- Entities: Product (stock), OrderItem
- Endpoints: enforced in checkout flow (no extra public endpoints)

## 6) Admin product management (medium)
- Features: CRUD products, upload/store image URLs, categories/tags, admin role access control.
- Acceptance: admin-only routes secured; admin can manage catalog.
- Entities: Product, User (role)
- Endpoints:
  - POST /api/products (admin)
  - PATCH /api/products/:id (admin)
  - DELETE /api/products/:id (admin)
  - GET /api/admin/products (admin list)

## 7) Validations & error handling (high)
- Features: input validation, standard error responses, HTTP status handling (400/401/403/404/500).
- Acceptance: consistent JSON error structure and clear validation messages.
- Entities: all
- Endpoints: applies to all API endpoints

## 8) Logging & metrics (low)
- Features: request logging, error logging, simple metrics (request count, error rate).
- Acceptance: logs emitted to console; basic metrics counters available.
- Entities: operational
- Endpoints: internal/monitoring (optional)

## 9) Tests (medium)
- Features: unit tests for services/controllers; integration tests for auth, product listing, checkout.
- Acceptance: CI runs tests; basic coverage enforced.
- Entities: all
- Endpoints: test harness covers core flows

## 10) API docs (low)
- Features: OpenAPI spec or README endpoint listing with request/response samples.
- Acceptance: README includes endpoint list and example requests for core flows.
- Artifacts:
  - /docs/openapi.yaml (optional)
  - README API section

---

## Entities (summary)
- User: id, name, email, passwordHash, role (user|admin), createdAt, updatedAt
- Product: id, title, description, price, currency, sku, images[], category, tags[], stock, createdAt, updatedAt
- Order: id, userId, status, total, currency, shippingAddress, items[], createdAt, updatedAt
- OrderItem: id, orderId, productId, quantity, unitPrice, totalPrice

## Minimal Acceptance Criteria (overall)
- Authenticated users can add products to cart and place orders.
- Admin users can manage product catalog.
- Checkout enforces stock and persists orders.
- API returns consistent JSON and status codes.
