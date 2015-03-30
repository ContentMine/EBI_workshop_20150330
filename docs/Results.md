
# Results of running scripts

The directory structure resulting is shown below. We comment in detail on each.

## regex

This was run on the clinical trials articles:

```
├── regexexample.sh
├── regextest
│   ├── http_www.trialsjournal.com_content_16_1_1
│   ├── http_www.trialsjournal.com_content_16_1_11
│   ├── http_www.trialsjournal.com_content_16_1_12
...
│   ├── http_www.trialsjournal.com_content_16_1_2
│   └── http_www.trialsjournal.com_content_16_1_3
```
A typical directory after searching looks like
```
http_www.trialsjournal.com_content_16_1_1
├── 1745-6215-16-1-1.gif
├── fulltext.html
├── fulltext.pdf
├── fulltext.xml
├── results
│   └── regex
│       └── consort0
│           └── results.xml
├── results.json
└── scholarly.html
```
The immediate subdirectory is the output from `quickscrape->norma` and contains the fulltext files , `results.json` , and the derived `scholarly.html`. However `ami` has added a `results` directory which contains the name of the plugin used (`regex`). 
this contains the parameter (here `consort0` - derived from the regex file `regex/consort0.xml`

If there are many `regex` files, then there can be many subdirectories. The names are contained in the regex files themselves, so attention to namespace clashes is important.
```
├── results
│   └── regex
│       └── consort0
│           └── results.xml
│       └── my.regex
│           └── results.xml
│       └── your.regex
│           └── results.xml
```

## sequence

```
├── sequenceexample.sh
├── sequencetest
│   └── plosjournal.pone.0121780_sequence
```
`sequenceexample.sh` was run on the CML directory `plosjournal.pone.0121780_sequence` . This used 2 search types (`dna` and `prot`). Both results are reported, but `prot/results.xml` is empty as it didn't find any.
```
.
└── plosjournal.pone.0121780_sequence
    ├── fulltext.xml
    ├── results
    │   └── sequence
    │       ├── dna
    │       │   └── results.xml
    │       └── prot
    │           └── results.xml
    ├── results.json
    └── scholarly.html
```

## species
```
├── speciesexample.sh
├── speciestest
│   └── plosjournal.pone.0121780_sequence
```
This ran 2 species types `binomial` and `binomialsp` and produced:
```
└── plosjournal.pone.0121780_sequence
    ├── fulltext.xml
    ├── results
    │   └── species
    │       ├── binomial
    │       │   └── results.xml
    │       └── binomialsp
    │           └── results.xml
    ├── results.json
    └── scholarly.html
```
The `binomialsp` is currently empty as it's not implemented.

## words

run on 12 clinical trials articles.
```
├── wordsexample.sh
└── wordstest
    ├── http_www.trialsjournal.com_content_16_1_1
    ├── http_www.trialsjournal.com_content_16_1_11
    ...
    ├── http_www.trialsjournal.com_content_16_1_19
    ├── http_www.trialsjournal.com_content_16_1_2
    ├── http_www.trialsjournal.com_content_16_1_3
    
```
this looked for words frequencies in EACH article. Here's a typical `CMdirectory`:
```
.
├── http_www.trialsjournal.com_content_16_1_1
│   ├── 1745-6215-16-1-1.gif
│   ├── fulltext.html
│   ├── fulltext.pdf
│   ├── fulltext.xml
│   ├── results
│   │   └── word
│   │       └── frequencies
│   │           ├── results.html
│   │           └── results.xml
│   ├── results.json
│   └── scholarly.html
```
the `word` plugin has created results - besides the normal `results.xml` there is also a word-cloud-like `results.html`


 The final directory `summary` was added by `ami-words` which was asked to summarize the results into a single directory
 ```
├── wordsexample.sh
└── wordstest
    ├── http_www.trialsjournal.com_content_16_1_1
    ...
    ├── http_www.trialsjournal.com_content_16_1_3
    └── summary
```    
within which we find:
```
└── summary
    ├── booleanFrequency.html
    └── booleanFrequency.xml
```
which summarizes word frequencies in all 12 articles.
