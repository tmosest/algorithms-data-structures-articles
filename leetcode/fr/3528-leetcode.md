---
Titre: LeetCode 3528. Conversion d'unité Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Ci-dessous sont **trois solutions complètes, prêtes à la production** pour LeetCode 3528 – Conversion d'unité I.
Chaque solution fonctionne en temps **O(n)** et en mémoire **O(n)**, manipulant facilement les limites (`n ≤ 105`, `facteur ≤ 109`).

La langue Idée clé Complexité
C'est pas vrai.
**Java**= DFS itératif sur un arbre dirigé (racine 0) – produit modulo *M*= **O(n)** temps, **O(n)** mémoire
**Python**==========================================================================================================================================================================================================================================================
DFS à base de piles – modulo du produit

> **NOTE**
> Le problème garantit que les « conversions » forment un arbre **dirigé enraciné à 0** (chemin unique de 0 à chaque noeud).
> Par conséquent, une simple propagation en profondeur du produit est suffisante – pas besoin de BFS ou Dijkstra.

---

### 1.1 Java – `Solution.java "

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

base publique int[]UnitConversions(int[][] conversions) {
int n = conversions.longueur + 1;
Liste<int[]>[] graphique = nouvelle liste de tableaux[n];
pour (int i = 0; i < n; i++) graphe[i] = nouvelle liste de distribution<>();

// Construire la liste d'adjacence dirigée
pour (int[] e : conversions) {
int src = e[0], tgt = e[1], facteur = e[2];
graph[src].add(new int[]{tgt, facteur});
}

long[] ans = nouveau long[n];
[0] = 1L; // 1 unité de type 0 égale 1 unité de type 0
Deque<Integer> pile = nouvelle ArrayDeque<>();
pile.push(0);

pendant que (!stack.isEmpty()) {
u = pile.pop();
pour (int[] edge : graph[u]) {
int v = bord[0];
long f = bord[1];
ans[v] = (ans[u] * f) % MOD;
empilage.push(v);
}
}

// Convertir en tableau int avant de retourner
résultat int[] = nouveau résultat int[n];
pour (int i = 0; i < n; i++) résultat[i] = (int) ans[i];
le résultat du retour;
}
}
«» "

---

### 1.2 Python – `solution.py "

'`python
de taper l'importation Liste

MOD = 10**9 + 7

Solution de classe:
def base UnitConversions(self, conversions: List[List[int]]) -> Liste[int]:
n = len(conversions) + 1
g = [[] pour _ dans l ' intervalle n)]
pour src, tgt, f en conversions:
g[src].append(tgt, f))

ans = [0] * n
ans[0] = 1
pile = [0]

pendant la pile:
u = pile.pop()
pour v, f en g[u]:
% MOD
pile.append(v)

retour et
«» "

---

### 1.3 C++ – `solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
static const int MOD = 1'000'000'007;

vector<int> baseUnitConversions(vecteur<vector<int>>& conversions) {
int n = conversions.size() + 1;
vecteur<vector<pair<int,long>>> g(n);
pour (auto &e : conversions) {
int src = e[0], tgt = e[1];
long f = e[2];
g[src].push_back({tgt, f});
}

vecteur <long> ans(n, 0);
[0] = 1;
Pile <int> m;
s.push(0);

pendant que (!st.vide()) {
u = st.top(); st.pop();
pour (auto &p : g[u]) {
int v = p.first;
long f = p.seconde;
ans[v] = (ans[u] * f) % MOD;
le point v) est remplacé par le texte suivant:
}
}

vecteur<int> res(n);
pour (int i = 0; i < n; ++i) res[i] = static_cast<int>(ans[i]);
retour rés;
}
};
«» "

