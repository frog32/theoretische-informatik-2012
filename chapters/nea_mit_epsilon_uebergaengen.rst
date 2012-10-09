====================================
NEAs mit :math:`\epsilon`-Übergängen
====================================

**Beispiel:** Suche nach mehreren Mustern

:math:`L=\{w \in \{a,b\}^*|\text{w enthält eines der Teilwörter aba, abb, bab}\}`

NEA N mit :math:`L(N)=L` mit :math:`\epsilon`-Übergängen

.. image:: 2_1.jpg

**Beispiel:** :math:`\epsilon`-NEA, der Dezimalzahlen akzeptiert, die sich zusammensetzen aus:

* optionales "+" oder "-"
* Zeichenreihe von Ziffern
* Dezimalpunkt
* Zeichenreihe von Ziffern
* nur eine der Ziffernfolgen darf leer sein

**Definition:** ein NEA mit :math:`\epsilon`-Übergängen (:math:`\epsilon`-NEA) A wird beschrieben durch :math:`A=(Q,\sigma, \delta, q_0, F)`, wobei :math:`Q,\sigma, q_0, F` wie beim DEA definiert sind und

:math:`\delta: Q \times (\sigma \cup \{ \epsilon \}) \rightarrow 2^Q` die Transitionsfunktion ist.

**Annahme:** :math:`\epsilon \notin \sigma`

**Beispiel:** von vorher

:math:`E=(\{q_0, q_1, q_2, q_3, q_4, q_5\}, \{\cdot, +, -, 0, 1, ...,9\}, \delta, q_0, \{q_5\})`

.. image:: 2_3.jpg

**Ziel:** Zeigen, dass es zu jedem :math:`\epsilon`-NEA einen äquivalenten DEA gibt.

**:math:`\epsilon`-Hüllen**
===========================

**Idee:** Finde für jeden Zustand die Menge aller Zustände, die von dort aus nur mit :math:`\epsilon`-Übergängen erreichbar sind.

**Rekursive Definition:** Die :math:`\epsilon`-Hülle eines Zustands :math:`q \in Q` wird bezeichnet mit :math:`\epsilon-Hülle(q)` und ist definiert durch:

* :math:`q \in \epsilon-Hülle(q)`
* Falls :math:`p \in \epsilon-Hülle(q)`, dann auch jeder Zustand r, so dass :math:`r \in \delta (p,\epsilon)`

**Beispiel:** von vorher

:math:`\epsilon-Hülle(q_0) = \{q_0, q_1\}`

:math:`\epsilon-Hülle(q_1) = \{q_1\}`

:math:`\epsilon-Hülle(q_3) = \{q_3, q_5\}`

:math:`\epsilon-Hülle(q_4) = \{q_4\}`

:math:`\epsilon-Hülle(q_5) = \{q_5\}`

**Beispiel:**

.. image:: 2_7.jpg

Bestimme :math:`\epsilon-Hülle(q_1)`:

1. :math:`q_1 \in \epsilon-Hülle(q_1)`
2. Finde alle Zustände aus :math:`\delta(q_1, \epsilon) = \{q_2, q_4\}`
   :math:`\Rightarrow \{q_2, q_4\} \leq \epsilon-Hülle(q_1)`
3. :math:`\delta(q_2, \epsilon) = \{q3\}, \delta(q_4, \epsilon) = \varnothing \Rightarrow q_3 \in \epsilon-Hülle(q_1)`
4. :math:`\delta(q_3, \epsilon) = \{q_6\} \Rightarrow q_6 \in \epsilon-Hülle(q_1)`
5. :math:`\delta(q_6, \epsilon) = \varnothing`

:math:`\Rightarrow \epsilon-Hülle(q_1) = \{q_1, q_2, q_3, q_4, q_6\}`

**Definition:** :math:`\epsilon-Hülle` einer Menge S von Zuständen:

:math:`\epsilon-Hülle(S) = \bigcup\limits_{q \in S} \epsilon-Hülle(q)`

Erweiterung der Übergangsfunktion auf Wörter:
=============================================

**Idee:** Finde alle Pfade im Graphen, die mit dem Wort w beschriftet sind (mit belibig vielen :math:`\epsilon` dazwischen).

**Rekursive Definition:**

* :math:`\hat{\delta}(q, \epsilon) = \epsilon-Hülle(q)`
* :math:`\hat{\delta}(q, xa)` wird für :math:`x\in \sigma^*` und :math:`a \in \sigma` definiert durch:

  1. Sei :math:`\hat{\delta}(q,x)=\{p_1,...,p_k\}`
  2. Sei :math:`\bigcup\limits_{i=1}^{k} \delta(p_i, a) = \{r_1,...,r_m\}`
  3. Dann gilt :math:`\hat{\delta}(q, xa) = \epsilon-Hülle(\{r_1,...,r_m\}) = \bigcup\limits_{i=1}^{m} \epsilon-Hülle(r_i)`

