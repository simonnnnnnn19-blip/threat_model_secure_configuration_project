# Threat Model: Fictional Web Application

## 1. Objective

Identify common security threats to a fictional web application and recommend proportionate mitigations. This assessment is educational and is not based on testing a live system.

## 2. System overview

The application contains:
1. **User browser** — displays the frontend and sends requests.
2. **Web/API server** — validates requests and enforces authorization.
3. **Database** — stores account and profile records.
4. **Administrator** — manages application settings and user access.

## 3. Assets to protect

- User credentials and session tokens
- Personal and profile data
- Application availability
- Administrator privileges
- Application secrets and database credentials
- Integrity of stored records and configuration

## 4. Trust boundaries

- Browser to web/API server over the network
- API server to database
- Standard user to privileged administrator functions
- Application runtime to deployment configuration and secret storage

Requests crossing a trust boundary should be authenticated where appropriate, validated, authorized, and logged without exposing sensitive data.

## 5. Threat identification and mitigations

| ID | Threat | Likelihood | Impact | Recommended mitigations |
|---|---|---|---|---|
| T1 | SQL/NoSQL injection through untrusted input | Medium | High | Use parameterized queries or safe ORM methods; validate input; use least-privilege database accounts. |
| T2 | Cross-site scripting (XSS) | Medium | High | Encode output; avoid unsafe HTML rendering; apply a suitable Content Security Policy; validate input as defense in depth. |
| T3 | Broken access control / IDOR | Medium | High | Check authorization on every server-side request; verify that the current user may access each requested record. |
| T4 | Weak or reused passwords | Medium | High | Enforce appropriate password policy; use a trusted password-hashing algorithm; support MFA for privileged accounts; rate-limit login attempts. |
| T5 | Session or token theft | Medium | High | Use HTTPS; protect cookies with Secure, HttpOnly, and appropriate SameSite settings; use short-lived tokens and safe storage/rotation practices. |
| T6 | Secrets committed to source control | Medium | High | Store secrets in environment-specific secret managers; use `.gitignore`; scan repositories for accidentally committed secrets and rotate exposed credentials. |
| T7 | Missing security updates | Medium | Medium/High | Patch operating systems, runtime, and dependencies; review dependency alerts; remove unused packages. |
| T8 | Excessive error details or sensitive logs | Medium | Medium | Return generic client errors; keep detailed diagnostics server-side; redact credentials, tokens, and personal data from logs. |
| T9 | Misconfigured HTTPS or security headers | Low/Medium | High | Enforce HTTPS; configure HSTS after HTTPS is verified; set suitable content and framing policies. |
| T10 | Denial of service or abusive traffic | Medium | Medium/High | Apply rate limits, request-size limits, timeouts, monitoring, and infrastructure-level protections. |

Likelihood and impact are qualitative estimates for this fictional example and should be reassessed for a real system.

## 6. Risk prioritization

**High priority**
- Enforce server-side authorization for every protected resource.
- Protect credentials, sessions, and secrets.
- Prevent injection and XSS.
- Enforce HTTPS and patch critical vulnerabilities.

**Medium priority**
- Configure rate limits and request-size limits.
- Improve security logging and alerting.
- Review dependencies and remove unused components.

## 7. Verification plan

For an authorized test environment only:
- Confirm users cannot access another user's records by changing an identifier.
- Confirm invalid input is rejected and database access uses safe parameterization.
- Review frontend output handling for unsafe HTML rendering.
- Confirm production traffic uses HTTPS.
- Check that secrets are absent from tracked source files and Git history.
- Review response headers and verify that error messages do not reveal stack traces.
- Confirm login and sensitive endpoints have appropriate rate limits.

Do not run tests against systems unless you own them or have explicit permission.

## 8. Conclusion

Threat modeling helps teams identify security risks before deployment. The most important controls are secure coding, server-side authorization, protected secrets and sessions, HTTPS, timely patching, and ongoing verification.
