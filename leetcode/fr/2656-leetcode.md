---
titre: LeetCode 2656. Somme maximale avec des éléments exactement K - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2656. Somme maximale avec des éléments exactement K
**Leetcode Facile – 100 % résolu avec une formule gourmande* *

> **Objectif** – Choisissez un élément *k* fois pour maximiser le score total.
> Chaque fois que vous choisissez *m* vous obtenez `+m` à votre partition, l'élément est supprimé, un nouvel élément `m+1` est inséré, et le tableau est mis à jour.

---

Résumé du problème

- Oui.
-- -- -- -- -- --
**Array** "nums" (en chiffres)
**Longueur** Autres
**k**
**Retour**= score maximum possible après les choix exactement *k*=

---

C'est pas vrai. Pourquoi une prise de graisse est optimale

1. **Augmentation de la valeur** – Après avoir choisi *m*, le même élément devient *m+1*.
2. **Valeur finale** – Choisir un élément plus petit ne peut jamais produire une valeur plus grande que choisir le maximum actuel, car l'élément choisi est *toujours* augmenté de 1 et reste le plus grand après le choix.

**Par conséquent**:
> **Choisissez toujours l'élément maximal actuel**.
> La séquence des pics sera :
> `max, max+1, max+2, ..., max+(k-1)`

Le score total est simplement la somme de cette progression arithmétique.

---

Formule mathématique

«» "
somme = k * max + (k * (k - 1)) / 2
«» "

* `k * max` – nous choisissons le maximum d'origine *k* fois.
* `(k * (k - 1)) / 2` – les valeurs progressives ajoutées par l'opération +1 à chaque fois.

La formule est O(1) après avoir trouvé «max».

---

- Oui. Algorithme (Pseudocode)

«» "
maxVal = élément maximal dans les nombres
réponse = k * maxVal + k * (k - 1) / 2
réponse de retour
«» "

*Trouver `maxVal`* – un simple balayage linéaire (O(n)).
Le reste est le temps constant.

---

## 4-

- Oui.
-- -- -- -- -- --
**Temps** $ `O(n)" – seul le balayage pour le maximum $
**Espace** – pas de structures de données supplémentaires

---

Mise en œuvre du code

> Toutes les solutions supposent que le tableau n'est pas vide et que *k* est valide en fonction des contraintes.

Java

"Java
solution de classe {
public int maximSum(int[] nums, int k) {
int max = entier.MIN_VALUE;
pour (int n : nombres) {
si (n > max) max = n;
}
retour k * max + k * (k - 1) / 2;
}
}
«» "

Python

'`python
Solution de classe:
def maximum Sum(self, nombres: Liste[int], k: int) -> Int:
max_val = max(nums)
retour k * max_val + k * (k - 1) // 2
«» "

C++

'`cpp
solution de classe {
public:
Int maximum Sum(vector<int>& nums, int k) {
int mx = *max_element(nums.begin(), nums.end());
retour k * mx + (k * (k - 1)) / 2;
}
};
«» "

Les trois implémentations sont moins de 20 lignes, rapides et claires.

---

# # # 6 Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Simplicité**= formule monoligne après avoir trouvé max== Pas besoin de simuler les opérations k== Aucune=
**Performance**=O(n) temps, espace O(1)=Ouvre dans les contraintes=Si vous simulez naïvement, O(nk) pourrait être *excessif* pour les contraintes plus grandes=
**Cas d'Edge**=Poignées `k = 1`, `max` à n'importe quel index=====================================================================================================================================================================================================================================
**Proof of Correctness**=Progression arithmétique claire== Parfois négligée dans les interviews==Une preuve gourmande doit être écrite: montrer que remplacer un choix par le maximum actuel ne diminue jamais les choix futurs===
**Interview Talk**) Quick (pick) l'argument max) Nécessite d'expliquer pourquoi choisir les plus grands reste optimum.

---

# # 7-

1. **Simulant le tableau** – Les élèves écrivent souvent une boucle qui supprime un élément et repousse `m+1`. Cela n'est pas nécessaire et peut conduire à une ETM si les contraintes étaient plus grandes.
2. **Manquement du terme incrémental** – L'oubli du terme `(k * (k-1))/2` entraîne une sous-estimation de la réponse.
3. **Débordement entier** – Dans les langues avec des limites de 32 bits, utiliser `long`/`long` si `k` ou `max` étaient plus grands (pas besoin ici, mais bonne pratique).
4. **En supposant que le tri est nécessaire** – le tri du tableau est O(n log n) et inutile.

---

- Oui. Comment utiliser ce blog pour votre recherche d'emploi

1. ** Mots clés du référencement** – Le titre et les titres contiennent des termes à volume élevé: *Somme maximale avec des éléments exactement K, Leetcode 2656, algorithme gourmand, interview de codage*, etc.
2. **Readable, Structured Content** – Les intervieweurs apprécient les explications claires. Copiez la section « Bon, mauvais, mauvais » pour présenter votre réflexion analytique.
3. **Lien vers le code** – Fournir des extraits dans les trois langues principales. Les recruteurs recherchent souvent la polyvalence linguistique.
4. **Proof & Complexité** – Mention de complexité temps/espace; les recruteurs veulent des solutions concises et correctes.
5. **Afficher le processus de pensée** – Dans votre curriculum vitae ou portfolio, référez ce billet de blog comme un problème que vous avez résolu; utilisez la section "Proof of Correctness" comme preuve d'une compréhension profonde.

---

TL;DR

- **Cueillir le nombre de fois maximum de k.
- Score total = `k * max + k*(k-1)/2`.
- Temps O(n), espace O(1).
- Implémentation en Java, Python et C++ fournis.

Utilisez cette solution concise et éprouvée pour ace Leetcode 2656 et impressionnez les intervieweurs avec un algorithme clair et optimal. C'est ce qu'il a dit