# Verification results

Full per-property verification outcomes across the five ProVerif models analysed in the paper. The paper (Section VI) summarises the findings and discusses the seven vulnerabilities (Att1–Att7) in detail; this document carries the complete 34-property matrix and the list of consequences when a CA is compromised.

- **✓** — property holds in the model
- **✗ (*N)** — property fails in the model; footnote `(*N)` explains the consequence (see [Consequences of CA compromise](#consequences-of-ca-compromise) below)
- **AttX** — property fails due to the named attack; full analysis in Section VI of the paper
- **Models:** Model 1 = no timestamps, no PoP; Model 2 = PoP only; Model 3 = PoP + timestamps (baseline secure); Model 4 = Model 3 with compromised AA; Model 5 = Model 3 with compromised EA.

## Enrolment request (ITS-S → EA)

| # | Property | Description | TARA | M1 | M2 | M3 | M4 | M5 |
|---|----------|-------------|------|----|----|----|----|----|
| 1 | Auth-Integ-Conf | Enrolment req: ITS-S → EA | P20, P15, P23 | ✓ | ✓ | ✓ | ✓ | ✗ (*3) |
| 2 | Replay | Enrolment req (injective) | P22 | Att1 | Att1 | ✓ | ✓ | ✗ (*3) |
| 3 | Auth | `Pri_Enr` (PoP) | P26 | ✓ | ✓ | ✓ | ✓ | ✓ |
| 4 | Replay | `Pub_Enr` uniqueness | P25, P43 | ✓ | ✓ | ✓ | ✓ | Att6 |
| 5 | Anonymity | Secret `vid` in enrolment req | P16 | ✓ | ✓ | ✓ | ✓ | ✗ (*3) |
| 6 | Anonymity | Cannot identify ITS-S by EA it contacts | P18 | Att7 | Att7 | Att7 | Att7 | Att7 |

## Enrolment response (EA → ITS-S)

| # | Property | Description | TARA | M1 | M2 | M3 | M4 | M5 |
|---|----------|-------------|------|----|----|----|----|----|
| 7 | Auth-Integ-Conf | Enrolment res: EA → ITS-S | P30, P29, P33 | ✓ | ✓ | ✓ | ✓ | ✗ (*7) |
| 8 | Replay | Enrolment res (injective) | P31 | ✓ | ✓ | ✓ | ✓ | ✗ (*7) |
| 9 | Auth-Integ | `Cert_Enr` issued by EA → ITS-S | P35 | ✓ | ✓ | ✓ | ✓ | ✗ (*8) |
| 10 | Replay | `pseudoid` in `Cert_Enr` uniqueness | P34, P44 | ✓ | ✓ | ✓ | ✓ | Att6 |

## Authorisation request (ITS-S → EA/AA)

| # | Property | Description | TARA | M1 | M2 | M3 | M4 | M5 |
|---|----------|-------------|------|----|----|----|----|----|
| 11 | Auth-Integ-Conf | Authorisation req: ITS-S → EA/AA | P56, P53, P58 | ✓ | ✓ | ✓ | ✗ (*2) | ✗ (*9) |
| 12 | Replay | Authorisation req (injective) | P57 | Att1 | Att1 | ✓ | ✗ (*2) | ✗ (*9) |
| 13 | Auth | `Pri_AT` (PoP) | P62 | ✗ (*1) | ✓ | ✓ | ✓ | ✓ |
| 14 | Replay | `Pub_AT` uniqueness | P61, P79 | Att2 | Att2 | ✓ | Att6 | ✓ |
| 15 | Anonymity | Secret `Cert_Enr` in authorisation req | P65 | ✓ | ✓ | ✓ | ✓ | ✗ (*9) |
| 16 | Anonymity | Cannot profile ITS-S by `services_{req/conf}` | P64, P97 | ✓ | ✓ | ✓ | Att5 | ✓ |
| 17 | Anonymity | Cannot identify ITS-S by AA it contacts | P55 | Att7 | Att7 | Att7 | Att7 | Att7 |
| 18 | Linkability | Cannot link multiple auth reqs → ITS-S | P66 | ✓ | ✓ | ✓ | ✓ | ✗ (*9) |

## Authorisation response (AA → ITS-S)

| # | Property | Description | TARA | M1 | M2 | M3 | M4 | M5 |
|---|----------|-------------|------|----|----|----|----|----|
| 19 | Auth-Integ-Conf | Authorisation res: AA → ITS-S | P68, P67, P71 | ✓ | ✓ | ✓ | ✗ (*3) | ✓ |
| 20 | Replay | Authorisation res (injective) | P69 | ✓ | ✓ | ✓ | ✗ (*3) | ✓ |
| 21 | Anonymity | Secret AT issued by AA → ITS-S | P83 | ✓ | ✓ | ✓ | ✗ (*2) | ✓ |
| 22 | Auth-Integ | `services_conf` (authorised by EA) | P73 | ✓ | ✓ | ✓ | Att4 | Att4 |
| 23 | Auth-Integ | AT issued by AA → ITS-S | P76 | ✓ | ✓ | ✓ | ✗ (*4) | ✓ |
| 24 | Replay | `pseudoid` in AT uniqueness | P75, P80 | ✓ | ✓ | ✓ | Att6 | ✓ |
| 25 | Auth-Integ | AT (authorised by EA) → ITS-S | P72 | ✓ | ✓ | ✓ | Att3 | ✗ (*10) |

## Authorisation validation request (AA → EA)

| # | Property | Description | TARA | M1 | M2 | M3 | M4 | M5 |
|---|----------|-------------|------|----|----|----|----|----|
| 26 | Auth-Integ-Conf | Auth val req: AA → EA | P87, P86, P89 | ✓ | ✓ | ✓ | ✗ (*5) | ✗ (*11) |
| 27 | Replay | Auth val req (injective) | P88 | Att1 | Att1 | ✓ | ✗ (*5) | ✗ (*11) |
| 28 | Linkability | Cannot link multiple auth val reqs → ITS-S | P92 | ✓ | ✓ | ✓ | ✓ | ✗ (*11) |

## Authorisation validation response (EA → AA)

| # | Property | Description | TARA | M1 | M2 | M3 | M4 | M5 |
|---|----------|-------------|------|----|----|----|----|----|
| 29 | Auth-Integ-Conf | Auth val res: EA → AA | P94, P93, P98 | ✓ | ✓ | ✓ | ✓ | ✗ (*10) |
| 30 | Replay | Auth val res (injective) | P95 | ✓ | ✓ | ✓ | ✓ | ✗ (*10) |

## V2X messages

| # | Property | Description | TARA | M1 | M2 | M3 | M4 | M5 |
|---|----------|-------------|------|----|----|----|----|----|
| 31 | Auth-Integ-Conf | V2X msg: ITS-S_rec → ITS-S_snd | P102, P99 | ✓ | ✓ | ✓ | ✗ (*12) | ✗ (*12) |
| 32 | Replay | V2X msg (injective) | P105 | Att1 | Att1 | ✓ | ✗ (*12) | ✗ (*12) |
| 33 | Anonymity | Cannot associate AT and V2X msg → ITS-S | P81, P82, P100 | ✓ | ✓ | ✓ | ✓ | ✓ |
| 34 | Linkability | Cannot link multiple ATs → ITS-S | P106 | ✓ | ✓ | ✓ | ✓ | ✓ |

## Not modelled in ProVerif

Properties that fall outside the symbolic-model threat surface and must be assessed by other means:

- **Physical / access protection** — P1, P4, P7, P10, P11, P46, P48, P49, P84
- **Cryptographic-key strength** — P2, P5, P8, P24, P60
- **Denial of service** — P3, P6, P9, P12, P27, P47, P50, P63, P85, P91

Correctness checks that are folded into the model itself (not exposed as standalone queries): P13, P14, P17, P19, P21, P36, P40, P45, P51, P52, P54, P59, P90, P101, P104.

## Consequences of CA compromise

Footnotes referenced by `✗ (*N)` entries in the tables above.

- **(*1)** PoP not provided.
- **Compromised AA can:**
  - **(*2)** decrypt current and past authorisation requests and responses using `Pri_AA`, revealing `services_req` and issued ATs;
  - **(*3)** refuse to issue, issue unusable, or deliberately downgrade ATs for legitimate ITS-Ss;
  - **(*4)** issue valid ATs to malicious ITS-Ss;
  - **(*5)** execute the authorisation validation phase with an honest EA.
- **Compromised EA can:**
  - **(*6)** decrypt current and past enrolment requests and responses using `Pri_EA`, revealing ITS-S `vid`, `attributes_req`, and issued `Cert_Enr`;
  - **(*7)** refuse to issue, issue unusable, or deliberately downgrade `Cert_Enr` for a legitimate ITS-S registered with it;
  - **(*8)** issue valid `Cert_Enr` to malicious ITS-Ss;
  - **(*9)** decrypt data intended for the EA in the authorisation request, revealing `Cert_Enr` and `services_conf`;
  - **(*10)** refuse to approve, or approve downgraded, authorisation validation requests for honest ITS-Ss, or approve such requests for malicious ITS-Ss;
  - **(*11)** decrypt current and past authorisation-validation requests and responses using `Pri_EA` and link them to a specific ITS-S.
- **Malicious ITS-S issued with a valid `Cert_{Enr_att}` and `AT_att` can:**
  - **(*12)** send V2X messages and access V2X services corresponding to the received AT.
