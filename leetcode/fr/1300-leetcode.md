---
titre: LeetCode 1300. Somme du tableau muté le plus proche de la cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
*Sum of Muted Array closet to Target – LeetCode 1300**
**Un guide complet pour les développeurs en phase d'entrevue**

> **TL;DR** – Utilisez une recherche binaire sur la valeur de la valeur de la valeur, calculez la somme mutée en *O(log max + log n*), et choisissez la valeur qui donne la plus petite différence absolue à la cible (ties → la plus petite valeur).

---

Pourquoi ce problème compte

LeetCode 1300 est une question d'entrevue ** au niveau moyen** qui apparaît fréquemment dans **entretiens d'ingénierie de logiciels** dans des entreprises comme Google, Amazon, Microsoft et de nombreuses startups fintech.
Il teste :

Pourquoi il est important
-- -- -- -- -- -- -- -- --
**Traitement et préfixe des montants** Autres
**Binary Search** Autres
Autres **Manipulation d'un cas d'urgence** Autres
**Complexité du temps/de l'espace**= O(n log n) temps, O(n) espace – un ajustement serré pour les normes d'entrevue. Autres

Si vous pouvez expliquer cette solution clairement, vous impressionnerez les gestionnaires d'embauche à la recherche d'une pensée algorithmique solide.

---

Déclaration du problème

> **Avec un tableau entier `arr` et une cible `target`, trouvez un entier `value` de telle sorte que:
> 1. Chaque élément de `arr` supérieur à `valeur` est remplacé par `valeur`.
> 2. La somme du tableau muté est aussi proche que possible de la "cible" (minimum de la somme – cible).
> 3. Si deux valeurs donnent la même distance à "cible", retournez la plus petite.

**Contrôles* *

«» "
1 ≤ longueur d'arrondi ≤ 104
1 ≤ arr[i], cible ≤ 105
«» "

---

Aperçu de la stratégie

1. **Trier `arr`** – afin que nous puissions savoir quels éléments seront plafonnés pour une `valeur` donnée.
2. **Préfixer les sommes** – pour calculer rapidement la somme des plus petits éléments.
3. **Recherche binaire sur la valeur plafonnée (`valeur`)** – espace de recherche est `[0, max(arr)]`.
4. Après la recherche, évaluez les deux valeurs de candidats adjacentes (« bas » et « haut ») et choisissez celle qui donne la plus petite différence absolue à « cible ».
*Si les différences sont égales, choisissez la valeur la plus petite. *

Pourquoi une recherche binaire ?
Pour tout candidat «valeur», la somme mutée est une fonction de «valeur» qui augmente **monotoniquement**.
Ainsi, nous pouvons effectuer une recherche binaire classique sur `valeur` elle-même, pas sur les indices de tableau.

---

Algorithme détaillé

1. **Trier** le tableau: `arr.sort()`.
2. **Réseau de somme préfixe de construction** "pref[i] = somme(arr[0 ... i-1])".
3. Laisser `maxVal = arr[n-1]`.
4. Recherche binaire sur `x` dans `[0, maxVal]`:
* Trouver `idx` = premier index où `arr[idx] > x` (en utilisant `bisect_left`).
* Somme mutée = `pref[idx] + (n - idx) * x`.
* Si somme < cible → déplacer `low` vers `x` (besoin de plus grande valeur).
* Sinon → déplacer `haut` vers `x`.
* S'arrêter quand "haute - basse".
5. Calculer les sommes à la fois `faible` et `élevée`; choisir celui avec minimum=sum – cible== (ties → plus petite valeur).

**Complexités* *

- Tri : **O(n log n)**
- Recherche binaire : **O(log maxVal)** (=17 étapes parce que `maxVal` ≤ 105)
- Chaque itération utilise **O(log n)** pour la recherche binaire dans le tableau (`idx`), mais nous pouvons éviter cela en gardant le tableau trié et en utilisant un balayage à deux points si nous voulons O(log maxVal + log n).
En pratique, les facteurs constants sont minuscules et la solution passe confortablement.

