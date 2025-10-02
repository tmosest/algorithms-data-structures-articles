---
titre: LeetCode 969. Tri de crêpes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Tri de crêpes – LeetCode 969
**Objectif:** Trier un tableau en utilisant seulement -pancake flips.
**Retour :** La séquence des valeurs `k` (les longueurs de retournement) qui triera le tableau.
**Limiter:** Toute réponse valide qui utilise ≤ 10 × arr.longueur flips est acceptée.

Vous trouverez ci-dessous une solution propre et prête à la production dans **Java**, **Python** et **C++**.
Après le code, lisez un court article de blog SEO-friendly qui explique le problème, l'algorithme, les parties "good / bad / lid" et comment cette connaissance peut vous aider à coder des interviews et atterrir votre prochain travail.

---

- Oui. 1. Java – 1-Based K, O(n2) flips (=2 n‐1)

"Java
Importation de java.util.*;

solution de classe publique {
Liste publique<Integer> crêpesTort(int[] arr) {
Liste <integer> flips = nouvelle liste d'array<>();
int n = longueur de l'arrond;

// Nous trions du plus grand élément jusqu'à 1
pour (int currSize = n; currSize > 1; currSize--) {

Voir l'index du plus grand élément dans arr[0 ... currSize‐1]
dans maxIdx = 0;
pour (int i = 1; i < currSize; i++) {
si (arr[i] > arr[maxIdx]) maxIdx = i;
}

// Déjà au bon endroit ? → continuer
si (maxIdx) == currSize - 1) continuer;

// / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / / /
Si (maxidx != 0) {
flip(arr, maxIdx); // k = maxIdx + 1
flips.add(maxIdx + 1);
}

3/ Déplacez-le à sa position finale
flip(arr, currSize - 1); // k = currSize
flips.add(currSize);
}

flips de retour;
}

/** Inverse arr[0 ... k] inclusivement (k est basé sur 0). */
vide privé flip(int[] arr, int k) {
i = 0, j = k;
pendant que (i < j) {
int tmp = arr[i];
arr[i++] = arr[j];
arr[j--] = tmp;
}
}
}
«» "

> **Pourquoi 1-basé `k`?**
> LeetCode s'attend à ce que la taille flip (`k`) soit **1-basée**.
> L'aide `flip(arr, k)` utilise un index basé sur 0 en interne.

---

- Oui. 2. Python – propre et pythonique

'`python
Solution de classe:
def pancake Tri(self, arr: List[int]) -> Liste[int]:
flips = []
n = len(arr)

pour le curr dans la plage (n, 1, -1):
# indice de l'élément le plus important dans les premiers éléments 'curr'
max_idx = arr.index(max(arr[:curr]))

si max_idx == curr - 1: # déjà en place
poursuivre

# apporter l'élément max à l'avant
si max_idx != 0:
arr[:max_idx+1] = inversé(arr[:max_idx+1])
flips.append(max_idx + 1)

# l'amener à sa position finale
arr[:curr] = inversé(arr[:curr])
flips.append(curr)

retour flips
«» "

---

- Oui. 3. C++ – Flips STL & O(n2)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> crêpesTrier(vecteur<int>& arr) {
vecteur<int> flips;
int n = arr.size();

pour (int curr = n; curr > 1; --curr) {
// Trouvez l'indice de l'élément le plus important dans arr[0 ... curr-1]
int maxIdx = max_element(arr.begin(), arr.begin() + curr) - arr.begin();

Si (maxIdx == curr - 1) continuer; // déjà en place correcte

// Apporte-le à l'avant si ce n'est pas déjà
Si (maxidx != 0) {
inverse(arr.begin(), arr.begin() + maxIdx + 1);
flips.push_back(maxIdx + 1); // k est basé sur 1
}

// Dépliez-le à sa position finale
inverse(arr.begin(), arr.begin() + curr);
flips.push_back(curr);
}
flips de retour;
}
};
«» "

---

- Oui. 4. Article de blog – Le bon, le mauvais, et le mauvais de la crêpe trier

