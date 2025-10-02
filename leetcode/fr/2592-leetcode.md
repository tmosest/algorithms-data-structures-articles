---
titre: LeetCode 2592. Maximiser la grandeur d'un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2592. ** Maximiser la grandeur d'un tableau** –
### Un guide complet de préparation à l'entrevue
C++*

---

### TL;DR
- **Objectif :** Réorganiser les "nums" pour maximiser le nombre d'indices où la nouvelle valeur est *strictement plus grande* que la valeur originale.
- **Greedy / Astuce à deux points :** Triez `nums` ascendant, puis utilisez deux indices (`i` – =candidate, `j` – =current) pour choisir le plus petit élément qui bat `nums[j]`.
- **Complexité temporelle:** `O(n log n)` (pour le tri).
- **Complexité spatiale:** `O(1)` auxiliaire (si nous trions en place) ou `O(n)` Si nous utilisons une copie.

---

- Oui. 1. Récapitulation des problèmes

> **Définition de la grandeur* *
> Pour une permutation `perm` du tableau initial `nums`, la *grandeur* est le nombre des indices `i` où `perm[i] > nums[i]`.

> **Tâche**
> Retourner la grandeur maximale possible après toute permutation de "nums".

---

- Oui. 2. Intuition et stratégie

1. **Trier le tableau**
Le tri nous donne les plus petits nombres disponibles à l'avant, ce qui est parfait pour une approche gourmande : nous voulons le plus petit nombre qui peut encore battre un élément particulier.

2. **Deux pointeurs**
- `i` – scanne à travers le tableau trié (les valeurs de "candidate").
- `j` – scanne le tableau d'origine (indices de la cible).
Nous essayons de jumeler le plus petit candidat qui est *plus grand* que la cible actuelle.

3. **Pourquoi l'avidité fonctionne* *
- Si nous avons un candidat `c` qui bat `nums[j]`, l'utiliser ici ne peut pas aggraver la réponse plus tard parce qu'un candidat plus grand pourrait également battre `nums[j]`.
- L'utilisation du plus petit candidat possible permet de disposer d'un plus grand nombre de candidats, ce qui maximise les possibilités futures.

---

- Oui. 3. Algorithme (Pseudocode)

«» "
Tri(nombres) // ascendant
i = 0 // indice du candidat
nombre = 0

pour j en 0 .. nombres. length-1: // j est l'indice cible
alors que i < nums.longueur et nums[i] <= nums[j]:
i += 1 // sauter tous les nombres qui ne peuvent pas battre nums[j]
Si i == longueur nums.:
pause // plus de candidats laissés
nombre += 1 // nombres[i] bat nombres[j]
i += 1 // passer au candidat suivant

Nombre de retours
«» "

---

- Oui. 4. Analyse de la complexité

Opération Coût
- C'est quoi ?
Trier "O(n log n)" Autres
Analyse à deux points Autres
Autres Temps total Autres
Autres Espace supplémentaire **`O(1)`** (tri en place) ou `O(n)` si une copie est nécessaire

Les contraintes (`n ≤ 105`) sont traitées confortablement par cette approche.

---

- Oui. 5. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

---

#### 5.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
de l'intérêt public Maximiser la grandeur(int[] nums) {
// Trier le tableau pour activer la stratégie avide à deux points
Tableaux.sort(nums);
int n = longueur nums;
i = 0; // pointeur candidat
nombre int = 0;

// Indices d'origine inversés
pour (int j = 0; j < n; j++) {
// Avancez i jusqu'à ce que nous trouvions un nombre qui bat les nombres[j]
alors que (i < n && nums[i] <= nums[j]) {
i++;
}
si (i == n) pause; // plus de candidats
nombre++; // nombres[i] > nombres[j]
i++; // utiliser ce candidat
}
le nombre de retours;
}

// Harnais d'essai rapide
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.maximizeGreatness(new int[]{1,3,5,2,1,1}); // 4
Système.out.println(sol.maximizeGreatness(new int[]{1,2,3,4}); // 3
}
}
«» "

---

5.2 Python

'`python
Solution de classe:
def maximum Grandeur (soi-même, nombres: list[int]) -> Int:
nums.sort() # en place tri
n = len(nums)
i = 0 # indice du candidat
nombre = 0

pour j dans la plage(n):
alors que i < n et nums[i] <= nums[j]:
i += 1
n: # plus de candidats
pause
nombre += 1
i += 1

Nombre de retours

