---
name: Browse Newcastle Permanent banking products (CDR PRD)
description: >-
  Retrieve and inspect Newcastle Permanent's openly-offered banking products
  (term deposits, savings, transaction accounts, home loans, credit cards) via
  the public, unauthenticated Consumer Data Right Product Reference Data API.
api: openapi/newcastle-permanent-cds-banking-products-openapi.yml
base_url: https://openbank.newcastlepermanent.com.au/cds-au/v1
auth: none
operations:
  - listBankingProducts
  - getBankingProductDetail
---

# Browse Newcastle Permanent banking products

Newcastle Permanent Building Society is an Australian CDR data holder. Its
Product Reference Data (PRD) API is **public and unauthenticated** — no API key,
token, or registration is required. It conforms to the DSB Consumer Data
Standards CDR Banking API.

## Conventions you must follow

- **Base URL:** `https://openbank.newcastlepermanent.com.au/cds-au/v1`
- **Version header (required):** send `x-v: 5` on product-list calls and
  `x-v: 7` on product-detail calls (the current endpoint versions). Optionally
  send `x-min-v` for the lowest acceptable version. Omitting `x-v` returns
  `400` (`urn:au-cds:error:cds:header:missing`); an unsupported version returns
  `406` (`urn:au-cds:error:cds:header:unsupported-version`).
- **WAF note:** the endpoint sits behind an F5 web application firewall — send a
  browser-like `User-Agent` and a `Referer` header or you receive a "Request
  Rejected" HTML page instead of JSON.
- **Tracing:** you may send `x-fapi-interaction-id` (a UUID); it is echoed back
  for correlation.
- **Errors:** 4xx responses use the CDS `ResponseErrorListV2` envelope
  (`{ "errors": [ { "code", "title", "detail", "meta" } ] }`) — see
  `errors/newcastle-permanent-problem-types.yml`.

## Step 1 — List products (`listBankingProducts`)

`GET /banking/products` with header `x-v: 5`.

Useful query parameters:
- `product-category` — filter to one of `TERM_DEPOSITS`, `RESIDENTIAL_MORTGAGES`,
  `TRANS_AND_SAVINGS_ACCOUNTS`, `CRED_AND_CHRG_CARDS`, `PERS_LOANS`, etc.
- `effective` — `CURRENT` (default), `FUTURE`, or `ALL`.
- `updated-since` — RFC 3339 timestamp; only products updated after it.
- `page` / `page-size` — standard pagination (default page 1, size 25). Read
  `meta.totalRecords` / `meta.totalPages` and `links.next` to page through.

The response `data.products[]` gives each product's `productId`,
`productCategory`, `name`, `description`, `brand`, and `lastUpdated`. Results are
ordered by `lastUpdated` descending.

## Step 2 — Get product detail (`getBankingProductDetail`)

For any `productId` from step 1, call
`GET /banking/products/{productId}` with header `x-v: 7`.

The `data` object adds the full detail: `features[]`, `constraints[]`,
`eligibility[]`, `fees[]`, `depositRates[]`, `lendingRates[]`, `bundles[]`,
`additionalInformation`, and `cardArt[]`. Rate objects carry `rateConditions[]`.

A `404` (`urn:au-cds:error:cds:resource:invalid`) means the `productId` does not
exist.

## Notes

- This skill covers only the **public** product-reference surface. Consumer data
  (accounts, balances, transactions) requires CDR accredited-data-recipient
  authorisation (OAuth2/OIDC/FAPI + mTLS) and is out of scope here — see
  `authentication/newcastle-permanent-authentication.yml`.
