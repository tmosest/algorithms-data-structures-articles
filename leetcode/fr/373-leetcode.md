---
titre: LeetCode 373. Trouvez des paires K avec les plus petites sommes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

♪ Trouvez des paires K avec les plus petites sommes – 373 – LeetCode
> **Votre guide unique pour maîtriser ce problème d'interview en Java, Python et C++* *

> **Meta‐Description** – Apprenez à résoudre le LeetCode 373 . Préparez-vous pour votre prochaine entrevue de codage avec des solutions claires et multilingues, une couverture de cas de bord et une analyse de blogs.

---

- Oui. 1. Pourquoi ce problème est important

- **Le sujet de l'entrevue à haute fréquence** – presque toutes les interviews de backend senior demandent les plus petites paires* ou une variation similaire.
- **Démontre la maîtrise de la structure des données** – files d'attente prioritaires, ensembles de hachage et astuces à deux points.
- **Showcases time-space compromis** – vous devrez expliquer pourquoi un min-heap bat une solution "O(m*n)" naïve.

Si vous pouvez attraper ce problème dans **Java**, **Python** et **C++**, vous aurez un point de discussion solide pour les interviews techniques et le codage des bootcamps.

---

- Oui. 2. Déclaration de problème (Code de bord 373)

On vous donne deux tableaux entiers **triés** `nums1` et `nums2`, et un entier `k`.

Une paire* est définie comme étant `(u, v)` où `u` vient de `nums1` et `v` vient de `nums2`.

Retournez les paires **k** avec les plus petites sommes.

> **Exemples**
> ```texte
> nombres1 = [1, 7, 11]
> nombres2 = [2, 4, 6]
> k = 3
> Produit: [[1, 2], [1, 4], [1, 6]]
> `` "
> ```texte
> nombres1 = [1, 1, 2]
> nombres2 = [1, 2, 3]
> k = 2
> Produit: [[1, 1], [1, 1]]
> `` "

> **Constraints**
1 ≤ nums1.longueur, nums2.longueur ≤ 105
> -109 ≤ nombres1[i], nombres2[i] ≤ 109
> - 1 ≤ k ≤ 104
> - `k` ≤ `nums1.longueur` × `nums2.longueur`

---

- Oui. 3. La rupture de la bonne – mauvaise – mauvaise

**Aspect**
C'est pas vrai.
**Structure des données**=L'extraction de Min-heap donne « O(log k) ». Naïve boucles imbriquées = temps `O(m*n)`, impossible pour 105 tableaux de taille. Oublier les paires de dudupe – les duplicatas peuvent conduire à des résultats incorrects. Autres
**L'espace**=Le tas `O(k)` + `O(k)` visité ensemble.=Le stockage de tout le produit cartésien est un gaspillage. L'utilisation d'un jeu de hachage d'objets `Pair` en Java peut causer de gros frais s'il n'est pas mis en œuvre correctement. Autres
Autres **Cas d'Edge**=Poigne les tableaux vides, la taille du produit `k` >, les valeurs dupliquées. Les limites codées en dur peuvent échouer sur des nombres négatifs ou des erreurs extrêmement importantes k. Autres
**Readability**. Code Java avec des classes internes anonymes. L'utilisation de l'indexation fondée sur 0 par rapport à l'indexation fondée sur 1 dans les commentaires est source de confusion. Autres
**Performance** Si vous poussez à la fois `(i+1, j)` et `(i, j+1)` sans vérifier les limites, vous obtiendrez "ArrayIndexOutOfBounds". Autres

---

- Oui. 4. Approche optimale – Ensemble Min‐Heap + visités

1. **Démarrer** avec la paire `(0, 0)` – la plus petite somme possible.
2. **Le lourd** stocke des tuples: `(sum, i, j)`.
3. **Set visible** se rappelle quels indices ont été poussés pour éviter les duplications.
4. **Alors que** nous avons encore besoin de paires ('k' times) et le tas n'est pas vide:
* Pop la plus petite somme.
* Ajouter `(nums1[i], nums2[j])` au résultat.
* Pousser `(i+1, j)` **Si** il n'a pas été visité et `i+1 < nums1.longueur`.
* Pousser `(i, j+1)` **Si** il n'a pas été visité et `j+1 < nums2.longueur`.
5. **Retour** la liste.

