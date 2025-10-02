---
titre: LeetCode 568. Jours de vacances maximum -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. Jours maximums de vacances – Code, analyse et SEO-Ready Blog

> **Source problématique:** LeetCode dur
> **Concepts clés:** Programmation dynamique, Compression d'État, Traversal graphique
> **Idéal pour :** Entretiens logiciels (Java/Python/C++)

---

### TL;DR

Nous conservons une table DP `dp[city]` qui stocke les *maximum* jours de vacances réalisables **de la semaine en cours à la fin** si nous sommes dans la "ville" au début de cette semaine.
Nous entrons dans les semaines **en arrière** (de la semaine `k-1` à la semaine `0`).
Pour chaque ville, nous considérons :

1. **Restez** – prenez les jours de vacances de cette ville dans la semaine en cours.
2. **Vol** – choisissez une ville que nous pouvons rejoindre par un vol direct, prenez ses jours de vacances pour la semaine en cours et ajoutez la meilleure valeur future ('dp[dest]').

La réponse finale est `dp[0]` parce que nous commençons à la ville `0` lundi.

Complexité
- **Heure:** "O(k * n2)" (k ≤ 100, n ≤ 100 → ~1 000 000 ops)
- **Espace:** `O(n)` pour le tableau DP (deux tableaux de longueur `n`).

---

Récapitulation des problèmes

Vous êtes dans un monde de **n villes** et **k semaines**.
- Les vols sont dirigés (matrice « vol[n][n]» – 1 = vol disponible, 0 = aucun).
- Chaque semaine vous pouvez *voler* **une fois** – seulement le lundi matin.
- `days[n][k]` donne le maximum de jours de vacances que vous pouvez prendre en ville `i` pendant la semaine `j`.
- Oui. Vous pouvez rester plus longtemps que les jours autorisés, mais seulement les jours autorisés comptent.
- Ville de départ: `0` le lundi de la semaine 0.

**Objectif:** Maximiser le nombre total de jours de vacances sur toutes les semaines.

---

Solution (PDD)

Voici une mise en œuvre concise et prête à la production dans **Java, Python et C++**.
Toutes les versions partagent la même logique, seule la syntaxe diffère.

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
Int public maxVacationDays(int[]] vols, int[] jours) {
si (jours) 0) retour 0;
int n = nombre de jours;
int k = jours[0]. longueur;

// dp[city] = maximum de jours de vacances de la semaine en cours à la fin si nous sommes à 'city '
int[] dp = nouvelle int[n];
// Semaines d' itération de la dernière à la première
pour (int semaine = k - 1; semaine >= 0; -semaine) {
int[] suivante = nouvelle int[n];
pour (int cur = 0; cur < n; ++cur) {
// Option 1: séjour dans la ville actuelle
suivant[cur] = jours[cur] + dp[cur];

// Option 2: voler vers une ville accessible
pour (int dest = 0; dest < n; ++ dest) {
si [flights[cur][dest]] 1) {
suivant[cur] = Math.max(next[cur],
jours [dest] [semaine] + dp[dest];
}
}
}
dp = suivant;
}
retour dp[0]; // début à la ville 0
}
}
«» "

- Oui. 2. Python

'`python
Solution de classe:
def maxVacation Jours(même, vols: Liste[Liste[int]],
jours: Liste[Liste[int]]) -> Int:
si non jours:
retour 0
n, k = len(jours), len(jours[0])
dp = [0] * n
pour la semaine en marche arrière(fourchette(k)):
nxt = [0] * n
pour cur dans la plage(n):
Reste
nxt[cur] = jours[cur] + dp[cur]
♪ voler
pour les déchets dans la plage(n):
si des vols[cur][destinés]:
nxt[cur] = max(nxt[cur],
jours[dest][semaine] + dp[dest])
dp = nxt
retour dp[0]
«» "

- Oui. 3. C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int maxVacationDays(std::vector<std::vector<int>>&vols,
std::vector<std::vector<int>>& jours) {
si (jours.vide()) retourne 0;
int n = jours.size();
int k = jours[0].size();
à:vecteur<int> dp(n, 0);

pour (int semaine = k - 1; semaine >= 0; -semaine) {
std::vector<int> suivant(n, 0);
pour (int cur = 0; cur < n; ++cur) {
// Séjour dans la ville actuelle
suivant[cur] = jours[cur] + dp[cur];
// Voler vers des villes accessibles
pour (int dest = 0; dest < n; ++ dest) {
si [flights[cur][dest]] 1) {
suivant[cur] = md::max(next[cur],
jours [dest] [semaine] + dp[dest];
}
}
}
dp.swap(suivant);
}
retour dp[0];
}
};
«» "

---

Pourquoi ça marche ?

1. **Définition de l'État** – «dp[city]» détient la valeur future optimale d'une ville donnée.
Cela évite la recomputation et capture la dépendance entre les semaines.

2. **Itération en arrière** – À partir de la dernière semaine s'assure que lorsque nous calculons la semaine `w`, toutes les semaines futures (`w+1...k-1`) sont déjà optimales.

3. **Deux choix par semaine** – Rester ou voler.
Parce que les vols ne sont que le lundi, la seule décision qui compte pour la semaine suivante est *où vous finissez* après le vol du lundi.

4. **Graphique traversant** – La boucle intérieure au-dessus de `est` explore tous les vols sortants de `cur`.
La complexité reste acceptable parce que «n ≤ 100».

---

Tableau de complexité

