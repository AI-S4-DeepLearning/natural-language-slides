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

---
disabled: true
---

@Brian deze les nog wat verder aanvullen
 - Intuitie kweken
 - Aansluiten op LA
 - Vooruitblik LLM (dit wordt ook gebruikt voor...)
 - Vooral werkcollege met embeddings in Numpy

---

# Word Embeddings

<img src="/embedding.png" style="margin: 40px auto; height: 75%; filter: invert(93%)" />

*Source: https://miro.medium.com/max/1400/1*sAJdxEsDjsPMioHyzlN3_A.png*

---

# Dimensionaliteit van Word Embeddings

- Elk woord heeft een eigen vector in een hoog-dimensionale ruimte
  - Eventueel meerdere embeddings per woord, o.b.v. part of speech (`zijn_V` vs `zijn_DET`)
  - Eventueel preprocessing om meerdere verschijningsvormen van woord samen te voegen (loop, loopt, lopen)

&nbsp;

### Traditioneel
 - 150, 300 of 500 dimensies

&nbsp;

### LLMs
 - 256-4096 dimensies
 - OpenAI’s `text-embedding-3-small` en `text-embedding-3-large` hebben respectivelijk 1536 en 3072 dimensies.
- Gemini Embedding: 3072 dimensies
- Gecko heeft 256 dimensies, maar presteert beter dan sommige 768-D modellen.

---
layout: image-right
image: jupyter.jpg
---

# Latente Informatie

- Word embeddings gewonnen uit statistische data
  - Structuur in resulterende vector-ruimte
  - Weerspiegelt structuren in taal
  - Afhankelijk van *corpus* (bronteksten)
  - Eventuele bias ook overgenomen

&nbsp;

- Allegorien
  - China : Beijing ~ Japan : Tokio
- Assen kunnen bepaalde betekenis uitdrukken
  - In sommige gevallen direct, maar ook na toepassing PCA
- Clusters

---
layout: chaptertitle
---

# Oefenopdracht

## Simpele Vector Space Models
---
layout: image-left
image: training.png
---

# How to get there

- Counting
- Training
- Contextuele modellen

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
  - One-hot Encoding $\to$ Sparsity
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
\end{bmatrix} \quad \text{Na reductie: } V \approx \begin{bmatrix}
-0.60 & 1.72 & -1.72 & 0.91 & -0.91 & 0.60 \\
-0.51 & 0.70 & 0.70 & -0.19 & -0.19 & -0.51 \\
\end{bmatrix}$

<div style="height: 2vh" />

**Iedere kolom staat voor een word-embedding:**

<div style="height: 2vh" />

Time heeft de vector 
$\ket v = \begin{bmatrix}
-0.60 \\ -0.51
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

<img src="/word2vec.svg" style="margin: 40px auto; height: 24vh" />

- Shallow neural network, 1 hidden layer
  - Size is formaat woordvectoren
  - Doorgaans lineaire activatie
- Word vector gegeven one-hot encoded $\ket v$ is $\Theta_1 \ket v$

---
layout: image-right
image: bert.jpg
---

# Contextuele modellen

- Embeddings from Language Models (ELMo)
  - Bidirectioneel LSTM, meerdere embeddings voor een woord o.b.v. PoS
    - "Stick to the plan"
    - "A wooden stick"
- Bidirectional Encoder Representations from Transformers (BERT)
  - Transformer, geeft context-bewuste embeddings los van PoS
    - "She went to the bank to deposit money"
    - "They sat down on the river bank"
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
layout: chaptertitle
---

# Oefenopdracht

## Training Word Vectors

---
layout: image-left
image: sentence.webp
---

# Sentence Embeddings

- Optellen woordvectoren?
  - Volgordelijkheid
- Product?
  - Inwendig Product?
    - Maar dat is $V \times V \to \mathbb R$...
  - Hadamard Product?
    - Zelfde probleem als optellen

---
layout: image-right
image: discocat.jpg
---

# DisCoCat

- Categorical Compositional Distributional (semantics)
- Word-vectors in meeste modellen "1D" (vectoren)
- Geen onderscheid grammaticale Functies
- DisCoCat gebaseerde modellen gebruiken matrices ("2D") voor bijvoorbeeld bijvoegelijk naamwoorden
- Extensie naar "3D" "matrices" voor transitieve woorden
- Tensors

