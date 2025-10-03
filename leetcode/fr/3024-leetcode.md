---
titre: LeetCode 3024. Type de triangle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> **LeetCode 3024 – Type de triangle* *
> On vous donne un tableau entier 0 indexé `nums` de longueur **3** qui contient les longueurs latérales d'un triangle potentiel.
>
> *Retour* `"équilatéral"`, `"isoscèles"`, `"scalene"`, ou `"none"` sur la base des longueurs latérales.

> **Constraints**
> * "longueur en nombres". 3'
> * `1 ≤ nombres[i] ≤ 100`

---

- Oui. 2. Idées fondamentales

1. **Inégalité des triangles** – Pour les 3 côtés "a ≤ b ≤ c", la seule condition requise pour former un triangle est "a + b > c".
2. **Nombre d'unités** – Le type est déterminé par le nombre de longueurs latérales distinctes
* 1 unique → `équilatéral "
* 2 uniques → `isoscèles "
* 3 uniques → `scalene "

Tri des garanties le plus grand côté est à la fin, rendant le contrôle d'inégalité trivial.
Un `Set` (ou une carte de fréquence) donne le nombre unique dans l'espace `O(1)`.

---

- Oui. 3. Mise en œuvre des références

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {
triangle à chaînes publiquesType(int[] nums) {
// 1. Tri pour faire le plus grand côté dernier
Tableaux.sort(nums);

// 2. Contrôle des inégalités dans les triangles
si (nombres[0] + nombres[1] <= nombres[2]) {
retourner "aucun";
}

// 3. Compter les parties distinctes
Définir <integer> distinct = nouveau HashSet<>();
pour (int n : nombres) distinct.add(n);

interrupteur (taille différente()) {
Cas 1: retour "équilatéral";
case 2: retourner les «isoscèles»;
par défaut: retourner "scalene";
}
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def triangle Type(self, nombres: List[int]) -> str:
nums.sort() # plus grand côté dernier
si nombres[0] + nombres[1] <= nombres[2]:
retour "aucun"

distinct = len(set(nums))
s'il est distinct] 1 :
retour "équilatéral"
s'il est distinct] 2 :
retour "isoscelles"
retour "scalene"
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
triangle à cordes Type(vecteur<int> &nums) {
tri(nums.begin(), nums.end()); // côté le plus grand dernier
si (nombres[0] + nombres[1] <= nombres[2]) // inégalité triangle
retourner "aucun";

unordered_set<int> s(nums.begin(), nums.end());
interrupteur (s.dimension()) {
Cas 1: retour "équilatéral";
case 2: retourner les «isoscèles»;
par défaut: retourner "scalene";
}
}
};
«» "

Les trois solutions fonctionnent dans **O(1)** temps (le tri de 3 éléments est constant) et utilisent **O(1)** espace supplémentaire.

---

- Oui. 4. Article de blog – Le bon, le mauvais, et l'acharnement de déterminer le type de triangle

4.1 Pourquoi ce problème est-il important?

- ** Géométrie fondamentale** – Comprendre les propriétés du triangle est une pierre angulaire de la géométrie computationnelle.
- **Compétence d'entrevue** – LeetCode 3024 est une question populaire qui apparaît dans de nombreux entretiens de codage.
- ** Pensée algorithmique** – Il vous force à penser à *cas de pointe* (`0`, négatif, non-triangle) et *structures de données optimales* (`Set` vs. `Map`).

4.2 Les bons

Autres Pourquoi c'est bon
C'est pas vrai.
**Simplicité**Le tri de 3 nombres est banal; pas besoin de structures de données complexes. Autres
**Robustness**Le garde de qualité triangle capture tous les cas impossibles. Autres
**Readability** raconte l'histoire en une seule ligne. Autres
**Temps/Espace**=O(1) temps et espace; parfait pour les contraintes d'entrevue. Autres

### 4.3 Les mauvaises (Pièges d'Edge)

Exemple de réparation
C'est pas vrai.
** Supposons que l'entrée soit triée**. Quelqu'un pourrait sauter le tri et penser par erreur que le tableau est déjà commandé. Toujours trier avant le contrôle des inégalités. Autres
L'utilisation de `>=` au lieu de `>` fait glisser le dégénéré (collinéaire) les triangles. Autres
** Nombre d'unicités incorrectes**= Nombre de fréquences incorrectes (par exemple, l'utilisation de `si (a==b && b==c) ...=) échoue lorsque les côtés sont serrés. Utilisez un jeu pour obtenir le vrai compte unique. Autres

4.4 Les mauvaises approches courantes

Mauvaise approche Pourquoi c'est bizarre
- C'est quoi ?
**L'algorithme de tri à l'échelle complète** (qui utilise Quicksort / Mergesort) est surqualifié et peut être plus lent dans la pratique. Autres
**Les boucles de Nested pour Count**=Vérifier chaque paire pour l'égalité ('si a==b && b==c') devient sujet à erreur lorsque vous ajoutez plus de côtés. Autres
**Missing Triangle Inequality**.Returning a type when `a + b <= c` passe conduit à de mauvaises réponses sur de nombreux tests cachés. Autres
Autres **L'utilisation de l'algorithme est O(n log n) est techniquement vraie pour les tableaux généraux, mais pour n=3 il est trompeur dans un contexte d'entrevue. Autres

---

- Oui. 5. Fermeture optimisée par le SEO

**Titre**: LeetCode 3024: Comment détecter le type d'un triangle (Java, Python, C++)

**Description détaillée**:
Découvrez comment résoudre LeetCode 3024 – *Type de triangle* – en Java, Python et C++. Comprendre l'inégalité des triangles, compter l'unicité, et pourquoi cette question facile est un must-savoir pour coder les entrevues. Obtenez les meilleurs extraits de code, conseils de cas de bord et stratégies de préparation d'entrevue.

**Mots clés**:
LeetCode 3024, type de triangle, inégalité de triangle, équilatéral, isocèle, scalène, interview de codage, solution Java, solution Python, solution C++, algorithme facile, utilisation de set, questions d'entrevue

**Appel à l'action**:
Si vous êtes en préparation pour votre prochaine interview de codage, appuyez sur l'onglet « J'aime » et inscrivez-vous pour plus d'algorithmes. Laissez un commentaire avec le prochain problème de LeetCode que vous souhaitez que nous crack!

---

- Oui. 6. A emporter

- Gardez votre code **petit** et **readable**.
- Protégez-vous toujours contre les cas de edge** – en particulier l'inégalité triangle.
- Utilisez un **set** pour compter des valeurs uniques – il est à l'épreuve des balles.
- Rappelez-vous, pour n = 3, le temps et l'espace sont **O(1)**, donc la simplicité prime les tours de fantaisie.

Bon codage – et que vos personnes interrogées soient impressionnées par votre triangle-savvy!