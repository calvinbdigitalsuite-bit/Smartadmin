# ECD Connect go-live checklist

A release is NOT production-ready until every mandatory gate is signed off.

## Product
- [ ] Production web app replaces localStorage prototype with authenticated Supabase APIs.
- [ ] Centre onboarding and first-owner provisioning tested.
- [ ] Parent/teacher/owner flows tested on Android, iPhone and desktop.
- [ ] CSV/XLSX import preview, validation, duplicate detection and rollback tested.
- [ ] Attendance corrections and audit history tested.
- [ ] Invoice/payment ledger and reconciliation tested.
- [ ] Reports export correct totals and respect centre permissions.

## Security and privacy
- [ ] RLS enabled on every exposed table and storage bucket.
- [ ] Cross-centre isolation tests pass (Centre A cannot read/write Centre B).
- [ ] Parent isolation tests pass (Parent A cannot access another child's data).
- [ ] Service-role key never reaches browser or Git.
- [ ] MFA, email verification, rate limits, CAPTCHA and secure password reset configured.
- [ ] Security review / penetration test completed and high-severity findings closed.
- [ ] POPIA risk assessment, privacy notice, operator agreements and retention schedule approved.
- [ ] Child-data processing authorisation questions reviewed with privacy counsel / Regulator.
- [ ] Incident response and breach notification process tested.
- [ ] Backup restore test completed.

## Integrations
- [ ] WhatsApp opt-in captured and approved templates live.
- [ ] WhatsApp webhook signature verification and delivery callbacks tested.
- [ ] Payment provider webhooks verified, if online payments are enabled.
- [ ] Payroll calculations independently validated for current SARS tax year.
- [ ] Payslip and payroll reports signed off by payroll specialist.

## Operations
- [ ] Domain registered to B-Digital and DNS verified in Vercel.
- [ ] HTTPS, redirects, transactional email and support inbox verified.
- [ ] Staging and production are separate.
- [ ] Error monitoring, uptime checks and database alerts configured.
- [ ] Staff support process and service status communications ready.
- [ ] Terms of service, privacy policy, data-processing agreement and pricing approved.
- [ ] Pilot with 2–3 ECD centres completed; feedback and fixes closed.
- [ ] B-Digital has documented owner/admin access recovery and offboarding process.

## Launch decision
- [ ] Technical lead approval
- [ ] Security/privacy approval
- [ ] Payroll specialist approval (if payroll enabled)
- [ ] Product owner approval
