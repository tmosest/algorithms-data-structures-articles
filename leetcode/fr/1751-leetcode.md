---
titre: LeetCode 1751. Nombre maximum d'événements qui peuvent être assistés II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Voici des solutions propres et conviviales pour **LeetCode 1751 – Nombre maximal d'événements auxquels on peut assister II**.
Les trois implémentations suivent la même idée :

1. **Début** d'ici leur fin de journée.
2. Pour chaque événement, **binaire-recherche** le dernier événement sans chevauchement.
3. Utiliser **DP** `dp[i][j]` – la valeur maximale réalisable en considérant les premiers événements triés `i` et en choisissant au plus `j` d'entre eux.

Langue Heure Espace Remarques
C'est pas vrai.
*Java** * O(N·K + N·log N) * O(N·K) * Utiliser `int[]]` pour DP. Autres
**Python** Utiliser `list[list[int]]`. Autres
**C++**= O(N·K + N·log N)== O(N·K)= Utiliser `vecteur<vecteur<long>>`. Autres

> **Pourquoi `long` / `long`?**
> `valeur` peut être jusqu'à `10^6` et `k·n` jusqu'à `10^6`, de sorte que la réponse peut atteindre `10^12`. Les entiers 64 bits évitent le débordement.

---

#### 1.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
valeur(int[]] événements, int k) {
// 1. Tri par jour de fin
Arrays.sort(événements, a, b) -> Integer.compare(a[1], b[1]));

int n = événements. longueur;
// dp[i][j] – meilleure valeur en utilisant les premiers événements i, prenant au plus j
long[] dp = nouveau long[n + 1][k + 1];

pour (int i = 1; i <= n; i++) {
int[] ev = événements[i - 1];
int prev = findLastNonOverlap(events, ev[0]); // recherche binaire

pour (int j = 1; j <= k; j++) {
long skip = dp[i - 1] [j];
longue durée = dp[prev + 1] [j - 1] + ev[2];
dp[i][j] = Math.max(skip, prise);
}
}
retour (int) dp[n][k];
}

// retourne l'index du dernier événement dont la fin < commence, -1 si aucun
privé int findLastNonOverlap(int[][] événements, int start) {
int l = 0, r = événements.longueur - 1, res = -1;
pendant que (l <= r) {
m = l + (r - l) / 2;
si (événements[m][1] < début) {
res = m;
l = m + 1;
} autre {
r = m - 1;
}
}
retour rés;
}
}
«» "

---

#### 1.2 Python

'`python
de bisect importer bisect_left
de taper l'importation Liste

Solution de classe:
def maxValue(self, events: List[List[int]], k: int) -> Int:
# 1. Tri par jour de fin
events.sort(key=lambda x: x[1])

n = len(événements)
# dp[i][j] – meilleure valeur en utilisant les premiers événements i, prenant au plus j
dp = [[0] * (k + 1) pour _ dans la plage (n + 1)]

# liste des jours de fin de recherche binaire
fin = [e[1] pour e dans les événements]

pour i dans la plage(1, n + 1):
s, e, val = événements[i - 1]
# dernier événement qui se termine avant s
prev = bisect_left(fins, s) - 1

pour j dans la plage (1, k + 1):
skip = dp[i - 1] [j]
prise = dp[prev + 1] [j - 1] + val
dp[i][j] = max(skip, prendre)

retour dp[n][k]
«» "

---

*## 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxValue(vector<vector<int>>& events, int k) {
// 1. Tri par jour de fin
tri(events.begin(), events.end(),
[](const auto& a, const auto& b) { retourner a[1] < b[1]; });

int n = events.size();
vecteur <long> extrémités(n);
pour (int i = 0; i < n; ++i) fin[i] = événements[i][1];

// dp[i][j] – meilleure valeur en utilisant les premiers événements i, prenant au plus j
vector<vector<long long>> dp(n + 1, vector<long long>(k + 1, 0));

pour (int i = 1; i <= n; ++i) {
int s = événements[i - 1][0];
int val = événements[i - 1][2];

// dernier événement qui se termine avant s
int prev = int(upper_bound(ends.begin(), end.end(), s - 1) - end.begin() - 1;

pour (int j = 1; j <= k; ++j) {
long saut long = dp[i - 1] [j];
longue durée = dp[prev + 1] [j - 1] + val;
dp[i][j] = max(skip, prise);
}
}
retourner static_cast<int>(dp[n][k]);
}
};
«» "

