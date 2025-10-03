---
titre: LeetCode 688. Probabilité Knight dans Chessboard -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions en trois langues pour la probabilité de nuit sur un tableau d'échecs

Le problème LeetCode **688 – Knight Probabilité in Chessboard** vous demande de calculer la probabilité qu'un chevalier reste sur un tableau *n × n* après avoir effectué exactement *k* se déplace, à partir de la cellule `(ligne, colonne)`.
Le chevalier choisit l'un de ses 8 mouvements possibles de façon uniforme au hasard, même si le mouvement choisi l'abaissait de la planche.
Quand il quitte la planche, le processus s'arrête; sinon, il continue jusqu'à ce qu'il ait fait *k* se déplacer.

L'approche la plus courante et efficace dans le temps est la programmation dynamique** (DP).
Vous trouverez ci-dessous des implémentations propres et autonomes dans **Java, Python et C++**.
Tous les trois partagent la même idée algorithmique :

1. ** État du PD** – `dp[i][j]` est la probabilité que le chevalier soit sur la case `(i, j)` après un nombre donné de mouvements.
2. **Transition** – pour chaque carré et chaque chevalier légal, ajouter `dp[prev] / 8.0` à la nouvelle grille de probabilité.
3. **Itération** – répéter la transition exactement *k* fois.
4. **Réponse** – totaliser toutes les probabilités dans la grille finale (le chevalier pourrait être n'importe où sur le plateau après *k* déplacements).

Le temps d'exécution est **O(k · n2)** et l'utilisation de la mémoire est **O(n2)** – optimal pour les contraintes données (n ≤ 25, k ≤ 100).

---

#### 1.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
// Tous les 8 mouvements de chevalier
finale statique privée [] MOUVEMENTS = {
2 et 2
{ 1, -2}, { 1, 2}, { 2, -1}, { 2, 1}
};

double chevalier publicProbabilité(int n, int k, int rang, int colonne) {
double[]dp = nouveau double[n][n];
dp[row][colonne] = 1,0; // position de démarrage

pour (int moving = 0; moving < k; moving++) {
double[][] suivante = nouveau double[n][n];
pour (int r = 0; r < n; r++) {
pour (int c = 0; c < n; c++) {
si [dp[r][c]] 0) continuer; // rien à répandre
pour (int[] m : MOUVEMENTS) {
Int nr = r + m[0];
int nc = c + m[1];
si [isValid(nr, nc, n)] {
suivant[nr][nc] += dp[r][c] / 8.0;
}
}
}
}
dp = suivant;
}

total double = 0,0;
pour (int r = 0; r < n; r++) {
pour (int c = 0; c < n; c++) total += dp[r][c];
}
le total des retours;
}

booléen privé est Valid(int r, int c, int n) {
r >= 0 && r < n && c >= 0 && c < n;
}
}
«» "

---

#### 1.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
# 8 possibles mouvements de chevalier
MOUVEMENTS: Liste [Liste[int]] = [
(-2, -1), (-2, 1), (-1, -2), (-1, 2),
(1, -2), (1, 2), (2, -1), (2, 1)
- Oui.

def  KnightProbabilité(self, n: int, k: int, rang: int, col: int) -> flotteur:
dp = [[0,0] * n pour _ dans la plage(n)]
dp[row][col] = 1,0

pour _ dans la plage(k):
next_dp = [[0.0] * n pour _ dans l'intervalle(n)]
pour r dans la plage(n):
pour c dans la plage(n):
si dp[r][c] == 0:
poursuivre
pour le Dr. Ça va ?
nr, nc = r + dr, c + dc
si 0 <= nr < n et 0 <= nc < n:
next_dp[nr][nc] += dp[r][c] / 8.0
dp = next_dp

retour sum(map(sum, dp))
«» "

---

*## 1.3 C++17

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
double chevalierProbabilité(int n, int k, int rang, int colonne) {
moves int const[8][2] = {
2 et 2
{ 1, -2}, { 1, 2}, { 2, -1}, { 2, 1}
};

vecteur<vecteur<double>> dp(n, vecteur<double>(n, 0,0));
dp[row][colonne] = 1,0;

pour (int step = 0; pas < k; + + step) {
vecteur<vecteur<double>> suivant(n, vecteur<double>(n, 0,0));
pour (int r = 0; r < n; ++r) {
pour (int c = 0; c < n; ++c) {
si [dp[r][c]] 0) poursuivre;
pour (auto &m : se déplace) {
Int nr = r + m[0];
int nc = c + m[1];
si (nr >= 0 && nr < n && nc >= 0 && nc < n) {
suivant[nr][nc] += dp[r][c] / 8.0;
}
}
}
}
dp.swap(suivant);
}

double résultat = 0,0;
pour (auto &row : dp)
pour (double v : ligne) résultat += v;
le résultat du retour;
}
};
«» "

