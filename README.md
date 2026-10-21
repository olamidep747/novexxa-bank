# Novexxa Bank — banking with comfort

A banking-interface preview for presentation and testing. Novexxa is not a licensed bank and does not move real money.

## Implemented
- Supabase email/password sign-up and sign-in.
- Separate Novexxa Supabase project: `zyloazosnfykpxpjxmuq`.
- Dedicated profiles, transaction, transfer-request, withdrawal-request, and support-ticket tables.
- Unique generated account numbers for new profiles.
- Admin-only server-side account lookup by account number and updates to account balance/status, with audit logging.
- Four-digit withdrawal PIN hashed server-side.
- Withdrawal requests require an active account profile and a correct PIN; they enter `verification_required`.
- Separate employee/admin queue requires an assigned staff account and a four-digit employee code to record verification. Verified requests remain `under_review`.
- Row-level security on exposed tables; direct client inserts to withdrawal requests are disabled.
- Transfer requests and support requests are stored for review.

## First-time setup still required
1. Deploy the repository with GitHub Pages or another static host.
2. Create the owner's user account through the sign-up screen and confirm the email if required.
3. Assign the owner as admin in Supabase SQL Editor using the verified account email:
   ```sql
   insert into novexxa_private.admins (user_id, role)
   select id, 'admin' from auth.users where email = 'OWNER_EMAIL_HERE'
   on conflict (user_id) do update set role = 'admin';
   ```
4. From the Admin / Employee page, assign staff by their registered email and set their four-digit staff identity code. Staff accounts must register first.
5. Test account creation, PIN setup, admin lookup, and employee verification using non-financial test data.

## Important limitations
- Balances, transaction history, and account activity shown in the interface are not real funds or real bank transactions. No real transfers, withdrawals, cards, or bank rails are connected.
- The transfer preview code `246810` is hardcoded and is not secure authentication.
- The four-digit withdrawal PIN is hashed server-side, but this interface is not a substitute for production-grade banking security.
- Never expose a Supabase service-role/secret key in the browser.
- Security advisor warnings for guarded `SECURITY DEFINER` RPCs are expected to be reviewed; each staff RPC checks the private role table before returning or changing privileged data.
