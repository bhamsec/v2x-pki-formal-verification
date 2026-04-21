# V2X PKI — Formal Verification Artefact

Formal verification artefact accompanying the paper

> **Formal Security Requirements for the V2X PKI**
> Simone Bussa, Daniel Clark, Tom Chothia, Luca Arnaboldi.
> Submitted to ESORICS 2026.

This repository holds the ProVerif models, the full Threat Analysis and Risk Assessment (TARA) outputs, and the complete security requirements catalogue that the paper summarises. The paper refers here for all tabular detail the paper itself does not carry: verification outcomes, the full TARA derivation, and the complete P01–P106 requirements list.

## Contents

### Quick links

| | What | Where |
|-|------|-------|
| Verification results | Per-property × per-model pass/fail matrix + CA-compromise footnotes | [`RESULTS.md`](./RESULTS.md) |
| Security requirements | Full P01–P106 list (browsable) | [`REQUIREMENTS.md`](./REQUIREMENTS.md) |
| Security requirements (PDF) | Same list, as rendered in the original deliverable | [`TARA/04_Security_privacy_requirements.pdf`](./TARA/04_Security_privacy_requirements.pdf) |
| Asset inventory | Complete asset list (A-series) | [`TARA/01_Asset_identification.pdf`](./TARA/01_Asset_identification.pdf) |
| Damage scenarios | With safety/operations/financial/privacy impact scoring (DS-series) | [`TARA/02_Damage_scenarios.xlsx`](./TARA/02_Damage_scenarios.xlsx) |
| Threat scenarios | STRIDE-derived threats (TS-series) | [`TARA/03_Threat_identification.pdf`](./TARA/03_Threat_identification.pdf) |
| ProVerif sources | 5 models + per-attack variants | [`proverif-models/`](./proverif-models/) |

### [`RESULTS.md`](./RESULTS.md)

The complete 34-property × 5-model verification matrix that the paper summarises in Section 6, grouped by protocol phase, together with the list of consequences when the AA or EA is compromised.

### [`REQUIREMENTS.md`](./REQUIREMENTS.md)

The complete P01–P106 security and privacy requirements catalogue derived via TARA (ISO/SAE 21434). Grouped by protected asset. Browsable on GitHub; the rendered PDF version is [`TARA/04_Security_privacy_requirements.pdf`](./TARA/04_Security_privacy_requirements.pdf).

### `TARA/` — ISO/SAE 21434 outputs

- **`01_Asset_identification.pdf`** — full asset inventory (A-series): registration, enrolment, authorisation data for each actor (ITS-S, EA, AA), plus authorisation and authorisation-validation requests and responses. Each asset is tagged with the Confidentiality / Integrity / Availability properties it requires.
- **`02_Damage_scenarios.xlsx`** — damage scenarios (DS-series): operational context, compromise type, unwanted behaviour, consequence, and a four-axis impact score (safety, operations, financial, privacy) on {Negligible, Moderate, Severe}.
- **`03_Threat_identification.pdf`** — threat scenarios (TS-series): STRIDE-classified threats tied to specific assets and properties. Generated with the Microsoft Threat Modelling Tool.
- **`04_Security_privacy_requirements.pdf`** — the rendered PDF of the full P01–P106 list (same content as [`REQUIREMENTS.md`](./REQUIREMENTS.md)).

### [`proverif-models/`](./proverif-models/)

Five formal models of ETSI 102 940, plus per-attack variants.

- `model1/` … `model5/` — the five models analysed in the paper (see Table 1 of the paper for the Ts / PoP / attacker-capability matrix).
- `attack 01 - PoP PubAT/` … `attack 08 - Compromised AA and EA capabilities/` — per-vulnerability sources and queries, one subdirectory per attack scenario identified in Section 6 of the paper.
- `README.md` — a per-attack reference listing the queries and their expected ProVerif outcomes (with and without the proposed fixes).

## Reproducing the analysis

All `.pv` files can be run directly with ProVerif. The paper was checked against ProVerif 2.05; any recent version should work. Each `.pv` is self-contained and can be run with:

```
proverif <file>.pv
```

Expected outcomes and fixes are documented in `proverif-models/README.md`.

## Authors

- **Simone Bussa** — Politecnico di Torino, Italy
- **Daniel Clark** — University of Birmingham, UK
- **Tom Chothia** — University of Birmingham, UK
- **Luca Arnaboldi** — University of Birmingham, UK

## Citation

A BibTeX entry will be added once the paper is accepted.

## License

Released under the MIT License — see [LICENSE](./LICENSE).
