# FPGA-Native Recurrent Logic Blocks as Spiking Hidden Units

Monorepo for a master's thesis on building the hidden layer of a spiking neural network from the FPGA's own logic block: a look-up table (LUT), a flip-flop and an output multiplexer, joined by routing feedback, rather than mapping a conventional neuron onto processor-style hardware. The starting point is the differential-time SNN architecture of Windhager et al. (AICAS 2024), which the report analyzes in detail: claims, mechanisms, a derived cost model, evidence, strengths, weaknesses and open questions.

**Status.** The report is an investigation draft: ideas carry *active*, *parked* or *rejected* status and **no experimental results exist yet** for the proposed design. The code project separately reports a working training pipeline and bit-exact RTL-versus-model agreement; FPGA synthesis and on-board results are not claimed there either.

## Layout

```
report/                LaTeX investigation draft (entry point: report/main.tex)
code/
  fpga-snn/            submodule: differential-time SNN accelerator
                       (Python training + SystemVerilog RTL, Tang Primer 20K)
  fpga-skill/          submodule: reusable Gowin FPGA engineering skill
.gitignore             global git ignores: LaTeX, Python, HDL simulation, OS junk
.ignore                search-tool exclusions: ripgrep, fd, VS Code
```

The two projects under `code/` are independent repositories with their own remotes, histories and ignore files, registered here as git submodules.

## Cloning this repository

```
git clone --recurse-submodules https://github.com/shamekhing/thesis_msc_snn_fpga.git
# or, for an existing plain clone:
git submodule update --init
```

> **Pending push:** `code/fpga-snn` is pinned at a commit that is 2 commits ahead of its GitHub remote (branch `handover-paper-faithful-snn`). Until those commits are pushed from the `code/fpga-snn` working copy, the fpga-snn submodule cannot be fetched on a fresh clone.

## Building the report

- **Overleaf:** New Project > Upload Project with a zip of the contents of `report/`. Compiler: pdfLaTeX; main file: `main.tex`; bibliography: BibTeX with `IEEEtran` (built into Overleaf).
- **Locally:** run `pdflatex main.tex`, `bibtex main`, then `pdflatex` twice in `report/`. This needs `IEEEtran.bst` in the TeX installation.

An executive summary precedes the table of contents (`report/sections/00-executive-summary.tex`).

## Components

### `report/` - the investigation draft
The report itself: research idea, background, a detailed analysis of the Windhager et al. baseline (including a derived cost model and questions for the author), the idea ledger (every idea with status, pros, cons and a next test), the recurrent logic unit designs (single block and cluster), the relation to LIF neurons and what is recovered inside the same primitives, Siamese change detection, learning methods, FPGA implementation notes, the experimental plan, and open questions. Build instructions, marker legend and the reading list are in `report/README.md`.

### `code/fpga-snn` - differential-time SNN accelerator
An experimental SNN project for MNIST combining a Python training and reference-model workflow (snnTorch training, event encoder, integer reference model, 4-bit quantizer/ROM exporter) with SystemVerilog RTL for the Sipeed Tang Primer 20K (Gowin GW2A-18C). The RTL and the integer reference model agree bit-exactly on the golden test set (per-event-time spike traces, final potentials, output spike counts, and digit). See `code/fpga-snn/README.md`.

### `code/fpga-skill` - Gowin FPGA engineering skill
A reusable skill for FPGA work on Gowin devices (Tang Primer 20K / GW2A-18C class) with Gowin EDA, openFPGALoader, Icarus Verilog, Verilator and SystemVerilog, distilled from about 180 AI coding sessions (September to November 2026). Entry point: `SKILL.md`. See `code/fpga-skill/README.md`.

## Ignore files

- `.gitignore` applies to everything tracked by this repository: LaTeX build artifacts, Python caches and virtual environments, HDL simulation and synthesis output, and OS/editor junk. The nested repositories manage their own ignore files.
- `.ignore` is for search tools (ripgrep, fd, the VS Code Ignore extension): it hides the tracked reference PDFs in `report/resources/`, the compiled `main.pdf`, and the local datasets under `code/fpga-snn/data/` from editor and CLI search.

## Markers used in the report

- red `[TODO: ...]` - work still to do
- orange `[verify: ...]` - a fact to check against a primary source before relying on it
- `[active]`, `[parked]`, `[rejected]` - the current status of an idea

Numbers marked "derived" in the report were computed from the baseline paper's reported values, not reported by it.

