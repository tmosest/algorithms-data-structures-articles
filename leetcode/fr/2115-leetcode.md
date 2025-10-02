---
titre: LeetCode 2115. Trouver toutes les recettes possibles de Fournitures Données -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Le problème est un problème classique *dependency graph*.
Chaque ingrédient ou recette peut être considéré comme un nœud.
Si une recette a besoin d'un ingrédient, nous tirons une flèche **de l'ingrédient à la recette**.

«» "
Carotte -> Soupe
sel -> Soupe
Soupe -> ragoût
«» "

Les seuls nœuds libres sont les fournitures données – nous pouvons penser à eux comme déjà préparé
ingrédients.
Une recette peut être cuite dès que **all** de ses bords entrants (ingrédients) sont disponibles.
Après une recette est cuite, il peut être utilisé comme un approvisionnement pour d'autres recettes.

C'est exactement ce qu'il y a de "topologique" (algorithme de Kahn) fait:
commencer avec tous les nœuds libres (fournissements), enlever plusieurs fois un noeud, et
diminuer le degré de ses voisins sortants.
Chaque fois qu'un voisin devient zéro, nous savons que tous ses ingrédients
sont maintenant disponibles – la recette peut être cuite.

L'algorithme fonctionne naturellement dans l'ordre dans lequel les conditions préalables sont remplies, qui
est tout le problème demande.



-----------------------------------------------------------------------------------

Algorithme
«» "
1. Construire deux cartes :
indegree[recette] = nombre d'ingrédients requis
graphe[ingrédient] = liste des recettes qui nécessitent cet ingrédient

2. Mettez toutes les réserves dans une file d'attente.
Gardez également un ensemble 'disponible' qui contient initialement toutes les fournitures.

3. Alors que la queue n'est pas vide
cur = file d'attente.pop()
// Si cur est une recette que nous venons de faire, elle est déjà disponible.
Pour chaque recette suivante qui dépend du cur
en degré[suivant]...
si indegré[suivant]] 0
// tous ses ingrédients sont disponibles
result.push_back(next)
file.push(next) // cette recette devient une nouvelle offre
disponible.insérer(suivant)

4. Le vecteur « résultat » contient maintenant toutes les recettes qui peuvent être cuites.
«» "

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie exactement l'ensemble des recettes qui peuvent être cuites.

---

Lemma 1
Lorsqu'une recette `r` est insérée dans la file d'attente (et donc dans le vecteur de résultat),
tous ses ingrédients requis sont disponibles à ce moment.

**Prof.**
`r` est inséré seulement lorsque son `indegré[r]` devient zéro.
"indegree[r]" est diminué seulement lorsque l'un de ses ingrédients requis (ou une recette qui
est supprimé de la file d'attente.
Ainsi, pour chaque ingrédient requis `x` de `r` il y avait un moment où `x` a été enlevé
de la file d'attente et `indegree[r]` a été décrémenté par un.
Puisque le degré final est zéro, chaque ingrédient requis a été retiré de la file d'attente.
exactement une fois, ce qui signifie qu'il était disponible lorsque `r` a été traité. *



Lemma 2
Si une recette `r` peut être cuite en utilisant les fournitures données, alors l'algorithme
insérez `r` dans la file d'attente.

**Prof.**
Nous utilisons l'induction sur la longueur de la dérivation la plus courte de `r`.

*Base:*
Si `r` utilise uniquement des fournitures originales, tous ses ingrédients sont initialement dans la file d'attente.
Lorsque l'algorithme traite la première de ces fournitures, il déprime
«indegré[r]» en conséquence.
Après que la dernière fourniture requise a été traitée, le «degré[r]» devient zéro et
"r" est inséré.

*Étape d'introduction:*
Supposons que toutes les recettes qui peuvent être cuites au plus `k` sont insérées.
Laissez `r` être une recette qui nécessite une recette `p` qui est elle-même cuisable en étapes `k`.
Par l'hypothèse d'induction, `p` sera inséré dans la file d'attente.
Lorsque `p` est traité, `indegre[r]` est décrémenté.
Tous les autres ingrédients requis de `r` sont soit des fournitures originales ou des recettes
cuissable au maximum `k`, ainsi inséré avant `r` est considéré.
Par conséquent, après transformation du dernier ingrédient de ce type, le «degré[r]» devient zéro
et `r` est inséré. *



Lemma 3
Aucune recette qui ne peut pas être cuite n'est jamais insérée dans la file d'attente.

**Prof.**
Une recette n'est insérée que lorsque son degré atteint zéro (Lemma 1).
Le degré zéro signifie que tous les ingrédients requis ont déjà été retirés de la file d'attente,
Ils sont disponibles.
Si une recette n'était pas cuisable, au moins un ingrédient requis n'est jamais disponible,
donc son degré ne peut jamais devenir zéro, et la recette n'est jamais insérée. *



C'est vrai. Théorème
Le vecteur de sortie `résultat` contient exactement toutes les recettes qui peuvent être cuites à partir du
des fournitures.

**Prof.**

*Sonneté* – chaque recette du "résultat" peut être cuite:
Par Lemma 1, chaque recette insérée a tous ses ingrédients disponibles, donc il est
Cuissible.

* Complètement* – chaque recette cuisable apparaît dans le « résultat » :
Par Lemma 2 chaque recette cuisable sera insérée dans la file d'attente, et
par construction, l'algorithme pousse chaque recette insérée dans "résultats". *



-----------------------------------------------------------------------------------

Analyse de complexité

Laissez

* `n` – nombre de recettes
* `m` – nombre total d'occurrences d'ingrédients (somme de toutes les longueurs de la liste des ingrédients)

La construction des deux cartes est `O(n + m)`.
Chaque retrait de l'ingrédient de la file d'attente déclenche un traitement à temps constant de tous les composants
bords sortants, qui touche tous les bords une fois – "O(m)".
Les opérations de queue elles-mêmes sont aussi `O(n + m)`.
Par conséquent, la durée totale de fonctionnement est `O(n + m)` et la consommation de mémoire est
«O(n + m)».



-----------------------------------------------------------------------------------

#### Mise en œuvre de la référence (C++)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> trouver toutes les recettes (vecteur<string> et recettes,
vecteur<vector<string>> et ingrédients,
vectorielle<chaîne>&approvisionnements) {
unordered_map<string, vector<string>> graphique; // ingrédient -> recettes qui en ont besoin
non ordonné_map<string, int> indegree; // recette -> nombre d'ingrédients manquants
unordered_set<string> disponible; // tous les ingrédients actuellement gratuits
vecteur <string> résultat;

// 1. Construire le graphique et la carte des degrés
pour (size_t i = 0; i < recettes.size(); ++i) {
const string& recette = recettes[i];
indegree[recette] = ingrédients[i].size();
pour (cost string & ing : ingrédients[i]) {
graphique[ing].push_back(recette);
}
}

// 2. Demander toutes les fournitures originales
file d'attente <string> q;
pour (côté chaîne & s : fournitures) {
si (disponible.insert(s).second) { // insérer une seule fois
q.push(s);
}
}

// 3. Algorithme de Kahn
pendant que (!q.vide()) {
Const string cur = q.front(); q.pop();

// Pour chaque recette qui dépend de 'cur', réduire son indegree
si (graph.find(cur) != graph.end() {
pour (cont string& nxt : graph[cur]) {
--indegré[nxt];
si (indegré[nxt]) 0) {
// tous les composants de 'nxt' sont maintenant disponibles
result.push_back(nxt);
(nxt);
q.push(nxt); // 'nxt' devient une nouvelle offre
}
}
}
}

le résultat du retour;
}
};
«» "

*Le code suit exactement l'algorithme;*
les commentaires à l'intérieur de la mise en œuvre reflètent les étapes décrites ci-dessus.

-----------------------------------------------------------------------------------

Autres mises en œuvre
Si vous préférez une solution basée sur la DFS ou l'approche BFS de force brute, ceux-ci sont également
disponible, mais la méthode basée sur Kahn est la plus efficace (temps linéaire) et est
exactement ce que le problème attend.