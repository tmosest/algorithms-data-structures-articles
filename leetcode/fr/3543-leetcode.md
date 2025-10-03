---
titre: LeetCode 3543. Piste K-Edge pondérée maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3543 – *Piste K-Edge pondérée maximale*
**DP sur DAG – Un poste-interview Power-Move* *

> ** Identification du problème**: 3543
> **Difficulté**: Moyenne
> **Tags**: Programmation dynamique, DAG, Tri topologique, Bitset, Graph

---

- Oui. 1. Le problème en coque

Vous recevez un graphique acyclique ** (DAG) avec des nœuds `n` (0 ... n‐1).
Chaque bord est `[u, v, w]` → un bord dirigé `u → v` avec le poids `w`.

Paramètres:

Sens de la variable
C'est pas vrai.
**Les bords exacts** `k` doivent être utilisés.
Le poids total doit être ** strictement inférieur** à `t` Autres

**Objectif**:
Retourne la somme maximale des poids** pour tout chemin qui satisfait aux deux contraintes.
Si ce chemin n'existe pas, retourner `-1`.

> **Constraints**
1 ≤ n ≤ 300
> * 0 ≤ bords longueur ≤ 300
* 1 ≤ l ≤ 10
0 ≤ k ≤ 300
1 ≤ t ≤ 600
> * Le graphique est garanti comme étant un DAG.

---

- Oui. 2. Pourquoi ce problème est important

- **Graph + DP combo** – De nombreuses personnes interrogées sont tombées sur la combinaison de la traversée graphique et des transitions de l'état DP.
- **Poids lié (`t ≤ 600`)** – Permet un *bitset* ou *boolean DP* truc qui court rapidement même pour le pire cas.
- **Biens du Groupe consultatif** – Détendons-nous sur la nécessité de contrôler le cycle et d'utiliser une simple propagation bord par bord.

---

- Oui. 3. Intuition et approche

3.1 État DP

Laissez

«» "
dp[u]e][s] = vrai
«» "

Les Il existe un chemin qui se termine au nœud `u`, utilise exactement les bords `e`, et a le poids total `s` (et `s < t`).

* `u` – indice des nœuds (`0 ... n‐1`)
* `e` – nombre de bords utilisés (`0 ... k`)
* `s` – poids courant (`0 ... t-1`)

Nous gardons seulement des états avec `s < t` – tout le reste n'est pas pertinent.

3.2 Cas de base

«» "
dp[u][0][0] = vrai pour chaque noeud u
«» "

Un chemin qui commence et se termine au même noeud avec les bords zéro a un poids 0.

3.3 Transition

Pour chaque bord `u → v` avec le poids `w`:

«» "
pour e = 0 ... k-1:
pour s = 0 ... T-1-w:
si dp[u]e][s]:
dp[v][e+1][s+w] = true
«» "

Nous extendons chaque état accessible par un seul bord.

Résultat

Après traitement de toutes les bords et de toutes les profondeurs:

«» "
réponse = max { s-[u][k][s] == vrai pour n'importe quel u }
«» "

Si aucun tel `s` existe → réponse = -1.

3.5 Complexité

Opération Coût
- C'est quoi ?
Tableau 3-D DP :
Lignes de transition
D'une manière générale **O(n·k·t + bords·k·t)** – bien dans les limites

La mémoire et le temps sont facilement traités en Java, Python (avec des jeux) et C++.

---

- Oui. 4. Mise en œuvre du code

On trouvera ci-dessous des solutions propres, prêtes à être copiées dans **Java**, **Python** et **C++**.
N'hésitez pas à les déposer dans votre soumission LeetCode.

---

#### 4.1 Java (Bitset-Optimized)

"Java
Importation de java.util.*;

solution de classe publique {
intérieur public maxPoids(int n, int[]] bords, int k, int t) {
// dp[u][e] -> bitset de sommes réalisables (< t) pour le noeud u utilisant les bords e
@SuppressAvertissements("non vérifié")
BitSet[][] dp = nouveau BitSet[n][k + 1];
pour (int u = 0; u < n; u++) {
pour (int e = 0; e <= k; e++) {
dp[u][e] = nouveau BitSet(t); // seuls les indices [0, t-1] sont utilisés
}
}

// Fond: 0 bords, poids 0
pour (int u = 0; u < n; u++) {
dp[u][0].set(0);
}

// Liste des bords pour une itération facile
Liste <int[]> ledgeList = nouvelle liste de répartition<>();
pour (int[] e : bords) edgeList.add(e);

// Transition
pour (int e = 0; e < k; e++) {
pour (int[]ed : edgeList) {
u = ed[0], v = ed[1], w = ed[2];
// Pour chaque somme réalisable à (u, e)
// Déplacement laissé par w et OR vers (v, e+1)
BitSet décalé = (BitSet) dp[u][e].clone();
déplacement.shiftLeft(w);
// Nous ne devons garder que des indices < t
masque BitSet = nouveau BitSet(t);
masque.set(0, t); // tous les indices valides
déplacement.et(masque);
dp[v][e + 1]ou(transféré);
}
}

// Trouver la somme maximale pour exactement k bords
int best = -1;
pour (int u = 0; u < n; u++) {
pour (int s = t - 1; s >= 0; s--) {
si (dp[u][k].get(s)) {
best = Math.max(best, s);
break; // premier (le plus grand) vrai est optimal
}
}
}
le meilleur retour;
}
}
«» "

