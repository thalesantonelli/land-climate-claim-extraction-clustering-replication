# Data Dictionary

This dictionary describes the supplied extracted_claims.csv and parliamentary_speeches.csv, with the updated taxonomy.csv. No new claim-classification fields have been added.


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

