---
titre: LeetCode 2959. Nombre d'ensembles possibles de succursales de fermeture -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Nombre d'ensembles possibles de branches de fermeture – le bon, le mauvais, et le mauvais
## Une solution dure de LeetCode profonde en Java, Python & C++

> **Mots-clés du référencement**: LeetCode, Nombre d'ensembles possibles de branches de fermeture, algorithme, Floyd-Warshall, backtracking, théorie des graphiques, Java, Python, C++, interview, défi de codage, solution

---

Présentation

Quand j'ai vu pour la première fois LeetCode **2959 – Nombre d'ensembles possibles de branches de fermeture**, mes yeux se sont élargis. L'énoncé semble simple, mais le combinatoire sous-jacent + twist le plus court-chemin en fait un problème *hard*.

Objectif :
> Compter tous les sous-ensembles de branches fermées de façon à ce que chaque branche restante puisse atteindre toutes les autres dans une distance maximale autorisée (`maxDistance`).

Les contraintes (`n ≤ 10`) donnent à penser qu'une force brute sur les sous-ensembles est viable, mais nous avons encore besoin d'une vérification efficace du trajet le plus court pour chaque sous-ensemble.

Ci-dessous, vous passerez par les *bons*, les *mauvais* et les *gros* parties de la solution à ce problème, puis vous présenterez un code propre et prêt à la production pour **Java, Python et C++**.

---

Récapitulation des problèmes

Description
- C'est quoi ?
Nombre de succursales (0-indexées). «1 ≤ n ≤ 10».
**Routes** Plusieurs bords autorisés. Autres
Toutes les branches restantes doivent être ≤ cette distance distante. Autres
**Retour**=Compte des ensembles de fermeture *valides* (masques) qui satisfont à la condition. Autres
**Caisse d'Edge**=L'ensemble vide de branches actives (toutes fermées) est toujours valide. Autres

---

- Oui. Le défi fondamental

1. **Explosion par sous-ensemble** – ensembles de fermetures possibles «2n» (n ≤ 10 ' → 1024).
2. ** Graphe dynamique** – chaque sous-ensemble enlève quelques sommets et bords d'incident.
3. **Shortest Path** – il faut connaître les distances toutes paires sur le graphique *remaining* rapidement.

La force brute la plus simple serait de lancer Dijkstra ou Floyd-Warshall *par* sous-ensemble, coûtant `O(2n * (n3))` – toujours bien pour `n=10`, mais nous pouvons faire mieux en précomputant les distances toutes paires une fois sur le graphique complet et ensuite *filtering* distances pour chaque sous-ensemble.

---

Approche 1 – Full Floyd-Warshall + Sous-set Check (facile mais clair)

1. ** Calculer toutes les paires de distances les plus courtes** (`dist[i][j]`) sur le graphique complet en utilisant Floyd-Warshall.
* Complexité: `O(n3)` avec `n ≤ 10`.
2. **Itérer sur tous les sous-ensembles** (bitmask).
* Pour chaque sous-ensemble, nous devons simplement nous assurer que *pour chaque paire de nœuds actifs* `i` et `j`, `dist[i][j] ≤ maxDistance`.
3. Compter les sous-ensembles qui satisfont à la condition.
* Le sous-ensemble vide (tous les nœuds fermés) passe automatiquement.

- Oui. Pourquoi cela fonctionne

Parce que supprimer les sommets * ne peut pas * créer un chemin plus court que celui déjà calculé sur le graphique complet. Si une paire se trouve à l'intérieur de `maxDistance` dans le graphique complet, elle reste à l'intérieur de cette distance lorsque nous fermons d'autres branches (sauf si nous fermons un des paramètres). Inversement, si une paire est *déjà* plus loin que `maxDistance`, le sous-ensemble est invalide, peu importe ce que nous fermons.

Ainsi, nous n'avons pas besoin de recalculer les distances pour chaque sous-ensemble – juste filtrer.

---

Analyse de complexité

Étape
C'est quoi ?
Floyd-Warshall sur le graphique complet `O(n3)` (opérations `= 1000` pour `n=10`) Autres
Dénombrement des sous-ensembles Autres
Autres Cochez toutes les paires dans le sous-ensemble "O(n2)" par sous-ensemble → "O(2n * n2)"
**Total**=O(n3 + 2n * n2)===effectivement==1,3e6==ops pour le pire des cas. Autres

Mémoire: `O(n2)` pour la matrice de distance.

---

Mise en œuvre

Ci-dessous sont propres, les implémentations commentées dans **Java**, **Python** et **C++** qui suivent l'approche ci-dessus. Chacun utilise une matrice de distance unique et un dénombrement bitmask.

> **Conseil pour les entrevues** – Lorsque vous expliquez la solution, mettez en évidence le *observation*: fermer les sommets ne peut pas raccourcir n'importe quel chemin le plus court, donc pré-computer toutes les paires une fois est sûr. C'est souvent ce que cherchent les intervieweurs.

---

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe {
numéro d'entrée publicOfSets(int n, int maxDistance, int[][] routes) {
Int final INF = (int)1e9;
int[]] dist = nouvelle int[n];

// initialiser les distances
pour (int i = 0; i < n; ++i) {
les tableaux.fill(dist[i], INF);
dist[i]i] = 0;
}

