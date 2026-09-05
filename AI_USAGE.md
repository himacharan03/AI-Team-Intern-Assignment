# AI Usage

## AI Tools Used
GitHub Copilot in VS Code was used for workspace inspection, Python scaffolding, documentation drafting, and command validation. No external AI model was used to fabricate missing project artifacts.

## Where AI Helped
- Suggested the repository layout and evidence-first audit structure.
- Drafted the workbook inspection script that verified language counts, split counts, and empty/duplicate rows.
- Drafted the tokenizer comparison scripts for `gpt2` and `xlm-roberta-base`.
- Helped separate the 200-sentence pilot from the canonical full `dev` analysis.
- Helped format the blocked A2 and Part B documentation so the project remains honest about missing source artifacts.

## AI-Generated Code Used
The accepted code was the actual workbook verifier and tokenizer analysis scripts in:
- `your-submission/partA/code/analyze_corpus.py`
- `your-submission/partA/code/tokenizer_analysis_fast.py`
- `your-submission/partA/code/tokenizer_analysis.py`

These scripts were used only after validation against the real workbook and the generated CSV outputs.

## AI Suggestions Rejected
The following claims were rejected because they would require fabricated material and would violate the assignment constraints:
- fabricating `fertility.py`
- fabricating `REPORT_v0.md`
- fabricating benchmark logs or model specs
- fabricating KV-cache values or throughput results
- fabricating A2 bug evidence or before/after measurements
- treating a corpus denominator as if it were a measured production-cost metric

## AI Mistakes / Limitations
The main limitation was not a technical model failure; it was the lack of source artifacts. The AI could propose plausible wording or code, but it could not legitimately manufacture the missing intern artifacts, benchmark files, or A2 results. Human verification was required for every claim.

## Human Verification
The final statements in this submission were verified by running the actual project commands and checking the generated files:
- `python your-submission/partA/code/analyze_corpus.py`
- `python your-submission/partA/code/tokenizer_analysis_fast.py`
- `python your-submission/partA/code/tokenizer_analysis.py`

Human checks confirmed:
- the workbook had 8036 `All_Sentences` rows,
- each language had 2009 rows,
- split counts were `dev=3988` and `devtest=4048`,
- empty rows = 0 and duplicate entries = 0,
- the pilot and full-dev CSV files were created,
- the missing A2 and Part B artifacts remain blocked rather than invented.

AI was not allowed to fabricate fertility.py, REPORT_v0.md, benchmark logs, KV-cache values, throughput results, or A2 bug evidence. The final project keeps those sections explicitly blocked.
