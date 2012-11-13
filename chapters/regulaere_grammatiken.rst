====================
Reguläre Grammatiken
====================

**Idee:** Mechanismus zur Erzeugung aller Wörter aus einer Sprache.

**Beispiel:** :math:`L=\left \{1w | w\in 0^* \right\} \leq \left \{0,1\right\}^*`

:math:`= \left\{1, 10, 100, 1000, ... \right\}`

Vorgehen bei der Konstruktion solcher Wörter:

* 1 an den Anfang setzen
* beliebig viele 0en auffüllen

Regeln:

* start :math:`\rightarrow` 1N (N ist Platzhalter für 0en)
* N :math:`\rightarrow` 0N, N :math:`\rightarrow\epsilon`

Konstruktion von 1000:

start :math:`\Rightarrow 1N \Rightarrow 10N \Rightarrow 100N \Rightarrow 1000N \Rightarrow 1000`

**Definition:** Eine rechtslineare Grammatik G erzeugt alle Wörter einer Sprache buchstabenweise von links nach rechts. Sie wird beschrieben durch :math:`G=(N,T,P,S)`, wobei

* :math:`T` das Terminalalphabet (Alphabet der Sprache)
* :math:`N` das Nichtterminalalphabet (Menge von Hilfssymbolen)
* :math:`P \leq N \times (T \cdot N \cup T \cup \{\epsilon\})` die menge von Produktionen (Regeln).

  Für :math:`p=(l,r) \in P` heisst l die linke Seite von P und r die rechte Seite von P.
  
  Wir schreiben statt :math:`p=(l,r)` auch :math:`l \rightarrow r`

* :math:`S \in N` ist das Startsymbol

**Anschauung:** Produktion :math:`p = l \rightarrow r` ist eine Ersetzungsregel. In einem Wort über :math:`T \cup N` wird durch Anwendung von p ein Vorkommen von l durch r ersetzt.

**Beispiel:** :math:`G=(\left\{S,A,B\right\}, \{0,1\}, P, S)`, wobei

:math:`P=\{S\rightarrow 0S, S\rightarrow 1S, S\rightarrow 0A, A\rightarrow 0B, A \rightarrow 1B, B \rightarrow 0, B \rightarrow 1\}`

**Definition:** Sei :math:`G=(N, T, P, S)` eine rechtslineare Grammatik. Ein Ableitungsschritt in G ist eine Relation :math:`\Rightarrow \leq T^*N \times T^*(N \cup \epsilon)`  definiert durch :math:`uA \Rightarrow uw` genau dann, wenn :math:`A \rightarrow w \in P`, wobei :math:`u \in T^*, A \in N, w \in TN \cup T \cup \{ \epsilon \}`

Eine Ableitung ist eine endliche Folge von Ableitungsschritten.

Formal ist :math:`\Rightarrow^*` die reflexive, transitive Hülle von :math:`\Rightarrow`

Die von G erzeugte Sprache ist definiert als :math:`L(G) = \left\{w \in \Sigma^* | S \Rightarrow^* w \right\}`, also die Menge aller Wörter, die aus S in endlich vielen Ableitungsschritten erzeugt werden können.

Zwei Grammatiken :math:`G_1` und :math:`G_2` heissen äquivalent, falls :math:`L(G_1) = L(G_2)`.

**Beispiel:**

:math:`S \Rightarrow 0S \Rightarrow 01S \Rightarrow 011S \Rightarrow 0110A \Rightarrow 01101B \Rightarrow 011010`

:math:`\Rightarrow \in L(G)`

**Beispiel:** Ableitung von 0111?

.. image:: 5_1.jpg

:math:`0111 \notin L(G)`

**Definition:** :math:`\textit{L}_{rlin} = \left\{ L | \text{es ex. eine rechtslin. Gr mit} L=L(G)\right\}`

Vereinfachung rechtslinearer Grammatiken

3 Typen von Regeln:

1. :math:`A \rightarrow aB`
2. :math:`A \rightarrow a`
3. :math:`A \rightarrow \epsilon`

**Zeige:** Regel 2 kann vermieden werden:

Ersetze :math:`A \rightarrow a` durch :math:`A \rightarrow aC` und :math:`C \rightarrow \epsilon`

Weitere vereinfachung: Es reicht eine Regel vom Typ 3, zusätzlich gegebenenfalls :math:`S \rightarrow \epsilon`, falls :math:`\epsilon \in L(G)`

Ersetze Regeln

:math:`A_1 \rightarrow a_1B_1, ... A_k \rightarrow a_kB_k`

und

:math:`B_1 \rightarrow \epsilon, ..., B_k \rightarrow \epsilon`

durch

:math:`A_1 \rightarrow a_1T, ..., A_k \rightarrow a_kT` und :math:`T \rightarrow \epsilon`

Äquivalenz von rechtslinearen Grammatiken und EA
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Theorem:** Zu jeder rechtslinearen Grammatik über :math:`T=\Sigma` existiert ein NEA A über :math:`\Sigma` mit :math:`L(A) = L(G)`.

**Beweis:** :math:`G=(N, \Sigma, P, S)` ohne Typ 2

NEA :math:`A = (Q, \Sigma, \delta, q_0, F)` mit

* :math:`Q=N`
* :math:`q_0 = S`
* :math:`F=\left\{X \in N | X \rightarrow \epsilon \in P \right\}`
* :math:`\delta` definiert durch: :math:`X \in \delta (Y, a) \Leftrightarrow Y \rightarrow aX \in P`

**Beispiel:** :math:`G = (\{S,A,B\}, \{a,b\}, P,S)` mit

:math:`P = \{S \rightarrow aB, S \rightarrow bA , A \rightarrow aB, B \rightarrow bA, A \rightarrow \epsilon, B \rightarrow \epsilon}`

NEA für :math:`L(G)`:

.. image:: 5_2.jpg

**Theorem:** Zu jedem DEA A über :math:`\Sigma` existiert eine rechtslineare Grammatik G über :math:`\Sigma = T` mit :math:`L(G)= L(A)`.

**Beweis:** :math:`A=(Q, \Sigma, \delta, q_0, F)`

:math:`G=(N, \Sigma, P, S)` mit

* :math:`N=Q`
* :math:`S=q_0`
* :math:`P` definiert durch :math:`p \rightarrow aq \in P \Leftrightarrow \delta(p,a) = q`

  :math:`q \rightarrow \epsilon \in P \Leftrightarrow q \in F`

**Beispiel:**

.. image:: 5_3.jpg


:math:`G = (\{a_0, a_1, a_2, a_3\}, \{a,b\}, P, q_0)`

mit

:math:`P = \{q_0 \rightarrow bq_0, q_0 \rightarrow aq_1, a_1 \rightarrow aq_1, ..., q_3 \rightarrow \epsilon}`