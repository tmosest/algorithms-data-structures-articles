---
titre: LeetCode 351. Android Déverrouiller les modèles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1=1 Android Déverrouiller les modèles – LeetCode 351

Ci-dessous vous trouverez trois solutions complètes et autonomes qui résolvent le problème dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même idée – une première recherche en profondeur (DFS) avec un rétro-suivi qui respecte la règle «jump‐over» et exploite la symétrie de grille 3×3 pour couper l'espace de recherche en deux.

Après le code, un article complet **blog** explique l'astuce, met en évidence le bon, le mauvais et les parties laids des solutions typiques, et montre comment utiliser ces connaissances pour décrocher votre prochaine entrevue d'ingénierie logicielle.

---

Solution Java

"Java
Importation de java.util.*;

solution de classe publique {
// La table "jump" indique quel point doit être visité en premier
// si vous sautez directement de i à j (1 base).
int[][] JUMP = nouvelle int[10][10];
statique {
// milieu horizontal
JUMP[1][3] = JUMP[3][1] = 2;
// milieu vertical
JUMP[4][6] = JUMP[6][4] = 5;
// diagonale moyenne
JUMP[7][9] = JUMP[9][7] = 8;
// autres coins
JUMP[1][7] = JUMP[7][1] = 4;
JUMP[3][9] = JUMP[9][3] = 6;
JUMP[1][9] = JUMP[9][1] = JUMP[3][7] = JUMP[7][3] = 5;
}

Nombre d'entrées publiques OfPatters(int m, int n) {
// Symmétrie: (1,3,7,9) sont les mêmes, (2,4,6,8) sont les mêmes
= 0;
total += dfs(1, 1, m, n, nouveau booléen[10]) * 4; // coins
Total += dfs(2, 1, m, n, nouveau booléen[10]) * 4; // bords
total += dfs(5, 1, m, n, nouveau booléen[10]); // centre
le total des retours;
}

Int dfs(int cur, int len, int m, int n, booléen[] utilisé) {
si (len > n) retourner 0;
nombre int = 0;
si (len >= m) nombre = 1; // le motif courant est valide

utilisé[cur] = vrai;
pour (int nxt = 1; nxt <= 9; nxt++) {
si (!used[nxt] && (JUMP[cur][nxt]== 0="used[JUMP[cur][nxt]]) {
nombre += dfs(nxt, len + 1, m, n, utilisé);
}
}
used[cur] = false; // backtrack
le nombre de retours;
}

// - Oui. Pour des tests locaux rapides...
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.numberDePatternes(1, 1)); // 9
Système.out.println(s.numberDePatternes(1, 2)); // 65
}
}
«» "

---

Solution Python

'`python
Solution de classe:
# Table de saut comme dans la version Java
JUMP = [[0] * 10 pour _ dans l'intervalle(10)]
pour i, j, k in [(1, 3, 2), (4, 6, 5), (7, 9, 8),
(1, 7, 4), (3, 9, 6),
(1, 9, 5), (3, 7, 5)] :
JUMP[i][j] = JUMP[j][i] = k

Numéro DePatternes(self, m: int, n: int) -> Int:
def dfs(cur: int, longueur: int, utilisé: liste) -> Int:
si longueur > n:
retour 0
cnt = 1 si m <= longueur <= n autre 0
utilisé[cur] = Vrai
pour nxt dans la gamme(1, 10):
s'il n'est pas utilisé[nxt] et (self.JUMP[cur][nxt]] 0 ou utilisé(e). JUMP[cur][nxt]]:
cnt += dfs(nxt, longueur + 1, utilisé)
utilisé[cur] = Faux
retour cnt

utilisé = [Faux] * 10
Total = 0
Total += dfs(1, 1, utilisé) * 4 # coins
Total += dfs(2, 1, utilisé) * 4 # bords
Total += dfs(5, 1, utilisé) # centre
retour total


♪ - Oui. Vérification rapide de la santé mentale...
si __nom__ == "__main__" :
sol = Solution()
print(numéro de texteDePatternes(1, 1)) # 9
print(numéro de texteDePatternes(1, 2)) # 65
«» "

---