> **Pourquoi BitSet?**
> Il stocke les bits `t` compactés et nous permet d'effectuer un changement de poste et un changement de temps dans ~O(t).

---

#### 4.2 Python (basé sur un ensemble)

'`python
Solution de classe:
def maxPoids(self, n: int, bords: List[List[int]], k: int, t: int) -> Int:
# dp[u][e] = ensemble de sommes réalisables (< t) pour le noeud u avec bords e
dp = [[set() pour _ dans la plage(k + 1)] pour _ dans la plage(n)]
pour u dans la plage(n):
dp[u][0].add(0) # cas de base

pour e dans la plage(k):
pour u, v, w dans les bords:
pour s dans list(dp[u][e]): # list() pour éviter la mutation pendant la boucle
ns = s + w
si ns < t:
dp[v][e + 1].add(ns)

meilleure = -1
pour u dans la plage(n):
pour s dans trié(dp[u][k], inverse=True):
best = max (meilleur, s)
pause
le meilleur retour
«» "

> La limite de poids "t ≤ 600" garantit que les tailles de l'ensemble restent minuscules.
> L'utilisation de `list(dp[u][e])` prévient l'erreur de runtime: définissez la taille modifiée pendant l'itération.

---

### 4.3 C++ (bitset\<601\>)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxWeight(int n, vector<vector<int>>& bords, int k, int t) {
// dp[u][e] : bitset de sommes réalisables (< t) pour noeud u avec bords e
vector<vector<bitset<601>>> dp(n, vector<bitset<601>>(k + 1));

// Fond: 0 bords, poids 0
pour (int u = 0; u < n; ++u) dp[u][0].set(0);

pour (int e = 0; e < k; ++e) {
pour (auto &ed : bords) {
u = ed[0], v = ed[1], w = ed[2];
// déplacement dp[u][e] laissé par w et OR dans dp[v][e+1]
bitset <601> décalé = dp[u][e] << w;
// garder seulement les bits < t
pour (int s = t; s < 601; +s) décalé.reset(s);
dp[v][e + 1]= décalé;
}
}

int best = -1;
pour (int u = 0; u < n; ++u) {
pour (int s = t - 1; s >= 0; --s) {
si (dp[u][k].essai(s)) {
best = max (meilleur, s);
break; // le plus grand trouvé
}
}
}
le meilleur retour;
}
};
«» "

> **Pourquoi `bitset<601>`? **
> Le poids lié (`t ≤ 600`) nous permet de garder exactement `t` bits – un ajustement parfait pour le bitset.

---

- Oui. 5. Le Bon, le Mauvais et l'Ugly

Aspect du bien
- C'est quoi ?
**Initialisation des cas de base**= Simple : chaque noeud peut démarrer un chemin de longueur zéro.= = Beaucoup de gens oublient de définir tous les nœuds – conduit à des réponses =false=.= = Oublier de nettoyer le tableau DP (réutiliser à travers les cas de test). Autres
**Loops de transition**=Loop triple-nested propre.===O(edges·k·t) est acceptable mais peut être lourd si vous oubliez de limiter `s` à `t‐1‐w`.===L'écriture de récursion manuelle avec mémorisation peut faire sauter la profondeur de la pile (k peut être 300). Autres
La recherche de tous les nœuds pour `dp[u][k]` sans descente peut renvoyer la somme **premier** valide (pas maximum). L'utilisation d'une file d'attente prioritaire ou d'une DFS pour suivre le poids maximum peut être sur-ingénierie. Autres
**Utilisation de la mémoire**= 54 Mo (Java bitset) / 54 Mo (C++ bitset) / sets (Python).=== L'utilisation de `List[List[List[bool]]]` en Java peut gâcher la mémoire (3D array).=== Les sets de Python peuvent être plus lents si ils ne sont pas captés par `t`. Autres

