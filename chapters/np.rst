Anschauliche Definition von NP
==============================

Polynomzeit-Verifizierer
~~~~~~~~~~~~~~~~~~~~~~~~

**Beispiel:** CLIQUE-Problem

**Gegeben:** ungerichteter Graph :math:`G=(V, E)`, Zahl :math:`k \leq |v|`.

**Frage:** Gibt es in :math:`G` eine Clique der Grösse :math:`k`?

Das heisst, gibt es eine Menge :math:`S \leq V`, so dass alle Knoten aus :math:`S` paarweise durch Kanten verbunden sind?

.. image:: 12_1.jpg

:math:`k=4`

:math:`S={v_1, v_2, v_3, v_4}` ist eine Clique

Zur Bestimmung einer Clique in einem Graphen sind nur exponentielle Verfahren bekannt.

Wenn man aber einen Lösungskandidaten kennt, kann man in linearer Zeit bezüglich der Anzahl der Kanten nachprüfen, ob die Lösung stimmt.

Formale Definition eines Verifizierers:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sei :math:`L \leq \Sigma^*` eine Sprache und :math:`p: \mathbb{N} \leftarrow \mathbb{N}` eine Funktion. Eine Turingmaschine :math:`M` ist ein p-Verifizierer für :math:`L`, falls :math:`M` wie folgt auf allen Eingaben aus :math:`\Sigma^* \times \{\#\} \times \{0,1\}^*` arbeitet:

1. :math:`\text{Time}_M(w\#x) \leq p(|w|)` für alle Eingaben w#x
2. Für jedes :math:`w\in L` existiert ein :math:`x \in \{0,1\}^*` mit :math:`|x| \leq p(|w|)`, so dass :math:`M` die Eingabe w#x akzeptiert.

  :math:`x` heisst **Zeuge** für :math:`w \in L`

Falls :math:`p \in O(n^k)` für ein :math:`k \in \mathbb{N}`, dann ist :math:`M` ein **Polynomzeitverifizierer**.

**Beispiel:** Polynomzeit-Verifizierer für das CLIQUE-Problem:

**Eingabe:**

  * Kodierung eines ungerichteten Graphen, Zahl :math:`k`
  * Zeuge: ein Bit für jeden Knoten des Graphen. Sei :math:`G=(V,E)` mit :math:`V=\{v_1, ..., v_n\}`
  
    Dann:
    
      * :math:`x_1=1`, falls :math:`v_i \in S`
      * :math:`x_1=0`, falls :math:`v_i \notin S`
      
    Für alle :math:`1 \leq i \leq n`

Verifizierer überprüft für alle Knotenpaare :math:`(v_i, v_j)` mit :math:`x_i = 1 = x_j`, ob die Kante in :math:`G` vorhanden ist.

:math:`\rightarrow` Rechenzeit :math:`O(n^2)`.

**Theorem:** (ohne Beweis)

NP = Menge aller Sprachen, für die ein Polynomzeit-Verifizierer existiert

**Zusammenfassung:**

* :math:`P \hat{=}` Lösung **finden** in Polynomzeit
* :math:`NP \hat{=}` Lösung **verifizieren** in Polynomzeit

**Offene Frage:** Gilt :math:`P = NP`?

**Vermutung:** :math:`P \neq NP`

NP-Vollständigkeit
------------------
Konzept zum Beweis relativer Schwierigkeit von Problemen.

.. image:: 12_2.jpg

**Polynomelle Reduktion:** Seien :math:`L_1 \subseteq \Sigma_1^*` und :math:`L_2 \subseteq \Sigma_2^*` zweier Sprachen. :math:`L_1` ist polynomell auf :math:`L_2` reduzierbar, :math:`L_1 \leq_p L_2`, falls eine Turingmaschine :math:`M` existiert mit :math:`\text{Time}_M(n) \in O(n^k)` für ein :math:`k \in \mathbb{N}`, die für eine Eingabe :math:`x \in \Sigma_1^*` ein Wort :math:`M(x) \in \Sigma_2^*` berechnet mit :math:`x \in L_1 \Leftrightarrow M(x) \in L_2`.

