# Put BloodBridge online

## 1. Put the code on GitHub
Create a repository and upload the whole BloodBridge folder (the `.gitignore` keeps your database out).

## 2. Create a web service (Render, PythonAnywhere or similar)
- Build command: `pip install -r backend/requirements.txt`
- Start command: `gunicorn --chdir backend app:app`
- Environment variables: `SECRET_KEY`, `ADMIN_PASSWORD`, `CONTACT_EMAIL`, `PRODUCTION=1`, `DB_PATH`
- Free plans on some hosts erase files on every redeploy, which would delete your donors.
  Use a persistent disk (set `DB_PATH` to a path on it) and check the host's current terms.

## 3. Buy a domain
1. Search `bloodbridge.in` (also try `.com`, `.org`) on a registrar such as GoDaddy India, Hostinger,
   Namecheap or Gandi. Compare first-year and renewal prices: renewals are often much higher.
2. Register for 1 year in your own name. Skip hosting and email extras. GST is added in India.
3. Verify the email they send, turn on two-factor login and the domain lock.

## 4. Connect the domain
1. In your host, open "Custom domains" and add `bloodbridge.in` and `www.bloodbridge.in`.
2. Copy the DNS records it shows (an A or ALIAS record for the main domain, a CNAME for `www`).
3. Add them in the registrar's DNS page. Wait from a few minutes to a few hours.
4. The host issues HTTPS automatically. Open `https://bloodbridge.in` to check.

## 5. Before inviting strangers
Test with friends first, use a strong admin password, and read the safety notes in README.md.
