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
|Week 2|NLTK Basics|**Feature Extraction, Vector Space Models I**|
|Week 3|Bayes’ Rule, Naïve Bayes|*hemelvaart*|
|Week 4|Vector Space Models II|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 4 – Feature Extraction
## & Intro Vector Space Models

---

# Recap: Regression

<img src="linreg.png" style="margin: 40px auto; height: 80%; filter: invert(93%)" />

---

# Recap: Regression

<img src="regressions.svg" style="margin: 40px auto; height: 35vh;" />
---

# Logistic Regression

<img src="logres.png" style="margin: 40px auto; height: 40vh; filter: invert(93%)" />

---

# In formules

### Linear Regression
$$h(x) = \theta_0 x_0 + \theta_1 x_1 + \theta_2 x_2 + ... \theta_N x_N$$

*$\theta$ bevat de "weights", $x$ is een input-vector.*

&nbsp;

### Logistic regression
$$ h(z) = \frac{1}{1+\exp^{-z}}$$
$$z = \theta_0 x_0 + \theta_1 x_1 + \theta_2 x_2 + ... \theta_N x_N$$

*$h(z)$ is een sigmoid (activatie)-functie.*

---
layout: chaptertitle
---

# Feature Extraction & Embeddings

---

# Feature Extraction

<img src="supervised.svg" style="margin: 40px auto; width: 60vw;" />

---
layout: image-left
image: public/data.jpg
---

# Feature Extraction

- Significante Woorden
  - Sentiment-analyse: positieve / negatieve woorden
  - Voorbereidende opdracht 1: "Troy", "Ulysses"

- Bag-of-Words
  - Telling woorden in een document

- Term-Frequency - Inverse Document Frequency (TF-IDF)
  - Hoe vaak komt een woord voor in een document?
  - Hoe vaak komt het woord voor in general?
  - Verhouding bepaalt "belangrijke" woorden

---
layout: chaptertitle
---

# Vector Space Models

---
layout: image-right
image: "vector.svg"
---

# Vectors - Recap

### 2D
$$\vec v : \mathbb{R}^2 = \begin{bmatrix}3\\2 \end{bmatrix}$$


### 3D
$$\qquad \vec v : \mathbb{R}^3 = \begin{bmatrix}3\\2 \\0 \end{bmatrix}\qquad \vec u : \mathbb{R}^3 = \begin{bmatrix}1\\2 \\3 \end{bmatrix}$$


### N-dimensional
$$\vec u : \mathbb{R}^{100} = \begin{bmatrix}u_0\\u_1\\ \vdots \\ u_{99} \end{bmatrix}$$

---

# Vectors

- Pijlen in een ruimte
- Lijsten van getallen
- Alles dat we kunnen:

    - Optellen
    - Negatieve / aftrekken
    - Vermenigvuldigen met een scalar (getal)
    - Een nul-vector heeft
<div style="height: 2vh" />

 $$\vec u + \vec v = \vec v + \vec u$$

 $$(\vec u + \vec v) + \vec w = \vec u + (\vec v + \vec w)$$

 $$a(\vec u + \vec v) = a\vec u + a \vec v$$

 $$(a+b) \vec v = a \vec v + b \vec v$$


---

# Inner Product & Norm

- Twee vectoren in dezelfde ruimte

$$\vec v : \mathbb{R}^2 = \begin{bmatrix}3\\2 \end{bmatrix} \qquad \vec u : \mathbb{R}^2 = \begin{bmatrix}5\\6 \end{bmatrix}$$

- Inwendig product geeft een getal

$$\langle v \mid u \rangle = 3 \times 5 + 2 \times 6 = 27$$

Ook wel: $u \cdot v$, $\langle u, v \rangle$ of $u^T v$

## Norm
$$ \lvert v \rvert  = \sqrt { \langle v \mid v \rangle } 
= \sqrt { 3 \times 3 + 2 \times 2 } = \sqrt{13} $$

Norm == _lengte_ van de vector, viz. _normaliseren_.

Dus ook: de afstand tussen twee punten (oorsprong en einde vector).

---

# Matrices

Lineaire transformaties: (Scaling), Stretching, Rotation, Skew

$$\mathbf{M} : \mathbb{R}^{3\times3}= \begin{bmatrix}0 & 0 & 3 \\ 0 & 2 & 0 \\ 1 & 0 & 0\end{bmatrix} \qquad v : \mathbb{R}^{3}= \begin{bmatrix}1 \\ 2 \\ 3 \end{bmatrix}$$

### Matrix Vector Product

$$\mathbf{M}v = \begin{bmatrix}
0 \times 1 + 0 \times 2 + 3 \times 3 \\
0 \times 1 + 2 \times 2 + 0 \times 3 \\
1 \times 1 + 0 \times 2 + 0 \times 3
\end{bmatrix} = \begin{bmatrix} 9 \\ 4 \\ 1 \end{bmatrix}$$

### Matrix Matrix Product
$$\mathbf{M}: \mathbb{R}^{m \times n} \quad \mathbf{N}: \mathbb{R}^{n \times o} \to \mathbf{MN}: \mathbb{R}^{m \times o}$$
$$\mathbf{M}(\mathbf{N} v) = (\mathbf{MN})v$$

---

# Numpy

- `numpy.array`
- Optellen, aftrekken: `+` en `-`
- Scalair vermenigvuldigen: `*`
- Inner product, matrix-vector, matrix-matrix: `M @ v` of `numpy.dot(M, v)` \
(technisch gezien `numpy.matmul(M, N)` voor matrixvermenigvuldiging,\
maar is identiek aan `dot` in minder dan 3 dimensies)
- `.norm()` voor norm / lengte / Euclidean distance

***Let op met `*` tussen vectoren, dat vermenigvuldigt per element!***


---
layout: image-right
image: public/projection.jpg
---

# Word Embeddings

- One-hot Encoding

    - Sparsity
    - Dimensionality Reduction

- Word Vectors

    - Counting
    - Predicting

---

# Word Embeddings

<img src="embedding.png" style="margin: 40px auto; height: 75%; filter: invert(93%)" />

*Source: https://miro.medium.com/max/1400/1*sAJdxEsDjsPMioHyzlN3_A.png*

---
layout: chaptertitle
---

# Oefenopdracht 4

## Training Word Vectors
