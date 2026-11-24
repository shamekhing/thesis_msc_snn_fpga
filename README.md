# SNN logic-block investigation notes (Overleaf)

Upload the zip: Overleaf > New Project > Upload Project. Compiler: pdfLaTeX, main file: `main.tex`. Bibliography uses BibTeX with `IEEEtran` (built into Overleaf).

## Layout
- `main.tex` - title, abstract, section includes
- `sections/02b-paper-analysis.tex` - detailed analysis of the Windhager et al. paper (claims, cost model, evidence, weaknesses, questions for the author)
- `sections/02c-idea-ledger.tex` - every idea with status, pros, cons and next test
- `sections/01..10-*.tex`, `sections/A-brainstorm.tex` - the other sections, one file per section
- `figures/fig-logic-block.tex`, `figures/fig-architecture.tex` - TikZ drawings (editable, no images)
- `references.bib` - entries marked `verify` were written from memory
- `resources/` - the Windhager et al. AICAS 2024 PDF and the research-notes PDF (not used by LaTeX)

## Markers in the text
- red `[TODO: ...]` - work still to do
- orange `[verify: ...]` - a fact to check against a primary source before relying on it

## Not measured
No simulation or hardware result exists yet. Numbers in Table 1 are copied from the baseline paper; everything about the proposed design is reasoning.

## Reading list
- Boutros, Betz - FPGA Architecture: Principles and Progression: https://www.eecg.utoronto.ca/~vaughn/papers/casm2021_arch_survey.pdf
- Kuon, Tessier, Rose - FPGA Architecture: Survey and Challenges: https://www.eecg.toronto.edu/~jayar/pubs/kuon/foundtrend08.pdf
- Betz, Rose - routing segmentation and buffering: https://www.eecg.utoronto.ca/~jayar/pubs/betz/fpga99betz.pdf
- Betz, Verilog to Routing seminar (video): https://www.youtube.com/watch?v=lQ1RKbEJZmE
