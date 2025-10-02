---
titre: LeetCode 3572. Maximiser Y-Sum en choisissant un triplet de X-Values Distinct -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3572 – *Maximiser Y-Sum en choisissant un triple de X-Values distinctes*
**Langues:** C++
**Interview Focus:** HashMap, gourmand, temps O(n), espace O(1) (si possible)
**SEO Mots-clés:** Leetcode 3572, Y-Sum, valeurs X distinctes, interview par algorithme, code d'entretien d'emploi, carte de hachage, avide, solution optimale, top 3, Java, Python, C++

---

Récapitulation des problèmes

On vous donne deux tableaux entiers `x` et `y`, tous deux de longueur `n`.
Chaque paire `(x[i], y[i])` peut être vue comme une paire *key-value*.
Choisissez trois indices `i, j, k` de sorte que les valeurs **x soient toutes distinctes* *
(`x[i] != x[j] != x[k]`).
Retourner la somme maximale possible `y[i] + y[j] + y[k]`.
S'il est impossible de choisir trois «x»-valeurs distinctes, retourner «-1».

Contraintes
- "3 ≤ n ≤ 10^5"
- `1 ≤ x[i], y[i] ≤ 10^6`

---

## -Savoir-faire

Pour toute valeur donnée «x» nous ne nous soucions que de son **maximum** «y».
Si nous gardons le plus haut `y` pour chaque `x` distinct, le problème devient:

> *De l'ensemble de ces valeurs `y` maximum, choisissez les trois premiers et ajoutez-les. *

Ainsi, tout le défi est réduit à:
1. Construire une cartographie `x → max(y)` – **O(n)**.
2. Choisissez les trois plus grandes valeurs cartographiées – **O(k)** où `k` est le nombre de `x` uniques.

Voici trois implémentations idiomatiques en Java, Python et C++.

---

Solution 1 – HashMap + PrioritéQueue (Java)

"Java
Importation de java.util.*;

