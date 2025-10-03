---
titre: LeetCode 1931. Peinture d'une grille avec trois couleurs différentes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Leetcode 1931 – *Peinture d'une grille avec trois couleurs différentes*
## Les bons, les mauvais et les méchants – Un billet de blog favorable à l'emploi

> **SEO Mots-clés**: Leetcode 1931, Peinture d'une grille avec trois couleurs différentes, DP, Bitmask DP, Coloration de la grille, Codage Interview, solution Java, Python solution, C++ solution, interview prep, algorithmes, programmation dynamique, défi de codage

---

- Oui. 1. Aperçu du problème

Description
- C'est quoi ?
*Titre * Peinture d'une grille avec trois couleurs différentes
**ID**
Difficulté
**Contraintes**
**Objectif**=Combien de façons de peindre une grille *m* × *n* avec 3 couleurs (rouge, vert, bleu) de telle sorte que ** aucune cellule adjacente orthogonalement ne partage la même couleur**. Autres
Autres **Réponse Mod.

**Pourquoi ce problème est digne d'entrevue**

* Il teste **state-compression DP** (bitmasking) – une base pour de nombreuses entrevues de niveau supérieur.
* Il vous défie de penser à **horizontal vs. vertical adjacence** séparément.
* Il s'écaille avec *n* jusqu'à 1000, vous forçant à trouver une solution *O(n · K2)* où *K* est le nombre d'états de colonne valides (= 81 pour *m* = 5).

---

- Oui. 2. Intuition et stratégie de haut niveau

1. **Traitez les colonnes en tant que dimension DP** – nous traitons la colonne de grille par colonne.
2. **Générer tous les états de colonne valides** (`état`) de sorte qu'aucune ligne consécutive dans la même colonne ne partage la même couleur. Pour *m* = 5, le nombre est au plus 35 = 243, mais les conflits verticaux réduisent à 81.
3. **Déterminer la compatibilité entre les états** – deux états `A` et `B` peuvent s'asseoir côte à côte si pour chaque ligne `i`, `A[i]` ↓ `B[i]` (pas de conflit horizontal).
4. ** Programmation dynamique**
* `dp[0][s] = 1` pour chaque état valide `s` (première colonne).
* Transition :
Texte
dp[col][next] += dp[col‐1][prev] si prev et suivante sont compatibles
«» "
* Tous les calculs sont effectués modulo "MOD".
4. **Réponse** – totaliser tous les «dp[n‐1][s]» pour la dernière colonne.

> **Le bien** – Le problème se décompose naturellement dans un espace d'état *finite* ; vous n'avez jamais besoin d' itérer sur toute la grille.
> **Le "Bad"** – Si vous générez naïvement toutes les 3n possibilités pour chaque cellule, le temps explose.
> **Les La subtilité des conflits *vertical* étant séparés des conflits *horizontal* peut faire voyager beaucoup de gens. La clé est de coder chaque colonne en un seul entier (bitmask) pour garder les transitions O(K2).

---

- Oui. 3. Algorithme détaillé

### 3.1. Codage d'une colonne

- Représenter chaque ligne avec 2 bits (`00` = rouge, `01` = vert, `10` = bleu).
- Pour *m* ≤ 5, la colonne correspond à un entier de 10 bits (5 × 2).
- Une colonne `masque` est *valable* si pour tous `row` > 0, les deux blocs 2 bits diffèrent.

3.2. Liste de compatibilité des bâtiments

- Pour chaque paire de masques valides `(masqueA, masqueB)`:
- Ils sont **compatibles** si `(maskA & 0x3) (maskB & 0x3)` pour la ligne la plus basse, `(maskA >> 2 & 0x3) 2 & 0x3)` pour la deuxième ligne, etc.
- Entreposez `maskB` dans un vecteur de transitions compatibles pour `maskA`.
- Complexité: *O(K2)*, K ≤ 81.

3.3. PDD à travers les colonnes

«» "
dp[0][s] = 1 // première colonne
pour col = 1 .. n-1:
pour prev dans les états valides:
pour la prochaine dans les transitions[prev]:
dp[col][next] = (dp[col][next] + dp[col-1][prev]) % MOD
«» "

Enfin, `réponse = ↓ dp[n-1][s]` pour tous `s`.

---

- Oui. 4. Analyse de la complexité

