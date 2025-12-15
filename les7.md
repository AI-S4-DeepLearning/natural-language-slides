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
.pca {
  background-size: 40% !important;
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
|Week 4|Vector Space Models II|**Principle Component Analysis**|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---

# Vorige les: Handmatige woord-vectoren

| |person|object|female|education|old|parent|friendship|
|---|---|---|---|---|---|---|---|
|man|1|0.2|-1|0|0.5|0|0|
|woman|1|0.2|1|0|0.5|0|0|
|child|1|0.2|0|0|-1|-1|1|
|parent|1|0.2|0|0|0.5|1|1|
|mother|1|0.2|1|0|0.5|1|1|
|father|1|0.2|-1|0|0.5|1|1|
|...||||||||


---
layout: chaptertitle
---

# Les 7 – Principle Component Analysis
## Dimensionality reduction

---
layout: image-right
image: coord.jpg
---

# Coordinaatstelsels en basis-vectoren

- Standaardbasis (orthonormaal)
- Datapunten niet afhankelijk van basis
  - Alleen coordinaten
- Liever werken in een fijnere basis

---
layout: image-left
image: rotation.jpg
---

# Principle Component Analysis

- Idee: roteer point-cloud (of camera)
- Dataspreiding zoveel mogelijk over klein aantal assen
- Bewaar belangrijkste assen
  - Vast aantal
  - Percentage 

---
layout: image
image: pca1.svg
class: pca
---

# Voorbeeld (2D)

---
layout: image
image: pca2.svg
class: pca
---

# Beste x-as

---
layout: image
image: pca3.svg
class: pca
---

# Data-transformatie

---
layout: image-right
image: blackboard.jpg
---

# Berekenen

- Kies een as
- Roteer voor maximale variantie
  - Minimaliseer afstand tot de as
  - Maximaliseer projectie op de as
- Herhaal voor orthagonale deel

---

# Vectorised: Eigenvectoren covariantie-matrix

$$
\begin{align*}
\max \sum_i\langle x_i \mid u \rangle^2
&= \max \sum_i \langle x_i \mid  u \rangle\ \langle x_i  \mid  u \rangle \\
&= \max \sum_i\ \langle u \rvert\ \lvert  x_i \rangle\ \langle x_i  \rvert\ \lvert  u \rangle \\
&= \max\ \langle u \rvert \sum_i \lvert x_i \rangle \langle x_i \rvert \ \lvert u \rangle \\
&= \max\ \langle u \rvert\ \mathbf{C}\ \lvert u \rangle \quad\text{ \scriptsize waar }\quad\mathbf{C} = \frac{1}{n}\sum_i\ \lvert x_i \rangle \langle x_i \rvert

\end{align*}$$
$$\text{ via Lagrange: }\quad \langle \mathbf{C} \mid u \rangle = \lvert \lambda u \rangle \quad\text{ met }\quad \lambda = \langle u \mid \mathbf{C} \mid u \rangle $$


<br/>

**Noot bij de notatie:** $\langle u \mid v \rangle$ was het inwendig product van $u$ en $v$. Bij $\langle u \rvert\ \mathbf{C}\ \lvert v \rangle$ wordt een matrix gebruikt<br/> om de twee vectoren te combineren - in beide gevallen levert dit een getal op. In algemene termen is $\lvert u \rangle$<br/> een "normale" vector, en $\langle u \rvert$ een "rij vector" ($u^\dagger$). Een vermenigvuldiging $\lvert u \rangle \langle v \rvert$ geeft een matrix.

---

# Covariantie-matrix

$$\begin{bmatrix}
\text{var}(x,x) & \text{cov}(x,y) & \text{cov}(x,z) \\
\text{cov}(y,x) & \text{var}(y,y) & \text{cov}(y,z) \\
\text{cov}(z,x) & \text{cov}(z,y) & \text{var}(z,z) \\
\end{bmatrix}$$

- Variantie $\sigma^2$
- Covarantie: $\text{cov}(x, y) = \text{cov}(y, x)$ hoeveel beweegt $x$ mee met $y$
- Als lineaire transformatie: invloed van $x, y, \dots$ op $x, y, \dots$
- Eigenvectoren: Welke richtingen schalen alleen?
- Eigenwaardes: Hoeveel schalen deze richtingen?
    - De eigenwaarde is de waarde $\lambda$ van de vorige slide.
    - Per eigenvector (as van de geroteerde basis) is er een $\lambda$-waarde (hoeveelheid informatie die deze as bevat).

---
layout: chaptertitle
---

# Inleveropdracht 1

## Vector Space Models & Principle Component Analysis
