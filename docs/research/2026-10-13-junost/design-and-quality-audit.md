# Design and quality audit

Inspected on 2026-10-13. Visual observations, measured values, automated findings, and proposed changes are separated below.

## Existing layout and styles

| Element | Observed/measured implementation |
| --- | --- |
| Outer page | Dark background, `#202020`; large advertising image above/behind the desktop site |
| Desktop width | Header/site width 1240 px at 1440 and 1920 px viewports |
| Header | Blue `#01579b`; orange wordmark, address, phone, VK, ticket-recovery action |
| Footer | Dark blue `#002f6c`; menu, payment logos, legal links, contact/hours, accessibility control |
| Accent | Orange `#ff6d00`; selected dates, showtimes, badges, login/recovery actions |
| Catalogue surface | White, with a pale grey date-control strip |
| Main type | Computed `Manrope, sans-serif`; regular, light, medium, bold WOFF2 resources observed |
| Shared styles | Also contain Inter and other fallback/template fonts; not all are active on this storefront |
| Navigation text | 14 px in desktop navigation; ordinary horizontal link row |
| Date controls | Rounded pills, 32 px high in the measured normal interface |
| Film cards at 1440 px | Four columns; first card 265 px wide; rounded poster corners |
| Film cards at 768 px | Grid cards approximately 224 px wide |
| Film cards at 1024 px | Grid cards approximately 227 px wide |
| Film rows at 390 px | Full-width rows; poster approximately 60 × 88 px; title/qualifiers/times to the right |
| Mobile header | Logo, login pill, menu icon; navigation remains below the header |
| Cookie banner | Lower-right desktop panel; nearly full-width bottom panel on mobile |

At the sampled 1440 × 1000 desktop viewport, the header began about **245 px** below the viewport top and the first poster began about **453 px** down. The advertising background therefore occupies substantial initial space before the catalogue. This is an observed layout fact; whether advertising revenue justifies it is a business decision, not something this audit can establish.

## What already works

- Film titles, age ratings, genres, and time shortcuts are present without opening every film.
- Film discovery and time-based browsing have separate views.
- The catalogue changes to rows on small screens rather than squeezing four desktop columns into mobile.
- Contacts and ticket recovery are directly linked.
- Date changes use the URL; film pages have their own canonical URLs.
- The sampled layouts did not produce document-level horizontal overflow.
- An accessibility-settings mode exists and was opened successfully.

## Specific usability problems and changes

| Issue | Evidence | Proposed change |
| --- | --- | --- |
| Advertising precedes the primary task on desktop | Initial screenshot and header/poster positions | Put date/session access first; if ads are included, give them an explicit, bounded slot |
| Schedule hides decision data until widget open | Observed rows show time/title/age/genres, not hall/price | Add hall, format, and price to session controls only when authoritative data supplies them |
| One film card combines title navigation and booking targets | Card is a link containing clickable-looking times | Separate the film link from semantic showtime actions |
| Cookie panel obstructs lower mobile content | 390 × 844 screenshot; panel around 240 px high | Reduce obstruction; provide clear choices and accessible preferences without covering the active booking controls |
| Mobile menu duplicates navigation | Same links in main row and expanding menu | Keep one primary nav model; use the menu for genuinely secondary actions |
| Date horizon is unclear | Today/Tomorrow only in the sampled published schedule | Show available dates explicitly; do not fabricate sessions beyond the provider's published horizon |
| Midnight session date can be ambiguous | 00:05 displayed alongside an October 13 business-day schedule | Display the actual calendar date/time and explain business-day grouping where needed |
| Recovery and refund share one initial form | Recovery copy mentions both resend and refund | Let the user choose the intent; do not imply a refund has happened after simple lookup |
| Venue information is minimal | Contacts has address/phone/hours/VK but no confirmed arrival/accessibility details | Add verified entrance, access, transit, and hall information when available |
| Unavailable conditional routes show home content | `/cinema/halls`, `/cinema/about`, `/soon` render catalogue | Use deliberate redirects or meaningful not-found states rather than unrelated content under the original path |

These recommendations are not claims of increased revenue or conversion. They require usability testing and provider data to validate.

## Accessibility findings

### Confirmed from DOM, accessibility tree, or automated audit

