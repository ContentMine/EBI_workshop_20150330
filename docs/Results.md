
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
A typical directory looks like
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

```
├── sequenceexample.sh
├── sequencetest
│   └── plosjournal.pone.0121780_sequence
├── speciesexample.sh
├── speciestest
│   └── plosjournal.pone.0121780_sequence
├── wordsexample.sh
└── wordstest
    ├── http_www.trialsjournal.com_content_16_1_1
    ├── http_www.trialsjournal.com_content_16_1_11
    ├── http_www.trialsjournal.com_content_16_1_12
    ├── http_www.trialsjournal.com_content_16_1_13
    ├── http_www.trialsjournal.com_content_16_1_14
    ├── http_www.trialsjournal.com_content_16_1_15
    ├── http_www.trialsjournal.com_content_16_1_16
    ├── http_www.trialsjournal.com_content_16_1_17
    ├── http_www.trialsjournal.com_content_16_1_18
    ├── http_www.trialsjournal.com_content_16_1_19
    ├── http_www.trialsjournal.com_content_16_1_2
    ├── http_www.trialsjournal.com_content_16_1_3
    └── summary
    
```

