========================
Nichtdeterministische EA
========================

**Idee:** Ein NEA kann sich nach dem Lesen eines Wortes in mehreren Zuständen befinden.

**Vorteil:** einfacher zu entwerfen.

**Beispiel:** akzeptiert alle Wörter die mit 01 enden.

..image:: 1_7.jpg

**Transitionstabelle:**

..image:: 1_8.jpg

Mögliche Berechnungen auf dem Wort 00101:

..image:: 1_9.jpg

:math:`\Rightarrow` 00101 wird akzeptiert

**Definition:** Ein NEA A wird beschrieben durch :math:`A=\{Q,\sigma,\delta, q_0, F\}`, wobei :math:`\delta : Q \times \sigma \rightarrow 2^Q` die Transitionsfunktion ist, die für jeden Zustand und jedes Eingabesymbol eine **Menge** von Folgezuständen bestimmt.

Erweiterung der NEA-Transitionsfunktion auf Wörter:

Sei :math:`w \in \sigma, q \in Q`. Dann definieren wir

:math:`\hat{\delta}: Q \times \sigma^* \rightarrow 2^Q` rekursiv wie folgt:

* :math:`\hat{\delta}(q,\epsilon) = \{q\}`
* Sei :math:`w=xa` und :math:`\hat{\delta}(q,x) = \{p_1, ..., p_k\}` für ein :math:`k \in \mathbb{N}`, dann ist :math:`\hat{\delta}(q,w)= \bigcup _{i=1} ^{k} {\delta(p_i,a)}`

**Beispiel:**

:math:`\hat{\delta}(q_0, \epsilon) = \{q_0\}` Grundregel

:math:`\hat{\delta}(q_0, 0) = \delta(q_0,0) = \{q_0, q_1\}`

:math:`\hat{\delta}(q_0, 00) = \delta(q_0, 0) \cup \delta(q_1, 0) = \{q_0, q_1\}`

:math:`\hat{\delta}(q_0, 001) = \delta(q_0, 1) \cup \delta(q_1,1) = \{q_0\} \cup \{q_2\} = \{q_0, q_2\}`

:math:`\hat{\delta}(q_0, 0010) = \delta(q_0, 0) \cup \delta(q_2, 0) = \{q_0, q_1\}`

:math:`\hat{\delta}(q_0, 00101) = \delta(q_0,1) \cup \delta(q_1,1) = \{q_0\} \cup \{q_2\} = \{q_0, q_2\}`

**Definition:** Sei :math:`A=(Q,\sigma, \delta, q_0, F)` ein NEA. Die von A **akzeptierte Sprache** :math:`L(A)` ist :math:`L(A) = \{w \in \sigma^* | \hat{\delta}(q_0,w) \cap F \neq\}`, also die Menge aller Wörter, mit denen vom Startzustand aus ein Endzustand erreichbar ist.

**Frage/Probleme:**

1. Wie kann man möglichst effizient entscheiden, ob ein gegebenes Wort in der Sprache eines gegebenen NEA enthalten ist?
2. Sind NEAs mächtiger als DEAs?

**Antwort:** DEAs und NEAs sind äquivalent.

**Ziel:** Automatische Umwandlung von NEAs in DEAs:

**Teilmengenkonstruktion** (Potenzenmengenkonstruktion)

**Idee:** Zustände des DEA sind Mengen erreichbarer Zustände des NEA.

**Formel:** Sei :math:`N=(Q_N, \sigma, \delta_N, q_0, F_N)` ein NEA. Konstruiere äquivalenten DEA :math:`D=(Q_D, \sigma, \delta_D, \{q_0\}, F_D)` mit

* :math:`Q_D = 2^{Q_N}`
* :math:`F_D = \{S \leq Q_N | S \cap F \neq \varnothing\}`
* :math:`\delta_D(S,a) = \bigcup _{p \in S} \delta_N (p,a)` für :math:`S \in Q_D, a \in \sigma`

**Beispiel:** (von vorher)

Konstruktion des äquivalenten DEAs als Übergangstabelle.

..image:: 1_10.jpg

als graphische Darstellung:

..image:: 1_11.jpg

**Ein ungünstiger Fall für die Teilmengenkonstruktion:**

:math:`L_n = \{w \in \{0,1\} | \text{Das n-te letzte Zeichen von w ist eine 1}\}`

:math:`= \{w \in \{0,1\} | \text{w=x1y mit x} \in \{0,1\}^* \}`

Aber **jeder** DEA für :math:`L_n` brauch mindestens :math:`2^n` Zustände, weil der DEA sich an die letzten n gelesenen Symbole erinnern muss, da er nicht weiss wann das Wortende kommt.

:math:`\rightarrow 2^n` verschiedene Teilwörter müssen unterschieden werden

:math:`\rightarrow 2^n` Zustände nötig