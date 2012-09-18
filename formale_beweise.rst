=========================================
Kurze Einführung in formale Beweisführung
=========================================

Motivation
**********
Insbesondere negative Aussagen der Form "Diese Aufgabe kann dieses Rechenmodell
**nicht** lösen" brauchen eine präzise Formulierung und Begründung, um
glaubwürdig zu sein.

Hopcraft Abschnitt 1.2 - 1.4

Beweismethoden
**************

1. Deduktion
~~~~~~~~~~~~
Zum beweis von Wenn-Dann-Aussagen:

z.B Wenn :math:`x \geq 4` (Hypothese, Verankerung), dann :math:`x^2 \geq 16` (Konklusion)).

**Vorgehen** Voraussetzung als wahr annehmen. dann Folgerungen darauf anwenden
bis Konklusion abgeleitet ist.

**Beispiel** Sei :math:`x \geq 4`. Es gilt :math:`x^2=16` und Quadratfunktion
ist steigend.

Daraus folgt :math:`x^2 \geq 4^2 = 16`

**Hierfür of Hilfreich:** Definitionen von begriffen einsetzen.

Beipiel: Wenn :math:`L = \{w\in \{a,b\} |w| gerade\}`, dann gilt für alle
:math:`x \in L^2`, dass :math:`|x|` gerade.

**Beweis**

Sei :math:`x \in L^2`.

Def. von :math:`L^2` einsetzen: Es existieren :math:`u,v \in L`, so dass
:math:`x=uv`.
Def. von L: :math:`|u|` gerade, :math:`|v|` gerade

Folgt: :math:`|x| = |u| + |v| \Rightarrow |x|` gerade.

2. Beweis von  "Genau dann, wenn"-Aussagen
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Zerlegen in zwei Wenn-Dann-Aussagen und getrennt beweisen.

z.B. Gleichung von Mengen zeigen

:math:`A=B`

:math:`A \leq B`

:math:`A \geq B`

**Beispiel** Seien :math:`L_1, L_2 \leq \sum^*`, dann gilt
:math:`L_1 \cdot (L_1 /cup L_2) = {L_1}^2 \cup L_1 \cdot L_2`

**Beweis** :math:`\leq` Sei :math:`x \in L_1 \cdot (L_1 \cup L_2)`

:math:`\Rightarrow` u,v mit :math:`x=uv`, :math:`u \in L_1, v \in L_1 \cup L_2`

:math:`\Rightarrow v \in L_1` oder :math:`v \in L_2`

Fallunterscheidung(a) :math:`v \in L_1 : \rightarrow x=uv` mit :math:`x \in L_1, v \in L_1`

:math:`\Rightarrow x \in {L_1}^2`

Fallunterscheidung(b) :math:`v \in L_2 \Rightarrow x=uv` mit :math:`u \in L_1, v \in L_2`

:math:`\Rightarrow x \in L_1 \cdot L_2`

:math:`\geq`: Sei :math:`x \in {L_1}^2 \cup L_1 * L_2`

:math:`\Rightarrow x \in L_1^2` oder :math:`x \in L_1 \cdot L_2`

Fallunterscheidung(a) :math:`x \in {L_1}^2 \Rightarrow x=uv` mit :math:`u,v \in L_1`

:math:`\Rightarrow v \in L_1 \cup L_2 \Rightarrow x\in L_1 \cdot (L_1 \cup L_2)`

Fallunterscheidung(b):math:`x /in L_1 \cdot L_2 \Rightarrow x=uv` mit
:math:`u \in L_1, v \in L_2 \Rightarrow v \in (L_1 \cup L_2)`

:math:`\Rightarrow x \in L_1 \cdot (L_1 \cup L_2)`

3. Widerspruchsbeweise
~~~~~~~~~~~~~~~~~~~~~~

**Beispiel:** Seien :math:`a,b \in \mathbb{N}` und :math:`a,b \geq 2`. Dann gilt:

a teilt nicht :math:`ab + 1`

**Beweis** Seien :math:`a,b \in \mathbb{N}`

**Angenommen**, a teilt ab+1

**Ziel** Annahme zum Widerspruch führen, dann folgt ihre Negation, also die
gewünschte Konklusion.

a teilt :math:`a \cdot b \Rightarrow` a teilt :math:`a \cdot b` **und** :math:`ab + 1`

:math:`\Rightarrow a` teilt :math:`(a \cdot b + 1) - (a \cdot b) =  1`

:math:`\Rightarrow a=1`