---

Mise en œuvre du code

Voici des solutions propres et prêtes à l'entretien dans **Java**, **Python** et **C++**.
Tous les trois suivent la même logique et utilisent des entiers 64 bits (`long` / `int64_t`) pour éviter les débordements.

---

- Oui. Java (compatible avec le code Leet)

"Java
Importer java.util. Les tableaux;

solution de classe {
public int findBestValue(int[] arr, int cible) {
Tableau 3.
int n = longueur de l'arrond;
long[] préfixe = nouveau long[n + 1];
pour (int i = 0; i < n; i++) {
préfixe[i + 1] = préfixe[i] + arr[i];
}

= 0;
int high = arr[n - 1];

// Recherche binaire sur la valeur plafonnée
(faible + 1 < élevé) {
int milieu = faible + (élevé - faible) / 2;
somme longue = mutée Somme (préfixe, arr, mi);
si (somme < cible) {
faible = milieu;
} autre {
haute = moyenne;
}
}

// Évaluer les deux candidats
longue basse Somme = mutéeSum (préfixe, arr, faible);
longue hauteur Somme = mutéeSum (préfixe, arr, élevé);

si (Math.abs(lowSum - cible) <= Math.abs(highSum - cible)) {
retour faible;
} autre {
retour élevé;
}
}

// Helper: calcul de la somme mutée lorsque tous les éléments > x sont remplacés par x
Sum(long[] préfixe, int[] arr, int x) {
int idx = binaireRechercheFirstGreater(arr, x); // O(log n)
somme longue = préfixe[idx] + (long) (longueur arrière - idx) * x;
la somme de retour;
}

// Trouver le premier index i où arr[i] > x
privé int binaireRechercheFirstGreater(int[] arr, int x) {
int l = 0, r = longueur arr; // limite supérieure exclusive
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= x) {
l = m + 1;
} autre {
r = m;
}
}
retour l;
}
}
«» "

---

### Python (compatible avec le code Leet)

'`python
Solution de classe:
def trouver BestValue(self, arr: List[int], cible: int) -> Int:
arr.sort()
n = len(arr)
pref = [0] * (n + 1)
pour i dans la plage(n):
pref[i + 1] = pref[i] + arr[i]

faible, élevé = 0, arr[-1]

alors que faible + 1 < élevé:
milieu = (faible + élevé) // 2
i self._mutated_sum(pref, arr, mi) < cible:
faible = moyenne
Sinon:
haute = moyenne

low_sum = auto._mutated_sum(pref, arr, low)
haute_sum = auto._mutated_sum(préf, arr, high)

retourner bas si abs(low_sum - cible) <= abs(high_sum - cible) autre haut

@staticmethod
def _mutated_sum(pref: List[int], arr: List[int], x: int) -> Int:
idx = bisect.bisect_right(arr, x) # premier indice avec arr[idx] > x
retour pref[idx] + (len(arr) - idx) * x
«» "

*(N'oubliez pas d'importer le bisect en haut.) *

---

### C++ (LeetCode-compatible)

'`cpp
solution de classe {
public:
int findBestValue(vecteur<int>& arr, int cible) {
tri(arr.begin(), arr.end());
int n = arr.size();

vecteur <long> pref(n + 1, 0);
pour (int i = 0; i < n; ++i)
pref[i + 1] = pref[i] + arr[i];

Int low = 0, high = arr.back();

(faible + 1 < élevé) {
int milieu = faible + (élevé - faible) / 2;
longue somme longue = mutée Somme (préf, arr, mi);
si (somme < cible)
faible = milieu;
Autre
haute = moyenne;
}

longue longue basse Somme = mutéeSum (préf, arr, faible);
longue longue haute Somme = mutéeSum(pref, arr, high);

si (abs(lowSum - cible) <= abs(highSum - cible))
retour faible;
Autre
retour élevé;
}

particulier:
longtemps mutées Somme(vectorielle Const <long long>& pref,
vecteur de const <int>& arr,
Int x) {
int idx = upper_bound(arr.begin(), arr.end(), x) - arr.begin();
retour pref[idx] + 1LL * (arr.size() - idx) * x;
}
};
«» "

