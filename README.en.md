# tel-icp-license-checker

[![License: MIT](https://img.shields.io/badge/Code%20License-MIT-yellow.svg)](LICENSE)
[![Content: ARR](https://img.shields.io/badge/Content%20License-ARR%20%7C%20citable-blue.svg)](LICENSE-CONTENT)

> **Status: RESERVED (placeholder · open for claim)** — this repository already ships the four-file industry-access skeleton per the platform protocol, and waits for an operator with domain credentials to claim it and fill in real rules.

This is the SynomosAI **domain profile** for telecom ICP filing vs. value-added telecom business licenses. It decomposes "does this website/service need a permit, and which one" into verifiable attributes, so that AI only provides path guidance — never a go-live or licensing conclusion.

## What this domain governs

Internet information services and value-added telecom service licensing verification.

ICP **filing** (备案) and value-added telecom **business license** (经营许可) are frequently conflated: one is a filing, the other is a license, with different triggers. Data-localization and content-compliance are overlay obligations. AI can lay out the business form vs. licensing status; the licensing power belongs to the telecom regulator.

## Domain identity

| Field | Value |
|---|---|
| Domain ID | `tel` (globally unique, never reused) |
| Domain name | Telecom · ICP filing & value-added telecom license |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Reserved at | 2026-09-12 |

## Attributes

| Key | Type | Meaning |
|---|---|---|
| `tel.service_category` | enum | Business category per the telecom classification catalog → filing vs. license · information_service/value_added/basic/other |
| `tel.license_type` | enum | Non-commercial filing / commercial license / not needed · icp_filing/icp_license/none/not_required/undetermined |
| `tel.filing_status` | enum | Current filing/license status per the regulator's public records · filed/pending/cancelled/none/not_required |
| `tel.data_localization` | enum | In-country data storage obligation status · compliant/deviation/not_applicable |
| `tel.content_compliance` | enum | Content compliance & rectification status · compliant/rectification_required/violation/unknown |

## Red lines (machine-readable, non-negotiable)

1. Never output a "go-live / may operate" clearance — the telecom regulator's license is the sole basis.
2. Without the corresponding license, never state that value-added telecom business may be conducted.
3. Never suggest circumventing licensing via overseas deployment, domain hopping, or borrowing another party's credentials.

Each red line has a matching blocking rule in `gate-map.json`; the platform validator fails if coverage is missing.

## Quick Start / 快速开始

This repo is a declarative skeleton — no runtime, no install.

```bash
git clone https://github.com/SynomosAI/tel-icp-license-checker.git
cd tel-icp-license-checker
python -m json.tool domain.manifest.json    # validate the manifest
cat checker.io.json                         # read the MCP tool contract
```

The checker MCP tool returns only four states — `shown / missing / expired / unverifiable` — and is forbidden from outputting "pass/fail / compliant" conclusions (see `_forbidden_outputs` in `checker.io.json`).

## Repository layout

```text
domain.manifest.json   # declaration: attributes / issuer requirements / red lines / validity
gate-map.json          # friction levels per action class (gate/1.0)
privacy.json           # privacy notice (privacy/1.0) — an admission condition
checker.io.json        # MCP checker I/O contract (show & verify, never judge)
LICENSE                # code & config: MIT
LICENSE-CONTENT        # prose content: All Rights Reserved (citable with attribution)
```

## References

- Regulations of the People's Republic of China on Telecom (电信条例)
- Measures for the Administration of Internet Information Services (互联网信息服务管理办法)
- Catalog of Telecom Services (电信业务分类目录)
- Measures for the Administration of Telecom Business Licenses (电信业务经营许可管理办法)
- Administrative Measures on Filing of Non-Commercial Internet Information Services (非经营性互联网信息服务备案管理办法)

The above references only explain the origin of the domain's attributes; they are not legal advice.

## Claiming this domain

The domain is open to qualified institutions. To claim:

1. Fork this repo and fill in `operator` and `checker_endpoint`.
2. Calibrate attribute values and red lines per current rules.
3. Run the platform validator self-test (all five criteria must pass).
4. Open a PR with credential proof and rule citations.

## License

Code and configuration are MIT-licensed. Prose content is copyrighted by SynomosAI.

© 2026 SynomosAI. All rights reserved.

Full terms: [LICENSE](LICENSE) (MIT) · [LICENSE-CONTENT](LICENSE-CONTENT) (ARR). Report security issues privately via [SECURITY.md](SECURITY.md).
