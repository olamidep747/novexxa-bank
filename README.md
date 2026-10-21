# Novexxa Bank — Demo Starter

A responsive dashboard prototype for **demo/testing only**.

## Included
- Responsive dashboard, mobile navigation, and inactive-account indicator.
- Illustrative USD balance, sample transactions, and a visual-only demo card.
- Demo transfer and withdrawal request forms with a client-side preview code.
- Country/provider selector and support-ticket form.
- Supabase Auth sign-in/sign-up integration.
- Dedicated Novexxa database tables in the Supabase project `zyloazosnfykpxpjxmuq`:
  - `novexxa_profiles`
  - `novexxa_transactions`
  - `novexxa_transfer_requests`
  - `novexxa_withdrawal_requests`
  - `novexxa_support_tickets`
- Row-level security enabled on all five tables. User-facing policies limit records to the signed-in user's own records; requests are stored as demo/pending only.

## Preview
Open `index.html` in a browser, or enable GitHub Pages in repository settings and select the `main` branch with the `/(root)` folder.

## Important limitations
- The preview code `246810` is hardcoded in browser JavaScript and is **not secure**. It is only a UI demonstration and is not used as real authentication.
- Transfer and withdrawal submissions only create demo requests. No real funds are sent or paid out.
- The displayed balance and sample transaction history are illustrative and are not read from a real ledger.
- Do not enter real bank credentials, card details, or sensitive financial information.
- The public Supabase publishable key is intended for browser use; **never** expose a service-role or secret key in frontend code.
- Before any production financial use, obtain appropriate licensing/compliance review and implement server-side authorization, secure verification/OTP, fraud controls, audit logging, rate limiting, and a properly maintained ledger.

This is a prototype, not a licensed bank or production financial service.
