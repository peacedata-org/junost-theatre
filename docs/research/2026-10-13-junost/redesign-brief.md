# Requirements for a new version

This is a proposed requirements document, not an approved implementation plan. No framework, license, hosting/deployment platform, live integration, or asset-reuse permission has been selected.

## Keep

- Film catalogue and chronological showtimes as separate views.
- A date selection shared across catalogue, schedule, and film details.
- Film title, age rating, runtime, genre, session date/time, and truthful eligibility labels.
- Direct ticket-recovery/help and contact paths.
- A recognisable blue/orange colour relationship as an optional continuity choice, without copying the logo.
- Useful venue information, but only after verifying facilities and permissions.

## Change

| Existing behavior | New requirement |
| --- | --- |
| Background advertisement precedes catalogue | Main task must be available before any large promotional block |
| Whole-card navigation mixed with time actions | Separate film link and showtime controls |
| Hall/price primarily inside ticket widget | Show available hall/format/price data before launching booking |
| Clickable `div` sessions/menu | Native semantic controls, keyboard operation, accessible names |
| Zoom restriction and missing language/main/headings | Browser zoom allowed; Russian language declaration; proper page landmarks/headings |
| Mobile cookie obstruction | Choices/preferences do not obscure the active task; accessible overlay focus |
| Only a sampled Today/Tomorrow horizon | Show the actual published dates; never fabricate a week's inventory |
| Unavailable conditional pages fall through to home | Explicit navigation redirects/not-found states |
| One recovery form for several intents | Separate lookup/resend/refund intent and truthful result states |

## Proposed information architecture

| Page | Required content | Optional content requiring additional confirmation |
| --- | --- | --- |
| Афиша | Date controls, current-film cards, showtimes, upcoming section | A small promotional feature that does not displace the schedule |
| Сеансы | Date, chronological sessions, available hall/format/price data | Time window, family/eligibility filters if data supports them |
| Film detail | Heading, poster, age/runtime/genre, sessions, synopsis, trailer | Ratings with source/usage rights, stills with rights |
| О кинотеатре / Контакты | Published contacts, location link, confirmed hours | Verified halls, history, entrance/accessibility/parking/bar information |
| Билеты и помощь | Demo boundary or authorized provider entry; resend/refund intents | Authenticated order history only with an authorized integration |

For the first prototype, contacts and venue information can be one page. Adding separate pages for every possible service is not required.

## Layout alternatives

| Alternative | Structure | Tradeoff |
| --- | --- | --- |
| Catalogue-first | Date controls, poster cards with showtimes, compact upcoming section | Good for choosing a film; more page length on mobile |
| Schedule-first | Date and nearest sessions, then film discovery | Good for choosing by time; poster browsing is secondary |
| Large featured-film landing | Promotional film area before the catalogue | Useful for a specific campaign, but delays ordinary date/session selection |

Recommended starting point: **catalogue-first with an immediately reachable schedule view**. Keep the top of the page short. Test whether returning visitors prefer a schedule-first landing before committing to a larger redesign.

This recommendation concerns information order, not presentation copy or an agreed visual direction.

## Concrete visual constraints for prototypes

- Separate page background, card surface, text, secondary text, accent, focus, and error tokens.
- Use a readable Cyrillic-capable typeface with a verified license. Existing Manrope is a useful reference, not a required dependency.
- Use a small, consistent typography scale; film titles must survive long Russian names without covering actions.
- Show time/price as readable data, not decorative metadata.
- Reserve poster dimensions and preserve aspect ratio; use original/synthetic/licensed assets.
- Start with one or two card columns on narrow devices according to the available content, not a fixed desktop grid shrunk down.
- Do not introduce nested catalogue scrolling, hover-only booking, mandatory carousels, parallax, or custom cursors.
- Use ordinary headings and functional labels. Do not add decorative section indices, status captions, slogans, or presentation-style text.
- If motion is added, keep it short, interruptible, and unnecessary for task completion; define a reduced-motion behavior.

## Priority and scope

### P0: prototype parity and safety

- Synthetic catalogue with date-addressable views.
- Catalogue, chronological schedule, film details, contacts/help.
- Separate semantic showtime controls and a clearly disclosed **demo** booking surface.
- Synthetic seat map if included; no remote inventory, seat holds, orders, payments, or actual ticket delivery.
- Phone/email forms must not collect real customer data or call real verification/lookup services.
- Keyboard navigation, labels, focus, contrast, zoom, responsive layout, reduced motion.
- Loading/empty/error/unavailable states can be exercised with local fixtures.

