# Production integration requirements

## A. Multi-centre accounts and permissions
Roles:
- B-Digital platform operator: subscription, centre onboarding, support metadata only;
  access to centre content must be restricted, justified, logged and support-controlled.
- Centre owner/admin: centre setup, staff, children, fees, reports, centre membership.
- Teacher: assigned class children, attendance and permitted daily records only.
- Parent/guardian: only linked child profiles, attendance, invoices, own payment submissions
  and approved centre messages.

Rules:
- Every centre-owned row carries `centre_id`.
- Server derives allowed centre membership from the authenticated session.
- RLS is mandatory; frontend filtering is not a security boundary.
- Prevent users from self-assigning owner/admin roles.
- Require invitation/verification for parent and staff accounts.
- Provide account recovery, session revocation, audit logs and admin MFA.

## B. Parent portal
- Secure parent sign-in and account invitation.
- A guardian can be linked to one or more children with verified relationship/contact data.
- Parent sees attendance calendar, attendance totals, invoices, payment history and centre
  notices only for linked children.
- Parent can submit proof/reference for payment; centre admin verifies and posts actual payment.
- No public child directory or class-wide parent list.
- Parent contact details are masked from other parents.

## C. WhatsApp Business Platform
Use Meta's official WhatsApp Business Platform / Cloud API, not browser automation.
Official developer hub: https://whatsappbusiness.com/developers/developer-hub/
Required:
- Meta Business Portfolio and WhatsApp Business Account.
- Approved sender phone number and verified business setup as required by Meta.
- Cloud API access token stored as a server secret; rotate and restrict it.
- Webhook endpoint with verification challenge and request-signature validation.
- Approved message templates for business-initiated payment reminders and other notifications.
- Record explicit WhatsApp opt-in, timestamp, source and opt-out requests per guardian/number.
- Respect template category, messaging window, opt-out and quality policies.
- Queue, retry with backoff, idempotency, delivery-status webhooks and dead-letter logging.
- Never send a payment reminder based only on a browser click or an unverified balance.
- Provide manual review/preview and an audit trail for bulk sends.
- Avoid including sensitive child information in message content.

## D. South African payroll
Do not release payroll as a statutory calculator until reviewed by a South African payroll
specialist. Implement:
- Effective-dated SARS PAYE tables and rebates by tax year.
- UIF employee and employer contributions and applicable remuneration ceiling.
- SDL applicability and exemptions.
- Taxable benefits, pension/provident deductions, allowances and other approved deductions.
- Leave, overtime, termination and mid-month proration.
- Payslip with gross pay, deductions, employer contributions and net pay.
- Monthly EMP201 support and annual EMP501 / IRP5-IT3(a) export support where in scope.
- Calculation version, audit trail and approval before payroll is finalised.
- Regression tests against specialist-verified payroll examples every tax-year update.
Official SARS employer guide: https://www.sars.gov.za/guide-for-employers-in-respect-of-employees-tax-2027/

## E. Payments and reconciliation
- Decide whether the first release accepts EFT/manual payment capture or an online payment
  provider. Do not store card details.
- If adding a payment provider, use hosted checkout/tokenisation and signed webhooks.
- Verify webhook signatures and amount/currency/invoice references server-side.
- Keep immutable payment events and reconciliation reports; handle reversals/refunds.
- Parent proof uploads remain pending until approved by authorised centre staff.

## F. POPIA and child data
Before onboarding centres:
- Determine contractual roles: each ECD centre will usually determine purposes of processing;
  B-Digital may act as an operator for platform processing. Confirm with legal counsel.
- Sign an operator/data-processing agreement with each centre.
- Complete a personal-information impact/risk assessment and data inventory.
- Confirm lawful basis and any required authorisation for processing children's information;
  consult the Information Regulator's children's-information guidance.
- Appoint/register Information Officer where applicable; provide privacy notice and contact route.
- Collect only necessary data; avoid storing ID numbers, medical/safeguarding notes unless
  the feature is justified and separately secured.
- Set retention/deletion schedules, access/correction process, export process and breach plan.
- Encrypt data in transit and at rest, restrict staff access, log privileged access and test backups.
- Review cross-border hosting/transfers and any section 57 prior-authorisation implications.
- Do not claim POPIA compliance solely because the app has RLS or encryption.

Information Regulator resources:
https://inforegulator.org.za/guidance-notes/
https://inforegulator.org.za/popia-forms/
https://eservices.inforegulator.org.za/priorauthorisation/

## G. Data import
- Support CSV/XLSX with a downloadable template and column mapping.
- Validate file size/type, encoding, date formats, phone numbers and currency.
- Preview and confirm before import; detect duplicates; show row-level errors.
- Require authorised centre user; create import audit event.
- Provide rollback for failed batch and export of centre-owned data.
- Never accept executable files or public links as uploads.
