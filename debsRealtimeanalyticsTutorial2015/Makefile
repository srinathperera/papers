NAME = debs
TEX_SOURCES = debs.tex 
BIB_FILES = sigproc.bib
EPS_FILES = figures/*

all: dvi
dvi: $(NAME).dvi
ps: $(NAME).ps
pdf: $(NAME).pdf

build: $(TEX_SOURCES) 
#	pdflatex $(NAME) && bibtex ${NAME} && pdflatex $(NAME) && pdflatex $(NAME)
#	pdflatex $(NAME) pdflatex $(NAME) && pdflatex $(NAME)
	latex $(NAME) && bibtex ${NAME} && latex $(NAME) && latex $(NAME)


# ps
$(NAME).ps: $(NAME).dvi
	dvips $< -o $@

# pdf
$(NAME).pdf: $(NAME).ps
	@ if [ -x /usr/local/bin/distill ]; then \
		echo distill $<; \
		distill $<; \
	else \
		echo; \
		echo 'Warning: No distill found.  Use ps2pdf instead.'; \
		echo ps2pdf $<; \
		ps2pdf $<; \
	fi

xdvi: dvi
	xdvi $(NAME).dvi &

gv: ps
	gv $(NAME).ps &

acroread: pdf
	acroread $(NAME).pdf &

print: lpr

lpr: ps
	lpr $(NAME).ps

clean:
	rm -f *.aux $(NAME).bbl $(NAME).blg $(NAME).log \
		$(NAME).dvi $(NAME).ps $(NAME).pdf
