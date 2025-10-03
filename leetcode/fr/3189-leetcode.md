---
titre: LeetCode 3189. Déplacements minimum pour obtenir un conseil d'administration pacifique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 3189 : *Le minimum se déplace pour obtenir un conseil d'administration pacifique*

> **Définition**
> Un tableau pacifique a exactement un rook dans chaque rangée ** et** chaque colonne d`un échiquier `n × n`.
>
> **Tâche**
> Compte tenu d'un tableau «rooks» où «rooks[i] = [xi, yi]» est la position actuelle de rook «i» (0-based indices), déplacer chaque rook une cellule verticalement ou horizontalement à la fois pour que le tableau devienne paisible.
> Retournez le nombre minimum de mouvements requis.
> **Constraints**
> * `1 ≤ n = longueur des prises ≤ 500`
> * `0 ≤ xi, yi ≤ n-1`
> * Il n'y a pas deux rooks qui partagent une cellule.
> * À aucun moment, deux tours peuvent occuper la même cellule.

---

- Oui. 2. Aperçu clé – Découper les lignes et les colonnes

Un rook se déplace **seulement** dans sa propre rangée ou sa propre colonne.
Si nous traitons la coordonnée de ligne et la coordonnée de colonne **indépendante**, le problème se réduit à deux problèmes 1-dimensionnels distincts:

1. **Alignement de la bande** – Mettre chaque tour dans une rangée distincte.
2. **Alignement des colonnes** – Mettre chaque prise dans une colonne distincte.

Parce que les lignes et les colonnes sont orthogonales, nous pouvons les résoudre l'une après l'autre ** sans jamais causer de collision**:
*Nous n'avons jamais besoin d'échanger deux tours dans la même ligne ou colonne – nous ne faisons que déplacer chaque tour vers sa ligne cible/colonne une étape à la fois. *

Dans une dimension, la stratégie optimale est évidente:
Trier les coordonnées et coupler la plus petite coordonnée avec la ligne 0, la plus petite suivante avec la ligne 1, ..., la plus grande avec la ligne `n‐1`.
Le nombre minimal d'étapes pour cette dimension est simplement la somme des différences absolues entre la coordonnée triée et son indice cible.

L'optimum global est la somme des deux optimums 1-dimensionnels, car les deux mouvements n'interfèrent pas.

---

- Oui. 3. Algorithme

Texte
1. Trier les prises par leur coordonnées de ligne (x).
2. Pour i = 0 ... n-1:
ligne Déplacement + = = rooks[i].x
3. Trier les prises par leur coordonnées de colonne (y).
4. Pour i = 0 ... n-1:
C'est la première fois que l'on s'en occupe.
5. Retour ligneMoves + colMoves
«» "

*Pourquoi ça marche toujours ? *
Après l'étape 2, chaque rangée de rooks est à une cible unique "i".
À l'étape 4, nous ne touchons que la coordonnée de la colonne, ne changeant plus jamais la ligne, de sorte que les lignes restent uniques.
De même, à l'étape 3, nous permutons seulement la coordonnée de la colonne, laissant intactes les lignes déjà fixées.
Ainsi, aucun deux tours n'entrent en collision, et nous sommes arrivés à un conseil pacifique dans les moindres mouvements possibles.

---

- Oui. 3. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Tri des lignes (en place)
Résumer les mouvements de rangée Autres
Tri des colonnes Autres
Nombre de mouvements de colonnes Autres
**Total**** Autres

Avec `n ≤ 500` cela satisfait facilement les limites de temps de LeetCode.

---

- Oui. 3. Mise en œuvre des références

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.

---

#### 3.1 Java (Java 17+)

"Java
Importation de java.util.*;
Importer java.util.stream.*;

solution de classe {
Int minMoves(int[][] rooks) {
int n = longueur des prises;

//
les tableaux.sort(rooks, Comparator.comparingInt(a -> a[0]);
ligne intMoves = IntStream.range(0, n)
.map(i -> Math.abs(rooks[i][0] - i))
.sum();

// 2/
les tableaux.sort(rooks, Comparator.comparingInt(a -> a[1]);
int colMoves = IntStream.range(0, n)
.map(i -> Math.abs(rooks[i ][1] - i))
.sum();

retour ligneMoves + colMoves;
}
}
«» "

---

3.2 Python 3

'`python
Solution de classe:
def minMoves(self, rooks: List[List[int]]) -> Int:
n = len(rooks)

# Alignement des lignes
rooks.sort(key=lambda r: r[0])
range_moves = somme(abs(r[0] - i) pour i, r dans le dénombrement(rooks))

# Alignement des colonnes
rooks.sort(key=lambda r: r[1])
col_moves = somme(abs(r[1] - i) pour i, r dans le dénombrement(rooks))

Return row_moves + col_moves
«» "

---

### 3.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minMoves(vecteur<vecteur<int>>& rooks) {
int n = rooks.size();