Langue Heure Espace
- C'est quoi ?
"O(k * n2) " Autres
Python : "O(k * n2) " Autres
C++=O(k * n2)=O(n)= Autres

---

Conseils pour les intervieweurs et les candidats

C'est bien, c'est mal.
C'est quoi ?
Utiliser des noms de variables clairs (`dp`, `next`). Éviter les tailles de tableau de codage dur. Oubliez de gérer les cas de bord ('jour' vide). Autres
**Bon**= Expliquez l'état du DP et pourquoi nous itérer à l'envers. Écrire des tests unitaires pour les boîtiers d'angle (pas de vols, tous les vols). Passer la preuve que rester dans la même ville est toujours considéré. Autres
Voir comment transformer la récurrence en code. Sur-commenter chaque ligne. Utiliser la récursion sans mémoisation → débordement de la pile. Autres
Remarquez que la solution peut être optimisée à `O(k * n + k * m)` où `m` est le nombre de bords si les listes d'adjacence sont utilisées. Ne pas optimiser davantage l'espace lorsque `n` peut être grand. Une mauvaise interprétation de "vol seulement lundi" conduisant à une mauvaise récurrence de DP. Autres

---

Article de blog optimisé du SEO

> **Titre:** Master LeetCode 568: Jours maximums de vacances – Java, Python, C++ Solutions et conseils d'entrevue
> **Meta Description:** Découvrez comment résoudre le LeetCode Hard #568 jours de vacances maximum avec le code Java, Python et C++. Comprendre l'approche du PDD, analyser la complexité et obtenir des conseils pour l'entrevue.

---

- Oui. 1. Présentation

Code du leet **Vacances maximales Days** est un problème de programmation dynamique classique qui teste votre capacité à gérer les transitions d'état sur un graphique. Avec **n villes** et **k semaines**, vous devez planifier des vols et des vacances pour maximiser le nombre total de jours de repos. Dans cet article, nous disséquons le problème, présentons des solutions Java, Python et C++ propres, et discutons des pièges à éviter lors des interviews.

---

- Oui. 2. Aperçu du problème

- **Vols**: «vols[i][j] = 1» signifie un vol direct de la ville «i» à «j».
- ** Limites de variation**: «jours [i][w]» est le maximum de jours de vacances que vous pouvez prendre en ville `i` pendant la semaine `w`.
- **Règlement** :
- Vous commencez en ville '0' la semaine 0 lundi.
- Les vols ne sont effectués qu'une fois par semaine, lundi.
- Un jour de vol compte vers la ville de destination des jours de vacances.

Votre objectif : ** Maximiser le nombre total de jours de vacances** sur les "k" semaines.

---

- Oui. 3. Intuition et formulation DP

Nous traitons chaque semaine comme une transition **état**.
Laissez "dp[ville]" indiquez le nombre maximal de jours de vacances possibles de la semaine *current* à la fin si vous êtes dans la "ville" au début de cette semaine.

Transition (pour la semaine "w"):
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * "
- ** Vol**: Pour chaque «est» accessible, «days[est][w] + dp[est] "

Le meilleur de ces deux donne la nouvelle valeur pour la "ville" de la semaine précédente.
Nous itérer des semaines à l'envers afin que toutes les semaines futures ('w+1...k-1') soient déjà optimales.

---

- Oui. 4. Passage du code

C'est vrai. Java

[Source complète indiquée dans la section "Solution" ci-dessus.]

Python

[Source complète ci-dessus.]

C++

[Source complète ci-dessus.]

---

- Oui. 4. Analyse de la complexité

avec «n ≤ 100» et «k ≤ 100»:

- **Heure**: "O(k * n2)" – jusqu'à 1 000 000 opérations, facilement dans les limites.
- **Espace**: `O(n)` – deux tableaux DP de longueur `n`.

---

- Oui. 5. Pièges d'entrevue

Autres Qu'est-ce que **Éviter**
-- -- -- -- -- -- -- --
Autres Pas des semaines itératrices à l'envers. Autres
Autres Ignorer le vol de lundi provoque une récurrence invalide. Autres
En utilisant la récursion simple sans mémoisation. Autres
Autres Sur-optimisation avec les listes d'adjacence sans besoin. Autres

---

- Oui. 6. Au-delà

Si vous voulez serrer la performance plus loin:
- Conservez le graphique comme une liste ** d'adjacence** (vecteur de vecteurs) pour sauter des vols impossibles.
- Réduire la boucle intérieure à "O(m)" où `m` est le nombre de bords, au lieu de `n2`.
- Oui. Cela donne du temps `O(k * (n + m)` – encore trivial pour les contraintes.

---

- Oui. 7. Pensées finales

LeetCode 568 est un problème DP *state-compression* qui mélange graphe traversal avec tabulation.
En définissant correctement «dp[city]» et en itérant des semaines à l'envers, nous transformons un graphe‐DP=» potentiellement désordonné en un algorithme propre, O(k · n2).

**Vous voulez briller dans votre prochain entretien? * *
- Pratique expliquant l'état et la récurrence du DP.
- Ecrivez un code concis dans la langue choisie.
- Oui. Cas de bord d'essai (pas de vol, tous les vols).
- Gardez une note mentale des compromis temps/espace.

Bon codage – et que vos jours de vacances soient toujours maximisés! (en milliers de dollars)

---

N'hésitez pas à laisser un commentaire ci-dessous si vous souhaitez discuter des variations de ce problème ou si vous avez besoin d'aide pour affiner vos réponses à l'entrevue. Joyeux entretien !