# Newcastle Permanent Building Society (newcastle-permanent)

Newcastle Permanent Building Society is a customer-owned Australian authorised deposit-taking institution (ADI) founded in 1903 and headquartered in Newcastle, New South Wales. As a mutual, it is owned by its members rather than shareholders. In March 2023 it merged with Greater Bank to form Newcastle Greater Mutual Group (NGM Group), one of Australia's largest customer-owned banks, while Newcastle Permanent continues to operate as a consumer brand. As a regulated ADI it is a data holder under Australia's Consumer Data Right (CDR / Open Banking) and exposes a live, public, unauthenticated Product Reference Data (PRD) API conforming to the Data Standards Body Consumer Data Standards.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/newcastle-permanent/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/newcastle-permanent/refs/heads/main/apis.yml)

## Tags

- Financial
- Banks
- Open Banking
- CDR
- Consumer Banking
- Building Society
- Mutual
- Australia

## Timestamps

- **Created:** 2026-07-20
- **Modified:** 2026-07-20

## APIs

### Newcastle Permanent Building Society CDR Product Reference Data API

Live, public, unauthenticated Consumer Data Right (CDR) Product Reference Data (PRD) API exposing Newcastle Permanent's banking product catalogue (term deposits, savings, transaction accounts, home loans, credit cards and more) under the standard Consumer Data Standards path `/cds-au/v1/banking/products`. Confirmed live with an HTTP 200 JSON response carrying a `data.products` array, an `x-v` response version header, and `x-fapi-interaction-id`, currently serving 41 products at endpoint version `x-v` 4.

- **Human URL:** [https://developer.newcastlepermanent.com.au/](https://developer.newcastlepermanent.com.au/)
- **Base URL:** `https://openbank.newcastlepermanent.com.au/cds-au/v1/banking/products`

#### Tags

- CDR
- Open Banking
- Product Reference Data
- Banking
- Australia

#### Properties

- [Documentation](https://developer.newcastlepermanent.com.au/)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-banking-api_get-products)
- [OpenAPI](openapi/newcastle-permanent-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Website](https://www.newcastlepermanent.com.au/)
- [Developer Portal](https://developer.newcastlepermanent.com.au/)
- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)
- [LinkedIn](https://www.linkedin.com/company/newcastle-permanent)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
