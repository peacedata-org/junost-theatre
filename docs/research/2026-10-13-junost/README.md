# Junost reference-site research

Research date: **2026-10-13**. Reference: [junost.ru](https://junost.ru/).

This is independent public-source research for a portfolio concept, not commissioned work, a partnership, or an assertion of permission to reuse the reference site's assets or software.

## Executive conclusion

The reference is **Юность, a cinema in Voronezh**, not a theatre. Its website is a Kinoplan cinema storefront: a date-based film catalogue, chronological showtimes, film details, contacts, and ticket recovery. Seat selection opens a separate Kinoplan/Kinokassa widget.

A modern alternative should preserve the useful cinema workflows and local identity, not reproduce the template or its advertising wrapper. The strongest opportunities are better showtime discovery, earlier price/hall information, accessible controls, a clearer mobile hierarchy, and an explicit boundary between the independent interface and an authorized ticket provider.

## Read the dossier

| Document | Purpose |
| --- | --- |
| [Venue and sources](venue-and-sources.md) | Institutional facts, history, current contacts, evidence quality, source register |
| [Functions and journeys](functions-and-journeys.md) | Public routes, observed controls, user journeys, platform-only features, unverified transaction steps |
| [Design and quality audit](design-and-quality-audit.md) | Existing visual system, responsive composition, accessibility evidence, usability opportunities |
| [Client code and integrations](client-code-and-integrations.md) | Public bundle inspection, runtime architecture, observed API families, vendor boundaries |
| [Redesign brief](redesign-brief.md) | Proposed information architecture, visual alternatives, MVP priorities, state contracts, acceptance criteria |
| [Coverage and verification](coverage-and-verification.md) | What was actually inspected/tested, audit settings/results, limitations, reproducibility |

## Most consequential findings

1. The public navigation exposes **Афиша / Сеансы / Контакты**, not a full editorial cinema website.
2. The observed booking boundary is a **cross-origin ticket widget**. Changing the storefront does not automatically permit changing payment, inventory, refunds, or the vendor's interface.
3. Desktop uses a blue header and orange controls inside a white catalogue, with a large third-party advertising background above/around the content. Mobile switches to small-poster film rows.
4. Important interactive surfaces use non-semantic `div` elements. The mobile menu trigger has no accessible name, button role, or keyboard tab stop; showtime rows have the same semantic problem.
5. Mobile zoom is explicitly restricted. The inspected home, schedule, and film surfaces lack an `h1`; the home lacks a main landmark and the document lacks a language declaration.
6. A single mobile Lighthouse run reported accessibility **74/100**. A desktop schedule snapshot reported **78/100**. These are limited automated results, not a complete accessibility assessment.
7. The initial HTML is an empty application shell. React renders the catalogue from vendor data. Titles, descriptions, and canonical links are updated at runtime; no JSON-LD was found on the inspected home/film surfaces.
8. Two halls and historical capacities of **179 / 124 seats** are published by Culture.RF; current capacities and facility accessibility still need confirmation.
9. Backend source, administration, authenticated account behavior, seat-lock rules, final checkout, payment, and actual refund behavior are **not verified**.

## Evidence labels

- **Observed:** directly rendered or activated in an anonymous browser on the research date.
- **Source-inspected:** public HTML/CSS/JavaScript or resource metadata; not a complete original codebase.
- **Published:** a claim in an identified institutional, news, directory, or vendor source.
- **Proposed:** a redesign recommendation, not an existing feature or agreed implementation decision.
- **Unknown:** unavailable, untested, permission-dependent, or insufficiently supported.

Live schedules, prices, availability, and platform bundles change. The dossier records a dated observation, not a maintained cinema listing.

## Safety and reuse

No customer information was entered, verification messages requested, seats selected/held, orders created, payments attempted, refunds submitted, or staff contacted. No accounts were used.

Only original research notes and source links are committed. Reference screenshots, downloaded bundles, raw audit reports, browser/session data, and widget configuration values are not included. The demo must use original, synthetic, or appropriately licensed content and remain disconnected from live booking/payment services.