solution de classe {
Int public maxSumDistinctTriplet(int[] x, int[] y) {
Carte <entier, entier> maxY = nouveau HashMap<>();

// 1. Conserver seulement le maximum y pour chaque x
pour (int i = 0; i < x.longueur; i++) {
(x[i], Math.max(maxY.getOrDefault(x[i], 0), y[i]);
}

// 2. Mettez toutes les valeurs dans un max-heap et pop le top 3
Priorité Queue<integer> pq = nouvelle prioritéQueue<>(Collections.reverseOrder());
pq.addAll(valeurs maximumY());

si (pq.size() < 3) retour -1;

= 0;
pour (int i = 0; i < 3; i++) somme += pq.poll();
la somme de retour;
}
}
«» "

- **Temps**: "O(n + k log k)" (opérations en lourd).
- **Espace**: `O(k)` – le tas plus le hashmap.

---

Solution 2 – HashMap + Tri (Python)

'`python
de taper l'importation Liste
importation heapq

Solution de classe:
def maxSumDistinctTriplet(self, x: List[int], y: List[int]) -> Int:
max_y = {}
pour xi, yi en zip(x, y):
max_y[xi] = max(max_y.get(xi, 0), yi)

si len(max_y) < 3:
retour -1

# Le plus grand du heapq donne les 3 plus grandes valeurs
top_three = heapq.nmest(3, max_y.values())
retour sum(top_trois)
«» "

- **Time**: `O(n + k log k)` – `nmest` fonctionne dans `O(k log 3)` qui est effectivement "O(k)".
- **Espace**: `O(k)` – le dictionnaire.

---

Solution 3 – Pure Greedy Pass (C++)

'`cpp
solution de classe {
public:
int maxSumDistinctTriplet(vecteur<int>& x, vecteur<int>& y) {
int best[3] = {0, 0, 0};
clé int[3] = {0, 0, 0};

pour (int i = 0; i < x.size(); ++i) {
si (x[i] == clé[0]) meilleur[0] = max(meilleur[0], y[i];
sinon si (x[i] == clé[1]) meilleur[1] = max(best[1], y[i]);
sinon, si (x[i] == clé[2]) meilleur[2] = max(meilleur[2], y[i]);
autres {
// nouvelle clé – essayez de l'insérer dans la plus petite fente
int mn = min(meilleur[0], min(meilleur[1], meilleur[2]);
si (y[i] > mn) {
si (mn == best[0]) { best[0] = y[i]; clé[0] = x[i]; }
sinon si (mn == best[1]) { best[1] = y[i]; clé[1] = x[i]; }
autre {meilleur[2] = y[i]; clé[2] = x[i]; }
}
}
}

Si (meilleur[0]] == 0="meilleur[1]== 0="meilleur[2]== 0)
retour -1; // moins de 3 clés uniques
le meilleur retour[0] + meilleur[1] + meilleur[2];
}
};
«» "

- **Heure**: `O(n)` – un balayage linéaire.
- **Espace**: "O(1)" – seulement six entiers (trois valeurs + trois clés).
- **Pourquoi c'est le meilleur pour les interviews**:
- Pas de conteneurs au-delà d'une poignée de variables.
- Démontre une stratégie avide claire qui peut être expliquée en quelques minutes.

---

Pourquoi ce col est idéal pour les entrevues

Explication
C'est pas vrai.
**O(n) temps**L'intervieweur aimera vous voir éviter un tas explicite ou trier étape. Autres
**O(1) espace auxiliaire**Vous montrez que vous pouvez garder l'algorithme maigre. Autres
**Facile d'expliquer**='Conservez le meilleur `y` pour chaque `x`; remplacez toujours le plus petit des trois premiers si un meilleur apparaît.=' Autres

Le seul compromis :
Si vous avez besoin de la solution optimale la plus défavorable quand `k` est énorme, vous pouvez revenir à la priorité L'approche en file d'attente ou de tri, mais ceux-ci utilisent de l'espace supplémentaire.

---

Nombre de cas d ' essai

X X X X X X X
C'est quoi ?
"[1,2,1,34]"" "[5,7,9,2,10]"" "26" (10+9+7)"
[1,1,1] Autres
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

---

Pièges communs

Comment éviter
C'est quoi ?
**Ajouter toutes les valeurs `y` avant la déduplication**= Toujours map `x → max(y)` *avant* toute logique de prise en haut 3=. Autres
**Utiliser `int` pour les sommes qui peuvent déborder**= Avec `y[i] ≤ 10^6` et `n ≤ 10^5`, la somme de trois valeurs correspond à l'int signé 32 bits (`=3·10^6'), mais soyez prudent dans d'autres langues. Autres
**Obligation de la valeur inférieure à trois touches uniques.

---

La feuille de chaleur de complexité

Démarche Temps Espace supplémentaire
- C'est quoi ?
HashMap + PQ. Autres
HashMap + Sort Autres
"O(n)" Autres

---

## -Take final- Loin

- Le *core* du problème est une réduction simple **max-value par clé**.
- Oui. L'approche gourmande est le *standard d'or* pour les intervieweurs : temps linéaire, mémoire auxiliaire constante, et pas d'appels de bibliothèque fantaisie.
- Oui. Si vous voulez une solution rapide, les variantes HashMap + PQ ou Sort fonctionnent aussi bien.

---

Article du blog – Le bon, le mauvais, et le mauvais de Leetcode 3572

---

Titre
**Le code 3572: Le bon, le mauvais et le mauvais – Une plongée profonde dans la distinction Somme triple de la clé**

Description de la méta
> Apprenez comment cracker Leetcode 3572 en Java, Python et C++. Découvrez la solution optimale O(n) gourmande, les pièges communs et le code prêt à l'entrevue. Augmentez votre préparation d'entrevue de codage et atterrissez votre prochain travail!

Introduction 250 mots

> Dans le monde du codage des interviews, **Leetcode 3572 – Maximiser Y-Sum en choisissant un triplet de X-Values Distinct** est un favori pour tester une maîtrise candidate de cartes de hachage et de logique gourmande. Le problème vous demande de coupler deux tableaux, de ne conserver que les meilleures valeurs par clé, puis de résumer les trois principales clés distinctes.
>
> Sur le papier, il semble simple, mais beaucoup de candidats trébuchent sur des détails subtils : oublier de dédoubler, mal gérer la file d'attente prioritaire, ou ignorer le cas de bord de moins de trois clés uniques. Dans ce post, nous allons casser la solution en trois sections—**le bon**, **le mauvais**, et **le mauvais**—et fournir des extraits de code prêts à l'interview en Java, Python et C++ que vous pouvez coller dans votre prochaine solution de Leetcode ou reprendre.

### Les bonnes – La stratégie Élégante, Interview-Proof

*Traitements clés: *
- **O(n) temps, O(1) espace** (en utilisant le col gourmand).
- Oui. Un seul passe par les données.
- Logique claire : Si vous trouvez un meilleur candidat, remplacez le plus petit des trois premiers.

> Dans la pratique, c'est le code que vous allez voir sur StackOverflow, discuter dans les blogs de technologie, et mettre en œuvre dans vos projets personnels. C'est aussi celui que vous devriez mettre en évidence dans un entretien d'emploi parce qu'il montre une compréhension profonde du raisonnement avide.

- Oui. La mauvaise – Suringénierie avec des conteneurs supplémentaires

* Approches communes : *
- **HashMap + Tri**: Construit une carte de maxima puis trie les valeurs.
- **HashMap + PriorityQuue**: Insère toutes les maxima dans un tas et vote les trois premiers.

Bien que les deux fonctionnent dans le temps `O(n + k log k)` et sont faciles à écrire, ils ajoutent des éléments supplémentaires de mémoire inutiles (`k`). Pour les intervieweurs, cela peut ressembler à un manque de sensibilisation à l'optimisation, surtout quand `n` peut être 105.

- Oui. L'Ugly – Mauvaise lecture des contraintes

- **En utilisant des entiers 64 bits pour la somme lorsque 32 bits est suffisant**: L'espace de type déchets.
- **Indices de sélection au lieu de clés**: Conduis à des bogues off-by-one dans la vérification à clé distincte.
- **Ne pas gérer correctement les valeurs dupliquées "x"**: Le maximum `y` par `x` est le crux; l'ignorer donne des résultats incorrects.

Ces erreurs sont typiques dans les solutions rapides de copie-colle et donnent généralement lieu à un verdict de `Wrong Answer` sur Leetcode.

---

### Exemples de codes complets (Java, Python, C++)

> Les trois extraits implémentent le **greedy O(n) pass**. Vous pouvez échanger les versions map/heap si vous préférez.

#### Java (Greedy O(n))

"Java
Importation de java.util.*;

classe publique Leetcode3572 {
Int public maxSumDistinctTriplet(int[] x, int[] y) {
// trois meilleures valeurs et leurs clés correspondantes
int a = 0, b = 0, c = 0;
Int key1 = -1, key2 = -1, key3 = -1;

pour (int i = 0; i < x.longueur; i++) {
int currX = x[i], currY = y[i];

si (currX == clé1) a = Math.max(a, currY);
sinon si (currX == clé2) b = Math.max(b, currY);
sinon, si (currX == key3) c = Math.max(c, currY);
autres {
// nouvelle clé – remplacer la plus petite des trois si elle est meilleure
int mn = Math.min(a, Math.min(b, c));
si (currY > mn) {
si (mn == a) { a = currY; key1 = currX; }
sinon si (mn == b) { b = currY; key2 = currX; }
sinon { c = currY; key3 = currX; }
}
}
}

retour (clef1 == -1--clé2 == -1-clé3 == -1) ? -1 : a + b + c;
}

public statique vide principal(String[] args) {
Leetcode3572 solveur = nouveau Leetcode3572();
[] x = {1, 2, 1, 3, 4};
int[] y = {5, 7, 9, 2, 10};
Système.out.println(solver.maxSumDistinctTriplet(x, y)); // 26
}
}
«» "

Python (Greedy O(n))

'`python
Solution de classe:
def maxSumDistinctTriplet(self, x, y):
a = b = c = 0
key1 = key2 = key3 = Aucun

pour xi, yi en zip(x, y):
Si xi == clé1:
a = max(a, yi)
xi de l'élif == clé2:
b = max(b, yi)
xi de l'élif == key3:
c = max(c, yi)
Sinon:
mn = min(a, b, c)
si yi > mn:
si mn == a:
a, clé1 = yi, xi
* B:
b, clé2 = yi, xi
Sinon:
c, clé3 = yi, xi

retourner -1 sinon (key1 et key2 et key3) sinon a + b + c
«» "

#### C++ (Greedy O(n))

*(Voir l'extrait ci-dessus dans la section "Pure Greedy Pass"*

---

### Comment utiliser ces extraits dans votre mémoire

1. **Ajouter un code à gauche 3572 – Distinct‐ Key Triplet Sum** sous Projets techniques ou défis de codage.
2. Décrivez brièvement la logique avide : *=Linear-time, algorithme d'espace constant qui maintient les trois premières paires de valeurs clés.
3. En option, un lien vers ce billet de blog ou joindre un Gist pour une référence facile.

---

### Clôture (= 200 mots)

> Cracking Leetcode 3572 n'est pas juste à propos d'obtenir la bonne réponse; il est à propos de montrer à l'intervieweur que vous pouvez penser *efficacement*, *proprement* et *robustly*.
>
> Le col O(n) avide démontre les trois : il fonctionne dans le temps linéaire, n'utilise que des variables primitives, et transmet clairement l'idée clé de la meilleure valeur par clé. (en milliers de dollars)
>
> Si vous préparez une entrevue technique ou polissez votre CV de codage, gardez cette stratégie au sommet de votre boîte à outils mentale. C'est un modèle éprouvé qui impressionnera les gestionnaires d'embauche à la recherche d'un code efficace et prêt à l'entrevue.

### Appel final à l'action

> * Prêt à s'attaquer au Leetcode 3572? Prenez les extraits de code ci-dessus, lancez-les contre les cas de test fournis, et ajoutez la solution gourmande à votre GitHub. Puis, dans votre prochaine entrevue, expliquez avec confiance la logique et montrez-vous que vous n'êtes pas seulement codant – vous êtes l'optimisation. *

### Mots clés et référencement Mots clés

- `code de la nuit 3572`
- "Codage de la préparation de l'entrevue"
- "Hash carte cupide "
- "somme triplette à clé distincte"
- `algorithme d'entretien "

---

Pourquoi vous Voir ceci sur le marché du travail

> Les recruteurs scannent souvent des recommendations pour des solutions de code de lecture 3572 qui mettent en évidence *temps linéaire* et *espace constant*. Un candidat qui peut pointer vers l'algorithme avide et l'expliquer en 3 à 5 minutes démontre une forte maturité algorithmique – un différenciateur clé pour les rôles logiciels seniors.

---

Enveloppe

> En comprenant *le bon*, *le mauvais* et *le laid*, vous pouvez choisir la bonne version de Leetcode 3572 pour toute situation – qu'il s'agisse d'un test de codage rapide ou d'un entretien technique approfondi. Collez les extraits fournis, pratique expliquant la logique, et vous serez prêt à aborder le problème avec confiance.

Fin de l'article

---

Appel à l'action pour les lecteurs

- **Pratique**: Copiez le code dans Leetcode et exécutez les tests d'échantillon.
- **Partager** : postez vos solutions sur GitHub ou Gist et liez-les dans votre CV.
- **Interview**: Pratique expliquant le passage avide en 30 secondes à un ami ou un mentor.

---

Note finale

> *Cracking Leetcode 3572 n'est pas seulement d'écrire n'importe quelle solution – il s'agit de choisir l'approche la plus conviviale, d'anticiper les cas de bord, et d'articuler clairement votre raisonnement. *

---

**Codage heureux – et bonne chance pour votre prochaine entrevue! * *

---

> (Word compter 1 350). Ce billet de blog est prêt à être partagé sur Medium, Dev.to, ou un blog personnel de technologie pour attirer les recruteurs à la recherche de solutions de Leetcode bien optimisées.

---

N'hésitez pas à adapter n'importe quelle partie de cet article ou de ce code à votre style ou à l'emploi spécifique que vous ciblez. Bonne chance !