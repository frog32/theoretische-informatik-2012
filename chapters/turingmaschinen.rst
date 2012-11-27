===============
Turingmaschinen
===============

**Motivation**

* Zeigen, dass es Probleme gibt die nicht lösbar (entscheidbar) sind. (Berechenbarkeit)
* Zeigen, dass es Probleme gibt die nicht handbar sind (Komplexitätstheorie)

**Ziel:** Berechnungsmodell, das so allgemein wie möglich ist, aber trotzdem einfach aufgebaut ist.

:math:`\rightarrow` Turingmaschine

Das Modell der Turingmaschine
-----------------------------

.. image:: 10_1.jpg

Situation am Anfang einer Berechnung

- Auf dem Band steht die Eingabe, der Rest ist leer (:math:`\visablespace`)
- Regelwerk ist im Anfangszustand :math:`q_0`

**Definition:** Eine Turingmaschine (TM) ist ein 6-Tupel :math:`M = (Q, \Sigma, \Gamma, \delta, q_0, F)` wobei:

* :math:`Q`: Zustandsmenge
* :math:`\Sigma`: Eingangsalphabet, :math:`\textvisiblespace \notin \Sigma`
* :math:`\Gamma`: Arbeitsalphabet, :math:`\textvisiblespace \notin \Gamma, \Sigma \subset \Gamma`
* :math:`q_0`: Angfangszustand
* :math:`F`: Menge der akzeptierenden Zustände
* :math:`\delta`: Transitionsfunktion

mit

:math:`\delta: Q \times \Gamma \rightarrow Q \times \Gamma \times \{L,R,N\}`

* :math:`Q`: aktueller Zustand
* :math:`\Gamma`: Symbol auf dem Band
* :math:`Q`: Folgezustand
* :math:`\Gamma`: neues Symbol auf Band
* :math:`\{L,R,N\}`: Bewegung des Kopfes L=links, R=rechts, N=stehenbleiben

* Damit die Turingmaschine halten kann, müssen nicht alle Transitionen vorhanden sein.

**Konfiguration einer TM**

.. image:: 10_2.jpg

**Berechnung einer Turingmaschine auf der Eingabe x**

Folge von Konfigurationen :math:`k_1,...,k_n`, so dass

- :math:`k_1` ist Anfangsposition :math:`(q_0, w)` mit Kopf auf dem ersten Symbol der Eingabe.
- :math:`k_{i+i}` entsteht aus :math:`k_i` durch die Anwendung einer Transition von M.

Die Turingmaschine M akzeptiert das Wort x, falls die Berechnung von M auf x in einem akzeptierenden Zustand hält.

:math:`L(M) = \left \{ w \in \Sigma^* | M \text{ akzeptiert } w \right \}`

Eine Sprache :math:`L` heisst rekursiv aufzählbar (semi-entscheidbar), falls es eine TM :math:`M` gibt, so dass :math:`L = L(M)`.

:math:`\mathscr{L}_{RE} = \left \{ L(M) | \text{M ist eine TM} \right \}` ist die Menge aller rekursiv aufzählbaren Sprachen.

**Beobachtung:** Eine Berechnung einer TM kann unendlich sein. Wenn das Wort nicht inder der Sprache ist, kann :math:`M` entweder verwerfen oder unendlich lange rechnen.

Eine Sprache :math:`L` heisst **rekursiv** (entscheidbar), wenn es eine TM :math:`M` gibt mit :math:`L = L(M)`, die auf jeder Eingabe :math:`w` hält und zwar in einem akzeptierenden Zustand für alle :math:`w \in L` und in einem nichtakzeptierenden für :math:`w \notin L`

:math:`\mathscr{L}` = Menge aller rekursiven Sprachen :math:`\mathscr{L}_R \subseteq \mathscr{L}_{RE}`

**Beispiel:** TM für :math:`L = \{a^kb^kc^k | k\geq 0\}`

  **Idee:**
  
.. code-block::

  wiederhole solange es unmarkierte a's gibt.
    markier das a
    Gehe nach rechts bis zum ersten unmarkierten b und markiere es.
    Gehe nach rechts bis zum ersten unmarkierten c und markiere es.
    Gehe links bis zum linksten unmarkierten a
  überprüfe von links nach rechts ob alle Symbole markiert sind.
  
:math:`\underline{a}abbcc \rightarrow a'\underline{a}bbcc \rightarrow a'a\underline{b}bcc \rightarrow a'ab'\underline{b}cc \rightarrow a'ab'b\underline{c}c \rightarrow a'ab'\underline{b}c'c \rightarrow a'a\underline{b'}bc'c \rightarrow a'\underline{a}b'bc'c \rightarrow \underline{a'}ab'bc'c \rightarrow a'\underline{a}b'bc'c \rightarrow a'a'\underline{b'}bc'c \rightarrow a'a'b'\underline{b}c'c \rightarrow a'a'b'b'\underline{c'}c \rightarrow a'a'b'b'c'\underline{c} \rightarrow a'a'b'b'\underline{c'}c' \rightarrow \text{überprüfen} \rightarrow \text{akzeptiert}` 

**Graphische Darstellung**

.. image:: 10_3.jpg
