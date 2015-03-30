# results.xml

The results from `ami` normally appear in `results.xml` in a hierarchy something like:
```
├── http_www.trialsjournal.com_content_16_1_3
│   ├── fulltext.html
│   ├── fulltext.pdf
│   ├── fulltext.xml
│   ├── results
│   │   └── word
│   │       └── frequencies
│   │           ├── results.html
│   │           └── results.xml
│   │   └── foo
│   │       └── bar
│   │           └── results.xml

```
The format of `results.xml` is still evolving, but here are examples:

## species

We searched for all `italic` spans and within those used the `regex` for binomial species names ("Homo sapiens"). Here's a typical result:
```
<?xml version="1.0" encoding="UTF-8"?>
<results title="binomial">
 <result pre="ntimicrobial activity (assessed on " wikipedia="3761158" match="Vibrio harveyi" post=" cultures) was limited in both H an"/>
 <result pre="ia genus Vibrio, including; " match="Vibrio harveyi" post=" [ [14]], V. mediterranei [ "/>
 <result pre="luding; V. harveyi [ [14]], " match="Vibrio mediterranei" post=" [ [7]], V. owensii [ [15]] "/>
 <result pre="]], V. mediterranei [ [7]], " match="Vibrio owensii" post=" [ [15]] and V. coralliilyticus&lt;"/>
 <result pre="7]], V. owensii [ [15]] and " match="Vibrio coralliilyticus" post=" [ [10]]. Furthermore, Piskorska, S"/>
 <result pre="ith [ [7]], reports an increase in " match="Vibrio mediterranei" post=" in the mucus of WS-affected Ech"/>
 <result pre="ei in the mucus of WS-affected " wikipedia="3941556" match="Echinopora lamellosa" post=", compared to healthy samples. Howe"/>
 <result pre="iated with healthy and WS-affected " match="Echinopora lamellosa" post=", an approach that can lead to phyl"/>
 <result pre="ve a dominant presence in diseased " match="A. muricata" post=" samples in a study screening the m"/>
 <result pre="eet and Bythell [ [18]] also found " match="Vibrio harveyi" post=" to increase in diseased samples, b"/>
 ```
For each hit there is the direct `match` (the characters that matched the regex) surrounded by the  `pre`fix text and 
`post`fix text (the immediate context of the match). In some cases the match was abbreviated (e.g. "V. harveyi"
