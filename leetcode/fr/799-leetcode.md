---
titre: LeetCode 799. Tour du Champagne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Tour de Champagne – LeetCode 799
**Un problème de PDD de niveau moyen qui frappe les recruteurs* *

> **Mots clés** – LeetCode, Tour de Champagne, programmation dynamique, problème d'entrevue, Java, Python, C++, algorithme, entretien de codage, entretien d'emploi, défi de codage.

---

Aperçu du problème

Sur le problème de LeetCode **799 – Tour de Champagne** on vous donne une pyramide de lunettes:

- La rangée 0 a 1 verre, la rangée 1 a 2 verres, ... la rangée 99 a 100 verres.
- Chaque verre peut contenir exactement **1 unité** de champagne.
- Vous versez des tasses dans le verre.
- Oui. Si un verre déborde, l'excédent est fractionné ** uniformément** entre les deux verres directement en dessous.
- Tout ce qui déborde de la rangée inférieure tombe par terre.

> **Objectif** – Après que tout le champagne ait été versé, retournez la pleine (0–1) du verre à `(query_row, request_glass)` Oui.

> **Constraints**
> `` "
> 0 ≤ coulé ≤ 10^9
> 0 ≤ requête < 100
> 0 ≤ request_glass ≤ request_row
> `` "

> **Exemple**
> versé = 2, requête_row = 1, requête_verre = 1 → **0.5**

---

- Oui. Pourquoi les recruteurs aiment ce problème

Raison Pourquoi c'est important
-- -- -- -- -- --
**La programmation dynamique (DP)**Shows vous permet de modéliser un problème de flux réel avec DP. Autres
**Simulation + Débordement** , Démontre une manipulation soigneuse des cas de point flottant arithmétique et de bord. Autres
**Time/Space O(r2)** Autres
**Language-agnostic** , facilement résolu en Java, Python ou C++ – idéal pour les interviews. Autres

Si vous pouvez expliquer votre solution et présenter un code propre et lisible, vous obtiendrez un "thumbs-up" dans toute entrevue technique.

---

- Oui. L'idée fondamentale – Simulation des lignes par lignes

Pensez à la tour comme au Triangle du Pascal** où chaque entrée est la quantité de champagne qui arrive à ce verre.
Le processus:

1. **Initialize** `tower[0][0] = versé`.
2. Pour chaque verre `tour[r][c]` à la ligne `r` (jusqu'à `query_row`):
- Si `tower[r][c] > 1`, calculer l'excédent ****:
```excès = (tour[r][c] - 1) / 2.0```
- Ajouter cet excès aux deux verres ci-dessous :
```tower[r+1][c] += excès`` "
```tower[r+1][c+1] += excès`` "
3. Après simulation, la réponse est `min(1.0, tour[query_row][query_glass]'.

> **Pourquoi min(1.0)? **
> Un verre ne peut jamais contenir plus d'une unité. La simulation peut calculer une valeur plus élevée si le flux entrant est énorme; nous le serrerons à 1.

---

Analyse de complexité

- **Time** – Nous visitons chaque verre jusqu'à `query_row`.
\[
T = 1 + 2 + \dots + (\text{query_row}+1) = O(\text{query_row}^2)
\]
Avec `query_row ≤ 99`, c'est trivial (5 000 opérations).

- **Espace** – Un tableau 2-D de taille `(query_row+1) × (query_row+1)` → `O(query_row^2) "
Nous pouvons le réduire à un tableau 1-D de taille `query_row+1` si désiré, mais la lisibilité gagne ici.

---

C'est pas vrai. Tranche Affaire Gotchas

Pourquoi ça compte ?
- Oui.
**Pured = 0**= Tous les verres restent vides. Autres
**query_glass = 0 ou query_glass = query_row** ► Géré automatiquement par DP. Autres
**Large versée (109)** Utiliser `double`. Autres
**Floating-point precision**.Return result with 5 décimum places. Autres

---

Mise en œuvre – trois langues

#### 6.1 Java

"Java
solution de classe publique {
publique double champagneTower(int versé, int requête_row, int requête_glass) {
Si (pourvu) 0) retourner 0,0;

double[][] tour = nouveau double[query_row + 2][query_row + 2];
tour[0][0] = coulé;

pour (int r = 0; r < requête_row; r++) {
pour (int c = 0; c <= r; c++) {
double excédent = (tour[r][c] - 1,0) / 2,0;
si (excès > 0) {
tower[r + 1][c] += excédent;
tower[r + 1][c + 1] += excédent;
}
}
}

retourner Math.min(1.0, tour[query_row][query_glass]);
}
}
«» "