// construire les bords du graphique
pour (int[] e : routes) {
u = e[0], v = e[1], w = e[2];
si (w < dist[u]v]) {
dist[u][v] = dist[v][u] = w;
}
}

// Floyd‐Warshall sur le graphique complet
pour (int k = 0; k < n; ++k)
pour (int i = 0; i < n; ++i)
pour (int j = 0; j < n; ++j)
si (dist[i][k] + dist[k][j] < dist[i][j])
dist[i]j] = dist[i]k] + dist[k]j];

Total Masques = 1 << n;
réponse int = 0;

// itérer tous les sous-ensembles de nœuds *fermés*
pour (int masque = 0; masque < total Masques; ++masques) {
booléen ok = vrai;
pour (int i = 0; i < n && ok; ++i)
pour (int j = i + 1; j < n; ++j)
si ((masque >> i) et 1) == 0 && (masque >> j) et 1) == 0) {
si (dist[i][j] > maxDistance) ok = faux;
}
si (ok) reply++;
}
réponse de retour;
}
}
«» "

---

6.2 Python

'`python
Solution de classe:
def numberOfSets(self, n: int, maxDistance: int, routes: List[List[int]]) -> Int:
INF = 10**9
dist = [[INF] * n pour _ dans la plage(n)]
pour i dans la plage(n):
dist[i]i] = 0

pour u, v, w dans les routes:
si w < dist[u][v]:
dist[u][v] = dist[v][u] = w

# Floyd–La guerre
pour k dans la plage(n):
pour i dans la plage(n):
pour j dans la plage(n):
si dist[i][k] + dist[k][j] < dist[i][j]:
dist[i][j] = dist[i][k] + dist[k][j]

réponse = 0
pour masque de portée(1 << n):
ok = Vrai
pour i dans la plage(n):
si masque >> i & 1: # noeud fermé
poursuivre
pour j dans la plage(i + 1, n):
si masque >> j & 1: # noeud j fermé
poursuivre
si dist[i][j] > maxDistance:
ok = Faux
pause
si ce n'est pas bien:
pause
si oui:
réponse += 1
réponse de retour
«» "

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre intOfSets(int n, int maxDistance, vecteur<vector<int>>& routes) {
INF = 1e9;
vecteurs<vector<int>> dist(n, vector<int>(n, INF)

pour (int i = 0; i < n; ++i) dist[i]i] = 0;

pour (auto &e : routes) {
u = e[0], v = e[1], w = e[2];
si (w < dist[u][v]) dist[u][v] = dist[v][u] = w;
}

// Floyd‐Warshall sur le graphique complet
pour (int k = 0; k < n; ++k)
pour (int i = 0; i < n; ++i)
pour (int j = 0; j < n; ++j)
dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j];

