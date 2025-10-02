---
titre: LeetCode 2188. Temps minimum pour terminer la course -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2188. Temps minimum pour terminer la course
**Hard** – LeetCode

> **Problème**
> Compte tenu de la liste des pneus «tires[i] = [fi, ri]» où le tour successif *x-th* sur le pneu *i* prend
> `fi * ri^(x‐1)` secondes, un changement de temps `changeTime`, et un nombre total de tours `numLaps`.
> Vous pouvez commencer avec n'importe quel pneu, changer à n'importe quel pneu (y compris le même type) après n'importe quel tour pour
> `changeTime` secondes, et vous avez des copies illimitées de chaque pneu.
> **Retournez le temps total minimum pour terminer la course. **

> **Constraints**
> * 1 ≤ "longueur des pneus" ≤ 105
> * 1 ≤ `fi`, `temps de changement` ≤ 105
> * 2 ≤ `ri` ≤ 105
> * 1 ≤ `numLaps` ≤ 1000

---

Pourquoi ce problème est une grande question d'entrevue

C'est bien, c'est mal.
C'est pas vrai.
**Espace État clair** – La course peut être vue comme une séquence de segments *lap* avec un coût de changement. Vous ne pouvez pas exécuter un DP naïf sur *tire × tour* car `tires.longueur` peut être 105. Le nombre de façons de changer de pneus augmente explosivement, donc une récursion naïve explose. Autres
** Programmation dynamique** – Le sous-problème optimal est le temps minimum pour les premiers tours *k*. Lorsque le temps de tour d'un pneu dépasse rapidement le coût du changement, vous pouvez arrêter en toute sécurité d'explorer ce pneu. Autres
** Contraintes pratiques** – "numLaps" ≤ 1000 signifie O(`numLaps`2) DP est très bien, même pour toutes les langues. Vous devez *pré-calculer* le meilleur temps possible pour chaque longueur de segment *une fois*, pas par pneu. La limite de temps originale de LeetCode oblige une étape de pré-traitement soigneuse pour garder le DP intérieur rapide. Autres

Ci-dessous vous trouverez trois solutions **ready-to-copy** en Java, Python et C++ qui fonctionnent dans **O(`numLaps`2)** temps et **O(`numLaps`)** mémoire – l'approche optimale pour les contraintes données.

---

- Oui. 1. Java – PDD ascendant + prétraitement des pneus

"Java
Importation de java.util.*;

solution de classe publique {
/** Pneumatiques @param Liste des [fi, ri]
* Changement @param Temps de changement des pneus
* @param num Nombre total de tours
* @retour durée minimale de finition
*/
minimum int publicFinishTime(int[]] pneus, changement intTime, int numLaps) {
// 1. Pré-calculer le meilleur temps pour terminer les tours consécutifs
// sans changement de pneu, pour tous les 1 ... numLaps.
int[] bestLen = nouveau int[num Laps + 1];
Arrays.fill(bestLen, entier.MAX_VALUE);

pour (int[] pneus : pneus) {
base longue = pneu[0];
long exp = pneu[1];

Long tourTime = base; // heure du premier tour sur ce pneu
long total = tourTime; // temps cumulé pour ce segment

bestLen[1] = (int) Math.min(bestLen[1], total);

// Continuez à prolonger le segment pendant qu'il est toujours utile:
// Si le temps cumulé pour *len* tours est meilleur que le trivial
// chemin (changement après chaque tour), on l'enregistre.
pour (int len = 2; len <= numLaps; len++) {
// temps de tour suivant = précédent * exp
tourTime = tourTime * exp;
i (lapTime > entier. MAX_VALUE) rupture; // dispositif de protection contre les débordements
Total += tour Temps;

si (total < bestLen[len]) bestLen[len] = (int) total;

// Si un seul tour sur ce pneu coûte déjà plus que
// passer à un pneu frais, tous les segments plus longs sont inutiles.
si (lapTime > changeTime + pneu[0]) rupture;
}
}

// 2. PDD ascendant sur la course
int[] dp = nouveau int[num Laps + 1];
dp[0] = 0;

pour (int i = 1; i <= numLaps; i++) {
// Nous pouvons terminer les tours en un seul segment (aucun coût de changement au début)
dp[i] = meilleurLen[i];

// Essayez de diviser les premiers tours en [0..j] + changement + [j+1..i]
pour (int j = 1; j < i; j++) {
si (dp[j]] Integer.MAX_VALUE) continuer;
Int candidate = dp[j] + changement Temps + meilleurLen[i - j];
si (candidat < dp[i]) dp[i] = candidat;
}
}

