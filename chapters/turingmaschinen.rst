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

:math:`\mathcal{L}_{RE} = \left \{ L(M) | \text{M ist eine TM} \right \}` ist die Menge aller rekursiv aufzählbaren Sprachen.

**Beobachtung:** Eine Berechnung einer TM kann unendlich sein. Wenn das Wort nicht inder der Sprache ist, kann :math:`M` entweder verwerfen oder unendlich lange rechnen.

Eine Sprache :math:`L` heisst **rekursiv** (entscheidbar), wenn es eine TM :math:`M` gibt mit :math:`L = L(M)`, die auf jeder Eingabe :math:`w` hält und zwar in einem akzeptierenden Zustand für alle :math:`w \in L` und in einem nichtakzeptierenden für :math:`w \notin L`

:math:`\mathcal{L}` = Menge aller rekursiven Sprachen :math:`\mathcal{L}_R \subseteq \mathcal{L}_{RE}`

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


Mehr-Band-Turing-Maschine
-------------------------

**Theorem**

Eine Turingmaschine mit mehreren Bändern kann Simuliert werden durch eine Turingmaschine mit einem Band.

**Idee**

Grösseres Alphabet, dass alle Bänder und Kopfpositionen beschreibt.

Universelle Turingmaschine
--------------------------

**Ziel:** Konstruktion einer Turingmaschine, die alle anderen Turingmaschinen simulieren kann.

  Sei :math:`M` eine beliebige Turingmaschine mit einem Band.
  
  :math:`M` kann vollständig beschrieben werden durch die Transitionstabelle.
  
  Transition ist darstellbar als ein Wort
  
  .. image:: 10_4.jpg
  
Turingmaschine :math:`M` darstellbar als Wort

:math:`Kod(m) = q_0\#q_{accept}\#q_{reject}`

über dem Alphabet :math:`Q \cup \Gamma \cup \{L,R,N\} \cup \{\#\}`

weobei :math:`t_i` die wie oben kodierten Transitionen von :math:`M` sind.

:math:`Kod(M)` heisst Kodierung von M.

**Bemerkung** Im Prinzip ist auch eine Binärkodierung möglich.

**Konstruktion einer universellen Turingmaschine U**

**Eingabe:** :math:`Kod(M)\#\#w` für eine Turingmaschine :math:`M`, die auf dem Wort w Simuliert werden soll.

**Arbeitsweise von U:**

1. U überprüft ob Kod(M) eine gültige Kodierung einer TM ist. Falls nicht, verwirft die Eingabe.
2. U schreibt die Anfangskonfiguration von :math:`M` auf :math:`w` auf das Arbeitsband.
3. U simuliert die Berechnung von :math:`M` auf :math:`w` wie folgt:

  Solange der Zustand in der aktuellen Konfiguration von M nicht :math:`q_{accept}` oder :math:`q_{reject}` ist, generiere die Nachfolgekonfiguration von :math:`M` auf :math:`w` aus dem Arbeitsband. (suche passende Transition in der Eingabe und führe diese Änderungen druch)

4. Wenn der Zustand von :math:`M` :math:`a_{accept}` is, dann akzeptiere die Eingabe, sonst verwerfe.

**Bemerkung** Falls :math:`M` auf :math:`w` unendlich lange läuft, dann auch :math:`U`.

**Behauptung:** Turingmaschinen sind ein geeignetes formales Modell zur Beschreibung der Rechenstärke realer Computer.

**Hierfür:** Zeige, wie man ein Programm einer beliebigen Programmiersprache durch eine äquivalente Turingmaschine darstellt.

**Beobachtung** Es reicht, eine solche Transformation für Assembler-Programme anzugeben.

**Idee der Transformation**

- Ein Band für Programmcode (Programmzeile 1 # Programmzeile 2 # ... # Initiale Registerbelegung) Eingabeband
- Ein Band für Register (Register 1 # Register 2 # ...) Arbeitsband zur Simulation der Register
- Hauptspeicherband
- Arbeitsband für Nebenrechnungen (Addressberechnungen etc.)

**Beobachtung:** Alle bisher entwickelten Modelle zur Beschreibung der algorithmischen Lösbarkeit sind äquivalent zum Modell der Turingmaschine.

:math:`\Rightarrow` **Church'sche These**

Das Modell der Turingmaschine die immer hält ist eine geeignete Formalisierung des intuitiven Begriffs "Algorithmus", das heisst die Klasse der rekursiven (entscheidbaren) Sprachen stimmt mit der Klasse der algorithmisch erkennbaren Sprachen überein.