# Part C — Decision Memo

## FACTS FROM ASSIGNMENT
- 2-week compute window
- 3-week launch review
- 10 reviewer hours/week
- Reviewer is limited to Hindi + Kannada
- One A100-80GB GPU is available
- No external API budget is available
- The model must produce casual, natural language output for Hindi, Kannada, Tamil, Telugu, Bengali, and Marathi

## ASSUMPTIONS
- The reviewer can judge Hindi and Kannada directly with a fixed rubric.
- The other four languages cannot be directly reviewed by a native speaker in this project.
- A prompt-engineering baseline is feasible within the timeline without external API spend.
- A local model rewrite path is possible on one A100-80GB GPU if needed.
- A fixed evaluation set is more defensible than a broad unbounded review pass.

## CALCULATIONS
The reviewer has 10 hours/week for 2 weeks, which is 20 review hours total.

If review takes 10 minutes per sample, then the reviewer can assess:
- 20 hours × 60 minutes/hour ÷ 10 minutes per sample = 120 total samples

A reviewer-feasible plan is therefore:
- 40 Hindi examples
- 40 Kannada examples
- 20 examples in each of the other four languages only under a proxy review method

This keeps the evaluation workload inside the actual reviewer limit without pretending the reviewer can validate all six languages directly.

## Primary human-reviewed metric
Primary human-reviewed metric:
- percentage of Hindi and Kannada outputs judged casual and natural by the native-speaker reviewer on a fixed set of prompts

Use a fixed evaluation set, for example:
- 40 Hindi examples
- 40 Kannada examples
- 10 prompts × 4 style variants = 40 examples per language

This is feasible within 20 hours if each item takes roughly 10 minutes to assess.

For the four languages without native-speaker review:
- use a clearly labelled proxy metric such as: percentage of outputs judged as non-textbook-like by a structured rubric from a bilingual reviewer or a rule-based style checklist
- or hold them as a validation limitation if no valid proxy is available

Do not claim direct native-speaker validation for Tamil, Telugu, Bengali, or Marathi when the reviewer does not have that capability.

## Success threshold
Assumption-based decision threshold:
- Pass the prompt-engineering baseline if at least 80% of Hindi and Kannada examples are judged casual and natural by the reviewer.
- Fail or escalate to a local rewrite path if the pass rate is materially below that threshold.
- For the other four languages, require at least a reasonable proxy improvement trend, but do not present this as native-speaker validation.

## Kill criterion
Kill the prompt-engineering path only if:
- after the first week, the reviewed Hindi/Kannada outputs are clearly not casual and natural,
- or the reviewer cannot complete the fixed evaluation set within the available 20 review hours,
- or the candidate model is not producing stable output quality improvements across the fixed benchmark set.

This is measurable and tied to the actual reviewer constraints.

## PREDICTIONS
Prediction: the cheapest credible first step is a prompt-engineering baseline, because it requires no external API budget and fits the limited review capacity.

Prediction: a local <=1B rewriter is the next justified step only if prompt engineering fails in Hindi or Kannada under the fixed review rubric.

Prediction: full SFT is not the first choice under the stated constraints because it is costlier, slower, and more difficult to validate with only 20 review hours and a single A100-80GB GPU.

## Recommendation
Choose prompt engineering first, then a local <=1B rewriter only if the Hindi/Kannada reviewer signal is poor. Do not commit to full SFT without a clear, reviewer-confirmed quality gap and a realistic path to validate the output in the 3-week launch window.

The recommendation is bounded by the actual review capacity: Hindi and Kannada are the only languages that can be directly validated by the reviewer in the time available, so any broader-language launch decision must treat the remaining languages as limited or proxy-evaluated rather than fully validated.
