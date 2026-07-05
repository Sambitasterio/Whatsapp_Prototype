# Guardian Gate

**A clickable prototype for verifiable parental consent on WhatsApp — built for Vedantu's Product Management Intern case study.**

🔗 **Live demo:** [sambitasterio.github.io/Whatsapp_Prototype](https://sambitasterio.github.io/Whatsapp_Prototype/)

---

## What this is

WhatsApp's own minimum age is 13. India's Digital Personal Data Protection (DPDP) Act, 2023
defines a "child" as anyone under 18 and requires **verifiable parental consent** before
processing a child's personal data. Every 13–17-year-old on WhatsApp is a legitimate user by the
app's own rules, yet is still legally a child under Indian law — a structural gap, not an edge
case.

**Guardian Gate** is a proposed consent mechanism that closes that gap using infrastructure
WhatsApp already has: the age-verification prompt it already asks at signup, and the
phone-number-verified trust model it already uses for every message. This repo is a working,
click-through prototype of that flow — happy path only, no backend, pure front-end.

This was built as part of a product management case study: designing how a consumer product
should handle personal data and consent to align with the DPDP Act, without driving users away.

## Try it

Open the [live demo](https://sambitasterio.github.io/Whatsapp_Prototype/) and click through in
order — every screen's primary button advances the flow:

| # | Screen | What happens |
|---|---|---|
| 1 | Birthdate check | Minor confirms date of birth (pre-filled to age 15) — the same prompt WhatsApp already has |
| 2 | Parent explainer | Plain-language explanation of why a parent needs to be involved |
| 3 | Choose parent contact | Minor selects a parent/guardian to send the request to |
| 4 | Pending — minor's chat list | Consent request appears as a native system message thread, status "pending" |
| 5 | Parent's device — consent card | A rich card (not a generic popup) shows exactly what's collected and why, with an Approve action |
| 6 | Confirmation | Parent sees the approval reflected immediately |
| 7 | Resolved — minor's chat list | The system thread updates to "Approved," core messaging was never blocked throughout |
| 8 | Normal chat list | The minor's account now behaves like any other, contact-sync restored |
| 9 | Family Center | The parent's ongoing dashboard: consent status, standing toggles (contact-sync, ad personalization locked off), and data-rights actions (view / correct / delete) |

A small map pill at the top of the page lets you jump between screens directly if you don't want
to click through linearly.

## Design principles

- **Reuse what already exists.** The age-check and the phone-verified trust model are both real
  WhatsApp mechanisms — Guardian Gate routes through them instead of inventing new
  infrastructure.
- **Never block core messaging.** While consent is pending, the minor's account stays fully
  functional for messaging — only secondary data flows (contact-sync) pause. This is a deliberate
  trade-off: it protects retention, but it also means consent has to be actively monitored (see
  the guardrail metrics in the accompanying deck), not just assumed to resolve itself.
- **Consent is a native message, not a popup.** WhatsApp already delivers non-chat content (like
  payment requests) as distinct card-style messages. Guardian Gate's parent-facing request reuses
  that exact pattern instead of introducing an unfamiliar UI paradigm.
- **The parent's say doesn't end at signup.** The Family Center screen gives a parent a standing
  dashboard, not just a one-time yes/no — including a data-rights section (view, correct, delete)
  addressing the DPDP rights gap directly.

## Tech stack

Plain **HTML, CSS, and vanilla JavaScript** — no framework, no build step, no dependencies.
Screen navigation is a single `showScreen()` function toggling visibility; all state (which
screen, which simulated device) lives in a few JS variables. This was a deliberate choice: a
fixed, non-branching happy-path click-through doesn't need a framework, and staying dependency-free
keeps it easy to host as a static file (see [Hosting](#hosting) below).

## Project structure

```
.
├── index.html              # Redirects to the prototype below (clean root URL for GitHub Pages)
├── prototype/
│   └── prototype.html      # The actual prototype — open this directly to preview locally
└── README.md
```

## Hosting

This is deployed via **GitHub Pages** directly from this repo (`main` branch, root folder) — no
build pipeline, no server. Any static host would work identically since there are zero external
dependencies or API calls.

To preview locally, just open `prototype/prototype.html` in any modern browser — no local server
required.

## Scope

This prototype covers the **happy path only** (parent approves, promptly), per the assignment's
requirements. Edge cases like a parent declining, being unreachable, or a minor aging into 18 are
addressed in the accompanying Product Thinking Deck, not in this clickable prototype.

## Author

**Sambit Behera** — submitted as part of the Product Management Intern hiring assignment for
Vedantu, July 2026.
