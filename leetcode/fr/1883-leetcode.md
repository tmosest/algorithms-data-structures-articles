---
titre: LeetCode 1883. Pass minimum pour arriver à la réunion à temps -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code Maître Leet 1883: **Le minimum passe à l'arrivée à la réunion à l'heure** – Le bon, le mauvais, et le mauvais
**Blogue optimisé pour les chercheurs d'emploi et les adeptes de l'algorithme* *

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi ce problème se trouve-t-il pour les entrevues] (# pourquoi ce problème se trouve-t-il)
3. [Observations clés et cas de bord] (#observations clés)
4. [La solution DP classique (en entier seulement)] (#dp-solution)
5. [Mise en œuvre de Java – PDD 1‐D de base] (#code de Java)
6. [Python Implementation – PDD 1-D avec Trick plafond](#python-code)
7. [C++ Implementation – Fast & Precise](#cpp-code)
8. [Complexité temporelle et spatiale](#complexité)
9. [Pièges communs (les affreux)] (#pièges communs)
10. [Comment polir votre solution pour une entrevue de travail](#job-interview-tips)
11. [FAQ]
12. [Conclusion et retrait] (#conclusion)

---

<a name="problème-overview"></a>
- Oui. 1. Aperçu du problème

> **Le minimum passe à l'arrivée à la réunion à l'heure**
> **Difficulté:** Dur

Vous avez des routes `n` avec des longueurs `dist[i]` (km).
Vous voyagez à vitesse constante `vitesse` (km/h).
Après avoir terminé la route `i`, vous *doit* attendre jusqu'à la prochaine heure entière **sauf** vous choisissez **skip** le reste.
Sauter vous permet de démarrer immédiatement la prochaine route.
Votre objectif : **Arrivé à la réunion dans le plus d ' heuresAvant les heures**.
Return le nombre minimum de skips requis, ou `-1` si impossible.

> **Constraints**
> - 1 ≤ n ≤ 1000
> - 1 ≤ dist[i] ≤ 105
1 ≤ régime ≤ 106
Avant ≤ 107

---

<un nom> </a>
- Oui. 2. Pourquoi ce problème se pose pour les entrevues

Comment le problème aide-t-il
[En milliers de dollars des États-Unis]
**Programmation dynamique**= 1-D DP avec les skips d'état utilisés et la transition =skip ou non. Autres
**Greedy & Math Insight**= Opération de plafond → entier arithmétique sans `double`. Autres
**Gestion de la complexité du temps** Autres
**Manipulation de précision** Autres
Autres **Edge-Case Thinking** . Autres

Les candidats qui s'attaquent à ce problème font preuve d'une forte intuition du PDD et d'une gestion soigneuse de la précision.

---

<un nom="observations clés"></a>
- Oui. 3. Observations clés et cas de bord

1. **Passer n'est toujours pas dangereux** – si vous sautez un repos, vous ne pouvez jamais arriver plus tard que si vous ne l'avez pas fait.
2. **Le temps passé sur une route peut s'exprimer comme un entier multiple de vitesse**:
`ceil(dist[i] / speed)` → `ceil( dist[i] )` en unités de *secondes* si vous multipliez tout par `speed`.
3. **La dernière route n'a jamais besoin de repos** – la règle d'attente ne s'applique qu'entre* routes.
4. **Arithmétique intégrale seulement** – multipliez toutes les fois par « vitesse » pour les garder entiers et éviter les erreurs de point flottant.
5. ** Etat du PD** – `dp[j]` = *temps total minimum (en unités de vitesse*)* pour terminer les routes traitées en utilisant exactement `j` skips.

---

<un nom="dp-solution"></a>
- Oui. 4. La solution de DP classique (seulement intégrale)

Nous utilisons un PDD *bottom-up 1-D* qui itère sur les routes et met à jour le tableau des comptes de saut élevés à bas.

«» "
Laisser T = heuresAvant * vitesse // Convertir la date limite en la même unité que les valeurs de dp

pour chaque route i:
pour j de maxSkips jusqu'à 0:
// 1. Sans sauter: ajouter le temps d'attente (plafond)
nonSkip = ceil(dp[j] + dist[i]) // identique à (dp[j] + dist[i] + vitesse-1) / vitesse * vitesse
// 2. Avec saut : seulement autorisé si j>0
skip = (j > 0) ? dp[j-1] + dist[i] : INF
i) Dernière route:
dp[j] = dp[j] + dist[i] // Pas d'attente après la dernière route
Sinon:
dp[j] = min(skip, pasSkip)
«» "

Après avoir rempli `dp`, la réponse est la plus petite `j` telle que `dp[j] <= T`.

Toutes les opérations restent dans 64 bits entiers (`long` in Java/C++/Python `int`).

---

<a name="java-code"></a>
- Oui. 5. Mise en œuvre Java – PDD 1-D

"Java
Importer java.util. Les tableaux;

solution de classe {
public int minSkips(int[] dist, int speed, int hoursAvant) {
int n = longueur dist.;
longue T = (long) heuresAvant * vitesse; // Date limite en unités de vitesse
INF longue = Long.MAX_VALUE / 4; // infinité sûre

long[] dp = nouveau long[n + 1];
Arrays.fill(dp, 0); // dp[0] = 0 avant le début

pour (int i = 0; i < n; i++) {
d = dist[i];
pour (int j = Math.min(i, n); j >= 0; j--) {
// Attendez si on ne saute pas.
long nonSkip = ceil(dp[j] + d, vitesse);

// Sauter le repos
long skip = (j > 0) ? dp[j - 1] + d : INF;

Si (i == n - 1) { // Dernière route
dp[j] = dp[j] + d; // aucune attente après le segment final
} autre {
dp[j] = Math.min(skip, pas Skip);
}
}
}

pour (int skips = 0; skips <= n; skips++) {
si (dp[skips] <= T) les sauts de retour;
}
retour -1;
}

// Plafond entier de (valeur / vitesse) * vitesse
Ceil privé long(valeur longue, vitesse int) {
retour (valeur + vitesse - 1) / vitesse * vitesse;
}
}
«» "

**Pourquoi cette version remporte-t-elle la note --good--? * *
*Pas de `double`, pas de perte de précision, de mises à jour de tableau unique et de noms de variables clairs. *

---

<un nom="code-python"></a>
- Oui. 6. Mise en œuvre de Python – PDD 1-D avec pose de plafond

Le "int" de Python est une précision arbitraire, donc nous pouvons tout garder dans la plage 64 bits sans débordement. Le truc du plafond est identique à Java.

'`python
Solution de classe:
def minSkips(self, dist: list[int], vitesse: int, heuresAvant: int) -> Int:
n = len(dist)
T = heuresAvant * vitesse # Délai dans la même unité que les valeurs de dp
INF = 10**18

dp = [0] + [INF] * n # dp[j] = durée min avec j skips

pour i, d en énumération(dist):
# itérer de haut en bas skips
pour j dans la plage (min(i, n), -1, -1):
# Temps d'attente sans sauter
not_skip = (dp[j] + d + vitesse - 1) // vitesse * vitesse
skip = dp[j - 1] + d si j > 0 autre INF

Si i == n - 1: # dernière route – pas d'attente
dp[j] = dp[j] + d
Sinon:
dp[j] = min(skip, non_skip)

pour les skips, temps en énumération(dp):
si temps <= T:
sauts de retour
retour -1
«» "

Pourquoi Python ? *
- Mêmes maths entiers; pas de flot.
- Propre et concis; seulement deux boucles imbriquées.

---

<a name="cpp-code"></a>
- Oui. 6. Mise en œuvre C++ – Rapide et précis

Ci-dessous se trouve une solution C++17 qui peut être compilée avec `-O2`.

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minSkips(vector<int>& dist, int speed, int hoursBefore) {
const int n = dist.size();
Const long long T = 1LL * heuresAvant * vitesse; // Date limite en unités de vitesse
longue INF = (1LL < < 60);

vector<long long> dp(n + 1, 0); // dp[j] – durée min avec j skips

pour (int i = 0; i < n; ++i) {
d = dist[i];
pour (int j = min(i, n); j >= 0; --j) {
long nonSkip = (dp[j] + d + vitesse - 1) / vitesse * vitesse;
long saut long = (j > 0) ? dp[j - 1] + d : INF;
si (i) n - 1) {
dp[j] += d; // pas d'attente après la dernière route
} autre {
dp[j] = min(skip, pas Skip);
}
}
}

pour (int skips = 0; skips <= n; ++) {
si (dp[skips] <= T) les sauts de retour;
}
retour -1;
}
};
«» "

> **Conseil:** Utilisez `long long` pour éviter le débordement (`dist[i] * n` peut être jusqu'à 108, ce qui s'adapte facilement en 64 bits).

---

<un nom="complexité"></a>
- Oui. 6. Complexité temporelle et spatiale

Heure de mise en œuvre
- Oui.
Java / Python / C++ DP () **O(n2)** (1 million d'itérations pour n = 1000) () **O(n)** (1-D tableau de taille `n+1`) Autres
Variante 2-D DP. **O(n2)**. **O(n2)** (généralement trop grande pour n = 1000 en Python, mais toujours acceptable en LeetCode en raison d'un petit facteur constant)

Les deux langues ci-dessus sont * assez rapides* pour les tests LeetCode .
Si vous avez besoin d'une solution O(n), le problème est en fait *NP‐hard* (c'est une forme de programmation avec des contraintes entières).
Le DP quadratique est donc la solution générale optimale.

---

<un nom="common-pitfalls"></a>
- Oui. 7. Pièges communs (les odieux)

Erreurs dans les résultats
- C'est quoi ?
**L'utilisation de `double` et `ceil()`** , la perte de précision de point flottant (par exemple, `3000001 <= 30` → faux). Travailler en *integers seulement*; multiplier par `vitesse` avant ceil. Autres
**Ne pas gérer la dernière route**= Ajoute une attente inutile après le dernier segment, le temps de surcompte. En cas spécial, la dernière itération ou retirer l'attente dans la boucle. Autres
**Mise à jour DP vers l'avant (faible → haut)**=Les mauvais états sont utilisés parce que les mises à jour antérieures écrasent les valeurs nécessaires pour les nombres de skip plus élevés. Mettre à jour `dp` des indices de saut élevés à bas. Autres
**Utiliser `int` au lieu de `long`**.
**En supposant que `skips ≤ n-1`**=A défaut lorsque vous devez sauter toutes les routes; le réseau DP doit supporter jusqu'à `n` skips. Initialiser la taille du DP `n+1` et la boucle `j` de `min(i, n)` jusqu'à `0`. Autres

---

<a name="job-interview-tips"></a>
- Oui. 8. Comment polonais votre solution pour un entretien d'emploi

1. ** Expliquez clairement l'état DP** – -dp[j] = durée minimale après avoir terminé les routes traitées en utilisant exactement j skips. (en milliers de dollars)
2. **Afficher la règle d'attente en code** – soulignez que la dernière route saute l'attente.
3. **Mention entier math** – Nous convertissons tous les temps en unités de "vitesse" pour éviter les erreurs de point flottant. (en milliers de dollars)
4. **Parcourez un petit exemple** (par exemple, `dist=[1,2,3]`, `speed=1`, `heuresAvant=2,5`) sur le tableau blanc.
5. **Demande à l'intervieweur** s'il préfère O(n2) ou O(n·log n) – s'adapter en conséquence.
6. **Préparer les questions de suivi**:
- Et si la vitesse est très grande ?
- Comment se comporte la solution si on saute toutes les routes ?
- On peut prouver que sauter ne fait jamais mal ?

> * Conseil professionnel :* Gardez le code rangé, utilisez les fonctions helper pour `ceil`, et commentez chaque itération de boucle. Code clair = cote supérieure dans les entrevues.

---

<un nom=faq></a>
- Oui. 9. FAQ

Question Réponse
C'est pas vrai.
Autres **Pouvons-nous résoudre cela en temps O(n)? Le problème est essentiellement un problème d'horaire limité qui est difficile NP. Le DP Quadratic est optimal pour n ≤ 1000. Autres
Autres **Pourquoi ne pas utiliser `double` et `ceil()` directement? Il fonctionne mais introduit des bugs subtils en raison de l'arrondi des points flottants. Les maths entiers garantissent la justesse. Autres
Autres **Et si « heures avant » n'est pas intégrale?** L'entrée garantit un entier, mais si c'était un flotteur, vous auriez converti la date limite en unités de vitesse en multipliant par "vitesse" et utiliser "ceil" sur les heures de route. Autres
Autres **Y a-t-il une solution cupide?**= No. Greedy échouerait dans les cas où sauter une route plus tard donne un meilleur calendrier global. PDD est nécessaire. Autres

---

<un nom="conclusion"></a>
- Oui. 10. Conclusion et à emporter

- **Programmation dynamique + maths entiers** est le bon qui résout efficacement LeetCode 1883.
- Éviter les pièges à points flottants** – ce problème est une illustration classique des bogues de précision.
- Le cas spécial **de la dernière route** et **les mises à jour de DP inversées** sont essentielles.
- Oui. Soyez prêt à ** expliquer clairement votre approche** ; l'idée algorithmique est simple une fois que vous mapez les contraintes de programmation à DP.

La maîtrise de ce problème démontre à la fois une compétence algorithmique* et une pratique de codage prudente*, deux qualités très appréciées par les recruteurs.

Bonne chance pour votre entretien ! C'est ce qu'il a dit.

---

**Mots clés**: LeetCode programmation dure, dynamique, entier math, précision, programmation, skips, Python, Java, solution C++, préparation d'entrevue.

---

* Fin de l'article. *