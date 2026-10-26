# Secure Configuration Checklist

Use this checklist for a fictional web application. Mark items only after you have actually verified them.

## Application
- [ ] Validate input on the server.
- [ ] Use parameterized database queries or safe ORM methods.
- [ ] Enforce authorization on every protected API operation.
- [ ] Use generic error messages for clients.
- [ ] Set request-size limits, timeouts, and rate limits.
- [ ] Keep dependencies updated and remove unused packages.

## Authentication and sessions
- [ ] Store passwords using a modern password-hashing algorithm through a trusted library.
- [ ] Rate-limit authentication attempts.
- [ ] Require MFA for privileged accounts where possible.
- [ ] Use HTTPS for login and authenticated pages.
- [ ] Configure session cookies with Secure, HttpOnly, and an appropriate SameSite value.
- [ ] Define session expiry and revocation procedures.

## Secrets and data
- [ ] Keep secrets out of source code and Git.
- [ ] Use environment-specific secret storage.
- [ ] Use least-privilege database accounts.
- [ ] Encrypt sensitive data in transit.
- [ ] Avoid logging passwords, access tokens, and unnecessary personal data.
- [ ] Define backups and test restoration procedures.

## HTTP and deployment
- [ ] Redirect HTTP to HTTPS after TLS is configured.
- [ ] Configure Content-Security-Policy for the actual application.
- [ ] Set X-Content-Type-Options to `nosniff`.
- [ ] Set an appropriate Referrer-Policy.
- [ ] Prevent framing where it is not required.
- [ ] Enable HSTS only when HTTPS works correctly across the intended domain.
- [ ] Disable debug mode and verbose stack traces in production.
- [ ] Restrict administrative endpoints and management ports.

## Monitoring and maintenance
- [ ] Record security-relevant events without recording secrets.
- [ ] Alert on suspicious authentication and authorization patterns.
- [ ] Review dependency and platform security updates.
- [ ] Periodically review permissions and exposed services.
- [ ] Document an incident response and credential-rotation process.

**Evidence rule:** Do not mark an item complete unless you have checked it in the target environment.
