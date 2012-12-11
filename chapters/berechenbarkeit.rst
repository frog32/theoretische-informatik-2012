===============
Berechenbarkeit
===============

Aufzählung von Wörtern
----------------------

Sei :math:`\Sigma = \left \{a_1,a_2,...,a_n \right\}` ein Alphabet. Es sei :math:`a_1 \lt a_2 \lt ... \lt a_n`.

Dann ist die **kanonische Reihenfolge** auf :math:`\Sigma^*` definiert durch :math:`w \lt_{kan} u` genau dann, wenn

* :math:`|w| \lt |u|`
* :math:`|w| = |u| = k, w=a_1 ... a_k, u=b_1 ... b_k`

es gibt ein :math:`i` mit :math:`1 \leq i \leq k_i`, so dass :math:`a_j = b_j` für :math:`j \lt i` und :math:`a_i \lt b_i`

**Beispiel**

:math:`ba \lt_{kan} aba` und :math:`abb \lt_{kan} aca`

Aufzählung von Turingmaschinen
------------------------------

Sei :math:`\mathcal{M}` die Menge aller Turingmaschinen. Dann ist die **kanonische Reihenfolge** auf :math:`\mathcal{M}` definiert durch :math:`M_1 \lt_{kan} M_2` genau dann, wenn :math:`Kod(M_1) \lt_{kan} Kod(M_2)`.

Berechenbarkeit
---------------

**Ziel:** Zeigen, dass es keine Turingmaschine :math:`U` gibt die hält, die für eine gegebene Turingmaschine :math:`M` und ein gegebenes Wort :math:`w` entscheidet, ob :math:`w \in L(M)` gilt.

**Motivation:** Gemäss Church'scher These bedeutet dies, dass es nicht möglich ist, ein Programm zu schreiben, dass beliebige andere Programme  verifiziert.

Dazu zeigen wir zunächst, dass es eine Sprache gibt, die keine Turingmaschine akzeptiert.

.. image:: 11_1.jpg

Die Diagonalisierungssprache
----------------------------

**Idee:** Wir zeigen, dass es mehr Sprachen als TM gibt. Das heisst es gibt (unendlich viele) Sprachen für die es keine Turingmaschine gibt.

**Methode der Diagonalisierung**

Wir haben gesehen, dass wir alle Wörter und Turingmaschinen aufzählen können.

Sei als :math:`w_i`, das i-te Wort in kanonischer Reihenfolge, sei :math:`M_i` die i-te Turingmaschine in kanonischer Reihenfolge.

Wir konstruieren eine (unendlich grosse) Tabelle :math:`D` mit Einträgen aus :math:`\{0,1\}`, so dass :math:`D(i,j) = 1` genau dann, wenn :math:`M_i` das Wort :math:`w_j` akzeptiert.

.. image:: 11_2.jpg

Wir betrachten die Diagonaleinträge :math:`D(i,i)`:

  :math:`D(i,i)` beschreibt, ob die Turingmaschine :math:`M_i` das Wort :math:`w_i` mit gleichem Index der Aufzählung, akzeptiert.
  
  Wir definieren nun die Sprache:
  
    :math:`L_d = \left\{ w \in \{0,1\}^* | w=w_i \text{ und } M_i \text{ akzeptiert } w_i \text{ nicht}\right\}`
    
    :math:`= \left\{ w \in \{0,1\}^* | w=w_i \text{ und } D(i,i) = 0 \right\}`
    
  In der Tabelle: Alle Spalten mit einer 0 un der Diagonalen.

**Theorem:** Es gibt keine Turingmaschine, die :math:`L_d` akzeptiert.

**Beweis:** Angenommen, es gibt eine Turingmaschine :math:`M`, die :math:`L_d` akzeptiert. Da wir in der Tabelle :math:`D` alle Turingmaschinen aufgezählt haben, gibt es einen Index :math:`j`, so dass :math:`M=M_j`, also gilt dann :math:`L_d = L(M_j)`.

Für den gewünschten Widerspruch, betrachten wir das entsprechende Wort :math:`w_j`.

Es gilt :math:`w_j \in L(M_j) \Leftrightarrow D(j,j) = 1` nach Definition von :math:`D`

aber :math:`w_j \in L_d \Leftrightarrow D(j,j) = 0` nach Definition von :math:`L_d`

Es kann also nicht :math:`L_d = L(M_j)` gelten, aslo war die Annahme falsch, somit gibt eis keine Turingmaschine, die :math:`L_d` akzeptiert.

**Wiederholung**

* Eine Sprache :math:`L` heisst **rekursiv aufzählbar**, wenn es eine Turingmaschine :math:`M` gibt, die :math:`L` akzeptiert.
  
  falls :math:`w \notin M` darf :math:`M` unendlich lange laufen
  
* Eine Sprache :math:`L` heisst **rekursiv** (entscheidbar), wenn es eine Turingmaschine :math:`M` gibt, die :math:`L` **entscheidet**,

  - für alle :math:`w \in L \rightarrow` akzeptiert
  - für alle :math:`w \notin L \rightarrow` verwerfen
  
  darf nicht unendlich lange laufen

