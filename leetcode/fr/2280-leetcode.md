---
titre: LeetCode 2280. Lignes minimales pour représenter un graphique linéaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2280. Lignes minimales pour représenter un graphique linéaire
## Solution dans **Java**, **Python** et **C++** + Un article de blog pleinement optimisé pour le référencement

> Tu veux attraper ce problème de LeetCode et atterrir cette interview ?
> Lire la suite pour une plongée profonde dans les maths, l'algorithme, les pièges et comment écrire une solution propre et prête à la production en trois langues.

---

- Oui. 1. Récapitulation des problèmes (Code Leet 2280)

> **Don** une liste de points `stockPrices[i] = [dayi, pricei]` (jours distincts, ordre arbitraire).
> **Objectif:** Connectez des points consécutifs avec des lignes droites. **Retour** le nombre minimum de lignes droites requis pour représenter l'ensemble du graphique.

**Contrôles* *

- Oui.
-- -- -- -- -- --
1 ≤ stockPrix.longueur ≤ 105' Autres
Autres Tous les `dayi` sont distincts

Le défi consiste à détecter quand une série de points consécutifs se trouve sur la même ligne droite. Un changement de pente force une nouvelle ligne.

---

- Oui. 2. Approche de haut niveau

1. **Trier les points de jour (`x`).
2. Calculez le vecteur *différence* entre chaque paire consécutive :
`Δx = xi – xi−1`, `Δy = yi – yi−1`.
3. Deux segments consécutifs appartiennent à la même ligne iff
`Δx1 * Δy2] Δx2 * Δy1` (la multiplication croisée évite la division en point flottant).
4. Incrémenter un compteur chaque fois que l'égalité ci-dessus échoue.
5. Manipulation spéciale: besoin d'un seul point **0** lignes, besoin de deux points **1** ligne.

Complexité
- **Heure:** `O(n log n)` en raison du tri (`n ≤ 105').
- **Espace:** "O(1)" (hors tableau d'entrée).

---

- Oui. 3. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Chacun utilise l'arithmétique entier seulement, donc il est à l'abri des erreurs de précision.

---

#### 3.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public int minimumLines(int[][] stockPrix) {
int n = stockPrix.longueur;
si (n <= 1) retourner 0; // aucune ligne nécessaire
si (n == 2) retourner 1; // un segment

// 1. Tri par jour (coordonné x)
les tableaux.sort(stockPrix, a, b) -> Integer.compare(a[0], b[0]);

// 2. Éléments de pente initiaux
long dxPrev = stockPrix[1][0] - stockPrix[0][0];
long dyPrev = stockPrix[1][1] - stockPrix[0][1];

lignes int = 1; // au moins une ligne

// 3. Scanner le reste
pour (int i = 2; i < n; i++) {
long dxCurr = stockPrix[i] [0] - stockPrix[i - 1][0];
long dyCurr = stockPrix[i] [1] - stockPrix[i - 1][1];

// Multiplication croisée pour comparer les pentes
si (dxCurr * dyPrev != dxPrev * dyCurr) {
lines++; // pente changée → nouvelle ligne
}

// Préparez la prochaine itération
dxPrev = dxCurr;
dyPrev = dyCurr;
}

les lignes de retour;
}
}
«» "

> **Pourquoi ? **
> Les différences peuvent aller jusqu'à `109`, et leur produit jusqu'à `1018`, ce qui correspond à un entier de 64 bits signé.

---

3.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def minimum Lignes(même, stockPrix: Liste[Liste[int]]) -> Int:
n = len(stockPrix)
si n <= 1:
retour 0
si n] 2 :
retour 1

# Tri par jour
stockPrix.sort(key=lambda p: p[0])

# Composants initiaux de pente
dx_prev = stockPrix[1][0] - stockPrix[0][0]
dy_prev = stockPrix[1][1] - stockPrix[0][1]

ligne = 1

pour i dans la plage(2, n):
dx_curr = stockPrix[i] [0] - stockPrix[i - 1][0]
dy_curr = stockPrix[i] [1] - stockPrix[i - 1][1]

si dx_curr * dy_prev != Dx_prev * dy_curr:
lignes += 1

dx_prev, dy_prev = dx_curr, dy_curr

lignes de retour
«» "

---

### 3.3 C++

'`cpp
#incluez <algorithme>
#incluez <vecteur>

solution de classe {
public:
Int minimumLignes(std::vector<std::vector<int>>& stockPrix) {
int n = stockPrix.taille();
si (n <= 1) retourner 0;
si (n) 2) retour 1;

// Tri par jour
std::sort(stockPrix.degin(), stockPrix.end(),
[](const std::vector<int>& a, const std::vector<int>& b) {
retourner a[0] < b[0];
});

long dxPrev = stockPrix[1][0] - stockPrix[0][0];
long dyPrev = stockPrix[1][1] - stockPrix[0][1];

lignes int = 1;

pour (int i = 2; i < n; ++i) {
long long dxCurr = stockPrix[i] [0] - stockPrix[i - 1][0];
long dyCurr = stockPrix[i] [1] - stockPrix[i - 1][1];

si (dxCurr * dyPrev != dxPrev * dyCurr) {
+ + lignes; // changement de pente
}

dxPrev = dxCurr;
dyPrev = dyCurr;
}

les lignes de retour;
}
};
«» "

