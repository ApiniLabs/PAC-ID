# Well-known `id segment key`s

We recommend using GS1 AI’s as keys of ID segments. Those however have a eCommerce focus. Correspondingly, especially for data related id segments it is often unclear what an adequate key choice would be. There is value in having clarity about that aspect because this will lead to more uniform, vendor-indepent interpretable ID segments, which in turn greatly simplify routing via Resolver.

There are three basic approaches:
1. Specify which of the preexisting GS1 AI’s should be used
2. Find other ontologies that could be used in addition to GS1 that cover the data side.
3. Specify the few ones that we need in addition to the GS1 AI’s ourselves

| **~id segment key~** | **Name** | **Ontology Origin** | **Comment** |
| :--- | :--- | :--- | :--- |
| `01` | Global Trade Item Number (GTIN) | GS1 |  |
| `240` | Additional product identification assigned by the manufacturer | GS1 | For all articles without GTIN, otherwise use `id segment key` `01` instead. |
| `21` | Serial number | GS1 |  |
| `10` | Batch or lot number | GS1 |  |
| `RNA` |  | PAC-ID-COMMONS |  |
| `RNR` |  | PAC-ID-COMMONS |  |
| `RNC` |  | PAC-ID-COMMONS |  |
| `SPL` |  | PAC-ID-COMMONS |  |
| `APP` |  | PAC-ID-COMMONS |  |
| `MTH` |  | PAC-ID-COMMONS |  |
| `RPT` |  | PAC-ID-COMMONS |  |
| `V` |  |  PAC-ID-COMMONS |  |
| `SOP` |  | PAC-ID-COMMONS |  |
