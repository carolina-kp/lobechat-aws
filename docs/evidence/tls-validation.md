# TLS Validation

Domain: `carolina-lobechat.duckdns.org` — EC2 IP: `54.74.229.65`

## End-to-end validation checklist

- [x] **Casdoor login flow completes** — Logged in as "User" (carolina.kogan@alumni.esade.edu) via Casdoor SSO from https://carolina-lobechat.duckdns.org. No cookie or redirect_uri errors. (See screenshots/lobechat-https.png) — 2026-05-09 04:30 UTC
- [x] **LobeChat chat streaming works** — Sent messages via anthropic/claude-3-haiku and openrouter/auto, tokens arrived incrementally confirming SSE path works through Caddy reverse proxy. (See screenshots/chat-mcp.png) — 2026-05-09 04:35 UTC
- [x] **MCP tool invoked from chat returns a result** — Used mcphub filesystem-list_directory tool to list /tmp, result rendered in chat. Confirms long-lived MCP Streamable HTTP transport works through Caddy. (See screenshots/chat-mcp.png) — 2026-05-09 04:35 UTC
- [x] **File upload to MinIO** — Uploaded an image file from chat, file stored successfully in MinIO. (See screenshots/minio-upload.png) — 2026-05-09 05:04 UTC
- [x] **Direct connection to EC2 origin rejected** — `curl -v --max-time 5 http://54.74.229.65:47000/` returns "Connection timed out". Port 47000 is not exposed in the security group. — 2026-05-09 02:39 UTC
- [x] **Valid certificate chain** — Let's Encrypt E8 intermediate, TLSv1.3, CN=carolina-lobechat.duckdns.org, valid 2026-05-08 to 2026-08-06. No browser warnings. — 2026-05-09 02:39 UTC

## Certificate details

```
$ curl -sv https://carolina-lobechat.duckdns.org/ 2>&1 | grep -E 'SSL|subject|issuer|start|expire|ALPN|subjectAlt'
* SSL connection using TLSv1.3 / TLS_AES_128_GCM_SHA256 / X25519 / id-ecPublicKey
* ALPN: server accepted h2
*  subject: CN=carolina-lobechat.duckdns.org
*  start date: May  8 11:40:56 2026 GMT
*  expire date: Aug  6 11:40:55 2026 GMT
*  subjectAltName: host "carolina-lobechat.duckdns.org" matched cert's "carolina-lobechat.duckdns.org"
*  issuer: C=US; O=Let's Encrypt; CN=E8
*  SSL certificate verify ok.
```

## Summary

| Property | Value |
|---|---|
| Issuer | Let's Encrypt (E8 intermediate) |
| Protocol | TLSv1.3 |
| Cipher | TLS_AES_128_GCM_SHA256 |
| Key exchange | X25519 |
| Certificate CN | carolina-lobechat.duckdns.org |
| Valid from | 2026-05-08 |
| Valid until | 2026-08-06 |
| HTTP/2 | Yes (ALPN negotiated h2) |
| Cert verify | OK (trusted chain) |

Caddy automatically provisioned and renews this certificate via Let's Encrypt ACME (HTTP-01 challenge).