---

# Parse tree

<img src="/man_telescope.svg" style="margin: 40px auto; height: 40vh;" />

---

# Translation

<img src="/discocat-grammar.svg" style="margin: 40px auto; width: 50vw;" />

---

# Result

<img src="/man_telescope_vec.svg" style="margin: 40px auto; height: 40vh;" />

---

# Index-notatie

Des te complexer tensoren worden, des te lastiger wordt het om deze te overzien.
- Hebben we te maken met een rij van kolommen van rijen? Of een rij van rijen van kolommen?
- Welke "assen" willen we verwisselen bij een transpositie?
- Op welke manier wordt een vermenigvuldiging uitgevoerd?

**In dit geval is het handiger om met index-notatie te werken, en de basis expliciet te benoemen.**

###  Voorbeeld

$T_{ij}^k\textcolor{grey}{e_k\otimes\epsilon^i\otimes\epsilon^j}$ staat voor *"[y] ziet [x]"*. We willen dit combineren met vectoren $m^a \textcolor{grey}{e_a}$ (*"man"*) en $h^b \textcolor{grey}{e_b}$ (*"hond"*).

- Voor *"(De) man ziet (de) hond"* zetten we de index van *"hond"* gelijk aan de eerste index van *"zien"*, en die van *"man"* aan de tweede: 
$$S = \mathbf T \ket h \ket m = T_{ij}^kh_im_j = T_{ij}^km_jh_i \mapsto S^k e_k$$
- Voor *"(De) hond ziet (de) man"* zetten we de index van *"man"* gelijk aan de eerste index van *"zien"*, en die van *"hond"* aan de tweede: 
$$S = \mathbf T \ket m \ket h = T_{ij}^km_ih_j = T_{ij}^kh_jm_i \mapsto S^k e_k$$


---

# Sommatie en Einstein Notatie

Als we de getallen in de vector / matrix indexeren, kunnen we het systematisch over individuele getallen hebben.

- $v^3$ staat voor het derde element van $\ket v$ 
$$\ket v = v^1{\color{grey}e^1} + v^2{\color{grey}e^2}$$
- $M^1_2$ staat voor het eerste element van de tweede kolom van $\mathbf M$
$$\mathbf M = M^1_1{\color{grey}e^1\otimes\epsilon_1} + M^1_2{\color{grey}e^1\otimes\epsilon_2} + M^2_1{\color{grey}e^2\otimes\epsilon_1} + M^2_2 {\color{grey}e^2\otimes\epsilon_2}$$

