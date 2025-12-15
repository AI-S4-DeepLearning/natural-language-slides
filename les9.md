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

# Week 5

|Week|Les A|Les B|
|-|-|-|
|Week 1|Natuurlijke taal|Parsing|
|Week 2|NLTK Basics|Feature Extraction, Vector Space Models I|
|Week 3|Bayes’ Rule, Naïve Bayes|*hemelvaart*|
|Week 4|Vector Space Models II|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|**Machine Translation**|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 9 – Machine Translation
## Putting it all together

---

# Opdracht 2

Toepassing vector space models en Locality Sensitive Hashing

## Deel I: Machine Translation

- Gradient Descent om een translation-matrix te minimaliseren
- K-Nearest Neighbour en Cosine-similarity om de output van $\mathbf{R}v$ aan een vertaling te koppelen

&nbsp;

## Deel II: Document Search

- Locality Sensitive Hashing
- Approximate K-Nearest Neighbour om beste match binnen een bucket te selecteren

---

# De Data

- `en_embeddings.p`
  - 6370 word vectors in $\mathbb{R}^{300}$
- `fr_embeddings.p`
  - 5766 word vectors in $\mathbb{R}^{300}$
- `en-fr.train.txt`

|en|fr|
|---|---|
|the|le|
|the|les|
|the|la|
|...|...|

---

# Doel

&nbsp;

$$\text{\sf cat} \xrightarrow{ \text{\sf en\_embeddings}} \mathbb{R}^{300} \xrightarrow{\mathbf{R}} \mathbb{R}^{300} \xrightarrow{\mathbf{\text{closest neighbour}}} \mathbb{R}^{300} \xrightarrow { \text { \sf fr\_embeddings} ^{-1} } \text{\sf chat}$$

&nbsp;

- Optimalisatie van matrix $\mathbf{R}$
- Best match d.m.v. KNN m.b.v LHS


---

# Frobenius Norm

- Frobenius Inner Product: Inner product voor matrices
- Twee $m\times n$ matrices naar een scalar getal

$$\langle \mathbf{A}, \mathbf{B} \rangle_F = \sum_{i=0}^m \sum_{j=0}^n \mathbf{A}_{ij} \mathbf{B}_{ij}$$

Vergelijkbaar met de Euclidean norm voor vectoren m.b.v. inner product

$$\lvert x \rvert^2 = \langle x \mid x \rangle, \quad \text{\scriptsize waar}\quad \langle a \mid b \rangle = \sum_{i=0}^m a_i b_i$$

ook een norm voor matrices m.b.v. Frobenius Inner Product

$$\lvert \mathbf{M} \rvert_F^2 = \langle \mathbf{M}, \mathbf{M} \rangle_F$$

---

# Frobenius Norm Loss

Loss functie gegeven $\mathbf{R}: \mathbb{R}^{o\times n}$ met training-data $\mathbf{X}: \mathbb{R}^{m\times o}$ en $\mathbf{Y}: \mathbb{R}^{m \times n}$ is gegeven door

$$ J(\mathbf{X}, \mathbf{Y}, \mathbf{R}) = \frac{\lvert \mathbf{X}\mathbf{R}-\mathbf{Y} \rvert_F^2}{m}$$

Minimalisatie van $J$ d.m.v. R met behulp van de gradient

$$ \frac{\partial J}{\partial \mathbf{R}} = \frac{\partial }{\partial \mathbf{R}} \frac{\lvert \mathbf{X}\mathbf{R}-\mathbf{Y} \rvert^2_F}{m} = \frac{2 \mathbf{X}^T (\mathbf{X}\mathbf{R} - \mathbf{Y})}{m}$$
