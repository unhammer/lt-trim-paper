# From http://www.wlug.org.nz/LatexMakefiles
TARGET=trim_talk
FIGURES=architecture.eps bi.eps bi-prefixed.eps bi-prefixed-moved.eps mono-simple.eps trimmed-simple-1.eps trimmed-simple-2.eps trimmed-simple-3.eps trimmed-simple-4.eps trimmed-simple.eps mono.eps trimmed.eps

# make pdf by default
all: ${TARGET}.pdf

# it doesn't really need the .dvi, but this way all the refs are right
%.pdf : ${TARGET}.tex ${FIGURES}
	latex $<
	pdflatex $<

${TARGET}.bbl: apertium.bib
# in case we don't already have a .aux file listing citations
# this should probably be a separate makefile target/dependency instead
# of doing it every time... but *shrug*
	latex ${TARGET}.tex
# get the citations out of the bibliography
	bibtex ${TARGET}
# do it again in case there are out-of-order cross-references
	latex ${TARGET}.tex

# Figures printable with tgif:
%.eps: %.obj
	tgif -color -print -eps $<



clean:
	rm -f ${TARGET}.{log,aux,ps,dvi,bbl,blg,log,toc,snm,nav,out} ${FIGURES}
	rm -rf auto/

reallyclean: clean
	rm -f ${TARGET}.{ps,pdf}

getbib:
	wget "http://bibsonomy.org/bib/user/unhammer/apertium?bibtex.entriesPerPage=100" -O apertium.bib
	touch apertium.bib

PHONY : ps all clean reallyclean getbib