:math:`L_1 \leq_p L_2` bedeutet, dass :math:`L_2` mindestens so schwer ist (bezüglich der Lösbarkeit in polynomieller Zeit) wi :math:`L_1`.

Wenn :math:`L_1 \leq_p L_2` gilt, dann könnte man eine polynomielle Turingmaschine :math:`B` für :math:`L_2` dafür verwenden, eine polynomielle Turingmaschine :math:`A` für :math:`L_1` zu bauen:

**Schema der Reduktion:**

.. image:: 12_3.jpg

**Definition:** Eine Sprache :math:`L` heisst **NP-schwer**, falls für alle Sprachen :math:`L' \in NP` gilt, dass :math:`L' \leq_p L`

Eine Sprache :math:`L` heisst **NP-Vollständig**, falls:

1. :math:`L \in NP`
2. :math:`L` ist NP-schwer

Die Menge aller NP-Vollständigen Sprachen betrachen wir jetzt die gesuchte Teilklasse von schwersten Entscheidungsproblemen in NP.

**Beobachtung:** Wenn es gelingt für ein NP-schweres :math:`L` nachzuweisen, dass :math:`L\in P`, dann gilt :math:`P=NP`

Ein erstes NP-vollständiges Problem
-----------------------------------

**Definition:** Boolesche Formeln sind induktiv definiert

  1. Die konstanten 0 und 1 und die Variabeln :math:`x_1, ..., x_n` sind Boole'sche Formeln.
  2. NEGATION:
  
    wenn :math:`\phi` eine Boole'sche Formel ist, dann ist auch :math:`\neg \phi`
  
  3. KONJNKTION, UND:
  
    Wenn :math:`\phi` und :math:`\psi` Boole'sche Formeln sind, dann auch :math:`(\phi \wedge \psi)`
  
  4. DISJUNKTION, ODER:
  
    Wenn :math:`\phi` und :math:`\psi` Boole'sche Formeln sind, dann auch :math:`(\phi \vee \psi)`


**Konventionen zur Klammerersparnis:**

* :math:`\neg` bindet stärker als :math:`\wedge` und :math:`\vee`
* :math:`\wedge` bindet stärker als :math:`\vee`
* statt :math:`\neg x_i` schreiben wir :math:`\bar{x_i}`

**Definition:** Eine Boole'sche Formel ist in konjunktiver Normalform (KNF), wenn sie eine Konjunktion von Disjunktionen von einfachen und negierten Variabeln ist.

**Beispiel:** :math:`(x_1 \vee x_2 \vee \bar{x_4}) \wedge (x_5 \vee x_2) \wedge (\bar{x_1} \vee \bar{x_3})`

**Definition:** Eine **Belegung** ist eine Funktion, die jeder Variablen einen Wert aus :math:`\{0,1\}` zuordnet.

Eine Belegung **erfüllt** eine Formel :math:`\phi`, wenn die Auswertung der Formel nach den üblichen Regeln der Aussagenlogik den Wert 1 ergibt.

Eine Formel heisst **erfüllbar** wenn sie eine erfüllende Belegung hat.

**Definition:** SAT ist das Problem zu entscheiden, ob eine gegebene Formel in KNF erfüllbar ist.

**Theorem:** (**Satz von Cook**)

SAT ist NP-Vollständig.

**Beweisidee:**

1. :math:`SAT \in NP`: p-Verifizierer für SAT:

  Zeuge :math:`l_1, l_2,..., l_n` mit :math:`l_i=1`, falls :math:`x_i=1` für eine erfüllbare Belegung und :math:`l_i=0` analog.
  
  Prüfen: polynomiell

2. **SAT ist NP-schwer:**

  :math:`L \leq_p SAT` **für alle** :math:`L \in NP`:
  
  Kodiere die Berechnung einer polynomialzeitbeschränkten nichtdeterministischen Turingmaschine durch eine KNF-Formel.

Nachweis der NP-Vollständigkeit weiterer Probleme durch Reduktion auf SAT
-------------------------------------------------------------------------

