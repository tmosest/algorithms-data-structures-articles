---
titre: LeetCode 3447. Attribuer des éléments aux groupes ayant des contraintes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Problème 3447 – Attribuer des éléments aux groupes ayant des contraintes
**Difficulté**: Moyenne **Tag**: Table en Hash, Diviseurs, Greedy

> **LeetCode**: <https://leetcode.com/problèmes/assigner-éléments-à-groupes-avec-contraints/>

On vous donne
* "groupes[i]" – la taille du groupe *i*-e.
* `éléments[j]` – l'élément *j*‐th.

Pour chaque groupe, nous devons choisir un élément qui satisfait :

Règle Description Autres
- C'est quoi ?
**Divisibilité** Les «groupes[i]» doivent être divisibles par les «éléments[j]». Autres
**Indice le plus petit**= Si plusieurs éléments fonctionnent, choisissez celui avec le plus petit indice `j`. Autres
**Pas de correspondance**= Si aucun élément ne satisfait à la règle, mettez `-1`. Autres

Un élément peut être réutilisé par de nombreux groupes.
Retourner un tableau `assigné` où `assigné[i]` est l'index de l'élément choisi pour le groupe `i` (ou `-1`).

> Exemple
> Groupes = [8,4,3,2,4], éléments = [4,2]
> `attribué = [0,0,-1,1,0] "

-----------------------------------------------------------------------------------

L'idée

La méthode de la force brute serait d'essayer chaque élément pour chaque groupe – `O(="groupes=" ×="éléments="), ce qui est beaucoup trop lent pour atteindre les éléments `105`.

- Oui. Observation clé
*Il suffit de savoir, pour chaque diviseur de la taille d'un groupe, si ce diviseur apparaît dans les éléments et, dans l'affirmative, son indice **le plus petit**. *

Donc le plan :

1. **Hash map** – stocker l'indice *le plus petit* pour chaque valeur unique dans les éléments.
`map[value] → index`

2. Pour chaque taille de groupe `g`
* énumérer tous les diviseurs `d` de `g` en ‘O( √g)` temps.
* Si `d` est dans la carte de hachage, gardez le plus petit index vu jusqu'à présent.
* la réponse est le plus petit indice, sinon `-1`.

Le travail total est de `="groupes[i]` qui est bien dans les limites (`= 3×107` ops pire cas).

-----------------------------------------------------------------------------------

Code

Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java, Python et C++**.
Chacun suit le même algorithme décrit ci-dessus.

### Java

"Java
Importation de java.util.*;

solution de classe publique {
int[] public assignerElements(int[] groupes, int[] éléments) {
// 1. valeur de l'élément de carte → plus petit indice
Carte<entier,entier> indexMap = nouveau HashMap<>();
pour (int i = 0; i < elements.longueur; i++) {
int val = éléments[i];
indexMap.putIfAbsent(val, i); // garder le premier indice (le plus petit)
}

int[] ans = nouveau int[groupes.longueur];

// 2. traiter chaque groupe
pour (int i = 0; i < groupes.longueur; i++) {
int g = groupes[i];
int mieux Idx = entier.MAX_VALUE;

// énumérer les diviseurs jusqu'à sqrt(g)
pour (int d = 1; d * d <= g; d++) {
Si (g % d != 0) poursuivre;

// Diviseur plus petit
Integer idx = indexMap.get(d);
si (idx != null) bestIdx = Math.min(bestIdx, idx);

// diviseur plus grand jumelé
int autre = g / d;
si (autre != d) {
idx = indexMap.get(autre);
si (idx != null) bestIdx = Math.min(bestIdx, idx);
}
}

ans[i] = (bestIdx == Integer.MAX_VALUE) ? -1 : bestIdx;
}
le retour des an;
}
}
«» "

**Complexité* *
*Temps*: "O(=groups) × √max(groups)"
*Espace*: "O(-)éléments"

-----------------------------------------------------------------------------------

Python

'`python
de taper l'importation Liste

