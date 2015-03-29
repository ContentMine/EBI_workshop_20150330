# Example material
There is a tutorial for `ami` in https://bitbucket.org/petermr/norma/downloads/tutorial.tar. Untar this (`tar -xvf tutorial.tar`)
It consists of
```
examples		regex			sequenceexample.sh	wordsexample.sh examples2		regexexample.sh		speciesexample.sh
```

## contentmine (CM) directories

These directories each hold the material (raw and derived) for a single article. A typical structure is:
```
plosjournal.pone.0121780_sequence/
fulltext.xml	results.json	scholarly.html
```
i.e. this directory contains the scraped XML (`fulltext.xml`), the metadata for the scrape (`results.json`) and the `norma`-transformed result (`scholarly.html`) which is what `ami` uses. `ami` results will go directly into this directory,
henceforce called a `CM` directory.

## examples

This is a directory (`examples`) containing 12 CM directories for clinical trials from BMC
```
http_www.trialsjournal.com_content_16_1_1	   http_www.trialsjournal.com_content_16_1_16
http_www.trialsjournal.com_content_16_1_11	 http_www.trialsjournal.com_content_16_1_17
http_www.trialsjournal.com_content_16_1_12	 http_www.trialsjournal.com_content_16_1_18
http_www.trialsjournal.com_content_16_1_13	 http_www.trialsjournal.com_content_16_1_19
http_www.trialsjournal.com_content_16_1_14	 http_www.trialsjournal.com_content_16_1_2
http_www.trialsjournal.com_content_16_1_15	 http_www.trialsjournal.com_content_16_1_3
```

## examples2

A directory (`examples2`) containing 1 directory for a PLoSONE article (`plosjournal.pone.0121780_sequence`) containing both sequences and species.

## regex

There's a directory of regexes:
```
├── regex
│   ├── agriculture.xml
│   ├── astrophys.xml
│   ├── common.xml
│   ├── commonnew.xml
│   ├── consort0.xml
│   ├── ebola.xml
│   ├── figure.xml
│   ├── genbank.xml
│   ├── metadata.xml
│   ├── pdb.xml
│   ├── phylotree.xml
│   ├── publication.xml
│   └── simpletest.xml
```
and a script to run `ami2-regex` which we'll look at later:
```
├── regexexample.sh
```

## scripts

These scripts can all be run by `sh sequenceexample.sh` or similar. They create local directories (e.g. `sequencetest`)
with the results.

###  `regexexample.sh`

runs `ami2-regex` . Some of the script is to output context

```
# prints help
echo "==================regex================"
echo
echo help 
echo
ami2-regex
echo
rm -rf regextest/
cp -R examples/ regextest
echo
echo "running regex on regextest"
echo
ami2-regex -q regextest/ --context 25 40 --r.regex regex/consort0.xml 
echo
echo "results in QSN"
echo
ls -ltR regextest/*/results/regex/consort0/
echo
```
but the prime command is
```
ami2-regex -q regextest/ --context 25 40 --r.regex regex/consort0.xml 
```

###  `sequenceexample.sh`
```
#! /bin/sh

rm -rf sequencetest
cp -r examples2 sequencetest
ami2-sequence --sq.sequence --sq.length "{6,20}" --context 35 50 --sq.type dna prot \
    -q sequencetest/plosjournal.pone.0121780_sequence -i scholarly.html
```

###  `speciesexample.sh`
```
#!/bin/sh

rm -rf speciestest
cp -r examples2 speciestest
ami2-species --sp.species --context 35 --sp.type binomial binomialsp -q speciestest/plosjournal.pone.0121780_sequence \
   -i scholarly.html --lookup wikipedia

```
###  `wordsexample.sh`
```
#!/bin/sh

rm -rf speciestest
cp -r examples2 speciestest
ami2-species --sp.species --context 35 --sp.type binomial binomialsp -q speciestest/plosjournal.pone.0121780_sequence -i scholarly.html --lookup wikipedia
localhost:tutorial pm286$ more wordsexample.sh 
#!/bin/sh

# example 1
# prints help (no arguments)
echo "==================words================"
echo
echo help 
echo
ami2-words
echo

# example 1
# runs ami-words on a small number of files 
# for tutorials we copy the files to a temporary directory so as not to overwrite them by mistake
# this calculates the frequencies of words
rm -rf wordstest/
cp -R examples/ wordstest
echo
echo "==========running ami2-words to get frequencies"
echo
ami2-words -q wordstest/ --w.words wordFrequencies  
echo
echo "results in QSN"
echo
# the results are written into the directories
# thus wordstest/http_www.trialsjournal.com_content_16_1_19/ should have a new directory
# http_www.trialsjournal.com_content_16_1_19/results/word/frequencies which will contain
#   results.xml (machine-readable)
#   results.html (human-readable)
# inspect http_www.trialsjournal.com_content_16_1_19/results/word/frequencies/results.html for a word cloud
# and list all the files we have produced
ls -ltR wordstest/*/results/word/frequencies
echo
rm -rf wordstest/
cp -R examples/ wordstest
echo
echo "==========running ami2-words to get summary frequencies"
echo
echo "there are a number of options here..."
echo "--w.stopwords applies lists of words to be omitted from the analysis"
echo "    stopwords.txt is a list of 335 common english words"
echo "    clinicaltrials200.txt is a list of the 200 next commonest words we found in trialsjournal.com"
echo "--w.case ignore  will ignore case"
echo "--w.summary denotes the concept to summarise on (boolean Frequency = 1 if word is in a document, else 0)"
echo "--summaryfile the directory to summarize in"
echo "--w.mincount frequencies below this will be ignored (not sure it's working yet)"
echo
ami2-words \
-q wordstest/ --w.words wordFrequencies  \
--w.stopwords \
  /org/xmlcml/ami2/plugins/word/stopwords.txt \
  /org/xmlcml/ami2/plugins/word/clinicaltrials200.txt \
--w.case ignore \
--w.summary booleanFrequency \
--summaryfile wordstest/summary \
--w.mincount 3
echo
echo "results are written to each results/words/frequencies/ directory and to the summaryfile"
echo
# the results are written into the directories
# thus target/wordstest/http_www.trialsjournal.com_content_16_1_19/ should have a new directory
# http_www.trialsjournal.com_content_16_1_19/results/word/frequencies which will contain
#   results.xml (machine-readable)
#   results.html (human-readable)
# inspect http_www.trialsjournal.com_content_16_1_19/results/word/frequencies/results.html for a word cloud
# and list all the files we have produced
ls -ltR wordstest/*/results/word/frequencies
echo
```
