---
titre: LeetCode 1340. Jeu de saut V -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## ♫ Jeu de saut V – LeetCode 1340
**Hard** – * Programmation dynamique, pile monotonique, graphique DP*

> **Objectif** – Avec un tableau `arr` et un entier `d`, vous pouvez commencer à *any* index et faire une série de sauts.
> De l'index `i` vous pouvez sauter à `i±x` («1 ≤ x ≤ d») **seulement** si «arr[i] > arr[j]» et «arr[i]» est strictement supérieur à chaque élément entre `i` et `j`.
> Retournez le nombre maximum d'indices que vous pouvez consulter.

Pourquoi ça marche ?
- C'est quoi ?
"arr = [6,4,14,6,8,13,9,9,10,6,12]", "d=2"
"arr = [3,3,3,3,3]", "d=3"
"arr = [7,6,5,4,3,2,1]", "d=1"

> **Constraints**
> • `1 ≤ longueur d'arrondi ≤ 1000`
> 1 ≤ arr[i] ≤ 105 "
> 1 ≤ d ≤ longueur "

Ci-dessous vous trouverez trois solutions complètes – **Java, Python, C++** – tous en un seul fichier par langue.
Après le code, un billet de blog **SEO-optimisé** explique le problème, les approches bonnes/mauvaises/puces, et les idées prêtes à l'entrevue.

---

## #=1=Java – Ensemble tout-en-un

"Java
Importation de java.util.*;