De berekeningen voor de elementen van $\ket w = \mathbf M \ket v$ ziet er nu als volgt uit:
$$w^i = \sum_{j = 1}^n M^i_j v^j = M^i_{\color{#00aaff}j} v^{\color{#00aaff}j}$$

Vaak laten we de $\Sigma$ en sommatie index $j$ weg, omdat die eigenlijk al duidelijk is: het is de enige index die twee keer voor komt, boven en beneden.



---
layout: chaptertitle
---

# [NLP-3] Cleaning en NLTK

---

# NLTK
## Natural Language Toolkit

Installatie:
- Package `nltk` installeren
- Kan in een venv, (grote) datasets centraal downloaden

Benodigde imports voor de inleidende opgaven:

```py
import nltk                                # Python library voor NLP
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
from nltk.tokenize import RegexpTokenizer
import matplotlib.pyplot as plt            # Library voor visualisatie
import random
```

---

<style>
.third {
    display: inline-block;
    width: 32%;
}
.emoji {
    font-size: 72px;
    text-align: center;
    margin: auto;
}
.tweet {
    text-align: center;
    font-style: italic;
    width: 100%;
}
</style>

# Casus: Sentiment analysis

**Bepalen van een willekeurige tekst (e.g. Tweet): positief of negatief?**

<div class="third">
<div class="emoji">😃</div>
<div class="tweet">Brilliant effort! Loved every second of it!</div>
</div><div class="third">
<div class="emoji">😐</div>
<div class="tweet">This was okay, I guess, but I expected more.</div>
</div><div class="third">
<div class="emoji">😡</div>
<div class="tweet">Worst customer service ever! Totally dissatisfied with how I was treated!</div>
</div>

&nbsp;

- Wat is nuttige info in een Tweet?
- Hoe kan je Machine Learning gebruiken?

---

# Plan de Campagne

<img src="/sa.svg" style="margin: 40px auto; width: 50vw;" />

**Wat geef je als input?**

---

# Preprocessing

- Tokenizing
- Lowercasing
- Stop words en interpunctie verwijderen
- Stemming

- Gebruik regular expressions, `re` library<br>
    Voorbeeld, hyperlinks verwijderen:
    ```py
    tweet = re.sub(r'https?://[^\s\n\r]+', '', tweet)
    ```

- Tokenizing in NLTK met regular expressions

    ```py
    from nltk.tokenize import RegexpTokenizer
    RegexpTokenizer(r'\w+|\$[\d\.]+|\S+')
    -> ['This', 'is', 'an', 'example', '.']
    ```

---
layout: image-left
image: ./python.jpg
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

</v-click>

---
layout: image-right
image: ./stem.jpg
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

---
layout: image-right
image: iliad.jpg
---

# Processing

- Inlezen teksten
  - Verwijderen preamble and postscript

<v-click>

- Splitsen in zinnen <v-click> - **hoe?** </v-click>

</v-click>
<v-click>

- Per zin, splitsen in woorden
  - `RegexpTokenizer`

</v-click>
<v-click>

- Verwijder stopwords (`nltk.corpus`) en interpunctie (`string`)

</v-click>
<v-click>

- Lowercase en stem
  - `PorterStemmer`

</v-click>
<v-click>

- Frequency Dictionary
  - Per $\text{woord} \times \text{tekst}$, hoevaak komt het woord in de tekst voor?
  - Scatterplot selectie woordfrequenties

</v-click>

---
layout: image-left
image: ./data.jpg
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

# [NLP-4] Locality Sensitive Hasing

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

---
layout: chaptertitle
---

# [NLP-5] Document Databases

---

# Werkcollege

## Klein beetje stof - toepassing LHS in Doc Databases, wat bestaat er?
TODO @Brian

---
layout: chaptertitle
---

# Portfolio-item
## [NLP-I] Word Embeddings

---
layout: chaptertitle
---

# [NLP-6] Large Language Models

---

# Vanaf hier @Tijmen?

---
layout: image-right
image: transformers.png
---

# Deep Learning for NLP

- Bidirectional Encoder Representations from Transformers (BERT)
- Generative Pre-trained Transformer (GPT)
- Transformers
- Attention

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

*Source: Vaswani et al. (2017)*

---
layout: image-left
image: bert.jpg
---

# BERT
- Bidirectional Encoder Representations from Transformers

- Transformer Encoder
- Input tokens matchen output tokens (of MASK)
- Left to right en right to left
- Generate all at once

---
layout: image-right
image: gpt.webp
---

# GPT
- Generative Pre-trained Transformer
- Autoregressive Transformer Decoder
- Token stream generator obv vorige token
- Geen encoder nodig
- Autonoom lezen corpora / unlabeled data

---

# Encoder / Decoder

<div style="display: inline-block; margin-right: 50px">

- Self-attention Mechanism 
- Bewerk delen input sequence parallel
- Efficienter in capturen relaties
- Encode global context in representaties
- Gebruik downstream (predict / answer)

</div> <img style="display: inline-block; margin:auto" width="400" src="/encoder-decoder.png" />

*Source: Chaudhari et al. (2021)*

---

# Attention


<a href="https://colab.research.google.com/github/tensorflow/tensor2tensor/blob/master/tensor2tensor/notebooks/hello_t2t.ipynb#scrollTo=OJKU36QAfqOC">
    <img style="padding: 3px; background: black; border: 2px solid #00a0ff; margin:auto" width="300" src="/attention.gif" />
</a>

&nbsp;

&nbsp;

*Source: [GPT and BERT: A Comparison of Transformer Architectures](https://dev.to/meetkern/gpt-and-bert-a-comparison-of-transformer-architectures-2k46), Leonard Püttmann*


---
layout: chaptertitle
---

# [NLP-7] Attention

---
layout: chaptertitle
---

# [NLP-8] NanoGPT

---
layout: chaptertitle
---

# Portfolio-item
## [NLP-II] Large Language Models
