# FIPS 140-2 → 140-3 transition: widely-deployed crypto modules, verified against NIST CMVP

**Data collected 2026-10-10, ~16:40Z.** Method: direct fetches of the CMVP validated-modules
search (`?moduleName=X`, server-rendered HTML) + per-certificate pages (`/certificate/<n>`)
for Status/Standard. No third-party summaries — every row links to the CMVP certificate page.

## The transition (confirmed at source)
Per the [CMVP program page](https://csrc.nist.gov/projects/cryptographic-module-validation-program):
FIPS 140-2 validated modules are accepted for **new federal systems through September 21, 2026**;
after that they move to the **Historical list** (existing systems only, risk-based).

## Verified rows (newest certificate per widely-deployed module family)

| module family | newest cert | vendor | standard | status | validated |
|---|---|---|---|---|---|
| wolfCrypt | [#5548](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5548) | wolfSSL Inc. | FIPS 140-3 | **Active** | 10/09/2026 |
| wolfCrypt | [#5041](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5041) | wolfSSL Inc. | FIPS 140-3 | **Active** | 07/18/2025 |
| GnuTLS (Rocky 9) | [#5496](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5496) | Ctrl IQ, Inc. | FIPS 140-3 | **Active** | 08/18/2026 |
| AWS-LC | [#5429](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5429) | Amazon Web Services Inc. | FIPS 140-3 | **Active** | 07/20/2026 |
| libgcrypt (SUSE) | [#5420](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5420) | SUSE, LLC | FIPS 140-3 | **Active** | 07/16/2026 |
| OpenSSL FIPS Provider (upstream, current) | [#4985](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4985) | The OpenSSL Project | FIPS 140-3 | **Active** | 03/11/2025 |
| Red Hat RHEL 9 OpenSSL | [#4857](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4857) | Red Hat, Inc. | FIPS 140-3 | **Active** | 10/29/2024 |
| Canonical Ubuntu 24.04 OpenSSL | [#5115](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5115) | Canonical Ltd. | FIPS 140-3 | **Active** | 01/06/2026 |
| SUSE OpenSSL 3 | [#5096](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5096) | SUSE LLC | FIPS 140-3 | **Active** | 11/26/2025 |
| Amazon Linux 2023 OpenSSL | [#5438](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5438) | Amazon Web Services, Inc. | FIPS 140-3 | **Active** | 07/27/2026 |
| AlmaLinux 9 OpenSSL (TuxCare) | [#5482](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5482) | Cloudlinux Inc., TuxCare | FIPS 140-3 | **Active** | 08/13/2026 |
| **OpenSSL FIPS Provider (the old canonical cert)** | [#4282](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4282) | The OpenSSL Project | FIPS 140-2 | **Historical** ("moved to historical list due to sunsetting") | — |
| **NSS (Mozilla)** | — | — | — | **no CMVP validation found** (module-name search: "Network Security", "Mozilla" → no results) | — |
| mbed TLS / Botan / BoringSSL | — | — | — | no CMVP validation found under those names (BoringSSL famously has none; AWS-LC is AWS's FIPS-capable fork) | — |

## The honest story
1. **The OpenSSL ecosystem already migrated.** The old canonical 140-2 cert (#4282) is Historical;
   the upstream project's own #4985 and the major distros' vendored certs are all 140-3 Active.
   59 OpenSSL-ecosystem certificates exist in CMVP (every distro vendors its own "based on the
   OpenSSL FIPS Provider" module). **Distro users are covered.**
2. **The gap is upstream pins:** teams holding deployments to the #4282-era module (or any 140-2
   cert) are now off the new-procurements list. The audit question changed from "is it validated?"
   to "is it Active?"
3. **wolfSSL validated a cert the day before this table was pulled** (#5548, 10/09/2026) — the
   migration is live and active, not a paper exercise.
4. **NSS has no findable validation** — Firefox-ecosystem users relying on NSS for FIPS compliance
   should verify their own footing (this absence is search-by-name-verified, with the method's
   caveat noted above).

## Method & caveats
- CMVP search matches by module-name substring; the absence rows (NSS/mbed TLS/Botan/BoringSSL)
  reflect name-search misses and could in principle hide differently-named validations. Status +
  Standard live only on the per-certificate pages; the search table shows date/vendor/type only.
- Data as of 2026-10-10; CMVP changes daily (see wolfSSL row). Re-check before citing.
