# FamilyFlow

A mobile-first family chore, responsibility, allowance, tablet-time, and rewards PWA.

## Current status

The repository starts from the working local prototype and is ready to be hosted on GitHub Pages for $0/month.

The next step is wiring the front end to Supabase Free for:
- parent authentication
- cloud sync
- per-family data separation
- child PIN verification
- chore approvals
- append-only reward ledger
- tablet redemptions
- teen payouts

## Demo PINs in the current local prototype

- Parent: `2468`
- Ava: `1111`
- Mia: `2222`
- Jack: `3333`

These are prototype-only credentials and must be replaced when cloud auth is connected.

## GitHub Pages

This repo includes `.github/workflows/pages.yml`.

Once the repo exists:
1. Push these files to `main`.
2. In GitHub: Settings → Pages.
3. Set **Source** to **GitHub Actions**.
4. The workflow will publish the app.

For a repo named `familyflow` under user `mlee331-crypto`, the normal Pages URL will be:
`https://mlee331-crypto.github.io/familyflow/`

## Supabase

1. Create a free Supabase project.
2. Open SQL Editor.
3. Run `supabase/schema.sql`.
4. Create the first parent Auth user.
5. Create a family tied to that Auth user.
6. Seed children and chores.
7. Replace localStorage calls in the front end with Supabase queries/RPCs.

## Security design

- Every data table carries `family_id`.
- RLS is enabled.
- Parent access is checked against authenticated membership.
- Child PINs are stored as bcrypt hashes through `pgcrypto`, not plaintext.
- Chore approval is performed through an atomic SQL function to prevent duplicate rewards.
- Balances are derived from the immutable reward ledger instead of trusting a manually edited balance field.

## Cost target

The MVP is designed to run on GitHub Pages + Supabase Free with no required monthly hosting charge.
