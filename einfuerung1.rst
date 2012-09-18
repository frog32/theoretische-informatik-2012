=======================
Theoretische Informatik
=======================

Buch: Einführung in die Automatentheorie, Formale Sprachen und Berechenbarkeit
Hopcraft, Motwan, Ullman
3. Auflage

Prüfungen
---------
| Hilfsmittel: Buch, Unterlagen
| Zw. Prüfung: 30. Okt 11. Dez

Ergänzende Literatur
--------------------
| Vossen, Witt: Grundkurs theoretische Informatik
| Sipser: Introduction to Theory of Computation
| Hormkovic: theoretische Informatik

Was ist theoretische Informatik
===============================

Konkrete Konzepte: Algorithmus, Berechnung, Komplexität

Was will die theoretische Informatik?
*************************************
Formale Bestimmung der Begriffe, unabhängig von Hard und Software.

Ziel:
~~~~~
* Grundlegende Eigenschaften von Algorithmen und Berechnungen erkennen.
* Methoden entwickeln zum Entwurf beweisbar korrekter Hard- und Software.
  (nicht Schwerpunkt dieser Vorlesung)
* Grenzen der automatischen Berechnung aufzeigen

Typische Fragestellungen:
~~~~~~~~~~~~~~~~~~~~~~~~~
* Ist es möglich, ein Programm zu schreiben, das ein anderes Programm als
  Eingabe erhält und feststellt ob dieses in eine Endlosschleife laufen kann?
  
  Antwort: NEIN!
* Gegeben ein Rucksack mit 30l Fassungsvermögen und 50 Gegenstände.

  Wie lange dauert es, herauszufinden wie viele der Gegenstände in den Rucksack
  passen?
  
  Antwort: zu lange! (exponentielle in der Anzahl der Gegenstände)
  
  Bemerkung: Die Antwort auf solche Fragen ist keineswegs immer offensichtlich.

Aufgabe
*******
Gegeben sei das folgende Strassennetz

.. image:: images/e1graph.jpg

a. Gibt es eine Möglichkeit alle Strassen genau einmal zu durchqueren und am
   Ausgangspunkt wieder anzukommen?
b. Gibt es eine Möglichkeit jede **Kreuzung** genau einmal zu passieren und am
   Ausgangspunkt wieder anzukommen?

Lösung
~~~~~~
a. **Einfache Aufgabe**: Geht immer, wenn die Anzahl der Abzweigungen an jeder
   Kreuzung gerade ist.
b. **Schwierige Aufgabe**: Keine wesentlich bessere Methode bekannt, als alles
   durchzuprobieren.
   
   Traveling Salesperson Problem TSP

Ziel
~~~~
Um solche Fragestellungen systematisch zu beantworten zu können, brauchen wir
ein **exaktes mathematisches Modell** eines Computers.

Automatentheorie
================

1. endliche Automaten
2. kontextfreie Grammatiken und Keller-Automaten

Zusätzliche Motivation: Compilerbau, Textverarbeitung

Endliche Automaten - Motivationsbeispiele
*****************************************

Modellierung eines Kippschalters:

.. image:: images/1kippschalter.jpg

* Zwei **Zustände**, davon ein *Startzusatand* und ein **akzeptierender**
  Zustand.
* **Transitionen** (Zustandsübergänge) führen den Automaten anhand einer Eingabe
  von einem Zustand in den anderen.

Beispiel
~~~~~~~~
Mustererkennung in Texten: Suche Wort "then"

.. image:: images/1then.jpg

Getränkeautomat
~~~~~~~~~~~~~~~
Anschauliches Beispiel eines endlichen Automaten (mit Ausgabe)

====== ======
Cola   2.- Fr
Wasser 1.- Fr
====== ======

Formale Sprachen
================
Ziel
****
Genaue Beschreibung der Ein- und Ausgabe eines Automaten.

Definition
**********
**Alphabet** - eine endliche, nicht leere Menge von **Symbolen**(Buchstaben)

Beispiel
~~~~~~~~

binäres Alphabet: :math:`sum_bin = {0,1}`
Tastaturalphabet: :math:`sum_alph = {a,b,c.....}`

**Wort** (auch Zeichenkette)
endliche Folge von Symbolen eines gegebenen Alphabets

Beispiel
~~~~~~~~
01110 ist eine Wort über :math:`sum_bin`

**leeres Wort** epsilon (manchmal lambda)

leere Folge von Symbolen (über beliebigem Alphabet)

Länge eines Wortes
~~~~~~~~~~~~~~~~~~
:math:`|w|` bezeichnet die Anzahl der Symbole im Wort w
:math:`|\epsilon|` = 0

Konvention
**********
========= =======================
a,b,c,... für Buchstaben, Symbole
v,w,y,... für Wörter
========= =======================

Definition
**********

Mengen aller Wörter einer bestimmten Länge sei :math:`sum()` Alphabet


