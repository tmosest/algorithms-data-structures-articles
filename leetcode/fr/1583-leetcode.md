---
Titre: LeetCode 1583. Compte des amis malheureux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Comment cracker le code de leet #1583 – Count des amis malheureux
C++ – La solution complète + un billet de blog qui vous aide à trouver un emploi*

---

Aperçu du problème

> **Couvercle d'amis malheureux**
> *Moyenne – Code de leet 1583*

Vous avez reçu :

Description
- C'est quoi ?
Même nombre d'amis (2 ≤ n ≤ 500) Autres
Une permutation de tous les amis **sauf** `i` – trié de la plupart à la moindre préférence
"Pairs[i] = [x, y]"" Le seul couplage légal (`x` "y`) Autres

Un ami `x` est **malheureuse** s'il existe un ami `u` tel que:

1. `x` préfère `u` à son propre partenaire `y`; ** et**
2. `u` préfère `x` à son propre partenaire `v`.

Rends le nombre d'amis malheureux.

> **Exemples**
> *Exemple 1* – 2 amis malheureux
> *Exemple 2* – 0 amis malheureux
> *Exemple 3* – les 4 sont malheureux

---

- Oui. Aperçu clé

L'état est *pas*.
C'est une préférence mutuelle** : les deux personnes préféreraient être ensemble.
Donc pour chaque personne nous devons:

1. Marchez dans leur liste de préférences *jusqu'à ce qu'on touche leur partenaire.
2. Pour chaque candidat « u » mieux que « partenaire », vérifiez si « u » nous préfère aussi à « u » s partenaire.

Si un tel "u" existe, la personne est malheureuse.

Pour faire l'étape 2 rapidement, nous précalculons une matrice **rank**:

«» "
rang[i][j] = position de l'ami j dans les préférences[i] (0 = choix supérieur)
«» "

Alors, "u" préfère x sur v" est juste "rank[u][x] < rank[u][v]".

---

Algorithme (temps O(n2), espace O(n2)

Étape Ce que nous faisons
C'est quoi ?
Construire `rank[n][n]` en scannant chaque `préférences[i]`. Autres
Autres Construire un partenariat des "paires". Autres
Pour chaque ami `x`:<br> *partenaire = partenaire[x]*<br> Pour chaque `u` dans `priorités[x]` jusqu'à ce que nous touchions `partenaire`:<br> *if* `rank[u][x] < rank[u][partenaire[u]` → `x` malheureux, `break`.
Autres Retournez le compteur. Autres

---

C'est pas vrai. Code

C'est vrai. Java

"Java
Importation de java.util.*;

solution de classe {
public int malheureuxAmis(int n, int[][] préférences, int[][] paires) {
// 1. matrice de classement
int[][] rang = nouveau int[n][n];
pour (int i = 0; i < n; i++) {
pour (int pos = 0; pos < preferences[i].longueur; pos++) {
rang[i][préférences[i][pos]] = pos;
}
}

// 2. tableau de partenaires
int[] partenaire = nouveau int[n];
pour (int[] p : paires) {
partenaire[p[0]] = p[1];
partenaire[p[1]] = p[0];
}

= 0;
// 3. scanner tout le monde
pour (int x = 0; x < n; x++) {
int y = partenaire[x];
pour (int u : préférences[x]) {
si (u == y) pause; // atteint son propre partenaire → heureux
int v = partenaire[u]; // partenaire de u
si (rank[u][x] < rank[u][v]) { // préférence mutuelle
malheureuse++;
pause;
}
}
}
retour malheureux;
}
}
«» "

Python

'`python
Solution de classe:
def malheureux Amis(self, n: int, préférences: List[List[int]],
paires: Liste[Liste[int]]) -> Int:
# rang[i][j] = position de j dans les préférences[i]
rang = [[0] * n pour _ dans l'intervalle(n)]
pour i, préf dans l'énumération(préférences):
pour pos, ami en énumération(pref):
rang[i][ami] =

partenaire = [0] * n
pour a, b par paire:
partenaire[a] = b
partenaire[b] = a

malheureuse = 0
pour x dans la plage(n):
y = partenaire[x]
pour u dans les préférences[x]:
Si u == y: pause
v = partenaire[u]
si rang[u][x] < rang[u][v]:
malheureuse += 1
pause
retour malheureux
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int malheureusesAmis(int n, vector<vector<int>>& préférences,
vecteur<vecteur<int>& paires) {
// rang[i][j]
vecteur<vector<int>> rang(n, vecteur<int>(n));
pour (int i = 0; i < n; ++i) {
pour (int pos = 0; pos < preferences[i].size(); ++pos) {
rang[i][préférences[i][pos]] = pos;
}
}

vecteur<int> partenaire(n);
pour (auto &p : paires) {
partenaire[p[0]] = p[1];
partenaire[p[1]] = p[0];
}

= 0;
pour (int x = 0; x < n; ++x) {
int y = partenaire[x];
pour (int u : préférences[x]) {
si (u) y) pause;
int v = partenaire[u];
si (rank[u][x] < rank[u][v]) {
++malheur;
pause;
}
}
}
retour malheureux;
}
};
«» "

---

C'est vrai. Analyse de complexité

Java / Python / C++
-- -- -- -- -- -- -- -- --
Temps **O(n2)** – nous visitons chaque ami liste de préférences une fois. Autres
L'espace **O(n2)** – la matrice `rank`; `partner` et les tableaux auxiliaires sont O(n). Autres

Avec `n ≤ 500`, cela passe facilement les limites du Code de Leet.

---

#### 6=" Pièges communs (="Les mauvais et les affreux")

Pourquoi il échoue
- C'est quoi ?
En utilisant une carte *hash* pour le rang au lieu d'un tableau 2-D. Utilisez une matrice d'inte – rapide cache friendly
Autres Breaking seulement après avoir trouvé *any* meilleur ami Nous devons également veiller à ce que *celui-ci* nous préfère. Autres
Autres Sauter le partenaire dans la boucle intérieure par `if(u==y) continue`.
L'algorithme compte chaque personne indépendamment, mais la condition est symétrique; aucun problème de double comptage.

---

- Oui. Pourquoi ce blog vous aide à trouver un emploi

1. **SEO-Mots-clefs optimisés** – -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
2. **Code clair** – Des solutions prêtes à copier pour Java, Python, C++ – les intervieweurs les plus courants de langues s'attendent.
3. **Deep Dive** – Comprendre *pourquoi* l'algorithme fonctionne vous donne la confiance pour l'expliquer dans une interview.
4. **Pitfalls** – Erreurs courantes que vous pouvez mentionner comme des choses que j'ai apprises pour vous montrer...
5. **Analyse du temps et de l'espace** – Montre votre capacité à évaluer la complexité – une compétence d'entrevue incontournable.

---

- Oui. A emporter rapidement

- Construire une matrice **rank** pour les requêtes de préférences O(1).
- Carte de chaque ami dans un tableau.
- Pour chaque ami, itérer les préférences jusqu'à ce que vous frappez le partenaire; si un candidat meilleur que le partenaire vous préfère aussi, vous êtes malheureux.
- Complexité: **O(n2)** temps, **O(n2)** espace – parfait pour `n ≤ 500`.

Déposez le code dans votre éditeur, lancez les tests Leet Code, et vous serez prêt à aser ce problème et impressionner les gestionnaires d'embauche! C'est ce qu'il a dit.

---

Bon codage, et la meilleure chance d'atterrir ce travail de rêve!