Solution de classe:
def assignElements(self, groupes: Liste[int], éléments: Liste[int]) -> Liste[int]:
# 1. valeur de l'élément → plus petit indice
idx_map = {}
pour i, valeur dans l'énumération (éléments):
si val n'est pas dans idx_map: # conserver le premier indice (le plus petit)
idx_map[val] = i

ans = []

# 2. traiter chaque groupe
pour g en groupes:
meilleure = flotteur('inf')
d = 1
alors que d * d <= g:
si g % d] 0:
si d dans idx_map :
best = min(best, idx_map[d])
autres = g // d
Si autre != d et autres dans idx_map:
best = min(meilleur, idx_map[autre])
d += 1

ans.append(meilleur si meilleur != flotteur('inf') sinon -1)

retour et
«» "

**Complexité** – identique à la version Java.

-----------------------------------------------------------------------------------

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> assignElements(vecteur<int>&groupes, vectorielle<int>&éléments) {
unordered_map<int, int> idx; // valeur -> plus petit indice
pour (int i = 0; i < (int)elements.size(); ++i)
idx.emplace(éléments[i], i); // garder la première occurrence

vector<int> ans(groups.size(), -1);

pour (int i = 0; i < (int)groups.size(); ++i) {
int g = groupes[i];
int best = INT_MAX;

pour (int d = 1; d * d <= g; ++d) {
si (g % d) se poursuit;

auto it = idx.find(d);
si (it != idx.end()) est le meilleur = min(meilleur, it->seconde);

int autre = g / d;
si (autre != d) {
il = idx.find(autre);
si (it != idx.end()) est le meilleur = min(meilleur, it->seconde);
}
}
ans[i] = (meilleur == INT_MAX) ? -1 : meilleur;
}
le retour des an;
}
};
«» "

-----------------------------------------------------------------------------------

Essai