> **Pourquoi 2-D?** Garde le code lisible. Le tableau est minuscule (= 102 × 102).

---

6.2 Python

'`python
Solution de classe:
def champagne Tower(self, versé: int, requête_row: int, requête_glass: int) -> flotteur:
si versé == 0:
retour 0,0

# initialiser les lignes (query_row+2) pour faciliter la manipulation de l'index
tour = [[0,0] * (query_row + 2) pour _ in range(query_row + 2)]
tour[0][0] = coulé

pour r dans range(query_row):
pour c dans la plage (r + 1):
Excédent = (tour[r][c] - 1,0) / 2,0
si excès > 0:
de la tour[r + 1][c] += Excédent
tour[r + 1][c + 1] += excédent

retour min(1.0, tour[query_row][query_verre])
«» "

> **Conseil de python** – La compréhension de la liste construit une matrice 2-D propre.

---

*### 6.3 C++

'`cpp
solution de classe {
public:
double champagne Tower(int versé, int requête_row, int requête_glass) {
Si (pourvu) 0) retourner 0,0;

vecteur<vecteur<double>> tour(query_row + 2,
vecteur<double>(query_row + 2, 0,0)
tour[0][0] = coulé;

pour (int r = 0; r < requête_row; ++r) {
pour (int c = 0; c <= r; ++c) {
double excédent = (tour[r][c] - 1,0) / 2,0;
si (excès > 0) {
tower[r + 1][c] += excédent;
tower[r + 1][c + 1] += excédent;
}
}
}

retour min(1.0, tour[query_row][query_glass]);
}
};
«» "

> **Pourquoi `vecteur<vecteur<double>>`? **
> Le C++ STL rend l'attribution dynamique simple, et la taille est toujours < 200 × 200.

---

## 7-- Une variante unique (facultative)

Si vous voulez impressionner les recruteurs que vous pouvez *optimiser* la mémoire, voici le tour 1-D (style Java):

"Java
double[] dp = nouveau double[query_row + 2];
dp[0] = versé;
pour (int r = 0; r < requête_row; r++) {
pour (int c = r; c >= 0; c--) { // itérer en arrière!
double excédent = (dp[c] - 1,0) / 2,0;
si (excès > 0) {
dp[c] += excédent;
dp[c + 1] += excédent;
}
}
}
retourner Math.min(1.0, dp[query_glass]);
«» "

* L'itération en arrière* garantit que les valeurs de la ligne courante ne sont pas écrasées avant leur utilisation.

---

C'est pas vrai. Comment présenter Ceci dans une interview

1. **Énoncer les hypothèses** – p.ex., "We"ll simulent rang par rang, serrer tout verre jusqu'à un maximum de 1. (en milliers de dollars)
2. ** Dessiner un diagramme rapide** – Montrez une petite tour de 3 rangées et comment coule le débordement.
3. **Exposer la récurrence du PDD** – Dépassement = `(montant actuel – 1) / 2`.
4. **Va à travers un échantillon** – Utilisez le tableau 2-D pour illustrer les calculs.
5. **Complexité de la concentration** – temps O(r2), espace O(r2) ; trivial pour r < 100.
6. **Parler sur les boîtiers de bord** – sortie anticipée pour "aspiré".

> **Astuce** – Conservez la réponse à 5 décimales : `System.out.printf("%.5f\n", ans);` (Java) ou `format(ans, '.5f')` (Python).

---

## 8-

- **Comprendre le flux** – Il ne s'agit pas seulement d'ajouter 1; il s'agit de *combien de débordements*.
- **DP + Simulation** – Un mélange parfait de pensée algorithmique et d'implémentation soignée.
- **Language-agnostic proof** – Montrez la même logique en Java, Python et C++ pour prouver la polyvalence.
- **Clarité > Micro-optimisation** – Les recruteurs se soucient plus de la logique propre que de serrer un octet.

> **Pro‐tip:** Lorsque vous écrivez votre propre solution LeetCode, ajoutez un commentaire en haut avec le lien de problème et une brève description. Cela indique que vous êtes organisé et préparé.

---

Résumé du SEO

> *=Champagne Tower==* est un défi commun d'entrevue de LeetCode qui teste la programmation dynamique, la simulation et la manipulation de cas de bord. Le problème est soluble en Java, Python ou C++ avec un simple DP ligne par ligne. Cet article vous guide dans la logique, analyse la complexité, énumère les pièges et fournit des extraits de code propres. Utilisez ceci comme un point de discussion dans votre prochaine entrevue de codage, et vous allez démontrer de solides côtelettes algorithmiques que les recruteurs aiment.

---