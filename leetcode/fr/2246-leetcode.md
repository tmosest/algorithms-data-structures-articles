---
titre: LeetCode 2246. Le chemin le plus long avec différents caractères adjacents - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2246 – Chemin le plus long avec différents caractères adjacents
*(LeetCode Hard)*

> **Objectif** – Dans un arbre enraciné où chaque noeud a une lettre minuscule, trouvez la longueur maximale d'un chemin simple de telle sorte que **aucun noeud adjacent ne partage le même caractère**.
> **Input** – `int[] parent` (taille `n`) et `String s` (longueur `n`).
> ** Sortie** – Longueur du chemin le plus long valide (1-basé).

Ci-dessous vous trouverez une solution complète, prête à coller dans **Java, Python, et C++** (tout l'espace O(n) time / O(n).
Après cela, lisez le blog d'accompagnement qui explique l'intuition, les pièges, et comment cette solution brille dans une entrevue de codage.

---

Code

### Java

"Java
Importation de java.util.*;

solution de classe {
int privé meilleur; // la longueur maximale globale

public int le plus longPath(int[] parent, Chaîne s) {
int n = longueur parent;
Liste <entier>[] enfants = nouvelle liste de répartition;
pour (int i = 0; i < n; i++) les enfants[i] = nouvelle liste de distribution<>();

pour (int i = 1; i < n; i++) { // build adjacency list
les enfants [parent[i]].add(i);
}

= 1; // au moins un noeud
dfs(0, enfants, s);
le meilleur retour;
}

/** retourne la chaîne la plus longue commençant par le nœud `v` qui satisfait à la règle */
int privé dfs(int v, Liste<integer>[] enfants, chaîne s) {
int first = 0, second = 0; // deux longueurs supérieures chez les enfants

pour (int u : enfants[v]) {
int len = dfs(u, enfants, s); // chaîne la plus longue de l'enfant u
si (s.charAt(u) == s.charAt(v)) continue; // ne peut pas utiliser cet enfant

si (len > premier) {
seconde = première;
première = len;
} sinon si (len > seconde) {
seconde = len;
}
}

best = Math.max(meilleur, premier + deuxième + 1); // chemin passe par v
retour premier + 1; // chaîne la plus longue vers le haut
}
}
«» "

---

Python 3

'`python
de taper l'importation Liste
de collections importer par défautdict
importation heapq

Solution de classe:
def leastPath(self, parent: List[int], s: str) -> Int:
n = len(parent)
enfants = [[] pour _ dans l'intervalle(n)]
pour i dans la plage (1, n):
enfants[parent[i]].appendice(i)

auto.meilleur = 1

def dfs(v: int) -> Int:
top_two = [0, 0] # plus grandes deux longueurs d'enfants

pour u chez les enfants[v]:
cur = dfs(u)
Si s[u] == s[v]:
poursuivre
# Gardez les deux plus grandes valeurs
si cur > top_two[0]:
haut_deux[1] = haut_deux[0]
haut_deux[0] = cur
elif cur > top_two[1]:
haut_deux[1] = cur

Self.best = max(self.best, top_two[0] + top_two[1] + 1)
retour top_two[0] + 1

dfs(0)
Revenez vous-même. le meilleur
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int le plus longPath(vector<int>& parent, chaîne s) {
int n = parent.size();
vecteur<vecteur<int>> enfants(n);
pour les enfants [parent[i]].push_back(i);

meilleure = 1;
dfs(0, enfants, s);
le meilleur retour;
}

particulier:
int mieux;

int dfs(int v, vecteur<vector<int>>& enfants, const string & s) {
int first = 0, second = 0; // deux longueurs supérieures chez les enfants

pour (int u : enfants[v]) {
int len = dfs(u, enfants, s);
si (s[u] == s[v]) continuer;

si (len > premier) {
seconde = première;
première = len;
} sinon si (len > seconde) {
seconde = len;
}
}

best = max (meilleur, premier + deuxième + 1);
retour en premier + 1;
}
};
«» "

---

Article de blog – *Le bon, le mauvais, et le mauvais de DFS sur les arbres*

> **Mots clés**: LeetCode 2246, Chemin le plus long avec différents caractères adjacents, DFS, arbre DP, codage d'entrevue, conception d'algorithme, cas de bord.

- Oui. 1. Présentation

Quand un recruteur vous met à la main **LeetCode 2246 – Le chemin le plus long avec différents personnages adjacents**, vous regardez un arbre classique‐ Problème DP. Le défi n'est pas seulement de trouver le chemin le plus long ; il est de le faire tout en obéissant à une règle de compatibilité de caractère.
Une recherche en profondeur (DFS) propre et récursive qui suit les deux meilleures chaînes de chaque enfant est la solution la plus élégante et la plus conviviale pour les interviews.

---

- Oui. 2. Rétablissement des problèmes

Étant donné un arbre enraciné avec des nœuds `n` (`0 ≤ n ≤ 105`), où chaque noeud `i` a une lettre `s[i]`, calculer la longueur du chemin simple le plus long (aucun nœud ne répète) de sorte que **chaque paire de nœuds consécutifs sur le chemin a des lettres différentes**.
Parce que `n` est grand, nous avons besoin d'un algorithme **O(n)**.

---

- Oui. 3. L'intuition – Pourquoi deux chaînes?

Pensez à un chemin qui traverse un nœud "v" et des branches en deux sous-arbres différents.
Si nous connaissons déjà la chaîne la plus longue à partir de chaque enfant qui se termine à cet enfant, nous pouvons

1. **Utilisez l'enfant seulement si sa lettre diffère de "v".**
2. ** Gardez les deux plus longues chaînes utilisables. **
3. **Ajouter 1 pour le noeud `v` lui-même** pour obtenir la longueur du chemin du candidat.

La réponse globale est le maximum de tous ces candidats. Il s'agit d'un calcul *post-commande*: les enfants sont traités avant leur parent.

---

- Oui. 3. Pourquoi le DFS + le "top-two" est le bon choix

Raison de détail
C'est quoi ?
Une fonction récursive, pas de structures de données fantaisistes. Autres
**Predictable Runtime**= Chaque noeud visité une fois → **O(n)**. Autres
**Memory Friendly**= Liste d'adjacence + pile de récursion → **O(n)** pire-cas. Autres
**Interview–Ready**= Explique clairement la transition d'état, facile à déboguer sur place. Autres
**Évoluabilité** Autres

La principale perspicacité est qu'un chemin valide **ne revisite jamais un nœud**, donc nous n'avons qu'à considérer *enfant → parent → autre enfant* modèles. Le suivi de deux chaînes maximales suffit parce qu'un chemin peut avoir au plus deux branches à un nœud.

---

- Oui. 3. Les mauvaises – pièges communs

1. **Ignorer la condition racine**
Certaines implémentations oublient que la racine peut être une feuille et retourner 0 au lieu de 1. Toujours initialiser le meilleur à 1 (un seul nœud).

2. **Mixation de la longueur du chemin par rapport au nombre de nœuds* *
Dans DFS, la valeur de retour représente la plus longue *chaîne* qui peut être étendue vers le haut. N'oubliez pas d'ajouter 1 pour le noeud courant lors du retour.

3. **O(n2) Erreur avec l'appariement naïf* *
L'association de chaque enfant avec chaque autre enfant ('O(k2)' par nœud) souffle rapidement sur un arbre en forme d'étoile. L'astuce « Garder deux plus gros » maintient la complexité linéaire.

4. **Dépassement de la prise en charge à la récursion**
Avec `n = 105`, la récursion profonde peut atteindre la limite de la pile dans certaines langues. En Java ou en C++, vous devrez peut-être augmenter la limite de récursion ou utiliser une pile itérative. Les solutions Python 3 passent généralement parce que la limite de récursion par défaut de CPython est plus élevée; sinon, utilisez `sys.setrecursionlimit`.

---

- Oui. 4. Les cas d'indignation – bord qui écrasent votre code

Ce qui se passe si vous le manquez
- C'est quoi ?
**Tous les nœuds La même lettre**La longueur du chemin est toujours 1. Si vous oubliez de mettre à jour `meilleur = 1` au début, vous pouvez retourner Initialiser `meilleur = 1`. Autres
**Grand arbre étoilé**= O(n2) si vous jumelez naïvement des enfants.= Gardez seulement les deux plus grandes chaînes utilisables. Autres
Autres **Arbre de nœuds simples**. Certains codes récursifs peuvent renvoyer 0 pour les nœuds foliaires. Retourner 1 pour une feuille (une chaîne de longueur 1). Autres
**Liste d'enfants vide**="enfants[v]" peut être vide; la boucle doit la gérer avec grâce. Utilisez une liste vide, aucun cas particulier nécessaire. Autres
**L'entrée non-rootée**LeetCode garantit `parent[0]== 0`. Si vous supposez incorrectement un arbre non dirigé, vous aurez un double comptage. Construire une liste d'adjacence dirigée de la racine aux enfants. Autres

---

- Oui. 5. Étape par étape

Laissez passer un petit exemple:

«» "
parent = [0, 0, 1, 1, 2,]
s = "abacbd"
«» "

1. Créer une liste d'adjacence :
`0 → {1, 2}`
`1 → {3, 4}`
`2 → {5}`

2. DFS(0):
* enfant 1 retour chaîne `2` (b → a → c)
* enfant 2 retourne la chaîne `1` c) mais `s[2]==s[0]`? Non → utilisable.
* `premier=2`, `deuxième=1` → meilleur candidat `2+1+1 = 4`.

