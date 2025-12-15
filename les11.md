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
layout: chaptertitle
---

# Inleveropdracht 5

## Recurrent Neural Networks

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
|Week 6|Andere Modellen en Toepassingen|**Deep Learning for NLP**|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 11 – Deep Learning for NLP
## State of the art?

---

# Neurale Netwerken
- Vaste input / output size
- Leent zich goed voor grafische problemen (vast aantal pixels) en dataframes
- Sommige problemen hebben variabele size
  - Stream input $\to$ 1 output (`fold`)
  - 1 input $\to$ stream output (`unfold`)
  - Stream input $\to$ stream output
- Voorbeelden:
  - Woorden / tokens in een tweet
  - Letters / klanken in een woord
  - Tijdsgebonden data - weer, beurs, etc.

---

# Recurrent Neural Networks

&nbsp;

<img src="rnn.svg" style="margin: auto; width: 280px;" />

---

# Unrolled

<img src="rnn-unroll.svg" style="margin: auto; width: 520px;" />

&nbsp;

$$h_t = \sigma \big( w_1 x_t + w_2 h_{t-1} + b_1 \big)$$
$$y_t = \sigma \big(w_3 h_t + b_2)$$

---

# Gradient

- Totale cost is de som over de cost per iteratie
$$J_t = \sum_{i=0}^t J_i$$

- Dit leidt tot een complexe afgeleide voor backpropagation
$$\frac{\partial J_t}{\partial \vec w} = \frac{\partial J_t}{\partial y_t} \frac{\partial y_t}{\partial h_t} \left( \sum_{i=0}^{t} \frac{\partial h_t}{\partial h_i} \frac{\partial h_i}{\partial \vec w} \right)$$

- Herhaaldelijk product $\to$ exponent
    - Vanishing Gradient
    - Exploding Gradient
- Long / short term memory of attention

---

# Internals

&nbsp;

<img src="rnn-vs-lstm.svg" style="margin: auto; width: 720px;" />

---

# LTSM (GRU, etc)

&nbsp;

<img src="lstm-vs-rnn.svg" style="margin: auto; width: 720px;" />

---
layout: image-right
image: treenet.svg
class: treenet
---

<style>
  .treenet ~ .w-full {
      background-size: 90% !important;
  }
</style>

# Recursive Neural Networks

- Recurrent NN etc gaan van links naar rechts (token stream)
- Recursive Neural Networks werken op een (binary) tree
    - Parse trees

---
layout: chaptertitle
---

# Oefenopdracht 10
## Recurrent Neural Networks