---

- Oui. 4. Billet de blog: Le bon, le mauvais, et le mauvais de lignes minimales pour représenter un graphique de ligne

> **Mots clés**: LeetCode 2280, Lignes minimales pour représenter une ligne Graphique, entretien par algorithme, solution Java, solution Python, solution C++, comparaison de pente, complexité temporelle, conseils d'entretien

---

4.1 Introduction

Lorsque vous préparez une interview d'ingénierie logicielle, vous allez rencontrer des problèmes qui vous demandent de **détecter la colinéarité** parmi les points—pensez aux problèmes classiques de coque -convexe ou d'intersection de ligne.
LeetCode 2280, **Lignes minimales pour représenter un graphique de ligne**, est un terrain de jeu parfait: vous êtes donné un ensemble de prix d'actions sur des jours distincts, et vous devez pointer la représentation droite la plus compacte.

Dans cet article, nous disséquerons les parties *bon*, *mauvais* et *puissante* de la résolution de ce défi, nous passerons par les maths, nous vous montrerons trois solutions polies et vous donnerons des astuces prêtes à l'entrevue.

---

#### 4.2 La bonne – Mathématiques directes

- **Égalité de la pente par la multiplication croisée**
`Δx1 * Δy2] Δx2 * Δy1`
Cela élimine complètement la division, en écartant les pièges flottants.
- **Trier par jour**
Une fois triés, les points sont garantis dans l'ordre chronologique, de sorte que les différences consécutives sont toujours significatives.
- **Scannage linéaire**
Après tri, un seul passage suffit pour compter les ruptures de ligne.

> *Résultat:* Un algorithme O(n log n) clair qui s'échelonne jusqu'à la taille d'entrée maximale de 100 000 points.

---

### 4.3 Les mauvaises – Pièges communs

Pourquoi ça arrive ?
- Oui.
**L'utilisation de la division à virgule flottante** Utilisez la multiplication croisée ou la rationalité de l'entier. Autres
**Ignorer le tri**=Les points peuvent être donnés sans tri; vous manquerez les changements de pente. Tri par jour d'abord. Autres
**Le débordement entier**= `Δx * Δy` peut dépasser 32 bits.= Utiliser 64 bits (`long`/`long`). Autres
**Cas d'Edge**= Point unique → 0 lignes, deux points → 1 ligne. Poignée séparément avant la boucle principale. Autres

---

### 4.4 La suringénierie et les choix sous-optimaux

- **BigDecimal en Java**
Certaines solutions utilisent `BigDecimal` pour calculer les gains. Bien que mathématiquement précis, il subit de lourds frais généraux ('O(n)' avec des facteurs constants élevés).
- **Différence répétée**
Computing pentes comme double et comparer l'égalité est risqué en raison des erreurs d'arrondi.
- **Ignorer le tri sur place**
Copier le tableau ou créer une nouvelle liste gaspille la mémoire.

