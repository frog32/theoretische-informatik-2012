==================
Reguläre Ausdrücke
==================
Besonders für Mustersuche geeignet, anderer Formalismus zu Beschreibung von regulären Sprachen.

**Operatoren für reguläre Ausdrücke**

* **Vereinigung** von Sprachen L und M, L :math:`\cup` M, ist die Menge aller Zeichenreihen die entweder in L oder in M enthalten sind oder in beiden enthalten sind.

  **Beispiel:** :math:`L=\{001,10,111\}, M=\{\epsilon,001\} \Rightarrow L \cup M = \{\epsilon, 10, 001, 111\}`

* **Verkettung** (Konkatenation) von L und M, L*M oder LM, ist die Menge aller Zeichenreihen gebildes aus einer Verkettung einer Zeichenreihe aus L mit einer beliebigen aus M.

  **Formal:** :math:`L \cdot M = \{w \in \epsilon^* | w=uv \text{mit u} \in \text{L und v} \in M\}`
  
  **Beispiel:** :math:`LM = \{001, 10, 111, 001001, 10001, 111001\}`
  
* Die **Kleensche Hülle** (Stern) von L, :math:`L^*`, ist die Menge aller Zeichenreihen, die durch die Verkettung einer beliebigen Anzahl von Zeichenreihen aus L gebildet wird.

  **Formal:** :math:`L^0 = \{\epsilon\}` :math:`L^* = \bigcup\limits_{i=0}^{\infty} L^i`
  
  **Anschaulich:** :math:`w \in L^*`, wenn sich w zerlegen lässt in endlich viele Wörter :math:`w=w_1 w_1 ... w_k` für ein :math:`k \in \mathbb{N}` so dass :math:`w_1 \in L, w_2 \in L, ...` gilt.
  
  **Spezialfälle:** :math:`\varnothing^* = \{ \epsilon \}`, da :math:`\varnothing^0 = \{ \epsilon \}`
  
  :math:`\{\epsilon\}^* = \{\epsilon\}`
  
  Aber: :math:`\varnothing^i` für i>1 ist :math:`\varnothing`


**Definition:** Reguläre Ausdrücke lassen sich wie folgt definieren:

1. :math:`\epsilon` und :math:`\varnothing` sind reguläre Ausdrücke
2. Jedes Symbol :math:`a \in \sigma` ist ein regulärer Ausdruck
3. Wenn :math:`\alpha` :math:`\beta` reguläre Ausdrücke sind dann sind

  * :math:`(\alpha \cdot \beta)` (Verkettung)
  * :math:`(\alpha + \beta)` (Vereinigung)
  
  reguläre Ausdrücke

4. Wenn :math:`\alpha` ein regulärer Ausdruck ist, dann ist auch :math:`(\alpha)^*` ein regulärer Ausdruck (Kleensche Hülle)

**Konvention:**

* überflüssige Klammern weglassen
* :math:`*` Bindet stärker als :math:`\cdot`
* :math:`\cdot` bindet stärker als +

**Bedeutung regulärer Ausdrücke:**

:math:`L(\alpha)` bezeichnet die durch den regulären Ausdruck :math:`\alpha` beschriebene Sprache.

Dabei gilt:

* :math:`L(\epsilon) = \{\epsilon\}`
* :math:`L(\varnothing) = \varnothing`
* :math:`L(a) = \{a\}`
* :math:`L(\alpha \cdot \beta) = L(\alpha) \cdot L(\beta)`
* :math:`L(\alpha + \beta) = L(\alpha) \cup L(\beta)`
* :math:`L(\alpha^*) = (L(\alpha))^*`

**Beispiel:** Beschreibung von Sprachen durch reguläre Ausdrücke

1. :math:`L_1 = \{w \in \{0,1\}^* | \text{w beginnt mit 011 und enthält das Teilwort 00}\}`

  RA für :math:`L_1`: 001 (0+1)* 00 (0+1)*

2. :math:`L_2 = \{w \in \{a,b,c\}^* | {\left | w \right |}_a \text{ist gerade}\}`

  **Notation:** :math:`{\left | w \right |}_a` = Anzahl der Vorkommen von a in w
  
  RA für :math:`L_2`: ((b+c)* a (b+c)* a (b+c)*) *
  
3. :math:`L_3 = \{w \in \{0,1\}^* | \text{in w kommen die Nullen und Einsen immer abwechselnd vor}\}`

  RA für :math:`L_3`: (01)* + (10)* + 1(01)* + 0(10)*
  
