---
# try also 'default' to start simple
theme: ./slidev-theme-hu
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Template for HU.

  Learn more at [Sli.dev](https://sli.dev)
fonts:
  sans: 'Avenir'
  serif: 'Roboto Slab'
  mono: 'Iosevka'
# persist drawings in exports and build
drawings:
  persist: false
# page transition
transition: fade-out
# use UnoCSS
css: unocss
themeConfig:
  paginationX: r
  paginationY: t
  paginationPagesDisabled: [1]
layout: cover
---

<link rel="stylesheet" type="text/css" href="s4.css" />

# AI-S4 Deep Learning
## Natural Language Processing

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: chaptertitle
---

# [NLP-1] Taal en Parsing

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
layout: image-left
image: speech.jpg
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
transition: none
layout: image-right
image: ontleden.jpg
---

# Syntax: Ontleden

Wat weten jullie nog?
- Redekundig (zin ontleden) $\to$ semantiek
- Taalkundig ontleden (woordsoorten) $\to$ syntax

&nbsp;

***"Kees riep zijn moeder."***

<v-clicks>

- Onderwerp?
- Gezegde?
- Lijdend voorwerp?

</v-clicks>

---
layout: image-right
image: ontleden.jpg
---

# Syntax: Ontleden

Wat weten jullie nog?
- *Redekundig (zin ontleden) $\to$ semantiek*
- Taalkundig ontleden (woordsoorten) $\to$ syntax

&nbsp;

***"Kees riep zijn moeder."***

- Onderwerp? &nbsp; **Kees**
- Gezegde? &nbsp; **riep**
- Lijdend voorwerp? &nbsp; **zijn moeder**

---
layout: image-right
image: tree.webp
---

# Syntax trees

Wat weten jullie nog?
- Redekundig (zin ontleden) $\to$ semantiek
- *Taalkundig ontleden (woordsoorten) $\to$ syntax*

&nbsp;

***"Kees riep zijn moeder."***

<br>

<img src="/ontleden.svg" style="width: 250px;" />

---

# Semantiek - Betekenis

*"Colourless green ideas sleep furiously." &mdash; Noam Chomsky*

<img src="/chomsky.svg" style="width: 450px;" />

---
layout: image
image: groucho.jpg
---

# Ambiguiteit

---
layout: center
---

# Ontleed dit eens:

*"I saw the man on the hill with the telescope"*

<!--
Op bord; klassikaal, evt. aanvullen. Voorbeeld parse trees in telescope.pdf.
-->

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

---
layout: image-right
image: ./data.jpeg
---

# Parsing van gestructureerde data

- Parsen = ontleden
- Zowel voor natuurlijke taal als voor formele talen
  - Gestructureerde data
  - Lexical Tokenisation
  - Abstract Syntax Trees
    - `ast` in Python

- Voorbeeld: paren van haakjes tellen

<v-clicks>

- Iets moeilijker: JSON
- Hoe is dit moeilijker? Wat is anders?
- Zelf proberen

</v-clicks>

<!--
ast libraty in Pyhton:

```pyhton
import ast
print(ast.dump(ast.parse('[(lambda x: x * 2)(y) for y in range(10)]', mode='single'), indent=4))
```

Klassikaal basis handelingen bedenken, dan naar oefenopgave, eerste deel maken
-->

---
layout: chaptertitle
---

# Oefenopdracht 3

## Parsing van code vs. taal

---
layout: image-right
image: ./language.jpg
---

# Parsing van natuurlijke taal

Hoe zou je een algoritme dit laten doen?<br><br>

***"Kees riep zijn moeder."***

<br>

<img src="/ontleden.svg" style="width: 250px;" />

<!--
Klassikaal discussie richting tokenizing en leiden naar stemming
-->

---
layout: image-left
image: ./ugh.jpg
---

# Uitdagingen bij natuurlijke taal

<v-clicks>

- Woord-functie minder herkenbaar
  - JSON: quotes $\to$ string of identifier
  - Nederlands: -en is zelfstandig meervoud? werkwoord? ...?

- Woordenlijsten
  - Hoe om te gaan met:
    - Woorden met meerdere functies
    - Verschijningsvormen van hetzelfde woord

- Capitalisatie
    - Mees vs mees, Ben vs ben

</v-clicks>

---
layout: chaptertitle
---

# [NLP-2] Vector Embeddings

