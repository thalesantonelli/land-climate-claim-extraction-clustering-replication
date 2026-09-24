# Land and Climate Claim Extraction and Clustering: Replication Data

## Overview

This dataset accompanies Thales Antonelli's research on land, territorial, climate and environmental discourse in the Brazilian Chamber of Deputies. The dissertation and article provide the methodological and substantive reference. The files support inspection of parliamentary speeches, extracted claims, sample selection and the researcher-developed Macro/Meso/Micro taxonomy.

The article reports **26,644 speeches, 41,039 extracted claims, 21,244 land-relevant claims, 5,246 contestatory claims, 797 final analytical claims, and a taxonomy of 5 Macro, 15 Meso and 15 Micro categories**. These are reported results, not a claim that every number is independently reproduced by the supplied files. The evidence below distinguishes exact reproduction from unresolved differences. Neither the dissertation nor the article has been edited as part of this file update.

## Files

| File | Contents |
| --- | --- |
| parliamentary_speeches.csv, inside the supplied parliamentary_speeches (1).zip | Parliamentary corpus and source metadata. The download suffix (1) has no analytical meaning. |
| extracted_claims.csv | Extracted claims, original component classifications, stored Macro/Meso/Micro labels and the confirmed considered selection. |
| taxonomy.csv | Hierarchy of named categories, supplemented with the two documented paths under Meso 5.5. |
| README.md | Consolidated documentation and evidence connecting files to reported results. |
| DATA_DICTIONARY.md | Standalone copy of the dictionary below. |

The source workbook, `2025.12.24 - Corpus Final - Proferimentos sobre Terra e Clima.xlsx`, is the provenance reference for the CSV export. It is not a second set of independent observations.

## Evidence connecting the files to the text

Dissertation page numbers below refer to the printed page numbers (PDF page = printed page + 1).

| Result in the text | Evidence or operation in the supplied files | Finding |
| --- | --- | --- |
| 26,644 speeches (dissertation pp. 92 and 109; article §3) | Count data records in parliamentary_speeches.csv. | Reproduced: 26,644. |
| 41,039 claims (dissertation p. 109; article §§3–3.1) | Count valid claim_id values in extracted_claims.csv and compare the workbook's claims sheet. | 41,038 identified claims. The source sheet has one additional row (Excel row 799) containing counting formulas in K/L and no claim identifier or text. Dissertation p. 102 also reports 41,038. The missing unit is not an identified claim that can be restored from these sources. |
| 21,244 land-relevant claims (dissertation p. 109; article §§3–3.2) | Count land_relevance = Sim. | Reproduced: 21,244. |
| 5,246 contestatory claims within the preceding stage (same passages) | Count land_relevance = Sim AND delegitimization = Sim. | Reproduced: 5,246. |
| 797 final claims (dissertation p. 109; article §§3–3.3) | Count considered = Sim; compare claim IDs to records with nonempty Macro in the source workbook. | Reproduced as a selected set: 797. Selection was confirmed by the author. The three stored component columns together return 706, so the final filtering operation is not independently reproduced by those columns. |
| All three substantive inclusion criteria positive (dissertation p. 104; article §3.2) | Compare the component columns with considered. | The intended definition is preserved. Source columns have missing values and do not reproduce the confirmed membership; no missing classification has been filled from membership. |
| 5 Macro, 15 Meso, 15 Micro (article §§3 and 5; dissertation narrative) | Count distinct named categories by level; inspect dissertation Figure 2 (p. 110) and category tables. | The updated taxonomy documents 5 Macro, 15 Meso and 14 Micro. The supplied taxonomy previously omitted Meso 5.5 and its two Micro children. A fifteenth named Micro category has not been located. |

This distinction keeps the text as the reference while making the evidential reach of the files explicit. Reported counts have not been made true by generating observations or classifications.

## Scope of this update

Only taxonomy.csv, README.md and DATA_DICTIONARY.md are replaced by this update. The current extracted_claims.csv, the speech ZIP and the source XLSX are retained unchanged. No original claim labels are removed or reassigned, and no original_* or final_* columns are introduced.

Two paths were appended to taxonomy.csv: 5 → 5.5 → 5.5.1 and 5 → 5.5 → 5.5.2. The existing 21 paths retain their values. Their wording is sometimes different from the shorter labels in the dissertation, so the numbered code is the appropriate link for already numbered assignments.

The final taxonomy is an analytical vocabulary, not proof of a complete claim-by-claim final coding table. In the supplied claims file, 142 of the 797 selected claims have numbered Macro categories; the other 655 have unnumbered labels. The present update preserves both and does not infer a historical mapping between them.

## Data dictionary


### `parliamentary_speeches.csv`

| Variable | Description |
| --- | --- |
| `speech_id` | Identifier of the parliamentary speech; used to link extracted claims to their source speech. |
| `date` | Date of the speech. |
| `session` | Parliamentary session identifier. |
| `session_stage` | Stage or phase of the parliamentary session. |
| `speaker` | Name of the parliamentarian who delivered the speech. |
| `party` | Political party affiliation recorded for the speaker. |
| `state` | Brazilian state represented by the speaker. |
| `time` | Recorded time associated with the speech. |
| `publication` | Publication information associated with the parliamentary record. |
| `speech_url` | URL of the original parliamentary record. |
| `full_speech` | Full text of the parliamentary speech. |
| `summary` | Summary information associated with the parliamentary record. |
| `keyword` | Keyword associated with corpus retrieval. |
| `land_relevance` | Classification of the speech's relevance to land and territorial issues. |
| `delegitimization` | Classification of contestatory or delegitimizing discourse concerning land struggles, territorial rights, or associated collective actors. |
| `environmental_repertoire` | Classification of the mobilization of environmental or climate-related discourse, including references to nature or sustainability. |

