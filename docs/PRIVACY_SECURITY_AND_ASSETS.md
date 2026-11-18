# Privacy, Security, and Asset Policy

This document defines project safeguards for the BYOP version of AnatoAR.

## Data minimization

The BYOP scope does not include:
- user accounts or authentication
- names, email addresses, phone numbers, or other learner identifiers
- patient information or medical records
- server-side learner profiles
- cloud-synced bookmarks or learning progress
- analytics, telemetry, session replay, or tracking pixels

If a future proposal would introduce personal-data processing, do not implement it under this scope without first confirming programme eligibility.

## Local browser storage

Local storage may be used only for minimal non-identifying application preferences, bookmarks, and learning completion state.

- Do not store sensitive information.
- Validate data read from local storage.
- Version the storage schema.
- Provide a clear-data action.
- Handle unavailable or malformed storage safely.

## Camera and AR

- Request camera access only after an explicit user action.
- Explain the purpose before requesting permission.
- Do not upload or persist camera frames.
- Stop camera tracks and AR sessions on exit.
- Handle permission denial and unsupported devices gracefully.

## Secrets and configuration

- Never commit API keys, passwords, private keys, or tokens.
- Keep `.env` files out of Git.
- Use `.env.example` only for non-secret configuration placeholders.
- If a secret is committed, revoke it and follow the repository's secret-removal process; deleting the current file alone is not sufficient.

## Third-party dependencies

- Review the license and maintenance status of dependencies.
- Avoid unnecessary dependencies.
- Keep dependencies updated and run available security checks.
- Do not add analytics or data-collection SDKs in the BYOP scope.

## 3D models, images, and other assets

For every external asset, record:
- asset name and description
- source URL
- creator/author
- license name and link
- required attribution
- modifications made
- date obtained

Do not assume that an asset is reusable because it is downloadable or visible online. Confirm the license permits the intended use and redistribution. Keep attribution notices where required.

## Educational accuracy

- Record references for anatomy descriptions.
- Mark content as draft until reviewed.
- Do not make diagnostic or treatment claims.
- Do not imply that the app replaces formal education or clinical supervision.

## Release checklist

- [ ] No secrets in current files or Git history.
- [ ] No real personal, customer, patient, or regulated data.
- [ ] No AI inference or prohibited AI infrastructure.
- [ ] No account or cloud learner-data functionality.
- [ ] Camera access is opt-in and local to the AR experience.
- [ ] All external assets have documented licenses and attribution.
- [ ] Educational content references and review status are recorded.
