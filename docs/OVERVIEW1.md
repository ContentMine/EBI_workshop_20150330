# PMR thoughts in email 20150327

Current update at our end...
* Richard has built the latest Quickscrape (e.g. PLoSONE changed its web pages)
* PMR has built the latest Norma. Currently Norma transforms NLM-XML and BMC-XML to ScholarlyHTML5.
* PMR has built the latest AMI-plugin. This contains tools for
  - word frequency analysis
  - regexes
  - species
  - sequences
and
  - lookup (e.g. from Wikidata)
* RSU has put all this in a Virtual machine which will be available
* MarkMcG is putting the same functionality in the CAT-alogue system which should be available

RSU and I have "frozen" the current VM (only critical bugfixes now). However there is a mechanism for updating the VM and, since Richard is available on Tuesday, we may be able to add new functionality.

* Nick Stenning has given me some tutorial and other material on annotation. The good news is that AMI's design seems to fit very well with the Open Annotation Standard (OAF). In particular facts from XML are now addressable by Xpath (normally html:p) and prefix/postfix text.

We have potentially the following re-usable outputs:
* quickscrapes of large number of journals
* normalized Open Access full-text on a large scale
* annotations for EuropePMC content
* all the extracted Facts in the CAT. CAT is based on ElasticSearch, facets, Lucene and has an exciting visualiser in early development.

These will be available for everyone to explore. I'd suggest that participants bring their own ideas and toolkits (in any language) for linguistic/statistical/graphical/bioscientific/metadata analysis). The primary outputs from contentmine.org will be XML and JSON.

Please let me know now if there are other Norma transformers that you are interested in and other AMI-plugins. By default my trajectory beyond Monday/Tuesday will be:
* identifiers (e.g. ENA/Genbank, PDB, ATCC, accession number, ORCID, grant numbers, etc.)
* lookup
* annotations
* "bibliography and metadata" (= everything except science). Examples are bibliographic metadata (author/title.journal..), licences, grants,
* clinical trials
* chemistry

I am building these in a "dev" branch (Thx RSU). These will not be available on Monday, but might be explorable on Tuesday. These could include:
* creating OAF from AMI
* extending Sequence searching
* classification
* chemistry if Christoph drops by
* linking to Wikidata (we can do this already, but much more can be done)
* tools for openness/licensing, etc.
