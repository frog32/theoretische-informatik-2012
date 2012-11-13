================
Nichtregularität
================

**Ziel:** Zeige, dass es Sprachen gibt, die nicht regulär sind.

**Idee:** DEAs analysieren: DEAs können nicht beliebig weit zählen.

**Beispie:** Betrachte den folgenden DEA:

.. image:: 4_3.jpg

Arbeit von A auf dem Wort :math:`w = abaaab`:

.. image:: 4_4.jpg

Enthält einen Zykel :math:`q_1 q_2 q_3 q_1`.

Wiederholung des Zykels: :math:`w' = abaaaaaab`  

.. image:: 4_5.jpg

Da :math:`q_4 \in F`, gilt :math:`w' \in L(A)`

**Allgemein:** Sei A ein DEA. Sei :math:`w=u \cdot x \cdot x` ein Wort in :math:`L(A), u,v,x \in \Sigma^*, x\neq \epsilon`-

Falls der Automat auf dem Teilwort x in einer Schleife läuft, dann ist auch :math:`w' = uxxv \in L(A)`.

**Formal:** Falls :math:`\hat{\delta}(q_0, u) = q` und :math:`\hat{\delta}(q,x)= q` und :math:`\hat{\delta}(q,v) \in F`, dann ist :math:`w' = uxxxv \in L(A)`

Im Beispiel oben:

:math:`w = abaaab \in L(A)`
  
:math:`w' = abaaaaaab \in L(A)`

**Bemerkung:** Ein DEA ist vollständig, das heisst für jedes :math:`q \in Q` und jedes :math:`a \in \Sigma` existiert genau ein Folgezustand :math:`\delta(q,a)`

:math:`\Rightarrow` Mit jedem Wort auf :math:`\Sigma^*` kann man durch den Automaten laufen, ohne stecken zu bleiben

:math:`\Rightarrow` Bei der Arbeit des DEA A mit :math:`n` Zuständen auf einem Wort der Länge :math:`\geq n` wird mindestens ein Zustand doppelt besucht.

**Beispiel:**

.. image:: 4_5.jpg

:math:`w_1 = abb \Rightarrow q_0 q_1 q_0 q_2 \Rightarrow q_2` wird doppelt besucht

:math:`w_2 = bba \Rightarrow q_0 q_2 q_1 q_0 q_1 \Rightarrow q_0, q_1` werden doppelt besucht

**Beobachtung:** Sei :math:`A = (Q, \Sigma, \delta, q_0, F)` ein DEA mit :math:`\left | Q \right | = n`. Sei :math:`w \in L(A)` mit :math:`\left | w \right | \geq n`. Dann wiederholt sich in der Berechnung von A auf w mindestens einmal ein Zustand. Wir nennen einen dieser wiederholt besuchten Zustände :math:`q_x`.

Dann lässt sich :math:`w` zerlegen in drei Teile

:math:`w= u \cdot x \cdot v`

:math:`u` bis zum ersten :math:`q_x`, :math:`x` von :math:`q_x` nach :math:`q_x`, :math:`v` nach :math:`q_x`

Berechnung von A auf w hat die Form

.. image:: 4_6.jpg

Damit gibt es auch eine Berechnung von A auf :math:`w'=uxxv`

.. image:: 4_7.jpg

Endet wieder in :math:`q_F`, also :math:`w' \in L(A)`

**Beispiel:** Diese Beobachtung können wir nutzen, um zu zeigen, dass :math:`L = \left \{a^k b^k | k \geq 0 \right\}` nicht regulär ist.

**Widerspruchsbeweis:** Zunächst:

Für :math:`L` kann es keinen DEA mit 7 Zuständen geben.

**Annnahme:** Es gibt ein DEA :math:`A = (Q, \Sigma, \delta, q_0, F)` mit :math:`|Q| = 7` und :math:`\Sigma = \left \{ a,b,\right\}`, so dass :math:`L(A)=L`.

**Wiederlegung der Annahme:**

2 Möglichkeiten:

1. alle möglichen DEA mit 7 Zuständen ausprobieren. (brauch viel Zeit)
2. Beobachtung über Zykel ausnutzen.

Betrache das Wort :math:`w=aaaabbbb \in L`.

Es gilt :math:`|w| = 8 \gt 7 = |Q|`

Also muss sich in der Berechnung von :math:`A` auf :math:`w` mindestens ein Zustand wiederholen.

:math:`w` zerteilen in :math:`w = u \cdot x \cdot v` mit der Berechnung

.. image:: 4_6.jpg

:math:`\Rightarrow w' = uxxv \in L(A)`

Wie kann das Wort x aussehen?

**Fallunterscheidung:**

1. Fall: x besteht nur aus a's:

  z.B: :math:`w=\text{aa aa bbbb}`
  
  :math:`\Rightarrow w' = \text{aa aa aa bbbb} = a^6 b^4 \notin L`

2. Fall: x besteht nur aus b's:

  z.B: :math:`w=\text{aaaab b bb}`
  
  :math:`\Rightarrow w' = \text{aaaab b b bb} = a^4 b^5 \notin L`

3. Fall: x besteht aus a's und b's:

  z.B: :math:`w=\text{aa aab bbb}`
  
  :math:`\Rightarrow w' = \text{aa aab aab bbb}  \notin L`
  
  weil sich a's und b's abwechseln

Da keine weiteren Fälle auftreten können, kann es eine solche Zerlegung nicht geben.

:math:`\Rightarrow` WIDERSPRUCH

:math:`\Rightarrow` Es gibt keinen DEA mit 7 Zuständen für L.

Wir bemerken: Denselben Beweis hätten wir auch für jeden andere Anzahl von Zuständen führen können.

:math:`\Rightarrow` Es gibt keinen DEA für L.

:math:`\Rightarrow` L ist nicht regulär.