**Pourquoi ça marche* *
Comme les deux tableaux sont triés, les plus petites sommes suivantes sont toujours adjacentes à la plus petite paire actuelle. En poussant seulement les deux candidats suivants, nous ne manquons jamais un candidat tout en gardant la taille du tas ≤ k.

**Complexité* *
- Temps: "O(k log k)" (chaque pop/poush est `log k`)
- Espace: `O(k)` (pap + ensemble visité)

---

- Oui. 5. Mise en œuvre du code

Ci-dessous sont **clean, production-ready** implémentations dans **Java**, **Python** et **C++**.
Les trois utilisent la même idée algorithmique et gèrent tous les cas de bord.

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
Liste publique<Liste<Intégrée>> kLes plus petitsPairs(int[] nums1, int[] nums2, int k) {
Liste <Liste<entier>> résultat = nouvelle liste <>();
si (nums1.longueur) : 0. 0) le résultat du retour;

// Commande de petite taille par somme
PrioritéQueue<int[]> minHeap = nouvelle prioritéQueue<>(Comparator.comparingInt(a -> a[0]);
Ensemble <Long> visité = nouveau HashSet<>(); // stocker (i << 32)

minHeap.offre(nouvelle int[]{nums1[0] + nums2[0], 0, 0});
visité.add(encode(0, 0));

pendant que (k-- > 0 & & & !minHeap.isEmpty()) {
nt[] cur = minHeap.poll();
somme int = cur[0];
i = cur[1];
int j = cur[2];

result.add(Arrays.asList(nums1[i], nums2[j]);

si (i + 1 < nums1.longueur) {
clé longue = code(i + 1, j);
si (visited.add(key)) {
minHeap.offre(nouvelle int[]{nums1[i + 1] + nums2[j], i + 1, j});
}
}
si (j + 1 < nums2.longueur) {
clé longue = code(i, j + 1);
si (visited.add(key)) {
minHeap.offre(nouvelle int[]{nums1[i] + nums2[j + 1], i, j + 1});
}
}
}
le résultat du retour;
}

// Encoder deux indices dans un seul long pour éviter les objets Pair
code long privé(int i, int j) {
retour (((long) i) << 32) (j & 0xffffffffL);
}
}
«» "

**Points clés* *

- Utiliser une touche `long` au lieu d'une classe `Pair` personnalisée maintient la mémoire basse.
- Oui. Le comparateur est simple : trier par la somme précalculée.
- Les cas de bord sont traités en amont (`k == 0`, tableaux vides).

---

#### 5.2 Python 3

'`python
importation heapq
de taper l'importation Liste, Tuple

Solution de classe:
def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> Liste[Liste[int]]:
s'il n'y a pas de nombres1 ou pas de nombres2 ou k == 0:
retour []

résultat: Liste[List[int]] = []
min_heap: Liste[Tuple[int, int, int]] = [] # (sum, i, j)
visité = set() # store (i, j) tuples

heapq.heappush(min_heap, (nums1[0] + nums2[0], 0, 0))
visité.add((0, 0))

alors que k et min_heap:
s, i, j = heapq.heappop(min_heap)
résultat.append([nums1[i], nums2[j]])
k -= 1

i + 1 < len(nums1) et (i + 1, j) non visités:
heapq.heappush(min_heap, (nums1[i + 1] + nums2[j], i + 1, j))
visité.add(i + 1, j))

si j + 1 < len(nums2) et (i, j + 1) non visités:
heapq.heappush(min_heap, (nums1[i] + nums2[j + 1], i, j + 1))
visité.add(i, j + 1))

résultat du retour
«» "

** Faits saillants* *

- `heapq` donne un tas binaire efficace hors de la boîte.
- Le jeu `visited` empêche de pousser les paires d'index dupliqués.
- Les conseils de type font l'auto-documentation de la fonction.

---

C++

'`cpp
#incluez <vecteur>
#incluez <queue>
#inclut <unordered_set>
#incluez <fonctionnel>

