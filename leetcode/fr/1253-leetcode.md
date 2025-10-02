---
Titre: LeetCode 1253. Reconstruire une matrice binaire 2-Row -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Remise en état des problèmes
**Reconstruire une matrice binaire de 2 lignes**

Données

* `upper` – la somme requise de la première ligne (0ème)
* `inférieure` – la somme requise de la deuxième ligne (1er)
* "colsum[]" – un tableau de longueur *n* où
* `colsum[i]` peut être `0`, `1` ou `2`
* il représente le nombre total de `1`s qui doivent apparaître dans la colonne *i* de la matrice 2 rangs finale

Retourne toute matrice binaire à 2 rangées `mat` qui satisfait à tout ce qui précède, ou une matrice vide si elle est impossible.



-----------------------------------------------------------------------------------

- Oui. 2. L'intuition et l'idée de l'avidité

* ** 'colsum[i] == Annexe
Les deux lignes doivent contenir un `1`. Cela consomme un `1` de `upper` ** et** un dans la section inférieure.

* ** 'colsum[i] == 0'**
Les deux lignes contiennent un `0`. Aucun quota n'est utilisé.

* ** 'colsum[i] == 1'**
Une des deux lignes doit contenir un `1`. Quelle que soit la ligne qui a encore le quota restant est choisi avec cupidité - il n'importe pas quelle ligne reçoit le `1` aussi longtemps que les quotas totaux sont respectés.

Le choix avide est sûr parce que les seules colonnes qui **force** un placement sont ceux avec `2`.
Une fois que toutes ces colonnes sont fixées, les colonnes `1` restantes sont libres de l'action – toute allocation qui utilise exactement les comptes `upper` et `lower` restants est valide.

-----------------------------------------------------------------------------------

- Oui. 3. Algorithme

«» "
1. Let m = colsum.longueur
2. Si somme (colsum) != supérieur + inférieur → impossible → retour []

3. Comptez le nombre de 2s en colsum, que ce soit deux
Si deux > supérieur ou deux > inférieur → impossible → retourner []

4. Créer la matrice de résultats res[2][m] initialisée avec 0

5. Premier passage : pour chaque i avec colsum[i] 2
res[0][i] = res[1][i] = 1
supérieur-- ; inférieur--

6. Deuxième passe : pour chaque i avec colsum[i] == 1
si supérieur > 0:
res[0]i] = 1 ; supérieur--
Sinon:
res[1][i] = 1 ; inférieur--

7. Retour rés
«» "

-----------------------------------------------------------------------------------

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie une matrice valide s'il existe, et renvoie `[]` sinon.

---

Lemma 1
Si `sum(colsum) != upper + lower`, il n'existe aucune matrice valide.

**Prof.**
Le nombre total de `1`s dans la matrice est égal
`sum(colsum)` (par définition des montants de la colonne) et égale également
`upper + lower` (par définition des montants en rangée).
S'ils diffèrent, les deux égaux ne peuvent pas tenir simultanément. *



Lemma 2
Si le nombre de colonnes `2` ('deux`) est supérieur ou inférieur, il n'existe pas de matrice valide.

**Prof.**
Chaque colonne `2` nécessite un `1` dans les deux lignes *.
Ainsi, chacune de ces colonnes consomme une unité du quota de *deux* lignes.
Si « deux » est plus grand que le quota d'une ligne, cette ligne aurait besoin de plus que « supérieur » (ou « inférieur ») C'est impossible. *



Lemma 3
Après la première passe, les valeurs restantes de `upper` et `inférieure` correspondent au nombre exact de `1`s qui doivent encore être placés dans les lignes correspondantes.

**Prof.**
Chaque colonne `2` a été remplie de deux colonnes `1`, une par rangée, et `upper` et `inférieure` ont été décrémentées en conséquence.
Aucun autre `1` n'a encore été placé, de sorte que les nouvelles valeurs représentent le quota restant. *



Lemma 4
Le deuxième passe place exactement les colonnes `1' restantes d'une manière qui satisfait les quotas restants.

**Prof.**
Chaque colonne `1` a besoin d'un seul `1'.
L'algorithme le place dans la rangée supérieure alors que `upper > 0`.
Si `upper` est déjà épuisé, il doit être placé dans la rangée inférieure, et par Lemma 3 `inférieur > 0 ' tient à ce moment.
Ainsi, chaque colonne `1` est assignée à une ligne qui a encore des quotas disponibles, et après le passage `upper` et `inférieur` deviennent `0`. *



- Oui. Théorème
L'algorithme renvoie une matrice qui satisfait toutes les contraintes si une telle matrice existe.

**Prof.**

*Si l'algorithme retourne une matrice*:
Par Lemma 1 et 2, il ne retourne jamais une matrice lorsque les contraintes sont insatisfaites.
Lorsqu'il procède, Lemmas 3 et 4 garantissent qu'après les deux passe chaque somme de colonne est respectée et que les deux sommes de ligne sont égales à l'original `upper` et `low'.
La matrice est donc valide.

*Si une matrice valide existe :
Toutes les conditions nécessaires de Lemmas 1 et 2 doivent être maintenues, sinon aucune matrice ne pourrait exister.
Ainsi, l'algorithme ne rejette jamais une instance réalisable tôt.
Avec les conditions satisfaites, l'affectation gourmande dans le second passage est toujours possible (Lemma 4), donc l'algorithme produit une matrice. *



-----------------------------------------------------------------------------------

- Oui. 5. Analyse de la complexité

*Let `n = colsum.longueur`.*

* Heure:
* Somme et nombre: `O(n)`
* Deux passes sur le tableau: `O(n)`
* **Total** "O(n)".

* Espace:
* matrice de résultats `2 × n`: `O(n)`.
* Variables auxiliaires: `O(1)`.

-----------------------------------------------------------------------------------

- Oui. 6. Mise en œuvre des références

Voici des implémentations idiomatiques propres dans **Java**, **Python** et **C++**.

---

#### 6.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
Liste publique<Liste<entier>> reconstruireMatrix(int supérieur, int inférieur, int[] colsum) {
int n = longueur colsum.;
= 0;
int twos = 0;
pour (int v : colsum) {
total += v;
si (v) 2) deux ++;
}
if (total != supérieur + inférieur)
retourner la nouvelle grille <>(); // matrice vide
}