### P1: improvements after basic flows work

- Time-window and family/eligibility filtering from explicit fixture fields.
- Session hall/format/price display.
- Clear actual-calendar-date treatment for midnight sessions.
- Better upcoming/no-session/sold-out distinctions.
- Confirmed venue/arrival information or clearly synthetic venue demonstration content.
- Appropriate route metadata and a deliberate crawl/indexing policy for a demo.

### P2: only after a separate authorization/decision

- Provider widget or gateway/API integration.
- Account/order history, promo codes, loyalty, online bar orders, actual payment/refunds.
- Official brand assets, actual venue photography, real repertoire feed, and licensed film media.
- Administration/CMS, hosting, production analytics, deployment, and official publication.

Do not add speculative subscriptions, favourites, ticket wallets, chatbots, or large CMS features just because other cinema sites have them. Their need is unverified here.

## Data needed by the interface

These are conceptual field requirements, not a vendor payload schema or backend choice:

| Record | Fields needed for the proposed UI |
| --- | --- |
| Film | Stable ID/slug, title, synopsis, genres, age rating, runtime, poster + rights/alt/dimensions, trailer + rights, release date, explicit qualifiers |
| Session | Film reference, start timestamp + timezone, cinema business date, hall reference, format/language, price or price range, currency, sales state, eligibility, approved booking destination |
| Hall | Name, confirmed seat map/categories, confirmed access information |
| Venue | Name, address, business contact, published hours, verified arrival/accessibility details, confirmed official links |
| Asset | Source/owner/license, attribution, permitted use, derivative restrictions |

The authoritative provider must own inventory/price/order truth in any production system. The storefront must not infer “sold out” from a missing response or keep stale prices as if verified.

## State requirements

| State | Required UI behavior |
| --- | --- |
| Initial/loading | Stable navigation/date shell; reserved poster/session space |
| Date refresh | Preserve selected date; no stale response overwriting a newer selection |
| No sessions on date | Explicit absence plus next available date/reset; not “sold out” |
| Upcoming, no sales yet | Release date/status without a fake Buy action |
| Sold out / sales closed / cancelled | Separate truthful states from upstream fields |
| Missing price/hall/metadata | Say unavailable or omit the field; do not invent data |
| Provider failure | Local error/retry and contacts; do not imply payment failed or refund succeeded |
| Demo selection | Selected seats and totals use synthetic records; demo disclosure at the consequential action |
| Expired/conflicting selection | Testable demo state; production contract depends on provider |
| Long film title | Wrap without covering time/price/actions |
| Trailer open/closed | Named dialog, focus entry/return, Escape, playback stopped on close |
| Cookie preferences | Necessary/optional categories, explicit choices, keyboard/focus semantics; production legal review separate |

## Acceptance checks before implementation is called complete

1. Test catalogue → film → dated session → demo/provider boundary and the schedule-first path.
2. Browser back/forward preserves route/date context; selected date is shareable.
3. Test 360, 390, 768, 1024, 1440, and 1920 px, plus breakpoint boundaries, landscape, large text, and zoom.
4. No document-level horizontal overflow or clipped booking controls; any seat-map pan/zoom remains usable and has an alternative.
5. Keyboard users can reach/open/close navigation, dates, sessions, trailer, help, and any seat simulation.
6. Measure text and required non-text contrast; main mobile targets have adequate size/spacing.
7. Exercise loading, empty, unavailable, error, long-content, conflict/expiry, and reduced-motion fixtures.
8. Verify there is no real ticketing/payment/verification request from the demo and no borrowed provider configuration.
9. Verify media/font rights and source/attribution records before adding public assets.
10. Run project checks only after the stack/build/test commands have been agreed; no build was run for this documentation-only task.

## Decisions still needed

- Prototype structure and preferred initial view.
- Stack/runtime/routing/rendering approach, after requirements are accepted.
- Content/asset strategy and whether the public demo uses the reference name or a synthetic cinema identity.
- Whether to include a seat-map simulation in the first version.
- Later provider/integration scope and the legal/customer-data boundary.
- Deployment platform and per-action deployment/publication approval.
- License, separately; research completion does not select one.
