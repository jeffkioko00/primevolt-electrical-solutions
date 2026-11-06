# PRIMEVOLT ELECTRICAL SOLUTIONS — website and business portal

This is a deployable Node.js/Express starter application with a public service website, client accounts, an admin dashboard, quotation acceptance, receipt generation, manual payment recording, M-Pesa STK Push and email/WhatsApp integration points.

## Included
- Responsive public website using the supplied Primevolt logo and navy/orange branding.
- Client registration and login.
- Service request form with optional photo upload.
- Admin-only dashboard with request notifications, request status updates and quotation creation.
- Quotation PDF and PNG generation; client electronic name/signature acceptance.
- M-Pesa STK Push endpoint and Safaricom callback handling.
- Manual payment recording and branded receipt PDF/PNG.
- SMTP email backup for accepted quotations and generated receipts.
- WhatsApp Cloud API service-request confirmation and quotation/payment messages.
- SQLite database and local file storage.

## Important production setup
This is the application source, not a hosted public website yet. It needs a domain/hosting account and credentials from the relevant providers before clients can use it online.

1. Install Node.js 20 or newer.
2. Copy `.env.example` to `.env`.
3. Set a long random `JWT_SECRET` and a NEW strong `ADMIN_PASSWORD`. Do not reuse a password previously shared in chat.
4. Set `BASE_URL` to the HTTPS website domain.
5. Configure SMTP. For Gmail, enable 2-step verification and create an App Password. Set `SMTP_USER`, `SMTP_PASS` and `BACKUP_EMAIL`.
6. Configure Meta WhatsApp Cloud API: set the access token, phone number ID and API version. For production, use approved WhatsApp templates where required by Meta's messaging rules. A normal WhatsApp personal number is not sufficient for API automation.
7. Configure Safaricom Daraja credentials: consumer key/secret, shortcode, passkey and a publicly reachable HTTPS callback URL. Test in sandbox before switching `MPESA_ENV=production`.
8. Run `npm install` then `npm start`. Open `http://localhost:3000`.
9. For deployment, use a Node.js host with persistent disk storage for `data/`, HTTPS, environment-variable secrets and regular encrypted database/file backups.

## First admin account
The first admin account is created from `ADMIN_EMAIL` and `ADMIN_PASSWORD` when the server starts and no account with that email exists. Set the password before the first start. The supplied password is intentionally not embedded in source code.

## Payment notes
- M-Pesa STK Push amount is the full quotation amount in this starter version. For deposits/instalments, use the manual payment recording flow or extend the payment form to allow a client-selected amount.
- Safaricom callback URL must be public HTTPS and must be configured in Daraja.
- A payment is recorded only after a successful callback. Never treat an STK prompt alone as proof of payment.
- Manual payment entries are admin-recorded; verify the transaction before issuing a receipt.

## Document and signature notes
Client acceptance uses an electronic typed-name signature with timestamp. If you require legally formal digital signatures, integrate a dedicated e-signature provider and obtain legal review for the applicable jurisdiction.

## Security / production checklist
- Configure a strong JWT secret, strong admin password, HTTPS and host-level secrets.
- Restrict admin account creation and add multi-factor authentication before public launch.
- Add CAPTCHA/anti-spam controls to public service request forms.
- Add a retention policy, encrypted off-site backups and audit logs.
- Verify WhatsApp templates, consent and opt-out requirements.
- Complete Safaricom Daraja production approval and callback testing.
- Add an admin user-management screen before allowing multiple staff accounts.

## Current limitations to address before launch
- The UI is a functional starter, not a fully audited production release.
- The admin quotation creator currently creates one line item per request through a simple prompt-based interface; a richer multi-line quotation editor is a recommended next improvement.
- Email sending is skipped until SMTP is configured; WhatsApp messages are skipped until Cloud API credentials are configured.
- The app stores uploaded project images and generated documents on the server disk. Use persistent storage and backups on the chosen host.
