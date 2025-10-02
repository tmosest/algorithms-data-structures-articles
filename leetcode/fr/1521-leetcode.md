---
titre: LeetCode 1521. Trouver une valeur d'une fonction mystérieuse plus proche de la cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1521 – *Trouver une valeur d'une fonction mystérieuse plus proche de la cible*
> **Language-agnostique solution**
> **Blog** – Le bon, le mauvais et le mauvais (friendly, interview-ready)

---

Récapitulation des problèmes

Compte tenu d'un tableau entier `arr` et d'une cible `t`, nous devons choisir tout sous-réseau `[l, r]` (inclus) et évaluer

«» "
func(arr, l, r) = arr[l] & arr[l+1] & ... & arr[r] // bitwise ET
«» "

Retourner la valeur minimale possible de `=func(arr, l, r)–=t=.

Valeur des contraintes
C'est pas vrai.
1 ≤ longueur de l'arrondi ≤ 105
1 ≤ arr[i] ≤ 106
0 ≤ objectif ≤ 107

Le scan O(n2) naïf de tous les sous-arrachages est impossible pour les limites données.

---

## -Savoir de base – Bitwise ET est monotone

Pour un index de départ fixe `l`, l'extension de la sous-banque vers la droite peut ** seulement transformer 1-bits en 0-bits**.
Par conséquent, l'ensemble de valeurs ET possibles pour les sous-réseaux se terminant à un indice particulier est *shrinking*.

Cette propriété nous permet de conserver, pour chaque indice, le *distinct* ET les résultats de tous les sous-réseaux qui se terminent à cet indice.
Comme chaque nouvelle opération ET peut tout au plus conserver la même valeur ou la réduire, le nombre de résultats distincts est limité par `O(log(max(arr))` (=20 pour 106).
Nous pouvons donc traiter le tableau en temps linéaire.

---

Algorithme (Set-Based O(n log k) Solution)

«» "
ans =
prev = {} // ET valeurs pour les sous-groupes se terminant à l'index précédent

pour num in arr:
curr = {num} // sub-array composé uniquement de num
ans = min(ans,..num - cible)

pour la valeur en prév:
nouveaux Val = valeur et nombre
(nouvelle Val)
as = min(ans,=nouvelVal - cible=)

prev = curr
retour et
«» "

- Oui. Pourquoi ça marche

* `prev` contient **tous les résultats distincts** ET les résultats des sous-groupes qui se terminent à l'élément précédent.
* Pour l'élément `num` actuel, chaque sous-poste se terminant ici est soit:
* juste "num" lui-même,
* ou une sous-entente antérieure prolongée par «num» (val & num).
* Parce que ET est monotone, la fusion de résultats identiques garde `curr` petit.
* La différence minimale globale `ans` est mise à jour chaque fois que nous générons une valeur candidate.

Complexité

Temps Espace
C'est le cas.
Nombre de bits, ≤ 20)

Avec `n = 105`, cela s'inscrit facilement dans les limites.

---

Mise en œuvre du code

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe {
Int public le plus procheToTarget(int[] arr, int cible) {
int ans = entier. MAX_VALEUR;
Définir <integer> prev = nouveau HashSet<>();

pour (int num : arr) {
Définir <integer> curr = nouveau HashSet<>();
le nom de l'autorité compétente;
ans = Math.min(ans, Math.abs(num - cible));

pour (int val : prev) {
int newVal = val & num;
curr.add(newVal);
ans = Math.min(ans, Math.abs(newVal - cible));
}
prev = curr;
}
le retour des an;
}
}
«» "

> **Pourquoi HashSet? * *
> Il garantit O(1) insert & lookup. Étant donné que la taille de l'ensemble est minuscule (20), les frais généraux sont négligeables.

---

# # # # # #

'`python
Solution de classe:
def le plus proche ToTarget(self, arr: List[int], cible: int) -> Int:
ans = flotteur('inf')
prev = set()

pour num in arr:
pourr = {num}
ans = min(ans, abs(num - cible))

pour la valeur en prév:
new_val = val & num
curr.add(new_val)
ans = min(ans, abs(new_val - cible))

prev = curr

retour et
«» "

> ** Touches pyroniques* *
> - Les compréhensions `set` sont rapides pour les petits ensembles.
> - `float('inf')` est une valeur initiale propre.

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int le plus procheToTarget(vecteur<int>& arr, cible int) {
int ans = INT_MAX;
non ordonné_set<int> prev;

pour (int num : arr) {
_set non ordonné<int> curr;
crr.insert(num);
ans = min(ans, abs(num - cible));

pour (int val : prev) {
int newVal = val & num;
curr.insert(newVal);
ans = min(ans, abs(newVal - cible));
}
prev = mouvement(curr); // mémoire de réutilisation
}
le retour des an;
}
};
«» "

