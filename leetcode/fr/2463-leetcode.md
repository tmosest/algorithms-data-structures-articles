---
titre: LeetCode 2463. Distance totale minimale parcourue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2463 – Distance totale minimale parcourue
**Hard** – solutions résolues à 100 %, acceptation à 100 %**

---

Récapitulation des problèmes

Vous êtes donné

"usine" Autres
C'est pas vrai.
"robot[i]" – la position de l'axe X du robot *i* – position et combien de robots cette usine peut réparer

Tous les robots commencent cassés et sont libres de choisir **une** direction (gauche ou droite) au tout début.
Ils se déplacent à la même vitesse, jamais en collision, et s'arrêtent quand ils atteignent une usine qui a encore une fente de rechange.
Si une limite d'usine est atteinte, le robot passe simplement par elle.

**Objectif:**
Réglez les directions initiales pour que *chaque* robot soit réparé et la distance totale parcourue** est **minimum**.

> **Constraints**
> 1 ≤ longueur robot, longueur usine ≤ 100 '
> • `-109 ≤ robot[i], usine[j][0] ≤ 109 "
> 0 ≤ usine[j][1] ≤ robot.longueur "
> • Il est toujours possible de réparer tous les robots.

---

- Oui. Pourquoi ça semble dur

Les robots sont libres de marcher dans les deux sens, et les usines ont des capacités différentes.
Une naïveté envoie chaque robot à son usine la plus proche, parce qu'une usine peut être épuisée, forçant un robot à aller plus loin.

Le point de vue clé :
**Une fois que les robots et les usines sont triés sur l'axe X, l'affectation optimale utilisera toujours un bloc *contitueux* de robots pour chaque usine. * *
Pourquoi ?
Déplacer un robot à gauche alors qu'un robot plus proche va à droite augmenterait la distance totale en raison de la convexité de la fonction de valeur absolue.

Avec cette propriété nous pouvons résoudre le problème par une programmation dynamique sur les positions triées.

---

Aperçu de la solution (DP)

1. **Trier**
* "robots" – ascendant par position
* "usines" – ascendant par position

2. **État du PD**
`dp[i][j]` – distance totale minimale pour réparer les premiers robots `i` utilisant les premières usines `j` (tous les robots `i` sont garantis pour être réparés).

3. **Transition**
Pour chaque usine `j` nous décidons combien de derniers robots `k` (`k` de `0` à `limit[j]`) sont réparés par elle:

Texte
dp[i][j] = min sur k ( dp[i-k][j-1] + coût(robots[i-k+1 ... i] → usine[j]) )
«» "

4. **Coût**
`cost(l ... r → pos)` = -robots[p] – p = L ... r.
Depuis `m ≤ 100`, nous pouvons calculer cela en O(m) à la volée; il est bon marché et garde l'implémentation simple.

5. **Réponse**
`dp[m][n]` où `m = robots.size()` et `n = usines.size()`.

---

La preuve de l'exactitude

*Lemme 1 – Affectation contiguë*
Pour toute solution optimale, si les robots `a < b < c` sont réparés par l'usine `f` et `d` (`a < d < b`) sont réparés par une autre usine, l'échange `d` avec `b` ne peut pas augmenter la distance totale.
La preuve utilise l'inégalité du triangle et la convexité de l'équation – y.
Ainsi, une solution optimale peut être ré-ordonnée pour que les robots assignés à une usine donnée forment un bloc contigu.

*Lemme 2 – PDD Récurrence*
Supposons que nous avons réparé les premiers robots `i-k` en utilisant de manière optimale les premières usines `j-1` (`dp[i-k][j-1]`).
Ajout de l'usine `j` pour réparer les robots `i-k+1 ... i` fournit une solution valable pour les premiers robots `i` utilisant les premières usines `j`, et son coût est exactement l'expression de transition.
Toute solution optimale doit être construite de cette façon en raison de Lemma 1.
Par conséquent, «dp[i][j]» conserve le coût optimal de ce sous-problème.

*Theorem* – `dp[m][n]` correspond à la distance totale minimale requise pour réparer tous les robots.
En intronisant sur `i` et `j`, le PDD explore toutes les allocations possibles en respectant les limites des usines, et par Lemma 2 chaque allocation optimale est envisagée.
Par conséquent, l'algorithme est correct. *

---

C'est vrai. Analyse de complexité

Étape
C'est quoi ?
Tri des robots Autres
Classer les usines Autres
Lignes de PDD
Autres Calcul des coûts par transition, mais constante amortie en raison de petites contraintes
**Total** (~104)

Les deux sont facilement dans les limites de Java, Python et C++.

---

#### 6.

Mauvaise pratique
- C'est quoi ?
Autres Ne pas trier d'abord.Les affectations peuvent croiser les usines, menant à des solutions sous-optimales ou invalides.
Autres Oubliant qu'un robot peut démarrer *à* une usine
Autres Utilisation d'une usine cupide, viole les contraintes de capacité, augmente la distance
Autres Calcul des coûts sur-optimisation avec des maths complexes

---

Mise en œuvre du code

Voici des solutions propres et commentées dans **Java, Python et C++**.
Chacun suit l'approche du PDD décrite ci-dessus.

---

Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
public long minimum TotalDistance(Liste<entier> robot, usine int[]) {
int m = robot.size();
int n = usine. longueur;

// 1. Tri des robots et des usines par position
Collections.sort(robot);
les tableaux.sort(usine, comparator.comparingInt(a -> a[0]);

// Convertir les robots en tableau pour l'indexation rapide
long[] r = nouveau long[m];
pour (int i = 0; i < m; ++i) r[i] = robot.get(i);

// 2. Table DP (utiliser longtemps pour éviter les débordements)
long[] dp = nouveau long[m + 1][n + 1];
pour (int i = 0; i <= m; ++i)
Tableau.fill(dp[i], Long.MAX_VALUE / 4);
dp[0][0] = 0;

// 3. PDD transition
pour (int j = 1; j <= n; ++j) {
int pos = usine[j - 1][0];
limite int = usine[j - 1][1];

pour (int i = 0; i <= m; ++i) {
// envisager d'assigner des robots k (0...limit) à cette usine
pour (int k = 0; k <= limite && k <= i; ++k) {
long prev = dp[i - k][j - 1];
si (prev == Long.MAX_VALUE / 4) continuer;

// coût du déplacement des robots (i-k .. i-1) vers cette usine
coût long = 0;
pour (int p = i - k; p < i; ++p)
coût += Math.abs(r[p] - pos);

dp[i][j] = Math.min(dp[i][j], prev + coût);
}
}
}
retour dp[m][n];
}
}
«» "

---

Python (Python 3,11)

'`python
de taper l'importation Liste
importer des maths

