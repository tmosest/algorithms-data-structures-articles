---
titre: LeetCode 546. Supprimer les boîtes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
(Code de la lettre 546) – Le bon, le mauvais et le mauvais
- Oui. Pourquoi maîtriser ce problème peut vous poser ce rôle d'ingénieur logiciel

> **Mots clés** – *Supprimer Boxes Leetcode 546, programmation dynamique, 3-D DP, Java, Python, C++, problème d'entrevue, interview de codage, conception d'algorithmes, préparation d'entrevue d'emploi*

---

Récapitulation des problèmes

> **Input**: `int[] boxes` – couleurs représentées par des entiers positifs.
> **Objectif**: Supprimer à plusieurs reprises un segment contigu de couleurs identiques de longueur `k` et gagner `k × k` points.
> **Retour** : Score total maximum possible jusqu'à ce qu'il ne reste plus de cases.

---

Intuition – Qu'est-ce qui rend ce problème difficile ?

- Une stratégie naïve d'avidité (p. ex., supprimer la plus longue manche en premier) est sous-optimale.
- Oui. L'ordre optimal des suppressions dépend des suppressions *future* qui peuvent fusionner des exécutions séparées de la même couleur.
- Oui. Vous devez garder une trace de ** combien de boîtes identiques que vous avez déjà sur le "right"** qui peut être fusionné plus tard.

Cela donne au problème sa caractéristique **3-dimensionnelle DP**.

---

C'est vrai. 3-D DP Formulation

Let `dp[l][r][k]` = points maximums que nous pouvons obtenir à partir de `boxes[l ... r]` **avec `k` boîtes supplémentaires de la même couleur que `boxes[r]` annexe à droite**.

Pourquoi ? *
Lorsque nous supprimons un segment à la fin, nous pouvons vouloir le reporter pour le combiner avec des boîtes de couleur égale qui sont toujours sur la gauche.

C'est vrai. Récurrence

«» "
dp[l][r][k] =
1) Supprimer le dernier segment maintenant:
dp[l][r-1][0] + (k+1)2
2) Fusionner avec une boîte précédente de même couleur:
Pour chaque i dans [l, r-1] où les boîtes[i]== boîtes[r]:
dp[l][i][k+1] + dp[i+1][r-1][0]
«» "

La réponse est «dp[0][n-1][0]».

Optimisation (trick commun)

Avant d'évaluer la récurrence, nous avons la bonne extrémité:

«» "
pendant que r > l et boîtes[r] == boîtes[r-1]:
r-- // fusionner des boîtes de queue identiques
k++ // augmenter le nombre de boîtes identiques de droite
«» "

Cela réduit considérablement l'espace de l'État.

---

Analyse de complexité

**Heure**
C'est le cas.
**Récursions et mémoisations** Tableau 3-D ou carte des mémos

`n3 = 1e6` – parfait pour les processeurs modernes et la mémoire.

---

Faits saillants de la mise en oeuvre