> **Tip** – Dans C++, utilisez `upper_bound` sur le vecteur `ends` pour la recherche binaire.
> `prev = upper_bound(ends.begin(), find.end(), s - 1) - find.begin() - 1'.

---

- Oui. 2. Article de blog – Le bon, le mauvais, le mauvais de LeetCode 1751

> **Mots clés:**
> *Nombre maximal d'événements qui peuvent être assistés II *= *LeetCode 1751 *= *programme dynamique*= *recherche binaire*= *Java*== *Python*== *C++*= *interview de codage*= *entrevue d'emploi*= *conception d'algorithmes*.

2.1 Introduction

Lorsque les recruteurs poussent un problème de **niveau dur** de LeetCode sur votre pile d'entrevues, il s'agit d'un signal qu'ils testent votre architecture de résolution de problèmes* plus que votre vitesse de codage.
LeetCode 1751 – Nombre maximum d'événements auxquels on peut assister II est l'un de ces problèmes de standard or qui met en évidence:

* **Logique de planification des événements** (contraintes non excessives).
* ** Programmation dynamique** (choix vs skip).
* **Recherche binaire** pour une recherche efficace.

Dans ce billet, nous disséquerons le problème, nous passerons par une solution propre, puis nous explorerons les aspects *bons*, *mauvais* et *puissants* qui se posent dans des contextes d'entrevue réels.

---

2.2 Récapitulation du problème

**Don**

* `events[i] = [startDay, finDay, valeur]` – un événement dure de `startDay` à `endDay` inclusivement.
* Vous pouvez assister à la plupart des événements `k`.
* Les événements ne peuvent se chevaucher (deux événements qui partagent un conflit quotidien).

**Objectif**

Retournez la valeur totale maximale que vous pouvez collecter.

**Contrôles* *

* `1 <= k <= events.longueur <= 10^5`
* `k * events.longueur <= 10^6` (garanties DP table correspond en mémoire)
* `1 <= débutJour <= finJour <= 10^9`
* `1 <= valeur <= 10^6`

---

Le bien

Explication
C'est pas vrai.
**Clear DP state** – `dp[i][j]` est *précisément* la meilleure valeur pour les premiers événements `i` et au plus des choix `j`. Évite les pièges qui tuent de nombreux candidats. Autres
**Sorti à la fin de la journée** – garantit que tout événement après l'index « i » se termine plus tard que l'événement « i ». Autres
**Binary search on end days** – La recherche `O(log N)` du dernier événement compatible. Il rend l'algorithme entier `O(N·K + N·log N)` au lieu de quadratique. Autres
**Tableau DP complet** (rubriques «N × K» ≤ «10^6»). S'adapte confortablement aux limites de mémoire de l'entrevue. Autres

---

Le mal

Pourquoi ça arrive ?
C'est-à-dire
**Les grandes gammes numériques** – le «démarrage» et le «démarrage» peuvent être jusqu'à «10^9». Naïve Les solutions de jours explosent en mémoire. Autres
**Risque de dépassement** – La somme des valeurs allant jusqu'à «k» peut atteindre «10^12». Un nombre entier de 32 bits en Java/Python `int` déborde. Autres
** Explosion de la dimension PD** – répartition naïve des événements. longueur × k` sans taille peut souffler la mémoire pour 10^5 × 10^5. Autres
**Edge‐case off‐by‐one** – Fin de journée inclusive vs fin de journée exclusive en recherche binaire. Autres Un bug subtil qui ne fait que des surfaces avec un petit jeu de test. Autres

---

#### 2.4 Les Ugly

Problème Conséquence réelle
- Oui.
**Plusieurs solutions optimales** – Vous pouvez produire la bonne réponse, mais utilisez un *incorrect PD récurrence*. Les recruteurs verront toujours que vous avez compris la structure, mais ils peuvent pénaliser pour avoir manqué la solution *canonique*. Autres
**Temps-limit vs memory-limit trade-off** – L'utilisation de `vector<vector<long long>>` en C++ ou d'un tableau 2-D complet en Java peut frapper les limites de pile si elles ne sont pas soigneusement dimensionnées. Le candidat doit équilibrer la lisibilité et la performance, une tension d'entrevue classique. Autres
**Binary search implementation errors** – En utilisant `lower_bound` incorrectement ou en manquant le réglage `-1` conduit à `IndexError` ou de mauvais résultats. Autres Les intervieweurs s'attendent souvent à ce que vous *expliquiez* chaque étape; un seul malentendu peut faire dérailler la solution. Autres

---

### 2.5 Solution propre – DP + Recherche binaire

2.5.1 Idées en coque

1. **Événements de la fin du jour.
2. Pour chaque événement `i` (ordre trié) calculer `prev(i)` – le plus grand indice `< i` de sorte que `events[prev].end < events[i].start`.
* Recherche binaire sur le tableau des jours de fin (`O(log N)`).
3. Tenir à jour un tableau PDD 2D :

«» "
dp[i][j] = max( dp[i‐1][j] , // saut événement i
dp[prev(i)+1][j‐1] + événements[i].valeur ) // prendre événement i
«» "

4. La réponse finale est «dp[n][k]».

