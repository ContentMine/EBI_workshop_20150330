# Example material
There is a tutorial for `ami` in https://bitbucket.org/petermr/norma/downloads/tutorial.tar. Untar this (`tar -xvf tutorial.tar`)
It consists of
```
examples		regex			sequenceexample.sh	wordsexample.sh examples2		regexexample.sh		speciesexample.sh
```
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

A directory (`examples2`) containing 1 directory for a PLoSONE article containing both sequences and species.

## scripts

These scripts can all be run by `sh sequenceexample.sh` or similar. They create local directories (e.g. `sequencetest`)
with the results.

###  `regexexample.sh`
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
#! /bin/sh

rm -rf sequencetest
cp -r examples2 sequencetest
ami2-sequence --sq.sequence --sq.length "{6,20}" --context 35 50 --sq.type dna prot \
    -q sequencetest/plosjournal.pone.0121780_sequence -i scholarly.html
```