> **Déplacer la sémantique**
> `move(curr)` évite de copier le petit jeu, en gardant la routine rapide.

---

Article du blog – Le bon, le mauvais et le mauvais

> **Titre**: *Code à gauche 1521 – Maîtriser la fonction mystérieuse avec la manipulation bit*
> **Meta‐Description**: Résoudre le LeetCode 1521 en O(n log k) en utilisant AND. Java, Python, codes C++ + aperçus prêts à l'entrevue.
> **Mots clés**: LeetCode 1521, le plus proche de la cible, manipulation de bits, subarray ET, algorithme d'entretien, solution O(n log k), codage d'entretien d'emploi, Python, Java, C++.

---

C'est pas vrai. Le Bon – Pourquoi Cette approche Rocks

1. **Temps linéaire** – Poigne 105 éléments confortablement.
2. **Space-Efficace** – Seulement quelques valeurs par indice.
3. ** Élégance conceptuelle** – Utilise la propriété monotonique de ET; aucune structure de données lourde.
4. **Cross‐Language** – Facile à traduire entre Java, Python et C++.
5. **Interview Friendly** – Démontre la compréhension des opérations bitwise, de la programmation dynamique et de l'optimisation.

---

C'est vrai. Les mauvaises – les cas de bord et les pièges

Numéro
C'est quoi ?
**Grands nombres** – Débordement de 32 bits dans des langues comme C++ si vous utilisez des ints signés. Autres
**Empty Array** – Problème garantit au moins un élément, mais le codage défensif aide. → retourner `cible`. Autres
**Précision en abs** – Dans Java `Math.abs(entier. _VALEUR MINIÈRE)» Utiliser `Math.abs(long)val - cible)` ou `Math.abs(long)val - (long)target)`. Autres
**La grande "cible"** – > 231 peut déborder dans "int" abs Utilisez `long` pour calculer la différence. Autres

---

C'est vrai. L'horrible – Quand le jeu simple fait défaut

Si `arr` contient tous ceux (p. ex., 1 000 000 répétés), chaque sous-barrage ET reste le même.
La taille de l'ensemble reste 1, ce qui est bien.
Mais si les nombres sont très variés, l'ensemble intermédiaire peut se développer momentanément (toujours ≤ log k).
Dans le pire des cas, les données obtenues, `prev` peuvent s'approcher `log2(106) 20`, toujours trivial.

**Et si on vous obligeait à utiliser un arbre segmentaire? * *
- Complexité: O(n log n log max)
- Mémoire: O(n)
- Frais généraux de mise en œuvre : plus difficile à expliquer dans une entrevue.
La méthode définie est préférable pour les scénarios d'entrevue.

---

####=4==EO–Traitements optimisés

- **Mots clés**: solution LeetCode 1521, plus proche de l'algorithme cible, bitwise ET subarray, problème de codage d'entretien, approche O(n log k), code Java/Python/C++, entretien de manipulation de bits.
- **Readability**: Utilisez des rubriques claires (`The Good`, `The Bad`, `The Ugly`) et des points de balle pour la numérisation rapide.
- **CTA**: Invitez les lecteurs à essayer le code sur LeetCode, à vous abonner pour plus de préparation d'entrevue, ou à vous contacter pour une séance d'entretien technique.

---

Liste de contrôle finale pour votre portefeuille

Objet
- Oui.
Solution Java dans une classe `Solution` avec méthode `plus proche Cible. Autres
Fonction Python avec conseils de type. Autres
Implémentation C++ en utilisant un_set non commandé. Autres
Blog article couvrant algorithme, complexité, cas de bord, référencement. Autres
Lien vers le problème LeetCode et discussion de solution. Autres
Lien du dépôt GitHub (facultatif). Autres

---

Enveloppe

Vous disposez désormais d'une solution de qualité de production prête à l'interview pour LeetCode 1521 en trois langues populaires. Le billet de blog présente non seulement votre profondeur technique, mais aussi vos positions pour des rôles d'ingénierie logicielle de haut niveau. Bon codage !