**Beispiel:** :math:`\hat{\delta}(q_0, 5.6)`:

1. :math:`\hat{\delta}(q_0, \epsilon) = \epsilon-\text{Hülle}(q_0) = \{q_0, q_1\}`
2. :math:`\hat{\delta}(q_0, 5)`: :math:`\delta(q_0, 5) \cup \delta(q_1, 5) = \{q_1, q_4\}`
3. :math:`\hat{\delta}(q_0, 5.)`: :math:`\delta(q_1, .) \cup \delta(q_4, .) = \{q_2, q_3\}` :math:`\hat{delta}(q_0, 5.) = \epsilon-\text{Hülle}(q_2) \cup \epsilon-\text{Hülle}(q_3) = \{q_2, q_3, q_5\}`
4. :math:`\hat{\delta}(q_0, 5.6)`: :math:`\delta(q_2, 6) \cup \delta(q_3, 6) \cup \delta(q_5, 6) = \{q_3\}` :math:`\hat{\delta}(q_0, 5,6) = \epsilon-\text{Hülle}(q_3) = \{q_3, q_5\}`

:math:`q_5` ist akzeptierend :math:`\Rightarrow 5.6 \in L(E)`

**Definition:** Für einen :math:`\epsilon`-NEA :math:`E=(Q, \sigma, \delta, q_0, F)` ist :math:`L(E) = \{w | \hat{delta}(q_0, w) \cap F \neq \varnothing \}`

**Umwandlung von :math:`\sigma`-NEAs in DEAs**

:math:`\rightarrow \epsilon`-Übergänge eliminieren

Sei :math:`E=(Q_E, \sigma, \delta_E, q_0, F_E)` ein :math:`\epsilon`-NEA Konstruiert einen äquivalenten DEA :math:`D=(Q_D,\sigma, \delta_D, q_{0,D}, F_D)`:

* :math:`Q_D = 2^Q_E`

  Alle erreichbaren Zustände sind :math:`\epsilon`-abgeschlossene Teilmengen, d.h. Mengen :math:`S \leq Q_E`, so dass :math:`S=\epsilon-\text{Hülle}(S)`. D.h. jeder :math:`\epsilon`-Übergang von einem Zustand :math:`q \in S` führt zu einem Zustand, der auch in S liegt.

* :math:`q_{0,D} = \epsilon-\text{Hülle}(q_0)`
* :math:`F_D = \{S \in Q_D | S \cap F_E \neq \varnothing\}`
* :math:`\delta_D(S,a)` wird für alle :math:`S \in Q_D` und alle :math:`a \in \sigma` wie folgt berechnet:

  1. Sei :math:`S=\{p_1,...,p_k\}`
  2. Berechne :math:`\bigcup\limits_{i=1}^{k} \delta(p_i, a)= \{r_1,...,r_m\}`
  3. Dann ist :math:`\delta_D(S,a) = \bigcup\limits_{j=1}^{m} \epsilon-\text{Hüllen}(r_j)`

**Beispiel:** von vorher

Äquivalenter DEA D: Startzustand ist :math:`\epsilon-\text{Hülle}(q_0) = \{q_0, q_1\}`

Finde Folgezustände von :math:`\{q_0, q_1\}` für alle Symbole des Alphabets:

* "+", "-": Kein Übergang von :math:`q_1`, von :math:`q_0` nach :math:`q_1` :math:`\rightarrow \epsilon-\text{Hülle}(q_1) = \{q_1\}`
* ".": Kein Übergang von :math:`q_0`, von :math:`q_1` nach :math:`q_2` :math:`\rightarrow \epsilon-\text{Hülle}(q_2) = \{q_2\}`
* 0,1,...,9: Kein Übergang von :math:`q_0`, von :math:`q_1` nach :math:`q_1` oder :math:`q_4` :math:`\rightarrow \epsilon-\text{Hülle}(q_1, q_4) = \{q_1, q_4\}`

.. image:: 2_5.jpg

.. image:: 2_6.jpg

**Konvention:**

* Der Zustand :math:`\varnothing` wird auch Senkezustand (Abfallzustand) genannt und darf weggelassen werden.
* Darstellung eines DEA mit fehlenden Transitionen sind immer so zu verstehen, dass die fehlenden Transitionen in einen solchen Senkezustand führen.

**Zusammenfassung:** DEAs und :math:`\epsilon`-NEAs sind äquivalent.

.. image:: 2_7.jpg
