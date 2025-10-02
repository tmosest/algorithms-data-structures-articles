---
titre: LeetCode 862. Subarray courte avec somme au moins K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**LeetCode 862 – Subarray le plus court avec somme au moins K* *

**Idée clé**
La somme d'un \([i+1, j]\) subarray peut être calculée rapidement
`pref[j] – pref[i]`, où `pref` est un tableau de préfixes.
Pour trouver la plus courte de ces subarraies, nous maintenons une deque **monotonique** des indices préfixe-somme :

* **Front** – donne le plus petit préfixe qui pourrait former un subarray valide se terminant à l'index courant.
* **Retour** – Nous rejetons les indices dont la somme du préfixe n'est pas plus petite que celle du courant, parce qu'ils ne peuvent pas produire un sous-array plus court plus tard.

---

Algorithme
«» "
1. Construire le tableau préfixe pref[0...n] (pref[0] = 0).
2. minLen ←
3. Pour j = 0 ... n:
• Bien que ne soit pas vide et pref[j] - pref[dq.front()] ≥ k:
minLen ← minLen, j - dq.front())
dq.pop_front() // front n'est plus utile
• Bien qu'il ne soit pas vide et que pref[j] ≤ pref[dq.back()]:
dq.pop_back() // maintenir des montants de préfixe croissants
• dq.push_back(j)
4. Retour (minLen)
«» "

---

Pourquoi ça marche ?

* `pref[j] - pref[dq.front()] ≥ k` → subarray `[dq.front()+1 ... j]` a la somme ≥ k.
L'enlever du front ne peut que rendre les candidats futurs plus longs, donc il est sûr de sauter.
* Le popping du dos ne conserve que les montants préfixés *minimaux* à des indices antérieurs, garantissant que toute subarray ultérieure sera au moins aussi courte si elle commence après l'un de ces indices.

---

Complexité
* **Heure:** `O(n)` – chaque index entre et quitte la deque au plus une fois.
* **Espace:** `O(n)` – préfixe tableau + deque.

---

**Ligne de bottom:** Utilisez un tableau de somme préfixe ainsi qu'une deque monotonique pour vérifier et mettre à jour le plus court subarray, en réalisant le temps linéaire et l'espace.