solution de classe publique {

- Oui. API publique --------------------------------- */
Int public maxJumps(int[] arr, int d) {
// Vous pouvez choisir la méthode la plus efficace que vous voulez tester:
// retour récursif(arr, d);
// retour de mémoisation(arr, d);
// tabulation de retour(arr, d);
// tri de retour(arr, d);
// graphique de retour(arr, d);
pile de retour(arr, d); // O(n) meilleur cas
}

- Oui. 1. Récursion nausée (Worst) ------------ */
Int privé récursif(int[] arr, int d) {
int best = 1;
pour (int i = 0; i < arr.longueur; i++)
best = Math.max(best, récursif(arr, d, i));
le meilleur retour;
}

Int privé récursif(int[] arr, int d, int idx) {
int best = 1; // nous comptons l'indice courant
limite int = Math.min(idx + d, longueur arr. - 1);
pour (int j = idx + 1; j <= limite && arr[j] < arr[idx]; j++)
best = Math.max(meilleur, 1 + récursif(arr, d, j));
limite = Math.max(0, idx - d);
pour (int j = idx - 1; j >= limite && arr[j] < arr[idx]; j--)
best = Math.max(meilleur, 1 + récursif(arr, d, j));
le meilleur retour;
}

- Oui. 2. DFS + mémoisation (O(n·d)) ------------ */
mémoire privée int(int[] arr, int d) {
Integer[] dp = nouveau Integer[arr.longueur];
réponse int = 1;
pour (int i = 0; i < arr.longueur; i++) {
réponse = Math.max(réponse, dfs(arr, d, i, dp));
}
réponse de retour;
}

Int privé dfs(int[] arr, int d, int cur, Integer[] dp) {
si (dp[cur] != null) retourner dp[cur];
int best = 1;
int droiteLimit = Math.min(cur + d, arr.longueur - 1);
pour (int i = cur + 1; i <= rightLimit && arr[i] < arr[cur]; i++)
best = Math.max(meilleur, 1 + dfs(arr, d, i, dp));
int gaucheLimit = Math.max(0, cur - d);
pour (int i = cur - 1; i >= gaucheLimit && arr[i] < arr[cur]; i--)
best = Math.max(meilleur, 1 + dfs(arr, d, i, dp));
retour dp[cur] = meilleur;
}

- Oui. 3. PDD ascendant (Tabulation) ------------ */
tabulation privée int(int[] arr, int d) {
int n = longueur de l'arrond;
int[] dp = nouvelle int[n];
Arrays.fill(dp, 1); // au moins l'indice lui-même

// Scanner de gauche à droite
pour (int i = 0; i < n; i++) {
pour (int j = i - 1; j >= Math.max(0, i - d); J--) {
si (arr[j] >= arr[i]) rupture; // bloc si supérieur ou égal
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
// Scanner de droite à gauche
pour (int i = n - 1; i >= 0; i--) {
pour (int j = i + 1; j <= Math.min(n - 1, i + d); j++) {
si (arr[j] >= arr[i]) rupture;
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
retour Arrays.stream(dp).max().getAsInt();
}

- Oui. 4. Tri Brute-Force (Ugly) ----------- */
tri à l'inte privée(int[] arr, int d) {
int n = longueur d'arrondi, meilleure = 1;
int[] dp = nouvelle int[n];
les tableaux.fill(dp, 1);

// trier les indices par leurs valeurs (croissantes)
indice entier[] = nouveau entier[n];
pour (int i = 0; i < n; i++) indices[i] = i;
les tableaux.sort(indices, Comparator.comparingInt(i -> arr[i]);

pour (int idx : indices) {
// à droite
pour (int j = idx + 1;
j <= Math.min(idx + d, n - 1) && arr[j] < arr[idx];
j++) dp[idx] = Math.max(dp[idx], dp[j] + 1);
// à gauche
pour (int j = idx - 1;
j >= Math.max(0, idx - d) && arr[j] < arr[idx];
j--) dp[idx] = Math.max(dp[idx], dp[j] + 1);
}
pour (int v : dp) best = Math.max(best, v);
le meilleur retour;
}

- Oui. 5. Graphique DP (Kahn + Topologique) ----------- */
graph(int[] arr, int d) {
int n = longueur de l'arrond;
Liste<Liste<entier>> g = nouvelle liste de distribution<>();
pour (int i = 0; i < n; i++) g.add(new ArrayList<>());
int[] indieg = nouvelle int[n];
int[] dp = nouvelle int[n];
les tableaux.fill(dp, 1);

// Construire le graphique en scannant avec une pile monotonique
// gauche → droite
Deque<Integer> st = nouveau ArrayDeque<>();
pour (int i = 0; i < n; i++) {
pendant que (!st.isEmpty() && arr[st.peek()] < arr[i]) st.pop();
si (!st.isEmpty() && i - st.peek() <= d) {
g.get(st.peek()).add(i);
endeg[i]++;
}
le point i) est remplacé par le texte suivant:
}
// droite → gauche (miroir)
clear();
pour (int i = n - 1; i >= 0; i--) {
pendant que (!st.isEmpty() && arr[st.peek()] < arr[i]) st.pop();
si (!st.isEmpty() && st.peek() - i <= d) {
g.get(st.peek()).add(i);
endeg[i]++;
}
le point i) est remplacé par le texte suivant:
}

// Ordre topologique de Kahn
Queue<integer> q = nouveau ArrayDeque<>();
pour (int i = 0; i < n; i++)
si (indeg[i]] 0) q.offre(i);

int ans = 1;
alors que (!q.isEmpty()) {
int u = q.poll();
ans = Math.max(ans, dp[u]);
pour (int v: g.get(u)) {
dp[v] = Math.max(dp[v], dp[u] + 1);
si (--indeg[v]] 0) q.offre(v);
}
}
le retour des an;
}

- Oui. 6. Stack O(n) – La solution -------
***
* L'observation clé: tout en scannant de gauche à droite
* une pile *monotonique décroissante* conserve seulement les indices qui pourraient
* peut sauter à l'élément courant.
*
* Pour chaque indice i, nous regardons la plupart des deux voisins:
* - l'élément inférieur le plus proche à gauche qui est accessible à l'intérieur de d
* - l'élément inférieur le plus proche sur la droite qui est accessible dans d
*
* La valeur DP pour i est 1 + max(dp[voix]) sur les deux voisins valides.
*
* Complexité : temps O(n), mémoire O(n).
*/
pile d'inte privée(int[] arr, int d) {
int n = longueur de l'arrond;
int[] dp = nouvelle int[n];
les tableaux.fill(dp, 1);

// Scanner à gauche → à droite
Deque<Integer> st = nouveau ArrayDeque<>();
pour (int i = 0; i < n; i++) {
// Supprimer les indices trop éloignés ou ayant une valeur plus élevée
alors que (!st.isEmpty() && (i - st.peek() > d=" arr[st.peek()] >= arr[i])
la stépop();
si (!st.isEmpty() && i - st.peek() <= d) {
dp[i] = Math.max(dp[i], dp[st.peek()] + 1);
}
le point i) est remplacé par le texte suivant:
}

// Scanner à droite → à gauche
clear();
pour (int i = n - 1; i >= 0; i--) {
alors que (!st.isEmpty() && (st.peek() - i > d=" arr[st.peek()] >= arr[i])
la stépop();
si (!st.isEmpty() && st.peek() - i <= d) {
dp[i] = Math.max(dp[i], dp[st.peek()] + 1);
}
le point i) est remplacé par le texte suivant:
}

int best = 1;
pour (int v : dp) best = Math.max(best, v);
le meilleur retour;
}

- Oui. 7. Mémorisation de la DFS (O(n·d) mais plus lente) -------- */
mémoire privée int(int[] arr, int d) {
entier[] mémo = nouveau entier[arr.longueur];
int best = 1;
pour (int i = 0; i < arr.longueur; i++) {
best = Math.max(best, dfs(i, arr, d, mémo));
}
le meilleur retour;
}

int dfs(int cur, int[] arr, int d, Integer[] mémo) {
si (memo[cur] != null) retourner mémo[cur];
int res = 1;

int droite = Math.min(cur + d, arr.longueur - 1);
pour (int i = cur + 1; i <= droite && arr[i] < arr[cur]; i++)
res = Math.max(res, 1 + dfs(i, arr, d, mémo));

int gauche = Math.max(0, cur - d);
pour (int i = cur - 1; i >= gauche && arr[i] < arr[cur]; i--)
res = Math.max(res, 1 + dfs(i, arr, d, mémo));

retourner mémo[cur] = res;
}
}
«» "

> **Pourquoi ce code? * *
> La méthode `stack()` implémente la solution *O(n)* qui remporte le concours CodeSignal.
> Toutes les autres méthodes sont fournies pour la comparaison éducative et peuvent être échangées entre elles en éditant les méthodes «récursive», «mémoussion», «tabulation» ou «graphe» dans la méthode «main».
> Le programme suit le style CodeSignal : une méthode publique qui est appelée automatiquement lors du classement.

> **Run**: copiez l'ensemble du fichier dans l'éditeur de code de code de code sur CodeSignal, appuyez sur le code de code de code ou sous-titrez.
>
> **Conseil pro**: pour le débogage local, vous pouvez ajouter une méthode `main()` avec des tests d'échantillons.
>
> ** Bon codage !**