### `extracted_claims.csv`

| Variable | Description |
| --- | --- |
| `speech_id` | Identifier linking the claim to its source record in `parliamentary_speeches.csv`. |
| `date` | Date of the source speech. |
| `claim_id` | Identifier of the extracted argumentative claim. All 41,038 identifiers are nonempty and unique. |
| `claim` | Argumentative claim extracted from the source parliamentary speech. |
| `canonical_claim` | Weakly normalized semantic representation of the claim used in subsequent analytical processing. This is a processed representation, not necessarily a verbatim quotation. |
| `land_relevance` | Classification of whether the claim is pertinent to land and territorial issues. |
| `delegitimization` | Classification of whether the claim is presented in a contestatory or delegitimizing manner. |
| `environmental_repertoire` | Classification of whether the claim mobilizes, in some way, environmental or climate-related discourse in making that contestation or delegitimization. |
| `macro` | Macro-level textual label. The supplied column mixes numbered final taxonomy categories with other unnumbered labels. It does not contain a uniform set of numerical cluster IDs. |
| `meso` | Meso-level textual label. The supplied column mixes numbered final taxonomy categories with other unnumbered labels. It does not contain a uniform set of numerical cluster IDs. |
| `micro` | Micro-level textual label. The supplied column mixes numbered final taxonomy categories with other unnumbered labels. It does not contain a uniform set of numerical cluster IDs. |
| `considered` | Author-confirmed inclusion in the final analytical corpus: `Sim` for 797 claims and empty for the other 40,241 claims. The substantive inclusion criterion is joint land relevance, contestation/delegitimization, and mobilization of climate/environmental discourse. This corrected field records the confirmed final selection rather than mechanically recomputing the conjunction of the three legacy classification columns. |

#### Interpretation of `considered`

The intended substantive rule requires all three conditions simultaneously: relevance to land issues, contestation or delegitimization, and mobilization of environmental/climate discourse in doing so.

The author confirmed that the 797 records with nonempty `macro` labels are the final analytical corpus. The corrected `considered` field encodes that confirmation. Filter on `considered == "Sim"` to recover these 797 claims.

The three component classification fields preserve the original stored values. Within the final corpus, 181 records have `Sim` in all three fields and 616 have an empty land-relevance or delegitimization field. Empty component fields must not be treated as verified negative judgments or overwritten from sample membership. Recomputing the conjunction from those fields yields 706 claims across the full export and does not reproduce the author-confirmed final selection.

### `taxonomy.csv`

| Variable | Description |
| --- | --- |
| `macro` | Broadest analytical category in the final researcher-developed taxonomy. |
| `meso` | Intermediate analytical category nested within the corresponding Macro category. |
| `micro` | Most specific analytical category nested within the corresponding Meso category. |

The taxonomy contains 23 rows, 5 distinct Macro categories, 15 distinct Meso categories, and 14 distinct nonempty Micro categories. Nine rows have an empty `micro` field: these rows specify no Micro category. The claims file mixes final numbered category labels and other textual labels. Do not join every label to the final taxonomy or interpret blank labels as an HDBSCAN noise code. Some labels differ in whitespace or wording.

The added paths are Meso 5.5 with Micro 5.5.1 and 5.5.2, documented in the dissertation's Figure 2 (printed p. 110), detailed Macro 5 table (p. 121), and discussion (pp. 122–123). The pre-existing 21 paths and their wording are preserved. Match numbered categories by their leading category code when wording differs; unnumbered labels cannot be assigned a final category from text matching alone.

## Semantic clustering and analytical interpretation


The final HDBSCAN settings recorded for the three levels of semantic granularity are:

| Level | `min_cluster_size` | `min_samples` | Additional recorded setting |
| --- | --- | --- | --- |
| Macro | 40 | 15 | — |
| Meso | 25 | 10 | — |
| Micro | 12 | 6 | `cluster_selection_method="leaf"` |

The dash indicates that no additional setting is specified here; it does not prescribe a software default. These are the recorded granularity settings, not a complete specification of the computational environment. Consult the replication repository for the pipeline, prompts, preprocessing, and implementation details.

The three clustering resolutions informed researcher-led interpretation and construction of the final Macro/Meso/Micro taxonomy. The nesting of the final analytical categories should not be taken as proof that independently computed cluster solutions are mechanically nested.

## Reuse and file conventions

Filter considered = Sim to retrieve the 797-claim analytical set. Link speech_id to the parliamentary corpus for source context. Keep identifiers as text. CSV files use UTF-8 with BOM, comma separators and standard CSV quoting. A blank component classification is not a verified negative judgment. A blank considered denotes exclusion from the confirmed final set.

The text and recorded files remain distinguishable: preserving the research's substantive definition of considered does not establish that incomplete stored component fields reproduce every selection decision.

## Provenance and related research


Parliamentary speech records originate from the Brazilian Chamber of Deputies Open Data portal. Claim extraction, analytical classification, semantic processing, clustering, and taxonomic organization were produced through the research workflow documented in the accompanying replication repository.

The dataset was produced as part of the author's Master's dissertation. At the time this documentation was prepared, no public persistent identifier for the dissertation had been supplied. No provisional dissertation URL or identifier is asserted here.

When citing the dataset, use the citation and DOI supplied by the published Zenodo record, including the relevant dataset version. Cite the accompanying code separately when reusing the computational pipeline.

## License

The replication dataset is released under the Creative Commons Attribution 4.0 International (CC BY 4.0) license.

The license applies to the original analytical, organizational, and derived components of this deposit to the extent permitted by applicable law. Parliamentary speech texts retain their original provenance in the Brazilian Chamber of Deputies. This statement does not assert authorship of the parliamentary speeches or specify the license of the accompanying software repository.
