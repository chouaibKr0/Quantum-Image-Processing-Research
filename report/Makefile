# Makefile for LaTeX Report Compilation
# Updated for modular document structure

MAIN = main-modular
LATEX = pdflatex
BIBTEX = bibtex

# Default target
all: $(MAIN).pdf

# Compile PDF (full build with bibliography)
$(MAIN).pdf: $(MAIN).tex references.bib
	$(LATEX) $(MAIN)
	$(BIBTEX) $(MAIN)
	$(LATEX) $(MAIN)
	$(LATEX) $(MAIN)

# Quick compile (without bibliography update)
quick:
	$(LATEX) $(MAIN)

# Clean auxiliary files
clean:
	rm -f *.aux *.log *.bbl *.blg *.toc *.lof *.lot *.out *.fls *.fdb_latexmk *.synctex.gz

# Clean everything including PDF
cleanall: clean
	rm -f $(MAIN).pdf

# Watch for changes and recompile (requires latexmk)
watch:
	latexmk -pdf -pvc $(MAIN)

.PHONY: all quick clean cleanall watch
