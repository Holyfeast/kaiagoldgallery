# 💎 Kaia Gallery — Premium Gold & Jewelry E-Commerce Platform

**[English](README.md)** | **[فارسی](README.fa.md)** 🇮🇷

A full-stack, production-ready gold and jewelry e-commerce solution built with a clean, scalable architecture. Built for the Persian/Iranian luxury jewelry market with RTL support.

> Brand colors: `#595959` (graphite) and `#eecdbc` (rose-gold)

---

## ✨ Highlights

- **Premium UI / UX** crafted for a luxury jewelry brand (RTL Persian, mobile-first).
- **Real-time gold pricing** with automatic per-karat price calculation and admin overrides.
- **Smart cart with 5-minute price lock** + visible countdown + automatic refresh.
- **Smooth, conversion-focused** OTP login → catalog → cart → checkout → payment flow.
- **Full-featured admin panel** for products, orders, categories, discounts, blog, gold prices, users, messages, and site settings.
- **Clean architecture** (.NET Core) + Next.js storefront + React (Vite) CRM, mirroring the proven Hamisigorta reference structure.

---

## 🧱 Project Structure

```
KaiaGallery/
├── Api/                       # .NET 9 backend (Domain, Application, Infrastructure, API)
│   ├── Domain/                # Entities, Enums, Constants
│   ├── Application/           # Features, Common (Interfaces, Exceptions, Models)
│   ├── Infrastructure/        # EF Core, Identity, Services, Background jobs
│   └── Api/                   # ASP.NET Web API host, JWT, Swagger
├── KaiaGalleryFront/          # Next.js 15 storefront (App Router, MUI v7, RTL)
├── crm-frontend/              # React + Vite admin panel (MUI v7, MUI X DataGrid, Recharts)
├── Docs/                      # Project documentation
└── docker-compose.yml         # Optional containerized stack
```

---

## 🚀 Quick Start (Development)

### Prerequisites

- **.NET 9 SDK** (`dotnet --version` >= 9.0)
- **Node.js 20+** and **npm** (or **yarn**)
- **SQL Server LocalDB** (Windows). On Linux/macOS, change the connection string in `Api/Api/appsettings.json` to a regular SQL Server instance.

### 1. Run the API

```powershell
cd Api/Api
dotnet restore
dotnet run
```

The API will:

- Apply all EF migrations automatically.
- Seed initial data (categories, sample products, blog posts, sliders, testimonials, pages, default admin user, etc.).
- Start at `http://localhost:5169` with Swagger UI at `http://localhost:5169/swagger`.

**Default admin login (OTP-based):**

- Mobile: `09000000000`
- OTP code: returned in the API response as `devCode` during development (also printed to the console).

### 2. Run the Storefront (Next.js)

```powershell
cd KaiaGalleryFront
npm install
npm run dev
```

Open `http://localhost:3000`.

### 3. Run the Admin Panel (React + Vite)

```powershell
cd crm-frontend
npm install
npm run dev
```

Open `http://localhost:5173`.

---

## 🔑 Key Features

### Storefront (`/KaiaGalleryFront`)

- Luxury home page with hero slider, gold ticker, category showcase, best-sellers, new arrivals, testimonials, and blog preview.
- Premium product catalog with rich filtering (search, category, karat, price range, sort).
- Detailed product page with gallery, specs tab, live unit-price, related products.
- **Cart with countdown timer** (5-minute price lock + manual refresh + similar product suggestions).
- Streamlined OTP-based authentication.
- Checkout with shipping methods, discount codes, and mock payment gateway.
- Customer profile, order history with PDF-ready detail page, wishlist.
- Blog with categories, search, full article view + related posts.
- About, Contact, and dynamic CMS pages (`/page/[slug]`).

### Admin Panel (`/crm-frontend`)

- **Dashboard** with KPIs (revenue, orders, products, customers) + 14-day sales bar chart + top-5 products pie chart.
- **Product management** with detailed editor (weight, karat, wage, profit, tax, additional price, images, SEO, flags).
- **Multi-level category management**.
- **Order management** with filtering, detail view, status updates, and tracking codes.
- **Gold price control center** (live ticker + manual price override).
- **Discount code management**.
- **Blog editor** (publish, feature, full HTML content, SEO meta).
- **User management** (search & paginate customers).
- **Customer message inbox** with reply.
- **Site settings** (grouped key-value editor for headers, footers, social links, etc.).
- Role-aware access (only `SuperAdmin`, `SalesManager`, `WarehouseManager` can login).

### API (`/Api`)

- Clean architecture: Domain → Application → Infrastructure → Api.
- ASP.NET Identity + JWT (access + refresh tokens) + OTP-based login.
- EF Core 9 + SQL Server LocalDB + automated migrations and seed data.
- Background `GoldPriceRefreshJob` (every 10 minutes) using a mock provider — swap to a real provider via `IGoldPriceProvider`.
- Mock payment gateway (`IPaymentGateway`) and SMS sender (`ISmsSender`) — replace with real providers in production.
- FluentValidation, global exception middleware, structured ApiResponse envelope.
- Swagger / OpenAPI for API exploration.

---

## 🧩 Architecture Decisions

- **Gold pricing logic** is centralized in `Application/Features/GoldPrice/GoldPriceCalculator.cs` and is used by both product listing/detail and cart price-locking. The formula:
  - `goldValue = weight × pricePerGramForKarat`
  - `wage     = weight × wagePerGram`
  - `profit   = (goldValue + wage) × profitPercent`
  - `tax     = (wage + profit) × taxPercent`
  - `total   = goldValue + wage + profit + tax + additionalPrice`
- **Cart price lock**: A 5-minute window stamps the cart with `PriceLockExpiresAt`. Prices and the gold spot price are snapshotted on the cart and remain stable until the user explicitly refreshes or the lock expires.
- **OTP**: Codes are stored in `OtpVerifications`. In development, the code is returned as `devCode`. Wire `ISmsSender` to a real provider for production.

---

## 🛠️ Customization

- **Theme colors**: edit `KaiaGalleryFront/src/theme/palette/primary.ts`, `secondary.ts` and the matching `crm-frontend/src/theme/index.ts`.
- **Add a real gold price source**: implement `IGoldPriceProvider` (see `Infrastructure/Services/GoldPrice/MockGoldPriceProvider.cs`) and replace the registration in `Infrastructure/DependencyInjection.cs`.
- **Add a real SMS provider** (e.g. Kavenegar, Twilio): implement `ISmsSender` and replace `DevSmsSender`.
- **Add a real payment gateway**: implement `IPaymentGateway` (currently a mock that auto-succeeds).

---

## 📜 Scripts

| Folder              | Command         | Description                            |
| ------------------- | --------------- | -------------------------------------- |
| `Api/Api`           | `dotnet run`    | Run the API (port 5169)               |
| `KaiaGalleryFront`  | `npm run dev`   | Run the storefront (port 3000)         |
| `KaiaGalleryFront`  | `npm run build` | Production build                       |
| `crm-frontend`      | `npm run dev`   | Run the admin panel (port 5173)        |
| `crm-frontend`      | `npm run build` | Production build                       |

---

## 📝 License

Internal project — © Karmast / Kaia Gold Gallery, 2026.