// Alignement des lignes
(rooks.begin(), rooks.end(),
[](const auto& a, const auto& b){ retourner a[0] < b[0]; });
ligne intMoves = 0;
pour (int i = 0; i < n; ++i)
rowMoves += abs(rooks[i][0] - i);

// Alignement de la colonne
(rooks.begin(), rooks.end(),
[](const auto& a, const auto& b) { retourner a[1] < b[1]; });
int colMoves = 0;
pour (int i = 0; i < n; ++i)
colMoves += abs(rooks[i ][1] - i);

retour ligneMoves + colMoves;
}
};
«» "

Les trois extraits partagent le même espace d'exécution O(n log n) et O(1).

---

- Oui. 4. Pourquoi cette solution gagne votre entrevue

Point Pourquoi ça compte pour les intervieweurs
-- -- -- -- -- -- ----------------------------------
**Clarté**Vous divisez immédiatement le problème en deux problèmes 1-D indépendants – un modèle que les intervieweurs aiment. Autres
**Proof d'optimalité**La méthode triée est probablement optimale dans une dimension (ce n'est que le problème du déplacement total minimum de . Autres
**Sécurité de l'appareillage** Autres
**Complexité** Autres
Autres **Taille du code**= Moins de 50 lignes dans chaque langue – propre et durable. Autres

Les bons
* **Décomposition élégante** – la résolution des lignes et des colonnes séparément est une stratégie classique qui s'adapte aux grandes planches.
* **Code de qualité à lire** – chaque ligne fait exactement une chose.

- Oui. Les mauvais
* ** Garantie de collision implicite** – les novices pourraient s'inquiéter de se croiser. Le découplage des coordonnées garantit que cela n'arrive jamais, mais l'explication est parfois omise dans les solutions de copie-collage.

- Oui. L'Ugly
* ** Hypothèse fondée sur le code 0** – si le tableau était basé sur 1 vous auriez besoin d'ajuster les indices cibles.
* **Missing test‐suite** – De nombreuses solutions de collage n'incluent pas un exemple de cas de test, ce qui est gênant pour les intervieweurs qui veulent voir votre solution en action.

---

- Oui. 5. Exemple d ' entrée/sortie

