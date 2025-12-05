TEX = platex
PDF = dvipdfmx
BIB = bibtex
VERSION = 11.0
UNAME = $(shell uname)
ifneq ($(UNAME),Darwin)
Adobe_Folder = /cygdrive/c/Program\ Files\ \(x86\)/Adobe/
ProgExists = $(shell find $(Adobe_Folder) -name Acrobat.exe)
ifeq ($(ProgExists),)
Adobe_EXE = AcroRd32.exe
HEADER = Reader
else
Adobe_EXE = Acrobat.exe
HEADER = Acrobat
endif
Adobe = /cygdrive/c/Program\ Files\ \(x86\)/Adobe/$(HEADER)\ $(VERSION)/$(HEADER)/$(Adobe_EXE)
else
Adobe = open -a Preview
PID = $(shell 	ps auxw | grep Preview | egrep -v grep |grep Application|awk '{ print $$2}' )
endif
#
#
#Task_Exists = $(shell tasklist | grep $(Adobe_EXE))
#
#
TARGET = main
SOURCE = $(TARGET).tex localenv.sty intro.tex concl.tex\
         sec2.tex sec3.tex sec4.tex sec5.tex

REFER = main.bib

#FIGS = 	eps/

.SUFFIXES: .tex .dvi .pdf

force: clean pdf

pdf: $(TARGET).pdf
	$(Adobe) $(TARGET).pdf 

ifneq ($(UNAME),Darwin)
clean:
	-taskkill /im AcroRd32.exe /f
	-rm -f *.dvi *.aux *.log *.toc *~ $(TARGET).pdf
else
clean:
ifneq ($(PID),)
	kill $(PID)
endif
	@rm -f *.dvi *.aux *.log *.toc *.idx *~ $(TARGET).pdf
endif

#.tex.dvi: $(SOURCE) $(FIGS)
.tex.dvi: 
#.tex.dvi: $(SOURCE)
	-rm -f *.aux *.toc. *.log *.dvi
	$(TEX) $<
#	$(BIB) $*
#	$(TEX) $*
	$(TEX) $*

bib: $(REFER)
	$(BIB) $(TARGET)

.dvi.pdf:
	$(PDF) -V 5 $<

#$(TARGET).pdf: $(TARGET).dvi
#$(TARGET).dvi: $(SOURCE) $(FIGS)
