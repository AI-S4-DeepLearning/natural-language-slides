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

# Week 1

| | | |
|-|-|-|
|Week 1|Natuurlijke taal|**Parsing**|
|Week 2|NLTK Basics|Feature Extraction, Vector Space Models I|
|Week 3|Bayes’ Rule, Naïve Bayes|*hemelvaart*|
|Week 4|Vector Space Models II|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 2 – Parsing
## Van taal naar data

---
layout: image-right
image: public/data.jpeg
---

# Parsing van gestructureerde data

- Parsen = ontleden
- Zowel voor natuurlijke taal als voor formele talen
  - Gestructureerde data
- Voorbeeld: paren van haakjes tellen

<v-clicks>

- Iets moeilijker: JSON
- Hoe is dit moeilijker? Wat is anders?
- Zelf proberen

</v-clicks>

<!--
Klassikaal basis handelingen bedenken, dan naar oefenopgave, eerste deel maken
-->

---
layout: chaptertitle
---

# Oefenopdracht 3

## Parsing van code vs. taal

---
layout: image-left
image: public/python.jpg
---

# Parsing: Regular Expressions

- Regex

```
/grey|gray/
/gr(e|a)y/
/kw[iea]k/
/colou?r/
/go*gle/
/go+gle/
```

<v-click>

- Parse een e-mail adres
```
/[a-z0-9]+@[a-z]+\.[a-z]{2,3}/
```

&nbsp;

</v-click>
<v-click>

- Lexical Tokenisation
- Abstract Syntax Trees

</v-click>

<!--
Introduceren regex indien nog niet aan de orde geweest
Zelf proberen in de les d.m.v. verder werken aan oefenopgave
-->

---
layout: image-right
image: public/language.jpg
---

# Parsing van natuurlijke taal

Hoe zou je een algoritme dit laten doen?<br><br>

***"Kees riep zijn moeder."***

<br>

<img src="ontleden.svg" style="width: 250px;" />

<!--
Klassikaal discussie richting tokenizing en leiden naar stemming
-->

---
layout: image-left
image: public/ugh.jpg
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
layout: image-right
image: public/stem.jpg
---

# Stemming

- Reductie van ruis, behoudt (zoveel mogelijk) informatie
- Met of zonder woordenboek
- Bijvoorbeeld: -s, -ing, -ed

&nbsp;

<v-click>

## Mixed results
- Hoofden $\to$ hoofd <span style="color:#0f0">&check;</span>
- Lopen $\to$ lop <span style="color:red">&cross;</span>
- Kinderen, kinderlijk $\to$ kinder <span style="color:yellow">?</span>

</v-click>

<!--
Proefje doen met een stuk voorbeeldtekst met correcte stemming erbij geleverd:
Meten hoeveel woorden correct lukken en welke er mis gaan
Bruggetje naar libraries, volgende les NLTK
Rest van de les verder werken aan oefenopgave
-->
