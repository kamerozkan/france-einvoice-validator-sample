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

All three records below are verbatim rows from successful run `gihL6N622hQRnwK7K`, build `0.0.4` (`vv4freSAs5T2ErfTr`), dataset `akTMJBhWLCtUX8eci`.

<details>
<summary><strong>01. ACCEPTED</strong> - official France_RFE EN 16931 UBL fixture</summary>

[`01_live_accepted_output.json`](01_live_accepted_output.json)

```json
{
  "inputIndex": 0,
  "documentId": "official-en16931-ubl",
  "fileName": "official-en16931-ubl.xml",
  "processingStatus": "SUCCEEDED",
  "conformanceStatus": "ACCEPTED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "externalStateStatus": "NOT_EVALUATED_EXTERNAL_STATE",
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
    "artifactManifestSha256": "f9c1a666a033768c487d9905cbfe59afcb7648eabad5f95acc0292219bb1a32c"
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
  "sha256": "f4ff1b06f056255061a5acffbb86b8e793720b031d0d289adb7a6e53de9d9c25",
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T11:53:35.576026Z",
  "reports": {},
  "error": null
}
```

</details>

<details>
<summary><strong>02. REJECTED</strong> - official fixture mutated with an empty invoice ID</summary>

[`02_live_rejected_output.json`](02_live_rejected_output.json)

```json
{
  "inputIndex": 1,
  "documentId": "mutated-missing-invoice-id",
  "fileName": "mutated-missing-invoice-id.xml",
  "processingStatus": "SUCCEEDED",
  "conformanceStatus": "REJECTED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "externalStateStatus": "NOT_EVALUATED_EXTERNAL_STATE",
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
    "artifactManifestSha256": "f9c1a666a033768c487d9905cbfe59afcb7648eabad5f95acc0292219bb1a32c"
  },
  "counts": {
    "fatal": 3,
    "error": 0,
    "warning": 2,
    "information": 0
  },
  "findings": [
    {
      "severity": "FATAL",
      "stage": "EN16931",
      "ruleId": "BR-02",
      "message": "[BR-02]-An Invoice shall have an Invoice number (BT-1).",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]",
      "test": "normalize-space(cbc:ID) != ''",
      "ruleset": "EN16931-1.3.16-UBL"
    },
    {
      "severity": "FATAL",
      "stage": "FRANCE_CIUS",
      "ruleId": "BR-FR-01_BT-1-2",
      "message": "[BR-FR-01/BT-1] : L'identifiant de facture (cbc:ID) contient des caractères non autorisés. Valeur actuelle : \"\". Seuls les caractères alphanumériques et les symboles + - _ / sont autorisés, sans espaces.",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]/*:ID[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2'][1]",
      "test": "custom:is-valid-id-format(.)",
      "ruleset": "FRANCE-RFE-1.4.0.02-UBL"
    },
    {
      "severity": "FATAL",
      "stage": "FRANCE_CIUS",
      "ruleId": "BR-FR-02_BT-1",
      "message": "[BR-FR-02/BT-1 : L'identifiant de facture (cbc:ID) doit être composé uniquement de caractères alphanumériques (A-Z, a-z, 0-9) et peut contenir les caractères spéciaux autorisés : tiret (-), plus (+), tiret bas (_), barre oblique (/). Il ne doit pas contenir uniquement des espaces, ni commencer ou se terminer par un espace, ni contenir d'espaces consécutifs. Valeur actuelle : \"\". Veuillez corriger le format de l'identifiant.",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]/*:ID[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2'][1]",
      "test": "custom:is-valid-id-format(.)",
      "ruleset": "FRANCE-RFE-1.4.0.02-UBL"
    },
    {
      "severity": "WARNING",
      "stage": "FRANCE_CIUS",
      "ruleId": "BR-FR-01_BT-1-2",
      "message": "[BR-FR-01/BT-1] : L'identifiant de facture (cbc:ID) contient des caractères non autorisés. Valeur actuelle : \"\". Seuls les caractères alphanumériques et les symboles + - _ / sont autorisés, sans espaces.",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]/*:ID[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2'][1]",
      "test": "custom:is-valid-id-format(.)",
      "ruleset": "FRANCE-RFE-1.4.0.02-UBL-WARNINGS"
    },
    {
      "severity": "WARNING",
      "stage": "FRANCE_CIUS",
      "ruleId": "BR-FR-02_BT-1",
      "message": "[BR-FR-02/BT-1 : L'identifiant de facture (cbc:ID) doit être composé uniquement de caractères alphanumériques (A-Z, a-z, 0-9) et peut contenir les caractères spéciaux autorisés : tiret (-), plus (+), tiret bas (_), barre oblique (/). Il ne doit pas contenir uniquement des espaces, ni commencer ou se terminer par un espace, ni contenir d'espaces consécutifs. Valeur actuelle : \"\". Veuillez corriger le format de l'identifiant.",
      "location": "/*:Invoice[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:Invoice-2'][1]/*:ID[namespace-uri()='urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2'][1]",
      "test": "custom:is-valid-id-format(.)",
      "ruleset": "FRANCE-RFE-1.4.0.02-UBL-WARNINGS"
    }
  ],
  "findingsTruncated": false,
  "previewCounts": {
    "fatal": 0,
    "error": 0,
    "warning": 0,
    "information": 0
  },
  "previewFindings": [],
  "previewFindingsTruncated": false,
  "sha256": "72626abb163a2f3092f5adeabae4d3ff39a45ae03856f3e5b4dd0efa3bdac358",
  "embeddedXmlSha256": null,
  "container": null,
  "checkedAt": "2026-07-29T11:53:41.008116Z",
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
  "documentId": "source-error",
  "fileName": "blocked.xml",
  "processingStatus": "FAILED",
  "conformanceStatus": "NOT_EVALUATED",
  "previewConformanceStatus": "NOT_EVALUATED",
  "validationScope": "OFFLINE_PREFLIGHT",
  "externalStateStatus": "NOT_EVALUATED_EXTERNAL_STATE",
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
    "artifactManifestSha256": "f9c1a666a033768c487d9905cbfe59afcb7648eabad5f95acc0292219bb1a32c"
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
  "checkedAt": "2026-07-29T11:53:41.080721Z",
  "reports": {},
  "error": {
    "code": "SOURCE_FETCH_FAILED",
    "message": "Only HTTPS source URLs are allowed"
  }
}
```

</details>

## Final-build release evidence

A separate build-matched smoke run `G5dhKHsKMUaXZdaZK`, build `0.0.4` (`vv4freSAs5T2ErfTr`), dataset `HvCe9Vik8A2YXPCYi`, validated the official Factur-X Extended PDF:

- `conformanceStatus: ACCEPTED`
- `sourceFormat: FACTUR_X_PDF`
- `profile: FRANCE_FACTUR_X_EXTENDED`
- `pdfaStatus: COMPLIANT`
- `metadataStatus: CONSISTENT`
- embedded `factur-x.xml` SHA-256: `c1c8eb44f72fa168f347cf72c843c2c9c5bb625b5019b60b20403d39f47c9157`

The same row reports `visibleContentConsistency: NOT_VERIFIED` and `signatureStatus: NOT_CHECKED`; it does not extend the Actor's technical-preflight claim. This additional evidence row is not one of the three JSON sample files above.

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
externalStateStatus -> NOT_EVALUATED_EXTERNAL_STATE
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
