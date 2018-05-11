# NLP WS (version 1.0.0)

**Natural language processing webservice for polish language**


1. [Overview](#overview)
1. [Webservice](#webservice) 
 1. [Simple query](#simple-query)
 1. [Extended query](#extended-query)
1. [Contact](#contact)


## Overview

The webservice was designed to enrich information about texts using [nlp processing](https://en.wikipedia.org/wiki/Natural_language_processing). For this purpuse we built a pipeline with the following steps:
1. [Tokenization](https://en.wikipedia.org/wiki/Lexical_analysis#Tokenization) - to split text into sentences and words
1. [Morphological analysis](https://en.wikipedia.org/wiki/Morphology_(linguistics)) - to define all grammar possibilities of a given word
1. [POS Tagging](https://en.wikipedia.org/wiki/Part-of-speech_tagging) - to disambiguate grammar categories of a given word

Our tool uses:
* grammar categories developed in [nkjp](http://nkjp.pl/) project. All grammar categories can be found in the following [book](http://nkjp.pl/settings/papers/NKJP_ksiazka.pdf)
* lexicon for morphological analysis developed in Applica company based on [polimorf](http://nlp.ipipan.waw.pl/NLP-SEMINAR/111205.pdf)

## Webservice

### Simple query

* **Url:** https://nlp.applica.pl/ams-ws-nlp/rest/nlp/simple
* **Input [application/json]:** `{"message":{"body":"Tekst do przetworzenia."},"token":"applica_token"}`
* **Output [plain/text]:** `tekst do przetworzyć .`
* **Curl:** `curl -H "Accept: application/json" -H "Content-type: application/json" -X POST -d '{"message":{"body":"Tekst do przetworzenia."},"token":"applica_token"}'  "https://nlp.applica.pl/ams-ws-nlp/rest/nlp/simple"`

### Extended query

* **Url:** https://nlp.applica.pl/ams-ws-nlp/rest/nlp/extended
* **Input [application/json]:** `{"message":{"body":"Tekst do przetworzenia."},"token":"applica_token"}`
* **Output [plain/text]:** `{"sentIdx":[1,1,1,1],"base":["tekst","do","przetworzyć","."],"cTag":["subst","prep","ger","interp"],"nps":[true,false,false,true],"orth":["Tekst","do","przetworzenia","."]}`
* **Output details:** json contains details for processed text in a format of dictionary 
 * `orth` - list of words in original form
 * `base` - list of base forms (lemma) for each word 
 * `cTag` - list of grammar categories for each word  
 * `nps` - list of flags for each word that inform, if in an original text was space before a word
 * `sentIdx` - list of sentence indexes for each word
* **Curl:** `curl -H "Accept: application/json" -H "Content-type: application/json" -X POST -d '{"message":{"body":"Tekst do przetworzenia."},"token":"applica_token"}'  "https://nlp.applica.pl/ams-ws-nlp/rest/nlp/extended"` 



## Contact

Write an email to [applica](mailto:tomasz.stanislawek@applica.ai) in case of:
* troubleshooting
* obtain applica_token 
