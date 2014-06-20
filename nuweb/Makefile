all : empty.pdf
.PHONY : all



NUWEB=/usr/local/bin/nuweb
.SUFFIXES: .pdf .w .tex .html .aux .log .php

FIGFILES=fileschema

FIGFILENAMES=$(foreach fil,$(FIGFILES), $(fil).fig)
PDFT_NAMES=$(foreach fil,$(FIGFILES), $(fil).pdftex_t)
PDF_FIG_NAMES=$(foreach fil,$(FIGFILES), $(fil).pdftex)
PST_NAMES=$(foreach fil,$(FIGFILES), $(fil).pstex_t)
PS_FIG_NAMES=$(foreach fil,$(FIGFILES), $(fil).pstex)

W2PDF=../nuweb/bin/w2pdf
HTML_PS_FIG_NAMES=$(foreach fil,$(FIGFILES), m4_htmldocdir/$(fil).pstex)
HTML_PST_NAMES=$(foreach fil,$(FIGFILES), m4_htmldocdir/$(fil).pstex_t)
MKDIR = mkdir -p

 

%.eps: %.fig
	fig2dev -L eps $< > $@

%.pstex: %.fig
	fig2dev -L pstex $< > $@

.PRECIOUS : %.pstex
%.pstex_t: %.fig %.pstex
	fig2dev -L pstex_t -p $*.pstex $< > $@

%.pdftex: %.fig
	fig2dev -L pdftex $< > $@

.PRECIOUS : %.pdftex
%.pdftex_t: %.fig %.pstex
	fig2dev -L pdftex_t -p $*.pdftex $< > $@

%.pdf : %.w $(W2PDF)  $(PDF_FIG_NAMES) $(PDFT_NAMES)
	chmod 775 $(W2PDF)
	$(W2PDF) $*

m4_htmldocdir/%.pstex : %.pstex
	cp  $< $@

m4_htmldocdir/%.pstex_t : %.pstex_t
	cp  $< $@


m4_empty.w : a_empty.w
	gawk '{if(match($$0, "@%")) {printf("%s", substr($$0,1,RSTART-1))} else print}' a_empty.w \
          | gawk '{gsub(/[\\][\$$]/, "$$");print}'  > m4_empty.w

empty.w : m4_empty.w
	m4 -P m4_empty.w > empty.w

bibfile : empty.aux /home/paul/bin/mkportbib
	/home/paul/bin/mkportbib empty litprog

.PHONY : bibfile
$(W2PDF) : empty.w
	$(NUWEB) empty.w
m4_htmlsource : empty.w
	cp  empty.w m4_htmlsource

m4_4htfildest : m4_4htfilsource
	cp m4_4htfilsource m4_4htfildest

m4_htmlbibfil : m4_anuwebdir/empty.bib
	cp m4_anuwebdir/empty.bib m4_htmlbibfil

m4_htmltarget : m4_htmlsource m4_4htfildest $(HTML_PS_FIG_NAMES) $(HTML_PST_NAMES) m4_htmlbibfil
	cp w2html /home/paul/projecten/programmeren/nuweb/nuwebtemplate/bin
	cd /home/paul/projecten/programmeren/nuweb/nuwebtemplate/bin && chmod 775 w2html
	cd m4_htmldocdir && /home/paul/projecten/programmeren/nuweb/nuwebtemplate/bin/w2html empty.w


pdf : empty.pdf

print : empty.pdf
	lpr empty.pdf

view : empty.pdf
	evince empty.pdf

html : m4_htmltarget

DIRS = @<directories to create@>

$(DIRS) : 
	$(MKDIR) $@

sources : empty.w $(DIRS)
	$(NUWEB) empty.w

jetty : sources
	cd .. && mvn jetty:run


