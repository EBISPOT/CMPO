CMPO
====

The Cellular Microscopy Phenotype Ontology (CMPO) is a species neutral ontology for describing general phenotypic observations relating to the whole cell, cellular components, cellular processes and cell populations. CMPO is an application ontology developed in OWL that contains precomposed phenotypes descriptions that are defined using the Gene Ontology (GO) and the Phenotype Trait Ontology (PATO).

Files
=====

release/cmpo.obo A simple OBO formatted released of CMPO
release/cmpo-simple.owl A simple OWL formatted version of CMPO, pre-reasoned and exludes logical axioms. 
release/cmpo.owl An OWL formatted version of CMPO, pre-reasoned and includes logial axioms. (GO/PATO terms imported using MIREOT)
src/cmpo.owl This is the source file for CMPO editors. It includes all logical axioms and imports the Gene Ontology and PATO. (NOTE: If you unpack the imports.tar.gz file and open cmpo.owl in Protege, the Protege will import GO and PATO from your file system rather than pulling form the web)
