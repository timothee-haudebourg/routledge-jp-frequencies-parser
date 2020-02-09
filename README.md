# Routledge's Japanese Frequency Dictionary parser

This repository provides a small `Ruby` script able to parse the PDF version
of "A Frequency Dictionary of Japanse" published by Routledge in 2013 and
transform the contained data into a machine-readable JSON file.

The dictionary is built from two following corpora:
the [Corpus of Spontaneous Japanese (CSJ)](https://pj.ninjal.ac.jp/corpus_center/csj/en/) and
the [Balanced Corpus of Contemporary Written Japanese (BCCWJ)](https://pj.ninjal.ac.jp/corpus_center/bccwj/en/).

The original authors of the dictionary are Yukio Tono, Makoto Yamazaki and
Kikuo Maekawa. I do not own any right on the original document (in particular
the example sentences) and hence cannot directly provide the output of this
script.

## Dependencies

The script depends on the [`romaji`](https://github.com/makimoto/romaji) gem to
translate romaji notations into katakana.
You can install it with the command `gem install romaji`.

## Usage

```
	$ pdftotext "A Frequency Dictionary of Japanese 2013.pdf" | ./routledge-frequencies > output.json
```

## Output

The output of this script is a JSON file presenting an array containing every
lemma entry of the dictionary. Here is a sample of one entry of the array:

```
{
	"lemma": [ "物" ],
	"pos": "n.",
	"forms": [ "モノ" ],
	"definitions": [ "thing, object, stuff" ],
	"frequency": 3676,
	"dispersion": 0.96,
	"samples": [
		[ "そんなに高い物は買えません。", "I can’t buy such expensive stuff." ],
	]
}
```

The `lemma` field contains the different forms of the lemma in the entry.
The `pos` field contains the associated Part of Speech of the lemma.
It can take one of the following values:

| Value   | Part Of Speech       |
|---------|----------------------|
| adn.    | adnominal            |
| adv.    | adverb               |
| aux.    | auxiliary            |
| conj.   | conjunction          |
| cp.     | compound             |
| i-adj.  | i-adjectif           |
| interj. | interjection         |
| n.      | noun                 |
| na-adj. | na-adjectif          |
| num.    | numeral              |
| p.      | particle             |
| p.case  | case particle        |
| p.conj. | conjunctive particle |
| p.disc. | discourse particle   |
| prefix  | prefix               |
| pron.   | pronoun              |
| suffix  | suffix               |
| v.      | verb                 |

The `forms` field contains the different pronunciations.
The `definitions` field contains the possibly multiple english definitions of the lemma.
The `frequency` field contains the normalized frequencies per million words.
The `dispersion` field is the dispersion value.
The `samples` contains a list of example sentences using the lemma.
Each sentence is an array where the first element is the japanese version,
and second element the english translation.
