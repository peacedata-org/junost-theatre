# Public client code and integration boundaries

Inspected on 2026-10-13. **This is not access to the original repository, backend source, build configuration, contracts, or administration.** Only publicly delivered frontend artifacts and anonymous rendered behavior were inspected.

## Architecture established by inspection

```text
junost.ru HTML application shell
    ├── public CSS, fonts, hashed JavaScript bundles
    ├── React-rendered film catalogue / schedule / details / contacts
    ├── requests to kinokassa.kinoplan24.ru API v2
    ├── film/poster/trailer resources on Kinoplan media hosts
    ├── Yandex Metrika resources
    └── kinowidget.kinoplan.ru cross-origin ticket iframe
            └── seat map and vendor-owned transaction UI
```

| Finding | Evidence level |
| --- | --- |
| Client-rendered React application | Initial empty root; React properties on rendered root; production React/React DOM bundle code |
| React DOM version marker `19.2.4` | Production renderer/reconciler marker in inspected vendor bundle; not a reconstructed dependency lockfile |
| Webpack-style chunks/runtime | Separate hashed runtime/vendor/app bundles and chunk registrations/loading |
| Redux-related state and i18next/Moment-related code included | Named identifiers/call sites in delivered bundles; exact versions not established |
| CSS uses BEM-like component selectors and generated class names | Rendered selectors such as header/release/calendar and hashed classes |
| Tenant/configuration-driven storefront | Conditional routes/navigation, runtime branding colours, provider configuration in HTML |
| Nginx observed as serving layer | Response server header; does not identify backend language, hosting provider, or infrastructure topology |
| Sentry SDK code included; version marker `8.27.0` | Public vendor bundle; no claim that active error reporting was verified |

A string match for another framework in a shared bundle is not enough to call it the site's framework. The React conclusion is based on render/runtime evidence, not substring searches alone.

## Inspected primary artifact sizes

Decoded response-body sizes, not compressed transfer sizes:

| Artifact | Bytes |
| --- | ---: |
| `common/app.min.42f68b9e400b2b72.js` | 436,473 |
| `common/chunks/vendor.min.f007f92b763ebbd7.js` | 628,681 |
| `common/common-styles.min.044d0d286334fa03.css` | 175,787 |
| `common/app.min.5ac620578a1fa53f.css` | 57,228 |

Those two JS bodies total about 1.02 MiB decoded. They exclude runtime, route chunks, ticket-widget resources, analytics, media, and fonts. In the initial unthrottled browser capture, the app/vendor transfer entries were approximately 142/201 kB including protocol overhead; later warm-cache requests differed. Do not use decoded bytes as a page-load measurement.

No `sourceMappingURL` reference was found in the two inspected JS bundles. This does not establish that no maps exist elsewhere; map discovery was not pursued.

Reference bundles were temporarily read for analysis, not added to this repository, reformatted into a derivative app, or treated as licensed reusable code. Backend language/database/authentication/session storage and original TypeScript/source layout remain unknown.

## Observed data-request families

Resource metadata on the home page showed requests to `https://kinokassa.kinoplan24.ru/api/v2/` with the following path families. No authentication/configuration values, headers, customer payloads, or copied responses are recorded here.

| Path family | Role inferred from call sites/rendered behavior |
| --- | --- |
| `/app` | Application/cinema configuration |
| `/location` | Location selection/context |
| `/cinema/analytics` | Cinema analytics configuration |
| `/promo` | Promotions |
| `/articles` | Editorial/news content |
| `/pages` | Configurable pages |
| `/banners` | Banner content |
| `/release/soon` | Upcoming releases |
| `/release/playbill/info` | Catalogue/schedule information |
| `/release/playbill` | Films and schedule for selected context/date |

The app bundle also contains call sites for film details and film sessions (`/release/:id`, `/release/:id/seances`), cinema-about/hall data, feedback, and recovery/verification operations. **Code presence is not authorization to call them and does not establish a stable, supported public API.** No verification/contact mutation endpoint was invoked.

Request-body schemas, credentials model, rate limits, pagination, caching rules, timezone semantics, error formats, and supported integration terms were not established. Do not build a production integration by copying requests observed in DevTools.

## Configurable routes versus enabled pages

Shared code includes route families for:

- Film releases and seances.
- Multiple cinemas/cities and cinema information.
- News/articles and promotions.
- Upcoming releases, alternative/non-film events, Pushkin Card content.
- IMAX/VIP sections and app-store redirects.
- Recovery, legal documents, and template/settings behavior.

The actual visible Юность navigation remained catalogue, schedule, and contacts. Some conditional route probes rendered the catalogue fallback. This is consistent with a multi-tenant product whose codebase supports more than one cinema configuration.

Do not probe or expose preview/admin/settings routes merely because their strings exist in a public bundle. No administrative access was attempted.

## Media and typography

- Posters were served from Kinoplan image hosts with size/fit parameters. Desktop sample requested up to 999 × 999; mobile sample used a 256-size request, then rendered a small portrait thumbnail.
- Upcoming posters also used smaller image requests.
- Native `srcset` was not present on sampled images; some images used lazyload classes. The full lazy-loading strategy was not reconstructed.
- Trailer activation rendered a video overlay using a Kinoplan media host and native controls.
- Self-hosted Manrope WOFF2 font resources were observed. Inclusion of fonts in delivered files does not grant redistribution rights; select and document permitted font licensing independently.
- Wordmark, background ad, film art, stills, and trailer footage remain third-party content. Do not hotlink or republish them as demo assets without appropriate rights.

## Ticketing is a separate product boundary

Opening a film's showtime created an embedded page from `kinowidget.kinoplan.ru`. The seat screen displayed the selected cinema/film/date, small hall, format, age rating, price category, occupied legend, diagram, zoom, registration, support/recovery/share actions, and disabled continuation while no seats were selected.

The storefront colours do not govern the whole widget: the sampled map used its own white/grey surface, blue selected-time chip, green seats, and grey occupied marks.

A storefront implementation may therefore have three materially different production options:

| Option | Ownership | Unresolved requirement |
| --- | --- | --- |
| Official widget or approved external redirect | Custom site handles discovery; provider handles transactions | Written authorization, configuration, supported embedding/branding/accessibility contract |
| Custom transactional UI through supported API/gateway | Custom site handles more UI/state; provider remains inventory/order authority | Vendor contract/docs/sandbox, seat-lock and order semantics, payment/fiscal/privacy responsibilities |
| Portfolio-only simulation | All demo records/inventory/transactions are synthetic and local | Clear demo disclosure; no live provider configuration or real customer collection |

The portfolio scope currently permits only the simulation unless another concrete integration is explicitly authorized. None of these options selects a framework or deployment platform.

## Vendor statements: what they do and do not establish

[Kinoplan's current product catalogue](https://kinoplan.ru/) describes storefronts/widgets, box-office ticketing, online ticket/bar sales, CRM/loyalty, reports, kiosks, apps, QR control, repertoire planning, TMS, and aggregator integrations. These are vendor capabilities, **not proof that Юность uses every product**.

A [historical vendor article](https://kinoplan.ru/news/premiera-top-3) describes several licensed/partner paths for online sales connected to Premiera. It is a vendor statement, contains references to 2019, and is not current legal advice or proof of Юность's box-office product/version.

The [April 2026 update](https://kinoplan.ru/tpost/657sns5xk1-novosti-i-obnovleniya-aprel-2026) states that cinemas with their own online sales can use a CRM API for user/order-related operations and obtain documentation from support/product contacts. It does not establish an unrestricted public seat-booking API.

## Questions before any real integration

1. Which box-office product/version and online-sales contract are actually active?
2. Does the venue/provider authorize a custom storefront, widget embedding, a redirect, or a custom checkout?
3. Which documented APIs are supported, with what environments, authentication, limits, and version/change policy?
4. Which system owns seat inventory, holds, expiry, orders, prices, discounts, refunds, and cancellation state?
5. What happens when two customers select the same seat or an offline box-office sale changes availability?
6. Are provider failure/retry/return events exposed, and can the site safely recover without duplicating an order?
7. Who is responsible for payments, receipts, customer data, consent, retention, and legal documents?
8. Which poster/trailer/brand/editorial materials may the new site use, and under what rights?
9. What purchase-completion analytics can be shared lawfully, rather than inferring completion from widget opens?
10. Which accessibility requirements and integration customizations are supported inside the provider widget?

Do not contact the venue/vendor, request access credentials, subscribe to services, or deploy on their behalf as part of this research task.