> * À emporter :* Gardez l'algorithme en place. La complexité n'est pas seulement une question de grande‐ O mais aussi les frais généraux à temps constant.

---

4.5 Dérivation étape par étape

1. **Trier les points**:
«points.sort(key=lambda p: p[0]» (Java & C++: `std::sort` ou `Arrays.sort`).
2. ** Vecteur initial** :
`dx_prev = x2 – x1`, `dy_prev = y2 – y1`.
3. **Loop** sur `i = 3 ... n` (0-based indexing) et calculer les différences actuelles.
4. **Comparer** en utilisant la multiplication croisée.
5. **Incrément** le compteur lorsque le produit diffère.

C'est ça, pas de tableaux supplémentaires, pas de division, pas de comparaisons en points flottants.

---

4.5 Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Trier "O(n log n)" "O(1)" supplémentaire (en place). Autres
Analyse linéaire Autres
Total "O(n log n)" "O(1)" Autres

La mémoire-footprint est minimale – juste le tableau d'entrée – qui est idéal pour les entrevues.

---

### 4.6 Entretien– Conseils prêts

1. ** Expliquez les maths d'abord** – J'utiliserai la multiplication croisée pour ne jamais diviser. (en milliers de dollars)
2. **Talk à travers les caisses de bord** – Un point signifie aucune ligne; deux points sont une ligne. (en milliers de dollars)
3. **Débordement de Mention** – Comme les différences peuvent aller jusqu'à 109, je stocke les produits dans un entier 64 bits. (en milliers de dollars)
4. **Afficher votre code de sécurité** – Tout arithmétique est entier; aucune erreur de point flottant. (en milliers de dollars)
5. **Discussion des compromis entre l'espace-temps** – J'évite BigDecimal de garder l'autonomie rapide; l'approche croisée est O(n log n) et l'autonomie. (en milliers de dollars)

---

4.7 Optimiser davantage (si vous êtes un utilisateur de puissance)

Idée Quand ça aide
C'est pas vrai.
**Compilation d'un dictionnaire de pentes**.Si vous devez regrouper *tous* segments par pente, vous pouvez stocker des paires `(dx, dy)` dans un `HashMap`.
Sur une machine multicore, Javas `Arrays.parallelSort` ou C++s `std::sort` peut diviser le travail. Autres
**Traitement Radix**= Puisque `day` est ≤ 109, un tri radix de base-10^5 peut battre le tri par comparaison sur de grandes entrées.= Seulement si vous frappez TLE sur le tri. Autres

---

4.8 Liste de contrôle à emporter pour l'entrevue

- [ ] **Trier les points par jour** (O(n log n)).
- [ ] **Utilisez 64 bits entiers** pour les produits différents.
- [ ] **Comparer les pentes avec la multiplication croisée**.
- [ ] **Handle 1‐point & 2‐point cases de bord**.
- [ ] ** Expliquez clairement votre logique** à l'intervieweur.

---

4.9 Pensées finales

LeetCode 2280 est trompeurment simple : vous cousez un graphique avec le moins de lignes droites possible.
Le crux détecte un *changement de pente*, qui est un test de colinéarité classique.
En triant une fois, puis en marchant linéairement avec des maths entiers, vous pouvez fournir une solution ** propre, efficace** dans n'importe quelle langue.

**Afficher votre intervieweur que vous connaissez les maths, respecter les contraintes, et garder votre code maigre. **
Bonne chance—*vous acquerrez celui-ci!*

---

4.10 Références

Lien
C'est quoi, ça ?
LeetCode Official Problème (en anglais seulement) https://leetcode.com/problèmes/minimum-lines-to-represent-a-line-chart/ Autres
Trick de la multiplication croisée https://en.wikipedia.org/wiki/Collineer Autres
Java Triage & `Arrays.sort`" https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html Autres
Python `sort` et `key`" https://docs.python.org/3/howto/sorting.html Autres
C++ "std::sort" https://en.cppreference.com/w/cpp/algorithm/sort Autres

---

> ** Besoin de plus d'entrevue ? * *
> Abonnez-vous à des pannes d'algorithmes hebdomadaires, à des conseils d'entrevue et aux meilleurs parcours LeetCode. Bon codage !