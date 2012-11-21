========================
Kontextfreie Grammatiken
========================

Definition: (Kontextfreie Grammatik)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Eine **kontextfreie Grammatik** :math:`G` wird beschrieben durch :math:`G=(\Sigma, N, P, S)`, wobei

* :math:`\epsilon` das Terminalalphabet
* :math:`N` das Nichtterminalalphabet
* :math:`P \subseteq N \times (\Sigma \cup N)^*` Menge von Produktionen (Regeln)

  statt :math:`(X, abY)` nutzen wir:math:`X \rightarrow abY`
  
* :math:`S` Startsymbol

**Beispiel** Kontextfreie Grammatik für :math:`L=\left\{a^n b^b | n \geq 0 \right\}`

:math:`G(\{a,b\}, \{S\}, P, S)`, wobei :math:`P=\{S \rightarrow aSb, S \rightarrow \epsilon \}`

**Beispielableitung** für aabb: :math:`S \Rightarrow aSb \Rightarrow aaSbb \Rightarrow aabb`.

**Definition** Eine Sprache :math:`L` heisst Kontextfrei, wenn es eine Kontextfreie Grammatik dafür gibt mit :math:`L= L(G)`.

:math:`\mathit{L}_{CF} = \text{Menge aller ktxf. Sprachen}`

Bemerkung: :math:`\mathit{L}_{REG} \subseteq \mathit{L}_{CF}`

**Beweis:** Jede reguläre Grammatik ist auch eine kontextfreie Grammatik.

**Beispiel:** Kontextfreie Grammatik zur Erzeugung aller arithmetischen Ausdrücke.

Induktion

* a ist ein arithmetischer Ausdruck
* Für arithmetische Ausdrücke :math:`\alpha` und :math:`\beta` sind

  :math:`(\alpha+\beta), (\alpha-\beta), \alpha\cdot\beta, \alpha/\beta`
  
  z.B. :math:`(a+a), (a \cdot (a + a \cdot a) + a)`
  
Beschreibung durch kontextfreie Grammatik :math:`G=(\Sigma, N, P, S)` mit

* :math:`\Sigma = \{(, ), a, +, -, \cdot, /\}`
* :math:`N = \{S, A, B, C \}`

  * C multiplikativer Operator
  * B additiver Operator
  * A Ausdruck
  
* Startsymbol :math:`S`
* Produktionen: :math:`P\{ S \rightarrow A, A \rightarrow a A \rightarrow (ABA), A \rightarrow ACA, B \rightarrow +, B \rightarrow -, C \rightarrow \cdot, C \rightarrow /\}`

Beispielableitung von :math:`a \cdot (a-a)+a)`.

:math:`S\Rightarrow (ABA) \Rightarrow (A+A) \Rightarrow (ACA + A) \Rightarrow A \cdot A + A \Rightarrow (A \cdot (ABA) +A) \Rightarrow (A \cdot (A-A) + A) \Rightarrow (a \cdot (A-A) + A) \Rightarrow (a \cdot (a-A) + A) \Rightarrow (a \cdot (a-a) + A) \Rightarrow (a \cdot (a-a) + a)`

bessere Notation: Ableitungsbaum (Parse-Baum)

* Startsymbol als Wurzel
* Terminale als Blätter
* Nichtterminale innere Knoten
* Regelanwendungen :math:`X \rightarrow \alpha_1 \alpha_2 ... \alpha_k`

Ableitungsbaum für :math:`(a \cdot (a - a) + a)` in :math:`G`

Vereinfachung von kontextfreien Grammatiken
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Elimination :math:`\epsilon`-Regeln (Regeln der Form :math:`X \rightarrow \epsilon`)
2. Elimination nutzloser Symbole
3. Elimination von Kettenregeln (Regeln :math:`X \rightarrow Y`)

**Elimination von** :math:`\epsilon` **-Regeln**

**Definition:** Eine kontextfreie Grammatik :math:`G` heisst :math:`\epsilon`-frei wenn sie keine Regeln in der Form :math:`X \rightarrow \epsilon` hat.

**Theorem** Sei :math:`G` eine kontextfreie Grammatik. Dann gibt es eine :math:`\epsilon`-freie kontextfreie Grammatik :math:`G'` mit :math:`L(G') = L(G) -\{\epsilon\}`

Beweis Transformation von :math:`G` in :math:`G'`:

1. Sei :math:`N_1` die Menge aller linken Seiten von :math:`\epsilon`-Regeln

  :math:`N_1 = \{A \in N | A \rightarrow \epsilon\}`

2. Bestimme alle zu :math:`\epsilon` ableitbaren Nichtterminale:

  Dann gilt :math:`N_1 = \{ A | A \overset{*}{\Rightarrow} \epsilon\}`
  
  Berechnung: :math:`N_1 \leftarrow N_1 \cup \{A \in N | A\rightarrow\alpha, \alpha \in N_1^*\}`

3. Für jede Regel :math:`A \rightarrow \alpha_1 B \alpha_2` mit :math:`B \in N_1, \alpha_1, \alpha_2 \in (\Sigma \cup N)^*`

  füge die Regel :math:`A \rightarrow \alpha_1 \alpha_2` zu :math:`P` hinzu und erhalte :math:`P_1`. Iteriere so lange bis sich :math:`P_1` nicht mehr ändert.

4. Eliminiere alle :math:`\epsilon`-Regeln aus P_1:

  :math:`P_2 \leftarrow P_1 - \{r \in P_1 | r=A \rightarrow \epsilon\}`
  
  :math:`\rightarrow G'= (\Sigma, N, P_2, S)`
  