Produit escompté
-- -- -- -- -- -- -- --
[[0,0],[0,1],[1,0],[1,1]
[[2,1],[0,0],[1,3],[3,2]
[[0,2],[2,0],[1,1],[3,3]"

*Test rapide de santé mentale en Python*

'`python
s = Solution()
[[0,0],[0,1],[1,0],[1,1]]]] # 2
print(s.minMoves([[2,1],[0,00],[1,3],[3,2]) # 4
«» "

---

- Oui. 6. Pseudocode (agnostique de la langue)

«» "
fonction minMoves(rooks):
n = longueur(s)

Étape de la ligne
Tri(rooks par x)
rangMoves = 0
pour i de 0 à n-1:
rowMoves += abs(rooks[i].x - i)

# Étape de la colonne
Tri(rooks par y)
colMoves = 0
pour i de 0 à n-1:
ColMoves += abs(rooks[i].y - i)

retour ligneMoves + colMoves
«» "

---

- Oui. 7. Le blog SEO-Optimized

> **Titre:** *Master LeetCode 3189 – Déplacements minimum pour obtenir un conseil d'administration pacifique (Rook Puzzle) – Guide complet pour les entrevues de codage*

> **Meta Description:** Apprenez à résoudre le LeetCode 3189 .Le minimum se déplace pour obtenir un tableau pacifique avec un algorithme rapide O(n log n). Obtenez des solutions pas à pas Java, Python et C++, ainsi que des conseils d'entrevue et une préparation d'entrevue de codage.

---

7.1 Introduction

Lorsque vous touchez le problème LeetCode **3189 – Déplacement minimum pour obtenir un conseil d'administration pacifique**, vous regardez un classique *rook puzzle*. Il se sent comme un Rubiks cube mais en 2-D, et de nombreux candidats sous-estiment sa solution faussement simple. Dans ce post, nous allons marcher à travers l'algorithme, afficher le code propre en Java, Python, et C++, et discuter de ce qui rend cette approche *bonne*, *mauvaise* et *meilleure*. À la fin, vous serez prêt à répondre à cette question dans une entrevue technique ou sur la plateforme de recherche d'emploi.

---

7.2 Aperçu du problème

- **Peaceful board**: une prise par ligne et colonne.
- **Coût de déplacement**: une cellule par déplacement, déplacements orthogonaux seulement.
- **Objectif**: minimiser les déplacements totaux.

---

### 7.3 Le bien – Découpler le problème

> **Pourquoi ça marche* *
> Chaque ligne et chaque colonne de rooks évoluent indépendamment.
> Trier les lignes et les aligner sur `[0...n‐1]` donne le coût minimum *row*.
> La répétition pour les colonnes donne le coût minimum *colonne*.

- **Optimalité**: En 1-D, déplacement minimal = somme de `=trié[i] - i=‘.
- **Sécurité** : Les lignes sont fixées avant les colonnes; aucune collision.
- **Time**: `O(n log n)` dominé par le tri.

---

### 7.4 The Bad-Surveillance des collisions

De nombreuses solutions copy-colle prétendent : -Le tri aligne les coordonnées. Sans expliquer la sécurité *collision*, les intervieweurs peuvent penser que vous ignorez un bug subtil.
**Solution:**
Expliquez qu'après le tri des lignes, chaque rook est dans une ligne cible distincte; la colonne ne touche plus jamais les lignes.
Cela garantit qu'aucun rook ne traversera jamais une autre, satisfaisant à l'exigence de la collision de l'un ou l'autre.

---

#### 7.5 Le "Ugly" – Pourquoi certains codes font défaut

- ** Hypothèses codées en caractères gras**:
Certains postes supposent une indexation basée sur 0 ou ignorent les limites du conseil.
- **Lac de tests d'exemple**:
Les candidats présentent souvent un code sans harnais d'essai, laissant les intervieweurs deviner l'exactitude.
- **Solutions longues et verbeuses**:
L'ajout de boucles inutiles ou de tableaux auxiliaires gonfle le code et masque la logique.

---

7.6 Captures de code propres

**Java**

"Java
les tableaux.sort(rooks, Comparator.comparingInt(a -> a[0]);
ligne intMoves = IntStream.range(0, n)
.map(i -> Math.abs(rooks[i][0] - i))
.sum();
«» "

**Python**

'`python
rooks.sort(key=lambda r: r[0])
range_moves = somme(abs(r[0] - i) pour i, r dans le dénombrement(rooks))
«» "

**C++**

'`cpp
tri(rooks.begin(), rooks.end(), [](const auto& a, const auto& b){ retourner a[0] < b[0]; });
ligne intMoves = 0;
pour (int i = 0; i < n; ++i) ligneMoves += abs[i][0] - i;
«» "

Ces trois extraits illustrent la même logique concise, adaptée à la syntaxe de chaque langue.

---

7.7 Comment expliquer Dans une interview

1. **Énoncer la décomposition**: Nous traitons les lignes et les colonnes séparément. (en milliers de dollars)
2. **Afficher le raisonnement 1-D optimal**: le tri et l'appariement à `[0...n‐1]' minimisent le déplacement total. (en milliers de dollars)
3. **Sécurité contre les collisions** : Après que les lignes sont fixes, les colonnes ne touchent plus jamais les lignes, donc elles restent distinctes. (en milliers de dollars)

Soyez prêt pour les questions de suivi : *Et si le tableau était basé sur 1 ?* – ajustez simplement les indices cibles à « i+1 ».
*Peut-on croiser deux tours?* – Non, car les coordonnées orthogonales sont permutées indépendamment.

---

7.8 Liste de contrôle pour la préparation de l'entrevue

Objet
- Oui.
Comprendre l'astuce de découplage tôt. Autres
Coder dans votre langue préférée. Autres
Expliquez la preuve d'optimalité en 1‐D. Autres
Fournir un exemple de test rapide. Autres
Soyez prêt à discuter de complexités temporelles et spatiales. Autres

---

### 7.9 A emporter et autres pratiques

- **Reconnaissance des brevets**: Cette décomposition apparaît dans de nombreux problèmes de déplacement de grille (p. ex. distance minimale de Manhattan pour aligner les points).
- **Entretien de codage**: Utilisez cette solution comme démarreur pour tout puzzle *rook* ou *grid*.
- **Recherche d'emploi**: Mettre en évidence la complexité O(n log n) et le code propre dans votre CV ou portfolio.

---

7.10 Pensées finales

LeetCode 3189 peut sembler une question astucieuse, mais avec le bon aperçu il se transforme en un exemple de manuel de *diviser et conquérir dans les dimensions orthogonales*. Les solutions Java, Python et C++ ci-dessus capturent le cœur du problème en quelques lignes, prouvant que l'élégance peut être à la fois rapide et infaillible. La prochaine fois que vous verrez un puzzle rook, rappelez-vous : **sort, align, sum, recommend** – et vous partirez toujours avec une réponse parfaite.

---

### 7.11 Références et ressources

- Problème de LeetCode 3189: https://leetcode.com/problèmes/minimum-moves-to-get-a-peaceful-board/
- Pensée algorithmique – Stanford CS221 Conférence sur la décomposition.
- L'article GeeksforGeeks sur le déplacement minimal.

---

**Codage heureux, et bonne chance pour votre prochaine interview! * *

---

> * Prêt à résoudre d'autres casse-tête ? Abonnez-vous à notre bulletin d'information pour connaître le problème d'entrevue hebdomadaire. *

---

Ceci conclut le guide complet. N'hésitez pas à adapter les extraits à votre propre style ou à les étendre avec des tests unitaires – la perspicacité du cœur reste la même. Joyeux entretien !