Reduktion
---------

Wir wollen die Unlösbarkeit von Sprachen auf andere Sprachen ausweiten. Die Idee ist eine Reduktion "leichter oder gleich schwer" bezüglich der algorithmischen Lösbarkeit einführen.

**Definition:** Seien :math:`L_1` und :math:`L_2` zwei Sprachen. :math:`L_1` ist auf :math:`L_2` **rekursiv reduzierbar**, geschrieben :math:`L_1 \leq_{R} L_2` falls es eine immer haltende Turingmaschine :math:`A` gibt, die :math:`L_2` entscheidet, und man daraus eine Turingmaschine :math:`B` bauen kann, die :math:`L_1` entscheidet.

Existiert eine Reduktion :math:`L_1 \leq_{R} L_2` dann gilt:

- Ist :math:`L_1` unentscheidbar, dann ist :math:`L_2` unentscheidbar
- Ist :math:`L_1` nicht rekursiv aufzählbar, dann ist :math:`L_2` ebenfalls nicht rekursiv aufzählbar

Komplemente rekursiver Sprachen
-------------------------------

Sei :math:`\overline{L} = \Sigma^*-L` das **Komplement** von :math:`L`.

**Theorem:** :math:`L` ist rekursiv :math:`\Rightarrow` :math:`\overline{L}` ist rekursiv.

**Beweis:** Wir zeigen, dass :math:`\overline{L} \leq_{R} L`. :math:`(L \leq_{R} \overline{L})`

  Sei :math:`A` eine Turingmaschine die :math:`L` entscheidet.
  
  Eine Turingmaschine :math:`B` die :math:`\overline{L}` entscheidet lässt sich mit folgendem Schema bauen.
  
  .. image:: 11_3.jpg
  
**Theorem:** :math:`\overline{L}_d` ist rekursiv aufzählbar

  :math:`\overline{L}_d = \{ w \in \{0,1\}^* | w=w_i \text{ und } M_i \text{ akzeptiert } w_i \}` 
  
**Beweis:** Eine Turingmaschine :math:`D` die :math:`\overline{L}_d` akzeptiert, kann wie folgt arbeiten:

1. Berechne :math:`i`, so dass :math:`w` das i-te Wort :math:`w_i` in der kanonischen Reihenfolge ist.
2. Generiere die :math:`Kod(M_i)` der i-ten Turingmaschine :math:`M_i`.
3. Simuliere die Berechnung von :math:`M_i`, auf dem Wort :math:`w_i.`

  - Falls :math:`M_i` das Wort :math:`w_i` akzeptiert, dann akzeptiert :math:`D` auch.
  - Falls :math:`M_i` das Wort :math:`w_i` verwirft, dann verwirft auch :math:`D`.
  - Falls :math:`M_i` auf :math:`w_i` unendlich lange arbeitet, dann auch :math:`D`. offensichtlich :math:`L(D) = \overline{L}_d`

Zeigen, dass Programmverifikation nicht lösbar ist.

Sei :math:`L_u = \left \{Kod(M) \# w | M \text{ ist eine TM die } w \text{ akzeptiert}\right\}`

Die **universelle Sprache**

Wir haben bereits gesehen, dass es eine universelle Turingmaschine gibt, also ist :math:`L_u` rekursiv auszählbar (:math:`L_u \in \mathscr{L}_{RE}`)

**Theorem:** :math:`L_u \notin \mathscr{L}_R`

**Beweisidee:** Wir zeigen, dass wir eine Turingmaschine die :math:`L_u` entscheidet, dafür verwenden können, um :math:`\overline{L_d}` zu entscheiden.

Da wir bereits wissen, dass :math:`\overline{L}_d \notin \mathscr{L}_R`, kann :math:`L_u` nicht rekursiv sein.

**Anders formluliert:** Wir zeigen :math:`\overline{L}_d \leq_{R} L_u`, d.h. wir zeigen, dass :math:`L_u` mindestens so schwer ist wie :math:`\overline{L}_d`.

Sei :math:`A` eine Turingmaschine, die :math:`L_u` entscheidet. Wir bauen daraus eine Turingmaschine :math:`B` die :math:`\overline{L}_d` entscheidet.

Die Turingmaschine :math:`B` hält immer, weil wir angenommen haben, dass :math:`A` immer hält.

:math:`\Rightarrow B` entscheidet :math:`\overline{L}_d`

Dies ist ein Widerspruch, da wir schon gezeigt haben, dass :math:`\overline{L}_d \notin \mathscr{L}_R`. Da die Turingmaschine :math:`C` offenbar existiert, muss also die Annahme falsch gewesen sein, dass es eine Turingmaschine :math:`A` gibt, die :math:`L_u` entscheidet.

:math:`\Rightarrow L_u \notin \mathscr{L}_R`