> **Pourquoi j'en ai plus que j'en ai plus exactement ?* *
> La récurrence permet naturellement de faire un skip et de gérer automatiquement le ski au maximum. Si vous voulez *exactement* `k` événements, vous pouvez vérifier `dp[n][k]` mais toujours autoriser `<k` en prenant le maximum sur `j ≤ k`.

#### 2.5.2 Détails de la recherche binaire

Parce que les événements sont triés par *fin* jour, le *dernier événement de non-overlaping* est tout simplement l'événement le plus droit dont `endDay` est `< courant.start Jour.
`bisect_left(ends, start)` retourne la première position où `end >= start`, donc soustraire 1 pour obtenir l'index valide.
Si un tel événement n'existe pas, `prev = -1`, et `dp[prev+1][...]` désigne `dp[0][...]` – le préfixe vide.

2.5.3 Complexité

* **Heure** :
* Tri – `O(N log N)`
* Pour chacun des événements `N`, recherche binaire – `O(log N)`
* Mises à jour DP – "O(N·K)" (le tableau DP contient au maximum des cellules `10^6`).
* **Total**: "O(N·K + N·log N)"

* **Espace**:
* Tableau DP – 'O(N·K) "
* Tableaux auxiliaires (événements triés, jours de fin) – `O(N)`

---

2.6 Pièges communs d'entrevue

Comment éviter
C'est quoi ?
**Utiliser `int` pour la réponse**= La réponse peut dépasser `2^31‐1'. Passez à `long`/`long long`. Autres
**Inclusive vs exclusivité day**. Utilisez `end < start` lors de la recherche. Autres
**Recherche binaire hors-par-un**=Vérifiez la logique `bisect_left` / `upper_bound`. Essai avec un petit échantillon (`[[1,2,3],[2,3,4]]`). Autres
**Plus grande entrée avec petit `k`**. Même si `k` est minuscule, vous devez encore construire une table DP de taille `(N+1) × (k+1)` parce que la récurrence dépend de "k". Autres
Autres **Wrong trier la clé**. La bonne clé est le *fin jour*. Autres

---

2.7 Variation : Nombre maximum d'événements auxquels on peut assister

LeetCode 2086 est la variante *easier* où vous pouvez assister à *au plus un* événement à la fois (`k` ne fait pas partie de l'entrée).
Le DP simplifie un tableau 1-D et utilise toujours la recherche binaire.
L'étude des deux versions crée une base solide** pour toute entrevue impliquant un calendrier d'intervalle*.

---

2.8 Entretien— Conseils prêts

Motif Autres
- Oui.
** Expliquez l'état avant de codifier** Affichez que vous comprenez le *problème-structure* – un must-have pour les entrevues seniors. Autres
**Parler à travers la recherche binaire**=Les intervieweurs adorent vous entendre peut *transformer* un événement naïf *scan tous les événements antérieurs= dans la recherche `O(log N)`. Autres
**Mention débordement**. Une remarque rapide `long`/`long` montre que vous lisez attentivement les contraintes. Autres
**Afficher l'essai d'échantillon** `k = 2` → réponse «7». Démonstrations de skip vs prise. Autres
**Discuse la complexité**= Être capable de décomposer `O(N·K)` et `O(N·log N)` en parties intuitives (triage, recherche binaire, boucles DP) impressionne les intervieweurs. Autres

---

2.9 Conclusion

LeetCode 1751 est plus qu'un problème difficile; c'est un **mini-curriculum** pour la préparation de l'entrevue:

* ** Programme des événements** – enseigne la détection des conflits.
* ** Programmation dynamique** – présente une sous-structure optimale.
* **Recherche binaire** – démontre l'optimisation algorithmique.

Le bon* est qu'un seul PDD bien structuré résout l'ensemble du problème.
Le *bad* est le risque de bugs subtils autour de dates inclusives et de débordement entier.
Le *ugly* apparaît quand les intervieweurs vous demandent de refactorer ou d'expliquer les optimisations à la volée.

**Si vous maîtrisez ce problème, vous aurez confiance en vous attaquant à tout intervalle– PDD ou question d'entrevue – une compétence clé que les recruteurs recherchent chez les candidats se préparant à des rôles de haute technologie. **

---

- Oui. 3. Takeaway final pour votre portefeuille d'entrevue

* **Mise en oeuvre** la solution DP‐BS dans **Java** (pour les rôles de moteur), **Python** (pour la science des données) ou **C++** (pour le niveau du système).
* ** Expliquer** le raisonnement clairement – *état, récurrence, transition, cas de base*.
* **Afficher** les compromis (temps vs espace) et pourquoi les contraintes permettent un PDD 2-D.

En présentant une solution propre et correcte dans trois langues populaires *et* une explication de style blog, vous aurez le **content** et la **confiance** à ace LeetCode 1751 dans une interview de codage – et impressionnerez vos futurs employeurs.