# Functions and user journeys

Research date: 2026-10-13. This inventory separates reachable visitor behavior from generic features found in the shared platform code.

## Public surface map

| Surface | URL/pattern | Observed content | Boundary |
| --- | --- | --- | --- |
| Film catalogue / Афиша | `/`, dated catalogue links | Posters, titles, age ratings, genres, premiere/children/Pushkin Card labels, showtime shortcuts, upcoming films | Vendor-backed live data |
| Daily schedule / Сеансы | `/seances?date=YYYY-MM-DD` | Chronological time/title rows, age/genre information, date controls | Rows launch ticketing; no visible search/filter UI observed |
| Film details | `/release/:id?date=YYYY-MM-DD` | Poster, title, rating where supplied, genres, dates/times, trailer, director/cast fields, duration, country, year, synopsis, upcoming suggestions | Metadata fields vary by film; no prose copied into this dossier |
| Contacts | `/contacts` | Name, box-office phone, address/map link, opening hours, VK | No submitted enquiry form observed |
| Ticket lookup / recovery | `/refund?cinemaID=92` | Phone/email mode, event/date fields, consent controls, Find, vendor support | Actual lookup/resend/refund requires customer data and was not tested |
| Seat selection | Cross-origin widget opened from showtime | Film/date, hall, format, age rating, category price, occupied/available diagram, zoom, registration, recovery/support/share actions | No seat clicked; no hold or checkout initiated |
| Login | Header Вход | Opens an iframe overlay | It remained blank during this attempt; inner auth/account behavior unknown |
| Accessibility mode | Footer/mobile-menu control | Font size, images, palette, serif/sans-serif, line height, letter spacing, reset/normal version | Supplementary mode, not a substitute for baseline accessibility |
| Cookie preferences | Initial banner and footer settings | Technical-required, analytics, marketing categories; cancel/save | Opened/cancelled; consent choices not used as production-compliance proof |
| Legal documents | Footer/widget links | Document entry point; terms/privacy/offer/requisites named in recovery form | Exact document/widget configuration values not reproduced; legal content not audited |

`/cinema/halls`, `/cinema/about`, and `/soon` were also opened because the shared code contains related routes. In this site's current configuration each rendered the **home catalogue fallback**, while retaining the requested path. Do not claim they are active hall, about, or standalone upcoming-film pages.

## Detailed function inventory

| ID | Function | Evidence / status | Redesign implication |
| --- | --- | --- | --- |
| F01 | Switch catalogue date | Today/Tomorrow controls observed | Keep dates explicit and URL-addressable |
| F02 | Switch schedule date | Tomorrow activated; URL changed to `date=2026-10-14` and rows changed | Preserve history/deep-link behavior |
| F03 | Browse current films | Poster grid on desktop, film rows on mobile | Support discovery without a large unrelated hero |
| F04 | Open film details | Cards link to a film route with date | Preserve selected date when navigating/backtracking |
| F05 | Open booking from a time | Sample 14:10 session activated | Use a named semantic link/button, not clickable static text |
| F06 | Show release qualifiers | Premiere, children, age, genres, selected Pushkin Card labels | Keep meaningful eligibility; avoid badge clutter |
| F07 | Show other-date availability | “Сеансы на Завтра” controls observed for films absent today | Make the alternate date explicit; distinguish no sessions from sold out |
| F08 | Browse upcoming releases | “Скоро в кино” section with start dates | Upcoming is not automatically bookable |
| F09 | Scan by time | Chronological schedule observed; 12 rows today, 15 tomorrow in this sample | Add hall/price/format only from authoritative data |
| F10 | Read film information | Sample detail opened and inspected | Make synopsis secondary to purchase-relevant facts |
| F11 | Play trailer | Play control activated; video overlay with native playback controls appeared | No autoplay on page load; accessible labelled trigger/dialog |
| F12 | View seat map | Sample widget rendered small-hall diagram | Demo must use a synthetic, clearly labelled map |
| F13 | See seat categories/availability | 270 ₽ category and occupied legend observed | Price is session-specific; availability changes |
| F14 | Zoom seat map | Plus/minus controls visually observed | Keyboard/list alternative needed; zoom behavior not exercised |
| F15 | Register/login in vendor UI | Registration control observed in seat widget; site login opened blank overlay | No actual account created or authenticated |
| F16 | Recover ticket by phone/email | Both tabs observed; email activated | Separate recovery from refund intent in new navigation |
| F17 | Select event/date for recovery | Required fields observed | Labels and clear local validation; dropdown operation not exhaustively tested |
| F18 | Gate recovery submission | Find disabled in empty/default form; consent controls observed | No submissions/verification codes requested |
| F19 | Resend/refund ticket | Form introduction and public client code indicate downstream paths | Advertised flow, not verified completed transaction |
| F20 | Call box office | `tel:` links observed | Keep one-tap phone access with clear service ownership |
| F21 | Open location/social | Yandex Maps link and VK link observed | Confirm destination and provide accessible names |
| F22 | Open mobile menu | Trigger invoked through DOM; menu expanded | Trigger itself is not keyboard-semantic |
| F23 | Adjust reading settings | Accessibility mode activated; settings/normal-version controls rendered | Build a readable default interface first |
| F24 | Manage cookie preferences | Configure opened; cancel activated | Accessible focus management; clear reject/preferences actions |
| F25 | Read legal notices | Footer and recovery form expose document entry points | Do not transplant another business's legal documents |
| F26 | Share/support from widget | Share, recovery, vendor support labels observed | Not activated; keep vendor ownership clear |

