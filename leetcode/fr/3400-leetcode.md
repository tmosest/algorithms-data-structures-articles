---
titre: LeetCode 3400. Nombre maximal d'indices correspondants après les quarts de travail à droite -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 3400 – Nombre maximal d'indices correspondants après des quarts de travail à droite

> **Problème**
> Compte tenu de deux tableaux entiers `nums1` et `nums2` de longueur égale, vous pouvez effectuer n'importe quel nombre de *justes quarts* sur `nums1`.
> Un décalage droit déplace l'élément à l'index `i` vers `(i + 1) % n`.
> Un indice `i` est **matching** si `nums1[i] == nums2[i]`.
> Retournez le nombre **maximum** d'indices de correspondance que vous pouvez obtenir après un nombre arbitraire de bons quarts de travail.

> **Constraints**
> * `1 ≤ nombres1.longueur = nombres2.longueur ≤ 3000`
> * `1 ≤ nums1[i], nums2[i] ≤ 10^9`

> **Lien** – <https://leetcode.com/problems/maximum-number-of-matching-indices-after-right-shifts/>

---

Pourquoi ce problème est-il un emploi-interview Gold-Mine

* **Manipulation d'images + hachage** – sujets classiques dans les interviews de structures de données.
* **Arithmétique modulaire** – montre que vous pouvez penser clairement aux déplacements circulaires.
* ** compromis espace-temps** – vous devez choisir la bonne structure de données pour la vitesse.
* **Language-agnostic** – des solutions existent en Java, Python, C++, etc.

Les moteurs de recherche adorent ce sujet lorsqu'ils sont combinés avec les mots-clés LeetCode 3400, Droite shift, Indices d'appariement et Interview d'emploi. Cet article est entièrement optimisé pour les recruteurs à la recherche de talents algorithmiques.

---

## C'est Brute-Force Insight

Une approche naïve consiste à simuler **chaque** changement possible (0...n‐1) et compter les matches.

Texte
maxMatches = 0
pour le quart en 0..n-1:
matches = 0
pour i en 0..n-1:
si nombres1[(i - poste + n) % n] == nombres2[i]:
équivalences += 1
maxMatches = max(maxMatches, allumettes)
«» "

*Heure*: 'O(n2)'
*Espace*: "O(1)"

Avec `n ≤ 3000`, cela passe LeetCode, mais vous pouvez faire *much better* en voyant qu'un match dépend seulement de ** combien d'indices dans nums1 aligner avec la même valeur dans nums2**.

---

Stratégie optimale – Fréquence des quarts de travail

1. **Mapper chaque valeur dans `nums1` à la liste des indices où elle se produit. **
2. Pour chaque indice «i» en «nums2», consulter les indices «nums2[i]» en «nums1».
3. Pour chacun de ces indices "idx", calculez le décalage qui amène "idx" à "i" :

«» "
déplacement = (idx - i + n) % n
«» "

4. Incrément d'un compteur de «poste de contrôle».
5. La réponse est la valeur maximale dans le "shiftCount".

Pourquoi ça marche ?
Si `nums1[idx]] == nums2[i]` et que nous sommes en position droite `nums1` par `shift`, alors `idx` passe à `(idx + shift) % n`.
Le paramètre égal à `i` donne exactement la formule de décalage ci-dessus.
Toutes les paires qui correspondent à *pour le même quart de travail* contribuent au même seau dans "shiftCount".

**Complexités* *

Métrique Brute-Force
C'est pas vrai.
"O(n2)" "O(n · f)" où "f" est la fréquence moyenne des valeurs ("n") → la pire "O(n2)" mais pratiquement beaucoup plus rapide. Autres
Espace "O(1)" "O(n)" pour le compteur de décalage + cartographie des valeurs vers les indices. Autres

---

Code en 3 langues

> Toutes les solutions sont **O(n2) dans le pire des cas** mais fonctionnent confortablement sous les contraintes.
> Ils manipulent correctement les duplicata et évitent les pièges de modulo négatifs.

### Java

"Java
Importation de java.util.*;