---

- Oui. 2. Article du blog : *Probabilité de nuit sur un tableau d'échecs – Le bon, le mauvais, et le mauvais*

2.1 Pourquoi ce problème se pose (et pourquoi c'est un grand sujet d'entrevue)

- **Flair mathématique** – Il combine combinatoire, probabilité et théorie graphique d'une manière tangible et visuelle.
- **Multiple Solution Paths** – Récursion de la force brute, mémoisation, DP itérative, et même exponentiation de matrice.
- ** Contraintes évolutives** – La solution doit être efficace mais lisible; un terrain de jeu parfait pour démontrer des compromis algorithmiques.

Si vous appliquez pour des rôles d'ingénierie logicielle qui mettent l'accent sur la pensée algorithmique (Google, Amazon, Facebook, etc.), la maîtrise de ce problème montre que vous pouvez:

- Traduire une description en langue naturelle dans un état formel.
- Optimisez les boucles imbriquées.
- Équilibrez les compromis entre l'espace temporel.

2.2 Le bon – la solution de DP classique

**Ce qu'il fait:**
Le tableau DP garde une trace de *combien de façons* (ou équivalent, *quelle probabilité*) le chevalier peut atteindre chaque cellule de planche après un certain nombre de mouvements.

**Pourquoi c'est bon:**

Caractéristique Explication
C'est pas vrai.
**Complexité du temps**= `O(k · n2)` – linéaire dans le nombre de mouvements et de cellules de planche. Autres
**Complexité de l'espace**"O(n2)" – seulement deux grilles `n × n` sont nécessaires. Autres
**Simplicité**= Transition en état clair; facile à déboguer. Autres
**Extensibilité**= Ajouter plus de mouvements (par exemple, un chevalier super) est un changement insignifiant. Autres

**Code type (Java)** – voir ci-dessus.

---

2.3 La mauvaise – Une approche naïve et récursive

** À quoi ça ressemble :**
Une première recherche en profondeur explorant toutes les séquences de déplacement possibles de 8n, en taille lorsqu'un déplacement quitte le tableau.

**Pourquoi c'est mauvais:**

- **Exponential Blow-up** – Même pour `k = 10`, il y a 810 km 1 073 741 824 sentiers.
- **Travail redondant** – De nombreux sous-problèmes sont recalculés (par exemple, atteindre la même cellule après le même nombre de déplacements).
- **Risque de dépassement de l'échelle** – Une récursion profonde peut atteindre la limite de l'échelle d'appel pour un *k* plus grand.

**Attention:**
Utilisez la mémoisation pour stocker la probabilité d'atteindre une cellule à une étape donnée. Cela transforme essentiellement la récursion en DP.

---

#### 2.4 L'Ugly – Sur-optimisation avec un tableau 3D ou un pouvoir de matrice

Bien que vous puissiez précalculer les probabilités de transition à l'aide d'un tableau 3-D ou traiter le tableau comme un graphique et utiliser une exponentiation matricielle ('Ak'), ce niveau d'optimisation est rarement nécessaire dans les entrevues :