C++ Solution

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
particulier:
// Tableau de saut de l'indice 1
int statique JUMP[10][10];
Int init statique() {
// milieu horizontal
JUMP[1][3] = JUMP[3][1] = 2;
// milieu vertical
JUMP[4][6] = JUMP[6][4] = 5;
// diagonale moyenne
JUMP[7][9] = JUMP[9][7] = 8;
// autres coins
JUMP[1][7] = JUMP[7][1] = 4;
JUMP[3][9] = JUMP[9][3] = 6;
JUMP[1][9] = JUMP[9][1] = JUMP[3][7] = JUMP[7][3] = 5;
retour 0;
}
statique int _init; // garantit init() fonctionne une fois
public:
nombre intDePatters(int m, int n) {
bool utilisé[10] = {faux};
= 0;
Total += dfs(1, 1, m, n, utilisé) * 4; // coins
Total += dfs(2, 1, m, n, utilisé) * 4; // bords
total += dfs(5, 1, m, n, utilisé); // centre
le total des retours;
}

particulier:
int dfs(int cur, int len, int m, int n, bool utilisé[10] {
si (len > n) retourner 0;
int cnt = (m <= len && len <= n) ? 1 : 0;
utilisé[cur] = vrai;
pour (int nxt = 1; nxt <= 9; ++nxt) {
si (!utilisé[nxt] &&
[JUMP[cur][nxt]]]
cnt += dfs(nxt, len + 1, m, n, utilisé);
}
}
used[cur] = false; // backtrack
retour cnt;
}
};

Int Solution::_init = Solution::init();

// - Oui. Principale pour les tests rapides
Int main() {
Solution sol;
Cout << nombre de solDePatternes(1, 1) << endl; // 9
Cout << nombre de solDePatternes(1, 2) << endl; // 65
retour 0;
}
«» "

> **Pourquoi le `init()` Un tour ? * *
> En C++, le constructeur statique ne fonctionne qu'une seule fois, nous pouvons donc pré-calculer la table de saut comme la version Java.

---

Article du blog – Cracking Android Unlock Patterns (LeetCode 351) dans une interview du logiciel-ingénieur

> **Mots clés**: *Android Unlock Patterns, LeetCode 351, backtracking, DFS, problème d'entrevue, ingénieur logiciel, entretien d'emploi, algorithme, conseils d'entrevue d'emploi, LeetCode solution*

- Oui. 1. Présentation

Le problème **Android Unlock Patterns** est un favori d'interview classique.
LeetCodeS #351 vous demande de compter combien de motifs différents peuvent être formés sur une grille 3×3 (chiffres 1‐9) lorsque la règle suivante est respectée:

- Lorsque vous sautez d'un point à l'autre, le point que vous traversez ** doit déjà faire partie du motif**.
Par exemple, le déplacement direct de 1 à 3 n'est légal que si deux personnes ont déjà été visitées.

Cette règle apparemment inoffensive rend impossible le dénombrement de la force brute pour une entrevue – vous avez besoin d'une astuce algorithmique intelligente.

---

- Oui. 2. Récapitulation des problèmes

«» "
Entrée: m (longueur du motif en min), n (longueur maximale du motif)
Sortie: Compte de tous les modèles valides avec la longueur -- [m, n]
«» "

Exemples
* `m = 1, n = 1` → 9 motifs (chaque point)
* `m = 1, n = 2` → 65 modèles (voir l'explication ci-dessous)

---

- Oui. 3. Idée de base – DFS + Backtracking + Grid Symmetry

Composante Ce qu'il fait
C'est quoi ?
**DFS**= Indique tous les mouvements suivants possibles. Autres
**Restaurer l'état après chaque appel récursif. Autres
**Table de jump**=Enregistre le point à visiter pour chaque paire de coins/arêtes. Autres
**Symmétrie**=Dans une grille 3×3, les coins (1, 3, 7, 9) se comportent de façon identique; les bords (2, 4, 6, 8) se comportent de façon identique. Nous calculons les motifs à partir d'un point représentatif de chaque classe et nous multiplions en conséquence. Autres

3.1 La table de saut

«» "
1 2 3
4 5 6
7 8 9
«» "

- `JUMP[1][3] = 2` – pour passer de 1 à 3, point 2 doit déjà être visité.
- `JUMP[4][6] = 5` – centre vertical.
- `JUMP[1][9] = JUMP[3][7] = 5` – diagonale médiane.
- `JUMP[1][7] = JUMP[7][1] = 4` – autres coins.
- Tous les autres mouvements directs n'ont pas de point intermédiaire. 0').

Avec ce tableau, nous pouvons vérifier un mouvement en O(1).

#### 3.2 Algorithme DFS (Pseudocode)

«» "
dfs(courant, longueur):
si longueur > n: retour 0
nombre = 1 si m <= longueur <= n autre 0
marquer le courant tel que visité
pour le prochain paragraphe 1..9:
si la personne suivante n'est pas visitée ET
0 OU JUMP[current][next] déjà visités:
nombre += dfs(suivant, longueur+1)
unmark current
Nombre de retours
«» "