## Journey A: “I know the film”

Observed path:

`Catalogue → film detail → date/time → ticket widget → seating diagram`

There are also time shortcuts on catalogue cards. A card-wide link contains separate-looking time targets, making navigation and booking intent less clear to keyboard/assistive-technology users.

Proposed path:

`Film → session with full date + hall + format + price → clearly disclosed demo/vendor boundary`

Keep a film title link separate from showtime buttons. Return visitors should not need to scroll through the synopsis to find today's sessions. Remember the selected date in the URL, not only in transient application state.

## Journey B: “I can go at this time”

Observed path:

`Сеансы → Today/Tomorrow → chronological row → ticket widget`

The schedule is compact and useful, but the inspected rows showed time/title/age/genre without price/hall. Rows are non-semantic `div` elements with no button/link role or tab stop.

Proposed path:

`Date → chronological sessions → optional time window/family/eligibility filters → session`

Keep chronological order. A proposed time-window filter must handle a cinema business day crossing midnight and must not hide all sessions without a visible reset/empty state.

## Journey C: “We are going with children”

Observed: age ratings, children labels, and some Pushkin Card labels aid browsing, but no dedicated visible family filter was found.

Proposed: use factual age/genre criteria, not an invented suitability guarantee. Age rating, runtime, date/time, and relevant eligibility belong near the session decision. Pushkin Card eligibility is different from “for children.”

## Journey D: “My ticket did not arrive”

Observed path:

`Header recovery link → phone/email + event + date + consents → disabled Find until requirements are satisfied`

No private data was entered. Sending a verification code, finding an order, resending a ticket, and completing a refund are unverified.

Proposed: “Билеты и помощь” with distinct “Билет не пришёл” and “Возврат” intents, clearly attributed ticket-provider support, and useful recovery instructions. A public portfolio demo must not accept real customer orders or silently forward personal data.

## Journey E: “Where is the cinema?”

Observed: contacts include address, map link, hours, phone, and VK. On mobile, some information is also in the expanding menu.

Proposed: retain direct contacts, add confirmed entrance/arrival/accessibility details when available, and keep any interactive map optional. Unknown parking or wheelchair access must not be filled with plausible-sounding copy.

## What was not established as active

The shared storefront bundle/vendor product catalogue includes conditional support for news, promotions, editorial pages, halls/about pages, multiple cinemas/cities, standalone upcoming content, non-film events, VIP/IMAX sections, Pushkin Card routes, app links, and other layouts. That is **platform capability**, not this cinema's enabled feature list.

Not verified for Юность: search, genre/price/format filters, favourites, email subscription, loyalty account, promo codes, gift certificates, online food ordering, own mobile apps, on-site event rental forms, official Telegram, multi-language controls, or a cinema administrator interface.

## Transaction boundary and unknowns

The observed seat map is the furthest inspected transaction stage. No seat-selection operation was performed because it may affect live inventory.

Unknown downstream contracts include:

- Seat locks, lock duration/expiry, concurrent purchases, selection limits, accessible/VIP seat rules.
- Order creation, final totals/fees, promo codes, loyalty, optional registration, required purchaser details.
- Payment providers actually offered per session/order, fiscal receipt behavior, redirect/return/error states.
- Pushkin Card verification/payment restrictions and failed eligibility handling.
- Successful QR/e-ticket delivery, resend authentication, refund eligibility, cutoffs, cancellation status, and refund timings.

Footer payment logos (MIR, Visa, Mastercard, Maestro, SBP, SberPay) were observed. They are **displayed branding**, not proof that every method is currently accepted for every transaction.
