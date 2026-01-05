# 🚀 Kalshi - Decentralized Prediction Markets

[![License: MIT+Commons](https://img.shields.io/badge/License-MIT--Commons-blue.svg)](./LICENSE)

Open-source decentralized prediction market platform built on Polygon blockchain with full transparency and control.

## ✨ Features

- **⚡ Fast & Scalable:** Built on Polygon for minimal fees and instant transactions
- **📊 Real-time Markets:** Live prediction markets with instant price updates
- **🔐 Secure:** Smart contracts with transparent on-chain operations
- **💳 Web3 Native:** MetaMask and Reown AppKit wallet integration
- **📱 Mobile Ready:** Responsive design for all devices
- **🎨 Modern UI:** Polymarket-inspired interface with advanced charts

## 🛠️ Tech Stack

- **Frontend:** Next.js 16 (React 19, TypeScript, Tailwind CSS, Zustand)
- **Backend/Database:** PostgreSQL with Drizzle ORM
- **Authentication:** Better Auth + SIWE (Sign-In with Ethereum)
- **Blockchain:** Polygon (viem, wagmi)
- **Storage:** Cloudflare R2

## 🚀 Quick Start

### Prerequisites

- Node.js 18+
- pnpm (package manager)
- PostgreSQL database
- Polygon RPC endpoint

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/kalshi.git
   cd kalshi
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Configure environment variables**
   ```bash
   cp .env.example .env.local
   ```

   Edit `.env.local` with your configuration:
   ```bash
   # Database
   POSTGRES_URL=postgresql://user:password@host:5432/database

   # Authentication
   BETTER_AUTH_SECRET=your-random-secret-32-chars

   # Blockchain
   NEXT_PUBLIC_REOWN_APPKIT_PROJECT_ID=your-project-id

   # CLOB API
   FORKAST_ADDRESS=your-address
   FORKAST_API_KEY=your-key
   FORKAST_API_SECRET=your-secret
   FORKAST_PASSPHRASE=your-passphrase

   # Storage
   CLOUDFLARE_ACCOUNT_ID=your-account-id
   CLOUDFLARE_R2_ACCESS_KEY_ID=your-key-id
   CLOUDFLARE_R2_SECRET_ACCESS_KEY=your-secret-key
   CLOUDFLARE_R2_BUCKET_NAME=your-bucket
   CLOUDFLARE_R2_PUBLIC_URL=https://your-cdn-url

   # Cron Jobs
   CRON_SECRET=your-random-secret-16-chars
   VERCEL_PROJECT_PRODUCTION_URL=https://your-domain.com
   ```

4. **Run database migrations**
   ```bash
   pnpm run migrate
   ```

5. **Start development server**
   ```bash
   pnpm run dev
   ```

   Open [http://localhost:3000](http://localhost:3000) in your browser.

## 📦 Database Setup

This project uses **Drizzle ORM** with **PostgreSQL**. Migrations are managed automatically.

### Running Migrations

Migrations are applied automatically during deployment. To manually run migrations:

```bash
pnpm run migrate
```

This script:
- Connects to your PostgreSQL database via `POSTGRES_URL`
- Applies all pending migrations from `src/lib/db/migrations/`
- Creates scheduled cron jobs for market synchronization

## ⏰ Scheduled Jobs (Cron)

The project includes three automated cron jobs for market synchronization:

### 1. sync-events (Every 5 minutes)
- Syncs prediction markets from the Goldsky PnL subgraph
- Endpoint: `GET /api/sync/events`
- Schedule: `*/5 * * * *`

### 2. sync-volume (Every 30 minutes)
- Updates market volume and trading data
- Endpoint: `GET /api/sync/volume`
- Schedule: `*/30 * * * *`

### 3. clean-cron-details (Daily at midnight)
- Cleans up old cron job logs
- Schedule: `0 0 * * *`

### Setting Up Crons with Dokploy

If deploying with **Dokploy**, configure schedule jobs in the dashboard:

1. Go to your project → **Schedule Jobs**
2. Create three new scheduled jobs:

**Job 1: sync-events**
- Schedule: `*/5 * * * *`
- Command: `curl -X GET https://your-domain.com/api/sync/events -H "Authorization: Bearer YOUR_CRON_SECRET"`

**Job 2: sync-volume**
- Schedule: `*/30 * * * *`
- Command: `curl -X GET https://your-domain.com/api/sync/volume -H "Authorization: Bearer YOUR_CRON_SECRET"`

**Job 3: clean-cron-details**
- Schedule: `0 0 * * *`
- Command: Handled automatically by PostgreSQL pg_cron extension

## 🧪 Testing

Run the test suite:

```bash
# Unit tests
pnpm run test

# E2E tests
pnpm run test:e2e

# Type checking
pnpm run type-check
```

## 📝 Scripts

```bash
pnpm run dev          # Start development server
pnpm run build        # Build for production
pnpm run start        # Start production server
pnpm run migrate      # Run database migrations
pnpm run test         # Run unit tests
pnpm run test:e2e     # Run E2E tests
pnpm run type-check   # Check TypeScript types
pnpm run lint         # Run ESLint
```

## 🔗 API Endpoints

### Markets
- `GET /api/events` - List all events
- `GET /api/events/[slug]` - Get event details
- `GET /api/markets` - List all markets
- `GET /api/markets/[id]` - Get market details

### Trading
- `POST /api/orders` - Place a new order
- `GET /api/orders` - Get user orders
- `GET /api/open-orders` - Get open orders

### User
- `GET /api/users/[address]` - Get user profile
- `GET /api/users/[address]/portfolio` - Get user portfolio

## 📚 Documentation

- [API Documentation](./docs/developers/markets-api/)
- [Trading Guide](./docs/users/getting-started/)
- [Architecture](./docs/developers/)

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License with Commons Clause. See the [LICENSE](./LICENSE) file for details.

## 💬 Support

- **Issues:** [GitHub Issues](https://github.com/yourusername/kalshi/issues)
- **Discussions:** [GitHub Discussions](https://github.com/yourusername/kalshi/discussions)

---

**Built with ❤️ for the decentralized prediction market ecosystem**
