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

# Week 3

|Week|Les A|Les B|
|-|-|-|
|Week 1|Natuurlijke taal|Parsing|
|Week 2|NLTK Basics|Feature Extraction, Vector Space Models I|
|Week 3|**Bayes’ Rule, Naïve Bayes**|*hemelvaart*|
|Week 4|Vector Space Models II|Principle Component Analysis|
|Week 5|Locality Sensitive Hashing|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 5 – Naïve Bayes
## Bayes’ Rule

---

# Bayes’ Rule

$$P(p\mid w) = \frac{P(w \mid p) \times P(p)}{P(w)} = \frac{P(w \mid p) \times P(p)}{P(w \mid p) \times P(p) + P(w \mid \neg p) \times P(\neg p)}$$

<img src="bayes1.svg" style="margin: 40px auto; height: 70%;" />

---

# Bayes’ Rule

- $P(p)$ -- Kans dat een random tweet positief is: $40\%$
- $P(w \mid p)$ -- Percentage positieve tweets met dit woord: $55\%$
- $P(w \mid \neg p)$ -- Percentage negatieve tweets met dit woord: $25\%$

&nbsp;

$$
\begin{align*}
P(p\mid w) &= \frac{P(w \mid p) \times P(p)}{P(w)} \\
&= \frac{P(w \mid p) \times P(p)}{P(w \mid p) \times P(p) + P(w \mid \neg p) \times P(\neg p)} \\
&= \frac{0.55 \times 0.4}{0.4 \times 0.55 + (1 - 0.4) \times 0.25} \\
&= 0.59
\end{align*}
$$

---
layout: image-right
image: public/terms.jpg
---

# Termen

&nbsp;

&nbsp;

&nbsp;

$$
\underbrace{P(p\mid w)}_\text{Posterior} = \frac{
\overbrace{P(w \mid p)}^{\text{Likelihood}}
\times
\overbrace{P(p)}^{\text{Prior}}
}{
\underbrace{P(w)}_{\text{Evidence}}
}$$

---

# Naïve Bayes Classification

$$P(\text{pos} \mid w_0 \dots w_n) \propto P(\text{pos}) \times \prod^n_{i=0} \frac{P(w_i \mid \text{pos})}{P(w_i)}$$

$$P(\text{neg} \mid w_0 \dots w_n) \propto P(\text{neg}) \times \prod^n_{i=0} \frac{P(w_i \mid \text{neg})}{P(w_i)}$$

Ratio positief over negatief

$$\frac{P(\text{pos})}{P(\text{neg})} \times \prod^n_{i=0} \frac{P(w_i \mid \text{pos})}{P(w_i \mid \text{neg})} > 1$$

---

# Naïve Bayes

Tweet:"Today is a good day"

$$\frac{P(\text{pos})}{P(\text{neg})} \times \prod^n_{i=0} \frac{P(w_i \mid \text{pos})}{P(w_i \mid \text{neg})}$$

<div style="font-size: 0.8rem">

| Word | Pos | Neg |
| --- | --- | --- |
| today | 0.2 | 0.2 |
| is | 0.2 | 0.2 |
| good | 0.6 | 0.15 |
| day | 0.1 | 0.1 |

</div>

$$1 \times \frac{0.2}{0.2} \times \frac{0.2}{0.2} \times \frac{0.6}{0.15} \times \frac{0.1}{0.1} = 4 > 1$$

---

# Logaritmes

- $P(*) \in [0, 1]$, dus product van kansen steeds kleiner
- Floating point precision $\to$ underflow
- Oplossing: logaritmes

&nbsp;

## Rekenregels
$$\log(ab) = \log(a) + \log(b)$$
$$\log(\frac{a}{b}) = \log(a) - \log(b)$$

**Let op:** $\log({P(*)}) \in (-\infty, 0]$

---

# Logaritmes

$$\log(ab) = \log(a) + \log(b)$$
$$\log(\frac{a}{b}) = \log(a) - \log(b)$$

ergo

$$P(p\mid w) = \frac{P(w \mid p) \times P(p)}{P(w)}$$

wordt

$$\log(P(p\mid w)) = \log{(P(w \mid p))} + \log{(P(p))} - \log{(P(w))}$$

---

# Logaritmes
$$\log(ab) = \log(a) + \log(b)$$
$$\log(\frac{a}{b}) = \log(a) - \log(b)$$

ergo

$$\frac{P(\text{pos})}{P(\text{neg})} \times \prod^n_{i=0} \frac{P(w_i \mid \text{pos})}{P(w_i \mid \text{neg})}$$

wordt

$$\log{\left(\frac{P(\text{pos})}{P(\text{neg})}\right)} + \sum^n_{i=0} \log{(P(w_i \mid \text{pos})}) - \log{(P(w_i \mid \text{neg}))}$$

---
layout: image-right
image: public/training.jpg
---

# Training

- Bereken de log prior o.b.v. verhouding traingsdata
- Bereken per woord de log-likelihood

&nbsp;

## Prediction

- Product kansen $\to$ som log-kansen
- Logposterior $\underset{?}> 0$
