# AGENTS.md

The one rulebook for this repository, for every person and every coding assistant (Claude Code,
Codex, Cursor, Gemini and others). CLAUDE.md only points here. Do not add a second rules file.

## Project overview

A concept redesign of the Identity Shift Hockey home page, made as a preview. It is one static
page, `index.html`, served by GitHub Pages at
https://maxketamine-spec.github.io/identity-shift-hockey-mockup/. It is not the official site:
every button and link goes out to the live site or to social profiles, and the footer says
"Concept redesign · preview only".

The repository is **public on purpose** (GitHub Pages serves it). Everything committed here,
including commit messages, branch names, issues and pull requests, can be read by anyone.

| Path | What it is |
|---|---|
| `index.html` | The whole site: styles, markup, script and every image (inlined as base64) |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are, without Jekyll |
| `README.md` | Title only |
| `ARCHITECTURE.md`, `SECURITY.md`, `DESIGN_SYSTEM.md` | How it is built, how it stays safe, how it looks |

## Setup, build, test, lint

- **Setup:** none. No packages, no environment variables, no secrets.
- **Run locally:** open `index.html` in a browser, or serve the folder:

  ```
  python3 -m http.server 8000
  ```

  then open http://localhost:8000/.
- **Build:** none. The file in the repository is the file that is served.
- **Test and lint:** none set up. TBD – confirm whether any check is wanted. Until then, check by
  eye in a browser (see "Dev workflow").
- **Deploy:** a merge to `main` is a deploy. GitHub Pages rebuilds from `main`, root folder, and
  the public page changes within a few minutes.

## Code style

Follow what `index.html` already does:

- One file. CSS in one `<style>` block in the head, JavaScript in one `<script>` at the end of the
  body, wrapped in an arrow-function IIFE `(() => { ... })();`.
- Colors, fonts, the column width and the easing curve are CSS variables on `:root`. Use them
  instead of new literal values; see DESIGN_SYSTEM.md.
- CSS is compact: one rule per line, grouped under short comments (`/* hero */`, `/* players */`).
- Sizes scale with `clamp()`; the phone layout lives in the `@media (max-width:640px)` block.
- Repeated content (player cards, the league strip) is data in the script, rendered with template
  strings. Text placed into HTML goes through the `esc()` helper.
- Images are inlined as `data:` URIs (the `IMG` map in the script, and `src` attributes in the
  markup). There is no image folder.

## Project rules

- Keep the page working at phone width (375px) and on desktop, with no sideways scroll. Respect
  the safe-area insets that are already in place.
- Keep `prefers-reduced-motion` support: the reduced-motion block turns off every animation and
  transition, and the canvas script checks `reduce`.
- Keep tap targets at least 44px tall, the visible `:focus-visible` outline, and the existing
  `aria-label` and `aria-live` attributes.
- The two email forms send nothing. They only show "Preview only. Sign-up connects when the site
  goes live." Wiring them to a real service is a decision for Max.
- External links open in a new tab with `target="_blank" rel="noopener"`.
- Watch the file size (about 770 KB today, mostly inlined photos). Compress an image before
  inlining it.

## Dev workflow

1. Start from a fresh `main` and make a branch for the change.
2. Edit `index.html`.
3. Open it in a browser and check: desktop width, phone width (375px), the player rail arrows and
   "Read more" buttons, the subscribe forms, and the page with reduced motion turned on. Check the
   browser console for errors.
4. Update ARCHITECTURE.md, SECURITY.md or DESIGN_SYSTEM.md if the change touches them (see
   "Living docs").
5. Push the branch and open a pull request against `main`. Max merges. After the merge, open the
   GitHub Pages address and confirm the change is live.

## Git conventions

- `main` is the live page. Nobody commits to it directly; every change is a branch and a pull
  request.
- Branch names are short and say what changes (for example `docs/agent-standards`).
- Stage files by path (`git add index.html`), never `git add -A` or `git add .`.
- One commit per change. The message says why, in plain words.
- Commits written with Claude end with a `Co-Authored-By: Claude ...` line.
- Never force-push or rewrite history without Max's yes.

## Do and don't

**Do**

- Keep the page a single self-contained `index.html`.
- Use the CSS variables and the existing components before adding new ones.
- Test in a real browser at phone and desktop widths before saying a change works.
- Keep docs in step with the code in the same commit.

**Don't**

- Don't commit secrets, keys, private notes, internal file paths, contact details or anything
  private. The repository is public.
- Don't add a build step, a framework or a package without Max's decision.
- Don't make the forms send data, and don't remove the "Concept redesign · preview only" label,
  without Max's go.
- Don't add anything about a real person (names, photos, quotes) that is not already public.
- Don't add new tool rule files (`.cursorrules`, `GEMINI.md` and the like). Rules go here.

## Living docs

Any change to architecture, dependencies, security, or UI must update ARCHITECTURE.md, SECURITY.md, or DESIGN_SYSTEM.md in the same commit.