---

- Oui. 6. Conseils d'entrevue

1. ** Expliquer la dimension DP d'abord** – les intervieweurs aiment un diagramme d'état clair.
2. **Mention de la propriété DAG** – Parce qu'il n'y a pas de cycles nous pouvons en toute sécurité itérer sur les bords dans n'importe quel ordre. (en milliers de dollars)
3. **Afficher l'astuce de la casquette de poids** – T ≤ 600, donc nous pouvons utiliser un bitset de 601 bits et le déplacer par le poids de bord. (en milliers de dollars)
4. ** Discutez du temps et de l'espace** – opérations de 54 M, mémoire de 54 Mo – bien au-dessous des limites. (en milliers de dollars)
5. **Cas d'Edge** – 0 → la réponse est 0 (si t > 0). k > bords.longueur → -1.
6. **Testing** – Ajouter un harnais de test personnalisé qui imprime l'ordre topologique et l'instantané DP pour déboguer les cas complexes. (en milliers de dollars)

---

- Oui. 7. Quand et comment utiliser ce problème

Pourquoi ça aide ?
C'est pas vrai.
**Entretien de graphes**Démontre que vous pouvez combiner *bords de graphe* avec *profondeur de graphe*. Autres
**DP sur une dimension délimitée** Autres
**Hiring for large-scale systems** Autres

> **Conseil pro**: Dans un entretien en direct, dessinez d'abord la matrice DP sur le tableau blanc.
> Puis écrivez la boucle triple-nested en pseudo-code avant de saisir la solution finale.

---

- Oui. 8. Mot final et appel à l'action

*Maîtriser la transition PDD. *
- Connaissez le truc lié au poids. *
*Soyez capable d'expliquer chaque ligne de votre code. *

Ce problème est un billet d'or** pour montrer aux recruteurs que vous pouvez :

* Comprendre les contraintes complexes
* Conception efficace DP sur les graphiques
* Fournir un code propre et prêt à la production en plusieurs langues

** Prêt à décrocher cette entrevue d'ingénierie logicielle? **
Pratiquez ce problème, ajoutez les solutions à votre portfolio et partagez-les sur LinkedIn avec le hashtag **#LeetCode3543**. Les recruteurs aiment voir * résolution de problèmes* avec un * récit clair*.

Bon codage ! C'est ce qu'il a dit.

---



---



Mots clés (pour le titre de l'article et le corps)

* LeetCode 3543 solution
* Voie K‐Edge maximale pondérée
* PDD sur DAG
* Programmation dynamique graphique
* Problème de codage de l'entrevue
* Programmation d'entrevues d'emploi
* Code en Java/Python/C++
* Graphique DP Bitset

---



Structure de l'article (style HTML)

html
<h1>Code de let 3543 – Master the Maximum Weighted K-Edge Path (Java, Python, C++)</h1>

<h2>1. Aperçu du problème</h2>
<p>...</p>

<h2>2. Pourquoi cela compte pour les entrevues</h2>
<ul>
<li>Graph + DP combo</li>
<li>Poids gonflé → Astuce de bitset</li>
<li>Biens du GAD</li>
</ul>

3. Intuition et approche du PDD</h2>
<ol>
<li>Définition de l'État</li>
<li>Cas de base</li>
<li>Transition</li>
<li> Extraction des résultats</li>
</ol>

<h2>4. Analyse de la complexité</h2>
<table>...</table>

<h2>5. Solutions de code</h2>
<h3>Java</h3>
<pré>...</pré>
<h3>Python</h3>
<pré>...</pré>
<h3>C++</h3>
<pré>...</pré>

<h2>6. Bons, mauvais et mauvais patrons</h2>
<table>...</table>

<h2>7. Conseils d'entrevue</h2>
<ol>...</ol>

<h2>8. Réflexions finales</h2>
<p>...</p>
«» "

> Utilisez ce squelette lors de la publication sur Medium, dev.to, ou votre blog personnel.

---



C'est tout. Profitez de l'écriture!