Formule métrique pour *m* = 5
C'est pas vrai.
**K (états)**=3m – conflits verticaux ≤ 81=Toutes les 35 possibilités moins celles avec des couleurs égales consécutives. Autres
**Temps**=O(n · K2)==1 000=812=6.5 M ops== Dominé par les boucles de transition. Autres
**L'espace**="O(K)=" ~ 81 entiers par colonne=" Nous ne pouvons conserver que les tableaux DP de la colonne actuelle et précédente. Autres

---

- Oui. 5. Mise en œuvre du code

> **Conseil pour les entrevues**: Affichez une seule passe de DP avec *O(K)* espace, mais gardez le code lisible.

Oui. Java 17 (Fastest readable)

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

couleur int publiqueTheGrid(int m, int n) {
Liste des états < entiers > = nouvelle liste de répartition<>();
// Générer tous les masques de colonnes valides
pour (int masque = 0; masque < (1 << (m * 2)); masque++) {
si (isValidColumn(masque, m)) indique.add(masque);
}

// Compatibilité précalculée
Liste<Liste<entier>> compat = nouvelle liste de distribution<>();
pour (int i = 0; i < states.size(); i++) {
Liste<entier> liste = nouvelle liste d'array<>();
pour (int j = 0; j < states.size(); J++) {
si (estCompatible(states.get(i), states.get(j), m))
liste.add(states.get(j));
}
compat.add(liste);
}

// PDD
long[] prev = nouveau long[states.size()];
Arrays.fill(prev, 1); // première colonne

pour (int col = 1; col < n; col++) {
long[] next = nouveau long[states.size()];
pour (int i = 0; i < states.size(); i++) {
longueurs = prev[i];
Si (toujours) 0) poursuivre;
pour (int nb : compat.get(i)) {
int idx = états.indexOf(nb);
suivant[idx] = (suivant[idx] + voies) % MOD;
}
}
prev = suivant;
}

// Somme
long ans = 0;
pour (long v : prev) ans = (ans + v) % MOD;
retour (int) ans;
}

booléen privé est ValidColumn (masque int, int m) {
Int prev = -1;
pour (int r = 0; r < m; r++) {
couleur int = (masque >> (2 * r) & 3; // 0=rouge,1=vert,2=bleu
si (couleur == prev) retourner faux;
prev = couleur;
}
retour vrai;
}

booléen privé estCompatible(int a, int b, int m) {
pour (int r = 0; r < m; r++) {
int ca = (a >> (2 * r)) & 3;
int cb = (b >> (2 * r)) & 3;
si (ca) cb) retourner faux;
}
retour vrai;
}
}
«» "

> **Pourquoi ce code Java gagne**
> * Utilise primitive `int` bitmask - pas de boxe au-dessus.
> * Conserve une empreinte de mémoire minimale (`states.size()` ≤ 81).
> * Démontre une séparation nette de la génération* (isValidColumn) et de la transition* (isCompatible).

---

5.2. Python 3 (propre et pyronique)

'`python
MOD = 1 000 000 007

