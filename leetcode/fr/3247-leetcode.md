---
titre: LeetCode 3247. Nombre de sous-séquences avec une somme marginale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes – LeetCode 3247
**Nombre de sous-séquences avec somme marginale* *
> Compter tous les sous-séquences dont la somme de l'élément est **odd**.
> Retournez la réponse modulo \(10^9+7\).

> **Constraints**
> - \(1 \leq n = \text{nums.longueur} \le 10^5\)
- \(1 \leq \text{nums}[i] \le 10^9\)

---

- Oui. Aperçu clé

Pour un subséquence seulement la **parité** de sa somme compte.

* Si nous ajoutons un nombre **odd** à une sous-séquence existante, sa parité bascule.
* L'ajout d'un nombre **even** maintient la parité inchangée.

Cela nous permet de garder ** juste deux compteurs**:

"oddCnt"
- C'est quoi ?
Nombre de sous-séquences vus jusqu'à présent avec une somme étrange Nombre de sous-séquences vus jusqu'à présent avec une somme égale Mise à jour après inspection de chaque élément de tableau

Lorsque nous rencontrons un nouveau numéro `x`, nous pouvons décider:

Nouveau "evenCnt"
- C'est quoi ?
*(probabilités existantes, paires existantes retournées, nouvelle séquence `[x]`)*
* (probabilités existantes dupliquées, avec ou sans `x`)* Autres

Toutes les opérations sont effectuées modulo \(10^9+7\).

L'algorithme est un seul passage : **O(n)** temps, **O(1)** espace supplémentaire.

---

Code de la solution

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Chaque mise en oeuvre suit la même logique O(n) DP décrite ci-dessus.

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

Sous-séquence publique d'intCount(int[] nums) {
longue impair = 0;
longue même = 0;

pour (int num : nombres) {
si ((num & 1)] 1) { // nombre impair
longue newOdd = (odd + même + 1) % MOD;
longue nouvelle Même = (odd + even) % MOD;
impair = nouveau Curieusement;
même = nouveau Même;
} autre { // même nombre
long nouveauOdd = (odd * 2) % MOD;
longue nouvelle Même = (même * 2 + 1) % MOD;
impair = nouveau Curieusement;
même = nouveau Même;
}
}
retour (int) impair; // impair Cnt tient la réponse
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
MOD = 1 000 000 007

def subséquence Compte(s), nombres: Liste[int] -> Int:
impair, même = 0, 0
pour num in nums:
si nombre % 2: # impair
new_odd = (odd + même + 1) % soi-même. MOD
new_even = (odd + even) % self. MOD
impair, même = nouveau_odd, nouveau_même
Autre: # même
new_odd = (odd * 2) % self. MOD
new_even = (même * 2 + 1) % self. MOD
impair, même = nouveau_odd, nouveau_même
retour impair
«» "

---

### 3.3 C++

'`cpp
solution de classe {
public:
sous-séquenceCount(vecteur<int>& nums) {
longue MOD = 1'000'000'007LL;
long long impair = 0, même = 0;

pour (int num : nombres) {
si (num & 1) { // impair
long long newOdd = (odd + même + 1) % MOD;
long long nouveau Même = (odd + even) % MOD;
impair = nouveau Curieusement;
même = nouveau Même;
} autre { // même
long long nouveauOdd = (odd * 2) % MOD;
long long nouveau Même = (même * 2 + 1) % MOD;
impair = nouveau Curieusement;
même = nouveau Même;
}
}
retourner static_cast<int>(odd);
}
};
«» "

---

- Oui. Les bons, les mauvais et les méchants

Qu'est-ce qui est bon Qu'est-ce qui est mauvais
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Concept**
**Brute-Force**
**Mémoisation de haut en bas** Nécessite O(n) profondeur de récursion, table de mémo supplémentaire
Un peu plus de code si vous stockez des tableaux.

> **Pourquoi le PDD itératif est la star des interviews* *
> *Fast*: un scan, travail constant par élément.
> *Robust*: aucun risque de récursion, aucun grand tableau auxiliaire.
> *Clear*: deux nombres, deux règles – facile à expliquer sur un tableau blanc.

---

Analyse de complexité

Calcul métrique
C'est pas vrai.
**Heure**="O(n)" – un passage sur le tableau="
**Espace** – seulement deux compteurs 64 bits
**Opérations de Modulo** aussi – chaque étape utilise quelques "% MOD" ops

---

## 6=" Interview-Ready Conseils

1. ** Expliquez d'abord l'observation de la parité** – cela montre que vous comprenez pourquoi seulement deux états sont suffisants.
2. **Parcourir un petit exemple** (par exemple, `[1, 2, 3]`) tout en mettant à jour `oddCnt` et `evenCnt`.
3. **Mention le modulo** – beaucoup d'intervieweurs s'attendent à ce que vous évitez le débordement tôt.
4. **Parlez des alternatives** (force brute, DP avec tableau) et pourquoi vous les avez rejetées.
5. **Afficher le code** dans votre langue préférée, en conservant les noms variables autodescriptifs (`odd`, `even`).

---

# # # 7--

Le problème "Nombre de sous-séquences avec Odd Sum" est un exemple classique de la façon dont une simple observation (flipping de la parité) peut transformer un problème combinatoire apparemment exponentiel en un DP linéaire.
La solution est compacte, efficace et linguistique-agnostique, ce qui en fait un excellent point de conversation.

> **Mots-clés de référence**: LeetCode 3247, nombre de sous-séquences avec somme impair, solution Java DP, solution Python DP, solution C++ DP, codage d'entrevue, interview par algorithme, prép d'entrevue, O(n) DP, parité de programmation dynamique, modulo 1e9+7.

Bonne chance pour votre voyage de codage! C'est ce qu'il a dit