Anwendungsbeispiel
------------------

Spezifikation einer Eingabemaske für Kontostände

**Bedingungen:**

* Währungsangabe: CHF, EUR, oder USD
* vor dem Betrag optionales Vorzeichen: + oder -
* Betrag ganzzahlig oder mit Dezimalpunkt und zwei Nachkommastellen
* keine führende Nullen

**Modellierung des RA:**

:math:`\sigma = \{C, D, E, F, H, R, S, U, +, -, ., 0, 1, ..., 9\}`

**Idee:** Setze den RA aus Teilen Zusammen

zahlung = waerung vorzeichen betrag

waehrung = (CHF + EUR + USD)

vorzeichen = (:math:`\epsilon` + "+" + "-")

betrag = ganzzahl (:math:`\epsilon` + . nachkommmazahl)

ganzzahl = (0 + (1 + ... + 9)(0 + 1 + ... + 9)*)

nachkomma = (0 + 1 + ... + 9)(0 + 1 + ... + 9)

zahlung = (CHF + EUR + USD) (:math:`\epsilon` + "+" + "-") (0 + (1 + ... + 9)(0 + 1 + ... + 9)*) (:math:`\epsilon` + . (0 + 1 + ... + 9)(0 + 1 + ... + 9))

**Theorem:** Reguläre Ausdrücke und endliche Automaten sind äquivalent:

1. für jeden RA :math:`\alpha` existiert ein DEA :math:`a_\alpha` mit :math:`L(\alpha) = L(A_\alpha)` und 
2. für jeden DEA ein RA :math:`\alpha_A` mit :math:`L(A) = L(\alpha_A)`

**Beweis: 1. Umwandlung von RA in DEA**

Vorgehensweise: :math:`RA \rightarrow \epsilon-NEA \rightarrow DEA`

Für gegebenen RA konstruiere einen :math:`\epsilon`-NEA induktiv entsprechend des Aufbaus des RA mit folgenden zusätzlichen **Eigenschaften**:

1. genau einen akzeptierenden Zustand
2. keine Transition zum Startzustand hin
3. keine Transition vom akzeptierenden Zustand ausgehend

**Induktionsanfang:** :math:`\epsilon`-NEA für :math:`\epsilon`:

.. image:: 3_1.jpg

**Induktionsschritt:**

* Sei :math:`\alpha = \beta + \gamma` ein RA, seien B,C :math:`\epsilon`-NEAs für :math:`\beta` und :math:`\gamma` wie oben mit Startzuständen :math:`q_{B0}` und :math:`q_{C0}` und akzeptierenden Zuständen :math:`q_{BF}` und :math:`q_{CF}`.

  .. image:: 3_2.jpg

  Erfüllt alle Bedingungen

* Seien :math:`\alpha = \beta \cdot \gamma` und B,C :math:`\epsilon`-NEA's für :math:`\beta,\gamma`.

  .. image:: 3_3.jpg

  Erfüllt alle Bedingungen

* Sei :math:`\alpha = \beta^*`, B ein :math:`\epsilon`-NEA für :math:`\beta`.

  .. image:: 3_4.jpg
  
  Erfüllt alle Bedingungen

**Beispiel:** :math:`\epsilon`-NEA für :math:`\alpha = (0+1)* 1 (0+1)`

:math:`\epsilon`-NEA für (0+1):

.. image:: 3_5.jpg

:math:`\epsilon`-NEA für (0+1)*:

.. image:: 3_6.jpg

:math:`\epsilon`-NEA für (0+1)* 1 (0+1):

.. image:: 3_7.jpg

**Beweis: 2. Umwandlung von DEA in RA**

**Idee:** Dynamische Programmierung

**Teilprobleme hier:** Für **jedes Paar** (p, q) von Zuständen finde einen regulären Ausdruck der alle Wörter beschreibt, die von p nach q führen.

**Genauer:** Sei :math:`A=(Q, \sigma, \gamma, q_0, F)` ein DEA, seien die Zustände druchnummeriert, d.H. :math:`Q=\{1,2,...,n\}`, :math:`q_0 = 1`

