---
titre: LeetCode 2387. Médiane d'une matrice triée par les sages de la ligne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème
**LeetCode 2387 – Médiane d'une matrice triée en rangée* *
> *Avec une matrice `m × n` (`m` et `n` sont tous les deux impairs) où chaque ligne est triée en ordre non décroissant, retourner la médiane de tous les éléments `m·n`. *

> **Objectif** – trouver la médiane dans **O(m·log n · log V)** time, où `V` est l'intervalle des valeurs (= 106), c'est-à-dire bien mieux que la naïve `O(m·n)` scan.

---

- Oui. 2. Pourquoi une recherche binaire sur l'espace *valeur*?
* Chaque ligne est triée → nous pouvons compter - combien de nombres sont ≤ X-- dans O(log n) avec recherche binaire.
* La médiane est le plus petit nombre `X` de telle sorte qu'au moins la moitié des éléments soit ≤X.
* Si nous pouvons rapidement répondre à -Combien d'éléments ≤ X?- Nous pouvons faire une recherche binaire sur l'espace *value* (du minimum global au maximum global).

Cette stratégie est la recherche classique *binaire sur la réponse*.

---

- Oui. 3. Algorithme (haut niveau)

1. **Déterminer les limites de la recherche* *
* `low` = plus petit élément de la matrice (premier élément de chaque ligne).
* `high` = élément le plus important de la matrice (dernier élément de chaque ligne).

2. **Recherche binaire sur les valeurs**
Alors que `faible < élevé`:
* `milieu = (faible + élevé) / 2`
* `cnt = ↓ countRow(row, mi)` – nombre d'éléments dans la matrice ≤ milieu.
* Si `cnt < (m·n + 1)/2` → médiane est **large** → set `low = milieu + 1`.
* Autrement → médiane est **.

3. Retour `faible` (ou `élevée`) – la médiane.

**countRow(row, mi)** est une recherche binaire standard (`upper_bound`) retournant le premier indice où l'élément > mi. L'indice retourné correspond au nombre d'éléments ≤ milieu de cette ligne.

---

- Oui. 4. Preuve d ' exactitude

On prouve que l'algorithme renvoie la vraie médiane.

Lemma 1
Pour tout entier `x`, `cnt(x) = ↓_i upper_bound(row_i, x)` est égal au nombre d'éléments de matrice ≤ x.

*Proof. *
Parce que chaque ligne est triée, `upper_bound` retourne l'index du premier élément strictement supérieur à `x`. Tous les éléments avant cet indice sont ≤ x. Le cumul entre les lignes compte tous les éléments de la matrice ≤ x.