"""
# Python
Python - <<'PY'
de taper l'importation Liste
Solution de classe:
def assignElements(self, groupes: Liste[int], éléments: Liste[int]) -> Liste[int]:
# identique à la mise en œuvre ci-dessus
idx = {}
pour i, valeur dans l'énumération (éléments):
si la valeur n'est pas idx:
idx[val] = i
res = []
pour g en groupes:
meilleure = flotteur('inf')
d = 1
alors que d*d <= g:
si g % d] 0:
if d in idx: best = min(best, idx[d])
autres = g//d
if other != d and other in idx: best = min(meilleur, idx[autre])
d+=1
res.append(meilleur si meilleur != float('inf') sinon -1)
retour res

print(Solution().assignerÉléments([8,4,3,2,4],[4,2])
PY
«» "

Produit :

«» "
[0, 0, -1, 1, 0]
«» "

Le même test passera pour les versions Java et C++.

-----------------------------------------------------------------------------------

Cas de bord

Pourquoi ça compte ?
- - - - - - - - - - Non.
Dupliquer les valeurs dans les éléments Nous avons besoin de l'index **small** `putIfAbsent` / `si (pas dans la carte) map[value] = idx`
Taille du groupe = 1= Seul le diviseur est 1=1 La boucle du diviseur fonctionne toujours (`1*1 <= 1`)=
Autres Tous les éléments plus grands que la taille du groupe.

-----------------------------------------------------------------------------------

- Oui. Pourquoi cela compte pour les entrevues

* **Greedy + Math** – démontre que vous pouvez mélanger la théorie des nombres avec les structures de données.
* **Analyse de la complexité** – LeetCode juge le temps et la mémoire; montrant un lien clair `O( √n)` est un plus.
* **Lisibilité du code** – Des boucles propres et des méthodes d'aide courtes rendent votre solution facile à lire – un facteur clé dans de nombreuses entrevues de codage.

-----------------------------------------------------------------------------------

Autres optimisations

Si vous voulez un 'O(-)groups) + maxGroup' solution vous pouvez construire une carte *diviseur*:

Texte
pour chaque valeur v en éléments:
pour plusieurs m de v jusqu'à maxGroupe:
enregistrer le plus petit indice de v qui divise m
«» "

C'est essentiellement un tamis.
La complexité devient `=(maxGroup / v)` qui peut être moins cher lorsque les éléments sont grands mais est plus lourd lorsque les éléments sont petits.
La solution de dénombrement des facteurs présentée ci-dessus est généralement la plus simple et la plus rapide pour les contraintes données.

-----------------------------------------------------------------------------------

Article du blog – Le bon, le mauvais et le mauvais de LeetCode 3447

> ** Mots clés du référencement**:
> *Codage 3447*, *Assigner des éléments aux groupes*, *solution de Java*, *solution de Python*, *solution de C++*, *entrevue de codage*, *entrevue de SDE*, *conseils d'entrevue de technologie*, *algorithme de division*, *problème d'entrevue de tableau de bord*, *prép* d'entrevue de GAANG

---

- Oui. Le Bon: Pourquoi 3447 est une Masterclass dans l'interview

- **Logique pure + structures de données** – Pas de tours de magie; juste une approche avide propre qui vous montre comprendre les diviseurs et les cartes de hachage.
- **Contraintes claires** – Valeurs ≤ `105`, rendant pratique une énumération de diviseur de √n.
- **Éléments réutilisables** – Teste votre capacité à réfléchir aux contraintes du problème (un indice par groupe mais de nombreux groupes par élément).
- **Application dans le monde réel** – La même idée (indexage inverse + dénombrement du diviseur) apparaît dans des problèmes comme la valeur manquante la plus petite, la plus petite ou l'élément minimal dans Subarrays.

### Les mauvaises: La Piège TLE

De nombreux candidats tombent dans le piège classique O(n2) :

Texte
pour g en groupes:
pour e en éléments:
si g % e] 0:
réponse = premier e
pause
«» "

Cette approche naïve vous donne un verdict *Time‐Limit Exceded* même avec une taille d'entrée modeste `104`.
Comme l'environnement d'évaluation de LeetCodeS est strict, un seul TLE fait échouer toute la soumission.
L'astuce est d'éviter l' itération sur tous les éléments pour chaque groupe.

- Oui. L'Ugly: Code sur-optimisé, difficile à lire

Quelques-uns essaient d'être fantaisistes avec des astuces ou un tamis personnalisé.
Bien que techniquement rapides, ces solutions:

- **Lisibilité insuffisante** – Dur pour les intervieweurs de vérifier rapidement.
- **Utilisez plus de mémoire** – Construire un tamis complet jusqu'à "max(groups)" peut utiliser jusqu'à 105 entiers pour chaque élément.
- **Bogues subtiles** – Mélanger des boucles, des opérations modulo et des mises à jour de cartes dans un bloc dense entraîne souvent des erreurs hors-par-un.

** Ligne de bottom** : L'équilibre entre vitesse et clarté est la caractéristique d'une grande réponse à l'entrevue.

-----------------------------------------------------------------------------------

Résumé

Langue Complexité Take‐away
- C'est quoi ?
Utiliser `HashMap` + boucle de diviseur. Autres
**Python**=O(=groups===maxGroupe===== Compréhension de la liste + `dict===
**C++**="O(="groups="="maxGroup)="="unordered_map` + boucles rapides. Autres

Les trois extraits ci-dessus sont prêts à être collés dans l'éditeur LeetCode.
Exécutez-les contre les tests d'échantillon et vous verrez des résultats identiques.

-----------------------------------------------------------------------------------

### TL;DR

1. Conservez l'index *premier* (le plus petit) de chaque élément dans une carte de hachage.
2. Pour chaque taille de groupe, énumérez tous les diviseurs dans `O( √g)` et choisissez le plus petit index de la carte.
3. Complexité: < < O(=]groups[i] > > , L'espace: "O" éléments".

Pour plus de pratique, implémentez la variante *sieve* qui précalcule le plus petit indice pour chaque multiple. Il s'exécute dans `O(="éléments=" × maxGroupe / valeur)` et répond à chaque groupe dans le temps `O(1)`, mais utilise plus de mémoire.

Bon codage, et bonne chance tuant que **LeetCode 3447** dans votre prochaine interview FAANG!