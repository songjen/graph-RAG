# FDA DMF Knowledge Graph — 3Q2026

Interactive knowledge graph built from the FDA "List of Drug Master Files (DMFs)" — 3rd Quarter 2026.

## Model

| Element | Graph entity | Source field |
|---|---|---|
| Entity node (blue) | Holder (DMF holder / manufacturer proxy) | `HOLDER` |
| Subject node (orange) | Product (DMF subject) | `SUBJECT` |
| Edge | DMF filing | `DMF#`, `TYPE`, `STATUS`, `SUBMIT DATE` |

**Caveat:** the source table has no standalone `Manufacturer` column. In the FDA DMF system the `HOLDER` is the filing entity (usually the API manufacturer or service provider), so it is used as the entity node. `SUBJECT` is the filed product, used as the product node.

## Scale

- 41,672 valid DMF records (out of ~1.05M rows scanned in the source sheet)
- 9,142 holders, 28,007 products, 41,098 holder→product filing relations
- TYPE: II 29,486 / III 7,415 / IV 3,684 / V 588 / I 499
- STATUS: Active 22,721 / Inactive 18,951
- Submission years: 1939–2026

## Files

- `index.html` — self-contained interactive graph (D3 v7 force layout, data embedded). Open directly in a browser. Supports multi-select search (e.g. select all products matching `amoxicillin`), TYPE/STATUS/year filters, joint-neighbourhood focus, node drill-down, and subgraph JSON export.
- `dmf_graph_data.json` — full graph data (`meta` + `nodes` + `links`), each link carrying DMF numbers, types, statuses and years.
- `dmf_graph_compact.json` — index-compacted form of the same graph for secondary development.

## Features

- Multi-select search: click search results to accumulate selections; "全选当前结果" selects all keyword matches; selected entities are shown as removable chips.
- Focus view takes the union of all selected nodes' filing neighbourhoods; detail panel lists each selected entity's top relations with DMF numbers.
- Top-N holder core-network view, multi-source product filter, and export of the current subgraph.
