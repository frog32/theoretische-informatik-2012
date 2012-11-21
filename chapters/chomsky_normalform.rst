======================
Die Chomsky-Normalform
======================

Definition (Chomsky-Normalform)

Sei :math:`G = (\Sigma, N, P, S)` eine kontextfreie Grammatik.

:math:`G` is in Chomsky-Normalform, falls :math:`P \subseteq N \times (N \cdot N \cup \Sigma)`, das heisst, falls alle Regeln die Form :math:`A \rightarrow BC` oder :math:`A \rightarrow a` haben für :math:`A,B,C \in N, a \in \Sigma`.

**Ziel:** Umwandlung einer beliebigen kontextfreien Grammatik in Chomsky-Normalform.

**Theorem** Zu jeder kontextfreien Grammatik :math:`G` mit :math:`\epsilon \notin L(G)` existiert eine äquivalente Grammatik :math:`G'` in Chomsky-Normalform.

Sei :math:`G = (\Sigma, N, P, S)` eine  :math:`\epsilon`-freie, reduzierte kontextfreie Grammatik ohne Kettenregeln mit :math:`\epsilon \notin L(G)`.

**Beweis:** Sei :math:`G` eine :math:`\epsilon`-freie, reduzierte kontextfreie Grammatik ohne Kettenregeln.

Forme alle Regeln, die noch nicht die gewünschte Form haben um: Regeln der Form :math:`A \rightarrow X_1 X_2 ... X_m, m \geq 2, X_i \in \Sigma \cup N`

1. Falls :math:`X_i \in \Sigma`, dann ersetze :math:`X_i` durch neues Nichtterminal :math:`C_{X_i}` und füge die Regel :math:`C_{X_i} \rightarrow X_i` hinzu.

2. Nach Schritt 1 haben alle nicht passenden Regeln die Form  :math:`A \rightarrow B_1 B_2 ... B_m` für ein :math:`m \geq 3` und :math:`B_i \in N`

  Zur Umformung dieser Regeln definiere neue Nichtterminale :math:`D_1, ..., D_{m-1}` und ersetze die Regel durch folgende Regeln: :math:`A \rightarrow B_1 D_1, D_1 \rightarrow B_2 D_2` ... :math:`D_{m-3} \rightarrow B_{m-2} D_{m-2}`, :math:`D_{m-2} \rightarrow B_{m-1} B_m`

**Beispiel:** :math:`G = (\{a,b\}, \{S,A,B\}, P, S)` mit :math:`P = \{ S \rightarrow bA, S \rightarrow aB, A \rightarrow bAA, A \rightarrow aS, A \rightarrow a, B \rightarrow aBB, B \rightarrow bS, B \rightarrow b\}`

1. .. image:: 8_1.jpg

2. Noch nicht in Chomsky-Normalform: :math:`A \rightarrow C_b AA` und :math:`B \rightarrow C_a BB`

  .. image:: 8_2.jpg

:math:`\Rightarrow` Äquivalente kontextfreie Grammatik :math:`G'` in Chomsky-Normalform

:math:`G' = (\{a,b\}, \{S,A,B,C_a, C_b, D_1, E_1\}, P', S)` mit :math:`P' = \{ S \rightarrow C_bA, S \rightarrow C_aB, A \rightarrow C_bD_1, A \rightarrow C_aS, A \rightarrow a, B \rightarrow C_aE_1, B \rightarrow C_bS, B \rightarrow b, C_a \rightarrow a, C_b \rightarrow b, D_1 \rightarrow AA, E_1 \rightarrow BB \}`

Anwendung der Chomsky-Normalform
--------------------------------

Überprüfung, ob ein gegebenes Wort in der Sprache der Grammatik enthalten ist. (sogenantes Wortproblem)

**Motivation** Ist gegebenes Programm syntaktisch korrekt.

**CYK-Algorithmus** (Cocke, Younger, Kasami)

Algorithmus basiert auf dynamischer Programmierung, d.h. Zusammensetzen der Lösung aus Teillösungen.

Sei :math:`G` eine kontextfreie Grammatik in Chomsky-Normalform.

Sei :math:`w = a_1a_1 ... a_n \in \Sigma^n`.

**Idee:** Bestimme für alle Teilwörter :math:`a_i ... a_j` von :math:`w` die Menge :math:`V(i,j)` aller Nichtterminale :math:`X \in N`, so dass :math:`X \overset{*}{\Rightarrow} a_i ... a_j`.

Dann ist :math:`w \in L(G)` genau dann, wenn :math:`S \in V(1,n)`

**Darstellung als Tabelle**

.. image:: 8_3.jpg

**Beispiel:** :math:`G=(\{a,b\}, \{S,A,B,C\}, P, S)` mit :math:`P=\{ S \rightarrow AB, S \rightarrow BC, A \rightarrow BA, A \rightarrow a, B \rightarrow CC, B \rightarrow b, C \rightarrow AB, C \rightarrow a\}` und :math:`w=bbab`

1. Bestimmung der V-Mengen für Teilwörter der Länge 1.

  Für alle :math:`i \in \{1, ..., n\}` gilt :math:`V(i,i) = \{x \in N | X \rightarrow a_i \in P\}`
  
  Beispiel:
  
    :math:`V(1,1) = \{B\}`, da :math:`B \rightarrow b \in P`

    :math:`V(2,2) = \{B\}`
    
    :math:`V(3,3) = \{A, C\}`

    :math:`V(4,4) = \{B\}`

2. Bestimmung der V-Mengen für alle Teilwörter der Länge 2.

  :math:`a_i | a_{i+1}`
  
  **Idee** Aufteilung eines Teilwortes in zwei kürzere und Zusammensetzen der Lösungen.
  
  Beispiel:
  
    :math:`V(1,2) = \{ X \in N | X \rightarrow YZ \in P \text{ mit } Y \in V(1,1) \text{ und } Z \in V(2,2)\} = \varnothing`

    :math:`V(2,3) = \{ X \in N | X \rightarrow YZ \in P \text{ mit } Y \in V(2,2) \text{ und } Z \in V(3,3)\} = \{S, A\}` da :math:`S \rightarrow BC` und :math:`A \rightarrow BA`

    :math:`V(3,4) = \{ X \in N | X \rightarrow YZ \in P \text{ mit } Y \in V(3,3) \text{ und } Z \in V(4,4)\} = \{C, S\}` da :math:`S \rightarrow AB` und :math:`C \rightarrow AB`


Allgemeine Regel für längere Teilwörter:

  Für alle :math:`i,j \in \{1,...,n\}` mit :math:`i<j` ist :math:`V(i,j) = \{X \in N | \text{ es existiert ein } k \text{ mit } i \leq k \lt j, \text{ so dass } X \rightarrow YZ \in P \text{ mit } Y \in V(i,k) \text{ und } Z \in V(k,j)\}`
  
  Beispiel
  
    :math:`V(1,3): bba` lässt sich als b ba (k=1) oder als bb a (k=2) aufteilen.
    
    :math:`V(1,3) = \{ X \in N | X \rightarrow YZ \text{ mit } [Y \in V(1,1) \text{ und } Z \in V(2,3)] \text{ oder } [Y \in V(1,2)  \text{ und } Z \in V(3,3)]\} = \{A\}` da :math:`A \rightarrow BA`