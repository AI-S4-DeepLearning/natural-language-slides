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
|Week 5|**Locality Sensitive Hashing**|Machine Translation|
|Week 6|Andere Modellen en Toepassingen|Deep Learning for NLP|
|Week 7|Attention|

---
layout: chaptertitle
---

# Les 8 – Locality Sensitive Hashing
## Hash functions

---

# Aanleiding

- Met word-vectors erg eenvoudig similarity te bepalen

$$\text{Sim}_{\cos} (A,B) = \cos^{-1} {\langle u \mid v \rangle \over \lvert u\rvert \ \lvert v\rvert}
$$

- Wat is de cosine similarity van "Croatia" en "Zagreb"?

- Ander type vraag: welke vector(en) hebben de meeste similarity met "Ulaanbaatar"?

<v-click>

```python
best_score, best_word = 0.0, None

for word in dictionary:
    sim = cosine_similarity(word, "Ulaanbaatar")
    if sim > best_score:
        best_score, best_word = sim, word
```

</v-click>

<v-click>

&nbsp;
### (╯°□°）╯︵ ┻━┻

</v-click>

---
layout: image-right
image: hash.png
---

# Hashing

- Kleine "fingerprint" van groter stuk data
- Makkelijk en sneller te vergelijken
- One way operatie
- Normaal: hashes zo uniek mogelijk
  - Geen collisions
  - Geen verband tussen gerelateerde hashes
  - Toepassingen: cryptografisch, indexing

&nbsp;
## Locality Sensitive Hashing

- Ook hier: kleine fingerprint van grotere data
- Maar: collisions gerelateerde data wel wenselijk
  - Overlap hashes gelijkende teksten
  - False positives
  - False negatives

---
layout: image-left
image: buckets.jpg
---

# Hashes en Buckets

- Uitgangspunt: hashes van punten in een metric space
    - Hier: embeddings in $\mathbb{R}^{300}$
- Hyperplane splitst vector space in 2 delen
- $x$ random hyperplanes: splitsing in $2^n$ delen (buckets)
- Doel: ~10 teksten per bucket
- $10000$ teksten $\to$ $1000$ buckets $\to \log_2(1000) \approx 10$ hyperplanes nodig

---
layout: image-right
image: hyperplane.jpg
class: hyperplane
---

<style>
.hyperplane ~ .w-full {
background-size: 130% !important;
background-position: 25% 50% !important
}
</style>

# Hyperplanes

- Hyperplane in 2D: lijn (1D subspace)
- Hyperplane in 3D: 2D vlak / subspace
- Hyperplane in 300D: 299D hypervolume

- Hyperplanes uniek aan de duiden met dual: normaalvector
  - Vector haaks op de hyperplane

**Voor document-vector $\lvert v \rangle$ en hyperplane $\langle h \rvert$**
  - $\langle h \mid v \rangle > 0$ aan de ene kant $\to$ bitwaarde 0
  - $\langle h \mid v \rangle < 0$ aan de andere kant $\to$ bitwaarde 1
  - $\langle h \mid v \rangle = 0$ erg onwaarschijnlijk

Met 10 hyperplanes 10-bits waarde per document

---

# Matchen

- Maak een hash van een nieuw document op basis van de woordvectoren
- Bereken de bucket van het document
- Itereer over de hashes in dezelfde bucket
    - Retrieve bekend document uit hash-tabel
    - Vergelijk deze meer in depth

&nbsp;

<v-click>

- **Wat gebeurt er met ongerelateerde documenten in dezelfde bucket?**

</v-click>
<v-click>

- **Wat gebeurt er met similar documenten in een andere bucket?**

</v-click>

<v-click>

&nbsp;

### Meerdere herhalingen met random hyperplanes
Rank op aantal collisions, evt. met ondergrens

</v-click>


---

# Toepassing

- Machine Translation
- Document Retrieval
- Recommendations
- Near-duplicate detection
- Nearest Neighbours
- Audio fingerprinting (Shazam etc.)
- Genome searching

<!--
## Approximate Nearest Neighbors
-->

---
layout: chaptertitle
---

# Oefenopdracht 7

## KNN Recap

---
layout: chaptertitle
---

# Samen Oefenen

## Locality Sensitive Hashing

---

# Setup

1. Maak een set van 26 3D vectoren voor ons alfabet
2. Maak een set van 1000 random documenten, bestaande uit 2-8 random letters
3. Maak een functie die de vector embedding van een letter geeft
4. Maak een functie die de vector embedding van een document geeft (gemiddelde vector)
5. Vergelijk alle paren van documenten met de cosine similarity
6. Verhoog het aantal documenten met een factor 10 en dan een factor 100

&nbsp;

## LSH

1. Genereer een hyperplane (2D vlak) om de vector-ruimte te splitsen
2. Bereken (met code) hoeveel hyperplanes nodig zijn om ~16 documenten per bucket te krijgen
3. Genereer een set van zoveel hyperplanes
4. Maak een functie om N universes van hyperplanes te genereren