Solution de classe:
def minimum TotalDistance(même, robot: List[int], usine: List[List[int]]) -> Int:
robot.sort()
usine.sort(key=lambda x: x[0])

m, n = len(robot), len(usine)
r = robot

INF = 10 ** 18
dp = [[INF] * (n + 1) pour _ dans la plage (m + 1)]
dp[0][0] = 0

pour j dans la plage(1, n + 1):
pos, limite = usine[j - 1]
pour i dans la plage (m + 1):
pour k (limite + 1):
i k > i: rupture
si dp[i - k][j - 1] INF: continuer
coût = somme(abs(r[p] - pos) pour p dans la fourchette(i - k, i))
dp[i][j] = min(dp[i][j], dp[i - k][j - 1] + coût)

retour dp[m][n]
«» "

---

C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long minimum long TotalDistance(vecteur<int> robot, vecteur<vecteur<int>> usine) {
tri(robot.begin(), robot.end());
Tri(usine.degin(), usine.end(),
[](const vector<int>& a, const vector<int>& b){ retourner a[0] < b[0]; });

int m = robot.size(), n = usine.size();
vecteur <long long> r(robot.begin(), robot.end());

Const. longue INF = 4e18;
vectorielle<vector<long long>> dp(m + 1, vectorielle<long long>(n + 1, INF);
dp[0][0] = 0;

pour (int j = 1; j <= n; ++j) {
int pos = usine[j-1][0];
limite int = usine[j-1][1];
pour (int i = 0; i <= m; ++i) {
pour (int k = 0; k <= limite && k <= i; ++k) {
si (dp[i-k][j-1] == INF) continuer;
coût long = 0;
pour (int p = i-k; p < i; ++p)
coût += llabs(r[p] - pos);
dp[i][j] = min(dp[i][j], dp[i-k][j-1] + coût;
}
}
}
retour dp[m][n];
}
};
«» "

> **Note :**
> Les trois implémentations utilisent une boucle triple-nested mais restent confortablement à l'intérieur du budget d'opération **106** parce que `m, n ≤ 100`.

---

- Oui. Ce qui fait sortir cette solution

**Beau**
C'est quoi ?
• Intuitive DP après tri. • Oublier de gérer les coordonnées négatives – peut conduire à un débordement ou de mauvais résultats. Autres
• Coût calculé avec une simple boucle – pas de maths délicats. • Greedy l'usine de nearest est tentant mais faux. Autres
• Fonctionne dans toutes les langues principales avec un minimum de mémoire supplémentaire. Autres

---

- Oui. Bonus: Coût plus rapide (facultatif)

Si vous souhaitez réduire le facteur constant, vous pouvez pré-calculer les montants de préfixe des positions du robot et ensuite utiliser la formule

«» "
Coût(l ... r → pos) =
(pos * k) - (préfixe[r] - préfixe[l-1]) si les robots sont à gauche de pos
(préfixe[r] - préfixe[l-1]) - (pos * k) sinon
«» "

mais pour les limites données, la boucle simple est **claire** et moins sujette à erreur.

---

#####=" SEO Cheat- Feuille

Mot-clé
- Oui.
Titre, lien de problème, commentaire de code
En-tête, description du problème
"programmation dynamique" Aperçu de la solution, section DP
"Java python c++ solution"
"problème d'usine de robots" Exemple, section « cas de bord »
Réparation de robots Problème narratif

Ajoutez-les à votre blog, article ou README et vous vous classez pour chaque recherche qu'un LeetCoder fait sur ce puzzle !

---

LT;DR

* Trier les robots et les usines → DP sur les positions triées → Transition : "assigner les derniers robots k à l'usine actuelle" → O(106) temps, O(104) mémoire.
Les trois langues principales: **Java, Python, C++** – prêt à copier-coller.

Parfait.
Mauvais.
Mince.
Maintenant c'est tout ** FAIT**!

Bon codage, et que votre distance totale reste minimale!