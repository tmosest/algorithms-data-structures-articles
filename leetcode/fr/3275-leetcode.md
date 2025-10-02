---
titre: LeetCode 3275. K-th plus près Obstacle requêtes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le bon, le mauvais et le mauvais de LeetCode 3275 – Les questions les plus près d'un obstacle* *

> Si vous pouvez résoudre cela en moins de 2 minutes, vous impressionnerez n'importe quel gestionnaire d'embauche.
> — *Quelques intervieweurs très expérimentés*

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi ce problème est-il à l'origine de votre dossier d'entrevue] (#pourquoi ce problème-rocks-votre entretien-portfolio)
3. [Le bien – La solution élégante Max-Heap] (#le bien)
4. [Le "Bad" – Pièges communs et comment les éviter] (#the-bad)
5. [The Ugly – Advanced Tweaks & Performance Conseils] (#the-ugly)
6. [Code complet (Java / Python / C++)](#code complet)
7. [Enregistrement – Comment faire tourner l'entrevue] (#Enregistrement)
8. [SEO-Friendly Takeaway](#seo-takeaway)

---

## Aperçu du problème <a name="problem-overview"></a>

> **LeetCode 3275 – Les questions les plus près d'un obstacle**
> **Difficulté:** Moyenne

Vous êtes sur un plan 2-D infini.
- Au départ, il n'y a pas d'obstacles.
- Vous recevez `queries[i] = [x, y]` – ajoutez un obstacle à cette coordonnée.
- Après chaque insertion, vous devez retourner la distance de l'obstacle **k‐th le plus proche** de l'origine.
- La distance est la distance de Manhattan: `..
- Oui. S'il y a moins d'obstacles `k`, retourner `-1`.

**Contrôles* *

Valeur
- C'est quoi ?
"1 ≤ requêtes.longueur ≤ 2·105"
"-109 ≤ x, y ≤ 109"
1 ≤ k ≤ 105
Autres Toutes les requêtes sont uniques.

**Exemple**

Texte
requêtes = [[1,2],[3,4],[2,3],[-3,0], k = 2
Produit : [-1,7,5]
«» "

---

## Pourquoi ce problème est-il à l'origine de votre portefeuille d'entrevues <un nom></a>

- **Modèle classique de la structure des données**: tas (en file d'attente prioritaire) – une base pour les entrevues de codage.
- ** Grande taille d'entrée** : nécessite des mises à jour `O(log k)`, et non `O(n)` par requête.
- **Space‐efficace**: ne garder que les distances «k» supérieures.
- **Proof en langage brut**: vous pouvez le résoudre en Java, Python ou C++ – montrant une polyvalence.

---

## Le Bon – La Solution Élégante Max-Heap <un nom Le Bon></a>

Intuition

Gardez un **max-heap** (en attente prioritaire) qui stocke les **k les plus petites** distances vues jusqu'à présent :

- Oui. Le sommet du tas est le **plus grand** parmi ces k plus petites distances.
- Oui. Cette valeur est précisément l'obstacle le plus proche**.
- Oui. Si nous insérons une nouvelle distance et que la taille du tas devient `k+1`, nous popons le haut (le plus grand) – ne maintenant que le plus petit k.

Algorithme

Texte
pour chaque requête (x, y):
d
Pousser d dans max-heap
si heap.size > k:
pop le haut (le plus grand)
Si c'est un tas. taille == k:
résultat = heap.top() // kth distance la plus proche
Sinon:
résultat = -1
«» "

La preuve de l'exactitude

- **Invariant**: Après avoir traité les premières requêtes `i`, le tas contient les plus petites distances `min(k, i)` parmi les premiers obstacles `i`.
- **Base**: `i = 0` → tas vide → invariant tient.
- **Étape**: Lors de l'ajout de la distance `d`:
- Si `i < k`: taille du tas `= k`, poussez simplement `d`.
- Si `i ≥ k`: poussez `d`; le tas a maintenant des éléments `k+1`. Le popping le plus grand restaure l'invariant.
- Oui. Par conséquent, le sommet du tas est la plus petite distance « k » lorsque la taille du tas est égale à « k ».

---

- Oui. Le "Bad" – Pièges communs et comment les éviter <un nom "the-bad"></a>

Pourquoi ça arrive ?
- Oui.
En utilisant un **min-heap** au lieu d'un max-heap. Autres
Autres Oublier à **pop** quand la taille du tas dépasse `k`. Autres
En utilisant `int` pour la distance lorsque les coordonnées peuvent être `±109`.
Retour **-1** lorsque la taille du tas est < `k` mais ne met pas à jour le tableau `results`
Impossible de manipuler les coordonnées dupliquées** Le problème garantit l'unicité, mais oublier de compter sur elle peut causer une mauvaise logique.

---

- Oui. L'Ugly – Avancé Tweaks & Performance Astuces <a name="the-ugly"></a>

1. ** Inscrire les lots**
Si de nombreuses requêtes sont traitées hors ligne, vous pouvez d'abord trier toutes les distances et utiliser un arbre Fenwick ou un arbre segment pour répondre à chaque requête dans le temps `O(log n). Pas nécessaire pour LeetCode mais utile dans les compétitions.

2. **Éviter les appels absolus répétés* *
Pré-calculer `abs` une fois par requête; en boucles serrées, insérez l'opération.

3. **Tapis optimisé pour la mémoire* *
Pour les langues comme Java, utilisez `IntPriorityQueue` (fast-util) ou `PriorityQueue<integer>` avec un comparateur personnalisé.
Dans C++, `std::priority_queue<int, vector<int>, plus<int>>` est déjà un heap min; utiliser `moins<int>` pour le heap max.

4. **Parallélisation**
Non applicable pour LeetCode, mais si vous avez plusieurs cœurs, vous pouvez diviser les requêtes et fusionner des tas partiels.

5. **Profil du pire cas**
Temps le plus défavorable: "O(n log k)"; mémoire du pire cas: "O(k)".
Pour `n = 2·105`, `k = 105`, c'est confortablement rapide dans les trois langues.

---

## Code complet (Java / Python / C++) <a name="full-code"></a>

Voici des implémentations propres et bien commentées dans **Java 17**, **Python 3.10** et **C++17**.

C'est pas vrai. Java

"Java
Importation de java.util.*;

***
* LeetCode 3275 – Les questions les plus près de K
*/
solution de classe publique {
résultats publics int[]Array(int[][] requêtes, int k) {
int n = requêtes. longueur;
// Max-heap pour garder les plus petites distances k
PriorityQueue<Long> maxHeap = nouveau PriorityQueue<>(Collections.reverseOrder());

int[] res = nouvelle int[n];
pour (int i = 0; i < n; i++) {
longue dist = requêtes Math.abs(long)[i][0] + requêtes Math.abs((long)[i][1]);
maxHeap.offre(dist);

// Conserver seulement les éléments k
si (maxHeap.size() > k) {
le nombre maximal d'unités de mesure est égal à celui des unités de mesure.
}

res[i] = (maxHeap.size() == k) ? maxHeap.peek().intValue() : -1;
}
retour rés;
}

// Conducteur (facultatif)
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
questions int[] = {{1,2},{3,4},{2,3},{-3,0}};
int k = 2;
Système.out.println(Arrays.toString(sol.resultsArray(queries, k)));
// Produit: [-1, 7, 5, 3]
}
}
«» "

# # # # # #

'`python
de taper l'importation Liste
importation heapq

Solution de classe:
Résultats Array(self, requêtes: List[List[int]], k: int) -> Liste[int]:
# Max-heap utilisant des distances négatives
max_heap = []
res = []

pour x, y dans les requêtes :
dist = abs(x) + abs(y)
heapq.heappush(max_heap, -dist) # pousser négative pour simuler max‐heap

si len(max_heap) > k: # conserver la taille <= k
heapq.heappop(max_heap)

res.append(-max_heap[0] si len(max_heap) == k sinon -1)

retour res

♪ Démo
si __nom__ == "__main__" :
sol = Solution()
requêtes = [[1,2],[3,4],[2,3],[-3,0]]
k = 2
print(sol.resultsArray(queries, k)) # [-1, 7, 5, 3]
«» "

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> résultatsArray(vecteur<vector<int>>& requêtes, int k) {
// Max-heap: plus grande distance en haut
priority_queue<long long> maxHeap;
vecteur<int> rés;
res.reserve(queries.size());

pour (auto &q : requêtes) {
longue dist longue = llabs(q[0]) + llabs(q[1]);
maxHeap.push(dist);

si (maxHeap.size() > k) // garder seulement k plus petit
le point d'entrée est remplacé par le texte suivant:

Res.push_back((int)(maxHeap.size()) == k ? maxHeap.top() : -1));
}
retour rés;
}
};

// Optionnel principal() pour les essais locaux
Int main() {
Solution s;
vecteur<vecteur<int>> requêtes = {{1,2},{3,4},{2,3},{-3,0}};
int k = 2;
vecteur<int> ans = s.résultats Arrangements (requêtes, k);
pour (int v : ans) cout << v << '; // -1 7 5 3
}
«» "

> **Conseil**: Compilez avec `-O2 -std=c++17` pour LeetCode.

---

## Wrapping Up – Comment faire pour éponger l'entrevue <a name="wrapping-up"></a>

1. **Commencez avec une déclaration claire** – réécrivez le problème dans vos propres mots.
2. **Expliquez le choix de la structure des données**: tas, pourquoi max-heap, quelles opérations nous avons besoin.
3. **Parcourir un exemple** sur le tableau blanc.
4. **Boîtes à bord**: moins d ' éléments < < k > > , grandes coordonnées.
5. **Discuse la complexité** ("O(n log k)", "O(k)" espace).
6. **Extensions possibles** pour montrer la profondeur.
7. **Testez localement** – utilisez les extraits de démo pour vérifier.

---

## SEO-Friendly Takeaway <a name="seo-takeaway"></a>

> **Titre:** Master LeetCode 3275 (K‐th Obstacle le plus proche) – Java, Python, C++
> **Mots clés:** LeetCode 3275, K‐th obstacle le plus proche, Manhattan distance, tas, file d'attente prioritaire, entretien de codage, solution Java, solution Python, solution C++, complexité temporelle, complexité spatiale, modèles d'entretien de codage.

**Pourquoi cela importe :**
- Les recruteurs analysent les titres des motifs – votre article contient le nom exact du problème et les étiquettes de langue.
- Les moteurs de recherche classent les articles avec une forte densité de mots clés et une structure utile.
- Oui. En incluant ce contenu, vous allez apparaître dans les meilleurs résultats pour la solution de requêtes d'obstacles la plus proche.

---

- Oui. Comment faire pour éponger l'entrevue <a name="wrapping-up"></a>

- **Afficher votre processus de pensée**: commencer par une idée simple (mauvaise), puis l'affiner.
- **Demander des éclaircissements** : p. ex., l'avion est-il loin de Manhattan ?
- **Écrire un code propre et autonome**; ne pas compter sur des bibliothèques cachées.
- **Parlez de la complexité** avant d'écrire le code.
- **Si le temps le permet**, mentionnez les modifications avancées que nous avons couvertes.

Bonne chance, vous avez compris ! C'est ce qu'il a dit.

---

**Prêt pour le prochain défi? **
Découvrez **LeetCode 3275** aujourd'hui et laissez le tas travailler pour vous.

---

**#LeetCode3275 #CodingInterview #Heap #Priorité Demande #Java #Python #C++**
---

La pensée finale

En maîtrisant l'astuce **max-heap** dans ce problème, vous démontrerez une pensée algorithmique solide et une forte compréhension des structures de données de base – exactement ce que les recruteurs recherchent. Bon codage !