int[][] res = nouveau int[2][n];

// Premier passage – colonnes avec 2
pour (int i = 0; i < n; i++) {
si (colsum[i]) 2) {
res[0]i] = 1;
res[1][i] = 1;
supérieur--;
inférieure--;
}
}

// Deuxième passage – colonnes avec 1
pour (int i = 0; i < n; i++) {
si (colsum[i]) 1) {
si (plus haut > 0) {
res[0]i] = 1;
supérieur--;
} autre {
res[1][i] = 1;
inférieure--;
}
}
}

Liste<Liste<entier>> réponse = nouvelle liste de distribution<>();
réponse.add(toList(res[0]);
add(toList(res[1]));
réponse de retour;
}

liste privée <integer> toList(int[] arr) {
Liste<entier> liste = nouvelle liste d'array<>(longueur arr.);
pour (int v : arr) list.add(v);
liste de retour;
}
}
«» "

---

#### 6.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def reconstruction Matrix (soi-même, supérieur: int, inférieur: int,
colsum: Liste[int]) -> Liste[Liste[int]]:

n = len(colsum)
total = somme (colsum)
twos = colsum.count(2)

si total != supérieur + inférieur ou deux > ou deux > inférieur:
retour []

# initialiser la matrice 2 rangs avec des zéros
res = [[0] * n pour _ dans l'intervalle(2)]

# premier passage – colonnes avec 2
pour i, v dans l'énumération (colsum):
Si v == 2:
res[0]i] = 1
res[1][i] = 1
supérieur -= 1
inférieur -= 1

# deuxième passe – colonnes avec 1
pour i, v dans l'énumération (colsum):
Si v == 1:
si supérieur > 0:
res[0]i] = 1
supérieur -= 1
Sinon:
res[1][i] = 1
inférieur -= 1

retour res
«» "

---

*### 6.3 C++17

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<vector<int>> reconstruireMatrix(int supérieur, int inférieur, vectorielle<int>& colsum) {
int n = colsum.size();
= 0, deux = 0;
pour (int v : colsum) {
total += v;
si (v) 2) + deux;
}
if (total != supérieur + inférieur)
retour {}; // matrice vide

vecteur<vector<int>> res(2, vecteur<int>(n, 0));

// colonnes qui doivent contenir deux 1
pour (int i = 0; i < n; ++i)
si (colsum[i]) 2) {
res[0]i] = res[1][i] = 1;
--en haut; --en bas;
}

// colonnes contenant exactement 1
pour (int i = 0; i < n; ++i)
si (colsum[i]) 1) {
si (plus haut > 0) {
res[0]i] = 1;
--en haut;
} autre {
res[1][i] = 1;
--inférieur;
}
}

retour rés;
}
};
«» "

-----------------------------------------------------------------------------------

- Oui. 7. SEO-Optimized Blog Post – Comment faire un entretien sur les structures de données *et* Land Your Next Tech Job

> **Mots-clés** – *reconstruire une matrice binaire de 2 lignes*, *Code de leet 1739*, *algorithme d'entrevue d'emploi*, *algorithme d'entrevue d'emploi*, *interview de codage de Java Python C++*, *conseils d'entrevue d'ingénieur en logiciel*, *structures de données questions d'entrevue*, *pensée algorithmique*, *tendances d'embauche technologique*

---

#### 7.1 Titre et méta-Description

Contenu de l'élément
C'est pas vrai.
**Titre** (Java, Python, C++) Autres
**Meta‐Description**=Maître le LeetCode==Reconstruire un problème de 2-Row Binary Matrix==. Algorithme cupide, preuve, complexité et solutions Java, Python, C++ propres. Parfait pour la préparation de l'entrevue avec un ingénieur logiciel. Autres

