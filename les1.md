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
  sans: Avenir
  serif: Roboto Slab
  mono: Cascadia Mono
drawings:
  persist: false
transition: fade
css: unocss
layout: cover
title: Natural<br>Language<br>Processing
---

# Natural<br>Language<br>Processing

<subtitle><b>2023-2024 Blok D</b><br>
HBO-ICT Artificial Intelligence Jaar 2
</subtitle>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)

Extra commentaar
-->

---
layout: image-right
image: intro-illustration.png
---

# Introductie NLP

Voorbeelden gebruik:
- Sentiment analysis
- Analogy
- Machine translation
- Autocomplete
- Text generation
- Named entity recognition
- Automatic summary generation
- Conversation bots

<Footnotes separator>
  <Footnote>Foto: Stable Diffusion: <i>“a photograph of two foreign exchange students trying<br>to have a conversation, daytime, outside”</i>
</Footnote>
</Footnotes>

---
transition: slide-left
---

# Introductie NLP
## Vakinhoud

| | | |
|-|-|-|
|Week 1|**Natuurlijke taal**|Parsing|
|Week 2|NLTK Basics|Feature Extraction, Vector Space Models I|
|Week 3|Bayes’ Rule, Naïve Bayes|*hemelvaart*|
|Week 4|Vector Space Models II|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
transition: slide-left
---

# Toetsing

| | | |
|-|-|-|
|Cleaning & Counting|26 april||
|Logistic Regression & Naive Bayes|10 mei||
|Vector Space Models & PCA|24 mei|40%|
|Machine Translation|31 mei|40%|
|Modern Network Architectures|14 juni|20%|

---
layout: chaptertitle
---

# Les 1 – Natuurlijke taal
## Wat weten jullie al/nog?

---

# Natuurlijke taal

- Context, interpretatie
- Beste voorbeeld: Ambiguïteit (Dubbelzinnigheid):
  - *"De man slaat de hond met de stok."*
  - *"Er is niemand die Bart leuk vindt."*
  - *"We zijn tegenwoordig met steeds minder tevreden."*
  - *"Mijn dochter is gelukkig getrouwd."*
  - *"De kip is klaar om te eten."*
  - *"De vrouw die de man behandeld heeft."*
  - *"Nergens is meer onrecht te zien."*<br>
  of nog erger:
  - *"Hij belooft zijn vrouw elke dag te bellen."*

<v-click>

Vraag: Welke van deze zinnen zijn **ook in het Engels** ambigu?

</v-click>

---

# Natuurlijke taal

- Syntax
  - Grammatica
  - Wat is een geldige zin?
  - Hoe maak je een geldige zin?
  - Ontleden
- Semantiek
  - Betekenis
  - Is een geldige zin betekenisvol?
  - Waarheid van zinnen
- Ambiguiteit

---

# Syntax: Ontleden

Wat weten jullie nog?<br><br>

<v-click>

***"Kees riep zijn moeder."***

</v-click>
<v-clicks>

- Onderwerp?
- Gezegde?
- Lijdend voorwerp?

</v-clicks>

---

# Syntax: Ontleden

Wat weten jullie nog?<br><br>

***"Kees riep zijn moeder."***

- Onderwerp? &nbsp; **Kees**
- Gezegde? &nbsp; **riep**
- Lijdend voorwerp? &nbsp; **zijn moeder**

---

# Syntax trees

Wat weten jullie nog?<br><br>

***"Kees riep zijn moeder."***

<br>

<img src="ontleden.svg" style="width: 250px;" />

---

# Semantiek - Betekenis

*"Colourless green ideas sleep furiously." &mdash; Noam Chomsky*

<img src="chomsky.svg" style="width: 450px;" />

---
layout: center
---

# Ontleed dit eens:

*"I saw the man on the hill with the telescope"*

---
layout: chaptertitle
---

# Oefenopdracht 1

## Ontleden, symboliek en context

---

# Taaldetectie

Welke taal is deze zin?<br><br>

<v-clicks>

- Aantal tekenbeten vorig jaar flink teruggelopen.
- It must be five o'clock somewhere.
- Ecoutez-nous, je vous en prie.
- At that moment she realized she had a sixth sense.
- Waar kunnen we de uitgang vinden?
- De hond kauwt op zijn bot.
- He told us a very exciting adventure story.
- Wie _____ _____ __ _____ in _________?
- Wie lange lebst du schon in Stuttgart?


</v-clicks>

---
layout: chaptertitle
---

# Oefenopdracht 2

## Taalherkenning

<!--
Inschatten hoe lang dit kost: Misschien les 1 en 2 nog samenvoegen?
-->