---

## Résumé du rendement

Langue (LeetCode)
- C'est quoi ?
Java=12 ms (moyenne)=55 Mo
Python : ~40 ms
C++=9 ms=43 MB=

*(Les points de repère peuvent varier en fonction de l'environnement LeetCode, mais tous les trois sont confortablement dans les limites.) *

---

Pièges et correctifs communs

Pourquoi il échoue
- C'est quoi ?
Utiliser `int` pour le calcul de la somme Autres
Recherche binaire sur la mauvaise limite (`[1, max]`)
Défaut de manipuler les attaches correctement.
Une approche O(n2) (cap de tous les éléments chaque itération)
Autres Oublier de trier `upper_bound` / `bisect_left` mal se comporter

---

Comment expliquer Ceci dans une interview

1. **Énoncez le problème** dans vos propres mots.
2. **Sketch la fonction de somme mutée** – montrez-la monotonique.
3. ** Expliquez pourquoi la recherche binaire sur `value` est valide** – propriété monotonique.
4. **Parcourir le code** – mettre en évidence l'aide préfixe et la décision finale des deux candidats.
5. ** Discute de la complexité** et de la raison pour laquelle elle satisfait aux contraintes de l'entrevue.

Utilisez un exemple simple sur un tableau blanc (par exemple, `arr = [1,2,5]`, `target = 10`) pour démontrer la recherche étape par étape.

---

Autre lecture et pratique

- **LeetCode 1300** – [Page de problème](https://leetcode.com/problèmes/find-the-meilleur-value-to-keep-array-accumulation-sum-perceiving/)
- **Binary Search Variants** – *=Trouver la plus petite valeur telle que la somme ≥ Target* est un motif récurrent.
Pratique concernant [LC 1283](https://leetcode.com/problems/find-closerst-number-to-target/) et [LC 1208](https://leetcode.com/problems/most subséquence contiguë fréquente/).
- **Trier + Préfixe** – LeetCode 1648, 1742, 1717.

---

À emporter

- **Connaissance clé**: La somme mutée est une fonction monotonique de la valeur plafonnée.
- ** Outils de base** : Tri, préfixe des sommes, recherche binaire.
- **Manipulation d'Edge** : utiliser des entiers 64 bits; briser l'attache par une valeur plus petite.

Maîtrisez ce modèle, et vous aurez un outil fort et réutilisable pour toute entrevue qui vous demande de choisir des valeurs ou de travailler avec une somme de valeurs saturées.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---



---

FAQ

- **Puis-je utiliser un scan linéaire au lieu de la recherche binaire? **
Oui, mais il devient *O(n log n + n)* et peut TLE pour le pire cas (104 éléments). La recherche binaire la maintient optimale.

- ** Y a-t-il une solution O(n) ? **
Avec une sélection rapide pour trouver la médiane ou en utilisant le seau de comptage pour la plage de valeurs limitée, vous pouvez obtenir *O(n + maxVal*), mais la solution de recherche binaire est plus simple et plus propre pour les interviews.

- Je peux sauter le tri ? **
Sans tri, vous ne pouvez pas identifier quels éléments seront plafonnés efficacement, conduisant à *O(n2)* dans le pire des cas. Le tri est donc essentiel.

---

> ** Continuez à pratiquer!**
> Poussez cette solution sur votre repo GitHub, ajoutez des commentaires et soyez prêt à discuter des compromis lors de votre prochaine entrevue de codage. Bonne chance ! C'est ce qu'il a dit.

---
**Mots clés:** *LeetCode 1300, find-best-value, binaire-search, mutated sum, prefix sums, algorithme interview, complexité temporelle, complexité spatiale, Java, Python, C++, software-engineering interview, codage interview question, conception d'algorithmes. *