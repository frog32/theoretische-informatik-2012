===============
Kellerautomaten
===============

(Push-Down Automaten)

**Ziel:** Automatenmodell für kontextfreie Sprachen.

**Idee:** Nichtdeterministischer endlicher Automat mit Zusatzspeicher in Form eines Stacks (Keller).

.. image:: 9_1.jpg

**Arbeitsschritte:** (Übergänge)

Abhängig vom Zustand, gelesenem Eingabesymbol und oberstem Symbol auf dem Keller:

- Bestimme neuen Zustand
- Entferne oberstes Symbol auf dem Keller und Schreibe beliebig viele Symbole auf den Keller

Ein Kellerautomat wird beschrieben durch :math:`A=(Q, \sigma, \tau, \delta, q_0, \bot, F)` wobei:

- :math:`Q`: Menge der Zustände
- :math:`\Sigma`: Eingabealphabet
- :math:`\tau`: Kelleralphabet
- :math:`\delta`: Übergangsfunktion
- :math:`q_0`: Anfangszustand, :math:`q_0 \in Q`
- :math:`\bot`: Kellerbodensymbol, :math:`\bot \in \tau, \bot \notin \Sigma`
- :math:`F`: Menge der akzeptierenden Zustände

Zur Übergangsfunktion:

:math:`\delta: Q \times \Sigma \cup \{\epsilon\} \times \tau \rightarrow \textit{P}(Q \times \tau^*)`

- :math:`Q`: aktueller Zustand
- :math:`\Sigma \cup \{\epsilon\}`: gelesenes Symbol der Eingabe oder Schritt ohne Lesen.
- :math:`\tau`: oberstes Kellersymbol (entfernen)
- :math:`Q`: Folgezustand
- :math:`\tau^*`: neu auf den Keller schreiben

Nichtdeterministisch: Zu einer Situation sind mehrere Übergänge möglich.

Ein Kellerautomat **akzeptiert** ein Wort :math:`w`, falls es eine Berechnung gibt, die die gesamte Eingabe liest und in einem akzeptierenden Zustand endet.

**Beispiel:** Kellerautomat für die Sprache :math:`L=\{a^kb^k | k\geq 0\}`

Idee der Arbeitsweise: Der Kellerautomat liest alle a's und speichert sie auf dem Keller, dann entfernt er für jedes b ein a vom Keller. Falls die Anzahl der a's gleich der Anzahl der b's ist, dann akzeptiert er, sonnst hat er keine Möglichkeit zum Weiterarbeiten, also verwirft er.

:math:`A = (\{q_0, q_1, q_2\}, \{a,b\}, \{A, \bot\}, \delta, q_0, \bot, \{q2\})` mit

- :math:`\delta = (q_0, \epsilon, \bot) = \{(q_2, \bot)\}`
- :math:`\delta = (q_0, a, \bot) = \{(q_0, a \bot)\}`
- :math:`\delta = (q_0, a, a) = \{(q_0, aa)\}`
- :math:`\delta = (q_0, b, a) = \{(q_1, \epsilon)\}`
- :math:`\delta = (q_1, b, a) = \{(q_1, \epsilon)\}`
- :math:`\delta = (q_0, \epsilon, \bot) = \{(q_2, \bot)\}`

**Graphische Darstellung**

.. image:: 9_2.jpg

Berechnung von :math:`A` auf dem Wort aaabbb:

:math:`(q_0, aaabbb, \bot) \rightarrow (q_0, aabbb, a\bot) \rightarrow (q_0, abbb, aa\bot) \rightarrow (q_0, bbb, aaa\bot) \rightarrow (q_1, bb, aa\bot) \rightarrow (q_1, b, a\bot) \rightarrow (q_1, \epsilon, \bot) \rightarrow (q_2, \epsilon, \bot)`

Äquivalenz von kontextfreien Grammatiken und Kellerautomaten
------------------------------------------------------------

**Theorem** Sei G eine kontextfreie Grammatik. Dann gibt es einen Kellerautomaten A, so dass :math:`L(A) = L(G)`

**Idee des Beweises** Simuliere die Schritte einer Ableitung von :math:`G` auf dem Keller von :math:`A`.

**Beobachtung** Sei :math:`G` eine kontextfreie Grammatik, sei :math:`w \in L(G)`. Dann gibt es eine Ableitung von :math:`w` in :math:`G`, in der in jedem Ableitungsschritt das jeweils am weitesten links liegende Nichtterminal abgeleitet wird. (sogenannte Linksableitung)

**zum Beweis** Der zu :math:`G` äquivalente Kellerautomat :math:`A` arbeitet wie folgt.