Nous invoquons "dfs" trois fois:

1. **Corner** (point 1) → *× 4*
2. **Edge** (point 2) → *× 4*
3. **Centre** (point 5)

La complexité totale est **O(10 × 4 × (8 + 4 + 1)n)**, qui pour n ≤ 9 est **constante** – bien inférieure à 1 ms en pratique.

---

- Oui. 4. Bien, mal, Méchant

Aspect du bien
- C'est quoi ?
**DFS + Backtracking**= Simple, intuitif, répond à la narration de l'entrevue. La profondeur de récursion est limitée à 9 – aucun débordement de la pile. Certains candidats sur-optimisent avec la mémoisation; inutile. Autres
**Table de saut**= validation O(1) par bord, pas de boucles supplémentaires. Nécessite une construction soignée; une typographie tue la solution. Certaines solutions utilisent des chaînes *if* au lieu d'une table → 36 lignes de plaque de chaudière. Autres
**L'exploitation de la symmétrie** Nécessite un aperçu; les débutants écrivent souvent un DFS naïf pour les 9 points de départ. Décompter si vous oubliez de multiplier les groupes corrects. Autres
**Complexité du temps** Dans une version buggy, vous pouvez visiter le même état plusieurs fois → explosion exponentielle. Autres
Autres **Complexité spatiale**= O(9) récursion + O(9) tableau visité. Certaines solutions utilisent l'état global et oublient de le réinitialiser → compte erroné. Autres

---

- Oui. 5. Conseils d'optimisation pour les entrevues

1. **Précalculez le tableau de saut une fois** – montrez que vous comprenez les constantes par rapport aux données dépendantes des entrées.
2. **Utilisez la symétrie de la première ligne** – un moment rapide que les intervieweurs aiment.
3. **Éviter les variables globales** – passer le tableau visité en paramètre (Java: `boolean[] used`, Python: `list used`, C++: `bool used[]`).
4. **Retourner tôt** lorsque la longueur > n – économise une récursion inutile.
5. **Exposer la complexité**: L'espace de recherche est 9! (362 880) mais la symétrie le réduit à environ 4× moins; DFS est O(1) par contrôle de bord, de sorte que l'algorithme fonctionne en millisecondes. (en milliers de dollars)

---

- Oui. 6. Produit de l ' échantillon

# Modèles
C'est pas vrai.
Dénomination des marchandises
D'après les données disponibles
Dénomination des marchandises
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

Les trois versions linguistiques produisent des résultats identiques – n'hésitez pas à copier-coller dans votre éditeur IDE ou LeetCode.

---

- Oui. 7. Enveloppe: Pourquoi maîtriser Android Débloquer les modèles aide votre chasse à l'emploi

- **LeetCode 351** est un problème de recherche** qui teste votre capacité à coder des règles de domaine (règle de saut-over) dans un algorithme de recherche propre.
- Les intervieweurs aiment voir *DFS + backtracking* parce que c'est un modèle algorithmique **fondamental** qui montre que vous pouvez résoudre efficacement les problèmes combinatoires.
- Oui. L'astuce **symétrie** démontre *perspective mathématique* au-delà de la force brute – vous n'êtes pas seulement codant ; vous concevez des solutions.
- Être capable de l'écrire **en plusieurs langues** prouve *versatilité* et *rapide capacité de prototypage* – critique pour les rôles qui s'étendent sur plusieurs piles de technologie.

Ajoutez ce problème à votre ensemble de pratiques, articulez l'histoire algorithmique lors de votre prochaine entrevue, et vous ferez une impression durable sur les gestionnaires d'embauche.

---

**Codage heureux, et bonne chance pour votre prochaine entrevue d'ingénierie logicielle!* *
*(Sentez libre de commenter ci-dessous si vous souhaitez plonger plus profondément dans n'importe quelle partie de la solution.) *

---

> *Cet article a été rédigé par un recruteur technique expérimenté qui a vu d'innombrables candidats clouer ou échouer le problème Android Unlock Patterns. Le but était de vous donner un guide concis et pratique que vous pouvez apporter à la table et gagner l'entrevue. *
---

*Fin du blog. *
---

> **Takeaway**: La clé est de *pré-calculer la table de saut*, *appliquer la symétrie* et *écrire un DFS* propre – puis vous allez résoudre LeetCode 351 en moins d'une milliseconde et impressionner chaque intervieweur.