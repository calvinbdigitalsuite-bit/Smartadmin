# ECD Connect by B-Digital — development build 0.2.0

Responsive React/Vite application for South African ECD centre administration.

## Included working demo modules
- Dashboard and centre summary
- Child registration, search, CSV import/export
- Daily child attendance register
- Fee invoices and manual payment recording
- Staff records and demo staff attendance
- Basic salary overview (not a statutory payroll calculator)
- Parent portal preview (not a live parent account)
- Reports and settings screens
- Browser-local demo persistence

## Run
Requires Node.js 20+.

```bash
npm install
npm run dev
npm run build
```

## Current release status — not production ready
This is a functional development/demo build. Unless Supabase is configured, records are saved only in the browser's local storage. The Supabase client dependency and environment-variable connection point are included, but the UI's CRUD operations are not yet connected to live database tables. Live role-based authentication, centre-scoped data access, guardian-child links, WhatsApp delivery, online payments, secure document storage, statutory payroll calculations and payslip generation are not implemented yet. Do not enter real children's or employee data.

The included SQL migration is a starting schema and needs review and staging tests. It is not a security certification. POPIA obligations and child-data safeguards require professional review. Payroll must be validated against current SARS tax tables and South African employment requirements by a qualified payroll professional before use.

## Supabase
Create `.env.local` using `.env.example` and set `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`. These are public browser configuration values. Never expose a service-role key in a `VITE_` variable or browser code. Review and apply the migration in a staging project first. Test RLS with at least two centres and separate owner, teacher and parent accounts.

## Vercel
Import the GitHub repository, use the Vite preset, build command `npm run build`, output directory `dist`. Configure environment variables per environment. Connect a domain later using the DNS records Vercel provides.

See `docs/` for deployment, integration requirements and go-live checks.
