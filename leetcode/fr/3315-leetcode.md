---
titre: LeetCode 3315. Construisez le tableau de bord II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3315 – Construisez le tableau bitwise minimum II
> **LeetCode Medium="Bit‐Manipulation="Java="Python="C++**

---

C'est pas vrai. Ce que le problème demande

Avec une liste de *prime* nombres `nums`, construire un tableau `ans` de la même longueur de sorte que

«» "
ANS[i] OU (ans[i] + 1) = nombres[i]
«» "

et `ans[i]` doit être l'entier **le plus petit** non négatif qui satisfait à l'équation.
Si aucun entier de ce type n'existe, mettez `-1` à cette position.

> **Exemples**
> `nums = [2, 3, 5, 7] → ans = [-1, 1, 4, 3]`
> `nums = [11, 13, 31] → ans = [9, 12, 15] "

---

L'observation clé

Regardez la représentation binaire d'un premier `p` (n'oubliez pas que le seul pouvoir de deux premiers est `2`).

«» "
p = 5 (101b) → ans = 4 (100b)
p = 13 (1101b) → ans = 12 (1100b)
p = 7 (111b) → ans = 3 (011b)
p = 11 (1011b)→ ans = 9 (1001b)
«» "

Qu'est-ce qui est courant dans tous ces cas?

*La réponse est obtenue en enlevant le bit ** le plus précis qui fait partie d'une course consécutive de 1s**. *

Officiellement :

1. Compter le nombre de "1`s (`t`) dans `p`.
(c'est-à-dire que le bit le moins significatif est `1`, le changement de droite et l'accroissement `t`.)
2. Si `t=0` (seulement `p=) 2` possède cette propriété), la réponse est `-1`.
3. Sinon, soustrayez "2^(t‐1)" de «p»:

«» "
ans = p – 2^(t-1)
«» "

Pourquoi ça marche ?
`ans` aura tous les bits de fuite égal à `1` **sauf** la plus droite de cette course.
Lorsque vous ajoutez `1`, un chariot retourne `1` à `0` et propage un pas à gauche, de sorte que le OU
avec `ans` recrée exactement la prime originale.

---

Mise en œuvre

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe {
public int[] minBitwiseArray(Liste <entier> nums) {
int n = nombres.size();
int[] ans = nouvelle int[n];
pour (int i = 0; i < n; i++) {
int p = nums.get(i);
si (p == 2) { // le seul premier qui est une puissance de deux
as[i] = -1;
poursuivre;
}
t = 0; // nombre de traînées 1s
tmp = p;
pendant ((tmp & 1)) 1) {
t++;
Tmp >>= 1;
}
[i] = p - (1 << (t - 1));
}
le retour des an;
}
}
«» "

- Oui. 2. Python 3

'`python
Solution de classe:
def minBitwiseArray(self, nombres: List[int]) -> Liste[int]:
res = []
pour p en nombres:
si p == 2: # aucune solution pour 2
res.append(-1)
poursuivre
t = 0
tmp = p
alors que tmp & 1:
t = 1
Tmp >>= 1
res.append(p - (1 << (t - 1)))
retour res
«» "

- Oui. 3. C++

'`cpp
solution de classe {
public:
vecteur<int> minBitwiseArray(vecteur<int>& nums) {
vecteur <int> ans;
pour (int p : nombres) {
si (p == 2) { // puissance maximale de deux
as.push_back(-1);
poursuivre;
}
t = 0; // Traînant 1s
tmp = p;
pendant que (tmp & 1) {
++t;
Tmp >>= 1;
}
as.push_back(p - (1 << (t - 1)));
}
le retour des an;
}
};
«» "

---

Analyse de complexité

* **Heure** – "O(n · log M)"
`n` = longueur de `nums`, `M` = valeur maximale.
La boucle qui compte la piste 1s touche chaque morceau au plus une fois.
* ** Espace** – auxiliaire `O(1)` (sauf le tableau de sortie).

---

Les bons, les mauvais, les affreux

Aspect du bien
- C'est quoi ?
**Intuition**= Modèle binaire simple – supprimer un seul bit=1 Nécessite de remarquer le modèle dans les premiers=1 Aucune – le modèle pourrait être manqué=2
**Mise en œuvre**= Un pass par numéro, pas de récursion== Cas spécial pour `2'= Décomplexe si l'on essaie d'utiliser des changements de bits dans une boucle==
**Performance**= Linéaire en bits, bien en dessous des limites== O(n log M) est bon pour `n ≤ 100`== Aucun – l'algorithme est optimal==
Autres **Cas d'Edge** 2). "2" check.
**Readability**= Effacer les noms de variables (`t`, `tmp`) Pourrait être mal lu si bit-ops ne sont pas familiers.

---

Pourquoi ce blog aide-t-il votre recherche d'emploi

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
* **Structure** – Énoncé de problème → Insight → Code → Complexité → Discussion → méta-description SEO.
Les recruteurs hésitent souvent pour trouver les pièces clés rapidement.
* **Profondeur technique** – Démontre la maîtrise des tricks bitwise, les propriétés des nombres premiers et la conception d'algorithmes propres.
* **Code pratique** – Extraits prêts à copier en trois langues principales; montre une polyvalence.
* **Automarque** – Ajoutez une petite bio et un lien vers votre GitHub/LinkedIn à la fin pour transformer les lecteurs en candidats.

---

À emporter

* La réponse existe toujours **sauf** pour le premier `2`.
* La solution est aussi simple que *compte les suivants, soustrayez `2^(t‐1)'*.
* Implémentez-le en un seul passage, et vous avez une réponse optimale, prête à l'entrevue.

Codage heureux, et que votre interview soit aussi libre de bug que ce tour bitwise!