- Falls das oberste Symbol auf dem Keller gleich dem nächsten Eingabesymbol ist, werden beide Symbole weggelesen.

- Falls das oberste Symbol auf dem Stack ein Nichtterminal ist, wird es durch die rechte Seite einer passenden Regel ersetzt.

  Dabei wird nichts von der Eingabe gelesen. (:math:`\epsilon`-Übergang)

**Formel:** Sei :math:`G=(\Sigma, N, P, S)`, dann :math:`A=(\{q\}, \Sigma, \Sigma \cup N, \delta, q, S, \{q\})` wobei:

- :math:`\delta(q,a,a) = \{(q, \epsilon)\}` für alle :math:`a \in \Sigma`
- :math:`\delta(q,\epsilon,X) = \{(q, \alpha) | x \rightarrow \alpha \in P\}` für alle :math:`X \in N`

**Beispiel:** kontextfreie Grammatik :math:`G=(\{a,b\}, \{S\}, P, S)` mit :math:`P=\{S \rightarrow aSb, S \rightarrow S \rightarrow \epsilon \}`

Dann ergibt sich der Kellerautomat :math:`A=(\{q\}, \{a,b\}, \{a,b,S\}, \delta, q, S, \{q\})` mit

- :math:`\delta(q, a, a) = \{(q, \epsilon)\}, \delta(q, b, b) = \{(q, \epsilon)\}`
- :math:`\delta(q, \epsilon, S) = \{(q, aSb), q, \epsilon\}`.

Berechnung von :math:`A` auf dem Wort aabb: :math:`(q, aabb, S) \rightarrow (q, aabb, aSb) \rightarrow (q, abb, Sb)  \rightarrow (q, abb, aSbb)  \rightarrow (q, bb, Sbb) \rightarrow (q, bb, bb) \rightarrow (q, b, b) \rightarrow (q, \epsilon, \epsilon)`

Akzeptiert wenn Eingabe und Stack leer sind.

**Theorem (ohne Beweis)** Sei :math:`A` Kellerautomat. Dann gibt es eine kontextfreie Grammatik :math:`G` mit :math:`L(G) = L(A)`.

Grenzen der kontextfreien Sprachen
----------------------------------

**Ziel:** Zeige, dass :math:`L=\{a^kb^kc^k | k \geq 0 \}` nicht kontextfrei ist.

Hierfür Pumping-Lemma für kontextfreie Sprachen.

Sei :math:`L` eine kontextfreie Sprache. Dann existiert ein :math:`n_0 \in \mathbb{N}`, so dass für **alle** Wörter :math:`w \in L` mit :math:`|w| \geq n_0` gilt: Es gibt eine Zerlegung :math:`w = x_1y_1zy_2x_2` mit folgenden Eigenschaften:

1. :math:`| y_1zy_2 | \leq n_0`
2. :math:`| y_1y_2 | \geq 1`
3. für alle :math:`i \in \mathbb{N}` ist :math:`x_1y_1^izy_2^iy_2 \in L`

**Beweisidee** :math:`L` kontextfrei :math:`\Rightarrow` existiert kontextfreie Grammatik in Chomsky-Normalform.

Sei G eine solche Grammatik. Betrachent wir den Ableitungsbaum für ein Wort :math:`w \in L` mit :math:`|w| \geq n_0`:

.. image:: 9_3.jpg

Aus diesem Ableitungsbaum lassen sich neue Bäume konstruieren, die ebenfalls Wörter aus L sind.

**Theorem:** :math:`L=\{a^kb^kc^k | k \geq 0\}` ist nicht kontextfrei

**Beweis:** mit Pumping-Lemma für kontextfreie Sprachen.

  **Annahme** :math:`L` ist kontextfrei
  
  * Dann **existiert** :math:`n_0 \in \mathbb{N}` mit den Eigenschaften des Pumping-Lemma
  * Wir **wählen** :math:`w = a^{n_0} b^{n_0} b^{n_0}`.
  * Dann **existiert** eine Zerlegung :math:`w = x_1y_1zy_2x_2`
  
    1. :math:`| y_1zy_2 | \leq n_0`
    2. :math:`| y_1y_2 | \geq 1`
    3. für alle :math:`i \in \mathbb{N}` ist :math:`x_1y_1^izy_2^iy_2 \in L`
    
  * Wegen (1) gilt: :math:`y_1zy_2` enthält nicht a und c.
  * :math:`\Rightarrow` Fallunterscheidung liefert in beiden Fällen einen Widerspruch (3)
  
    Zwei Buchstaben werden hochgepumpt, einer nicht
    
    Nach dem Pumpen nicht mehr gleich viele a's, b's und c's.