Titre
**Traitement du pancake : la façon la plus douce d'inventer le LeetCode 969 (et les intervieweurs d'impression)* *

### Méta-Description
Découvrez comment résoudre LeetCode 969 – Tri de crêpes – en Java, Python et C++. Comprendre l'algorithme, la complexité temporelle, les pièges, et pourquoi ce problème est un *must-know* pour votre prochaine entrevue d'ingénierie logicielle.

---

- Oui. 1. Présentation

Imaginez une pile de crêpes. Vous pouvez retourner le haut *k* crêpes et inverser leur ordre.
Dans l'informatique que l'on appelle un "pancake flip**".
Le problème : étant donné une permutation de 1...n, triez-le à l'aide de ces flips.
Pourquoi un recruteur s'en préoccupe ? Parce qu'il teste :

- **Manipulation d'images**
- **Stratégie relative au mariage**
- ** compromis espace/temps**
- **Attention au détail** (glissement du nombre correct d'éléments)

---

- Oui. 2. Déclaration de problème (Code de bord 969)

Paramètre Contraintes
C'est pas vrai.
1 ≤ n ≤ 100
1 ≤ arr[i] ≤ n, tous uniques (permutation)
Produit Toute liste de valeurs `k` qui trie le tableau, avec au plus `10 * n` flips

> **Note:** `k` est basé sur *1* (par exemple, `k = 4` retourne les 4 premiers éléments).

---

- Oui. 3. L'idée de l'avidité – La plus grande jusqu'à la fin

1. **Itérer de la fin au front. **
Pour `currSize = n ... 2`, l'élément qui devrait être en position `currSize‐1` est le *plus grand* parmi les premiers `currSize`.
2. ** Apportez cet élément au front** (si ce n'est déjà fait).
Dépliez le sous-réseau `[0 ... maxIdx]`.
`k = maxIdx + 1`.
3. **Déplacez-le jusqu'à sa dernière place** en renversant le sous-barrage `[0 ... currSize‐1]`.
`k = currSize`.

Pourquoi ça marche ?
Parce qu'après l'étape 2, le plus grand élément non trié est à l'index 0.
L'étape 3 inverse le préfixe `[0 ... currSize‐1]`, en déplaçant cet élément vers son indice final (`currSize‐1`) tout en conservant tous les éléments plus grands déjà placés.

**Fils maximaux:**
Au plus 2 flips par élément → '= 2n − 2 ' flips, confortablement en dessous de la limite `10n`.

---

- Oui. 4. Complexité algorithmique

Opération Temps Espace
- C'est quoi ?
Trouver "maxIdx" O(currSize) → O(n2) global
Révérends O(currSize) → O(n2)
Total **O(n2)** (n ≤ 100, trivial)

L'algorithme est *simple* mais *optimal* pour les contraintes d'entretien.

---

- Oui. 5. Faits saillants de la mise en œuvre

### Java
- Utilisez un helper `flip(int[] arr, int k)` qui inverse `arr[0 ... k]`.
- Sauter les flips de la taille 1 (ils ne font rien).
- Gardez une "Liste " pour la réponse.

Python
- Tirer parti de Python : "arr[:k] = inversé(arr[:k])".
- `list.index()` + `max()` dans la tranche donne `maxIdx`.
- Ajouter `maxIdx+1` et `currSize` au résultat.

C++
- Utiliser `reverse(debut, fin)` de `<algorithme>`.
- `max_element` trouve l'index du maximum dans le préfixe.

---

- Oui. 6. Bien, mal, Méchant

Les bons
- **Conceptuellement simple**: Plus grand → avant → arrière.
- **Déterministe**: Pas de retour ou de récursion.
- **LeetCode-ready**: suit le format de sortie exact et les limites.

- Oui. Les mauvais
- **O(n2)**: Pour `n=100` toujours trivial, mais pas optimal pour les données plus grandes.
- **Scans répétés**: Trouver le maximum de chaque itération peut être coûteux dans d'autres contextes.
- **Déchargement des frais généraux**: Dans les langues avec des copies de tranches coûteuses (p. ex., certaines variantes de Python), vous pouvez frapper des limites de mémoire sur des tableaux plus grands.

- Oui. L'Ugly
- **Pièges hors d'usage**: Rappelez-vous que `k` est basé sur 1 alors que les indices sont basés sur 0 en code.
- **Diviser le tableau comme une pile**: Si vous inversez le tableau *tout* au lieu du préfixe, l'algorithme se casse.
- **En supposant que l'entrée soit triée**: Beaucoup de candidats commencent par vérifier `if arr[currSize-1] == currSize`, mais oublier que `currSize` est la longueur *préfixe*, pas la valeur de l'élément.

---

- Oui. 7. Analogies du monde réel

- **Recommandement de la file d'attente d'emploi** dans une base de données où seules les opérations "bulk reverse" sont bon marché.
- **Tempiles d'annulation/refaire**: Les segments de basculement sont semblables à l'inversion d'un segment d'actions.
- **Réorganisation de la ligne de cache CPU**: Certaines optimisations de bas niveau utilisent le segment inverse pour minimiser le trafic de mémoire.

---

- Oui. 7. FAQ

C'est ce qu'il a dit.
-- -- -- -- -- --
*Peut-on réduire la complexité du temps à O(n log n) ?*= Oui, en maintenant une carte de position pour que vous puissiez trouver `maxIdx` dans O(1). Mais c'est inutile pour n ≤ 100. Autres
*Et si `arr` contient déjà 1 à la première position? L'algorithme fonctionne toujours : nous sautons le premier flip (`maxIdx == 0`). Autres
*Est-ce que l'ordre des flips compte? * Seule la séquence compte. L'algorithme produit une séquence *canonique*, mais n'importe quel correct passera. Autres
*Pouvons-nous utiliser une structure de données de pile? Vous pouvez, mais c'est exagéré – le tableau lui-même est la pile de pancake. Autres

---

- Oui. 8. Comment utiliser ces connaissances dans les entrevues

Compétence testée Pourquoi ça compte
C'est pas vrai.
**Le raisonnement de la grêle**Shows vous permet de transformer un optimum global en étapes locales. Autres
De nombreux problèmes d'entrevue impliquent « inverse », « rotation » ou « droits de rotation ». Autres
Les erreurs hors-par-un sont les 3 principaux bugs d'entrevue. Autres
**Les recrues aiment les candidats qui considèrent les entrées vides ou déjà triées. Autres

** Conseil professionnel :** Lorsque vous êtes demandé un problème qui *regarde* mais qui a une solution avide soignée, demandez à l'intervieweur s'il y a un algorithme optimal connu. Parfois une solution simple est tout ce qu'il faut.

---

- Oui. 9. Liste de contrôle des essais rapides

Objet
- Oui.
Autres [x] Poignées `k = 1` avec grâce. Autres
Autres [x] Produit ≤ 10 n flips. Autres
Autres [x] Fonctionne pour n = 1 (returne une liste vide). Autres
Autres [x] C'est inutile. Autres
Autres [x] Utilise seulement l'espace supplémentaire O(1) (en plus de la réponse). Autres

---

- Oui. 10. Conclusion

Le tri des crêpes est la vitrine *parfait* de l'interview pour la manipulation de tableau et la stratégie gourmande.
Il est assez court pour coder sous une limite de 30 minutes, mais assez profond pour qu'un recruteur puisse voir que vous comprenez :

- **Dessin de mariage**
- ** compromis de complexité**
- **Pièges linguistiques* *

Maîtrisez les trois implémentations ci-dessus, rappelez-vous le quirk off-by-one, et vous serez prêt à **conquer LeetCode 969** – et tout autre problème inverse de tableau qui suit.

Bonne chance, et que votre code soit toujours parfaitement retourné dans l'ordre! C'est ce qu'il a dit.

---

- Oui. Prêt à s'entraîner ?
- Clonez les extraits de code dans votre IDE.
- Faites les tests officiels de LeetCode.
- Paire-programme avec un ami pour expliquer l'avide étape par étape.

Bon codage !