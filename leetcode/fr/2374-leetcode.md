---
titre: LeetCode 2374. Noeud avec le plus haut score de bord -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2374 – Noeud avec le meilleur score de bord
**Un problème de LeetCode, résolu en Java, Python, & C++ + un billet de blog SEO complet* *

---

TL;DR
- **Objectif:** Trouvez le nœud qui reçoit le plus grand score *edge* (somme des étiquettes de nœud entrantes).
- **Input:** `int[] bords` où `edges[i]` est la destination du seul bord sortant du nœud `i`.
- **Output:** Indice du noeud avec le score le plus élevé (indice le plus petit si lié).
- **Complexité:** "O(n)" temps, "O(n)" espace supplémentaire.
- **Pourquoi c'est important :** Démontre le comptage graphique, la sécurité 64 bits et des solutions d'un seul passage propres, de grands points d'entrevue pour un rôle de backend/data-engineering.

---

Récapitulation des problèmes

> **Nœud avec le plus haut score de bord* *
> On vous donne un graphique dirigé avec des nœuds `n` (`0 ... n-1`).
> Chaque noeud a exactement un bord sortant, donné par le tableau "edges".
> Le score *edge* du nœud `i` est la somme des étiquettes de tous les nœuds qui pointent vers `i`.
> Retourner le noeud avec le score le plus élevé du bord; si plusieurs nœuds se lient, retourner le plus petit index.

Exemple

Texte
bords = [1,0,0,0,0,7,5]
Produit : 7
«» "

- Node 0 reçoit des bords de 1,2,3,4 → score = 1+2+3+4 = 10
- Node 5 reçoit le bord de 7 → score = 7
- Le nœud 7 reçoit des bords de 5,6 → score = 5+6 = 11 (max)

---

## Solution de haut niveau

1. **Traverser une fois** au-dessus de "edges".
2. Pour chaque `i`, ajouter `i` au score du noeud `edges[i]`.
3. Tenir une trace du score maximal et de son indice de nœuds pendant la mise à jour.
4. Retournez le nœud avec le score le plus élevé (tie → index plus petit).

Étant donné que la somme des indices peut atteindre ~`n*(n-1)/2` (5 × 109 pour `n = 105`), utiliser **64‐bit entiers** (`long` in Java & C++, `int64`/`long` in Python) pour éviter les débordements.

---

Solutions de code

### Java

"Java
// 2374. Noeud avec le plus haut score de bord
// Java 17 – Solution monopass O(n)

solution de classe publique {
edge int publicScore(int[] edges) {
int n = bords.longueur;
long[] score = nouveau long[n]; // 64‐bit pour éviter le débordement
int bestNode = 0;
long bestScore = 0;

pour (int i = 0; i < n; i++) {
int à = bords[i];
score[to] += i; // ajouter l'étiquette de nœud entrant

si (score[to] > bestScore
(score[to] == bestScore && à < bestNode)) {
bestScore = score[à];
bestNode = à;
}
}
le meilleur retour Numéro;
}
}
«» "

> **Traitement des clés:**
> *Utilisez un tableau brut au lieu d'un `HashMap` pour les recherches O(1); gardez un meilleur fonctionnement pour éviter une seconde analyse. *

---

Python

'`python
# 2374. Noeud avec le plus haut score de bord
# Python 3 – Solution monopass O(n)

def edgeScore(edges):
n = len(edges)
score = [0] * n # liste des ints, 64 bits sur CPython
best_node = 0
best_score = 0

pour i, à énumérer:
score[à] += Les
si score[to] > best_score ou (score[to]) best_score et < best_node) :
best_score = score[à]
best_node = à

_noeud de retour
«» "

> **Pourquoi lister au-dessus de `defaultdict`:**
> L'espace d'index est déjà connu (`0 ... n-1`), donc une liste donne l'accès O(1) et pas de hachage au-dessus.

---

C++