**Widerspruch** zu :math:`a \geq 2`

**Beispiel:** Es gibt unendlich viele Primzahlen.

(äq. Formulierung: Es gibt keine grösste Primzahl.)

**Beweis** Angenommen die Anzahl der Primzahlen sei endlich, nenne die Anzahl k.

Seien :math:`p_1 < p_2 < p_3 < .... < p_k` die Primzahlen, betrachte

:math:`x= p_1 \cdot p_2 \cdot ...... \cdot p_k + 1`.

Da :math:`p_k` die grösste Primzahl ist und :math:`x > p_k`, kann x also keine
Primzahl sein.

Also gibt es eine Primfaktorenzerlegung von x , sei :math:`p_L` die kleinste
Primzahl in dieser Zerlegung.

Dann gilt: :math:`p_L` teilt :math:`p_1 \cdot p_2 \cdot ...... \cdot p_k` und 
:math:`p_L` teilt x

:math:`p_L` teilt :math:`p_1 \cdot p_2 \cdot ....... \cdot p_k + 1`

**Widerspruch** zum vorherigen Beispiel mit :math:`a=p_L` und :math:`b=p_1 p_2 ... p_k`

Die Annahme ist falsch es existieren unendlich viele Primzahlen.

4. Induktionsbeweise:
~~~~~~~~~~~~~~~~~~~~~
Verwendet für aussagen über natürliche Zahlen

**Ziel** Zeige, dass die Aussage :math:`S(n)` für alle :math:`n \geq 0`
(oder :math:`n \geq 1` o.ä.) gilt.

Methode:

**Induktionsanfang:** Zeige :math:`S(0)`.

**Induktionsschritt:** Setze :math:`S(i)` voraus und zeige :math:`S(i+1)`, d.h.
Zeige die Aussage :math:`S(i) \rightarrow S(i+1)`

**Idee** Wenn :math:`S(0)` gilt und :math:`S(i) \rightarrow S(i+1)` für alle
:math:`i \geq 0`, dann aus :math:`S(0)` und :math:`S(0) \rightarrow S(1)` folgt :math:`S(1)`,
aus :math:`S(1)` und :math:`S(0) \rightarrow S(1)` folgt :math:`S(2)`, ...

**Beispiel**: Für alle :math:`n \geq 1` gilt :math:`\sum_{i=1}^{n} i = \frac{n(n+1)}{2}`

**Beweis**: 

Ind. Anfang: n=1 :math:`\sum_{i=1}^{1} i = \frac{1(1+1)}{2}` (ok)

Ind. Schritt: Es gelte :math:`\sum_{i=1}^{k} i = \frac{k(k+1)}{2}`
(Induktionsvoraussetzung)

Zeige: :math:`\sum_{i=1}^{k+1} i = \frac{k+1(k+1+1)}{2}` (Induktionsbehauptung)

Beweis hiervon: Es gilt :math:`\sum_{i=1}^{k+1} i = (\sum_{i=1}^{k} i) + (k+1)`

:math:`= \frac{k(k+1)}{2} + (k+1)`

:math:`= \frac{k(k+1) + 2(k+1)}{2}`

:math:`= \frac{(k+2) \cdot (k+1)}{2}`

:math:`= \frac{(k+1) \cdot ((k+1) + 1)}{2}`

5. Rekursive Definitionen und strukturelle Induktion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Beispiel
--------

Rekursive Definition von arithmetischen Ausdrücken.

**Basis:** Jede Zahl und jede Variable ist arithm. Ausdruck.

**Rekursion:** Wenn E und F Ausdrücke sind, dann auch :math:`E + F, E \cdot F, (E)`

Behauptung
----------

Jeder Ausdruck enthält gleich viele linke wie rechte Klammern.

Beweis mit struktureller Induktion:
-----------------------------------
I.A.: Basisausdrücke haben keine Klammern (ok)

Ind. Schritt: Sei G ein arithmetischer Ausdruck
:math:`\Rightarrow G = E + F, E \cdot F, (E)` nach Rekursion

Fallunterscheidung(1): :math:`G = E + F` Ind. vor.: E und F haben gleich viele
linke und rechte Klammern.

:math:`\Rightarrow` gilt auch für G, da keine Klammern hinzu kommen.

Fall(2): :math:`G = E \cdot F` analog

Fall(3): :math:`G=(E)` Ind vor ist E hat gleich viele linke Klammern wie rechte
Klammern.

:math:`\Rightarrow` gilt auch für G, da eine linke und eine rechte Klammer
hinzukommt.
