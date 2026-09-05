# Part A Recommendation Memo

## Headline numbers from the independent multilingual tokenizer analysis
Using the existing FLORES-200 workbook as the multilingual corpus, the verified dataset statistics are:
- English: 2009 sentences
- Hindi: 2009 sentences
- Kannada: 2009 sentences
- Tamil: 2009 sentences
- All_Sentences: 8036 rows total
- Empty rows: 0
- Duplicate entries: 0

The independent A3 analysis used the full `dev` split as the primary result. This is the canonical A3 analysis: 997 sentences per language, 3988 total `dev` sentences.

| tokenizer | English | Hindi | Kannada | Tamil |
|---|---:|---:|---:|---:|
| `gpt2` tokens/whitespace-word | 1.23 | 7.79 | 22.68 | 24.62 |
| `xlm-roberta-base` tokens/whitespace-word | 1.38 | 1.49 | 2.57 | 2.42 |

These values are measured on the canonical `dev` dataset; the earlier 200-sentence per-language run remains a pilot/sanity check and is not the primary result.

## What the A3 results mean
The A3 result is useful because it cleanly separates three distinct ideas:

1. Linguistic fertility metric: tokens per whitespace word. This is a language-and-tokenizer comparison metric. It is informative because it approximates how much more tokenization overhead a script or language family imposes relative to a human-written word boundary. Its weakness is that whitespace words are not a constant unit across scripts or languages; they can vary with orthography and tokenization choices.
2. Text-size normalization metric: tokens per UTF-8 byte. This measures tokenization overhead relative to encoded text size. It is useful when the goal is to compare how much token budget a language consumes for the same byte budget. Its weakness is that UTF-8 byte count is not itself a linguistic unit and does not reflect actual serving cost or prompt structure.
3. Actual production serving metric: measured input/output token counts and latency. This is the metric that directly answers operational cost. Its weakness is that it requires real traffic or representative serving logs, which are unavailable in this assignment.

## Which single number should drive the routing-and-cost decision?
For cross-language corpus normalization, I would use `tokens per UTF-8 byte` as the primary comparison number for a first-pass routing heuristic because it holds encoded text size approximately constant across languages and therefore better reflects the cost of carrying the same byte budget through the model. This is a better corpus-level normalization than tokens per sentence, because sentence length itself varies substantially across languages and prompt structure.

That said, this is not a universal truth. For actual production cost, the project should validate this proxy against observed tokenizer token counts and request latency. In other words:

> For cross-language corpus normalization, use tokens per UTF-8 byte as the primary comparison because it holds encoded input size approximately constant. For actual production cost, validate this proxy against observed tokenizer token counts and latency.

The measured results support this framing: the gap between English and Indic languages is large under tokens per whitespace word, but it shrinks substantially under tokens per UTF-8 byte for the multilingual tokenizer. That makes UTF-8 byte count a stronger normalized proxy than sentence count when comparing languages on the same corpus, while still recognizing that actual production cost must be measured directly.

## Biggest caveat
This corpus is a benchmark, not a serving trace. It does not include latency, prompt distribution, batch sizing, or real deployment traffic. The results are therefore useful for corpus-level normalization and routing heuristics, but they are not production cost facts.

## Explicit blocker on A2
The original `fertility.py` audit remains blocked because the original script and its baseline artifacts are unavailable. The project does not claim to have corrected a previous intern's result. The original fertility.py audit remains blocked because the original script is unavailable.

## Recommended operational rule
For a routing decision, monitor actual input/output tokens and latency by language and prompt length, and use the corpus ratios as a prior signal only. The benchmark can inform a language-specific cost heuristic, but the final routing rule should be calibrated with real serving data.