Lemma 2
Let `k = (m·n + 1)/2` (la position de la médiane dans l'ordre trié).
Si `cnt(mid) < k`, la médiane > au milieu; si `cnt(mid) ≥ k`, la médiane ≤ au milieu.

*Proof. *
`cnt(mid)` compte le nombre d'éléments ≤ milieu.
* Si moins d'éléments `k` sont ≤ mi, alors l'élément `k`-th (la médiane) doit être plus grand que `mid`.
* Si au moins les éléments `k` sont ≤ mi, alors l'élément `k`-th ne peut pas être plus grand que `mid`.

Lemma 3
Pendant la recherche binaire l'invariant
`faible` est toujours ≤ médiane et `élevée` est toujours ≥ médiane.

*Profil par induction. *
*Base*: Initialement, `faible` est le minimum mondial et `élevé` le maximum mondial; la médiane se situe entre.
*Étape* :
- Si `cnt(mid) < k` → par Lemma 2 médiane > mi → nous définissons `low = mi+1`. Étant donné que le « milieu < médian », le « faible » reste ≤ médian.
- Autres (`cnt(mid) ≥ k`) → médiane ≤ milieu → nous définissons `haut = milieu`. Étant donné que le « milieu ≥ médiane », le « haut » demeure ≥ médiane.

- Oui. Théorème
Lorsque la boucle se termine ("low == high`), la valeur retournée est égale à la médiane de la matrice.

*Proof. *
Par Lemma 3, l'intervalle de recherche contient toujours la médiane. La résiliation n'est possible que lorsque l'intervalle se réduit à une seule valeur. Cette valeur unique doit être la médiane car aucune valeur plus petite ne peut satisfaire à la condition médiane (`cnt < k`) et aucune valeur plus grande ne peut satisfaire `cnt ≥ k`. *

---

- Oui. 5. Analyse de la complexité

*Que `m` soit le nombre de lignes, `n` le nombre de colonnes. *

Étape Opération Temps
C'est pas vrai.
Rechercher `low`/`high`=Scanner les premiers et derniers éléments de chaque ligne="O(m)` Autres
Pour chaque ligne de `m`, effectuer `upper_bound` (`O(log n)`)" Autres
Nombre d'itérations où «intervalle ≤ 106» → ≤ 20 (= log2(106))

Durée totale: `O(m·log n·log V)` -"O(m·log n)` pour les contraintes données.
Espace: `O(1)` – seulement quelques variables entières.

---

- Oui. 6. Mise en œuvre des références

Ci-dessous vous trouverez **ready‐to-copy** code dans **Java, Python, et C++**. Chaque mise en œuvre suit l'algorithme décrit ci-dessus et contient des commentaires en ligne pour plus de clarté.

#### 6.1 Java (compatible avec le code Leet)

"Java
Importation de java.util.*;

solution de classe {
matrice d'entrée publiqueMedien(int[][]) {
int m = longueur de grille, n = longueur de grille[0];

// 1. Trouver global min et max
int low = entier. MAX_VALEUR;
int high = entier.MIN_VALUE;
pour (int[] ligne : grille) {
low = Math.min(faible, rang[0]); // premier élément d'une ligne triée
haute = Math.max(haut, rang[n - 1]); // dernier élément
}

int cible = (m * n + 1) / 2; // k-th élément dans l'ordre trié

// 2. Recherche binaire sur la plage de valeurs
pendant que (faible < haut) {
int milieu = faible + (élevé - faible) / 2;

nombre int = 0;
pour (int[] ligne : grille) {
nombre += supérieurBound(ligne, milieu); // #éléments ≤ milieu de cette ligne
}

si (compte < cible) {
faible = milieu + 1; // médiane est plus grande
} autre {
élevé = milieu; // médiane est ≤ milieu
}
}
retour bas; // bas == haut
}

/** retourne le premier indice > cible (c'est-à-dire le nombre d'éléments ≤ cible) */
Int privé supérieurBound(int[] arr, int cible) {
int lo = 0, hi = arr.longueur; // hi est exclusif
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (arr[mid] <= cible) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}
}
«» "

---

6.2 Python

'`python
de bisect import bisect_right
de taper l'importation Liste

Solution de classe:
def matrixMedian(self, grid: List[List[int]]) -> Int:
m, n = len(grid), len(grid[0])

# limites mondiales
low = min(row[0] pour la ligne de la grille)
haute = max(row[-1] pour la ligne de la grille)

cible = (m * n + 1) // 2

alors que faible < élevé:
milieu = (faible + élevé) // 2
count = sum(bisect_right(row, mi) pour la ligne de la grille)

si le nombre < cible:
faible = milieu + 1
Sinon:
haute = moyenne

retour faible
«» "

---

*### 6.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
matrice intMedien(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();

Int low = INT_MAX, high = INT_MIN;
pour (const auto & ligne : grille) {
faible = min(faible, rang.front());
haute = max(élevé, rang.back());
}

cible int = (m * n + 1) / 2;

pendant que (faible < haut) {
int milieu = faible + (élevé - faible) / 2;
nombre int = 0;
pour (const auto & ligne : grille) {
nombre += upper_bound(row.begin(), rang.end(), milieu - rang.begin();
}

si (compte < cible) faible = milieu + 1;
Autre haut = milieu;
}
retour faible;
}
};
«» "

---

- Oui. 7. Billet de blog – *=Le bon, le mauvais et l'acharnement de trouver le médiateur dans une matrice triée en rangée

#### 7.1 Pourquoi ce problème compte (mots-clés du référencement : *entrevue d'algorithme, recherche binaire, matrice médiane, entrevue de codage, LeetCode 2387*)

Quand les recruteurs demandent comment trouver la médiane d'une matrice triée ? Ils testent vraiment trois compétences de base:

1. **La pensée algorithmique** – Pouvez-vous repérer l'opportunité de recherche binaire sur *valeurs* au lieu d'indices?
2. ** Sensibilisation à la complexité** – Connaissez-vous les compromis temps/espace entre le tri et la recherche?
3. **Mise en oeuvre Compétence** – Pouvez-vous traduire une idée concise en code prêt à la production?

Une réponse bien faite à ce problème démontre les trois et vous rapporte des points de brownie lors de votre prochaine entrevue sur la structure des données.

---

#### 7.2 Le bon – Ce qui fait de ce problème une mine d'or

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Row-wise trié**= Permet *log‐n* de rechercher chaque ligne. Autres
**Dimensions approximatives** Autres
Autres ** Petite plage de valeurs (= 106)** Active la recherche binaire sur la plage de valeurs dans un nombre constant d'itérations. Autres
**Évoluable**= Fonctionne pour 500×500 matrices (250k éléments) en moins d'une milliseconde. Autres
**Réutilisable**La recherche binaire sur la réponse s'applique à de nombreuses questions d'entrevue (kth plus grand, tableau divisé, etc.). Autres

---

7.3 Les mauvaises – Pièges communs

Comment l'éviter
C'est-à-dire
**Utiliser le scan linéaire**=Le `O(m·n)` est trop lent; assurez-vous que vous n'importiez pas sur chaque élément lors du comptage. Autres
**Utiliser `mid = (faible + élevé) / 2` sans dispositif de protection contre les débordements**. Autres
**Diversité de la position médiane**. Les erreurs hors-par-un produisent de mauvaises réponses. Autres
**Ignorant que chaque ligne est triée**= Si vous essayez de fusionner les lignes naïvement, vous perdez le bénéfice `log n`. Autres
**Ne pas utiliser `upper_bound` correctement Il doit renvoyer le nombre d'éléments ≤ mi, pas < mi. Autres

---

7.4 Les horribles cas de bord qui vous emportent

Cas de bord Pourquoi il est difficile
- C'est quoi ?
**Toutes les lignes sont identiques.La recherche binaire fonctionne encore, mais de nombreuses valeurs `mid` donnent le même nombre. Aucun changement nécessaire – l'algorithme converge correctement. Autres
**Matrix avec une très petite portée (par exemple, tous les nombres sont 1)**La boucle fonctionne toujours ~20 fois mais trouve toujours la réponse rapidement. Autres Gardez le même `log V` lié. Autres
**Grands entiers proches de `int` max/min**. Utilisez `long long` (C++/Java) ou arithmétique sécuritaire (`(faible + élevé) >>> 1'). Autres
**Matrice non carrée (m)**= Les gens utilisent parfois par erreur `n` pour les deux dimensions. Calculer explicitement «cible = (m*n + 1)/2». Autres
**Les valeurs négatives**=La plage de valeur peut être négative; assurez-vous que la capture est faible et élevée. L'algorithme gère automatiquement les négatifs parce que la plage est définie par les premiers/derniers éléments. Autres

---

#### 7.5 Comment le faire dans votre entrevue

1. **Expliquer la recherche binaire sur l'idée de réponse*** avant d'écrire un code. Afficher l'invariant que l'intervalle de recherche contient toujours la médiane.
2. **Parcourez un petit exemple** sur le tableau blanc (par exemple, une matrice 3×3). Afficher comment `cnt(mid)` change et comment l'intervalle se rétrécit.
3. **Supprimer la mise en œuvre** (cochez l'une des solutions de référence ci-dessus). Mentionnez les fonctions clés (`upper_bound`, `bisect_right`) et pourquoi elles sont O(log n).
4. **Mentionner la complexité du temps/de l'espace** succinctement: "O(m·log n)", "O(1)".
5. **Ajouter une petite optimisation** – en Java/C++ vous pouvez pré-stocker les premiers et derniers éléments de chaque ligne pour éviter de scanner toute la ligne lors de la recherche des limites.

---

7.6 Pensée finale – Pourquoi maîtriser ceci vous donne un avantage concurrentiel

- **LeetCode Mastery**: Résoudre le LeetCode 2387 efficacement vous place dans le centile supérieur de problèmes de matrice.
- **Confiance d'entrevue** : Vous savez comment pivoter du tri naïf à une solution logarithmique.
- **Problem–Solving Reputation**: Les recruteurs se souviendront de votre élégante utilisation de la recherche binaire sur une gamme de valeurs – un modèle qu'ils se rappelleront dans les prochaines interviews.

---

### 7.7 Appel à l'action (Référencement : *préparation de l'entrevue de codage, algorithme médian, matrice de recherche binaire, conseils d'entrevue*)

> Voulez-vous voir comment cette solution s'empile contre l'approche «Merge‐K‐sorted‐arrays»? Plongez dans le dépôt **GitHub** relié ci-dessous, où chaque version de langue est livré avec un harnais de test et des mesures de performance.

**GitHub**: https://github.com/votrenom d'utilisateur/matrix-median-impl

---

- Oui. 8. Note de clôture

Maîtriser le problème médian en matrice est un *show-stopper* dans les entrevues techniques. Avec la stratégie **binary search on reply**, vous pouvez la résoudre dans le temps sub-quadratique et démontrer une compréhension profonde des modèles algorithmiques. Utilisez le code de référence ci-dessus pour pratiquer, comparer, puis expliquer clairement la solution à tout panel d'entrevues. Bonne chance !

---

*Soyez libres d'adapter le billet de blog à votre style ou d'ajouter des sections supplémentaires telles que Solutions alternatives (monceau, divisez-et-conquer) (si vous le souhaitez). Bon codage ! *

---

> *Si vous avez aimé ce post, envisagez de vous abonner à d'autres guides d'entrevue en algorithme, des tutoriels de codage et du contenu de préparation d'entrevue. *

---

**Fin de la documentation* *