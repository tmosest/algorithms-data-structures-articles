---
titre: LeetCode 1643. Les instructions les plus petites -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1643 – La méthode la plus petite
*Des chemins simples à un difficile défi combinatoire*

---

Récapitulation des problèmes

Vous êtes debout dans le coin supérieur gauche d'une grille `R × C`.
Vous ne pouvez bouger que **à droite** (`H`) ou **à bas** (`V`).
Toutes les séquences qui utilisent exactement `R` `V`s et `C` `H`s vous amèneront à la destination `(R,C)`.

Les séquences sont triées **lexicographiquement** («H» < «V»).
Compte tenu d'un `k` indexé, retourner la séquence *kth* la plus petite.

«» "
destination = [2, 3], k = 1 → "HHHV"
destination = [2, 3], k = 3 → "HHVVH"
«» "

Contraintes
`1 ≤ R, C ≤ 15` – assez petite pour une table DP mais assez grande pour qu'une explosion combinatoire brutale soit impossible.

---

- Oui. Pourquoi la programmation dynamique gagne
*Le point de vue clé:*
A n'importe quelle cellule `(i, j)` le nombre de chemins restants au but est égal à la somme des chemins de la cellule à la droite `(i, j+1)` et la cellule ci-dessous `(i+1, j)` – la récurrence classique de chemins Uniques.

Avec cette table en main nous pouvons **marcher** la grille:

1. Si le chemin *k*th commence par un mouvement **droit**, il doit appartenir au premier chemin `dp[i][j+1]` lexicographiquement plus petit.
2. Sinon, le chemin commence par un mouvement **down** et on soustrait ces premiers chemins `dp[i][j+1]` de *k* et on continue.

Cette marche gourmande court dans `O(R+C)` temps une fois que la table DP est construite.
La mémoire est `O(R*C)` – confortablement petite pour les limites.

---

Faits saillants de la mise en oeuvre

Mots clés Autres
C'est pas vrai.
*Java**= Utilisez `long` pour tenir compte du nombre de sentiers (`C(30,15)` = 155 117 520 < 231). Construisez DP bas vers le haut, puis marchez la grille. Autres
**Python**"int" n'est pas lié – même logique DP. `append()` à une liste, enfin `''.join()`. Autres
**C++**=Le long non signé (64 bits) suffit. Utiliser `vecteur<vecteur<non signé long>>`. Autres

> **Bien** – temps O(R·C), mémoire O(R·C), simple à comprendre.
> **Bad** – Pour des grilles beaucoup plus grandes, cela deviendrait mémoire-lourd; aussi "long" en Java est 64-bit, mais nous restons bien en dessous du débordement.
> **Ugly** – Une approche naïve combinatoire qui tente de générer tous les chemins ou utilise des formules factorielles déborde rapidement ou devient « O(k) » dans le temps.

---

# # # #=# Code Snippets

Java
"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne kthPetitePath(int[] destination, int k) {
int R = destination[0] + 1; // lignes comprenant la cellule de démarrage
int C = destination[1] + 1; // colonnes incluant la cellule de départ
long[] dp = nouveau long[R][C];

// dernière ligne et colonne n'ont qu'une seule façon de terminer
pour (int i = 0; i < R; i++) dp[i][C-1] = 1;
pour (int j = 0; j < C; j++) dp[R-1][j] = 1;

// Remplir DP bottom-up
pour (int i = R-2; i >= 0; i--) {
pour (int j = C-2; j >= 0; j--) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

StringBuilder sb = nouveau StringBuilder();
i = 0, j = 0;
alors que (i < R-1 && j < C-1) {
longue droite Voies = dp[i][j+1];
si (k <= patte droite) { // aller à droite
sb.annexe('H');
j++;
} autre { // descendre
k -= patte droite;
sb.annexe('V');
i++;
}
}
// terminer la ligne droite restante
sb.append("V".repeat(R-1-i));
sb.append("H".repeat(C-1-j));
retour sb.toString();
}
}
«» "

Python
'`python
Solution de classe:
def kthSmallestPath(self, destination: list[int], k: int) -> str:
R, C = destination[0] + 1, destination[1] + 1
dp = [[0] * C pour _ dans la plage(R)]

Nombre de cas de base
pour i dans la plage(R): dp[i][C-1] = 1
pour j dans la plage(C): dp[R-1][j] = 1

# construire DP bas-up
pour i dans la plage (R-2, -1, -1):
pour j dans la plage (C-2, -1, -1):
dp[i][j] = dp[i+1][j] + dp[i][j+1]

# marcher sur la grille
i = j = 0
chemin = []
alors que i < R-1 et j < C-1:
si k <= dp[i][j+1]: # aller à droite
chemin.append('H')
j += 1
Sinon: # descendre
k -= dp[i][j+1]
chemin.append('V')
i += 1

# ajouter le dernier segment droit
chemin.append('V' * (R-1-i))
chemin.append('H' * (C-1-j))
retour ''.join(chemin)
«» "

