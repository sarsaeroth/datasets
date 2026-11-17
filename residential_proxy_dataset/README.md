# Residential-proxy Android application dataset

Android applications that embed the SDK of a commercial residential-proxy provider, with their
provider labels, label provenance and validation status. This is the corpus of *Static Attribution of
Android Residential Proxy Malware Using Graph Kernels* (arXiv:2604.27302).

`residential_proxy_dataset.jsonl` has one JSON record per build (4,524 records), keyed by SHA-256:

```json
{"id": "00012e8f…", "pkg_id": "com.desoline.android.pdfreader", "family": "luminati",
 "proxy_providers": ["luminati"], "label_source": "c2_domain_pivot", "status": "kept",
 "marker_confirmed": true, "date": "2020-06-06", "androzoo_first_seen": "2020-07-14",
 "sources": ["androzoo"], "dex_group": 0, "lineage_group": 0}
```

| Field | Meaning |
|---|---|
| `id` | SHA-256 of the APK |
| `pkg_id` | Android package name |
| `family` | provider label (`multi` for builds carrying the SDKs of two or more providers) |
| `proxy_providers` | providers whose SDK markers were found in the build |
| `label_source` | `mi_network`: network-observed label from Mi et al. (CCS 2021); `dex_pivot`: shares a DEX file with a labeled application; `version_pivot`: another build of a labeled package; `c2_domain_pivot`: reported as contacting the provider's published command-and-control domains |
| `status` | `kept`; `dropped_unvalidated_pivot` (a DEX pivot that carries no marker of its provider's SDK); `multi_label` |
| `marker_confirmed` | whether a marker of the assigned provider's SDK is present in the build |
| `date` | first VirusTotal submission (YYYY-MM-DD), else first AndroZoo sighting; null if neither is known |
| `androzoo_first_seen` | first AndroZoo sighting, where indexed |
| `sources` | where the build was obtained or can be retrieved (`corpus`: AndroZoo or VirusTotal by hash) |
| `dex_group`, `lineage_group` | leakage groups for grouped cross-validation of the 3,777 evaluated applications: builds sharing a DEX file, and builds of one host lineage (shared package name or near-identical call graph), each joined transitively |

Counts: 3,808 kept builds (Luminati 2,085, Monkeysocks 1,125, IPIDEA 205, Popa 182, Oxylabs 91, CashRaven 39,
IPNinja 37, Traffmonetizer 17, and 27 builds of six rarer providers that are not evaluation classes), 675 dropped
pivots and 41 multi-provider builds. Dropped and multi-provider builds are listed so that the validation can be
checked, not for use as labeled data.

The APKs are third-party software and are not redistributed; retrieve them by SHA-256 from AndroZoo or the listed
source. The code and result files that reproduce the paper are in
https://github.com/sarsaeroth/artifacts/tree/main/static.
