=======================
Endliche Automaten (EA)
=======================
Unterscheidung:
~~~~~~~~~~~~~~~
* deterministische EA: Automat kann zu einem Zeitpunkt nur einen Zustand annehmen.
* nicht deterministische EA: Automat kann gleichzeitig mehrere Zustände besitzen.

Beispiel:
~~~~~~~~~
DEA zum Erkennen eines Musters aba:
..image:: 1_1.jpg

**Zustände** speichern das bereits gelesene Teilmuster:

:math:`q_0`: noch nichts vom Teilwort aba gelesen

:math:`q_1`: a von aba glesen

:math:`q_2`: ab von aba gelesen

:math:`q_3`: aba gelesen, also akzeptiern

**Transitionen** (Zustandsübergänge) Beschreiben die Änderungen beim Lesen eines Zeichens des Wortes.

..image:: 1_2.jpg

**Def**: Ein DEA A wird beschrieben durch :math:`A=(Q,\sum,q_0,F)`, wobei:

* Q ist eine endliche **Menge von Zuständen**
* :math:`\sigma` ist das **Eingabealphabet**
* :math:`q_0` ist der Startzustand, :math:`q_0 \in Q`
* F ist die Menge von **Endzuständen** (akzeptierende Zustände), :math:`F \leq Q`.
* :math:`\delta \times \sigma \rightarrow Q` ist die **Transitionsfunktion** (Übergangsfunktion) die für jeden Zustand und jedes Eingabesymbol einen eindeutigen Folgezustand definiert.

**Beispiel** (von Vorher)

:math:`A=(\{q_0, q_1, q_3,\},\{a,b\}, \delta, q_0, \{q_3\})`, wobei :math:`\delta` gegeben ist durch:

:math:`\delta (q_0, a) = q_1` :math:`\delta (q_0, b) = q_0`

:math:`\delta (q_1, a) = q_1` :math:`\delta (q_1, b) = q_2`

:math:`\delta (q_2, a) = q_3` :math:`\delta (q_2, b) = q_0`

:math:`\delta (q_3, a) = \delta (q_3, b) = q_3`

**Transitionstabelle** (einfachere Darstellung)

..image:: bild1.jpg

Die Transitionstabelle enthält alle Informationen über einen DEA. Meist ist aber die graphische Darstellung übersichtlicher.

..image:: 1_3.jpg

**Ziel:** Automaten zur Beschreibung von Sprachen verwenden.

**Definition:** Sei :math:`A=(Q,\sigma,\delta, q_0, F)` ein DEA, :math:`w \in \sigma^*` ein Wort.

Die **Berechnung** von A auf w ist die Folge von Zuständen, die A beim Lesen von w durchläuft, also für :math:`w=a_1 a_2 ... a_k`

..image:: 1_4.jpg

**Beispiel**

Berechnung von A auf w=abbaba:

..image:: 1_5.jpg

**Schreibweise:** Erweiterung von :math:`\delta` auf Wörter (erweiterte Übergangsfunktion)

:math:`\delta: Q \times \sigma^* \rightarrow Q` ist rekursiv definiert wie folgt:

* :math:`\hat{\delta}(q,a) = \delta(q,a)` für alle :math:`q \in Q, a \in \sigma`
* :math:`\hat{\delta}(q, xa) = \delta(\delta(q,x), a)` für alle :math:`q \in Q, x \in \sigma^*, a \in \sigma`

Anschaulich: :math:`\hat{\delta} (q,w)` bestimmt, in welchem Zustand A endet, wenn er vom Zustand q aus das Wort w liest.

**Definition:** Sei :math:`A=(Q,\sigma, \delta, q_0, F)` ein DEA. Die von A **akzeptierte Sprache** :math:`L(A) \leq \sigma^*` ist die Menge aller :math:`w \in \sigma^*`, so dass :math:`\hat{\delta} (q_0, w) \in F`.

**Anschaulich:** die Menge aller Wörter, die den DEA vom Anfangszustand aus in einen Endzustand führen.

**Beispiel:** :math:`\hat{\delta}(q_0, babbaba) = q_3 \in F`

(w wird von A akzepiert)

**Definition:** :math:`\mathcal{L}(DEA)=\{L(A)| \text{A ist ein DEA}\}`

ist die Klasse der Sprachen, die von DEAs akzeptiert werden. Man nennt sie die **Klasse der regulären Sprachen** und :math:`L \in \textit{L}(DEA)` wird **regulär** genannt.

**Beispiel:** DEA A entwerfen, der die Sprache :math:`L=\{w \in \{0,1\}^*|\text{w enthält eine gerade Anzahl von Nullen und eine gerade Anzahl von Einen enthalten}\}`

**Idee:** 4 Zustände, die speichern, wieviele Nullen und Einsen modulo 2 bereits gelesen wurden.

:math:`q_00`: gerade # Nullen, gerade # Einsen

:math:`q_01`: gerade # Nullen, ungerade # Einsen

:math:`q_10`: ungerade # Nullen, gerade # Einsen

:math:`q_11`: ungerade # Nullen, ungerade # Einsen

..image:: 1_6.jpg

:math:`\hat{\delta}(q_00, 011011) = q_00`
