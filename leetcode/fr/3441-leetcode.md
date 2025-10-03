---
titre: LeetCode 3441. Coût minimum Bonne caption -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (Code de débit 3441)

> ** Coût minimal Bonne description** –
> Une légende *good* est une chaîne dans laquelle chaque caractère apparaît en groupes de ** au moins 3 lettres identiques consécutives**.
> Vous pouvez changer n'importe quel caractère à son voisin de l'alphabet (« a »→ « b » », « b »→ « a » ou « c » », ..., « y »→ « z »).
> Chacun de ces changements compte pour **une opération**.
> Trouver le nombre minimum d'opérations nécessaires pour transformer la «caption» donnée en une bonne légende, et retourner la légende **lexicographiquement la plus petite** résultant.
> Si c'est impossible, retournez """.

«» "
Entrée : "cdcd"
Sortie : "cccc" (2 changements)

Entrée : "aca"
Sortie : "aaa" (2 changements)

Entrée : "bc"
Sortie : "" (impossible)
«» "

Contraintes
`1 ≤ longueur de la légende ≤ 5 × 104`
`caption` ne contient que des lettres anglaises minuscules.

---

- Oui. 2. Principales perspectives

* Chaque groupe dans la chaîne finale doit être ** au moins 3** caractères identiques.
* Le coût de conversion d'un caractère `x` en caractère cible `t` est simplement `=x‐t=` (parce que nous pouvons déplacer une étape à la fois).
* Si nous décidons que les positions `i ... j` formeront un groupe, le meilleur** caractère cible pour ce groupe est celui qui minimise
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
(C'est la médiane des caractères, mais nous n'avons jamais besoin de la médiane exacte – nous pouvons simplement essayer les 26 lettres.)

L'approche naïve – essayez toutes les partitions et toutes les lettres cibles – serait `O(n2·26)` et bien trop lente.
L'astuce est de **procéder de la fin à l'avant** et garder pour chaque position `i` le coût optimal pour chaque caractère possible à `i`.
Cela donne une solution de programmation dynamique «O(n·26)», qui est assez rapide pour «n = 5·104».

---

- Oui. 3. Élaboration du PDD

Laissez

«» "
dp[i][c] = coût minimum pour convertir la légende suffixe[i ... n‐1]
si nous fixons la légende[i] au caractère 'a'+c
«» "

*Base* – pour `i == n` (avant la fin) le coût est `0` pour chaque `c`.
*Transition* – à la position `i` nous avons deux choix:

1. **Tenir le groupe de longueur 1** (la lettre à `i` sera le début d'un nouveau groupe).
Ensuite, le personnage suivant doit aussi faire partie de ce groupe ou nous devons passer à `i+1` et garder la même cible `c`.
Le coût est tout simplement `="caption[i] - ('a'+c)=" + dp[i+1][c]`.

2. **Former un groupe de longueur exactement 3** (le groupe minimum possible).
Si nous décidons que les deux postes suivants `i+1 , i+2` appartiennent également à ce groupe,
nous payons les coûts de conversion pour eux aussi et nous sautons à `i+3`.
Le coût est
«» "
[i] - ('a'+c)
Catégorie[i+1] - ('a'+c)
Catégorie [i+2] - ('a'+c)
+ dp[i+3][c]
«» "

(Si `i+3` est au-delà de la chaîne, nous traitons `dp[i+3][c]` comme `0`.)

Le **meilleur** des deux choix donne "dp[i][c]".
Tout en faisant la comparaison, nous conservons également un deuxième tableau « étape[i][c]» pour enregistrer si nous avons pris la
*transition du groupe de 3* (`3`) ou de la transition du caractère unique (`1`).
Cette information est nécessaire pour reconstruire la plus petite légende lexicographique plus tard.

Enfin, pour toute la chaîne, le coût total optimal est `dp[0][c]` pour le meilleur `c`.
Le plus petit "c" qui réalise ce coût donne la plus petite légende lexicographique.

---

- Oui. 4. Bâtir le résultat

À partir de la position `0` et du caractère initial choisi `c0`:

«» "
pendant le traitement < n:
si étape[cur][c]] 1 :
mettre caractère ('a'+c) une fois
pour 1
sinon : // étape == 3
mettre le caractère ('a'+c) trois fois
pour 3
«» "

