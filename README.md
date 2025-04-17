# 🔒 SSL Certificate Expiry Checker

This GitHub Action checks a list of domain names for SSL certificate expiry and creates a GitHub Issue if any certificates are expiring soon.

## 📋 How It Works

- A domain list is checked daily at 8 AM UTC.
- The custom [`expirybot`](https://github.com/sheran/install-expirybot-action) tool is used to scan domains.
- If any certificates are expiring soon, a GitHub Issue is created in the repository to notify maintainers.
- Optionally, Tailscale can be used to resolve internal/private domain names.

## 🧰 Requirements

- A file named `domains.txt` at the root of the repository containing one domain per line optionally followed by a number separated by a comma. The number is the number of days are left on the cert validity before alerts should be sent. The default is 14 days.
- GitHub repository secrets if using Tailscale (optional):
  - `TS_OAUTH_CLIENT_ID`
  - `TS_OAUTH_SECRET`

## 🗂️ Example `domains.txt`
```
example.com
subdomain.internal.ts.net
google.com,20
```

## 🛠️ Setup

1. Fork this repo into your own GitHub account.
2. Create or edit the `domains.txt` file at the root to include your domains that you want to check.
3. (Optional) If you want to check your Tailscale IPs that have DNS A records, then [create a Tailscale OAuth client](https://tailscale.com/kb/1213/oauth-clients/) and add the credentials as GitHub secrets:
   - `TS_OAUTH_CLIENT_ID`
   - `TS_OAUTH_SECRET`

## 📌 Notes

- The Action uses `actions/github-script` to create an issue titled:  
  `⚠️ SSL Certificate Expiry Warning`
- If an issue with the same title already exists and is open, it won't create a duplicate.
- The `expirybot` is expected to output human-readable results that include "expires in" for matching logic.

## 🧪 Manual Trigger

You can also manually trigger the workflow using the **"Run workflow"** button in the GitHub Actions tab.

---

## 👤 Author

Maintained by [@sheran](https://github.com/sheran)
