# Gmail OAuth Email-Keying Research

Code-pattern audit across 2M+ public repositories on Sourcegraph. 124 open-source projects still key Google OAuth handlers on `email` instead of the stable `sub` claim.

**Full report with tables, severity breakdown, and methodology:** https://neelagiri65.github.io/gmail-oauth-research/

## Summary

- **Scope:** 2M+ non-archived, non-forked public repos
- **Findings:** 124 repositories with email-keyed Google OAuth handlers
- **Ecosystems:** Passport.js (73), Ruby/OmniAuth (19), NextAuth (17), Python/Django (15)
- **Notable hits:** PostHog (32K stars, CRITICAL), LibreChat (35K, HIGH), GitLab (24K, HIGH), MeshCentral (6.4K, CRITICAL), CircuitVerse (1.2K, CRITICAL)
- **Reference implementation:** cal.com (41K stars) uses `token.sub` as the primary identity key

## Why this matters

Google enabled Gmail username changes in March 2026. For twenty years, `email` was treated as a stable unique identifier across OAuth integrations. It never was. The `sub` claim in the OIDC ID token is the only stable identifier Google guarantees.

Projects that key users on email will fracture identity on rename: duplicate accounts, orphaned data, broken audit trails, lost access.

## Methodology

Sourcegraph public code search. Non-archived, non-forked repositories only. Library-specific patterns in each ecosystem. Manual verification on sampled results. 0% false positive rate on sample.

Full methodology section in the [report](https://neelagiri65.github.io/gmail-oauth-research/).

## What to do

1. Switch your primary identity key to `sub` (or `googleId` / `profile.id` depending on your library). Email becomes a display field.
2. Add Semgrep rules to your CI to catch email-keying before it ships: [authdrift](https://github.com/Neelagiri65/authdrift)
3. Audit code generators and scaffolds. If you scaffolded from a template with an email-keyed auth handler, the vulnerability is baked in.

## Related

- Scanner / Semgrep ruleset: [authdrift](https://github.com/Neelagiri65/authdrift)
- Full essay on the rename cascade: [Google Externalised the Cost of Renaming Gmail](https://nativerse-ventures.com/gmail-rename-cascade)

## Author

Srinathprasanna Shanmugam · [LinkedIn](https://www.linkedin.com/in/srinathprasanna/)

Published 13 April 2026.
