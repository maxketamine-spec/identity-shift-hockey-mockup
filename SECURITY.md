# Security

This repository is public and serves a static preview page. There is no server, no database, no
login and no stored user data. Most of the risk is in what gets committed.

## Secrets

- The page needs no keys, tokens or passwords, and none belong here.
- Everything committed is public: files, commit messages, branch names, issues and pull requests.
  Never commit secrets, private notes, internal file paths or contact details.
- A gitleaks scan of the full history (2 commits) on 2026-11-16 found no secrets. Run it again
  before a change that adds anything other than page content:

  ```
  gitleaks git . --redact
  ```

- If a secret is ever committed, treat it as leaked: revoke it at its source first, then tell
  Max. History is not rewritten without his yes.

## Auth

None. The page has no accounts and no sign-in. The "Log In" link in the nav goes to the live site,
which handles its own sign-in.

## Input validation

- The only inputs are the two email fields. Their forms do not send anything: the submit handler
  stops the submit and shows a preview note. Nothing is stored or transmitted.
- If the forms are ever connected to a real service (Max's decision), validate the address, send
  it only to that service over HTTPS, and update this file in the same commit.
- Player content is hard-coded in the script and written into the page through the `esc()`
  helper. Any new text built into HTML must go through it too. `esc()` escapes `&` and `<` only,
  so do not put data that may contain quotes inside an HTML attribute without escaping quotes as
  well.

## Dependencies

- No packages and no build tools.
- The only outside load is the Google Fonts stylesheet and font files (Inter Tight, Inter,
  JetBrains Mono, Barlow Condensed). Loading them sends the visitor's IP address to Google.
- Adding any outside script, stylesheet, tracker or analytics is a decision for Max and must be
  recorded in ARCHITECTURE.md.
- Links that open a new tab use `rel="noopener"`.

## Data handling

- No PHI. No form data is collected.
- The page shows the names, photos and quotes of a coach and of players. Add nothing about a real
  person that is not already public, and remove content promptly if asked.
- Images are inlined in `index.html`, so a removed photo stays in git history. Check before you
  commit a photo.

## Reporting a problem

Tell Max, the repository owner, directly and privately. Do not open a public issue or pull request
that describes a security problem or contains a secret.
