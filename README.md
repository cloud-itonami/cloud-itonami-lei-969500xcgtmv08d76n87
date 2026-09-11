# cloud-itonami-lei-969500xcgtmv08d76n87

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Europcar Mobility Group SA.**

This repository archives the publicly published Terms of Use / Terms and Conditions of
**Europcar Mobility Group SA**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Europcar Mobility Group SA — the live GLEIF record (last updated
  2026-03-27) registers the name as `EUROPCAR MOBILITY GROUP` (language `fr`, no
  other names); the `SA` here is the ISO 20275 legal form `5VCF`
  (`SA à directoire (s.a.i.)`), not part of the registered name. `facts.edn`
  below carries the registry's spelling, and the checker flags the suffixed form
  as drift if it is written into `facts.edn`.
- **LEI (ISO 17442)**: [969500XCGTMV08D76N87](https://search.gleif.org/#/record/969500XCGTMV08D76N87) (GLEIF-verified)
- **Jurisdiction**: FR — registered with INSEE's Sirene register (`RA000189`,
  SIREN `489099903`, OpenCorporates `fr/489099903`), created 2006-03-05, seat at
  13T Boulevard Berthier, 75017 Paris.
- **Website**: https://www.europcar-mobility-group.com
- **Ticker**: (unknown) — GLEIF maps **6 ISINs** to this LEI (`FR0014001HB5`,
  `FR0014001HC3`, `FR0014006U91`, `FR0011083039`, `FR0014001HD1`,
  `FR0012789949`; each is an entity in `facts.edn`). Whether any of them is
  currently admitted to trading, and on which venue, is not something GLEIF
  answers, so no ticker is asserted here.

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived Terms of Use documents,
  each entry carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`,
  `:tos/sha256`, `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 17 verified registry facts with per-fact provenance (the entity, its
  registration, issuer and issuer accreditation, registration authority, legal form,
  securities count plus the 6 securities themselves, children count plus the 2
  children themselves, and both parent-reporting exceptions). **Generated** — see
  below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind
them. `facts.edn` now carries them as data, and every value in it was read out of a
public registry response whose URL and retrieval time sit next to the value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T08:05Z, golden copy 2026-08-23T00:00Z) — the LEI record (legal name
`EUROPCAR MOBILITY GROUP`, jurisdiction `FR`, entity **ACTIVE**, registration
**ISSUED** with the next renewal due 2027-01-19, last updated 2026-03-27,
`FULLY_CORROBORATED`, conformity flag `CONFORMING`, no BIC, S&P Global id
`36567370`, OpenCorporates `fr/489099903`; entity status and registration status
are different fields and are recorded separately), its **6 ISINs**, read from
`meta.pagination.total` of the cited page (the whole list fits in one page, so
each identifier is also mirrored as a `:security` entity), its managing LOU and
LEI-issuer accreditation (INSEE — Institut National de la Statistique et des
Études Économiques, LEI `969500Q2MA9VBQ8BG884`, accredited 2018-01-30),
registration authority `RA000189` (Register of Companies — Sirene, INSEE), ISO
20275 legal form `5VCF` (`SA à directoire (s.a.i.)`, `FR`), reporting exceptions
at both consolidation levels (`NO_KNOWN_PERSON` — GLEIF's relationship data
records no accounting-consolidation parent for this entity and gives that
reason; this file records the registry's answer, not a group chart, so nothing
about who owns the group is asserted here), and **2 direct children**, read from
`meta.pagination.total` of the cited page and each mirrored as a `:direct-child`
entity (`EUROPCAR PARTICIPATIONS`, LEI `969500D928TX61MHVK19`, and
`EUROPCAR INTERNATIONAL SA`, LEI `969500YFACU6IWBY7S55`, both `FR`, both
ACTIVE). The `direct-parent` and `ultimate-parent` endpoints answered `404`
because GLEIF publishes the exception side of that pair for this entity, which
the checker treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the
live sources, `1` a citation broke or a fact drifted, `3` the check could not be
performed at all — an absent `facts.edn`, or every request failing at the
transport level. A check that could not run must not be indistinguishable from a
check that ran and found nothing, so it refuses to report a pass rather than
exiting 0. All outcomes were exercised before this landed: unmodified `0`
(`OK all 17 recorded fact(s) still match`); `:securities/isin-count` edited
`6` → `7` → `1` naming `DRIFT gleif-isins :securities/isin-count`;
`:company/legal-name` rewritten to `EUROPCAR MOBILITY GROUP SA` → `1` naming
`DRIFT gleif-lei-record :company/legal-name`; the measured
`:relationship/direct-child-count` rewritten `2` → `1` → `1` naming
`DRIFT gleif-direct-children-count`; the direct-level
`:relationship/exception-reason` rewritten to `NON_CONSOLIDATING` → `1` naming
`DRIFT gleif-direct-parent-reporting-exception :relationship/exception-reason`;
SIREN `489099903` rewritten `489099904` → `1` naming the drift in
`gleif-lei-record` (`:company/registered-as` and `:company/open-corporates-id`)
and `gleif-registration-authority`; the `gleif-isin-fr0012789949` entity
deleted → `1` naming `ADDED gleif-isin-fr0012789949`; `:elf/local-name`
rewritten → `1` naming `DRIFT iso-20275-entity-legal-form :elf/local-name`; the
GLEIF host in the checker rewritten to an unresolvable name → `3`
(`INCONCLUSIVE … refusing to report a pass`); and with no `facts.edn` at all →
`3`.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
