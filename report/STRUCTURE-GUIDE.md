# Report Structure Guide

This document explains the modular structure of the LaTeX report and how to work with it.

## File Structure

```
report/
├── main-modular.tex          # Main document (use this for compilation)
├── main.tex                  # Original monolithic version (backup)
├── references.bib            # Bibliography
├── Makefile                  # Build automation
├── figures/                  # Images and diagrams
├── chapters/                 # Main content chapters
│   ├── abstract.tex
│   ├── conventions.tex
│   ├── introduction.tex
│   ├── chapter1.tex          # Classical Paradigm
│   ├── chapter2.tex          # Quantum Clustering (includes algorithms)
│   ├── conclusion.tex
│   └── algorithms/           # Individual algorithm files
│       ├── quantum-kmeans.tex
│       ├── quantum-spectral.tex
│       ├── variational-quantum.tex
│       ├── quantum-fuzzy.tex
│       └── comparative-analysis.tex
└── appendices/
    ├── appendix-a-quantum-primer.tex
    └── appendix-b-fuzzy-logic.tex
```

## Compiling the Document

To compile the modular version:

```bash
# Using pdflatex
pdflatex main-modular.tex
bibtex main-modular
pdflatex main-modular.tex
pdflatex main-modular.tex

# Or use the Makefile (update target name first)
make
```

## Parallel Editing

Each file can be edited independently. Multiple team members can work on different files simultaneously:

- **Person A**: `chapters/chapter1.tex` (Classical methods)
- **Person B**: `chapters/algorithms/quantum-kmeans.tex` (q-Means algorithm)
- **Person C**: `chapters/algorithms/quantum-spectral.tex` (Spectral clustering)
- **Person D**: `appendices/appendix-a-quantum-primer.tex` (Quantum basics)

## How to Add a New Quantum Algorithm

### Step 1: Create the Algorithm File

Create a new file in `chapters/algorithms/`. For example, `quantum-newmethod.tex`:

```latex
% chapters/algorithms/quantum-newmethod.tex
% Quantum New Method Algorithm

\subsection{Quantum New Method}

Brief introduction to the algorithm...

\subsubsection{Algorithm Description}

Detailed description...

\begin{algorithm}
\caption{Quantum New Method}
\begin{algorithmic}[1]
\STATE \textbf{Input:} ...
\STATE ...
\STATE \textbf{Output:} ...
\end{algorithmic}
\end{algorithm}

\subsubsection{Complexity Analysis}

\textbf{Complexity:} $O(...)$ compared to $O(...)$ classically.

\begin{tipbox}
Helpful tips about the algorithm...
\end{tipbox}

\begin{warningbox}
Limitations or caveats...
\end{warningbox}
```

### Step 2: Include in Chapter 2

Open `chapters/chapter2.tex` and add an `\input` line before the comparative analysis:

```latex
\input{chapters/algorithms/quantum-kmeans}
\input{chapters/algorithms/quantum-spectral}
\input{chapters/algorithms/variational-quantum}
\input{chapters/algorithms/quantum-fuzzy}
\input{chapters/algorithms/quantum-newmethod}    % <-- ADD THIS LINE
\input{chapters/algorithms/comparative-analysis}
```

### Step 3: Update Comparative Analysis

Open `chapters/algorithms/comparative-analysis.tex` and add a row to the comparison table:

```latex
\begin{tabular}{@{}lccc@{}}
\toprule
\textbf{Algorithm} & \textbf{Speedup} & \textbf{Hardware} & \textbf{Maturity} \\
\midrule
q-Means & Exponential & Fault-tolerant + qRAM & Theoretical \\
Quantum Spectral & Exponential & Fault-tolerant & Theoretical \\
QAOA Clustering & Potential & NISQ & Experimental \\
VQE Clustering & Heuristic & NISQ & Experimental \\
Quantum Fuzzy & Quadratic & Fault-tolerant & Theoretical \\
Quantum New Method & Your Speedup & Your Hardware & Your Maturity \\  % <-- ADD THIS
\bottomrule
\end{tabular}
```

## Available Callout Boxes

Use these environments for consistent styling:

| Environment | Color | Icon | Use Case |
|------------|-------|------|----------|
| `notebox` | Blue | sticky-note | Background info, context |
| `tipbox` | Teal | lightbulb | Best practices, advice |
| `warningbox` | Orange | exclamation-triangle | Caveats, pitfalls |
| `cautionbox` | Red | fire | Critical limitations |
| `definitionbox` | Gray | book | Formal definitions |
| `keyconceptbox` | Orange | key | Core ideas, takeaways |
| `examplebox` | Light gray | code | Concrete examples |

### Example Usage:

```latex
\begin{definitionbox}[My Custom Title]
Your definition here...
\end{definitionbox}

\begin{tipbox}
Your tip here...
\end{tipbox}

\begin{warningbox}[Important Warning]
Your warning here...
\end{warningbox}
```

## File Naming Conventions

- Use lowercase with hyphens: `quantum-kmeans.tex`, `quantum-spectral.tex`
- Prefix algorithm files with `quantum-` for consistency
- Keep names descriptive but concise

## Tips for Collaboration

1. **Pull before editing**: Always get the latest version before starting work
2. **Edit only your assigned files**: Avoid merge conflicts
3. **Test compilation**: Run `pdflatex` to check for errors before committing
4. **Use comments**: Add `% TODO:` or `% FIXME:` for incomplete sections
5. **Keep backups**: The original `main.tex` serves as a reference

## Questions?

If you need to add new packages or environments, edit the preamble in `main-modular.tex`.
