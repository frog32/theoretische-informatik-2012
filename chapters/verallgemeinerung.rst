Verallgemeinerung der Methode
=============================

**Ziel:** Zeige, dass es gar keinen DEA für L gibt.

Pumping-Lemma für reguläre Sprachen:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sei L eine reguläre Sprache. Dann gibt es eine Konstante :math:`n_0` (die von L abhängt), so dass für jedes Wort :math:`w \in L` mit :math:`|w| \geq n_0` gilt:

w kann zerlegt werden in :math:`w = u \cdot x \cdot v` mit den folgenden Eigenschaften:

a. :math:`|x|\geq 1`, d.h. :math:`x\neq \epsilon`
b. :math:`|ux| \leq n_0`
c. Für alle :math:`k \geq 0` ist auch :math:`ux^kv \in L`

Begründung der Korrektheit:
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Falls L regulär ist, existiert ein DEA A für L.

Setze :math:`n_0 = |Q|`. x ist dann die Beschriftung eines Zykels in A, der in den ersten :math:`|Q|` Berechnungsschritten auftritt. (:math:`|ux| \leq n_0`)

Wiederholung des Zykels ändert nichts an der Akzeptanz des Wortes.

**Beispiel:** :math:`L \left \{a^kb^k | k \in \mathbb{N} \right\}`

Widerspruchsbeweis

Annahme: L ist regulär

Das Pumping-Lemma gibt uns die Existens einer Konstanten :math:`n_0`, so dass für alle Wörter :math:`w \in L` mit :math:`|w| \geq n_0` alle Bedingungen gelten.

Um einen Wierspruch herzuleiten, können wir uns ein Wort :math:`w \in L` auswählen, sei also :math:`w=a^{n_0}b^{n_0}`.
Nach dem Pumping-Lemma gibt es eine Zerlegung :math:`w=uxv` mit :math:`|ux| \leq n_0` und :math:`|x| \geq 1`.

:math:`\Rightarrow u=a^j` für ein :math:`0 \leq j \leq n_0` und :math:`x = a^i` für ein :math:`1 \leq i \leq n_0`.

Weiter gilt nach dem Pumping-Lemma. :math:`ux^kv \in L` für alle :math:`k`.

Um den Widerspruch herzuleiten, wählen wir :math:`k=2`.

Nach dem Pumping-Lemma muss gelten, dass :math:`ux^2v = a^{n_0+i}b^{n_0}` gilt. **Falsch** weil :math:`n_0+i \neq n_0`

:math:`\Rightarrow` L kann nicht regulär sein.

**Bemerkung:**

* Das Pumping-Lemma gibt nur notwendige Eigenschaften für reguläre Sprachen an, aber keine hinreichenden.

  * Regularität kann nicht gezeigt werden

* Es gibt Sprachen, die nicht regulär sind und trotzdem das Pumping-Lemma erfüllen.

Anwendung des Pumping-Lemma als Spiel gegen einen Gegner:

1. Wir wählen die Sprache, deren Nichtregularität wir nachweisen wollen.
2. Der Gegner wählt :math:`n_0`.
3. Wir wählen das Wort w mit :math:`|w| \geq n_0`.
4. Gegner wählt Zerlegung :math:`w=uxv` gemäss Pumping-Lemma.
5. Wir wählen k und gewinnen, falls wir einen Widerspruch herleiten können.