# Test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.maximizeGreatness([1, 3, 5, 2, 1, 3, 1]) # 4
print(sol.maximizeGrandeté([1, 2, 3, 4])) # 3
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximum Grandeur(vecteur<int>& nums) {
tri(nums.begin(), nums.end()); // ascendant
int n = nombres.size();
i = 0; // pointeur candidat
nombre int = 0;

pour (int j = 0; j < n; ++j) {
alors que (i < n && nums[i] <= nums[j]) ++i;
si (i == n) pause; // plus de candidats
++compte; // nombres[i] > nombres[j]
++i;
}
le nombre de retours;
}
};

// Essai rapide
Int main() {
Solution sol;
Cout << sol.maximizeGreatness({1,3,5,2,1,3,1}) << endl; // 4
Cout << sol.maximizeGrandeté({1,2,3,4}) << endl; // 3
retour 0;
}
«» "

---

- Oui. 6. Article de blog – Le bon, le mauvais, et le lamentable de LeetCode

#### 6.1 Pourquoi ce problème est-il un grand arrêt d'entrevue

- **Profondeur conceptuelle:** Il teste le raisonnement *greedy*, *deux-pointer* et une compréhension que le tri peut déverrouiller la structure cachée.
- **Language-agnostique:** Votre solution fonctionne en Java, Python, C++, Allez, Rust – la même idée, juste une syntaxe différente.
- **Évoluable :** Avec `n = 105`, une approche naïve `O(n2)` serait sans temps, donc les intervieweurs apprécient une solution `O(n log n)`.

6.2 Les bonnes

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Simplicité**= Après tri, la logique se réduit à un seul passage linéaire. Autres
**Déterministe** Autres
**Le temps déterministe est acceptable même pour les grandes entrées. Autres
La technique avide est réutilisable (p. ex., problème de deux tableaux permutants). Autres

Les mauvais

Sujet Atténuation
- C'est quoi ?
**Traitement du coût**= Pour des tableaux extrêmement grands (`n > 106`), vous pouvez avoir besoin d'un tri de comptage ou de seau, mais pas besoin ici. Autres
**Certains intervieweurs demandent de conserver le tableau original; vous pouvez en faire une copie avant de le trier. Autres
**Cas d'Edge**= Tous les éléments égaux → réponse `0`. Tableau vide (pas dans les contraintes) → gérer gracieusement. Autres

### 6.4 La moche

- **Misscompréhension plus grande que : Certains candidats utilisent accidentellement l'expression « au lieu de l'expression « au lieu de l'expression « au lieu de l'expression « au lieu de l'expression « au lieu de l'expression « au lieu de l'expression » », causant des erreurs hors-par-un.
- **Pointeur dépassé**: Oublier de vérifier `i < n` à l`intérieur de l``intérieur ` while` peut conduire à un `ArrayIndexOutOfBoundsException` en Java ou un défaut de segmentation en C++.
- **Effets secondaires douloureux**: Si l'entrevue nécessite la commande originale pour une utilisation ultérieure, n'oubliez pas de copier le tableau en premier.

#### 6.5 SEO— A emporter amical

Si vous êtes à la recherche d'une solution *=LeetCode 2592* ou *=maximize greatness of an array interview==*, ce guide est votre guichet unique:

- **Titre** – *LeetCode 2592 – Maximiser la grandeur d'un tableau – Java, Python, C++ Solutions*
- **Description de la Meta** – Découvrez comment résoudre LeetCode 2592 avec le code Java, Python et C++. Comprendre l'approche cupide à deux points, les cas de bord et les conseils d'entrevue. (en milliers de dollars)
- **Mots clés** – LeetCode, Maximize Greatness, array permutation, deux pointeurs, algorithme gourmand, interview de codage, défi algorithmique, solution Java, solution Python, solution C++, préparation d'entretien d'emploi.

---

- Oui. 7. Mots finals – Comment faire l'entrevue

1. ** Expliquez l'idée cupide** – Déprimez le tableau afin que nous puissions toujours choisir le plus petit nombre qui bat la cible actuelle. (en milliers de dollars)
2. **Mention temps/espace** – Nous trions dans `O(n log n)` et ensuite exécutez un balayage linéaire. (en milliers de dollars)
3. **Cover edge cases** – Tous les éléments sont égaux → 0; taille du tableau 1 → 0.
4. **Afficher le code** – Fournir la solution propre et commentée dans la langue de votre choix.
5. ** Réutilisabilité de la lumière** – Le même schéma résout les problèmes de «Permuting Two Arrays» et de nombreux problèmes de «beat‐the‐cible». (en milliers de dollars)

Avec cette approche, vous transformerez un problème de LeetCode apparemment complexe en une vitrine de conception d'algorithmes propres et de solides compétences de codage – exactement ce que veulent les recruteurs. Bonne chance !