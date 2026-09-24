# Data Dictionary

Corrected release: 26,644 speeches, 41,038 identified claims, and 797 author-confirmed final analytical claims. The article reports 41,039 extracted claims; see the correction notes for the distinction.

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

The taxonomy contains 21 rows, 5 distinct Macro categories, 14 distinct Meso categories, and 12 distinct nonempty Micro categories. Nine rows have an empty `micro` field: these rows specify no Micro category. The claims file mixes final numbered category labels and other textual labels. Do not join every label to the final taxonomy or interpret blank labels as an HDBSCAN noise code. Some labels differ in whitespace or wording.

## Relationships and reuse

Use `speech_id` to trace an extracted claim back to its source speech and to consult the original text and metadata. The speech and claim files represent different units of observation: a count of claims is not a count of speeches.

To recover the final analytical corpus, filter `considered` for `Sim`: this returns exactly 797 records. A nonempty `macro` field identifies the same set in this release. This equivalence is specific to this dataset and is based on author confirmation.

Consult the source speech when interpreting a claim, and distinguish extracted wording from the processed representation in `canonical_claim`. Classifications and categories are research outputs and should be interpreted in the context of the documented analytical procedure.

## Language and file conventions

Parliamentary speeches, extracted claims, and substantive analytical categories are in Portuguese. Variable names and this documentation are in English.

All three supplied CSVs decode as UTF-8 with a byte-order mark (BOM). They use comma delimiters, double-quoted text where required, and doubled internal quotation marks. Import them with a CSV-aware reader rather than splitting lines on commas. Every parsed record has the expected number of fields.

Dates are recorded as `YYYY-MM-DD`. Speech dates range from 2000-10-10 to 2024-12-19. Recorded times include values such as `14h14`. Treat identifiers as text. The fields `speaker`, `party`, and `state` retain source/export conventions: speaker strings can include party/state information, party values can contain leading spaces, and state values are not uniformly standardized two-letter codes. Retrieval keywords can be separated by semicolons within a cell.

The classification fields and `considered` contain only `Sim` or empty cells. Empty cells also occur in metadata and category fields. In `considered`, an empty cell denotes exclusion from the final analytical corpus. In the legacy component classification columns, an empty cell is an unrecorded affirmative value whose substantive meaning is not established by this correction.

## Counts, corrections, and remaining limitations

The dissertation, *É tudo sobre a Terra: A instrumentalização do clima na deslegitimação da luta pela terra no Congresso Nacional (2000–2024)* (Thales Rodrigues Antonelli, 2026), reports **797 final claims** on printed page 109 (PDF page 110). Printed page 104 describes the joint three-condition inclusion criterion.

The dissertation reports 41,038 extracted claims on printed page 102 and 41,039 on printed page 109. The article's historical total is 41,039. The corrected CSV contains 41,038 identified claims, agreeing with printed page 102. The final corpus remains 797 claims.

The original workbook and earlier claims CSV matched on all exported fields. The corrected release makes two changes:

1. Marks 655 additional author-confirmed final claims as `considered=Sim`, retaining the original 142 positive flags, for a total of 797.
2. Removes the record without speech ID, date, claim ID, claim text, or canonical claim, which contained only `meso=0` and `micro=0`. This was original data record 798 (CSV record 799 counting the header).

All other values, including component classifications, claim text, category labels, and identifiers, are unchanged. All 41,038 corrected claim IDs are unique and link to existing source speeches. The 26,644 speech records and the taxonomy CSV are unchanged.

The final 797 claims include 142 with numbered final Macro categories and 655 with other textual Macro labels. The author confirmation establishes sample membership, not a complete mapping of all stored labels to the final taxonomy. Among the original 142 marked claims, 6 Meso labels and 10 nonempty Micro labels do not match the corresponding taxonomy vocabulary after trimming whitespace. Exact-text taxonomy joins therefore still require review. No category assignments or component classifications were inferred or replaced in this correction.