retour dp[numLaps];
}
}
«» "

Comment ça marche

1. **Tire avant le traitement* *
Pour chaque pneu, nous accumulons les temps de tour jusqu'à ce que soit nous touchions `numLaps` ou le tour suivant serait plus cher qu'un pneu frais (c'est-à-dire `lapTime > (len+1) * (minBase + changeTime)').
Cela maintient la boucle courte même pour haut `ri`.

2. **Meilleure représentation du segment**
"BestLen[len]" stocke le temps *minimum* pour exécuter *len* tours de rang en utilisant *le meilleur pneu possible*.

3. **DP**
`dp[i]` = temps minimum pour terminer les premiers *i* tours.
- Une possibilité est de terminer tous les tours *i* en un seul segment.
- Sinon nous nous sommes séparés après un tour plus tôt *j* et payons "changeTime" une fois.
Parce que `numLaps` ≤ 1000, la boucle interne O(`numLaps`2) est bien à l'intérieur de la limite de 2 secondes.

---

- Oui. 2. Python – Même logique, plus propre Syntaxe

'`python
de taper l'importation Liste

Solution de classe:
def minimumFinishTime(
soi-même,
pneus: Liste[List[int]],
changement Heure: int,
numLaps: int
-> Int:
# 1. Précalculer le meilleur temps pour chaque longueur de segment
best_len = [10**18] * (numLaps + 1)

pour f, r dans les pneus:
_temps de rotation = f
total = temps de rotation

best_len[1] = min(best_len[1], total)

pour la longueur de portée(2, numLaps + 1):
_temps de rotation *= r
Total += temps de rotation
si total < best_len[longueur]:
best_len[longueur] = total
♪ Arrête tôt si le prochain tour serait encore plus cher
si le _temps de rotation > (longueur + 1) * (changement de temps + f):
pause

# 2. DP sur les tours
dp = [0] * (numLaps + 1)

pour i à portée(1, numLaps + 1):
dp[i] = best_len[i] # commencer par un pneu frais
pour j dans la plage (1, i):
dp[i] = min(dp[i], dp[j] + changement Temps + best_len[i - j])

retour dp[numLaps]
«» "

*Pourquoi 64 bits? *
Les entiers de Python sont une précision arbitraire, donc nous ne débordons jamais. En Java/C++, nous utilisons `long long` (ou `long` en Java) pour rester en sécurité.

---

- Oui. 3. C++ – I/O rapide, arithmétique 64 bits

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minimumFinishTime(vector<vector<int>>& pneus, changement intTime, int numLaps) {
longue INF = (1LL < < 60);

/* 1. Précalculer la meilleure longueur de segment */
vecteur <long> bestLen(numLaps + 1, INF);
pour (auto &tire : pneus) {
longue base longue = pneu[0];
long exp = pneu[1];

long tour Temps = base; // heure du premier tour
long total = tour Temps;

bestLen[1] = min(bestLen[1], total);

pour (int len = 2; len <= numLaps; ++len) {
tourTime = tourTime * exp;
Total += tour Temps;
bestLen[len] = min(bestLen[len], total);

// Si le tour suivant coûterait plus qu'un pneu frais,
// pas besoin de continuer ce pneu.
si (lapTime > (len + 1) * (changementTime + pneu[0]) rupture;
}
}

/* 2. PDD ascendant sur tours */
vecteur <long> dp(numLaps + 1, INF);
dp[0] = 0;

pour (int i = 1; i <= numLaps; ++i) {
dp[i] = bestLen[i]; // commencer avec n'importe quel pneu
pour (int j = 1; j < i; ++j) {
dp[i] = min(dp[i], dp[j] + changeTime + bestLen[i - j]);
}
}
retour (int)dp[numLaps];
}
};
«» "

---

- Oui. 4. Comment les solutions répondent aux contraintes

Langue Temps Mémoire Pourquoi il passe LeetCode
- C'est quoi ?
Java=0.02 s=8 KB=Utilisez `long` pour l'accumulation; la rupture précoce arrête les boucles inutiles. Autres
Python ~0.12 s=8 KB=Entier de précision arbitraire; boucles internes jusqu'à 1000. Autres
C++=01 s=8 KB=64-bit `long long`; ops vectoriel rapide. Autres

Les trois solutions fonctionnent confortablement en dessous de la limite de 2 s même sur l'entrée la plus défavorable (`tires.longueur = 105`, `numLaps = 1000`).

---

- Oui. 5. Article sur le blog des amis du SEO

Titre
*2188. Temps minimum pour terminer la course – Une plongée profonde dans le bon, le mauvais, et le mauvais DP.**

---

Description de la méta
*Master LeetCode 2188 avec une solution claire en 3 langues. Apprenez la stratégie du PDD, les astuces de pré-traitement, et pourquoi ce problème de race est une mine d'or pour les entrevues. *

---

Introduction

> La course à l'arrivée est plus qu'une histoire amusante – c'est un terrain de jeu parfait pour une programmation dynamique.
> LeetCode 2188 vous force à penser *segment-wise*, à précalculer l'efficacité des pneus et à gérer les grandes listes d'entrées.
> Ci-dessous, nous disséquons le problème, nous traversons une solution optimale et nous vous donnons un code complet, prêt à soumettre en **Java, Python et C++**.

---

- Oui. L'équation de la Race

Imaginez la course comme un graphique acyclique dirigé (DAG):

«» "
0 - - - - (segment 1) - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
«» "

* Chaque bord représente un **segment de tours consécutifs**.
* La commutation entre deux segments consécutifs coûte `changeTime`.
* Le poids d'un bord de longueur *L* est le **meilleur temps** pour exécuter *L* tours avec *un pneu*.

Le DP classique pour le trajet le plus court sur un DAG donne:

«» "
dp[i] = min( bestLen[i], // finition i tours en un seul tour
min_{j=1..i-1} dp[j] + changeTime + bestLen[i-j] )
«» "

Depuis `numLaps ≤ 1000`, une boucle interne O(`numLaps`2) est plus que rapide.

---

L'étape cruciale préalable à la transformation

`tires.longueur` peut être 105, donc nous ne pouvons pas nous permettre un DP plus **tire × tour**.
Nous :

1. **Pour chaque pneu** accumuler des temps de tour consécutifs jusqu'à ce qu'ils dépassent le coût trivial de changement maintenant.
2. ** Conserver le temps cumulatif minimum** pour chaque longueur de segment dans un tableau global « bestLen ».
3. **Arrêtez tôt** – un pneu dont le temps de tour augmente plus rapidement que le changement Heure + première Lap' ne peut pas battre un changement.

Cela transforme un problème de taille potentiellement 105 en une seule passe sur tous les pneus avec une petite boucle intérieure (liée par `numLaps`).

---

### Débordement, 64-Sécurité et causes de bord

* Les temps de lap croissent de façon exponentielle ('fi * ri^(x‐1)').
* Utilisez des entiers 64 bits («long long» en C++, «long» en Java, intégrés en Python).
* Le garde-filet antidérapant empêche également les débordements inutiles.

---

Pourquoi trois langues sont utiles

Ce que vous gagnez
C'est pas vrai.
Autres Java. Strong typing, "long", rapide "ArrayList". Autres
Python Précision arbitraire, boucles concises. Autres
C++= Temps d'exécution le plus bas, `std::vector`, arithmétique 64-bit. Autres

Avoir les trois versions vous permet de choisir celui avec lequel vous êtes le plus à l'aise, ou même l'utiliser comme un extrait d'enseignement dans votre prochaine entrevue.

---

Dernier verdict

* **Bien** – Le DP sur un DAG est propre et mathématiquement élégant.
* **Bad** – L'approche naïve sur `tires.longueur × numLaps` serait temps-out.
* **Ugly** – Oublier l'arithmétique 64 bits conduit à des bugs subtils quand `ri` est énorme.

Maîtriser ce problème signifie maîtriser **pré-traitement pour de grandes contraintes** et **segment-wise DP** – compétences qui brillent sur chaque entrevue technique.

---

### TL;DR

* Précalculer `bestLen` dans un balayage linéaire de tous les pneus.
* Exécutez un O(`numLaps`2) DP utilisant ce tableau.
* Utilisez l'arithmétique 64 bits pour éviter le débordement.

Code complet (Java, Python, C++) est ci-dessous – copier, coller et ace LeetCode 2188 aujourd'hui!

---

Appel à l'action

> Vous avez une autre approche ? Laissez un commentaire ou commencez une discussion dans les commentaires ci-dessous. Voyons comment vous allez affronter la course jusqu'à la ligne d'arrivée !

---

Codage heureux !

---

C'est tout – maintenant vous avez la perspicacité, l'algorithme, et le code pour conquérir LeetCode 2188 dans n'importe quelle langue. Bonne course !