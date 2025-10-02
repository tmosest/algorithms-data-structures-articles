---
titre: LeetCode 3327. Vérifiez si les cordes DFS sont des palindromes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Article du blog – Le bon, le mauvais et le mauvais de **LeetCode 3327**

### TL;DR
LeetCode 3327 vous demande de décider, pour chaque nœud d'un arbre enraciné, si la chaîne produite par un DFS **post-order** est un palindrome.
La solution "Easy" qui reconstruise simplement la chaîne pour chaque noeud est **O(n2)** et sera time-out sur la limite 105.
La solution la plus rapide acceptée utilise **passage post-commande + double laminage-hash** pour tester les palindromes dans le temps **O(n)** et la mémoire **O(n)** – la partie "bonne".
La partie "bad" est la subtilité de gérer correctement l'ordre inverse.
La partie "gugly" ? Un couple de nombres magiques (deux modules primaires) et la nécessité de pré-calculer les pouvoirs – mais ce sont des tours communs que vous allez apprendre à aimer.

> ** Mots-clés du référencement**: *Leetcode 3327, Vérifiez si les cordes DFS sont des palindromes, Tree Palindrome DFS, solution Java, solution Python, solution C++, Hash roulant, détection de Palindrome, prép d'entrevue, interview algorithmique, Tree traversal, DFS post-commande, analyse de complexité*

---

- Oui. 1. Aperçu du problème

«» "
Entrée :
parent[0...n-1] (parent[0] = -1, tous les autres parents[i] [0,n-1])
s[0...n-1] (lettres minuscules)

Définition:
dfs(x):
pour chaque enfant y de x en ordre croissant
dfs(y)
ajouter s[x] à une chaîne globale dfs Échelle

Tâche :
Pour chaque noeud i, commencez par un dfsStr vide, appelez dfs(i) et définissez
réponse[i] = true iff les dfs résultants Str est un palindrome.

Contraintes: 1 ≤ n ≤ 105
«» "

- Oui. 2. Intuition

La chaîne produite par `dfs(v)` est exactement:

«» "
S(v) = S(enfant1) + S(enfant2) + ... + S(enfantk) + s[v]
«» "

où les enfants sont traversés dans l'ordre ** croissant**.
Essai de palindrome pour `S(v)` nous obligerait normalement à construire la chaîne entière pour chaque noeud – **O(n2)** – ce qui est impossible pour n = 105.

L'observation clé :
**Nous pouvons calculer un hachage vers l'avant et un hachage inverse de chaque `S(v)` dans une passe ascendante. **
Si les deux hachages correspondent (pour deux modules différents), `S(v)` est un palindrome à faible probabilité de collision astronomique.

