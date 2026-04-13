# Officer Equipment Checkout App

A Vercel-ready Next.js web app for managing officer shift start/end and equipment checkout/check-in using badge IDs and QR codes.

## Features

- Badge scan / start shift
- Officer profile display after scan
- Unknown officer registration
- No-equipment button
- QR equipment checkout / check-in
- End-of-shift logging
- Audit search by shift ID, day, or month
- Equipment registration
- Camera-based QR scanner for web browsers

## Stack

- Next.js (App Router)
- TypeScript
- Prisma ORM
- PostgreSQL
- Vercel deployment compatible

## 1. Create the project

```bash
npm install
cp .env.example .env
```

Set `DATABASE_URL` in `.env`.

Example:

```env
DATABASE_URL="postgresql://USER:PASSWORD@HOST:5432/equipment_app?schema=public"
```

## 2. Create the database schema

```bash
npx prisma db push
npm run db:seed
```

## 3. Run locally

```bash
npm run dev
```

Open `http://localhost:3000`

## 4. Deploy to Vercel

1. Push this project to GitHub.
2. Import the repo into Vercel.
3. Add the environment variable:
   - `DATABASE_URL`
4. Deploy.
5. After first deploy, run Prisma schema sync:

```bash
npx prisma db push
```

If you use a managed Postgres provider such as Neon, Supabase, or Vercel Postgres, use the provider connection string as `DATABASE_URL`.

## Notes

- Officer photos are stored as base64 data URLs in the database for simplicity.
- Badge scanners usually behave like keyboard input, so scanning into the badge field and pressing Enter will start the shift.
- QR scanners can also behave as keyboard input, or you can use the built-in browser camera scanner.
- The app prevents double check-out of equipment when the last event is still an open check-out.

## Seeded test data

Officer:
- Badge ID: `10001`
- NUID: `900001`

Equipment:
- `RADIO-001`
- `KEYS-101`

## API routes

- `POST /api/officers/register`
- `GET /api/officers/[badgeId]`
- `POST /api/shifts/start`
- `POST /api/shifts/no-equipment`
- `POST /api/shifts/end`
- `POST /api/equipment/register`
- `POST /api/equipment/scan`
- `GET /api/audit?shiftId=...`
- `GET /api/audit?day=YYYY-MM-DD`
- `GET /api/audit?month=YYYY-MM`

