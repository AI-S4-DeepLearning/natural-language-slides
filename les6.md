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

<style>
.gridspace {
  background-size: 60% !important;
  background-position: -20% 15% !important;
}

.gridspace p {
  font-size: 1.1rem;
  margin-left: 24vw;
}

.gridspace h2, .gridspace h3 {
  margin-left: 24vw;
}

.gridspace h1 {
  padding-bottom: 36px;
}
</style>

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

# Week 4

|Week|Les A|Les B|
|-|-|-|
|Week 1|Natuurlijke taal|Parsing|
|Week 2|NLTK Basics|Feature Extraction, Vector Space Models I|
|Week 3|Bayes’ Rule, Naïve Bayes|*hemelvaart*|
|Week 4|**Vector Space Models II**|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 6 – Vector Space Models II
## Multidimensional classification

---

# Doel: Vector Space Models

<img src="embedding.png" style="margin: 40px auto; height: 75%; filter: invert(93%)" />

*Source: https://miro.medium.com/max/1400/1*sAJdxEsDjsPMioHyzlN3_A.png*

---
layout: image
image: "metric.svg"
class: gridspace
---

# Metrics

***Hoe vinden we de afstand tussen twee vectoren?***

---
layout: image
image: "metric2.svg"
class: gridspace
---

# Metrics - Euclidean Norm

$$\begin{align*}
\lvert v - u \rvert
&= \sqrt{ \langle v - u \mid v - u \rangle } \\
&= \sqrt { 2 - -2 \times 2 - -2 + 2 - -1 \times 2 - -1 } \\
&= \sqrt { 4^2 + 3^2 } \\
&= 5
\end{align*}$$

Whatabout $\lvert u - v\rvert$  ?

---
layout: image
image: "metric3.svg"
class: gridspace
---

# Metrics - Cosine Similarity

$$\langle u\mid v \rangle
=\lvert u\vert \vert v\vert \cos\theta$$

$$S_C (A,B):= \cos(\theta) = {\langle u \mid v \rangle \over \lvert u\rvert \ \lvert v\rvert}
= \frac{ \langle u \mid v \rangle }{\sqrt{ \langle u \mid u \rangle \langle v \mid v \rangle }}$$

---
layout: chaptertitle
---

# Oefenopdracht 5

## Vector Maths Recap

---

# Dimensionality Reduction

- Terugbrengen van meer naar minder dimensies
- Van 100000 (cooccurrence) naar 500 (embeddings)
- Van 500 (embeddings) naar 2-3 (plots)
- Singular Value Decomposition
- Principal Component Analysis
- Volgende les!

---
layout: chaptertitle
---

# Vector Space Models

---

# Doel: Vector Space Models

<img src="embedding.png" style="margin: 40px auto; height: 75%; filter: invert(93%)" />

*Source: https://miro.medium.com/max/1400/1*sAJdxEsDjsPMioHyzlN3_A.png*

---

# Vector Space Models

- Word2Vec
- GloVe
- Tensor Based Models (DisCoCat)

&nbsp;

- Handmatig **(oefenopdracht)**
- PCA op count / cooccurrence matrix
- Neurale netwerken
  - Local (Word2Vec Skip-gram / Bag-of-words)
  - Global (GloVe)

---
layout: image-right
image: count.jpg
---

# How to get there: Counting

- Idee: capture semantische relaties
  - Gelijkende woorden $\Leftrightarrow$ gelijkende vectoren
  - Komen woorden voor in dezelfde context?

- Plan
  - Geef elk woord een index $0..n$
  - Maak een lege $n\times n$ cooccurence matrix
  - Doorloop corpus (sliding window), vul matrix
  - Reduceer dimensionaliteit

- Keuzes
  - Stemming of niet?
  - Window size
  - Volgorde belangrijk?

---

# Counting: Voorbeeld

**Time flies like an arrow, fruit flies like a banana** (symmetric window, size 1)

| | time | flies | like | arrow | fruit | banana |
| --- | --- | --- | --- | --- | --- | --- |
| time | | 1 | | | | |
| flies | 1 | | 2 | | 1 | |
| like | | 2 | | 1 | | 1 |
| arrow | | | 1 | | 1 | |
| fruit | | 1 | | 1 | | |
| banana | | | 1 | | | |

---

# Counting: Voorbeeld

$C = \begin{bmatrix}
0 & 1 & 0 & 0 & 0 & 0 \\
1 & 0 & 2 & 0 & 1 & 0 \\
0 & 2 & 0 & 1 & 0 & 1 \\
0 & 0 & 1 & 0 & 1 & 0 \\
0 & 1 & 0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 & 0 & 0 \\
\end{bmatrix} \quad \text{Na reductie: } \quad V \approx \begin{bmatrix}
-0.597 & -0.513 \\
 1.718 &  0.700 \\
-1.718 &  0.700 \\
 0.914 & -0.188 \\
-0.914 & -0.188 \\
 0.597 & -0.513 \\
\end{bmatrix}$

<div style="height: 2vh" />

**Iedere rij staat voor een word-embedding:**

<div style="height: 2vh" />

