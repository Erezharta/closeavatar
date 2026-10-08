# AGENTS.md — CloseAvatar marketing site

Read this first. It tells you what the site is, what is true about the company, and how to change it safely.

## What this is
Static marketing site for **CloseAvatar** (https://closeavatar.com), an early-access product where B2B sales reps practice calls against AI buyer avatars and get line-by-line coaching. The product is **built on the Claude API (Anthropic)**. This repo is only the website: plain HTML + CSS, no build step, no JavaScript, no dependencies, no secrets.

- Contact: **erez@closeavatar.com** (the only contact; keep it visible in nav, hero, final CTA, footer, privacy).
- Hosting: GitHub Pages via `.github/workflows/pages.yml` on every push to `main`. Custom domain via `CNAME`.

## Repo map
| Path | Role |
| --- | --- |
| `index.html` | The whole landing page (hero + product window mock, problem, 3 product moments, scenarios, teams, final CTA). Contains JSON-LD. |
| `privacy.html` | Privacy page. Must stay accurate: no cookies/analytics/forms. |
| `styles.css` | All styling, tokens in `:root`, responsive breakpoints at 1060 / 860 / 560px. |
| `fonts/` | Self-hosted woff2 (Instrument Serif, Inter Tight, JetBrains Mono; OFL). No third-party font requests. |
| `llms.txt` | Machine-readable summary for AI agents/crawlers. Keep in sync with copy. |
| `robots.txt`, `sitemap.xml`, `CNAME`, `favicon.svg`, `.nojekyll` | Site plumbing. |
| `.github/workflows/pages.yml` | Copies an explicit file list into `_site/`. **New top-level files must be added to its `cp` line or they will not deploy.** |

## Design system (do not drift)
- Palette: ultramarine `--blue #2a17ee`, signal lime `--lime #d8ff3e`, night `--night #0b0930`, paper `--paper #f6f6fb`, ink `--ink #0b0a24`. Lime is the single accent; use it sparingly.
- Type: Instrument Serif (headings, italic for emphasis words), Inter Tight (body), JetBrains Mono (labels, small caps-style tags).
- Motion: CSS only, subtle. Scroll reveal uses `animation-timeline: view()` as progressive enhancement and must stay **transform-only** (never opacity) so content can never render blank. Everything is disabled under `prefers-reduced-motion`.
- Paths must be **relative** (`styles.css`, `fonts/...`, `./#product`) so the site works both at `closeavatar.com` and at the `erezharta.github.io/closeavatar/` subpath. Never use root-absolute `/…` asset paths.

## Content rules (non-negotiable)
1. **No fabricated proof.** No fake logos, customer names, testimonials, metrics, pricing, or compliance claims. The product UI on the page is an *illustrative sample* and is labelled as such; keep that caption.
2. **Claude is woven in lightly.** Allowed: "Built on Claude" chip, "Powered by Claude" / "Coaching by Claude" tags, the footer tech note, `llms.txt`/JSON-LD mentions. **Not allowed:** a "How we use Claude" section or any Claude-centred pitch block.
3. **Early-access honesty.** Say early access; do not imply GA, self-serve signup or customers.
4. Voice: tight, concrete, no hype words. Keep the narrative: roleplay is polite → feedback arrives late → training is generic → buyer avatar → exact-line coaching → next drill → scenarios → team patterns → request access.
5. The email address is `erez@closeavatar.com`. Do not reintroduce `hello@`.

## How to verify a change
```sh
python3 -m http.server 8000        # serve repo root
```
Then check at 1440px and 390px: no horizontal scroll, no blank sections, hero window readable, reduce-motion shows everything. Run `grep -rn "hello@" --exclude-dir=.git .` (expect nothing) and confirm any new file is in the workflow `cp` list.

## Workflow
Branch off `main`, open a PR, merge to `main` to deploy. Do not commit straight to `main`. Pages settings (custom domain, HTTPS) are changed in the GitHub UI, not in the repo.

## Agent-readability notes
The page is semantic HTML: one `h1`, `h2` per section, landmarks (`header`, `nav`, `main`, `footer`), skip link, and the product mock is real text (not an image) exposed in the accessibility tree. Machine-readable context lives in `llms.txt` and the JSON-LD block in `index.html`.
