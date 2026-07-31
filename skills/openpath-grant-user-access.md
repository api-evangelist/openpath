---
name: Onboard a user and grant them a credential
description: Create a user in the org, issue them a credential, and confirm which entries they can access.
api: openapi/openpath-openapi-original.json
operations: [createUser, describeUser, createCredential, listCredentials, listEntryUsers]
generated: '2026-07-20'
method: generated
---

# Onboard a user and grant them a credential

Requires a token with user write scope (e.g. `o{orgId}-user:w`). Paths are under
`/orgs/{orgId}/...`.

## Steps

1. **Create the user** — `createUser` adds the person to the org. Read them back with
   `describeUser`.
2. **Issue a credential** — `createCredential`
   (`/orgs/{orgId}/users/{userId}/credentials`) issues a mobile/card/other credential
   to the user. List existing ones with `listCredentials`.
3. **Confirm access** — from the door side, `listEntryUsers` lists the active users who
   can access a given entry, and `listEntryUserSchedules` shows them with their
   schedules — use these to verify the new user resolved to the intended doors.

Access is governed by group/role/schedule assignment; see the `orgs/groups`,
`orgs/roles`, and `orgs/schedules` operation families. Follow the pagination
convention (`offset`/`limit`/`sort`) in `conventions/openpath-conventions.yml`.
