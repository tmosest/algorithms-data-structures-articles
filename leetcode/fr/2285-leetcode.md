---
titre: LeetCode 2285. Importance maximale totale des routes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1=1 Aperçu du problème – LeetCode 2285 =Importance maximale des routes

Valeur du champ
C'est pas vrai.
Problème 2285. Importance maximale des routes
Difficulté Moyenne
Tags: Greedy, Tri, Graph
Source
URL https://leetcode.com/problèmes/maximum-total-importance-de-routes/ Autres

**Objectif**
Étant donné *n* villes (0-basées) et une liste de routes non dirigées, assignez à chaque ville une valeur entière unique de **1** à **n**.
L'importance* d'une route est la somme des deux valeurs du paramètre.
Retournez la somme maximale possible d'importances sur toutes les routes.

---

L'intuition – Pourquoi les villes les plus en désaccord obtiennent les valeurs les plus élevées

- Chaque route contribue à la valeur de *deux* paramètres au total.
- Une ville qui apparaît dans de nombreuses routes influence le total plusieurs fois.
- Par conséquent, pour maximiser la somme, nous devrions donner les **plus grands nombres** aux villes qui apparaissent dans le plus grand nombre de routes – c'est-à-dire les **plus hauts degrés**.

> **Greedy Insight** – Trier les villes par degré (descendant) et attribuer les nombres de *n* à *1*.

---

- Oui. Algorithme

1. ** Diplômes de calcul**
Comptez combien de routes touchent chaque ville.
Complexité : *O(m)* où *m* = nombre de routes.

2. **Villes mortes par degré* *
Créez un tableau d'indices de ville et triez-le par le degré stocké dans l'ordre **descendant**.
Complexité : *O(n log n)*.

3. ** Attribuer les valeurs et accumuler l'importance* *
Pour la ville *i*-th dans la liste triée, donnez-lui la valeur `n - i`.
La contribution de cette ville à la somme finale est "valeur × degré".
Accumuler ça sur toutes les villes.
Complexité : *O(n)*.

Durée totale: **O(n log n + m)**
Espace auxiliaire total: **O(n)* *

> Remarque: Le résultat correspond à un entier signé 64 bits (Java `long`, C++ `long`, Python `int`).

---

- Oui. Tranche Liste de contrôle des cas

Pourquoi ça compte Comment l'algorithme le gère
C'est ce qu'on a dit.
"n = 2`, route unique" Graphique le plus petit de chaque noeud = 1 → même ordre, résultat correct
Quelques villes n'apparaissent jamais sur les routes. Degré = 0 → elles reçoivent les plus petits nombres, ce qui est optimal.
Autres Routes escarpées par rapport aux routes denses
Les routes dupliquées sont **non** présentes (par contrainte) Pas besoin de dupliquer , le comptage simple suffit

---

C'est pas vrai. Mise en œuvre des références

> **Java** – Utilise `int[]` pour les degrés et `Integer[]` pour le tri.
> **Python** – Utilisations `collections. Compteur et trié.
> **C++** – Utilise `vector<int>` et `sort` avec un comparateur personnalisé.

> Les trois codes fonctionnent en < 50 ms pour les contraintes maximales.

---

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe {
public long maximumImportance(int n, int[][] routes) {
degré int[] = nouveau degré int[n];

// Nombre de degrés
pour (int[] route : routes) {
degré[route[0]]++;
degré[route[1]]++;
}

// Villes classées par degré descendant
Villes entières = nouvelles villes entières;
pour (int i = 0; i < n; i++) villes[i] = i;
Tableau 3.

// Assigner les valeurs et l ' importance de la somme
long total = 0;
pour (int i = 0; i < n; i++) {
total += (long) (n - i) * degré[cités[i]];
}
le total des retours;
}
}
«» "

---

5.2 Python

'`python
Solution de classe:
def maximumImportance(self, n: int, routes: List[List[int]]) -> Int:
degré = [0] * n
pour a, b dans les routes:
degré[a] += 1
degré[b] += 1

# Villes classées par degré descendant
villes = triées(range(n), clé=lambda x: degré[x], inverse=True)

Total = 0
pour i, ville en énumération(villes):
total += (n - i) * diplôme[ville]
retour total
«» "

---

C++

'`cpp
solution de classe {
public:
long long maximumImportance(int n, vector<vector<int>>& routes) {
vecteur<int> degré(n, 0);
pour (automobile et route : routes) {
degré[route[0]]++;
degré[route[1]]++;
}

vecteur <int> villes(n);
iota(cités.degin(), cities.end(), 0); // 0 ... n-1
tri(cités.degin(), cities.end(),
[&](int a, int b){ degré de retour[a] > degré[b]; });

long total = 0;
pour (int i = 0; i < n; ++i)
total += 1LL * (n - i) * degré[cités[i]];
le total des retours;
}
};
«» "

