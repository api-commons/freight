# Freight and TMS

The common freight vocabulary -- the loads that move by truck, the freight quotes that price them, the tenders that offer them to carriers and the trucking carriers who haul them -- distilled from the APIs that already exist. Parcel shipping belongs to the shipping context. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Freight, Trucking, TMS, Transportation Management, Freight Brokerage, LTL, Truckload, Logistics in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| load | 12 | 9 | commodity 56%, id 56%, status 56%, weight 56% | loads 10, load 1, shipments 1 |
| freight_carrier | 5 | 4 | email 75%, id 75%, name 75%, phone 75% | carriers 3, carrier 2 |

Cohort: 205 providers with harvested OpenAPI, 12 crosswalks. Of the providers exposing a load: 75% create, 50% list, 58% fetch, 17% update, 33% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A load agrees on its weight, commodity, status and id: what is moving and how heavy, not where -- origin, destination and dates are each nested differently (stops, pickup/delivery objects, addresses).
- Freight publishes thinly as OpenAPI: 205 providers in the cohort, 13 mapped.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Loads cover freight shipments, TMS orders and freight bookings; parcel shipments are shipping's.
- Carriers are `/freight-carriers` (trucking companies identified by SCAC, DOT and MC numbers); shipping's carriers are parcel networks.
- Freight quotes and tenders were measured and dropped.
- Duplicates merged: Kargo.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