solution de classe {
public:
md::vector<std::vector<int>> kPairs les plus petits(
L'objectif est de faire en sorte que l'utilisation de l'énergie nucléaire soit considérée comme une source d'énergie.
L'objectif est de faire en sorte que l'utilisation de l'eau potable et de l'eau potable ne soit pas compromise.
Int k) {

md::vector<std::vector<int>> rés;
Si (nums1.vide()) 0) retour rés;

// Min–heap: {sum, i, j}
en utilisant HeapNode = std::tuple<int, int, int>;
cmp = [](cont HeapNode& a, cont HeapNode& b) {
retour à la md::get<0>(a) > md:get<0>(b); // inversement pour min‐heap
};
std::priority_queue<HeapNode, std::vector<HeapNode>, décltype(cmp)> pq(cmp);
std::unordered_set<long long> visité; // encode (i,j) -> longue

code automatique = [](int i, int j) -> long {
retour (static_cast<long long>(i) << 32) (j & 0xffffffffLL);
};

pq.emplace(nums1[0] + nums2[0], 0, 0);
visited.insert(encode(0,0));

pendant que (k > 0 & & & !pq.vide() {
auto [s, i, j] = pq.top(); pq.pop();
res.push_back({nums1[i], nums2[j]});
--k;

si (i + 1 < nums1.size() && visited.insert(encode(i + 1, j))seconde) {
pq.emplace(nums1[i + 1] + nums2[j], i + 1, j);
}
si (j + 1 < nums2.size() && visited.insert(encode(i, j + 1)).second) {
pq.emplace(nums1[i] + nums2[j + 1], i, j + 1);
}
}
retour rés;
}
};
«» "

**Pourquoi c'est rapide en C++**

- `std::tuple<int, int, int>` est léger.
- Encodage des indices dans un seul "long long" garde le set visité maigre.
- Oui. Le comparateur lambda maintient le code concis.

---

- Oui. 6. Essais et bords Cas couverts

**Scénarios **Quoi tester**
C'est ce qu'on dit.
**Tableaux d ' amplitude**
**Nombres négatifs** → des paires correctes
**Les valeurs du duplicata**.
**k plus grand que le produit**
**k = 0** immédiatement
Autres ** Longueur des deux tableaux Essai simple à 1 paire

Utilisez des tests unitaires qui couvrent chacun de ces scénarios – il montre interviewers que vous êtes non seulement pirater une solution mais penser à la robustesse de production.

---

- Oui. 7. Quand n'avez - vous pas besoin de l'ensemble de visites?

Si vous êtes absolument sûr que les deux tableaux ont des valeurs **uniques** et que vous savez que `k` ≤ `nums1.length` + `nums2.length`, vous pouvez **drop** le jeu visité et pousser à la fois `(i+1, j)` et `(i, j+1)` sans condition.
Mais pour les contraintes générales LeetCode, l'ensemble visité est obligatoire – sinon vous allez pousser la même paire plusieurs fois, faire sauter le tas, et produire de mauvaises réponses.

---

- Oui. 8. Entretien rapide‐ Résumé prêt

- **Algorithme**: Min-heap de `(sum, i, j)` + hash ensemble d'indices visités.
- **Complexité**: temps "O(k log k)", espace "O(k)".
- **Pourquoi c'est optimal**: Les entrées triées garantissent que les plus petites sommes suivantes sont voisines.
- **Langues**: prêt à être collé Code Java, Python et C++ ci-dessus.

Si vous pouvez expliquer cela en **5 minutes**, vous êtes à mi-chemin d'une interview stellaire.

---

- Oui. 9. Prochaines étapes – Pratique et entrevue Préparation

1. **Run le code** contre les tests cachés de LeetCode.
2. **Temps vous-même** – une solution `Java` devrait finir sous 1 s sur une entrée 105-size avec `k = 104`.
3. **Exposer les compromis**: Pourquoi un tas est nécessaire, ce qui se passe si vous sautez l'ensemble visité, etc.
4. **Entretien de masse**: Joignez-vous à un ami et pratiquez la discussion « good-bad-ugly » – c'est un début parfait de conversation.

---

10. Appel à l'action

** Prêt à accepter votre prochaine entrevue de codage? * *
- **Télécharger** les solutions multilingues (copie-colle)
- **Run** vos propres tests sur GitHub ou un IDE local
- **Partager** cet article avec des pairs – il est SEO-friendly et prêt pour votre Linked En poste.

Autres **Réservez un entretien simulé avec moi** ou ** rejoignez notre défi hebdomadaire LeetCode** – laissez-les transformer la pratique en performance!

Bon codage !