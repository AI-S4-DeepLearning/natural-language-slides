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

# Week 6

|Week|Les A|Les B|
|-|-|-|
|Week 1|Natuurlijke taal|Parsing|
|Week 2|NLTK Basics|Feature Extraction, Vector Space Models I|
|Week 3|Bayes’ Rule, Naïve Bayes|*hemelvaart*|
|Week 4|Vector Space Models II|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|**Andere Modellen en Toepassingen**|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 10 – Andere Modellen en Toepassingen
## Variaties op Vector Spaces

---

# Transfer Learning in NLP

- Common theme in machine learning / deep learning:
  - Train model op probleem A
  - Pas toe op probleem B
- Ook wel "pre-training"
- Bijvoorbeeld:
  - Train model op next / masked word prediction
  - Toepassing op semantic modelling en analogy
- 1 data representatie, 2 toepassingen
- Stapje verder: 2 soorten data in 1 representatie

---

# Shared Representations - Bilingual Vector 

<img src="bilingual.png" style="margin: 40px auto; width: 36vw" />

*Source: Socher et al. (2013)*

---

# Shared Representations - Text + Image

<img src="ImageClassManifold.png" style="margin: 40px auto; width: 36vw; filter: invert(93%)" />

*Source: Socher et al. (2013)*

---
layout: chaptertitle
---

# Vectoren combineren

---

# Addition en Hadamard Product

$$\overrightarrow{\textsf{red\_dog}} = \overrightarrow{\textsf{red}} + \overrightarrow{\textsf{dog}}$$

- Baseline
- Annoyingly hard to beat
- Werkt als OR gate
  - Saturation
- Commutative

$$\overrightarrow{\textsf{red\_dog}} = \overrightarrow{\textsf{red}} \odot \overrightarrow{\textsf{dog}}$$

- Werkt als AND gate
  - Sparsity
- Commutative

---

# Commutativity

$$\overrightarrow{\textsf{man}} + \overrightarrow{\textsf{bites}} + \overrightarrow{\textsf{dog}} = 
\overrightarrow{\textsf{dog}} + \overrightarrow{\textsf{bites}} + \overrightarrow{\textsf{man}}$$

- Alternatief: matrices en tensoren

$$(\mathbf{Bites}\ \overrightarrow{man})\ \overrightarrow{dog} \neq (\mathbf{Bites}\ \overrightarrow{dog})\ \overrightarrow{man}$$

- Grammatica als input
- Parse Trees
- Polysemy

- DISSECT toolkit

---

# Higher Order Objecten

- Noun: $\mathbb{R}^n$ (persoon)

- Adjective: $\mathbb{R}^{n\times n}$ (rood/rode)

- Verb: $\mathbb{R}^{n\times n}$ (loopt)
  - of $\mathbb{R}^{n\times n \times n}$ (ziet)
  - of $\mathbb{R}^{n\times n \times n \times n}$ (geeft)

## Meerdere / verschillende spaces

- Ziet: $\mathbb{R}^{s\times n \times n}$
  - Onderwerp en Lijdend voorwerp in Noun-space
  - Resultaat in sentence space

**$M : \mathbb{R}^{n\times n}$ kan gezien worden als $M : \mathbb{R}^n \to \mathbb{R}^n$, maar ook als $M : \mathbb{R}^n \to \mathbb{R}^n \to \mathbb{R}$. Voor de tweede deelopdracht gebruiken we de matrix in die vorm: $\langle a \mid \mathbf{M} \mid b \rangle$.**

---
layout: chaptertitle
---

# Oefenopdracht 9
## Andere modellen

---

# Andere Toepassingen van NLP

Bijvoorbeeld:
- Analogy
- Autocomplete
- Text generation
- Named entity recognition
- Automatic summary generation
- Conversation bots
