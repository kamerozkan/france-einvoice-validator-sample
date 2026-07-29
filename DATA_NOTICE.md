# Data Notice

## Purpose

This repository is a technical sample for the [France E-Invoice Validator API](https://apify.com/kamerozkan/france-einvoice-validator). It contains three real dataset rows and the corresponding standalone JSON Schema.

The Actor and this repository are independent, unofficial products. They are not affiliated with, sponsored by, or endorsed by FNFE-MPE, the French tax administration, an approved platform, any invoice recipient, or any upstream validation project.

## Provenance snapshot

The three JSON records were retrieved on 2026-07-29 from successful Apify run `gihL6N622hQRnwK7K`, build `0.0.4` (`vv4freSAs5T2ErfTr`), dataset `akTMJBhWLCtUX8eci`.

- `01_live_accepted_output.json` is an `ACCEPTED` result for the pinned official France_RFE EN 16931 UBL fixture.
- `02_live_rejected_output.json` is a `REJECTED` result produced by emptying the invoice ID in that pinned fixture.
- `03_live_not_evaluated_output.json` is a `NOT_EVALUATED` source-safety result caused by a non-HTTPS URL.

The JSON files are verbatim dataset records. No field was reconstructed, inferred, or edited.

A separate final-build release run `G5dhKHsKMUaXZdaZK`, build `0.0.4` (`vv4freSAs5T2ErfTr`), dataset `HvCe9Vik8A2YXPCYi`, returned `ACCEPTED` for the official Factur-X Extended PDF with `pdfaStatus: COMPLIANT` and `metadataStatus: CONSISTENT`. That additional evidence row is referenced in the README but is not copied into this repository.

## Privacy and security

This repository contains no customer invoice, raw XML, PDF, base64 document, access token, cookie, signed URL, webhook URL, email address, bank detail, tax identifier, or customer account identifier.

The accepted fixture is public test data. The rejected document is a deterministic mutation of that fixture, and the source-error entry is synthetic. The output rows expose technical metadata and findings, not invoice parties, line items, payment details, or full invoice bodies.

Customer validation findings and optional reports can contain invoice values. Users remain responsible for lawful processing, access control, retention, deletion, and applicable privacy, tax, accounting, database, and contractual requirements.

## Interpretation limits

- `ACCEPTED` means the submitted bytes passed the pinned offline technical checks.
- `REJECTED` means the document was evaluated and at least one required technical rule failed.
- `NOT_EVALUATED` means a processing or safety failure prevented a technical decision.
- A result does not prove legal or tax validity, issuer identity, authenticity, delivery, payment, approved-platform acceptance, or recipient acceptance.
- A future ruleset update can change findings for the same source bytes.

## License boundary

The MIT License applies only to the original documentation, JSON output samples, and JSON Schema committed here.

It does not relicense France_RFE, EN 16931, UBL, CII, Factur-X, veraPDF, Mustangproject, public fixtures, specifications, third-party software, names, marks, or report formats. Review upstream licenses and terms before redistribution or commercial use.
