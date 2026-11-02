# Deployment runbook — Vercel + Supabase

## Accounts and ownership
Create the Vercel, Supabase and GitHub accounts under B-Digital-controlled email addresses.
Turn on MFA for all three. Keep at least two trusted organisation owners. Do not share
passwords in chat or commit secrets to source control.

## 1. GitHub
- Create a **private** repository, e.g. `bdigital/ecd-connect`.
- Upload the completed application source and this starter pack.
- Protect `main`: require pull-request review and passing checks.
- Keep staging changes on a separate branch.
- Do not commit `.env`, access tokens, database passwords or service-role keys.

## 2. Supabase
- Create separate `ecd-connect-staging` and `ecd-connect-production` projects.
- Select a region after reviewing latency, data-residency, contractual and POPIA implications.
- Save the project URL and publishable/anon key for the app configuration.
- Keep the service-role key server-side only.
- Apply migrations to staging first, then test role and centre isolation.
- Enable SSL enforcement, database network restrictions where practical, MFA, auth email
  confirmation, custom SMTP, CAPTCHA/rate limits and Security Advisor checks.
- Configure backups and recovery objectives; verify a restore drill.
- Configure Storage buckets privately with RLS policies before any child documents or
  payment proof files are uploaded.

## 3. Vercel
- Import the private GitHub repository as a new Vercel project.
- Select the correct framework/build settings once the production app is implemented.
- Set separate Preview and Production environment variables.
- Add `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`.
- Add server-only secrets (`SUPABASE_SERVICE_ROLE_KEY`, WhatsApp credentials) only in
  Vercel server environment variables. Never expose these through `NEXT_PUBLIC_`.
- Set the function region close to the Supabase project region.
- Deploy a preview and complete acceptance testing before promoting to production.
- After changing environment variables, redeploy.
- Add the purchased custom domain in Vercel and apply the exact DNS records Vercel provides.
  Do not guess A, CNAME or TXT values. Enable HTTPS and verify redirects.

## 4. Domain
No domain has been purchased yet. Candidate names to check (availability not verified):
- ecdconnect.co.za
- ecdconnect.africa
- ecdconnect.app
- ecdconnect.co.za is the recommended first check for a South African audience.
Register the selected domain in a B-Digital-owned account. Enable auto-renewal and MFA.
Use a dedicated support mailbox on the chosen domain.

## 5. Supabase production hardening
Follow the official production checklist:
https://supabase.com/docs/guides/deployment/going-into-prod
At minimum: RLS on every exposed table, explicit policies, SSL, network restrictions,
MFA, email confirmations, custom SMTP, CAPTCHA, rate limits, performance review, backups,
load tests and a documented incident/recovery process.

## 6. Vercel production hardening
Use Git-based production deployments and preview deployments. Keep production secrets
separate from Preview/Development. Protect preview deployments and restrict project/team
access. Document who can deploy and who can change production environment variables.

## 7. Rollback
- Keep the previous known-good Vercel deployment available for instant rollback.
- Database changes must be backward-compatible where possible; do not assume rolling back
  frontend code reverses a database migration.
- Take and verify backups before risky schema changes.
- Document a named incident owner and contact route.
