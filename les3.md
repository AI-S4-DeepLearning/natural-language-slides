---
theme: ./slidev-theme-hu
highlighter: shiki
lineNumbers: false
info: |
  ## Natural Language Processing
  Hogeschool Utrecht<br>
  HBO-ICT Artificial Intelligence Jaar 2<br>
  Stephan van der Feest, Brian van der Bijl, 2024
fonts:
  sans: 'Avenir'
  serif: 'Roboto Slab'
  mono: 'Cascadia Mono'
drawings:
  persist: false
transition: fade
css: unocss
layout: cover
---

# Natural<br>Language<br>Processing

<subtitle><b>2023-2024 Blok D</b><br>
HBO-ICT Artificial Intelligence Jaar 2
</subtitle>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: slide-left
---

# Week 2

|Week|Les A|Les B|
|-|-|-|
|Week 1|Natuurlijke taal|Parsing|
|Week 2|**NLTK Basics**|Feature Extraction, Vector Space Models I|
|Week 3|Bayes’ Rule, Naïve Bayes|*hemelvaart*|
|Week 4|Vector Space Models II|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 3 – NLTK Basics
## Open-source Python toolkit

---

# NLTK
## Natural Language Toolkit

Installatie:
- Package `nltk` installeren
- Kan in een venv, (grote) datasets centraal downloaden

Benodigde imports voor de inleidende opgaven:

```py
import nltk                                # Python library voor NLP
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
from nltk.tokenize import RegexpTokenizer
import matplotlib.pyplot as plt            # Library voor visualisatie
import random
```

---

<style>
.third {
    display: inline-block;
    width: 32%;
}
.emoji {
    font-size: 72px;
    text-align: center;
    margin: auto;
}
.tweet {
    text-align: center;
    font-style: italic;
    width: 100%;
}
</style>

# Casus: Sentiment analysis

**Bepalen van een willekeurige tekst (e.g. Tweet): positief of negatief?**

<div class="third">
<div class="emoji">😃</div>
<div class="tweet">Brilliant effort! Loved every second of it!</div>
</div><div class="third">
<div class="emoji">😐</div>
<div class="tweet">This was okay, I guess, but I expected more.</div>
</div><div class="third">
<div class="emoji">😡</div>
<div class="tweet">Worst customer service ever! Totally dissatisfied with how I was treated!</div>
</div>

&nbsp;

- Wat is nuttige info in een Tweet?
- Hoe kan je Machine Learning gebruiken?

---

# Supervised Machine Learning

<img src="supervised.svg" style="margin: 40px auto; width: 70vw;" />

**Wat geef je als input?**

<!--
Net vers ML gehad dus zou er snel uit moeten komen
We gaan een statistisch model trainen
Input zijn de woorden, gestemmed (ref. vorige les) en voor training natuurlijk de pos/neg classificatie
Volgende les model, nu eerst de 'data cleaning' van NLP
-->

---

# Preprocessing

- Tokenizing
- Lowercasing
- Stop words en interpunctie verwijderen
- Stemming

- Gebruik regular expressions, `re` library<br>
    Voorbeeld, hyperlinks verwijderen:
    ```py
    tweet = re.sub(r'https?://[^\s\n\r]+', '', tweet)
    ```

- Tokenizing in NLTK met regular expressions

    ```py
    from nltk.tokenize import RegexpTokenizer
    RegexpTokenizer(r'\w+|\$[\d\.]+|\S+')
    -> ['This', 'is', 'an', 'example', '.']
    ```

---
layout: chaptertitle
---

# Inleidende opdracht 1

## Cleaning & Tagging

---
layout: image-right
image: homer.webp
---

# Cleaning & Tagging

- We gaan toewerken naar een classifier voor zinnen die uit verschillende teksten afkomstig zijn.
- In de opdrachten gaat dit om 2 teksten:
  - De Ilias
  - De Odyssee
- Oud-Griekse teksten (Engels vertaald) van dezelfde auteur (as far as we know)
- Beschikbaar van Project Gutenberg
- Aan de hand van woordfrequenties voorspellen in welke tekst een zin thuis hoort
- Vergelijkbaar met sentiment analysis
- Eerste opdracht: data cleaning

---
layout: image-right
image: iliad.jpg
---

# Processing

- Inlezen teksten
  - Verwijderen preamble and postscript

<v-click>

- Splitsen in zinnen <v-click> - **hoe?** </v-click>

</v-click>
<v-click>

- Per zin, splitsen in woorden
  - `RegexpTokenizer`

</v-click>
<v-click>

- Verwijder stopwords (`nltk.corpus`) en interpunctie (`string`)

</v-click>
<v-click>

- Lowercase en stem
  - `PorterStemmer`

</v-click>
<v-click>

- Frequency Dictionary
  - Per $\text{woord} \times \text{tekst}$, hoevaak komt het woord in de tekst voor?
  - Scatterplot selectie woordfrequenties

</v-click>