Time heeft de vector 
$\vec v = \begin{bmatrix}
-0.597 \\ -0.513
\end{bmatrix}$ gekregen


---
layout: image-right
image: predict.jpg
---

# How to get there: Predicting

- One hot encoding van data

- Gegeven een woord, voorspel ander woord
  - CBOW: gegeven context, voorspel woord
  - Skip-gram: gegeven woord, voorspel context

<div style="height: 2vh" />

- Sliding window (geparameteriseerd op size)
  - Lijst van tuples `:: [(Target, Context)]`
  - Voorbeeld (Continuous bag of words, size 2):

**Time flies like an arrow, fruit flies like a banana** $\to$

`[(time, flies), (flies, time), (time, like), (like, time), (flies, like), ..]`

---

# Predicting: Data

**Time flies like an arrow, fruit flies like a banana** (CBOW, size 2)

| Input | Output | | t | fl | l | a | fr | b | | t | fl | l | a | fr | b |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---| --- | ---  | --- |
| time | flies | | 1 | 0 | 0 | 0 | 0 | 0 | | 0 | 1 | 0 | 0 | 0 | 0 |
| flies | time | | 0 | 1 | 0 | 0 | 0 | 0 | | 1 | 0 | 0 | 0 | 0 | 0 |
| time | like | | 1 | 0 | 0 | 0 | 0 | 0 | | 0 | 0 | 1 | 0 | 0 | 0 |
| like | time | | 0 | 0 | 1 | 0 | 0 | 0 | | 1 | 0 | 0 | 0 | 0 | 0 |
| flies | like | | 0 | 1 | 0 | 0 | 0 | 0 | | 0 | 0 | 1 | 0 | 0 | 0 |

---

# Predicting: Architecture

<img src="word2vec.svg" style="margin: 40px auto; height: 24vh" />

- Shallow neural network, 1 hidden layer
  - Size is formaat woordvectoren
  - Doorgaans lineaire activatie
- Word vector gegeven one-hot encoded $\vec v$ is $\Theta_1 \vec v$

---
layout: image-left
image: consider.jpg
---

# Afweging

- Count (co-occurence)
  - behoudt semantische relaties
  - kost veel geheugen (eenmalig, up front)
- Predict
  - kost relatief weinig geheugen
  - is probabilistisch (random startwaarde nodig)
  - kan divergen

---
layout: image-right
image: discocat.jpg
---

# DisCoCat

- Word-vectors in meeste modellen "1D" (vectoren)
- Geen onderscheid grammaticale Functies
- DisCoCat gebaseerde modellen gebruiken matrices ("2D") voor bijvoorbeeld bijvoegelijk naamwoorden
- Extensie naar "3D" "matrices" voor transitieve woorden
- Tensors


---

# Vector Basis

Alternatieve manier van opschrijven:
$$\vec v : \mathbb{R}^2 = \begin{bmatrix}3\\2 \end{bmatrix} \qquad \vec u : \mathbb{R}^2 = \begin{bmatrix}5\\6 \end{bmatrix}$$

Neem $n$ basisvectors (voor $n$ dimensies), idealiter als volgt (orthonormaal):
$$\vec e_0 : \mathbb{R}^2 = \begin{bmatrix}1\\0 \end{bmatrix} \qquad \vec e_1 : \mathbb{R}^2 = \begin{bmatrix}0\\1 \end{bmatrix}$$

Nu kunnen we onze vector opschrijven als een lineaire combinatie van de basis-vectoren
$$\vec v : \mathbb{R}^2 = 3 e_0 + 2 e_1 \qquad \vec u : \mathbb{R}^2 = 5 e_0 + 6 e_1 $$

---

# Tensors

Notatie met basis-vectoren komen we tegen bij higher-order tensors:
- Vector is een 1-dimensionale lijst getallen
- Matrix is een 2-dimensionale tabel met getallen, werkt als functie $\mathbb{R}^n \to \mathbb{R}^m$
- Sommige modellen gebruiken 3- of 4-dimensionale "tensoren"
    - Functies met meerdere argumenten:
    - $(\mathbb{R}^n \otimes \mathbb{R}^m) \to \mathbb{R}^o$
    - Transitieve werkwoorden: De bakker **bakt** het brood: bakt(bakker, brood)

$$M = \begin{bmatrix}1&0\\0&1\end{bmatrix} = 1 e_0 \otimes e_0 + 0 e_0 \otimes e_1 + 0 e_1 \otimes e_0 + 1 e_1 \otimes e_1$$

$$\begin{align*}
T &= 1 e_0 \otimes e_0 \otimes e_0
    + 2 e_0 \otimes e_1 \otimes e_0
    + 3 e_1 \otimes e_0 \otimes e_0
    + 4 e_1 \otimes e_1 \otimes e_0 \\
    &+ 5 e_0 \otimes e_0 \otimes e_1
    + 6 e_0 \otimes e_1 \otimes e_1
    + 7 e_1 \otimes e_0 \otimes e_1
    + 8 e_1 \otimes e_1 \otimes e_1 
    \end{align*}
    $$

---
layout: chaptertitle
---

# Oefenopdracht 6

## Simpele Vector Space Models

