# ----------------------------------------
# Standard Constants
# ----------------------------------------
# these can be overwritten on the command line

OBO=http://www.ebi.ac.uk
ONT=cmpo
BASE=$(OBO)/$(ONT)
SRC=$(ONT)-edit.owl
RELEASEDIR=../..
ROBOT= ../../bin/robot
OORT=../../bin/ontology-release-runner
OWLTOOLS= owltools
USECAT= --use-catalog
SPARQLDIR = ../sparql

# ----------------------------------------
# Top-level targets
# ----------------------------------------

all: sparql_test imports $(ONT).owl $(ONT)-simple.owl $(ONT).obo
test: sparql_test all
prepare_release: all
	cp $(ONT).owl $(ONT)-simple.owl $(ONT).obo catalog-v001.xml $(RELEASEDIR) &&\
	tar cpfvz $(RELEASEDIR)/imports.tar.gz imports/*.owl  &&\
	echo "Release files are now in $(RELEASEDIR) - now you should add, commit, push and make a release on github"

# extract imports

#../../imports.tar.gz: imports/*.owl
#	tar cpfvz ../../imports.tar.gz imports/*.owl

imports: ../../imports.tar.gz
	tar xfvz ../../imports.tar.gz 

# ----------------------------------------
# Main release targets
# ----------------------------------------

# by default we use Elk to perform a reason-relax-reduce chain
# after that we annotate the ontology with the release versionInfo
$(ONT).owl: $(SRC)
	$(OORT) --outdir oort --reasoner elk --allow-overwrite --simple --simple-filtered --relaxed --re-mireot --add-support-from-imports --catalog-xml catalog-v001.xml --ignoreLock $< && cp oort/http\:/www.ebi.ac.uk/cmpo/cmpo.owl.owl $@ && $(ROBOT) annotate --ontology-iri $(BASE)/$@ --version-iri $(BASE)/releases/`date +%Y-%m-%d`/$@ -i $@ -o $@

$(ONT)-simple.owl: oort/subsets/cmpo.owl
	cp  $< $@ && $(ROBOT) annotate --ontology-iri $(BASE)/$@ --version-iri $(BASE)/releases/`date +%Y-%m-%d`/$@ -i $@ -o $@

$(ONT).obo: $(ONT)-simple.owl
	$(ROBOT)  annotate --ontology-iri $(BASE)/$@ --version-iri $(BASE)/releases/`date +%Y-%m-%d`/$@ -i $< filter --term obo:BFO_0000050 convert -f obo -o $(ONT).obo.tmp && mv $(ONT).obo.tmp $@ 

# ----------------------------------------
# Import modules
# ----------------------------------------
# Most ontologies are modularly constructed using portions of other ontologies
# These live in the imports/ folder
# These can be regenerated with make all_imports

IMPORTS = 
IMPORTS_OWL = $(patsubst %, imports/%_import.owl,$(IMPORTS)) $(patsubst %, imports/%_import.obo,$(IMPORTS))

# ----------------------------------------
# Release
# ----------------------------------------
# copy from staging area (this directory) to top-level
release: $(ONT).owl $(ONT).obo
	cp $^ $(RELEASEDIR) && cp imports/* $(RELEASEDIR)/imports

# ----------------------------------------
# Sparql queries: Q/C
# ----------------------------------------

# these live in the ../sparql directory, and have suffix -violation.sparql
# adding the name here will make the violation check live
VCHECKS = equivalent-classes trailing-whitespace owldef-self-reference xref-syntax nolabels inslim missingid

# run all violation checks
VQUERIES = $(foreach V,$(VCHECKS),$(SPARQLDIR)/$V-violation.sparql)
sparql_test: $(SRC)
	$(ROBOT) verify -i $< --queries $(VQUERIES) -O reports/

# ----------------------------------------
# Sparql queries: Reports
# ----------------------------------------

REPORTS = basic-report class-count-by-prefix edges xrefs obsoletes synonyms
REPORT_ARGS = $(foreach V,$(REPORTS),-s $(SPARQLDIR)/$V.sparql reports/$V.tsv)
all_reports: $(SRC)
	$(ROBOT) query -f tsv -i $< $(REPORT_ARGS)
