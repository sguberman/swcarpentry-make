include config.mk

TXT_FILES=$(wildcard books/*.txt)
DAT_FILES=$(patsubst books/%.txt, %.dat, $(TXT_FILES))
PLOT_FILES=$(patsubst %.dat, %.plot, $(DAT_FILES))
ZIPF_DIR=zipf_analysis
ZIPF_ARCHIVE=$(ZIPF_DIR).tar.gz

## all		: Generate archive of code, data, plots, and Zipf summary table.
.PHONY : all
all : $(ZIPF_ARCHIVE)

$(ZIPF_ARCHIVE) : $(ZIPF_DIR)
	tar -czf $@ $<

$(ZIPF_DIR) : Makefile results.txt $(DAT_FILES) $(PLOT_FILES) $(COUNT_SRC) $(PLOT_SRC) $(ZIPF_SRC)
	mkdir -p $@
	cp $^ $@

## plots		: Plot word occurences.
.PHONY : plots
plots : $(PLOT_FILES)

%.plot : %.dat $(PLOT_SRC)
	$(PLOT_EXE) $< ascii > $@

## results.txt 	: Generate Zipf summary table.
results.txt : $(DAT_FILES) $(ZIPF_SRC)
	$(ZIPF_EXE) $(DAT_FILES) > $@

## dats		: Count words in text files.
.PHONY : dats
dats: $(DAT_FILES)

%.dat : books/%.txt $(COUNT_SRC)
	$(COUNT_EXE) $< $@

## clean		: Remove auto-generated files.
.PHONY : clean
clean :
	rm -f $(DAT_FILES)
	rm -f results.txt
	rm -f $(PLOT_FILES)
	rm -f $(ZIPF_ARCHIVE)
	rm -rf $(ZIPF_DIR)

## variables	: Print variables.
.PHONY : variables
variables :
	@echo TXT_FILES: $(TXT_FILES)
	@echo DAT_FILES: $(DAT_FILES)
	@echo PLOT_FILES: $(PLOT_FILES)
	@echo ZIPF_DIR: $(ZIPF_DIR)
	@echo ZIPF_ARCHIVE: $(ZIPF_ARCHIVE)

.PHONY : help
help : Makefile
	@sed -n 's/^##//p' $<

