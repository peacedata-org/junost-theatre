# Coverage and verification

Research date: 2026-10-13. This document describes executed checks, not a proposed test suite or a claim to know every server/account/transaction feature.

## Method

- Read the project's documentation and repository state before making changes.
- Used public search/fetch for institutional, local-news, and vendor sources. A bounded independent Codex research pass supplied additional leads; important claims were cross-checked instead of accepting its output as ground truth.
- Opened public pages in a task-specific disposable headless Chrome instance with an isolated anonymous browser context.
- Inspected screenshots, accessibility snapshots, DOM geometry/styles, resource metadata, and publicly served minified CSS/JS.
- Used Chrome DevTools CLI for browser interactions and Lighthouse.
- Recorded summaries only. Raw reports, downloaded bundles, third-party images, browser logs, and configuration/session values are excluded from Git.

Browser version at the research endpoint: Chrome 155.0.8059.39. The DevTools CLI initially ran 1.8.0 and its installed version changed to 1.10.1 during the task; the connection was re-established to the same disposable instance. Final geometry checks were repeated in normal reading mode after that recovery. This is a tooling limitation, not evidence of a website failure.

## Inspected pages

| Page | Executed check |
| --- | --- |
| `/` | Rendered content, desktop/mobile screenshots, metadata, links, styles, resources, catalogue/date controls, cookie-preferences opening/cancel |
| `/seances` | Rendered chronological rows, DOM semantics, desktop Lighthouse snapshot |
| `/seances?date=2026-10-14` | Activated Tomorrow; URL and schedule update observed |
| `/contacts` | Business contacts/hours/map/VK; login-overlay opening attempt |
| `/release/23934?date=2026-10-13` | Film detail, metadata, trailer activation, booking-widget launch |
| Embedded seat screen | Diagram, price/hall/format/age, occupied legend, controls, screenshot; no seat selection |
| `/refund?cinemaID=92` | Initial form, phone/email modes, email tab switch, required fields/consents, disabled Find, support entry points |
| `/cinema/halls` | Rendered catalogue fallback, not an active hall-information page |
| `/cinema/about` | Rendered catalogue fallback, not an active venue-history page |
| `/soon` | Rendered catalogue fallback; upcoming content is present on home instead |
| Accessibility-mode control | Activated via DOM; reading-settings panel rendered; returned to normal |
| Mobile menu | Activated via DOM, expansion observed; trigger semantics inspected |
| `/robots.txt` and `/sitemap.xml` | Direct anonymous reads; allow-all robots and HTML returned at sitemap path |

DOM invocation of mobile-menu/accessibility controls establishes that the UI opened; it is **not** evidence that a keyboard user can reach those controls. The non-semantic menu trigger is recorded as a defect, not passed as accessible because programmatic activation worked.

## Automated audit results

| Surface/mode | Settings | Accessibility | Best practices | SEO |
| --- | --- | ---: | ---: | ---: |
| Schedule, snapshot | Desktop current rendered page | 78 | 100 | 83 |
| Home, navigation | Lighthouse mobile preset | 74 | 73 | 92 |

Mobile report settings: 412 × 823, device scale factor 1.75, simulated throttling, CPU slowdown multiplier 4. Selected categories were accessibility, SEO, best practices, and an experimental agentic-browsing category. **Performance was absent.** No LCP, INP, CLS, speed score, or real-user performance result is claimed.

The experimental category is not used to grade the redesign requirements. Missing `llms.txt` is not treated as a core cinema usability defect.

Relevant reported failures:

- Insufficient text contrast on header/footer/film badges.
- Missing HTML language, missing home main landmark, unnamed links.
- Restricted mobile zoom.
- Address anchors without crawlable destinations.
- Poster aspect-ratio warnings on mobile.
- Third-party cookie/browser issue warnings.

Audit scores vary with page, content, viewport, tool version, state, and timing. A best-practices score of 100 on one snapshot does not mean ticketing is secure or compliant. The reports do not cover all cross-origin widget states or replace manual assistive-technology/user testing.

## Responsive evidence

- Normal home screenshots/DOM at 390 × 844 and 1440 × 1000.
- Additional DOM geometry at 360 × 800, 768 × 1024, 1024 × 768, and 1920 × 1080 on the catalogue rendered at a fallback path.
- Final repeated geometry checks confirmed normal reading-mode body class and no document-width overflow at those four additional sizes.
- A mobile/touch emulation was used for the additional menu check.
- Desktop ticket-widget screenshot was inspected.

Not covered: exhaustive breakpoint/height combinations, full 200%/400% zoom, all long/malformed content, real phones, every trailer/widget state, print, reduced-motion runtime behavior, screen-reader testing, and final payment dialogs.

## Important limits

1. **Code:** public compiled frontend only. No original source repository, backend, database, server auth, infrastructure, or administration.
2. **Accounts:** site login opened an iframe overlay, but it remained blank during the attempt. Cause was not established; no assertion that login is universally broken. No authenticated profile/order history inspected.
3. **Transactions:** seat selection, holds, purchaser details, verification requests, orders, payments, receipts, successful tickets, and actual refunds were not exercised.
4. **Prices/schedules:** dated samples, not current guarantees. One 270 ₽ category is not the cinema's pricing model.
5. **Facilities:** institutional capacities/amenities may be historical. No visit or facility/accessibility verification occurred.
6. **Privacy/legal:** analytic resources were observed before an explicit banner-accept action, and the widget launch carried consent-related flags. No cookie/storage values were inspected/exported; no compliance verdict is made from those observations.
7. **Rights:** source visibility is not reuse permission. No reference media, logo, third-party prose, code, or legal documents were added as demo assets.
8. **Market:** no interviews, analytics, representative review analysis, competitor benchmark, conversion experiment, or commercial agreement.

## Safety checks

- No login, account creation, outreach, real form submission, seat hold, payment, refund, deployment, or external profile change.
- No credentials or personal customer information requested from the user.
- No widget configuration values copied into documentation or implementation.
- No real service integration added.
- Repository changes are original English research documentation and a correction of the cinema/theatre identity in README/guidance.
- No application build/test commands exist yet; documentation checks are the relevant local verification.

## Rechecking the reference later

1. Start a fresh anonymous disposable browser; do not use a saved personal profile.
2. Open the home, schedule, contacts, film, and recovery surfaces.
3. Record the date, viewport, displayed schedule horizon, metadata, navigation, and vendor origin without copying sensitive query/header/session values.
4. Stop booking inspection before clicking a live seat or performing a customer/transaction operation.
5. Repeat representative screenshots, geometry, semantic checks, and selected Lighthouse categories with recorded settings.
6. Reconfirm hall/facility and integration claims with the authorized venue/vendor before a production implementation.

Local reference captures were kept under `/tmp/opencode/junost-research-2026-10-13/` for this research session. They are temporary inspection material, not committed project assets or a promise of durable storage.