1. Berechne für alle :math:`i, j \in \{1,...,n\}` RA :math:`\alpha_{ij}^{(0)}`, die die **direkten** Verbindungen von Zustand i zu Zustand j beschreiben:

  a) i=j:
  
    .. image:: 3_9.jpg
    
    :math:`\alpha_{ii}^{(0)} = \epsilon + a_1 + a_2 + ...`
    
    .. image:: 3_10.jpg
    
    :math:`\alpha_{ii}^{(0)} = \epsilon`
    
  b) :math:`i \neq j`:
  
    .. image:: 3_11.jpg
    
    :math:`\alpha_{ij}^{(0)} = a_1 + a_2 + ...`
    
    .. image:: 3_12.jpg
    
    :math:`\alpha_{ij}^{(0)} = \varnothing`
    
2. Nun werden nacheinander alle anderen Zustände als mögliche Zwischenstationen auf dem Weg von i nach j hinzugenommen. Zunächst Zustand 1: :math:`\alpha_{ij}^(1)` beschreibt die Wörter, mit denen man von i nach j kommt und zwischendurch nur 1 besucht:

  .. image:: 3_13.jpg
  
  :math:`\alpha_{ij}^{(1)} = \alpha_{ij}^{(0)} + \alpha_{i1}^{(0)} (\alpha_{11}^{(0)})^* \alpha_{1j}^{(0)}`

**Induktion:** Wir nehmen an, dass wir :math:`\alpha_{ij}^{(k-1)}` für alle i,j schon berechnet haben.

Dann gilt: :math:`\alpha_{ij}^{(k)} = \alpha_{ij}^{(k-1)} + \alpha_{ik}^{(k-1)} (\alpha_{kk}^{(k-1)})^* \alpha_{kj}^{(k-1)}`

:math:`\Rightarrow` RA für den DEA A mit :math:`q_0=1` und :math:`F=\left\{f_1, ..., f_m \right\}`: :math:`\alpha_{1f_1}^{(n)} + \alpha_{1f_2}^{(n)} + ... + \alpha_{1f_m}^{(n)}`

**Beispiel:** DEA A:

.. image:: 3_14.jpg

1.
 
  :math:`\alpha_{11}^{(0)} = 1 + \epsilon`
  
  :math:`\alpha_{12}^{(0)} = 0`
  
  :math:`\alpha_{21}^{(0)} = \varnothing`
  
  :math:`\alpha_{22}^{(0)} = \epsilon + 0 + 1`
  
2.

  :math:`\alpha_{11}^{(1)} = \alpha_{11}^{(0)} + \alpha_{11}^{(0)} (\alpha_{11}^{(0)})^* \alpha_{11}^{(0)}`
  
  :math:`(1 + \epsilon) + (1 + \epsilon)(1 + \epsilon)^* (1 + \epsilon) = (1 + \epsilon)^* = 1^*`
  
  :math:`\alpha_{12}^{(0)} = \alpha_{12}^{(0)} + \alpha_{11}^{(0)} (\alpha_{11}^{(0)})^* \alpha_{12}^{(0)}`
  
  :math:`0 + (1 + \epsilon)(1 + \epsilon)^* 0 = 1^* 0`
  
  :math:`\alpha_{21}^{(1)} = \alpha_{21}^{(0)} + \alpha_{21}^{(0)} (\alpha_{11}^{(0)})^* \alpha_{11}^{(0)}`
  
  :math:`= \varnothing + \varnothing (1 + \epsilon)^* (1 + \epsilon) = \varnothing`
  
  :math:`\alpha_{22}^{(1)} = \alpha_{22}^{(0)} + (\alpha_{22}^{(0)})^* \alpha_{22}^{(0)}`
  
  :math:`= (\epsilon + 0 + 1) + \varnothing .... = \epsilon + 0 + 1`
  
3.

  :math:`\alpha_{11}^{(2)} = \alpha_{11}^{(1)} + \alpha_{12}^{(1)} (\alpha_{22}^{(1)})^* \alpha_{21}^{(1)}`
  
  :math:`1^* + 1^* 0 (\epsilon + 0 + 1)^* \varnothing = 1^*`
  
  :math:`\alpha_{12}^{(2)} = \alpha_{12}^{(1)} + \alpha_{12}^{(1)} (\alpha_{22}^{(1)})^* \alpha_{22}^{(1)}`
  
  :math:`1^* 0 + 1^* 0 (\epsilon + 0 + 1)^* (\epsilon + 0 + 1)`
  
  :math:`1^* 0 (0+1)^*`
  