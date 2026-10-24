# Novexxa authentication email setup

The HTML file in this folder is a branded Supabase **Confirm signup** template. It is committed to GitHub for easy copying, but committing it does not automatically change the template stored in Supabase.

## 1. Authenticate the sending domain in Brevo

1. Sign in to Brevo using the account that owns the sending domain.
2. Open **Settings → Senders, Domains & Dedicated IPs** (the exact menu can vary).
3. Add the domain you will send from and complete the verification steps.
4. Publish the exact DNS records Brevo provides for your domain, especially DKIM and any SPF/DMARC instructions. Do not copy example DNS values from another domain.
5. Wait until Brevo reports the domain as authenticated.

Before adding or changing an SPF record, inspect the existing SPF TXT record for that domain. A domain should normally have one SPF record; do not create a second one or overwrite records used by another mail provider. If the domain already sends mail, merge providers only according to their documented instructions.

## 2. Connect Brevo to Supabase Auth

In Supabase Dashboard, open **Authentication → Emails → SMTP Settings** and enable custom SMTP.

Use the values from your Brevo account:
- **Sender name:** Novexxa
- **Sender email:** the exact sender address verified in Brevo
- **SMTP host:** smtp-relay.brevo.com
- **Port:** 587 (STARTTLS) or 465 (SSL/TLS)
- **Username:** the SMTP login shown in Brevo
- **Password:** a Brevo SMTP key (not a Brevo API key)

Save the settings. Never put the SMTP key, Supabase secret key, or service-role key in this repository or browser code.

## 3. Install the signup email template

In Supabase Dashboard, open **Authentication → Email Templates → Confirm signup**. Set a concise subject such as:

**Confirm your Novexxa email address**

Copy the HTML from `confirm-signup.html` into the template editor and save it. The template uses Supabase's `{{ .Token }}` variable for the OTP. The actual code length is controlled by the Supabase Auth email/OTP settings, not by the HTML template. Keep that setting at six digits if the website expects six digits.

If Supabase does not allow template editing, verify that custom SMTP is enabled and saved first.

## 4. Improve inbox placement

- Turn off open/click tracking for authentication emails in Brevo if those options are enabled; tracking rewrites can hurt auth-email reliability.
- Keep authentication messages separate from marketing messages.
- Use a short subject, minimal links, no attachments, and consistent sender name/address.
- Publish a DMARC TXT record after checking current mail use. Start with a monitoring policy (often `p=none`) if you do not already have one, review reports, and only tighten policy after SPF/DKIM alignment is verified.
- Send a test to Gmail and another mailbox. Check **Brevo → Transactional → Email logs**, then inspect the message's original headers for SPF, DKIM, and DMARC results.
- Ask test recipients to mark a legitimate message as **Not spam** and add the sender to contacts; do not send repeated tests to many people.

Domain authentication improves deliverability but cannot guarantee inbox placement. Sender reputation, recipient engagement, and message content also matter.