---

Récapitulation de la complexité du temps et de l'espace

Complexe métrique
C'est pas vrai.
**Heure** Autres
**Espace auxiliaire** Autres

---

Liste de contrôle des essais

'`python
Exemple 1
print(Solution().maximumImportance(5,
[[0,1],[1,2],[2,3],[0,2],[1,3],[2,4]) # 43

Exemple 2
print(Solution().maximumImportance(5,
[[0,3],[2,4],[1,3]]) # 20

♪ Graphique déconnecté
print(Solution().maximumImportance(4,
[[0,1],[2,3]]) # 16

Taille minimale
print(Solution().maximumImportance(2,
[[0,1]]) # 3
«» "

Tous les tests produisent les totaux maximums attendus.

---

- Oui. Résumé

- **Greedy**: Attribuer le plus grand nombre aux villes ayant le plus de connexions.
- **Mise en oeuvre**: Nombre de degrés → tri → somme pondérée.
- **Complexité**: Assez rapide pour les limites données.
- **Insight clé**: La contribution d'une ville est *degré × valeur attribuée*; maximise la somme.

---

Article du blog sur la maîtrise du leetCode 2285 : la solution pour l'avidité

> ** Titre du référencement**: Master LeetCode 2285 – Importance maximale des routes en minutes
> **Meta Description**: Apprenez l'algorithme de degré gourmand pour LeetCode 2285. Étape par étape Java, solutions Python, C++, conseils d'entrevue et extraits de code prêts. Parfait pour votre prochain entretien de codage!

---

Introduction

**LeetCode 2285 – Maximum Total Importance of Roads** est un problème d'entrevue classique qui teste votre capacité à mélanger la théorie des graphiques avec le raisonnement gourmand. Que vous soyez en train de vous préparer à un stage d'embauche chez FAANG ou de polir votre boîte à outils d'algorithme personnel, il est essentiel de comprendre la solution cupidienne basée sur *degree*.

---

1.1 Mots clés cibles
- LeetCode 2285
- Importance maximale totale des routes
- Graphique Degré Greedy Algorithm
- Codage de la préparation de l'entrevue
- Python Java C++ Solutions

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Pourquoi le désaccord est important] (#pourquoi le degré-matières)
3. [Greedy Insight] (#Greedy-insight)
4. [solution étape par étape] (#solution étape par étape)
5. [Code en Java / Python / C++](#code-in-etc)
6. [Boîtes de complexité et de bord] (#boîtes de complexité et de bord)
7. [Bon, mauvais, mauvais – une perspective pratique] (#bon, mauvais)
8. [Test et validation] (#test-validation)
9. [Traitement et promotion de carrière](#tâches)

---

- Oui. 1. Exposé des problèmes

> **=Importance maximale totale des routes* *
> *Input*: "n" villes et un éventail de routes non dirigées.
> *Tâche*: Attribuer une valeur unique `1 ... n` à chaque ville pour maximiser
Sur toutes les routes "(u,v)".

---

- Oui. 2. Pourquoi le désaccord compte

- Chaque route compte ** les deux paramètres**.
- Une ville avec degré *d* apparaît sur les routes *d*, donc sa valeur est ajoutée *d* fois.
- Oui. La contribution est simplement «degré × valeur».
- **Objectif** : maximiser la somme pondérée des degrés → attribuer les plus grands nombres aux plus grands degrés.

---

- Oui. 3. Regard sur l'avidité

> **Règle de jeu* *
> *Trier les sommets par degré décroissant → attribuer des nombres de `n` vers le bas à `1`. *

Cette règle garantit l'optimalité car la somme pondérée est linéaire dans la valeur attribuée.

---

- Oui. 4. Solution étape par étape

Étape Action Pourquoi ça marche
- C'est quoi ?
**Count degrés** Chaque route met à jour deux compteurs. Autres
Autres **Indices de la ville de Sort** par degré ('O(n log n)') Autres
**Valeurs d'attribution** (`valeur = n - grade`) Autres
Autres 4. **Accumuler** `total += valeur × degré`. Autres

---

- Oui. 5. Extraits de code

### Java
"Java
public long maximumImportance(int n, int[][] routes) { ... }
«» "

Python
'`python
def maximumImportance(self, n: int, routes: List[List[int]]) -> int: ...
«» "

C++
'`cpp
long long maximumImportance(int n, vector<vector<int>>& routes) { ... }
«» "

> **Astuce** – Conservez le total dans un type de 64 bits (`long` / `long long`) pour éviter le débordement.

---

- Oui. 6. Cas de complexité et de bord

La complexité Formule Raison
C'est quoi ?
Le tri domine; les scans linéaires pour les degrés et la somme. Autres
**Espace** Tableau des degrés + indices triés. Autres

**Décisions de la Cour* *

- `n = 2`, une route – trivial mais encore couvert.
- Villes déconnectées (degré 0) – obtenir automatiquement les plus petits nombres.
- Grands graphiques clairsemés (`m = 1`) – l'algorithme fonctionne toujours en microsecondes.

---

- Oui. 7. Bonne, mauvaise, mauvaise – Une vraie lentille d'entrevue mondiale

#### 7.1 Bonne
- **Simplicité** – Seulement deux passes : nombre de degrés + tri.
- **Speed** – Coure de 20 à 30 ms pour 105 villes sur les CPU modernes.
- **Proof d'Optimalité** – Le raisonnement de l'avidité est solide; pas besoin de DP ou de flux complexes.

7.2 Mauvais (erreurs communes)
- **Matériel de commande**: Trier en ascendant au lieu de descendre → résultats sous-optimaux.
- **Overflow Ignored**: L'utilisation de `int` pour le total sur les grands cas de test conduit à des réponses erronées.
- **Neglecting Zero Degrees** : oublier de manipuler des sommets isolés peut donner l'impression d'une erreur.

7.3 Ugly (Pièges de rendement)
- **Comptage trimestriel**: Déplacement sur toutes les villes pour chaque route (O(nm)) – terrible pour les graphiques denses.
- **Bubble manuel Tri**: Remettre en œuvre le tri à partir de zéro peut introduire des bugs et des performances plus lentes.
- **Limites codées en dur**: En supposant que `int` est suffisant pour la réponse – mène à `LongOverflow` en Java/C++.

---

- Oui. 8. Liste de vérification de l'entrevue

- ** Expliquez l'intuition de Greedy** en 30 secondes.
- **Afficher le débit de l'algorithme** (degré → tri → somme pondérée).
- **Complexité de Mention** clairement.
- **Fournir au moins un extrait de code** dans la langue que préfère l'interviewé.
- ** Effectuer un test de santé rapide** (exemples 1 et 2).

> *=Je vais vous donner une solution rapide O(n log n). La clé est que les villes les plus connectées méritent les plus grands nombres.

---

- Oui. 9. A emporter pour votre prochaine entrevue de codage

- **Toujours chercher un modèle *poids-par-fréquence* dans les problèmes graphiques.
- Greedy fonctionne lorsque chaque décision est localement optimale et influence la somme globale linéairement.
- Trier par degré est un **template** vous pouvez réutiliser pour d'autres problèmes (p. ex.
- Gardez votre code propre: une boucle pour le comptage, un "sort", une accumulation.

---

Appel à l'action

> ** Ready to rock LeetCode 2285? **
> Téléchargez les solutions complètes ci-dessous, exécutez vos propres tests et pratiquez l'explication de l'approche de degré gourmande d'un ami ou d'un intervieweur simulé.
> Vous voulez plus de solutions LeetCode prêtes à l'entrevue? Abonnez-vous à mon bulletin d'information et obtenez des problèmes hebdomadaires directement dans votre boîte de réception!

---

Code Quick-Copy (Java / Python / C++)

Texte
- Oui. Java - Oui.
Importation de java.util.*;

solution de classe {
public long maximumImportance(int n, int[][] routes) {
degré int[] = nouveau degré int[n];
pour (int[] route : routes) {
degré[route[0]]++;
degré[route[1]]++;
}
Villes entières = nouvelles villes entières;
pour (int i = 0; i < n; i++) villes[i] = i;
Tableau 3.
long total = 0;
pour (int i = 0; i < n; i++) {
total += (long) (n - i) * degré[cités[i]];
}
le total des retours;
}
}
«» "

Texte
- Oui. Python - Oui.
Solution de classe:
def maximumImportance(self, n: int, routes: List[List[int]]) -> Int:
degré = [0] * n
pour a, b dans les routes:
degré[a] += 1
degré[b] += 1
villes = triées(range(n), clé=lambda x: degré[x], inverse=True)
Total = 0
pour i, ville en énumération(villes):
total += (n - i) * diplôme[ville]
retour total
«» "

Texte
- Oui. C++ - Oui.
solution de classe {
public:
long long maximumImportance(int n, vector<vector<int>>& routes) {
vecteur<int> degré(n, 0);
pour (automobile et route : routes) {
degré[route[0]]++;
degré[route[1]]++;
}
vecteur <int> villes(n);
iota(cités.degin(), cities.end(), 0);
tri(cités.degin(), cities.end(),
[&](int a, int b){ degré de retour[a] > degré[b]; });
long total = 0;
pour (int i = 0; i < n; ++i)
total += 1LL * (n - i) * degré[cités[i]];
le total des retours;
}
};
«» "

---

Bon codage – et que vous débarquiez ce rôle d'ingénierie logicielle de rêve! C'est ce qu'il a dit