'`cpp
// 2374. Noeud avec le plus haut score de bord
// C++17 – Solution monopass O(n)

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int edgeScore(vecteur<int>& bords) {
int n = bords.dimension();
Vecteur <long> score(n, 0); // 64-bit
int bestNode = 0;
long long bestScore = 0;

pour (int i = 0; i < n; ++i) {
int à = bords[i];
score[à] += i);
si (score[to] > bestScore=" (score[to] == bestScore && to < bestNode)) {
bestScore = score[à];
bestNode = à;
}
}
le meilleur retour Numéro;
}
};
«» "

> **À emporter:**
> Utilisez `long long` pour la sécurité; le reste est identique à Java/Python.

---

Analyse de complexité

L'approche du temps L'espace Pourquoi ça compte
-- -- -- -- -- -- -- -- -- -- -- -- --
* Chaque bord traité une fois; la taille du tableau de score = `n`.
Deux passes (premiers scores de calcul, deuxièmes maxis de recherche) Autres
HashMap (Java) / unordered_map (C++) Autres

Toutes les solutions fonctionnent confortablement dans les limites de LeetCode.

---

Ce qui fait ce problème

1. **Graphiques fondamentaux** – Dénombrement des degrés, traversée des bords.
2. **Manipulation des caisses** – débordement de 64 bits, liens par index.
3. **Optimalité d'un passage** – Montrez que vous pouvez concevoir des algorithmes linéaires.
4. **Modèles d'agnostiques linguistiques** – Le même algorithme fonctionne en Java, Python, C++, Allez, etc.

---

Les pièges communs

Piège Explication
- C'est quoi ?
Utiliser `int` pour les scores?La somme peut dépasser `2^31‐1`. Autres
Re-scanning pour le maximum après la construction du tableau de scores. Continuer à courir max pendant la construction. Autres
Utiliser un `HashMap` pour une gamme d'indices denses. Utilisez un tableau simple (`int[]`, `long[]`). Autres
Ne pas manipuler les liens. Comparer `à < bestNode` quand les scores sont égaux. Autres

---

Analogies du monde réel

- ** Serveurs d'équilibrage de charge** – Les nœuds représentent les serveurs ; chaque requête (bord entrant) contribue à la charge *request ID* (index).
- **Réseau social** – Le score d'Edge est comme le *somme des ID de suivi* pointant vers un utilisateur.

Ces analogies aident les recruteurs à voir votre état d'esprit de résolution de problèmes au-delà du codage.

---

Le bon, le mauvais, et le mauvais
> *SEO-Optimized: Leetcode noeud avec le plus haut score de bord, -graph indegree, -

---

# Noeud avec le plus haut score de bord – une plongée profonde
### Pourquoi c'est un LeetCode Gem & Comment le faire dans votre prochaine interview

