# Well-known `id segment key`s

It is RECOMMENDED to use well-known `id segment key`s. The following approach SHALL be used to define an `id segment key`:

1. Use a preexisting [GS1 Application Identifier](https://ref.gs1.org/ai/). Some commonly used GS1 AIs are referenced in the table below.
2. Use a predefined key as defined in the table below with origin `PAC-ID-COMMONS`.
3. Use a self-defined key. It is RECOMMENDED to base such a key on a well-known existing ontology.

| **Key (`id segment key`)** | **Ontology Origin** | **Meaning / Comment** |
| :--- | :--- | :--- |
| `01` | GS1 AI[^1] | Global Trade Item Number (GTIN) |
| `10` | GS1 AI[^1] | Batch or lot number |
| `21` | GS1 AI[^1] | Serial number |
| `240` | GS1 AI[^1] | Additional product identification assigned by the manufacturer. For all articles without GTIN; otherwise use `id segment key` `01` instead. |
| `RNA` | PAC-ID-COMMONS | An absolute run id (i.e. unique in itself) |
| `RNR` | PAC-ID-COMMONS | A relative run id; relative to a previous run (i.e. only unique together with previous run ids) |
| `RNC` | PAC-ID-COMMONS | A run collection id |
| `SPL` | PAC-ID-COMMONS | A sample record |
| `APP` | PAC-ID-COMMONS | An application id |
| `MTH` | PAC-ID-COMMONS | A method id; CAN be a reference to an SOP (standard oparating procedure) |
| `RPT` | PAC-ID-COMMONS | A report id |
| `V` |  PAC-ID-COMMONS | A version or revision |
| `SOP` | PAC-ID-COMMONS | A reference to a SOP (standard oparating procedure); often a sysnonym to `MTH` |

[^1]: [GS1](https://www.gs1.org/) (Global Standards 1) is a not-for-profit organisation that works closely with industries to agree how information should be stored in a barcode. This ensures organisations around the world can extract meaningful information about a product when its barcode is scanned. The organization, however, has an eCommerce focus. Correspondingly, especially for data related id segments it is often unclear what an adequate key choice would be. There is value in having clarity about that aspect because this will lead to more uniform, vendor-indepent interpretable `id segment key`s, which in turn greatly simplify routing via a `PAC-ID Resolver`.