---

Présentation

> *Les questions relatives à la structure des données et à l'algorithme sont la pierre angulaire de chaque entrevue sur l'ingénierie logicielle. L'un des modèles les plus fréquemment demandés consiste à reconstruire une matrice à partir de la somme des rangées et des colonnes – un problème trompeurment simple mais étonnamment délicat. Dans cet article, nous parcourons le défi de 2-Row Binary Matrix. *

---

7.3 Pourquoi ce problème est important dans les entrevues

1. ** Démontre la compréhension du comptage de base** – Vous devez suivre simultanément les montants des lignes et des colonnes.
2. **Faits saillants Greedy Decision-Making** – Choisir où placer un `1` dans des colonnes libres est un piège cupide classique; la résoudre montre correctement la maturité algorithmique.
3. **Shows Edge‐Case Rigor** – Le rejet précoce d'entrées impossibles teste votre capacité à repérer les conditions nécessaires avant de faire un travail lourd.
4. **Scales à travers les langues** – Une solution solide dans trois langues populaires prouve la pensée linguistique-agnostique – un atout précieux pour les postes complets ou systèmes.

---

7.4 Algorithme pas à pas (en anglais clair)

1. **Frais de validation* *
* Le nombre total de «1» doit correspondre à la somme des quotas de deux lignes.
* Chaque colonne avec "2" force un placement; son nombre ne peut dépasser aucun quota.

2. ** Colonnes forcées à remplir** ('colsum[i] == 2`) – les deux lignes obtiennent `1`, et nous réduisons les deux quotas.

3. **Allocate -Gratuit** Colonnes** (`colsum[i] == 1`) – mettre avidement le `1` dans la rangée qui en a encore besoin. Après ce passage, les deux quotas atteignent zéro.

4. **Retourner la matrice** ou une liste vide si une vérification a échoué.

---

### 7.5 Aperçu du code

Informations clés sur la mise en œuvre
- C'est quoi ?
**Java**=Utilisez `List<List<Integer>>=` pour correspondre au type de retour de LeetCode==; helper `toList()` pour la lisibilité. Autres
**Python**=List-comprehensions pour la création de matrices concises; retour précoce sur impossibilité. Autres
**C++**=2-dimensionnel `vector<vector<int>>`; sortie précoce avec `{}`. Autres

---

7.6 Complexité et performance

* **Heure** – `O(n)` où *n* est le nombre de colonnes.
* **Espace** – "O(n)" pour la matrice résultante.

Ces limites serrées sont optimales; aucun algorithme ne peut être asymptotiquement meilleur parce que nous devons inspecter chaque colonne au moins une fois.

---

# ### 7.7 Surmonter Liste de contrôle des cas

Scénario Résultat prévu
-- -- -- -- -- -- -- --
= supérieur + inférieur
Trop de colonnes `2`
Autres Toutes les colonnes sont la matrice `0`=0 de tous les zéros
Autres Toutes les colonnes sont `2` et `upper == plus bas ==

---

7.8 Dernier départ

*L'algorithme cupide ci-dessus est **probablement correct** et fonctionne dans le temps linéaire.
La mettre en œuvre dans plusieurs langues démontre à la fois la pensée algorithmique et l'artisanat spécifique à la langue – exactement le genre de compétences que recherchent les recruteurs. *

---

- Oui. 8. Comment ce blog stimule votre carrière de technicien

Le bénéfice de l'article aide
- Oui.
**Reconstruire une matrice binaire de 2-Row, solution LeetCode 1739, solution Java Python C++, apparaît naturellement tout au long du post, ce qui le rend décelable lorsque des recruteurs ou des gestionnaires d'embauche recherchent des problèmes d'entrevue communs. Autres
**Showcases Problem-Solving Skills**L'article passe par la preuve, la complexité et la manipulation de cas de bord – signe aux recruteurs que vous pouvez raisonner rigoureusement sur les algorithmes. Autres
** Démontrer une expertise multilingue** En fournissant des solutions claires et idiomatiques dans trois langues principales, vous illustrez la capacité d'adaptation à une pile technologique de l'entreprise. Autres
Autres **Ajout de la valeur à votre portfolio**=Vous pouvez intégrer les extraits de code dans votre site Web personnel ou GitHub README, et l'explication sert de référence rapide pour les prochaines entrevues. Autres
**Engages Recruters with Structured Content**L'utilisation de tableaux, de listes de puces et de blocs de code correspond au format que les recruteurs apprécient lorsqu'ils écument des blogs ou des profils techniques. Autres

** Prendre des mesures :**
* Poster cet article sur Medium, Dev.to, ou votre blog personnel. *
*Ajouter un lien vers votre dépôt GitHub qui contient les fichiers de la solution complète. *
*L'utiliser comme un point de discussion dans les prochaines entrevues – expliquer l'intuition, marcher à travers la preuve, et présenter les implémentations propres. *

Joyeux codage – et heureux entretien! C'est ce qu'il a dit