=================================
Asymptotische Komplexitätsmessung
=================================

O-Notation
----------

(Landau Symbol)

Seien :math:`f,g \mathbb{N} \rightarrow \mathbb{R}^+` zwei Funktionen. Dann gilt :math:`f(n) \in O(g(n))`, falls ein :math:`n_0 \in \mathbb{N}` und ein :math:`c \in \mathbb{N}` existiert, so dass für :math:`n \geq n_0` gilt :math:`f(n) \leq g(n)`

:math:`f(n) \in \Omega(g(n))`, falls ein :math:`n_0 \in \mathbb{N}` und ein :math:`d \in \mathbb{N}` existiert, so dass für alle :math:`n \geq n_0` gilt: :math:`f(n) \geq \frac{1}{d} g(n)`.

:math:`f(n) \in \Theta(g(n))`, falls ein :math:`f(n) \in O(g(n))` und :math:`f(n) \in \Omega(g(n))` gilt.

**Beispiel:**

1. :math:`7n+5 \in O(n)`
2. :math:`\frac{1}{2}n^2 + 5n - 4 \in O(n^2)`
3. :math:`n log(n) \in O(n^2)`

**Algemeine Beobachtung:**

* konstante Vorfaktoren kann man weglassen
* Bei Polynomen ist nur die höchste Potenz entscheidend
* O-Notation ist transitiv:

  Aus :math:`f \in O(g(n))` und :math:`g \in O(h(n))` folgt :math:`f \in O(h(n))`

Komplexitätstheorie
-------------------

**Ziel:** Klassifizierung von (entscheidbaren) Problemen nach ihrer Schwierigkeit (**Komplexität**)

**Komplexitätstheorie:** Theorie der quantitativen Gesetze und Grenzen der algorithmischen Informationsverarbeitung.

Verschiedene Komplexitätsmasse
------------------------------

* Zeitkomplexität (Laufzeit des besten Programms, das das Problem löst)
* Platzkomplexität (Speicherplatzbedarf des besten Programms)
* Beschreibungskomplexität (Länge des kürzeste Programms)

**Im Formalismus der Turingmaschine:**

Sei :math:`M` eine Turingmaschine mit Eingabealphabet :math:`\Sigma`, die immer hält und sei :math:`w \in \Sigma^*`

Der Zeitbedarf von :math:`M` auf der Eingabe :math:`w` ist

:math:`Time_M(w) =` Anzahl der Konfigurationsübergänge in der Berechnung von :math:`M` auf :math:`w`

**Verallgemeinerung:** Zeitkomplexität in Abhängigkeit der Eingabelänge:

  Für :math:`n \in \mathbb{N}`
  
    :math:`Time_M(n) = max \left \{ Time_M(w)| |w| = n\right \}`
  
  der Zeitbedarf von :math:`M` auf Eingaben der Länge genau :math:`n` im schlechtesten Fall.

asymptotische Bestimmung von :math:`Time_M(n)`

O-Notation

Exkurs: alternatives Modell einer Turingmaschine

.. image:: 11_1.jpg

:math:`M=(Q, \Sigma, \Lambda, \delta, q_0, q_{accept}, q_{reject})`, wobei

* :math:`Q`: Zustandsmenge
* :math:`\Sigma`: Eingabealphabet, leersymbol :math:`\notin \Sigma, \cent, $ \notin \Sigma`,
* :math:`\Lambda`: Arbeitsalphabet, leersymbol :math:`\notin \Lambda`, :math:`\cent \Lambda` 
* :math:`q_0`: Anfangszustand
* :math:`q_{accept}`: akzeptierender Zustand
* :math:`q_{reject}`: verwerfender Zustand
* :math:`\delta`: Transitionsfunktion

:math:`\delta: Q \times (\Sigma \cup \{\cent,$\}) \times (\Lambda \cup \{\cent\})`

:math:`\rightarrow Q \times \{L,R,N\} x \Lambda`

**Beispiel:** Zeitkomplexität einer Turingmaschine zum Vergleich von zwei Wörtern :math:`x` und :math:`y` der Länge jeweils :math:`n`:

1. x auf das Arbeitsband kopieren :math:`O(n)`
2. Lesekopf auf Arbeitsband an den Anfang :math:`O(n)`
3. Zeichen für Zeichen vergleichen :math:`O(n)`

Total ist :math:`O(n)`

Zeitkomplexität auf Problemen
-----------------------------

im Allgemeinen nicht exakt bestimmbar

Seien :math:`f,g: \mathbb{N} \rightarrow \mathbb{R}^+`. Sei :math:`U` ein (entscheidbares) Problem.

* :math:`O(f(n))` ist eine obere Schranke für die Zeitkomplexität von :math:`U`, falls eine Turingmaschine :math:`M` existiert, die :math:`U` löst und eine Zeitkomplexität :math:`\in O(f(n))` hat.
* :math:`\Omega(g(n))` ist eine untere Schranke für die Zeitkomplexität von :math:`U`, falls für alle Turingmaschinen :math:`M` die :math:`U` lösen gilt, dass :math:`Time_M(n) \in \Omega(g(n))`

**Idee:** Zur Klassifizierung von Problemen nach Schwierigkeit

:math:`\rightarrow` verwende **relative Schwierigkeit**:

  "Wenn Problem A schnell lösbar wäre, dann auch tausend andere Probleme."

**Was heisst schnell lösbar?**

Ansatz: Problem :math:`U` heisst in Polynomzeit lösbar, wenn es eine obere Schranke :math:`O(n^c)` gibt für eine Konstante :math:`c \geq 1`

**Definition:** Die Klasse aller in Polynomzeit entscheidbaren Sprachen nennen wir **P**.

Nichtdererministische Turingmaschine
------------------------------------

Prinzipieller Aufbau:

.. image:: 11_1.jpg

**Formal:**

:math:`M=(Q, \Sigma, \Lambda, \delta, q_0, q_{accept}, q_{reject})`

wobei:

* :math:`\delta`: :math:`Q \times (\Sigma \cup \{\cent, $\}) \times (\Lambda \cup \{ \cent \})`

:math:`\rightarrow 2^{Q \times \{L,R,N\} \times \Lambda \times \{L,R,N\}}`

Menge aller Berechnungen einer nichtdeterministischen Turingmaschine kann dargestellt werden als Berechnungsbaum:

.. image:: 11_2.jpg

* Wurzel: Anfangskonfiguration
* Blätter: akzeptierende oder verwerfende Berechnungen

:math:`\rightarrow` NTM akzeptiert, wenn es einen Pfad im Baum gibt von der Wurzel zu einem akzeptierenden Blatt.

! Keine zusätzliche Ausdrucksstärke!

**Theorem:** Sei :math:`M` eine NTM. Dann gibt es eine äquivalente deterministische Turingmaschine :math:`A`, also eine DTM :math:`A` mit :math:`L(A) = L(M)`.

**Idee:** Breitensuche auf dem Berechnungsbaum.

:math:`A` arbeitet wie folgt: (2-Band-TM)

1. schreibt Arbeitskonfiguration auf das erste Arbeitsband
2. überprüft ob eine akzeptierende Konfiguration auf dem 1. Band.

  Falls ja: halten, akzeptieren

3. auf 2. Band: alle Nachfolgekonfigurationen.

  Falls es keine Nachfolgekonfigurationen gibt, hält :math:`A` und verwirft.

4. :math:`A` löscht das 1. Band, kopiert Inhalt des 2. auf das 1., löscht das 2. Band und geht zu Schritt 2.

:math:`\rightarrow` Falls :math:`M` eine akzeptierende Konfiguration erreicht, dann akzeptiert auch :math:`A`. Falls jede Berechnung von :math:`M` endlich ist, hält auch :math:`A`.

**Zeitkomplexität einer NTM:** Länge einer kürzesten akzeptierenden Berechnung.

**Definition:** Die Klasse aller von einer NTM in Polynomzeit entscheidbaren Sprachen nennen wir **NP**