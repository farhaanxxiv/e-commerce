@AGENTS.md

# Umami Analytics

This project uses Umami for privacy-friendly analytics. **Whenever adding a new feature, always consider what analytics events should be tracked.**

## Setup
- Script is loaded in `app/layout.tsx` via `next/script` (gated on `NEXT_PUBLIC_UMAMI_WEBSITE_ID` env var)
- `lib/umami.ts` exports `trackEvent(event, data?)` for use in client components

## Tracking approaches
- **Client components** — call `trackEvent("event_name", { key: value })` from `lib/umami.ts`
- **Server components** — add `data-umami-event="event_name"` and `data-umami-event-<key>="value"` HTML attributes; Umami's script picks these up automatically

## Events already tracked
| Event | Where | Data |
|---|---|---|
| `category_filter` | `components/store/category-filter.tsx` | `category` |
| `search_open` | `components/store/search-dialog.tsx` | — |
| `search_select` | `components/store/search-dialog.tsx` | `product` |
| `whatsapp_buy` | `components/store/product-grid.tsx` | `product`, `source: "product_grid"` |
| `whatsapp_buy` | `app/(store)/products/[slug]/page.tsx` | `product`, `source: "product_page"` |

## Required env vars
```
NEXT_PUBLIC_UMAMI_WEBSITE_ID=   # your Umami website ID
NEXT_PUBLIC_UMAMI_SCRIPT_URL=   # defaults to https://cloud.umami.is/script.js
```