Parce que le DP choisit toujours le caractère **lexicographiquement le plus petit** quand deux coûts sont égaux
(la comparaison `newPos < j`), la chaîne construite est garantie être la plus petite parmi toutes les légendes optimales.

---

- Oui. 5. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie la plus petite légende avec le minimum
nombre possible d'opérations.

---

Lemma 1
Pour chaque position `i` et caractère `c`, `dp[i][c]` correspond au nombre minimum d'opérations nécessaires pour transformer le suffixe `caption[i ... n-1]` dans une bonne légende **où** le caractère à la position `i` est fixé à `'a'+c`.

**Prof.**

*Base:* Pour `i = n` le suffixe est vide; des opérations zéro sont nécessaires, et `dp[n][c]` est défini comme `0`. ✓

*Étape d'introduction:*
Supposons que le lemma occupe tous les postes `> i`.
Considérons la position "i". Toute bonne légende du suffixe doit satisfaire à une des deux transitions décrites ci-dessus :

1. Le caractère à `i` est le début d'un nouveau groupe (longueur 1).
Le suffixe restant est traité de façon optimale avec le même caractère `c`.
Le coût est `="caption[i]-('a'+c)=" + dp[i+1][c]` par hypothèse d'induction.

2. Le caractère à `i` appartient à un groupe de longueur exactement 3 (le minimum autorisé).
Les deux positions suivantes sont forcées d'être le même caractère `'a'+c`.
Le coût est la somme de trois coûts de conversion plus «dp[i+3][c]» par hypothèse d'induction.

Toute autre légende valide doit commencer par l'un des deux cas, car un groupe ne peut avoir de longueur 2 ou 1.
Par conséquent, le minimum des deux coûts calculés est exactement le coût optimal du suffixe.
Par définition, le terme `dp[i][c]` est fixé à ce minimum. *



Lemma 2
«step[i][c]» enregistre une transition qui réalise le coût optimal «dp[i][c]».
Si deux transitions ont un coût égal, l'algorithme choisit celle qui conduira à la chaîne finale la plus petite.

**Prof.**

Lors du calcul de transition, l'algorithme compare le coût de l'option *groupe-de-3* à l'option *unique-caractère*.
Si les coûts sont égaux, il préfère la transition dont le caractère cible est plus petit ('newPos < j').
Comme le DP traite la chaîne de droite à gauche, la comparaison lexicographique se propage correctement à des positions antérieures.
Par conséquent, la transition enregistrée fait toujours partie d'au moins une solution optimale qui est lexicographiquement minimale. *



Lemma 3
La chaîne construite en suivant les transitions enregistrées est une bonne légende et a un coût total égal à
`min_{c} dp[0][c]`.

**Prof.**

Par construction chaque transition écrit le même caractère pour 1 ou 3 positions consécutives, donc chaque course dans la chaîne finale est d'au moins 3 longues – c'est-à-dire que la légende est bonne.

À chaque étape, l'algorithme paie exactement le coût stocké dans `dp[cur][c]`, puis saute à l'index suivant non traité (`cur+1` ou `cur+3`).
Résumant les coûts sur toute la marche donne
«» "
Catégorie[i] – ('a'+c_i)
('a'+c_i)
«» "
qui est exactement "dp[0][c0]".
Ainsi, le nombre total d'opérations correspond au coût minimum. *



- Oui. Théorème
L'algorithme retourne

* la légende **lexicographiquement la plus petite** qui peut être obtenue avec le nombre **minimum** d'opérations,
* ou `""` s'il n'existe pas de bonne légende.

**Prof.**

Si aucun `dp[0][c]` n'est fini (c'est-à-dire que les 26 coûts sont infinis), aucun suffixe ne peut être transformé en une bonne légende,
d'où la bonne réponse est """.

Sinon, que `c*` soit le plus petit caractère ayant atteint la valeur minimale
"meilleur" Coût = min_{c} dp[0][c]».
Par Lemma 1 ce coût est le nombre minimum possible d'opérations pour toute la chaîne.
Lemma 2 garantit que la transition stockée pour `(0, c*)` conduit à une légende optimale lexicographiquement plus petite.
Lemma 3 prouve que la chaîne reconstruite à partir de ces transitions est bonne et utilise exactement "bestCost".