:math:`{\sum}^0 = {\epsilon}` Wörter der Länge 0
:math:`{\sum}^1 = \sum` alle Wörter der Länge 1
:math:`{\sum}^2 = {ab|a,b element \sum}` alle Wörter der Länge 2
:math:`{\sum}^i`= {a_1...a_i|a_1,...,a_i element \sum}` alle Wörter der Länge i

:math:`{\sum}^* = \bigcup_{i=1}^\infty {\sum}^i` Menge aller Wörter über :math:`\sum`

:math:`{\sum}^+ = \bigcup_{i=0}^\infty {\sum}^i` Menge aller **nichtleeren** Wörter über :math:`\sum`

Definition Konkatenation (Verkettung)
*************************************

:math:`v=a_1...a_k, w=b_1...b_c über \sum`

:math:`v*w = a_1...a_k b_1...b_c`

Kurz: vw

Beispiel
********
.. math::
  v=abc w=cba
  vw= abccba
  
Berechnungen
============
(a) :math:`u\cdot(v\cdot w) = (u\cdotv)\cdot w`
(b) :math:`|x\cdoty| = |x| \cdot |y|`
(c) :math:`x\cdot\epsilon = \epsilon\cdotx = x`
  
Definition
**********
Seien :math:`v,w \in {\sum}^*` für ein Alphabet :math:`\sum`.

v ist ein **Teilwort** (Infix) von w fals es :math:`x,y\in {\sum}^*` gibt, so
dass :math:`w=x*v*y`

v ist ein Präfix von w falls es :math:`y\in{\sum}^*` gibt, so dass :math:`w=x*v`

v ist Suffix von w, falls es :math:`x \in{\sum}^*` gibt, so dass :math:`w=x*v`

Beispiele
*********
* abc ist Teilwort von aabcc
* aa ist Präfix und Suffix von aabcaa
* :math:`\epsilon` ist Teilwort von jedem Wort
* Jeder Präfix und Suffix ist Teilwort

Definition Sprache
******************
L über Alphabet :math:`\sum` ist eine Teilmenge von :math:`{\sum}^*, L\leq{\sum}^*`

Mengen von Wörtern, kann unendlich gross sein

**Leere Sprache**: :math:`\varnothing` enthält keine Wörter (ist über jedem Alphabet definitert)

:math:`L_\epsilon = \{\epsilon\}`: Sprache, die das leere Wort enthält

:math:`L_\epsilon\neq\varnothing`

Definition Konkatenation von Sprachen
*************************************
:math:`L_1,L_2\leq{\sum}^*`

:math:`L_1 \cdot L_2=L_1 L_2 = \{v \cdot w | v \in L_1 und w \in L_2\}`

Potenzen von Sprachen
*********************
:math:`L^0 = L_\epsilon = \{\epsilon\}`

:math:`L^{i+1} = L^i \cdot L für i \in \mathbb{N}`

Kleene-Stern
************
:math:`L^* von L^i`

:math:`L^* = \bigcup L^i = L^0 \cup L^1 \cup L^2 \cup ...`

:math:`L^+ = L^* - L_\epsilon = \bigcup_{i\in\mathbb{N}-\{0\}}L^i`

Beispiel
~~~~~~~~
.. math::
  
  Sei \sum = \{a,b\}
  
  L_1 = \{a^i | i\geq 0\} = \{\epsilon, a, aa, aaa, ....\}
  
  L_2 = \{a^j | j\geq 0\} = \{\epsilon, b, bb, bbb, ....\}
  
  L_1 \cdot L_2 = \{\epsilon, a, b, ab, aab, abb, aaab,...\}
  
  = \{a^i b^j | i \geq 0, j \geq 0\}
  
= Menge aller Wörter über {a,b}, in dem alle as vor allen b's vorkommen.

Aufgabe
~~~~~~~
Gilt :math:`(L_1 \cdot L_2) \cdot L_3 = L_1 \cdot (L_2 \cdot L_3)`?
   
Ja die Konkatenation ist komutativ
   
.. math::
 (L_1 \cdot L_2) \cdot L_3 = \{v \cdot w | v \in L_1 und w \in L_2\}
 
 =\{xyw | x \in L_1, y \in L_2, w \in L_3\}
 
 =\{xz | x \in L_1, z \in L_2 \cdot L_3\}
 
 = L_1 \cdot {L_2 \cdot L_3}
 

Gilt :math:`(L_1 \cup L_2) \cdot L_3 = L_1 \cdot L_3 \cup L_2 \cup L_3`?

.. math::
  (L_1 \cup L_2) \cdot L_3 = \{vw | v \in L_1 \cup L_2, w \in L_3\}
  
  = \{vw | v \in L_1, w \in L_3\} \cup \{vw | v \in L_2, w \in L_3\}
  
  = (L_1 \cdot L_3) \cup (L_2 \cdot L_3)
  
Gilt :math:`(L_1 \cdot L_2) \cup L_3 = (L_1 \cup L_3) \cdot (L_2 \cup L_3)`?

Nein Gegenbeispiel

.. math::
  L_1 = L_2 = \{a\}, L_3 = \{b\}
  
  L_1 \cdot L_2 = \{aa\}
  
  L_1 \cup L_3 = \{a,b\} = L_2 \cup L_3


Gilt :math:`L_1 \cdot L_2 = L_2 \cdot L_1`?
   
Die Konkatenation ist nicht assoziativ

.. math::
  L_1 = \{a\}, L_2 = \{b\}
  L_1 \cdot L_2 = \{ab\} \neq L_2 \cdot L_1 = \{ba\}
  
Bemerkung gilt aber für :math:`\left |\sum \right | = 1`

Definition Entscheidungsproblem
*******************************
Eingabe: Eine Sprache L über einem Alphabet :math:`\sum und ein Wort
:math:`w \in {\sum}^*`

Ausgabe: JA, falls :math:`w \in L`, Nein falls :math:`w \notin L`

Modellierung von vielen alltäglichen Berechnungsproblemen im Formalismus der
formalen Sprachen.

Beispiel Primzahltest
~~~~~~~~~~~~~~~~~~~~~

:math:`\sum = \{0,1\}`
  
  
  L = \left \{ w \in {\sum}^* | w ist Binärdarstellung einer Primzahl \right\}
  
  Eine Zahl p \in \mathbb{N} ist Primzahl genau dann, wenn Bin(p) \in L.
  
Identifizierung von Sprachen als Probleme.