Langue
-- -- -- -- -- --
Utiliser un "int" 3-D[][][] dp` rempli de "-1". Aide récursive à la mémorisation. Autres
**Python**. Autres
**C++**= Tableau 3-D statique `int dp[101][101][101]` initialisé à `-1`. Aide récursive. Autres

Toutes les implémentations suivent la même récurrence ; seule la syntaxe diffère.

---

Le bon, le mauvais et le mauvais problème

Aspect du bien
C'est pas vrai.
**Le concept**Démontre comment les décisions futures peuvent affecter l'état actuel – un modèle d'entrevue classique. Requiert un raisonnement prudent sur l'état* dont vous devez vous souvenir. Autres La lecture erronée de l'énoncé (p. ex., en pensant à "supprimer toutes les boîtes d'une couleur à la fois") entraîne un gaspillage d'efforts. Autres
**L'algorithme**Le DP 3-D est une solution soignée et élégante une fois comprise. Le PDD 3-D peut prêter à confusion; de nombreux candidats sautent directement dans un PDD 2-D et échouent. Erreurs d'implémentation: erreurs hors-par-un, clés de mauvais mémo, débordement dans `(k+1)*(k+1)` pour grand `k`. Autres
**Readability** La chaudière pour les tableaux 3-D peut masquer la logique. La profondeur de récursion dans Python/Java pourrait atteindre les limites pour `n=100`; le DP itératif pourrait être plus sûr mais plus verbeux. Autres
**Remplir les contraintes confortablement. Certaines solutions allouent des tableaux 1003 sans égard à la "n" réelle, gaspillant la mémoire. Autres

---

## -- À emporter pour les entrevues de travail

1. **Déclarer clairement l'état** – «dp[l][r][k]» signifie : *considérer la sous-requête «l..r» et nous avons déjà des boîtes «k» de la même couleur que la case la plus droite que nous pouvons fusionner plus tard*.
2. **Afficher l'astuce de rétrécissement** – la fusion de boîtes de queue identiques réduit la complexité et évite les états supplémentaires.
3. **Discuss complexity** – `O(n3)` est très bien pour `n=100`; justifie pourquoi nous utilisons la mémorisation.
4. **Cas d'Edge** – un seul élément, toutes les mêmes couleurs, pas deux couleurs adjacentes.
5. **Optimisation facultative** – discutez en utilisant une `HashMap<Long, Integer>` (clé d'état empaquetée) dans les langues où les tableaux 3-D sont gênants.

---

Code complet

> Les extraits de code suivants résolvent **Enlever les boîtes** dans **Java**, **Python** et **C++**.
> Chacune comprend de nombreux commentaires et suit la récurrence du PDD 3D décrite ci-dessus.

---

Solution Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
// dp[l][r][k] = points maxi pour les boîtes[l..r] avec k boîtes supplémentaires de la même couleur que les boîtes[r] à droite
[]] [] dp;

int public removeBoxes(int[] boxes) {
int n = cases.longueur;
dp = nouvelle int[n][n][n + 1]; // +1 car k peut être n-1
pour (int[]] arr2 : dp)
pour (int[] arr1 : arr2)
Arrays.fill(arr1, -1); // -1 signifie "non calculé"

retour résolve(boîtes, 0, n - 1, 0);
}

interne résolvez(int[] boîtes, int l, int r, int k) {
si (l > r) retourne 0;

// Fusionner les boîtes identiques à droite
pendant que (r > l && boîtes[r]] Boîtes [r - 1] {
R--;
k++;
}

si [dp[l][r][k] != -1) retour dp[l][r][k];

// Option 1: supprimer le dernier segment maintenant
int best = resolve(boîtes, l, r - 1, 0) + (k + 1) * (k + 1);

// Option 2: fusionner avec une précédente boîte de même couleur
pour (int i = l; i < r; i++) {
si (boîtes[i] ==boîtes[r]) {
int left = resolve(boxes, l, i, k + 1); // fusionner i avec le segment de droite
int right = resolve(boxes, i + 1, r - 1, 0); // supprimer la partie centrale d'abord
best = Math.max (best, gauche + droite);
}
}

retour dp[l][r][k] = meilleur;
}
}
«» "

---

Solution Python

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def removeBoxes(self, boxes: List[int]) -> Int:
n = len(boîtes)

@lru_cache(maxsize=Aucune)
def dfs(l: int, r: int, k: int) -> Int:
"""Return max points for box[l..r] with k extra boxs meme que box[r] on the right."""
si l > r:
retour 0

Fusionner des boîtes identiques à droite
pendant que r > l et boîtes[r] == boîtes[r - 1]:
r -= 1
k += 1

# Option 1: supprimer le segment le plus droit maintenant
best = dfs(l, r - 1, 0) + (k + 1) ** 2

# Option 2: fusionner avec une boîte de même couleur antérieure
pour i dans la plage(l, r):
si cases[i]== cases[r]:
best = max (best,
dfs(l, i, k + 1) + # fusion i avec droite
dfs(i + 1, r - 1, 0) # supprimer la partie médiane

le meilleur retour

retour dfs(0, n - 1, 0)
«» "

---

C++ Solution

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int removeBoxes(vector<int>& boxes) {
int n = cases.size();
// dp[l][r][k] = -1 indique une valeur non calculée
dp[101][101][101]; // n <= 100
memset(dp, -1, taille de(dp);
retour dfs(boîtes, 0, n - 1, 0, dp);
}

particulier:
int dfs(vector<int>& boxes, int l, int r, int k,
[101][101] {
si (l > r) retourne 0;

// Réduire les boîtes de queue identiques
pendant que (r > l && boîtes[r]] Boîtes [r - 1] {
R--;
k++;
}

si [dp[l][r][k] != -1) retour dp[l][r][k];

// Option 1: supprimer le segment le plus droit maintenant
int best = dfs(boîtes, l, r - 1, 0, dp) + (k + 1) * (k + 1);

// Option 2: fusionner avec une boîte de même couleur antérieure
pour (int i = l; i < r; ++i) {
si (boîtes[i] ==boîtes[r]) {
int left = dfs(boxes, l, i, k + 1, dp); // fusionner i avec le droit
int droite = dfs(boîtes, i + 1, r - 1, 0, dp); // supprimer la partie médiane
best = max (meilleur, gauche + droite);
}
}

retour dp[l][r][k] = meilleur;
}
};
«» "

---

Liste de contrôle finale avant de soumettre

Objet
-- -- -- -- -- --
Définition de l ' État Autres
La logique de la rupture de la queue est-elle incluse? Autres
Mémotisation : `-1` / `lru_cache` / `memset`? Autres
Le terme `dp[101][101][101]` est sûr pour `n ≤ 100`. Autres
Un seul élément, tous les mêmes, aucun égal adjacent – vérifié par des tests unitaires. Autres
"(k+1)" s'adapte à l'int signée 32 bits pour "k ≤ 99" (max 10 000). Autres

---

Pensée de clôture

Retirez Boxes est **un problème classique d'entrevue 3-D DP** qui vous oblige à penser *à l'avance* et à gérer un état *non évident* ('k').

Maîtriser cela signifie que vous êtes à l'aise avec:

- Concevoir des états qui capturent *les possibilités de fusion futures*
- Écriture propre, récursive DP avec mémoisation
- Communiquer l'intuition algorithmique sous pression d'entrevue

Donc, la prochaine fois que vous verrez "Supprimer la plus longue course en premier, rappelez-vous: ** le meilleur ordre pourrait être celui qui fusionne tourne plus tard**.

Bonne chance, et que votre prochaine entrevue ressemble plus à un puzzle résolu* qu'à un «break de cerveau*»! C'est ce qu'il a dit