Les trois implémentations utilisent **itative DFS** (stack) pour éviter le débordement de la pile pour les arbres profonds (jusqu'à 100 000 nœuds).
Ils propagent le produit des facteurs de conversion de la racine (unité 0) à tous les autres nœuds, en prenant le modulo `1 000 000 007` selon les besoins.

---

- Oui. 2. Article de blog – Unit Conversion I sur LeetCode: le bon, le mauvais, et le mauvais

> **SEO Mots-clés:** *LeetCode 3528*, *Unit Conversion*, *Java solution*, *Python solution*, *C++ solution*, *DFS*, *BFS*, *graph tree*, *coding interview*, *job interview*, *algorithme analyse*, *software engineer interview*, *coding interview questions*

---

2.1 Introduction

Lorsque vous préparez une entrevue d'ingénierie logicielle, le jeu de problèmes LeetCode est votre terrain de jeu. Parmi les nombreux défis de l'unité, **Unit Conversion I (LeetCode 3528)** se distingue: il teste graphe traversal, arithmétique modulaire, et la capacité de repérer la structure cachée dans l'entrée.

Dans ce post nous allons disséquer le problème, marcher à travers les solutions les plus élégantes dans **Java, Python, et C++**, et discuter:

* **Le Bon** – pourquoi le problème est une grande question d'entrevue
* **Les mauvais** – pièges communs qui voyagent candidats
* **Le Ugly** – nuances de cas de bord qui peuvent en silence briser votre code

À la fin, vous aurez une solution prête à la production et un récit clair à partager avec les intervieweurs.

---

2.2 Récapitulation du problème

Vous recevez des types d'unités `n` (0 ... n‐1) et un tableau `conversions` de longueur `n-1`.
Chaque élément `conversions[i] = [source, cible, facteur]` signifie *1 unité de `source` équivaut à `facteur` unités de `cible`*.

**Objectif:** Pour chaque type d'unité `i`, calculer le nombre d'unités de type `i` équivalent à *une* unité de type "0". Retourner les résultats modulo `1 000 000 007`.

**Contrôles* *

* «2 ≤ n ≤ 105»
* `1 ≤ facteur ≤ 109 "
* Le graphique est un arbre **dirigé enraciné à 0** (chemin unique de 0 à n'importe quel noeud).
* La réponse peut être énorme, si modulo `MOD = 1 000 000 007` est obligatoire.

---

2.3 Mettre en évidence la structure cachée – La bonne

Le problème ressemble à un problème générique du graphique pondéré, mais la ligne supplémentaire dans les contraintes est un billet d'or*:

> *Il est garanti que l'unité 0 peut être convertie en n'importe quelle autre unité par une combinaison unique de conversions. *

Cela signifie que l'entrée est en fait un arbre ** dirigé** (pas de cycles, pas de branchement de la racine vers elle-même). En théorie graphique, les arbres sont les structures les plus simples connectées. Une fois que vous reconnaissez cela, l'ensemble du problème se réduit à un seul DFS/BFS qui multiplie les poids de bord le long du chemin unique.

Pourquoi est-ce un bon aperçu de l'entrevue?

1. **Épargnes de temps** – vous évitez les algorithmes génériques les plus courts (Dijkstra, Bellman-Ford) qui seraient autrement exagérés.
2. **Clarté** – un énoncé de problème clair → une stratégie de solution claire → un répondant confiant.
3. **Optimisation** – vous pouvez implémenter un algorithme *O(n*) qui s'inscrit confortablement dans une limite de 1 s.

---

2.4 L'algorithme – Propagation du DFS

**Idée de base**
À partir de la racine (unité 0), traverser l'arbre.
Pour chaque bord `u → v` avec le poids `w`, propager

«» "
valeur[v] = valeur[u] * w mod MOD
«» "

Parce que le chemin de 0 à n'importe quel noeud est unique, il n'y a pas besoin de la logique ou des files d'attente de priorité.

**Détails sur la mise en œuvre**

Étape Que faire ? Pourquoi ça compte ?
- C'est quoi ?
Construire une liste d'adjacence. Autres
Autres Utiliser une pile/queue itérative. Autres
Maintenir les valeurs intermédiaires "long`" `long val = ans[u] * w % MOD; `" facteur` peut être jusqu'à `109`; le produit peut déborder `int`. Autres
Return `int[]`.Convertir le `long[] ans` en `int[]` avant de retourner. Autres

> **BFS contre DFS**
> Les deux vont bien. DFS (stack) est un peu plus mémoire-friendly pour les arbres parce que vous devez seulement stocker les valeurs parent. BFS (queue) ferait de même avec essentiellement les mêmes frais généraux.

---

#### 2.5 Passage du code – Les cas de bords laids

Langue Erreur commune
C'est ce qu'on dit.
Le code Leet attend `int[]`. La conversion finale est obligatoire. Autres
**Python**= Utiliser `stack = [0]` et `stack.pop()` Fonctionne, mais une "deque" donne un peu meilleure performance pour les grandes n.
Utiliser `int` pour les poids. Autres

C'est vrai. Tranche Décision 1: Modulo Zero
Lorsque `facteur` est un multiple de `MOD`, `facteur % MOD` devient 0 et propage zéro en aval. C'est *correct* parce que modulo arithmétique se comporte ainsi. Assurez-vous d'appliquer le modulo **après** chaque multiplication, pas seulement à la fin.

C'est vrai. Tranche Cas 2 : Dépassement des entiers 32 bits
«1 000 000 007 × 109» dépasse la plage d'entier signée de 32 bits («»;
Utiliser `long` (64-bit) pour le produit intermédiaire, puis prendre `mod` garantit l'exactitude.

C'est vrai. Tranche Cas 3: Taille de la pile en récursion
Un DFS récursif naïf peut faire sauter la pile d'appel JVM/CPython/C++ sur un arbre profond. Utiliser une pile explicite (`ArrayDeque` / `std::stack`) est un *must*.

---

2.5 Analyse de complexité

Algorithme Temps Espace
- C'est quoi ?
(tous les nœuds et bords visités une fois)
BFS / file d'attente
Générique Dijkstra (si vous avez ignoré la propriété de l'arbre)

La solution optimale est la plus simple et la plus rapide, vous donnant un avantage **10 points** dans une entrevue.

---

2.6 Entretien Conseils prêts

1. ** Expliquez la propriété de l'arbre d'abord** – demandez à l'intervieweur si le graphique est garanti être un arbre. Il montre que vous cherchez des contraintes cachées.
2. ** Clarifier l'opération modulo** – assurez-vous que l'intervieweur sait que vous prendrez `mod` à *chaque multiplication*, pas seulement la réponse finale.
3. **Discuss pile vs récursion** – mentionner pourquoi une approche itérative est plus sûre pour le LeetCode 100 000 limite.
4. **Afficher le code en plusieurs langues** – vous pouvez dire que j'ai un DFS propre, O(n) en Java/Python/C++.

---

2.7 Ce que le recruteur remarquera

* **Reconnaissance des arbres** – le repérage de la structure de l'arbre est la marque d'un codeur assaisonné.
* **Attention au détail** – manipuler correctement le modulo, en utilisant `long` pour éviter le débordement, et en choisissant un passage itératif, tous démontrent un codage prêt à la production.
* **La communication** – en passant par l'algorithme étape par étape montre que vous pouvez simplement expliquer des idées complexes – une compétence souple critique pour les rôles supérieurs.

---

2.8 Bonus : Comment utiliser ce problème pour un point de vue réel

Si vous postulez pour un rôle **Backend Engineer** ou **Systems Engineer**, vous pouvez encadrer votre solution en tant que moteur de conversion modulaire.
* J'ai construit un système léger de propagation à base d'arbres qui peut être étendu à des graphiques dirigés arbitraires. (en milliers de dollars)
* Le modèle arithmétique modulaire que j'ai utilisé ici est exactement ce que nous employons dans les contrôles d'accès basés sur des jetons. (en milliers de dollars)

Ces connexions vous aident à transformer un problème de codage en un **histoire sur l'architecture** que les gestionnaires d'embauche aiment.

---

2.9 Pensée finale

Conversion des unités Je suis faussement simple quand vous lisez attentivement les contraintes.
Un DFS/BFS propre qui multiplie les poids le long d'un arbre est la stratégie *optimale*.
Avec les trois échantillons de code ci-dessus, vous êtes prêt à impressionner n'importe quel intervieweur – qu'ils demandent **Java**, **Python** ou **C++**.

> **Prochaines étapes**
> 1. Exécutez les solutions sur le harnais de test LeetCode.
> 2. Ajoutez-les à votre feuille de tricherie personnelle. (en milliers de dollars)
> 3. Pratique expliquant la propriété de l'arbre et l'algorithme de propagation – la question la plus fréquente sera *=Pourquoi avez-vous choisi DFS sur Dijkstra?

Bonne chance, et que votre entretien soit aussi doux qu'un arbre parfaitement équilibré!

---

### 2.10 TL;DR

- Oui. Qu'est-ce que vous allez apprendre ?
-- -- -- -- -- -- -- -- --
Autres Reconnaissance des arbres dans les problèmes graphiques
O(n) propagation DFS avec module **Candidats** – facile à coder, rapide
* Tous** – copier-coller dans votre IDE

Déposez ces extraits dans votre portfolio, lancez-les contre les tests LeetCode, et apportez le **story** de l'arbre caché dans votre prochaine interview. Bonne chance – et profiter de la conversion des unités de temps en victoires d'entrevue!