| Finding | Evidence | Required treatment in the new interface |
| --- | --- | --- |
| Mobile zoom restricted | Viewport has `maximum-scale=1,user-scalable=no`; Lighthouse failure | Do not restrict browser zoom |
| Document language absent | Empty `html.lang`; Lighthouse failure | Use `lang="ru"` for Russian visitor content |
| Home lacks main landmark | DOM inspection and mobile Lighthouse | One main landmark for page content |
| Home/schedule/film pages lack `h1` | DOM inspection | One appropriate page heading; film title should be a heading |
| Showtime rows not keyboard-semantic | `.daily-seance-item` is `DIV`, no role, `tabIndex=-1`; times appear as static text in tree | Use links/buttons with full accessible names |
| Mobile menu trigger not keyboard-semantic | `.header-menu__icon` is `DIV`, no role/name/tab stop | Labelled button with expanded/control relationships |
| Closed menu still exposed | Height zero/overflow hidden, no `aria-hidden`; its links remain in the accessibility snapshot | Remove collapsed content from interaction/accessibility or use a suitable native disclosure pattern |
| Some links lack accessible names | Advertising background link and footer VK link flagged by Lighthouse | Name meaningful links; remove empty decorative links |
| Address pseudo-links lack `href` | Header links flagged by Lighthouse | Real navigation destinations or non-interactive text |
| Cookie preference overlay does not announce itself as a dialog | Form overlay, no dialog role/aria-modal; focus remained on background Configure immediately after opening | Accessible dialog semantics, entry focus, keyboard containment/dismissal, return focus |
| Widget iframe lacks a title | DOM inspection | Give the provider surface a useful iframe title where integration permits |
| Some controls are small | Login/date pills measured 32 px high; normal recovery action 32 px | Use adequate targets/spacing; target 44–48 px for main touch actions |

The default `div` menu icon measured only 18 × 2 px as an element rectangle; its surrounding visual/pseudo-element hit area was not separately measured. The conclusive finding is its missing keyboard semantics, not a precise final pointer-target area.

### Measured contrast failures

| Rendered pair | Ratio | Location/source |
| --- | --- | --- |
| `#99bcd7` on `#01579b` | 3.71:1 | 13 px secondary header address/contact text; desktop schedule Lighthouse |
| `#8097b6` on `#002f6c` | 4.32:1 | 12 px footer advertising notice; desktop schedule Lighthouse |
| `#727276` on `#f2f2f5` | 4.28:1 | 12 px film metadata badges; mobile home Lighthouse |

These normal-sized text pairs fall below 4.5:1. Ratios come from the rendered automated audit, not visual estimation of a screenshot. This is not a complete contrast audit of all states or the cross-origin ticket widget.

### Motion and reading settings

- No `prefers-reduced-motion` rule was found in the two inspected primary CSS bundles. That is a source-inspection finding, not proof that every script animation ignores the setting.
- Trailer playback starts after activating the play control; no page-load autoplay was established.
- Accessibility mode exposes font size, image visibility, multiple colour combinations, serif/sans-serif, line heights 1.5/2.0/2.5, letter spacing, reset, and return-to-normal controls.
- Do not rely on a separate “accessible version” to repair non-semantic booking controls in the normal interface.

## Responsive checks

| Width × height | Document width | Sample card width | Check type |
| --- | --- | --- | --- |
| 360 × 800 | 360 px | 360 px | DOM geometry on catalogue fallback |
| 390 × 844 | 390 px | 390 px | Normal home screenshot and DOM; additional mobile/touch menu check |
| 768 × 1024 | 768 px | ~224 px | DOM geometry on catalogue fallback |
| 1024 × 768 | 1024 px | ~227 px | DOM geometry on catalogue fallback |
| 1440 × 1000 | 1440 px | 265 px | Normal home screenshot and DOM |
| 1920 × 1080 | 1920 px | 265 px | DOM geometry on catalogue fallback |

No document-level horizontal overflow was found in these samples. Width-only checks at 360/768/1024/1920 do not establish good wrapping, accessible zoom, every breakpoint, or every widget state. Full visual inspection was limited to representative home/widget views.

## SEO and loading observations

- Initial HTML contains an empty root, static generic title/description, styles, scripts, and provider configuration, not the rendered film catalogue.
- Runtime home/film titles, film description, and canonical links were observed. Preserve this useful route identity; do not incorrectly describe the existing site as having no metadata.
- No structured-data script or Open Graph metadata was found on the inspected home and sample film page.
- `robots.txt` allows crawling. The attempted `sitemap.xml` returned HTML, not a sitemap.
- Public routes falling back to home can create ambiguous indexing; server status/redirect behavior was not exhaustively audited.
- The provided Lighthouse CLI runs did **not include a performance category**. No performance score, LCP/INP/CLS result, or real-user speed claim is made.
- JavaScript and cross-origin data are dependencies for catalogue rendering. The relative impact needs a controlled performance test, not an inference from bundle size alone.

## Priority order

1. Fix semantic controls, language, zoom, page structure, names, contrast, and overlay focus.
2. Make the session decision include the available date/time/hall/format/price data.
3. Remove catalogue obstruction and clarify the mobile navigation/date/session hierarchy.
4. Define loading, missing-data, empty, sold-out, provider-unavailable, and after-midnight behavior.
5. Then refine typography, spacing, imagery, and motion. Do not present a visual restyle as proof of functional improvement.
