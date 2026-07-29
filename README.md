> **Live API:** [Run France E-Invoice Validator on Apify](https://apify.com/kamerozkan/france-einvoice-validator)

# France E-Invoice Validator API: Samples and JSON Schema

[![Apify Actor](https://img.shields.io/badge/Apify-Run%20Actor-00c7b7?logo=apify)](https://apify.com/kamerozkan/france-einvoice-validator)
![Validation](https://img.shields.io/badge/scope-OFFLINE__PREFLIGHT-0055a4)
![Rules](https://img.shields.io/badge/France__RFE-1.4.0.02-0055a4)
![Samples](https://img.shields.io/badge/live%20samples-3-2f855a)
![JSON Schema](https://img.shields.io/badge/schema-2020--12-4c1)
![License](https://img.shields.io/badge/license-MIT-blue)

Validate French UBL 2.1, CII D22B, and Factur-X invoices before transmission. Each evaluated document returns a deterministic technical result, structured findings, SHA-256 evidence, and the exact pinned rule versions.

This repository contains three real output rows from one successful Actor run and the machine-readable contract in [`dataset_record.schema.json`](dataset_record.schema.json).

> **Decision boundary:** `ACCEPTED` means the submitted document passed the pinned offline technical checks. It is not legal, tax, accounting, authenticity, delivery, approved-platform, or recipient acceptance evidence.

## Why this pipeline

| Need | Generic XML parser | This validator |
|---|---|---|
| UBL and CII structure | XML syntax only | Pinned XSD validation |
| French reform rules | Usually absent | France_RFE `1.4.0.02` and EN 16931 |
| Factur-X PDF | Usually ignored | PDF/A-3 and embedded XML route |
| Audit evidence | Ad hoc text | Rule IDs, locations, hashes, versions |
| Batch failures | One error can stop a batch | One independent result per document |
| Unsafe or unsupported source | Ambiguous error | Explicit `NOT_EVALUATED` result |

## Result contract

| Processing | Conformance | Meaning | `invoice-validated` billing |
|---|---|---|---|
| `SUCCEEDED` | `ACCEPTED` | Every required pinned technical layer passed | Charged |
| `SUCCEEDED` | `REJECTED` | At least one required technical rule failed | Charged |
| `FAILED` | `NOT_EVALUATED` | No technical decision was possible | Not charged |

The Actor charges `$0.004` per evaluated document. A platform Actor-start event can also apply. Check the current Store page before production use.

## Real output examples

All three records below are verbatim rows from successful run `zRojE158Pc2yIwNba`, dataset `N3fw2lYnnT7Jmeica`.

<details>
<summary><strong>01. ACCEPTED</strong> - public EN 16931 UBL fixture</summary>

[`01_live_accepted_output.json`](01_live_accepted_output.json)

```json
{
  "inputIndex": 0,
  "documentId": "accepted-official-sample",
  "fileName": "ubl-21-en16931.xml",
  "processingStatus": "SUCCEEDED",
  "conformanceStatus": "ACCEPTED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "rulesetEffectiveAt": "2026-09-01",
  "sourceFormat": "XML",
  "validationFamily": "FRANCE_RFE",
  "syntax": "UBL_INVOICE",
  "profile": "FRANCE_EN16931_UBL",
  "scenario": "France RFE EN 16931 UBL 2.1 Invoice",
  "versions": {
    "franceRfe": "1.4.0.02",
    "franceRfeCommit": "e9520ce398cc99bed4bab493773a494af8ca5aff",
    "franceRfeArchiveSha256": "5d30054c99d970457ca50c89ce895770cae695f5fe8d73750433079f9f1ec3a1",
    "xpZ12_012": "1.4",
    "ubl": "2.1",
    "cii": "D22B",
    "en16931Schematron": "1.3.16",
    "facturX": "1.09",
    "facturXExtendedSchemaPatch": "1.09.2",
    "mustang": "2.24.0",
    "saxonHe": "12.8",
    "veraPdf": "1.30.2",
    "activeRuleset": {
      "name": "France_RFE 1.4.0.02",
      "effectiveAt": "2026-09-01"
    },
    "artifactManifestSha256": "155a73f1d0a8a6abb2f2e209860b972db58dd81521a28ef3f87f5ca094ac04d6"
  },
  "counts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "findings": [],
  "findingsTruncated": false,
  "previewCounts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "previewFindings": [],
  "previewFindingsTruncated": false,
  "sha256": "90c598998073f00952bbcdb75ab9dbce02c2caeed26e88d3094eabeda982435a",
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T10:39:21.887450Z",
  "reports": {},
  "error": null
}
```

</details>

<details>
<summary><strong>02. REJECTED</strong> - incomplete UBL with bounded technical findings</summary>

[`02_live_rejected_output.json`](02_live_rejected_output.json)

```json
{
  "inputIndex": 1,
  "documentId": "rejected-incomplete-ubl",
  "fileName": "incomplete-ubl.xml",
  "processingStatus": "SUCCEEDED",
  "conformanceStatus": "REJECTED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "rulesetEffectiveAt": "2026-09-01",
  "sourceFormat": "XML",
  "validationFamily": "FRANCE_RFE",
  "syntax": "UBL_INVOICE",
  "profile": "FRANCE_EN16931_UBL",
  "scenario": "France RFE EN 16931 UBL 2.1 Invoice",
  "versions": {
    "franceRfe": "1.4.0.02",
    "franceRfeCommit": "e9520ce398cc99bed4bab493773a494af8ca5aff",
    "franceRfeArchiveSha256": "5d30054c99d970457ca50c89ce895770cae695f5fe8d73750433079f9f1ec3a1",
    "xpZ12_012": "1.4",
    "ubl": "2.1",
    "cii": "D22B",
    "en16931Schematron": "1.3.16",
    "facturX": "1.09",
    "facturXExtendedSchemaPatch": "1.09.2",
    "mustang": "2.24.0",
    "saxonHe": "12.8",
    "veraPdf": "1.30.2",
    "activeRuleset": {
      "name": "France_RFE 1.4.0.02",
      "effectiveAt": "2026-09-01"
    },
    "artifactManifestSha256": "155a73f1d0a8a6abb2f2e209860b972db58dd81521a28ef3f87f5ca094ac04d6"
  },
  "counts": {
    "fatal": 16,
    "error": 2,
    "warning": 6,
    "information": 0
  },
  "findings": [
    {
      "severity": "ERROR",
      "stage": "XSD",
      "ruleId": "SCHEMAV_ELEMENT_CONTENT",
      "message": "Element '{urn:oasis:names:specification:ubl:schema:xsd:Invoice-2}Invoice': Missing child element(s). Expected is one of ( {urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2}CopyIndicator, {urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2}UUID, {urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2}IssueDate ).",
      "location": "/*",
      "ruleset": "UBL-2.1-INVOICE-XSD",
      "line": 1,
      "column": 0
    },
    {
      "severity": "FATAL",
      "stage": "EN16931",
      "ruleId": "BR-01",
      "message": "[BR-01]-An Invoice shall have a Specification identifier (BT-24).",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]",
      "test": "normalize-space(cbc:CustomizationID) != ''",
      "ruleset": "EN16931-1.3.16-UBL"
    },
    {
      "severity": "FATAL",
      "stage": "EN16931",
      "ruleId": "BR-03",
      "message": "[BR-03]-An Invoice shall have an Invoice issue date (BT-2).",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]",
      "test": "normalize-space(cbc:IssueDate) != ''",
      "ruleset": "EN16931-1.3.16-UBL"
    },
    {
      "severity": "FATAL",
      "stage": "EN16931",
      "ruleId": "BR-04",
      "message": "[BR-04]-An Invoice shall have an Invoice type code (BT-3).",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]",
      "test": "normalize-space(cbc:InvoiceTypeCode) != '' or normalize-space(cbc:CreditNoteTypeCode) !=''",
      "ruleset": "EN16931-1.3.16-UBL"
    },
    {
      "severity": "FATAL",
      "stage": "EN16931",
      "ruleId": "BR-05",
      "message": "[BR-05]-An Invoice shall have an Invoice currency code (BT-5).",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]",
      "test": "normalize-space(cbc:DocumentCurrencyCode) != ''",
      "ruleset": "EN16931-1.3.16-UBL"
    }
  ],
  "findingsTruncated": true,
  "previewCounts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "previewFindings": [],
  "previewFindingsTruncated": false,
  "sha256": "c93ffbc01ae38cdb76d5e2176ea2ddf20e0ea0d9a7cf4c04ab884e330a24d8b9",
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T10:39:25.883652Z",
  "reports": {},
  "error": null
}
```

</details>

<details>
<summary><strong>03. NOT_EVALUATED</strong> - unsafe source rejected before validation</summary>

[`03_live_not_evaluated_output.json`](03_live_not_evaluated_output.json)

```json
{
  "inputIndex": 2,
  "documentId": "not-evaluated-http-source",
  "fileName": "invoice.xml",
  "processingStatus": "FAILED",
  "conformanceStatus": "NOT_EVALUATED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "rulesetEffectiveAt": "2026-09-01",
  "sourceFormat": "UNKNOWN",
  "validationFamily": "UNKNOWN",
  "syntax": "UNKNOWN",
  "profile": "UNKNOWN",
  "scenario": null,
  "versions": {
    "franceRfe": "1.4.0.02",
    "franceRfeCommit": "e9520ce398cc99bed4bab493773a494af8ca5aff",
    "franceRfeArchiveSha256": "5d30054c99d970457ca50c89ce895770cae695f5fe8d73750433079f9f1ec3a1",
    "xpZ12_012": "1.4",
    "ubl": "2.1",
    "cii": "D22B",
    "en16931Schematron": "1.3.16",
    "facturX": "1.09",
    "facturXExtendedSchemaPatch": "1.09.2",
    "mustang": "2.24.0",
    "saxonHe": "12.8",
    "veraPdf": "1.30.2",
    "activeRuleset": {
      "name": "France_RFE 1.4.0.02",
      "effectiveAt": "2026-09-01"
    },
    "artifactManifestSha256": "155a73f1d0a8a6abb2f2e209860b972db58dd81521a28ef3f87f5ca094ac04d6"
  },
  "counts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "findings": [],
  "findingsTruncated": false,
  "previewCounts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "previewFindings": [],
  "previewFindingsTruncated": false,
  "sha256": null,
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T10:39:25.969300Z",
  "reports": {},
  "error": {
    "code": "SOURCE_FETCH_FAILED",
    "message": "Only HTTPS source URLs are allowed"
  }
}
```

</details>

## Supported routes

- UBL 2.1 Invoice and CreditNote with EN 16931 or EXTENDED-CTC-FR profiles
- UN/CEFACT CII D22B with EN 16931 or EXTENDED-CTC-FR profiles
- Factur-X 1.09 XML
- Factur-X PDF/A-3 with safe embedded XML extraction

Input can be supplied through HTTPS URL, inline XML, base64, console upload, or an Apify key-value store record. HTTPS source controls block private, local, reserved, and cloud metadata targets.

## Machine-readable schema

Use [`dataset_record.schema.json`](dataset_record.schema.json) to validate stored rows before loading them into an ERP, webhook, Make, n8n, or another data pipeline.

```text
processingStatus -> SUCCEEDED | FAILED
conformanceStatus -> ACCEPTED | REJECTED | NOT_EVALUATED
validationScope -> OFFLINE_PREFLIGHT
findings[] -> severity, stage, ruleId, message, location
versions{} -> pinned rule and artifact identities
```

See [`DATA_NOTICE.md`](DATA_NOTICE.md) for run provenance, privacy boundaries, and interpretation limits.

## Use the live API

- [Run the Actor on Apify](https://apify.com/kamerozkan/france-einvoice-validator)
- Price: `$0.004` per evaluated invoice
- `NOT_EVALUATED` documents do not emit the `invoice-validated` event

## License

The repository's original documentation, JSON samples, and schema are MIT licensed. Upstream rules, specifications, fixtures, software, names, and marks retain their own licenses and terms.
