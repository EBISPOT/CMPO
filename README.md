CMPO
====

The Cellular Microscopy Phenotype Ontology (CMPO) is a species-neutral ontology for describing general phenotypic observations relating to the whole cell, cellular components, cellular processes and cell populations. CMPO is an application ontology developed in OWL that contains precomposed phenotypes descriptions that are defined using the Gene Ontology (GO) and the Phenotype Trait Ontology (PATO).

For more information see the CMPO website at http://www.ebi.ac.uk/cmpo

CMPO is avilable for download from the following URLs  

* http://www.ebi.ac.uk/cmpo/cmpo.owl
* http://www.ebi.ac.uk/cmpo/cmpo-simple.owl - without axioms referening to external ontologies
* http://www.ebi.ac.uk/cmpo/cmpo.obo - OBO formatted file

### Contact ###

Simon Jupp <jupp@abi.ac.uk>
Gabriella Rustici <gr231@cam.ac.uk>

### Licence ###

Apache License, version 2.0. 

### GitHub Files ###

* __release/cmpo.obo__ 
 * A simple OBO formatted released of CMPO
* __release/cmpo-simple.owl__ 
 * A simple OWL formatted version of CMPO, pre-reasoned and exludes logical axioms. 
* __release/cmpo.owl__ 
 * An OWL formatted version of CMPO, pre-reasoned and includes logial axioms. (GO/PATO terms imported using MIREOT)
* __src/cmpo.owl__ 
 * This is the source file for CMPO editors. It includes all logical axioms and imports the Gene Ontology and PATO. (NOTE: If you unpack the imports.tar.gz file and open cmpo.owl in Protege, the Protege will import GO and PATO from your file system rather than pulling form the web)
