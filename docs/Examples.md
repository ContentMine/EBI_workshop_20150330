# Example material
There is a tutorial for `ami` in https://bitbucket.org/petermr/norma/downloads/tutorial.tar. Untar this ('tar -xvf tutorial.tar`)
It consists of
## examples
This is a directory (`examples`) containing 12 CM directories for clinical trials from BMC
## examples2
A directory (`examples2`) containing 1 directory for a PLoSONE article containing both sequences and species.

## scripts

These scripts can all be run by `sh sequenceexample.sh` or similar. They create local directories (e.g. `sequencetest`
with the results.

### sequences 
see `sequenceexample.sh`

#! /bin/sh

rm -rf sequencetest
cp -r examples2 sequencetest
ami2-sequence --sq.sequence --sq.length "{6,20}" --context 35 50 --sq.type dna prot -q sequencetest/plosjournal.pone.0121780_sequence -i scholarly.html