Solution de classe:
def couleur TheGrid(self, m: int, n: int) -> Int:
N° 1 Générer tous les masques de colonnes valides
def gen(row, prev, masque):
si ligne == m:
États.annexe(masque)
retour
pour le col dans l'intervalle(3): #0,1,2 pour R,G,B
si ligne > 0 et (masque >> (2*(row-1)) et 3 == col:
poursuivre
(col << (2*row))

États = []
gén(0, -1, 0)

N° 2 Transitions précalculées
comp = {s: [] pour s dans les états}
pour a dans les états:
pour b dans les états:
si tous((a >> (2*i) et 3) != (b >> (2*i) et 3) pour i dans l'intervalle(m)):
Comp[a].appendice(b)

# 3-
dp = {s: 1 pour s dans les états} # première colonne
pour _ dans la plage(1, n):
Nouveau = {}
pour prev, manières dans dp.items():
pour nxt dans comp[prev]:
new[nxt] = (new.get(nxt, 0) + manières) % MOD
dp = nouveau

N° 4 Réponse sommaire
retour sum(dp.values()) % MOD
«» "

> **Points saillants spécifiques au python**
> * Générateur récursif est minuscule – aucune bibliothèque externe.
> * Utilise le dictionnaire pour les transitions DP; toujours O(K2).
> * Garde petite utilisation de la mémoire – seulement deux dictionnaires à la fois.

---

5.3. C++17 (Fastest possible)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
l'état statique du constexpr MOD = 1'000'000'007;

couleur int LeGrid(int m, int n) {
// -------- 1. Construisez tous les états de colonne valides ---------
les états vectoriaux<int>;
pour (int masque = 0; masque < (1 << (m * 2)); ++masque) {
si (validColumn(mask, m)) states.push_back(mask);
}

// -------- 2. Compatibilité précalculée ---------
vecteur<vector<int>> trans(states.size());
pour (int i = 0; i < (int)states.size(); ++i) {
pour (int j = 0; j < (int)states.size(); ++j) {
si (compatible(états[i], états[j], m))
[i].push_back(j);
}
}

// -------- 3. PDD sur les colonnes ----------
vector<int> dp(states.size(), 1), ndp(states.size(), 0);
pour (int col = 1; col < n; ++col) {
Remplissage(ndp.begin(), ndp.end(), 0);
pour (int i = 0; i < (int)states.size(); ++i) {
si (!dp[i]) continue;
pour (int j : trans[i]) {
ndp[j] = (ndp[j] + dp[i]) % MOD;
}
}
dp.swap(ndp);
}

// -------- 4. Résumez...
Int ans = 0;
pour (int x : dp) ans = (ans + x) % MOD;
le retour des an;
}

particulier:
Bool valide Colonne(int masque, int m) const {
Int prev = -1;
pour (int r = 0; r < m; ++r) {
int col = (masque >> (2 * r)) & 3;
si (col == prev) retourner faux;
prev = col;
}
retour vrai;
}

compatible(int a, int b, int m)
pour (int r = 0; r < m; ++r) {
int ca = (a >> (2 * r)) & 3;
int cb = (b >> (2 * r)) & 3;
si (ca) cb) retourner faux;
}
retour vrai;
}
};
«» "

> **Pourquoi cette solution C++ excelle**
> * Utilise `vector<int>` – mémoire contiguë, cache amical.
> * `trans` comme liste d'adjacence → O(K2) mais seulement des indices entiers.
> * Constante `MOD` – opération mod en ligne est très bon marché.

---

- Oui. 6. Ce qu'il faut souligner dans les entrevues

1. **Réduction de l'espace d'état** – Montrez comment l'encodage d'une colonne dans un bitmask réduit le problème aux états `K`.
2. **Pré-computation de transition** – Préciser que la compatibilité est indépendante de l'index des colonnes, ce qui permet de réutiliser toutes les colonnes `n`.
3. ** Optimisation de l'espace** – Conserver seulement deux lignes DP (`prev`, `next`) au lieu de `n` matrices complètes.
4. **Arithmétique modulaire** – Toutes les sommes doivent être modulo `MOD` (cas de bord important).
5. **Edge Cases** – Quand `n == 0`? (Bien que les contraintes disent `n ≥ 1').
6. **Test** – Vérifier les cas échantillonnés, par exemple `m=2, n=3 → 18`.

---

- Oui. 7. Pensées finales

> **En résumé**:
> *Tirer parti du petit espace d'état, coder des colonnes avec des bitmasks, pré-calculer des transitions compatibles, et exécuter un DP simple. *

> **Stratégie d'entrevue* *
> * Parlez d'abord de la décomposition du problème.
> * Afficher la logique de génération d'état et de compatibilité.
> * Alors expliquez la transition du PDD.
> * Fin de la somme finale.

Avec cette structure, vous démontrez à la fois une compréhension **conceptuelle** et une implémentation **pratique** – la combinaison gagnante pour toute entrevue de codage.

---

- Oui. 8. Lectures supplémentaires et problèmes similaires

- **"Nombre de moyens de remplir un tableau avec des entiers K"** (LeetCode 1106) – DP similaire basé sur l'état.
- **"Grès colorés"** – programmation dynamique sur bitmasks.
- **"Grid Coloring with Contraintes"** – combinatoire avancé avec DP.

> ** Bon codage !**

---

> *Si vous voulez une marche pas à pas dans les conversions, n'hésitez pas à demander. Joyeux entretien ! *

---
**Mots clés**: `LeetCode 1106`, `Grid coloring`, `Bitmask DP`, `Java`, `Python`, `C++`, `Dynamitic Programming`, `Combinatorics`.