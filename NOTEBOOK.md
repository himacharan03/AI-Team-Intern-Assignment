# AI Team Intern Assignment — Audit Notebook

This notebook records the actual commands and outputs that were checked in this workspace. Measured values are labelled as measured; calculated values are labelled as calculated; interpretations and assumptions are explicitly separated.

## 2026-09-05 — Phase 1: Workspace Recovery

### Hypothesis
The missing starter artifacts may still exist in hidden directories, archives, or repository history.

### Experiment
I inspected the full workspace tree, searched for the expected files and archives, and checked whether a git repo or prior history existed.

### Command
Get-ChildItem -Force -Recurse; Get-ChildItem -Recurse -Include *.zip,*.tar,*.gz,*.rar,*.7z; git rev-parse --is-inside-work-tree

### Result
Measured result: the only assignment artifact found in the workspace was the workbook `FLORES_200_4_Languages.xlsx`. No `fertility.py`, `REPORT_v0.md`, `bench/model_spec.md`, `bench/bench_log.csv`, `corpus_sample` directory, archive, or git repository was found.

### Interpretation
This is a measured fact: A2 and Part B cannot be reconstructed from local verified evidence alone.

### Revision
No missing starter artifacts were fabricated or recreated.

### Next Step
Validate the workbook and complete the A1 corpus check.

## 2026-09-05 — Phase A1: Corpus Verification

### Hypothesis
The workbook in the workspace is a valid parallel four-language corpus for A1.

### Experiment
I loaded the workbook with `openpyxl` and computed language counts, split counts, total rows, empty rows, duplicate rows, and per-language sentence-length statistics.

### Command
python your-submission/partA/code/analyze_corpus.py

### Result
Measured result: the workbook contains the sheets `All_Sentences`, `English`, `Hindi`, `Kannada`, and `Tamil`. `All_Sentences` contains 8036 rows total; by language, English=2009, Hindi=2009, Kannada=2009, Tamil=2009. Split counts are `dev=3988` and `devtest=4048`. Empty rows = 0. Duplicate sentence entries = 0.

Calculated result: average characters per sentence = English 128.00, Hindi 127.66, Kannada 134.45, Tamil 149.46.

### Interpretation
The workbook is a valid aligned multilingual evaluation corpus for A1. The source is documented as FLORES-200; the workbook itself does not provide a narrower domain claim beyond that.

### Revision
The corpus is treated as a benchmark corpus, not as production traffic or a serving log.

### Next Step
Run the A3 tokenizer analysis using the canonical full `dev` split and keep the 200-sentence pilot distinct.

## 2026-09-05 — Phase A3: Tokenizer Pilot

### Hypothesis
A generic tokenizer and a multilingual tokenizer will differ meaningfully across languages, and denominator choice will change the apparent comparison.

### Experiment
I ran a pilot on the first 200 `dev` sentences per language for English, Hindi, Kannada, and Tamil using `gpt2` and `xlm-roberta-base`.

### Command
python your-submission/partA/code/tokenizer_analysis_fast.py

### Result
Measured result: the pilot wrote `partA/analysis/tokenizer_results.csv`.

Measured `gpt2` tokens per whitespace word: English 1.2486, Hindi 7.6986, Kannada 22.0359, Tamil 24.2254.
Measured `xlm-roberta-base` tokens per whitespace word: English 1.4922, Hindi 1.5871, Kannada 2.6826, Tamil 2.5588.
Measured `gpt2` tokens per UTF-8 byte: English 0.2086, Hindi 0.5924, Kannada 0.9757, Tamil 0.9928.
Measured `xlm-roberta-base` tokens per UTF-8 byte: English 0.2493, Hindi 0.1221, Kannada 0.1188, Tamil 0.1049.

### Interpretation
This pilot is a sanity check, not the canonical A3 result. It confirms the ranking differences and the denominator sensitivity but does not replace the full-dev analysis.

### Revision
The 200-sentence pilot remains labelled as a sample analysis; the full `dev` analysis is the primary A3 result.

### Next Step
Run the canonical full-dev tokenizer analysis and write the full-dev CSV as the A3 primary result.

## 2026-09-05 — Phase A3: Full-dev Analysis

### Hypothesis
The full `dev` split can be used as the canonical A3 comparison and should be reproducible without network access if the local tokenizer cache is available.

### Experiment
I ran the full-dev tokenizer comparison across the complete `dev` split: 997 sentences per language, 3988 dev rows total, across the same two tokenizers and denominators.

### Command
python your-submission/partA/code/tokenizer_analysis.py

### Result
Measured result: the command completed successfully and wrote `partA/analysis/tokenizer_results_full_dev.csv`.

Measured full-dev `gpt2` tokens per whitespace word: English 1.2285, Hindi 7.7865, Kannada 22.6843, Tamil 24.6169.
Measured full-dev `xlm-roberta-base` tokens per whitespace word: English 1.3837, Hindi 1.4890, Kannada 2.5680, Tamil 2.4226.
Measured full-dev tokens per UTF-8 byte and per sentence were also recorded in the CSV for both tokenizers.

### Interpretation
This full-dev output is the canonical A3 measurement for the assignment because it covers the whole `dev` split and is methodologically consistent with the same tokenizer policy.

### Revision
The pilot CSV remains a pilot/sanity check; the full-dev CSV is the primary result used for A3 comparison and recommendation.

### Next Step
Write the A4 memo using the full-dev result and clearly state the blocked A2 status.

## 2026-09-05 — A2 Recovery Attempt

### Hypothesis
A local recovery source may still exist for the original fertility script and baseline output.

### Experiment
I searched the workspace recursively and checked for hidden files, archives, and git history.

### Command
Get-ChildItem -Force -Recurse; Get-ChildItem -Recurse -Include *.zip,*.tar,*.gz,*.rar,*.7z; git rev-parse --is-inside-work-tree

### Result
Measured result: no recovery source was found. The original `fertility.py`, `REPORT_v0.md`, `bench/model_spec.md`, `bench/bench_log.csv`, and `corpus_sample` directory remain absent.

### Interpretation
This is a measured blocker: A2 cannot support any valid bug claim, metric-flaw claim, or before/after comparison without the original script and baseline output.

### Revision
A2 remains explicitly blocked and is documented in `partA/analysis/A2_BLOCKED.md`.

### Next Step
Keep the blocker explicit and do not claim the A2 audit is complete.

## 2026-09-05 — Part B Recovery Attempt

### Hypothesis
The original benchmark artifacts may still be recoverable from the local workspace.

### Experiment
I searched for the required benchmark files and checked the workspace for any archived or hidden copies.

### Command
Get-ChildItem -Force -Recurse; Get-ChildItem -Recurse -Include *.zip,*.tar,*.gz,*.rar,*.7z; git rev-parse --is-inside-work-tree

### Result
Measured result: the benchmark artifacts are missing. The workspace does not contain `bench/model_spec.md`, `bench/bench_log.csv`, or `REPORT_v0.md`.

### Interpretation
This is a measured blocker: B1-B4 cannot be legitimately completed because the original benchmark artifacts are missing.

### Revision
Part B remains explicitly blocked and documented in `partB/B_BLOCKED.md`.

### Next Step
Finish the final validation pass and keep all unsupported claims out of the submission.