**Mots clés:**
`leetcode`, `node avec le plus haut score de bord`, `graph`, `indegree`, `one-pass`, `Java solution`, `Python solution`, `C++ solution`, `interview d'emploi`, `interview d'arrière-plan`, `algorithm interview`, `array vs hashmap`, `64-bit de trop`, `programmation compétitive "

---

C'est pas vrai. Quel est le problème?

LeetCode 2374 vous défie de travailler sur un graphe **orienté** où chaque noeud a ** exactement un bord sortant**.
Le twist : vous n'êtes pas à la recherche du *reach* d'un noeud mais de son **edge score** – la somme des indices de tous les nœuds qui le pointent.
Si deux nœuds ont le même score, vous retournez celui avec le plus petit index.

---

- Oui. Le bien – Pourquoi Ce problème est une masterclass

Pourquoi il est bon
C'est quoi ?
**Graphique classique en comptage des degrés**= Renforce les fondamentaux qui sont utilisés pour le routage, l'analyse des graphiques sociaux et les passes du compilateur. Autres
**La solution linéaire du temps**Shows vous permet de concevoir des algorithmes optimaux – un trait d'entrevue clé. Autres
**Sensibilisation à l'écoulement** , vous force à considérer les limites numériques – un détail subtil mais essentiel de la production. Autres
**L'élégance d'un passage**Démontre que vous pouvez combiner l'accumulation de données et l'extraction de résultats en une seule boucle. Autres
**Language-agnostique**Le même algorithme fonctionne en Java, Python, C++, Go, Rust – idéal pour les recruteurs techniques qui apprécient les compétences multiplateformes. Autres

---

C'est vrai. Les choses qui rendent le problème plus dur qu'il ne semble

1. ** Grande taille d'entrée (`n ≤ 100 000`)* *
- Vous devez garder la solution linéaire ; les hacks O(n2) seront time‐out.
2. **Dépassement des notes**
- La somme des indices peut atteindre 5 × 109 – nécessite 64-bit arithmétique.
3. ** Règle portant atteinte aux droits**
- L'index le plus petit si attaché peut remonter la logique naïve de recherche max.

---

C'est pas vrai. Les erreurs courantes et comment les éviter

Pourquoi ça arrive ?
-- -- -- -- -- -- -- --
En utilisant `int` pour les scores. Autres
Autres Recalculer le max dans une seconde boucle. Autres
Utiliser un tableau HashMap/HashTable Ajouter des frais généraux de hachage inutiles lorsque les indices sont contigus Utiliser un tableau brut (`int[]`, `long[]`). Autres
Autres Ignorer la règle de l'égalité. Autres

---

####5=1 Étape par étape (Java)

"Java
int bestNode = 0; // candidat à la réponse
long bestScore = 0; // score maximal actuel

pour (int i = 0; i < n; i++) {
int à = bords[i];
score[à] += i; // accumuler l'étiquette entrante

// Mettre à jour le mieux si nous avons trouvé un score plus élevé ou le même score mais un indice plus petit
si (score[to] > bestScore=" (score[to] == bestScore && to < bestNode)) {
bestScore = score[à];
bestNode = à;
}
}
le meilleur retour Numéro;
«» "

> **Pourquoi `score[to] += i`?**
> `i` est l'étiquette du nœud entrant. L'ajouter directement au score du nœud de destination implémente la définition de *edge score* en O(1).

---

- Oui. Analogies du monde réel (à utiliser dans votre entrevue)

- **Load Balancer** – Serveurs = nœuds, requêtes = bords. Chaque requête contribue son ID à un serveur ..
- **Médias sociaux** – Utilisateurs = nœuds, - Suivre les relations = bords. Le *score* est comme la popularité de l'influenceur.

Ces analogies aident les recruteurs à relier l'algorithme aux problèmes commerciaux.

---

### # 7- Loin

- **Problème :** Calculer les scores basés sur le degré dans un graphique avec un bord sortant par noeud.
- **Solution:** Un passage linéaire avec un tableau de notes 64 bits + un maximum d'exécution.
- **Pourquoi les recruteurs l'adorent :**
1. Bases graphiques + manipulation de cas de bord.
2. Démontre l'attention portée aux limites numériques.
3. Montre la maîtrise des structures de données linguistiques-agnostiques.

> ** Conseil professionnel :** Il s'agit d'une façon rapide de présenter la pensée algorithmique et la sensibilisation à la production.

---

Les pensées de clôture – Comment présenter Ceci dans un portefeuille

- **Les extraits de code** (Java, Python, C++) sur GitHub avec commentaires.
- **Blog post** qui explique le problème, la solution, les pièges et les prises d'entrevue.
- **Lié Dans post** qui fait référence à la solution LeetCode et tags recruteurs avec des mots clés: *Graph, Indegree, LeetCode 2374, Algorithm, Job Interview, Backend Engineer, Data Engineer*.

L'ajout de ce problème à votre portefeuille démontre :

1. **Compétence algorithmique** – traitement linéaire des graphiques.
2. **L'état d'esprit de la production** – Sécurité 64 bits, logique de rupture.
3. ** Compétences en communication** – explications claires et concises (le billet de blog lui-même).

Les trois langues fournissent une logique identique, ce qui facilite l'échange de code entre les piles tech lors des entretiens.

Bon codage – et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit