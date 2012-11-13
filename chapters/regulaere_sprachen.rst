========================================
Reguläre Sprachen und ihre Eigenschaften
========================================

**Definition:** Eine Sprache heisst **regulär**, wenn sie von einem DEA akzeptiert wird.

.. math:: \mathcal{L}_{REG} =\mathcal{L} (DEA) = \{L | \text{L ist regulär}\}

**Ziel:** Charakterisierung von regulären Sprachen

Abschlusseigenschaften regulärer Sprachen
-----------------------------------------

1. **Vereinigung:** Wenn :math:`L` und :math:`M` reguläre Sprachen sind, dann ist auch :math:`L \cup M` regulär.

  **Beweis:** Wenn L und M regulär sind, existieren RAs :math:`\alpha` und :math:`beta` für :math:`L` und :math:`M`, d.h. :math:`L(\alpha) = L` und :math:`L(\beta) = M`.
  
  :math:`\Rightarrow \alpha + \beta` ist ein RA, :math:`L(\alpha + \beta) = L \cup M`.
  
analoge Begründung (über die Definition von :math:`\cdot` und :math:`^*`) für

2. **Verkettung:** L,M regulär :math:`\Rightarrow L \cdot M` regulär
3. **Kleenscher Stern:** L regulär :math:`L^*` regulär
4. **Komplement:** Wenn L eine reguläre Sprache über dem Alphabet :math:`\Sigma` ist, dann ist auch :math:`\overline{L} = \Sigma^* -L` regulär.

  **Beweis:** Sei ein DEA für L.
  
  Dann gibt es für jedes Wort w aus :math:`\Sigma^*` einen eindeutigen Zustand, in dem er DEA endet, wenn er w liest.
  
  Aller Wörter aus :math:`L(A) = L` führen in Endzustände, alle anderen Wörter aus :math:`\Sigma^* - L = \overline{L}` in nichtakzeptierende Zustände.
  
  Vertauschen von Endzuständen und Nichtendzuständen ergibt einen DEA für :math:`\overline{L}`
  
5. **Durchschnitt:** Wenn :math:`L` und :math:`M` reguläre Sprachen sind, dann ist auch :math:`L \cap M` regulär.

  **Beweis:**
  
  De Morgansche Gesetze:
  
  :math:`\overline{A \cap B} = \overline{A} \cup \overline{B}`
  
  :math:`\overline{A \cup B} = \overline{A} \cap \overline{B}`
  
  L,M regulär :math:`\Rightarrow \overline{L}, \overline{M}` regulär
  
  :math:`\Rightarrow \overline{L} \cup \overline{M}` regulär
  
  :math:`\Rightarrow \overline{\overline{L} \cup \overline{M}}` regulär
  
  :math:`\overline{\overline{L}} \cap \overline{\overline{M}} = L \cap M` regulär
  
6. **Mengendifferenz:** Wenn :math:`L` und :math:`M` regulär sind, ist :math:`L - M` regulär.

  **Beweis:** Es gilt :math:`L - M = L \cap \overline{M}`
  
7. **Spiegelung:**

  **Definition:** Sei :math:`w = a_1 ... a_k` ein Wort. Dann ist :math:`w^R = a_k ... a_1` die Spiegelung von w
  
  **Bemerkung:**
  
  * :math:`\epsilon^R = \epsilon`
  * :math:`(w^R)^R = w`
  
  Sei :math:`L \leq \Sigma^*` eine Sprache. Dann ist :math:`L^R = \left \{ w \in \Sigma^* | w^R \in L \right \}` die Spiegelung von L.
  
  **Satz:** Wenn L regulär ist, dann ist auch :math:`L^R` regulär.
  
  **Beweis 1:** Sei :math:`A = (Q, \Sigma, \delta, q_0, F)` ein DEA für L.
  
  Wir konstruieren einen :math:`\epsilon`-NEA B für :math:`L^R` wie folgt:
  
  :math:`B = (Q \cup \{q_s\}, \Sigma, \delta_B, q_S, F_B)` mit
  
  * :math:`F_B = \{q_0\}`
  * :math:`\delta_B (q, a) = \{p\} \text{für} \delta(p,a) = q`
  * :math:`\delta_B (q_S, \epsilon) = \{p\} \text{für alle} p \in F`
  
  B simuliert A in umgekehrter Richtung :math:`\Rightarrow` B akzeptiert :math:`L^R`
  
  **Beispiel:** :math:`L = \left \{ w \in {\{a,b\}}^* | \text{w endet auf ba oder ab} \right \}`
  
  DEA A für L:
  
  .. image:: 4_1.jpg
  
  :math:`L^R = \left \{ w \in {\{a,b\}}^* | \text{w beginnt mit ab oder ba} \right\}`
  
  .. image:: 4_2.jpg
  
  **Beweis 2:** Sei :math:`\alpha` ein regulärer Ausdruck mit :math:`L(\alpha) = L`
  
  zu Zeigen: es gibt einen RA :math:`\beta` mit :math:`L(\beta) = (L(\alpha))^R = L^R`
  
  Strukturelle Induktion über den Aufbau von :math:`\alpha`:
  
  * Induktionsanfang:
    
    :math:`\epsilon^R = \epsilon`
    
    :math:`\varnothing^R = \varnothing`
    
    :math:`q^R = a \text{für ein} a \in \Sigma`
    
  * Induktionsschritt:
  
    (i) :math:`\alpha = \alpha_1 + \alpha_2`
    
      :math:`L(\alpha_1 + \alpha_2)^R = (L(\alpha_1) \cup L(\alpha_2))^R = L(\alpha_1)^R \cup L(\alpha_2)^R`
      
      :math:`\Rightarrow \alpha^R = \alpha_1^R \alpha_2^R`
      
    (ii) :math:`\alpha = \alpha_1 \alpha_2`
    
      :math:`L(\alpha_1 \alpha_2)^R = (L(\alpha_1) L(\alpha_2))^R = L(\alpha_1)^R L(\alpha_1)^R`
      
      :math:`\Rightarrow \alpha^R = \alpha_2^R \alpha_1^R`
      
    (iii) :math:`\alpha = \alpha_1^*`
    
      :math:`L(\alpha_1^*)^R = (L(\alpha_1)^R)^*`
      
      :math:`\Rightarrow \alpha^R = (\alpha_1^R)^*`

8. **Homomorphismus:**

  **Definition:** Ein (Wort-) Homomorphismus ist eine Abbildung :math:`h: \Sigma_1 \rightarrow \Sigma_2^*`, die die Symbole eines Alphabets auf Wörter abbildet.
  
  **Beispiel:** :math:`\Sigma_1 = \{0,1\}, \Sigma_2 = \{a,b\}, h(0) = ab, h(1) = \epsilon`
  
  Erweiterung auf Wörter: Sei :math:`w = a_1 ... a_k`. Dann ist :math:`h(w) = h(a_1) \cdot h(a_2) ... h(a_k)`
  
  **Beispiel:** :math:`h(0101) = ab \cdot \epsilon \cdot ab \cdot \epsilon = abab`
  
  **Definition:** Sei :math:`h: \Sigma_1 \rightarrow \Sigma_2^*` ein Homomorphismus, sei :math:`L \leq \Sigma_1^*` eine Sprache.
  
  Dann ist :math:`h(L) = \left \{ w \in \Sigma_2^* | w = h(x) \text{für ein} x \in L \right\}`
  
  :math:`= \left \{ h(x) | x \in L \right\}`
  
  Satz: Sei :math:`h: \Sigma_1 \rightarrow \Sigma_2^*` ein Homomorphismus. Wenn :math:`L \leq \Sigma_1^*` regulär ist, dann ist auch :math:`h(L)` regulär.
  
  **Beweis:** Für einen regulären Ausdruck :math:`\alpha` über :math:`\Sigma_1` ist :math:`h(\alpha)` der reguläre Ausdruck über :math:`\Sigma_2`, der entsteht, wenn jedes Vorkommen von :math:`a \in \Sigma_1` durch :math:`h(a)` ersetzt wird. (strukturelle Induktion)
  
  **Beispiel:** :math:`\Sigma_1 = \{0,1\}, \Sigma_2 = \{a,b\}, h(0) = ab, h(1) = \epsilon`
  
  :math:`\alpha = ((0 + 1) 0)^* 1 \Rightarrow h(\alpha) = ((ab + \epsilon) ab)^* \epsilon = (ab)^*`
  
  Es gilt: :math:`L(h(\alpha)) = h(L)`