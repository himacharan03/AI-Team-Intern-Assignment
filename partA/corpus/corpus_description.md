# A1 Corpus Description

## Source
This corpus was already present in the workspace as `FLORES_200_4_Languages.xlsx`.
It was used as the evaluation corpus without replacement or recreation.

## Languages
- English
- Hindi
- Kannada
- Tamil

## Domain
The workbook identifies the source as FLORES-200. It is a general multilingual evaluation corpus, not a custom production-domain dataset. The available workbook metadata is not sufficient to make a narrower domain claim.

## Corpus size
Verified from the workbook itself:
- All_Sentences: 8036 rows total
- English: 2009 rows
- Hindi: 2009 rows
- Kannada: 2009 rows
- Tamil: 2009 rows

## Structure
Workbook sheets:
- All_Sentences
- English
- Hindi
- Kannada
- Tamil

Columns in each sheet:
- split
- sentence_id
- language
- language_code
- sentence

## Parallel structure
The data appears parallel by `sentence_id` and `split` across languages.
A direct workbook check found:
- 0 empty sentence rows
- 0 duplicate sentence entries
- 3988 `dev` rows in the combined table
- 4048 `devtest` rows in the combined table

This supports the use of a parallel, aligned multilingual corpus for cross-language comparisons.

## Preprocessing
No preprocessing steps were applied by this project to the original workbook. The corpus was read directly from the Excel file as provided.

## Limitations / caveats
- The corpus is not a custom domain-specific evaluation set; it is a general multilingual benchmark.
- The `All_Sentences` table contains a mixture of `dev` and `devtest` splits, not just one evaluation set.
- The workbook was not modified, and no synthetic rows or translations were added.
- For a stricter fairness analysis, the same sentence IDs and same split set should be compared across languages.
- The file does not document any explicit cleaning or normalization beyond the source dataset itself.

## What the corpus can tell us
This corpus is suitable for measuring tokenization and corpus-level multilingual characteristics such as:
- tokens per word
- tokens per character
- cross-language fertility differences
- denominator sensitivity across languages

## What it cannot tell us
It cannot establish production cost or inference latency by itself; it is a benchmark corpus, not a serving trace or deployment log.
