# Well-known `id segment key`s

It is RECOMMENDED to use well-known `id segment key`s.

The following approach SHALL be used to define an `id segment key`:

1. Use a preexisting [GS1 Application Identifier](https://ref.gs1.org/ai/). Some commonly used GS1 AIs are referenced in the table below.
2. Use a predefined key from the table below (with origin `PAC-ID-COMMONS`).
3. Use a self-defined key. It is RECOMMENDED to base such a key on a well-known existing ontology. New keys MAY be added to the table below through a pull request.

| **Key (`id segment key`)** | **Ontology Origin** | **Meaning / Comment** |
| :--- | :--- | :--- |
| `01` | GS1 AI[^1] | Global Trade Item Number (GTIN) |
| `10` | GS1 AI[^1] | Batch or lot number |
| `21` | GS1 AI[^1] | Serial number |
| `240` | GS1 AI[^1] | Additional product identification assigned by the manufacturer. For all articles without GTIN; otherwise use `id segment key` `01` instead. |
| `RNA` | PAC-ID-COMMONS | An absolute run id (i.e. unique in itself without further information) |
| `RNR` | PAC-ID-COMMONS | A relative run id (i.e. only unique together with other information, e.g. a device identifier) |
| `SMP` | PAC-ID-COMMONS | A sample id |
| `EXP` | PAC-ID-COMMONS | An experiment id |
| `RST` | PAC-ID-COMMONS | A result id (i.e. an id pointing to result data) |
| `MTD` | PAC-ID-COMMONS | A method id; e.g. a reference to an SOP (standard operating procedure) |
| `RPT` | PAC-ID-COMMONS | A report id; e.g. a reference to a result report |
| `TS` | PAC-ID-COMMONS | A timestamp. It is RECOMMENDED to use YYYYMMDDTHHMM, YYYYMMDDTHHMMSS or YYYYMMDDTHHMMSS in ISO8601 Basic Format|
| `V` |  PAC-ID-COMMONS | A version or revision number. It is RECOMMENDED to use version numbers that follows the [semantic versioning](https://semver.org/) guidelines. |

[^1]: [GS1](https://www.gs1.org/) (Global Standards 1) is a not-for-profit organisation that works closely with industries to agree how information should be stored in a barcode. This ensures organisations around the world can extract meaningful information about a product when its barcode is scanned. The organization, however, has an eCommerce focus. Especially for data-related id segments, it is often unclear what an adequate key choice would be. There is value in having clarity about that aspect because this will lead to more uniform, vendor-indepent interpretable `id segment key`s, which in turn greatly simplify routing via a `PAC-ID Resolver`.