solution de classe {
Nombre maximal d'indices(int[] nombres1, int[] nombres2) {
int n = nombres1.longueur;
// Valeur de la carte -> liste des indices où elle apparaît en nombres1
Carte<entier, liste<entier>> positions = nouvelle HashMap<>();
pour (int i = 0; i < n; i++) {
positions.computeIfAbsent(nums1[i], k -> nouvelle liste de distribution<>()add(i);
}

int[] shiftCount = nouvelle int[n];
Int maxMatches = 0;

pour (int i = 0; i < n; i++) {
Liste<integer> idxList = positions.get(nums2[i]);
si (idxList == null) continuer; // valeur non présente en nombres1
pour (int idx : idxList) {
changement d'int = (idx - i + n) % n; // changement de droite nécessaire pour aligner idx sur i
Déplacement Nombre[poste]++;
si (déplacement[déplacement] > maxMatches) {
maxMatches = décalageCount[shift];
}
}
}
retour maxMatches;
}
}
«» "

Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maximum Indices correspondants(self, nums1: List[int], nums2: List[int]) -> Int:
n = len(nums1)
pos = defaultdict(list) # value -> liste des indices dans nums1
pour i, val dans l'énumération(nums1):
Pos[val].append(i)

_compte de changement = [0] * n
_matches max = 0

pour i, valeur dans l'énumération(nums2):
pour idx dans pos.get(val, []):
déplacement = (idx - i + n) % n
= nombre de postes 1
si shift_count[shift] > max_matches:
max_matches = poste_compte[poste]

_matches de retour max
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximumMatchingIndices(vecteur<int>& nums1, vecteur<int>& nums2) {
int n = nombres1.size();
non ordonné_map<int, vector<int>> pos; // valeur -> indices en chiffres
pour (int i = 0; i < n; ++i) pos[nums1[i]].push_back(i);

vecteur<int> changementCount(n, 0);
Int maxMatches = 0;

pour (int i = 0; i < n; ++i) {
auto it = pos.find(nums2[i]);
si (it == pos.end() continue;
pour (int idx : it->seconde) {
changement d'int = (idx - i + n) % n;
Déplacement Nombre[poste]++;
maxMatches = max(maxMatches, shiftCount[shift]);
}
}
retour maxMatches;
}
};
«» "

---

Cas de bord & Gotchas

Autres Décision Pourquoi ça compte ?
Il n'y a pas de lien entre les deux.
**Dupliquer les valeurs**=________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
Autres * Pas de correspondances * * Certaines valeurs de `nums2` n'apparaissent jamais dans `nums1` , `get` / `find` retourne la liste/itats vides à `continue` Autres
**Modulo négatif**
**Large `n`**

---

Conseils pour l'entrevue

1. ** Expliquez l'observation** : Une correspondance est déterminée par les positions relatives de valeurs égales. (en milliers de dollars)
2. **Afficher clairement la formule de changement**; les recruteurs aiment voir les mathématiques modulaires.
3. **Complexité du comportement** début – cas le plus défavorable de O(n2) mais pratiquement rapide.
4. **Discussion de l'utilisation de la mémoire** – un tableau de taille `n` + carte de hachage.
5. **Optionnel:** Fournissez d'abord une version de force brute pour afficher le niveau de référence, puis améliorez.

---

À emporter

- **Problème résolu** en mappant chaque valeur à ses indices, puis en comptant le décalage qui aligne chaque paire.
- **La solution optimale** fonctionne confortablement dans les limites de LeetCode et les échelles bien.
- **Trois implémentations propres** (Java, Python, C++) prêtes pour la préparation d'entrevue ou le défi de codage.

Déployez ce code, lancez les exemples, et vous serez prêt à impressionner les recruteurs sur le code 3400 et les problèmes similaires de changement de tableau. Bon codage !

---

**Mots clés**: LeetCode 3400, indices de correspondance maximum, décalage droit, appariement de tableau, algorithme d'entretien, solution Java, solution Python, solution C++, entretien d'algorithme, entretien d'emploi, entretien de structure de données, arithmétique modulaire.