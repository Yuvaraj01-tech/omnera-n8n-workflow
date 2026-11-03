# Security Audit & Operational Policies

## Security Audit Summary

| ID | Issue | Severity | Risk | Mitigation |
| :--- | :--- | :--- | :--- | :--- |
| **SEC-01** | Unencrypted `.env` files committed to Git | **CRITICAL** | Exposure of Meta access tokens, Groq keys, and ImgBB keys | Rotate all active tokens immediately; scrub Git history with `git-filter-repo`. |
| **SEC-02** | Public ntfy topics used for approvals | **HIGH** | Unauthorized users on public channels could approve or reject posts | Use private ntfy instances or require Bearer token authentication. |
| **SEC-03** | Public image hosting (ImgBB) | **MEDIUM** | Marketing assets stored on public third-party servers | Migrate to AWS S3 or Cloudflare R2 with temporary pre-signed URLs. |

---

## Credential Hygiene Policy

1. **Never commit real keys**: Always verify that `.gitignore` contains `.env` before running `git add`.
2. **Use placeholders in exports**: When exporting workflows from n8n, ensure all credential references are parameterized.
3. **Least Privilege**: Generate Meta System User access tokens restricted strictly to `instagram_basic` and `instagram_content_publish`.
