# A1 — Multilingual Corpus Verification

## Dataset source
The corpus already present in the workspace was used without replacement or recreation:

- `FLORES_200_4_Languages.xlsx`

## Languages
- English
- Hindi
- Kannada
- Tamil

## Corpus size
Verified from the workbook:
- All_Sentences rows: 8036
- English rows: 2009
- Hindi rows: 2009
- Kannada rows: 2009
- Tamil rows: 2009

## Domain
This is a general multilingual evaluation set derived from FLORES-200 rather than a task-specific domain corpus. It is suitable for multilingual benchmarking but not a production traffic distribution dataset.

## Structure
The workbook contains sheets:
- All_Sentences
- English
- Hindi
- Kannada
- Tamil

Each sheet contains:
- split
- sentence_id
- language
- language_code
- sentence

## Alignment and split structure
The combined dataset contains:
- 3988 rows with split = `dev`
- 4048 rows with split = `devtest`

The per-language rows are aligned by sentence_id and split, as expected for a parallel multilingual corpus.

## Preprocessing
No extra preprocessing or filtering was performed in this project. The dataset was used as provided.

## Quality checks
Verified:
- empty sentence rows: 0
- duplicate sentence entries: 0

## Character and word statistics
Calculated from the workbook as provided:

| language | avg chars/sentence | avg whitespace words/sentence | min chars | max chars |
|---|---:|---:|---:|---:|
| English | 128.00 | 21.33 | 28 | 368 |
| Hindi | 127.66 | 25.01 | 31 | 381 |
| Kannada | 134.45 | 15.69 | 34 | 388 |
| Tamil | 149.46 | 16.38 | 30 | 404 |

## Limitations and caveats
- This is a benchmark corpus, not a serving log.
- It is not custom-domain data for the target assistant scenario.
- It is useful for measuring tokenizer behavior, but not latency or throughput.
- The corpus does not include extra domain metadata beyond the source sentence text.

## Conclusion
The existing workbook is a valid and usable multilingual corpus for Part A analysis. It satisfies the required language set and is suitable for cross-language tokenizer evaluation when paired with actual measurement code.