**Beispiel:** Betrachte :math:`G=(\{a,b,c\}, \{S,A,B,C\}, P, S)` mit :math:`P= \{P\rightarrow AB, S \rightarrow C, A \rightarrow aB, A \rightarrow \epsilon, B \rightarrow bA, B \rightarrow \epsilon, C \rightarrow c\}`.

1. :math:`N_1 = \{ A, B\}`
2. Wegen :math:`S \rightarrow AB` und :math:`A, B \in N_1` erfolgt :math:`N_1 \leftarrow N_1 \cup \{S\}`

  :math:`N_1 = \{A, B, S\}`

3. :math:`P_1 \leftarrow P \cup \{ S \rightarrow B, S \rightarrow A\, A \rightarrow a, B \rightarrow b\}`
4. :math:`P_2 \leftarrow P_1 - \{ A \rightarrow \epsilon, B \rightarrow \epsilon\}`

**Elimination nutzloser Symbole**

Ein Symbol X heisst **erreichbar** falls es eine Ableitung :math:`S \overset{*}{\Rightarrow \alpha}` gibt, so dass X in :math:`\alpha` vorkommt.

Bestimmung der Menge erreichbarer Symbole
  
Sei :math:`G=(\Sigma, N, P, S)` eine kontextfreie Grammatik
  
1. :math:`E_N := \{S\}` (erreichbare Nichtterminale)
  
  :math:`E_{\Sigma} := \varnothing` (erreichbare Terminale)
    
2. Für alle :math:`A \rightarrow \alpha` in :math:`P` mit :math:`A \in E_N`:
  
  Füge die Symbole von :math:`\alpha` zu :math:`E_N` bzw :math:`E_{\Sigma}` hinzu
    
  Wiederhole solange, bis sich :math:`E_N` und :math:`E_{\Sigma}` nicht mehr ändern.
    
3. Reduziere die Grammatik zu :math:`G' = (E_{\Sigma}, E_N, P', S)` mit :math:`P'=\{A\rightarrow \alpha \in P | A \in E_N \}`

**Bestimmung der Menge der produktiven Nichtterminale**

Ein Nichtterminal X heisst **produktiv** (erzeugend), falls es eine Ableitung :math:`X \overset{*}{\Rightarrow} w` gibt für ein :math:`w \in \Sigma^*`
  
1. :math:`Prod := \{ A \in N | A \rightarrow w \in P, w \in \Sigma^* \}`
2. Für alle :math:`A \in N`: Falls :math:`A \rightarrow \alpha \in P` mit :math:`\alpha \in (\Sigma \cup Prod)^*`, füge A zu Produ hinzu.
  
  Wiederhole solange, bis sich Prod nicht mehr ändert.
  
3. Reduziere die Grammatik zu :math:`G' = (\Sigma, Prod, P', S)` mit :math:`P' = \{ A \rightarrow \alpha \in P | A \in Prod  \text{ und } \alpha \in Prod\}`.

**Beispiel:** Betrachte kontextfreie Grammatik

:math:`G = (\{a,b,c\}, \{S,A,B,C\}, P, S)` mit :math:`P = \{ S \rightarrow A, S \rightarrow AB, A \rightarrow Aa, A \rightarrow a, A \rightarrow bB, B \rightarrow Bb, C \rightarrow c \}`

erreichbare Symbole: S, A, B, a, b

erhalten Grammatik :math:`G' = (\{a,b\}, \{S,A,B\}, P', S)` mit :math:`P' = \{ S \rightarrow A, S \rightarrow AB, A \rightarrow Aa, A \rightarrow a, A \rightarrow bB, B \rightarrow Bb \}`

Produktive Nichtterminale in G': A, S

erhalten Grammatik :math:`G'' = (\{a\}, \{S,A\}, P', S)` mit :math:`P'' = \{ S \rightarrow A, A \rightarrow Aa, A \rightarrow a \}`

**Definition:** Eine kontextfreie Grammatik :math:`G` heisst **reduziert**, falls sie keine unproduktiven und keine nicht erreichbaren Symbole enthält.

**Elimination von Kettenregeln** :math:`A \rightarrow B`

1. Bestimme für jedes Nichtterminal :math:`A` die Menge:

  :math:`K(A) = \{D \in N | A \overset{*}{\Rightarrow} D \}`
  
  aller Nichtterminale, die in :math:`G` aus :math:`A` (nur mit Kettenregeln) abgeleitet werden können.
  
  iterativ Berechnen: :math:`K(A) := \{A\}`
  
  :math:`K(A) := K(A) \cup \{ x \in N | \text{existiert } C \in K(A) \text{ mit } C \rightarrow \in P \}`
  
2. Für jedes :math:`X \in K(A)` und jede Regel :math:`X \rightarrow \alpha`, die keine Kettenregel ist, füge die Regel :math:`A \rightarrow \alpha` zu :math:`P'` hinzu und entferne alle Kettenregeln.

**Beispiel:** :math:`G = (\{a,b,c,d\}, \{F,S\}, P, S)` wobei :math:`P=\{S \rightarrow F, F \rightarrow a, F \rightarrow bF, F \rightarrow d, F \rightarrow c\}`

1. :math:`K(S) = \{S, F\}`

  :math:`K(F) ) = \{F\}`

2. :math:`P' = \{ S \rightarrow a, S \rightarrow bF, S \rightarrow d, S \rightarrow c, F \rightarrow a, F \rightarrow bF, F \rightarrow d, F \rightarrow c \}`

