RM       = /bin/rm
CP       = /bin/cp
ECHO     = /bin/echo
LATEX    = latex
DVIPS    = dvips
PDFLATEX = pdflatex
RCS      = rcs
CI       = ci -zLT -s- -t-
L2H      = latex2html

#
#

TEXSRC  = resume.tex
TEXMAC  = ${wildcard *.macros.tex}
#DVISRC  = ${patsubst %.tex, %.dvi, ${TEXSRC}}
PSDOC   = ${patsubst %.dvi, %.ps, ${DVISRC}}
PDFDOC  = ${patsubst %.tex, %.pdf, ${TEXSRC}}
#HTMLDOC = ${patsubst %.tex, %.html, ${TEXSRC}}
SOURCES = ${TEXSRC} ${TEXMAC} GNUmakefile

#
#

all: ${PSDOC} ${PDFDOC}
#all: ${DVISRC} ${PSDOC} ${PDFDOC} ${HTMLDOC}

%.dvi: %.tex
	${LATEX} $< > /dev/null

%.ps: %.dvi
	@echo -n Building PS from DVI        :
	@${DVIPS} $<
	@echo [Done]

%.pdf: %.tex
	@echo -n Building PDF from LaTeX     :
	@${PDFLATEX} $< > /dev/null
	@echo " [Done]"

%.html: %.tex
	${L2H} $<

ci: ${SOURCES}
	if [ ! -d RCS ] ; then mkdir RCS ; fi
	- ${RCS} -i -U ${SOURCES}
	${CI} -u ${SOURCES}

clean:
	- ${RM} ${DVISRC} ${PSDOC} ${PDFDOC} 
	- ${RM} -rf resume/

spotless: clean
	- ${RM} *.aux *.log
