---
name: Authenticate with the Openpath API
description: Log in with email/password (+ optional MFA), use the returned JWT, and refresh or validate it.
api: openapi/openpath-openapi-original.json
operations: [login, describeAccessToken, validateAccessToken, refreshLogin, logout]
generated: '2026-07-20'
method: generated
---

# Authenticate with the Openpath API

Base URL: `https://api.openpath.com`. Auth scheme `jwt`: send the token in the
`Authorization` header. HTTP Basic Authentication is also accepted.

## Steps

1. **Log in** — `POST /auth/login` (`login`). Body requires `email` and `password`;
   optionally `mfa.totpCode` when MFA is enabled, and `namespaceId`/`namespaceNickname`
   to disambiguate the org. The response `data` contains the access token and the
   identity. (Use `loginAll` if one email maps to multiple orgs.)
2. **Send the token** — put the JWT in the `Authorization` header on every subsequent
   request.
3. **Inspect the token** — `GET` `describeAccessToken` returns the identity and the
   scope strings (e.g. `o{orgId}-site:w`) the token carries, so you can confirm the
   caller has the scopes an operation requires.
4. **Validate** — `validateAccessToken` checks signature, format, expiration and active
   status. Possible error names: `TokenExpiredError`, `JsonWebTokenError`,
   `TokenNotFoundError` (see `errors/openpath-error-codes.yml`).
5. **Refresh** — `refreshLogin` issues a new token with refreshed scopes/expiration and
   invalidates the old one. **Logout** — `logout` invalidates the current token.

See `conventions/openpath-conventions.yml` for the scope model and pagination rules.