C'est vrai. Hachage vers l'avant
«» "
H_f(v) = ((( ( H_f(child1) * P^{len(child1)} + H_f(child2) ) * P^{len(child2)} + ... ) * P + code(s[v])
«» "

C'est vrai. Hash inverse
Le revers de `S(v)` est
«» "
inverse(S(v)) = s[v] + inverse(S(childk)) + ... + inverse(S(child1))
«» "
Nous devons donc construire le hachage dans l'ordre des enfants inversés**:

«» "
H_r(v) = (( code(s[v]) * P^{len(childk)} + H_r(childk) ) * P^{len(childk-1)} + H_r(childk-1) ) ...
«» "

Les deux hachages exigent également la longueur exacte de la corde à chaque noeud (`len[v]`) et les pouvoirs de la base `P`.

---

- Oui. 3. Approche naïve

'`python
def dfs(v):
pour les enfants[v]:
dfs(enfant)
res.append(s[v])

résoudre():
ans = [Faux]* n
pour v dans la plage(n):
Res.clear()
dfs(v)
ans[v] = res == res[:-1] # reconstruire & inverser
«» "

*Temps*: <<Sv>=O(n2)>
*Mémorie*: O(n) par appel – la récursion de la pile va exploser en Java ou C++.

**Résultat**: TLE sur les tests moyens et durs.
Donc nous devons faire quelque chose de plus intelligent.

---

- Oui. 4. Approche optimisée – O(n) avec double glissière

Étape Quoi calculer Pourquoi ?
- C'est quoi ?
Construisez une liste d'adjacence.
Après-commande DFS (bottom-up)
Comparer les hachages (mod1 & mod2) Essai de palindrome

Pré-computation

«» "
P1 = 91138223, MOD1 = 1_000_000_007
P2 = 972663749, MOD2 = 1_000_000_009
pow1[i] = P1^i (mod MOD1)
pow2[i] = P2^i (mod MOD2)
«» "

Nous précalculons les pouvoirs jusqu'à n de sorte que la combinaison d'un hasch enfant n'a besoin qu'une seule multiplication et addition.

Formule ascendante (avant)

«» "
Valeur = 0
pour les enfants[v] # ordre croissant
val = (val * pow1[len[enfant]] + H_f[enfant]) % MOD1
val = (val * pow2[len[child]] + H_f[child]) % MOD2

val = (val * P1 + code(s[v])) % MOD1
val = (val * P2 + code(s[v])) % MOD2

H_f[v] = valeur
«» "

Formule ascendante (inverse)

«» "
Valeur = 0
val = (code(s[v]) * 1) % MOD1
val = (code(s[v]) * 1) % MOD2

pour enfant inversé(enfants[v]): # ordre inverse
val = (val * pow1[len[enfant]] + H_r[enfant]) % MOD1
val = (val * pow2[len[child]] + H_r[child]) % MOD2

H_r[v] = valeur
«» "

*Note*: `code(ch)` est simplement `ord(ch) - ord('a') + 1`.

Contrôle du Palindrome

«» "
réponse[v] = (H_f[v] == H_r[v]) # Les deux paires de modules doivent correspondre
«» "

---

- Oui. 5. Détails de la mise en œuvre

Voici les solutions **ready‐to-paste** dans **Java, Python et C++**.
Tous utilisent le même squelette algorithmique : construire l'arbre, pré-calculer les pouvoirs, effectuer un DFS post-commande *itative*, puis comparer les deux hachages.

> **Important** – nous utilisons *deux* moduli pour maintenir la probabilité de collision négligeable.
> Le code est fortement commenté de sorte que vous pouvez comprendre chaque étape sans le besoin d'inverser l'ingénieur.

---

##### 5.1 Java (Java 17)

"Java
importation java.io.*;
Importation de java.util.*;

solution de classe publique {
MOD1 = 1_000_000_007L;
MOD2 = 1_000_000_009L;
base1 = 9113823323L; // toute prime aléatoire < MOD1
interne statique finale longue BASE2 = 972663749L; // toute prime aléatoire < MOD2

public statique vide main(String[] args) lance IOException {
FastScanner fs = nouveau FastScanner (System.in);
int n = fs.nextInt();
int[] parent = nouveau int[n];
pour (int i = 0; i < n; i++) parent[i] = fs.nextInt();
char[] s = fs.next().àCharArray();

// 1. Créer des listes d'enfants
Liste <entier>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) g[i] = nouveau tableau <>();
pour (int i = 1; i < n; i++) g[parent[i]].add(i);
pour (int i = 0; i < n; i++) Collections.sort(g[i]);

// 2. Pouvoirs de précalcul
long[] pow1 = nouveau long[n + 1];
long[] pow2 = nouveau long[n + 1];
pow1[0] = pow2[0] = 1;
pour (int i = 1; i <= n; i++) {
pow1[i] = (pow1[i - 1] * BASE1) % MOD1;
pow2[i] = (pow2[i - 1] * BASE2) % MOD2;
}

// 3. Post-commande itérative ascendante
int[] len = nouvelle int[n];
long[] hf1 = nouveau long[n], hf2 = nouveau long[n];
long[] hr1 = nouveau long[n], h2 = nouveau long[n];
booléen[] visité = nouveau booléen[n];
Deque<Integer> pile = nouvelle ArrayDeque<>();
pile.push(0);

pendant que (!stack.isEmpty()) {
int v = empil.peek();
si (!visité[v]) {
visité[v] = vrai;
pour (int enfant : g[v]) empil.poush(enfant);
} autre {
pile.pop();
// longueur du calcul
= 1;
pour (int child : g[v]) total += len[child];
len[v] = total;

// Hash avant
long f1 = 0, f2 = 0;
pour (int enfant : g[v]) {
f1 = (f1 * pow1[len[enfant]] + hf1[enfant]) % MOD1;
f2 = (f2 * pow2[len[enfant]] + hf2[enfant]) % MOD2;
}
f1 = (f1 * BASE1 + (s[v] - 'a' + 1)) % MOD1;
f2 = (f2 * BASE2 + (s[v] - 'a' + 1)) % MOD2;
hf1[v] = f1; hf2[v] = f2;

// hachage inverse
longue r1 = (s[v] - 'a' + 1) % MOD1;
long r2 = (s[v] - 'a' + 1) % MOD2;
pour (int i = g[v].size() - 1; i >= 0; i--) {
l'enfant int = g[v].get(i);
r1 = (r1 * pow1[len[enfant]] + hr1[enfant]) % MOD1;
r2 = (r2 * pow2[len[enfant]] + h2[enfant]) % MOD2;
}
hr1[v] = r1; hr2[v] = r2;
}
}

// 4. Construire la réponse
StringBuilder out = nouveau StringBuilder();
pour (int i = 0; i < n; i++) {
boolean ok = (hf1[i] == hr1[i]) && (hf2[i] == hr2[i]);
out.append(ok ? "vrai" : "faux");
si (i + 1 < n) ou.annexe(' ');
}
Système.out.println(out);
}

/* --------- scanner rapide ---------- */
classe statique privée FastScanner {
entrée finale privée;
octet final privé[] tampon = nouvel octet[1 << 16];
Int privé ptr = 0, len = 0;
FastScanner(InputStream in) { this.in = in; }
int private readByte() lance IOException {
si (ptr >= len) {
len = in.read(buffer);
ptr = 0;
si (len <= 0) retour -1;
}
retour du tampon[ptr++];
}
int nextInt() lance IOException {
int c, signe = 1, val = 0;
pendant que (c = readByte()) <= ') si (c == -1) retourne -1;
si (c) { signe = -1; c = readByte(); }
alors que (c > ' ') { val = val * 10 + c - '0'; c = readByte(); }
val de retour * signe;
}
Chaîne suivante() lance IOException {
StringBuilder sb = nouveau StringBuilder();
Int c;
pendant que (c = readByte()) <= ') si (c == -1) retourne null;
pendant que c > ' ' ) { sb.append(char) c); c = readByte(); }
retour sb.toString();
}
}
}
«» "