- **3-D DP** («dp[step][i][j]»») donne une formulation propre mais augmente la mémoire à «O(k · n2)» (pas grand pour «k = 100»).
- **Matrix Exposentiation** réduit le temps d'exécution à `O(log k · (n2)3)` mais nécessite beaucoup de code de plaque de chaudière et une compréhension profonde de l'algèbre linéaire.
- **Readability Hit** – Les intervieweurs pénalisent souvent les solutions qui semblent intelligentes mais sont difficiles à suivre.

N'utilisez ces astuces avancées que si vous écrivez une bibliothèque de qualité de production ou si vous vous attaquez à un suivi *théorique*.

---

### 2.5 SEO Conseils – Faites sortir votre blog

L'élément SEO
C'est quoi, ça ?
**Titre** – **Probabilité de nuit sur un tableau d'échecs : DP, Récursion, et puissance de matrice expliquée*** Capture le mot-clé "Probabilité de nuit" + *
**Meta Description** – Extrait de 155 caractères contenant l'identifiant de question et les termes clés. Améliorez le taux de clic sur les résultats de recherche. Autres
**En-têtes** – H1, H2, H3 avec mots-clés. Les moteurs de recherche analysent la hiérarchie du contenu. Autres
**Code Snippets** – Chaque langue est enveloppée dans `<pre><code>` des étiquettes. Plus facile pour les lecteurs (et les robots) à analyser. Autres
**Anchor Links** – #the-good, #=the-bad, #=the-ugly améliore la navigation et le référencement. Autres
**Liens internes/externes** – Lien vers la page LeetCode, problèmes similaires (par exemple, jeu de saut super). Signale la pertinence. Autres

---

#### 2.6 Mettre tout ensemble – un récit de préparation à l'emploi

Quand vous êtes dans une entrevue, décrivez le problème comme:

1. **Définition de l'état** – Let=s trace la probabilité que le chevalier soit sur chaque cellule après *t* se déplace. (en milliers de dollars)
2. **Cas de base** – Initialement, la probabilité est 1.0 à la cellule de départ et 0 ailleurs. (en milliers de dollars)
3. **Transition** – Chaque mouvement distribue la probabilité actuelle aux 8 destinations, divisée par 8. (en milliers de dollars)
4. **Itération** – Rupture de la transition *k* fois. (en milliers de dollars)
5. **Résultat** – Sommez la grille finale. (en milliers de dollars)

Ajouter une vérification rapide de la santé mentale (p. ex., `n=8, k=1, rang=0, col=0` → probabilité ↓ 0,125).
Cela démontre à la fois la justesse et une profondeur de pensée.

---

2.7 À emporter pour les demandeurs d'emploi

1. **Afficher les mathématiques, puis le code** – Expliquez la logique du DP avant de plonger dans l'implémentation.
2. **Remarque des compromis** – Mentionnez pourquoi la force brute échoue et comment DP la résout.
3. **Keep It Clean** – Utilisez des constantes pour les mouvements, les clauses de garde et les noms de variables claires.
4. **Talk About Variants** – Mentionnez que le même cadre DP peut résoudre les variantes *Super Knight* (10-move) ou *Hexa-Knight* (5-move).
5. **Lien Retour à votre portefeuille** – Si vous hébergez votre code sur GitHub, incluez un lien (par exemple, `https://github.com/votre-repo/nuit-probabilité`).

**Résultat:** Les intervieweurs verront que vous pouvez:

- **Interpret** l'énoncé du problème,
- **Choisir** un algorithme approprié,
- **Mise en oeuvre** en plusieurs langues,
- **Expliquer** le raisonnement—exactement l'ensemble des compétences pour lesquelles ils chassent.

---

- Oui. 3. Liste de contrôle rapide pour votre entrevue

Poste Statut Pourquoi ça compte
C'est-à-dire
Comprendre le tableau comme un graphique Aide à la modélisation de l'état
Master the 8 Knight se déplace
La plupart des solutions d'entretien
Mention mémoization vs force brute
Discutez des compromis entre le temps et l'espace.
Optionnel: Exponentiation de la matrice

Bon codage, et bonne chance sur votre prochain entretien d'algorithme! C'est ce qu'il a dit