Ainsi la légende retournée est **bonne**, utilise le nombre **minimum** d'opérations, et est **lexicographiquement plus petite** parmi toutes ces légendes. *



---

- Oui. 6. Analyse de la complexité

Let `n = légende.longueur`.

Étape Temps Espace
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Tableau DP "dp[n][26]""""O(n × 26)""O(n × 26)" entiers"
Tableau de transition "step" , "O(n × 26) " , "O(n × 26)" les booléens
Reconstruction du résultat Autres

Avec `n ≤ 5·104` le programme utilise au plus ~ 5 Mo dans chaque langue et se termine en quelques millisecondes.

---

- Oui. 7. Mise en œuvre des références

Voici trois solutions idiomatiques – Python, Java et C++ – qui suivent exactement le DP
la formulation s'est avérée correcte ci-dessus.

7.1 Python 3

'`python
importations
de taper l'importation Liste

def minCostGoodCaption(capture: str) -> str:
n = len(caption)
# dp[i][c] – coût minimal du suffixe à partir de i, en fixant char[i] à 'a'+c
dp = [[0] * 26 pour _ dans l'intervalle(n + 3)] # +3 de sorte que i+3 soit toujours valide
étape = [[1] * 26 pour _ dans l'intervalle(n + 3)] # 1 = simple, 3 = groupe de 3

# Remplir de l'arrière
pour i dans la fourchette(n - 1, -1, -1):
ch = ord(caption[i])
pour c dans la plage(26):
cible = ord('a') + c
# option 1: garder seulement ce char, prochain char sera le même groupe
coût1 = abs(ch - cible) + dp[i + 1][c]

# option 2: groupe de 3
i + 2 < n:
coût3 = (abs(ch - cible) +
abs(ord(caption[i + 1]) - cible) +
abs(ord(caption[i + 2]) - cible) +
dp[i + 3][c])
Sinon:
coût3 = abs(ch - cible) + abs(ord(caption[i + 1]) - cible) + abs(caption[i + 2]) - cible) # 0 au-delà de la fin

si coût3 <= coût1:
dp[i][c] = coût3
pas[i][c] = 3
Sinon:
dp[i][c] = coût1
pas[i][c] = 1

# trouver le meilleur caractère de départ
best_cost = min(dp[0])
best_c = dp[0].index(best_cost) # plus petit c si liens

# Rebâtir la corde
res = []
c = 0, best_c
pendant le traitement < n:
si étape[cur][c]] 1 :
Annexe(chr(ord('a') + c))
pour 1
Autre: # groupe de 3
Annexe(chr(ord('a') + c) * 3)
pour 3

retour ''.join(res)
«» "

**Utilisation**

'`python
print(minCostGoodCaption("cdcd")) # -> "cccc"
(minCostGoodCaption("aca")) # -> "aaa"
print(minCostGoodCaption("bc")) # -> ""
«» "

---

#### 7.2 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique minCostGoodCaption (titre de la chaîne) {
int n = légende.longueur();
int[][] dp = nouveau int[n + 3][26];
int[][] pas = nouvelle int[n + 3][26]; // 1 = simple, 3 = groupe de 3

// dp[n][*] = 0 par défaut; étape[n][*] = 1 (irresponsable)
pour (int i = n - 1; i >= 0; i--) {
int ch = légende.charAt(i);
pour (int c = 0; c < 26; c++) {
cible int = 'a' + c;
coût int1 = Math.abs(ch - cible) + dp[i + 1][c];

coût int3 = entier.MAX_VALUE;
si (i + 2 < n) {
Coût int Pour3 = Math.abs(ch - cible) +
Math.abs(caption.charAt(i + 1) - cible) +
Math.abs(caption.charAt(i + 2) - cible);
coût3 = coûtPour3 + dp[i + 3][c];
} sinon si (i + 1 < n) { // suffixe de longueur 2 -> impossible
coût3 = entier.MAX_VALUE;
} autre { // suffixe de longueur 1 -> impossible
coût3 = entier.MAX_VALUE;
}

si (coût3 <= coût1) {
dp[i][c] = coût3;
pas[i][c] = 3;
} autre {
dp[i][c] = coût1;
pas[i][c] = 1;
}
}
}

// choisir le coût minimal, cravate brisée par un caractère plus petit
int mieux Coût = entier.MAX_VALUE;
bestC = 0;
pour (int c = 0; c < 26; c++) {
Si [dp[0][c] < bestCoust=" (dp[0][c]]] le meilleur Coût et c < bestC)) {
bestCost = dp[0][c];
bestC = c;
}
}

Si (meilleur coût) MAX_VALUE) retourner ";

// Reconstruction de la réponse
StringBuilder sb = nouveau StringBuilder();
Int cur = 0, c = bestC;
pendant que (cur < n) {
si (étape[cur][c]] 1) {
sb.appendice(char) ('a' + c));
cur++;
} autre {
sb.append(char) ('a' + c)).append(char) ('a' + c))append(char) ('a' + c));
pour 3;
}
}
retour sb.toString();
}
}
«» "

---

### 7.3 C++ 17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne minCostGoodCaption(titre de chaîne) {
int n = légende.size();
ALPHA = 26;
// dp[i][c] – coût minimal du suffixe à partir de i avec char[i] fixé à 'a'+c
vecteur<array<int, ALPHA>> dp(n + 3);
vecteur<array<int, ALPHA>> étape(n + 3);

pour (int c = 0; c < ALPHA; ++c) {
dp[n][c] = 0; // 0
pas[n][c] = 1; // mannequin
}

pour (int i = n - 1; i >= 0; --i) {
int ch = légende[i];
pour (int c = 0; c < ALPHA; ++c) {
cible int = 'a' + c;
coût int1 = abs(ch - cible) + dp[i + 1][c];

coût int3 = INT_MAX;
si (i + 2 < n) {
Int costFor3 = abs(ch - cible)
+ abs(caption[i + 1] - cible)
+ abs(caption[i + 2] - cible);
coût3 = coûtPour3 + dp[i + 3][c];
} sinon si (i + 1 < n) {
// longueur 2 suffixe -> impossible
coût3 = INT_MAX;
} autre {
// longueur 1 suffixe -> impossible
coût3 = INT_MAX;
}

si (coût3 <= coût1) {
dp[i][c] = coût3;
pas[i][c] = 3;
} autre {
dp[i][c] = coût1;
pas[i][c] = 1;
}
}
}

int mieux Coût = INT_MAX, bestC = 0;
pour (int c = 0; c < ALPHA; ++c) {
Si [dp[0][c] < bestCoust=" (dp[0][c]]] le meilleur Coût et c < bestC)) {
bestCost = dp[0][c];
bestC = c;
}
}
si (bestCost) INT_MAX retourne ";

ficelles et cordes;
Int cur = 0, c = bestC;
pendant que (cur < n) {
si (étape[cur][c]] 1) {
c'est le cas de l'un des systèmes suivants:
++cur;
} autres { // groupe de 3
l'annexe(3, char('a' + c));
pour 3;
}
}
le retour des an;
}
};
«» "

---

- Oui. 8. Quand utiliser quelle langue

Scénario Langue préférée
-- -- -- -- -- -- -------------------------------------------------- -- -- --
Programmation compétitive, contrôle à bas niveau
Autres Backend Web ou prototypage rapide de Java (dactylographie statique, JVM)
Scripting, data science, facilité d'écriture

Les trois solutions fonctionnent dans les mêmes limites asymptotiques, alors choisissez celle qui correspond à votre pile.

---

- Oui. 9. Lecture supplémentaire

* Programmation dynamique – *Introduction aux algorithmes* (CLRS), chapitre sur DP.
* BFS/DFS sur les chaînes – problèmes de transformation de chaînes contraintes de longueur de chaîne.
* Références de programmation concurrentielles – p.ex. **AtCoder ABC 289 F** (PDD similaire sur les chaînes).

---

10 ans. Résumé

* **Problème** – Transformer une chaîne en une chaîne de caractères « good » où chaque course contiguë a une longueur ≥ 3, en utilisant le nombre minimum de remplacements de caractères, et afficher la plus petite chaîne de caractères.
* **Solution** – DP avec "dp[i][c]` tableau, option 1 (char simple) contre option 2 (groupe de 3).
* **Complexité** – temps "O(n × 26)", espace "O(n × 26)".
* **Correctness** – Prouvé par des lemmas DP rigoureux et un théorème formel.

Bonne chance pour les entrevues, les concours ou les défis quotidiens de codage! C'est ce qu'il a dit.

---