---

5.2 Python

'`python
importations
de collections import defaultdict, deque

MOD1 = 1_000_000_007
MOD2 = 1 000 000 009
BASE1 = 91138223
BASE2 = 972663749

résoudre():
données = sys.stdin.read().strip().split()
it = iter(données)
n = int(next(it))
parent = [int(next(it)) pour _ dans la plage(n)]
s = liste(suivant(it))

# Construire un arbre
g = [[] pour _ dans l ' intervalle n)]
pour i dans la plage (1, n):
g[parent[i]].appendice(i)
pour la première en g:
Ist.sort()

# Pouvoirs précalculés
pow1 = [1]*(n+1)
pow2 = [1]*(n+1)
pour i dans la plage(1, n+1):
pow1[i] = (pow1[i-1] * BASE1) % MOD1
pow2[i] = (pow2[i-1] * BASE2) % MOD2

# DSV ascendante
lenv = [0]*n
hf1 = [0]*n; hf2 = [0]*n
hr1 = [0]*n; h2 = [0]*n
visité = [Faux]*n
pile = [0]
pendant la pile:
v = pile[-1]
si elle n'est pas visitée[v]:
visité[v] = Vrai
pour c en g[v]: pile.append(c)
Sinon:
Pile.pop()
Total = 1
pour c en g[v]: total += lenv[c]
lenv[v] = total

# hachage vers l'avant
f1, f2 = 0, 0
pour c en g[v]:
f1 = (f1 * pow1[lenv[c]] + hf1[c]) % MOD1
f2 = (f2 * pow2[lenv[c]] + hf2[c]) % MOD2
f1 = (f1 * BASE1 + (ord(s[v]) - 96)) % MOD1
f2 = (f2 * BASE2 + (ord(s[v]) - 96)) % MOD2
hf1[v], hf2[v] = f1, f2

# hachage inversé
r1, r2 = (ord(s[v]) - 96) % MOD1, (ord(s[v]) - 96) % MOD2
pour c en sens inverse(g[v]):
r1 = (r1 * pow1[lenv[c]] + hr1[c]) % MOD1
r2 = (r2 * pow2[lenv[c]] + hr2[c]) % MOD2
hr1[v], hr2[v] = r1, r2

ans = [ (hf1[i]==hr1[i] et hf2[i]==hr2[i]) pour i dans l'intervalle(n) ]
print(' '.join('true' if x other 'false' for x in ans))

si __nom__ == "__main__" :
résoudre()
«» "

---

#### 5.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue MOD1 = 1'000'000'007LL;
longue MOD2 = 1'000'000'009LL;
Const longue BASE1 = 911382323LL; // prime aléatoire < MOD1
Const longue BASE2 = 972663749LL; // prime aléatoire < MOD2

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

l'élément n;
si (!(cin >> n)) retourner 0;
vecteur<int> parent(n);
pour (int i = 0; i < n; ++i) cin >> parent[i];
str; cin >> str;
vecteur <char> s(str.begin(), str.end());

// Créer une liste d'enfants
vecteur<vector<int>> g(n);
pour (int i = 1; i < n; ++i) g[parent[i]].push_back(i);
pour (int i = 0; i < n; ++i) tri(g[i].debut(), g[i].end());

// Pouvoirs précalculateurs
vecteur <long> pow1(n + 1, 1), pow2(n + 1, 1);
pour (int i = 1; i <= n; ++i) {
pow1[i] = (pow1[i-1] * BASE1) % MOD1;
pow2[i] = (pow2[i-1] * BASE2) % MOD2;
}

// DSV itérative ascendante
vecteur<int> len(n, 0);
vecteur <long long> hf1(n), hf2(n), hr1(n), hr2(n);
vecteur<bool> vis(n, false);
vector<int> pile = {0};

pendant que (!stack.vide()) {
int v = pile.back();
si (!vis[v]) {
vis[v] = vrai;
pour (int child : g[v]) pile.push_back(child);
} autre {
pile.pop_back();
= 1;
pour (int child : g[v]) total += len[child];
len[v] = total;

// Hash avant
long f1 = 0, f2 = 0;
pour (int enfant : g[v]) {
f1 = (f1 * pow1[len[enfant]] + hf1[enfant]) % MOD1;
f2 = (f2 * pow2[len[enfant]] + hf2[enfant]) % MOD2;
}
f1 = (f1 * BASE1 + (s[v] - 'a' + 1)) % MOD1;
f2 = (f2 * BASE2 + (s[v] - 'a' + 1)) % MOD2;
hf1[v] = f1; hf2[v] = f2;

// hachage inverse
long r1 = (s[v] - 'a' + 1) % MOD1;
long r2 = (s[v] - 'a' + 1) % MOD2;
pour (int i = (int)g[v].size() - 1; i >= 0; --i) {
enfant int = g[v][i];
r1 = (r1 * pow1[len[enfant]] + hr1[enfant]) % MOD1;
r2 = (r2 * pow2[len[enfant]] + h2[enfant]) % MOD2;
}
hr1[v] = r1; hr2[v] = r2;
}
}

// Produit
pour (int i = 0; i < n; ++i) {
bool ok = (hf1[i] == hr1[i]) && (hf2[i] == hr2[i]);
<< (ok ? « vrai » : « faux ») << (i + 1 < n ? » : «\n »);
}
}
«» "

---

- Oui. 6. Analyse de la complexité

Opération de complexité temporelle de complexité mémoire Autres
[En milliers de dollars des États-Unis]
Arbre de construction Autres
Puissance avant le calcul Autres
Délivrance itérative après l'ordre
Réponse finale Autres

Dans l'ensemble: **'O(n)' temps, `O(n)` mémoire** – bien dans les limites pour 105 nœuds.

---

- Oui. 7. Résumé

- **Problème** : Déterminer si chaque noeud est un palindrome.
- **Naïve**: O(n2) – échoue.
- **Optimisé**: Utilisez *double hachage roulant* avec *bottom-up* traversal, calculant des hachages avant et inverse dans des ordres d'enfant corrects.
- **Complexité**: temps «O(n)», mémoire «O(n)».
- **Toutes langues**: La même logique, avec des commentaires clairs et des E/S rapides.

Avec cette solution, vous pouvez affronter avec confiance tout test moyen/dur dans LeetCode **Postorder DFS Palindrome** ou des problèmes similaires de hachage d'arbre. Bonne chance, et le codage heureux!