(und andere Probleme, die NP-vollständig sind)

**Satz:** Wenn :math:`P_1` NP-vollständig ist und :math:`P_2` in NP enthalten ist und eine polynomielle Reduktion von :math:`P_1 \leq_p P_2` existiert, dann ist :math:`P_2` NP-vollständig.

**Theorem:** CLIQUE ist NP-vollständig

**Beweis:**

1. :math:`\text{CLIQUE} \in NP`: siehe vorher
2. :math:`\text{SAT} \leq_p CLIQUE`

  Sei :math:`\phi = F_1 \wedge F_2 \wedge ... \wedge F_m` mit :math:`F_i = l_{i1} \vee ... \vee l_{ik_i}`, :math:`k_i \in \mathbb{N}` für :math:`1 \leq i \leq m` eine Formel in KNF.
  
  Konstruiere Eingabe :math:`(G,k)` für CLIQUE, so dass: :math:`\phi \in SAT \Leftrightarrow (G,k) \in \text{CLIQUE}`.
  
  Setze :math:`k=m`.
  
  :math:`G=(V,E)` mit :math:`V=\{[i,j] | 1 \leq i \leq m, 1 \leq j \leq k_i\}` (ein Knoten für jedes Auftreten eines Literals in :math:`\phi`)
  
  :math:`E = \left \{ \{[i,j], [r,s]\} | [i,j], [r,s] \in V, i \neq j, l_{ij} \neq l_{rs} \right \}` (Kanten zwischen Knoten aus unterschiedlichen Klauseln, falls Literale nicht Negation voneinander sind.)
  
**Beispiel:**

:math:`\phi = (x_1 \vee x_2) \wedge (x_1 \vee \bar{x_2} \vee \bar{x_3}) \wedge (\bar{x_1} \vee x_3) \wedge (\bar{x_2})`

.. image:: 12_4.jpg

Konstruktion polynomiell.

Bleibt zu zeigen: :math:`\phi \text{ erfüllbar} \Leftrightarrow G \text{ enthält Clique der Grösse } k`

**Idee:** Keine Kante zweischen :math:`x` und :math:`\bar{x}`

  :math:`\Rightarrow` Jede Clique in :math:`G` entspricht einer Menge von gleichzeitig auf 1 setzbaren Literalen.
  
  :math:`\Rightarrow` Clique der Grösse :math:`k` enthält einen Knoten Pro Klausel, also ist jede Klausel erfüllt.

Umgekehrt erfüllende Belegung definiert eine Clique der Grösse :math:`k`.

**Definition:** Vertex-Cover-Problem (VC)

**Gegeben:** Ungerichteter Graph :math:`G=(V,E)`, natürliche Zahl :math:`k \leq |V|`

**Frage:** Gibt es eine Menge :math:`S \subseteq V` mit :math:`|S| = k`, so dass jede Kante mindestens einen Endpunkt in :math:`S` hat?

**Beispiel:**

.. image:: 12_5.jpg

:math:`k=4`

:math:`S = \{v_1, v_4, v_5, v_6\}` ist ein Vertex-Cover

**Theorem:** :math:`\text{CLIQUE} \leq_p VC`

**Beweis:** Sei :math:`G=(V,E)` und :math:`k \in \mathbb{N}` eine Eingabe des Clique-Problems. Wir konstruieren hieraus eine Eingabe für das VC wie folgt:

 :math:`(\bar{G}, m)`, wobei :math:`m:= |V| - k`
 
   :math:`\bar{G} = (V, \bar{E})`, wobei :math:`\bar{E}= \left\{\{u,v\} | u,v \in V, u \neq v, \{u,v\} \notin E \right\}`
   
**Beobachtung:** Falls :math:`S` eine Clique in :math:`G` ist, dann ist :math:`V-S` ein Vertex-Cover in :math:`\bar{G}` und umgekehrt.

:math:`\Rightarrow (G,k) \in \text{CLIQUE} \Leftrightarrow (\bar{G}, m) \in VC`