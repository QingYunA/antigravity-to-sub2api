<div align="center">

# antigravity-to-sub2api

<p>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/dependencies-0-green.svg?style=flat-square" alt="Dependencies">
  <img src="https://img.shields.io/badge/offline-100%25-brightgreen.svg?style=flat-square" alt="Offline">
  <img src="https://img.shields.io/badge/privacy-client--side-blueviolet.svg?style=flat-square" alt="Privacy">
</p>

<p>
  Zero-dependency, client-side generator for converting Google AntiGravity / Gemini Refresh Tokens into Sub2API account import packages.
</p>

<p>
  <a href="https://vercel.com/new/clone?repository-url=https://github.com/QingYunA/antigravity-to-sub2api">
    <img src="https://vercel.com/button" alt="Deploy with Vercel">
  </a>
</p>

</div>

---

## Highlights

- **Zero runtime dependencies:** Single self-contained HTML file without npm packages, external build tools, or remote CDNs. Runs offline with zero network latency.
- **Canonical AntiGravity client integration:** Built-in Google AntiGravity public OAuth Client ID (`1071006060591-...apps.googleusercontent.com`) and Client Secret, bypassing interactive browser authorization callbacks.
- **Dual-format output generation:** Generates native Sub2API data bundles (`sub2api-data.json`) and Antigravity-Manager format (`antigravity-accounts.json`) in real time.
- **Delimited batch parser:** Automatically extracts account email, Refresh Token, and GCP Project ID from raw dealer delivery strings (`----`, `|`, and `:` separators).
- **100% client-side privacy:** All string parsing, state management, and file blob generation run strictly inside browser memory. No credentials or telemetry ever leave your machine.
- **Native dark mode:** System-aware theme toggle matching shadcn zinc neutral palette with persistent local storage.

---

## Output Formats

### 1. Sub2API Data Bundle (`sub2api-data.json`)

Directly importable via Sub2API Web Dashboard (`Accounts -> Data Management -> Import Data`) or Admin API:

```json
{
  "exported_at": "2026-09-08T09:00:00Z",
  "proxies": [],
  "accounts": [
    {
      "name": "user@gmail.com",
      "platform": "antigravity",
      "type": "oauth",
      "credentials": {
        "_token_version": 1788856623206,
        "antigravity_project_id": "gen-lang-client-your-gcp-id",
        "email": "user@gmail.com",
        "model_mapping": {
          "gemini-3.8-flash-tiered": "gemini-3.8-flash-tiered"
        },
        "oauth_type": "antigravity",
        "plan_type": "Pro",
        "project_id": "aicode-consumers",
        "refresh_token": "<YOUR_REFRESH_TOKEN>",
        "token_type": "Bearer"
      },
      "extra": {
        "model_rate_limits": {},
        "oauth_type": "antigravity",
        "privacy_mode": "privacy_set"
      },
      "proxy_key": "",
      "concurrency": 4,
      "priority": 1,
      "rate_multiplier": 1,
      "auto_pause_on_expired": true
    }
  ]
}
```

### 2. Antigravity-Manager Format (`antigravity-accounts.json`)

Compatible with Antigravity-Manager, OpenCode, and native Sub2API account readers:

```json
{
  "version": 3,
  "accounts": [
    {
      "email": "user@gmail.com",
      "refreshToken": "<YOUR_REFRESH_TOKEN>",
      "projectId": "antigravity-proj-448102"
    }
  ]
}
```

### 3. Sub2API Admin API cURL

Instant shell execution commands targeting your self-hosted Sub2API backend:

```bash
curl -X POST "http://127.0.0.1:8080/api/v1/admin/accounts" \
  -H "Authorization: Bearer YOUR_ADMIN_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "platform": "antigravity",
    "email": "user@gmail.com",
    "refresh_token": "<YOUR_REFRESH_TOKEN>",
    "project_id": "antigravity-proj-448102",
    "concurrency_limit": 5,
    "status": "active"
  }'
```

---

## Quickstart

### Local Use

No build step required. Clone and open directly in any browser:

```bash
git clone https://github.com/QingYunA/antigravity-to-sub2api.git
cd antigravity-to-sub2api
open index.html
```

Or serve via any static HTTP server:

```bash
npx serve .
# or
python3 -m http.server 8080
```

### Deploy to Vercel

Click the deploy button above, or deploy via Vercel CLI:

```bash
vercel --prod
```

---

## Operational SOP for Gemini Accounts

1. **Verify Token:** Import Refresh Token into AntiGravity Tools to test token refresh and model inference before modifying credentials.
2. **Re-associate Country:** Connect via a clean target-region IP and submit Google's official [Country Association Form](https://policies.google.com/country-association-form?source=policies-site) to reset account jurisdiction.
3. **Hardening:** Change account password, replace recovery email, bind TOTP 2FA, and terminate all active legacy sessions.
4. **Provision GCP Project:** Open [Google Cloud Console](https://console.cloud.google.com/), create a project, enable Generative Language API and Vertex AI API, and extract the globally unique `Project ID`.
5. **Convert & Import:** Paste credentials into this tool, export `sub2api-data.json`, and upload directly into Sub2API.

---

## License

[MIT](LICENSE) © 2026 QingYunA