3. La récursion renvoie `first+1 = 3` au nœud 0.
4. Le meilleur = 4. Chemin: `b → a → c → d`.

Toutes les opérations sont "O(1)" par enfant; globalement "O(n)".

---

- Oui. 6. Analyse de la complexité

Langue Heure Espace
- C'est quoi ?
Java **O(n)****O(n)** (liste des dépendances + pile de récursion)
Python **O(n)**
* * * * * * * *

Le seul facteur supplémentaire constant est le coût de la comparaison des caractères et de la mise à jour de deux maximums – négligeable.

---

- Oui. 7. Variations et extensions

Comment s'adapter
C'est quoi ?
**Plusieurs lettres autorisées** Autres
**Return le poids de la chaîne plutôt que le nombre de nœuds. Autres
**Arbre non rodé**=Enraciner l'arbre arbitrairement (par exemple, noeud 0) – l'algorithme est agnostique à la racine parce que la règle ne concerne que les noeuds adjacents. Autres

---

- Oui. 8. Stratégie d ' essai

Autres Essai Description
- C'est quoi ?
Un seul noeud → réponse = 1.
Autres Toutes les mêmes lettres
Autres Lettres alternantes (p.ex., ABABA)
Autres Arbre d'étoiles avec un enfant différent
Un grand arbre aléatoire (105 nœuds)

Utilisez les tests unitaires LeetCode, ainsi que vos propres générateurs aléatoires pour tester le stress.

---

- Oui. 9. Conclusion

LeetCode 2246 est un problème DP** de l'arbre **pure-DFS qui récompense une pensée claire et une solution linéaire minimale.
Le motif de maintien des deux chaînes supérieures est un motif réutilisable pour de nombreuses questions d'entrevue sur les chemins les plus longs, les subséquences les plus longues en augmentation dans les arbres, ou les problèmes maximum indépendants.

> *À emporter*: Toujours **penser bas vers le haut**. En résumant chaque contribution de l'enfant dans une petite paire d'entiers, vous pouvez résoudre tout le problème en un seul passage.

---

10 ans. Pensée finale

Si vous préparez un entretien technique, pratiquez ce modèle exact jusqu'à ce que vous puissiez l'écrire sans regarder une référence. La maîtrise de DFS sur les arbres ouvre la porte à de nombreux problèmes de LeetCode dur et impressionne les gestionnaires d'embauche qui apprécient les algorithmes propres et efficaces.

---

Bon codage ! C'est ce qu'il a dit