Total int = 1 << n, ans = 0;

pour (int masque = 0; masque < total; ++masque) {
bool ok = true;
pour (int i = 0; i < n && ok; ++i)
pour (int j = i + 1; j < n; ++j)
si ((masque >> i) et 1) == 0 && (masque >> j) et 1) == 0)
si (dist[i][j] > maxDistance) ok = faux;
si (ok) ++ans;
}
le retour des an;
}
};
«» "

---

# # # # # # # Bonne, mauvaise et laid dans l'espace de solution

**Aspect**
C'est pas vrai.
**Observational Insight**= *Key* – les noeuds de fermeture ne peuvent raccourcir le trajet le plus court. Difficile à repérer sans penser à la contraction du graphique. Autres Les intervieweurs demandent souvent *pourquoi* les distances précomputantes sont sûres. Autres
**Simplicité algorithmique**= Effacer `O(n3)` pré-computation + filtre bitmask. Peut sembler trop de boucles pour les débutants. Le Floyd-Warshall triple-néché peut se sentir lourd dans d'autres contextes. Autres
**Échelle**= Fonctionne pour `n ≤ 10`.= Pour un `n` plus grand, le facteur `2n` devient impossible.= Si `n` étaient 20+, nous aurions besoin d'une stratégie différente (par exemple, DP + BFS). Autres
**Lisibilité de l'implémentation** Chaque version de langue est ~50 lignes. Trop de tableaux temporaires si vous recalculez les distances par sous-ensemble. L'utilisation de listes d'adjacence pour chaque sous-ensemble (force brute) conduit à un code difficile à déboguer. Autres
**Mémoire d'empreintes de l'objet** Même chose.

---

# # # 8.

Piège
- Oui.
**Bords multiples** – garder le poids minimum*. Dans l'étape d'initialisation, toujours `min(w, dist[u][v]`. Autres
** Graphique disjoint** – Certaines paires peuvent ne jamais se connecter (`INF`). Traiter `INF` > `maxDistance` comme invalide; le sous-ensemble sera rejeté. Autres
**Tous les nœuds sont fermés** – Assurez-vous de compter ce sous-ensemble. Dans la boucle sous-ensemble, si * aucun nœud actif* existe, `ok` reste `True`. Autres
**Large `maxDistance`** – > 1e9 – assurez-vous que votre `INF` est plus grand. Utiliser `1e9` ou `Long.MAX_VALUE` en conséquence. Autres

---

N° 9 : Conseils d'entrevue

1. **Démarrer par l'observation**: La fermeture des sommets peut raccourcir un sentier le plus court. (en milliers de dollars)
2. **Mention pré-computation**: un Floyd-Warshall sur le graphique complet.
3. **Afficher la logique bitmask** – itérer tous les sous-ensembles, filtrer les distances par paire.
4. **Discuss Complexité** – `n` est minuscule, donc 1024 sous-ensembles sont très bien.
5. **Demander des questions précises** – p. ex., l'ensemble actif vide est-il considéré comme valide?

---

Conclusion

LeetCode 2959 est un beau mélange de combinatoire et de théorie graphique.
- Oui. La partie *bon* est l'élégante idée qu'une matrice précalculée de toutes les paires suffit.
- La partie *mauvaise* est qu'il est facile d'ignorer l'impossibilité de raccourcir le chemin et finir par recalculer les distances pour chaque sous-ensemble.
- Oui. La partie *ugly* traite de multiples bords et veille à ce que la valeur `INF` soit suffisamment élevée.

Avec les extraits de code ci-dessus, vous êtes prêt à soumettre ou à distribuer une solution propre dans **Java, Python ou C++**. Bonne chance lors de votre prochaine entrevue de codage – ce problème est une grande vitrine de la façon dont une petite observation peut transformer un défi apparemment difficile en une solution parfaitement gérable.