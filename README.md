# V2X PKI — Formal Verification Artefact

Formal verification artefact accompanying the paper

> **Formal Security Requirements for the V2X PKI**
> Simone Bussa, Daniel Clark, Tom Chothia, Luca Arnaboldi.
> Submitted to ESORICS 2026.

This repository holds the ProVerif models, the full Threat Analysis and Risk Assessment (TARA) outputs, and the complete requirements catalogue that the paper summarises. The paper refers here for message-level details and the complete P01–P106 list.

## Contents

### `TARA/` — ISO/SAE 21434 TARA outputs (full)

The paper shows only excerpts. This folder contains the full catalogue:

| File | Contents |
|------|----------|
| `01_Asset_identification.pdf` | Complete asset inventory (A-series) |
| `02_Damage_scenarios.xlsx` | Damage scenarios with safety / operational / financial / privacy impact scoring (DS-series) |
| `03_Threat_identification.pdf` | STRIDE-derived threats against the V2X PKI (TS-series) |
| `04_Security_privacy_requirements.pdf` | Full P01–P106 security and privacy requirements |

### `proverif-models/` — ProVerif sources

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