C++
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
string kthSmallestPath(vector<int>& destination, int k) {
int R = destination[0] + 1;
int C = destination[1] + 1;
vecteur<vecteur<non signé long>> dp(R, vecteur<non signé long> (C, 1));

// dernière ligne / colonne déjà 1
pour (int i = R-2; i >= 0; --i) {
pour (int j = C-2; j >= 0; --j) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

ficelles et cordes;
i = 0, j = 0;
alors que (i < R-1 && j < C-1) {
si (k <= dp[i][j+1]) { // aller à droite
ans.push_back('H');
++j;
} autre { // descendre
k -= dp[i][j+1];
as.push_back('V');
++i;
}
}
Annexe(R-1-i, 'V');
Annexe(C-1-j, 'H');
le retour des an;
}
};
«» "

> Les trois solutions sont "O(R*C)" temps, "O(R*C)" mémoire, et fonctionnent pour la taille maximale de la grille (`15 × 15`).

---

Analyse de complexité

Opération de Java Python C++
- C'est quoi ?
**Heure** Même
**Mémorie** Autres
**Risque de surflux** Autres

---

C'est pas vrai. Case & -Qu'est-ce que si

Traitement des bords Autres
- Oui.
`k` est égal au nombre total de chemins.La marche ira toujours à droite jusqu'à ce qu'elle soit forcée, produisant la dernière chaîne. Autres
`k` est égal Immédiatement toujours prendre à droite, donnant la première rangée de `H`s suivie de tous `V`s. Autres
Destination `[0, 0]`"" `R = C = 1`, DP est une cellule unique, boucle ne fonctionne jamais; nous ajoutons une chaîne vide. Autres
"k" > "dp[0]]" Le problème garantit la validité de « k »; autrement, nous lancerions une exception. Autres

---

## 7--Des conseils d'entrevue

Thème Pourquoi c'est important
- Oui.
**Maîtrise de la programmation dynamique**La plupart des gestionnaires d'embauche aiment les solutions DP claires. Mettre en évidence la récurrence, les cas de base et la construction ascendante. Autres
Autres **Optimisation de l'espace** si vous ne gardez que la ligne actuelle, mais pour ce problème, la table complète est bonne. Autres
**Combinatoire par rapport à DP**= Montrez pourquoi le dénombrement factoriel échoue (dépassement, temps). Autres
**Test**= Générer des grilles aléatoires (=15) et un contrôle de la force brute à l'aide d'ortools. produit` pour les petites tailles. Autres
Autres **Codage Style**= Effacer les noms de variables (`rightPaths`, `dp`), les fonctions de responsabilité unique et les commentaires. Autres

> **Hook d'interview**: Pouvez-vous trouver le chemin kth dans une grille `R × C` sans énumérer toutes les possibilités? Cette question est un favori dans les rondes d'entretien algorithmiques et apparaît dans LeetCode 1643. Maîtrisez-le, et vous acquerrez la portion DP de presque n'importe quel test de codage.

---

Article de blog optimisé par le SEO

> **Description détaillée**
> Apprendre à résoudre le LeetCode 1643 – Kth Smallest Instruction – avec programmation dynamique. Obtenez le code en Java, Python, C++, et des conseils prêts à l'interview pour la chasse au travail. (en milliers de dollars)

---

# Kth plus petite instruction – LeetCode 1643 – Un complet Guide

- Oui. Qu'est-ce que l'instruction la plus petite?
LeetCode 1643 est un problème de combinatoire de chemin de grille qui vous défie de retourner la plus petite séquence de mouvements lexicographiquement `kth` qui mène du coin supérieur gauche à une destination de grille en utilisant seulement les étapes droite (`H`) et descendante (`V`).

> **Mots clés**: *Kth Smallest Instruction*, *LeetCode 1643*, *grid path combinatorics*, *dynamique interview question*, *grid path DP*, *unique path*

Pourquoi c'est un problème d'entrevue
- **Concepts de base**: relations de récurrence, combinatoire, ordre lexicographique.
- **Coding Practice**: Parfait pour pratiquer le PDD, la manipulation des cordes et la prise de décision gourmande.
- **Real‐World Application**: Algorithmes de navigation, planification du mouvement des robots et optimisation combinatoire.

---

## Description du problème (en bref)

«» "
destination int[] = {R, C}; // R lignes, colonnes C (1-indexées)
int k; // 1-position indexée dans la liste des chemins triés
retourner kth lexicographiquement la plus petite séquence de 'H' et 'V'.
«» "

Contraintes: «1 ≤ R, C ≤ 15».

---

Approche : PDD ascendante + promenade en plein air

1. ** Tableau PD** :
`dp[i][j] = dp[i+1][j] + dp[i][j+1]`
Cas de base : dernière ligne/colonne → 1.

2. **Greedy Walk**:
Dans la cellule `(i, j)`, si `k` est ≤ `dp[i][j+1]`, le prochain mouvement est `H`; sinon `V` et soustraire `dp[i][j+1]` de `k`.

3. **Finir droit**:
Une fois que vous êtes sur la dernière ligne ou colonne, ajoutez les autres `V`s ou `H`s.

---

Complexité

- **Heure**: `O(R · C)` pour le bâtiment DP + `O(R + C)` pour la marche = `O(R·C)`.
- **Espace**: `O(R · C)` (= 256 cellules pour les limites données).

---

Code complet (Java, Python, C++)

### Java
"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne kthPetitePath(int[] destination, int k) {
int R = destination[0] + 1;
int C = destination[1] + 1;
long[] dp = nouveau long[R][C];

pour (int i = 0; i < R; i++) dp[i][C-1] = 1;
pour (int j = 0; j < C; j++) dp[R-1][j] = 1;

pour (int i = R-2; i >= 0; i--) {
pour (int j = C-2; j >= 0; j--) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

StringBuilder sb = nouveau StringBuilder();
i = 0, j = 0;
alors que (i < R-1 && j < C-1) {
si (k <= dp[i][j+1]) {
sb.annexe('H');
j++;
} autre {
k -= dp[i][j+1];
sb.annexe('V');
i++;
}
}
sb.append("V".repeat(R-1-i));
sb.append("H".repeat(C-1-j));
retour sb.toString();
}
}
«» "

Python
'`python
Solution de classe:
def kthSmallestPath(self, destination: list[int], k: int) -> str:
R, C = destination[0] + 1, destination[1] + 1
dp = [[1] * C pour _ dans l ' intervalle (R)]

pour i dans la plage (R-2, -1, -1):
pour j dans la plage (C-2, -1, -1):
dp[i][j] = dp[i+1][j] + dp[i][j+1]

chemin = []
i = j = 0
alors que i < R-1 et j < C-1:
si k <= dp[i][j+1]:
chemin.append('H')
j += 1
Sinon:
k -= dp[i][j+1]
chemin.append('V')
i += 1

chemin.append('V' * (R-1-i))
chemin.append('H' * (C-1-j))
retour ''.join(chemin)
«» "

C++
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
string kthSmallestPath(vector<int>& destination, int k) {
int R = destination[0] + 1;
int C = destination[1] + 1;
vecteur<vecteur<non signé long>> dp(R, vecteur<non signé long> (C, 1));

pour (int i = R-2; i >= 0; --i) {
pour (int j = C-2; j >= 0; --j) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

ficelles et cordes;
i = 0, j = 0;
alors que (i < R-1 && j < C-1) {
si (k <= dp[i][j+1]) {
ans.push_back('H');
++j;
} autre {
k -= dp[i][j+1];
as.push_back('V');
++i;
}
}
Annexe(R-1-i, 'V');
Annexe(C-1-j, 'H');
le retour des an;
}
};
«» "

---

## 9--Ce que vous devriez dire aux intervieweurs

L'aspect L'aspect
- C'est quoi ?
**Complexité algorithmique** Pour les grilles > 2000, le tableau DP dépasserait les limites de mémoire. "Essai de calculer le chemin kth par le dénombrement factoriel complet ("O(2^(R+C)") est à la fois lent et susceptible de déborder. Autres
**Détail de la mise en œuvre**= Code clair et testable avec commentaires; aucun nombre magique. Des hypothèses codées de manière rigide (par exemple, ignorer le mot "k" invalide) pourraient susciter des soupçons. La force brute récursive sans élagage est un overflow de pile et "O(2^(R+C)")". Autres
Autres **Edge‐Case Handling**= Tous les cas d'angle couverts; l'algorithme se vérifie automatiquement.= Si `k` est hors de portée, vous devez lancer une erreur. Unchecked `k` conduit à une indexation négative ou des boucles infinies. Autres

> **Déclaration d'entrevue* *
> Nous pouvons trouver le chemin kth sans énumérer tous les chemins en construisant une table DP qui compte les chemins restants et puis en marchant avidement à travers la grille, en prenant des décisions basées sur le nombre restant. (en milliers de dollars)

---

La pensée de clôture

Maîtrise **LeetCode 1643 – Kth le plus petit Instruction** présente votre capacité à traduire des problèmes combinatoires en solutions de programmation dynamique efficaces. Les exemples de code propre en Java, Python et C++ ci-dessus vous aideront à clouer la partie de codage, et le commentaire prêt à l'entrevue vous permet de discuter de votre processus de pensée avec confiance.

> **Prêt pour le prochain défi?** Continuez à pratiquer le DP, la manipulation des cordes et les algorithmes gourmands. Votre futur employeur vous remerciera!

---

> **Mots clés** répétés pour une portée maximale : *Kth Smallest Instruction*, *LeetCode 1643*, *grid DP*, *entrevue de programmation dynamique*, *robot path planning*, *unique paths problem*, *coding interview question*.

---

Joyeux codage et bonne chance avec votre recherche d'emploi!

---


---

> **Fin du blog**
> N'hésitez pas à partager sur GitHub, StackOverflow ou les communautés de codage – ce jeu de solutions est la norme d'or pour LeetCode 1643.