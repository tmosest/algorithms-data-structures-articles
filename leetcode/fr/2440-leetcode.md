---
titre: LeetCode 2440. Créer des composants avec la même valeur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2440 – Créer des composants avec la même valeur
### Un guide complet (Java-Python-C++) + SEO-Optimized Blog Post

---

- Oui. 1. Récapitulation des problèmes
On vous donne un **tree** avec des nœuds `n` (`0 ... n‐1`).
- "nums[i]" est la valeur du noeud `i`.
- Les «edges» décrivent l'arbre non dirigé.

Vous pouvez **supprimer n'importe quel nombre de bords**.
Après les suppressions, l'arbre se divise en plusieurs composants connectés.
La *valeur* d'une composante est la somme de `nums[i]` pour tous les nœuds de cette composante.

**Objectif:**
Retourne le nombre maximum de bords** qui peut être supprimé de telle sorte que *chaque composante* ait la même valeur**.

---

- Oui. 2. Intuition – Pourquoi la factorisation importe

Laissez :

* `S` = somme totale de toutes les valeurs de nœuds.
* `k` = nombre de composants que nous souhaitons créer.
* `T` = valeur de chaque composant.

Nous avons la relation
«» "
S = k × T
«» "
Par conséquent, `T = S/k`.
Pour une partition valide `S` doit être divisible par `k`.
Les nombres possibles de composants sont donc les **diviseurs de `S`**.

**Idée** – Pour chaque diviseur `k`
1. calculer `cible = S/k`
2. exécutez un DFS qui maintient une somme de sous-arbre en cours d'exécution
3. chaque fois qu'un sous-arbre est égal à "cible", il peut devenir un composant (couper le bord à son parent)
4. Si nous nous retrouvons avec des composants exactement `k`, la réponse est `k‐1` (nous coupons les bords `k‐1`).

---

- Oui. 3. Aperçu de l'algorithme

«» "
1. Construire une liste d'adjacence de l'arbre.
2. Calculer la somme totale S des nombres.
3. Trouvez tous les diviseurs de S (O( √S)).
4. Pour chaque diviseur k (nombre de composants):
cible = S/k
exécuter DFS à partir de la racine (tout noeud, p.ex. 0)
- retourne la somme du sous-arbre actuel
- si la somme est retournée == cible:
count++ (un composant est terminé)
retour 0 (ne pas propager cette somme)
- autre
retourner sous-tree_sum
Après DFS:
si le nombre == k:
ans = max(ans, k-1)
5. Retourner
«» "

**Complexités* *
* Heure* : `O(n * d)` où `d` = nombre de diviseurs de `S` (= ~103 pour les contraintes).
*Espace*: `O(n)` pour la liste d'adjacence + pile de récursion.

---

- Oui. 4. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

> **Note:** Toutes les solutions supposent des indices de nœuds 0 et que les "edges" d'entrée forment un arbre valide.

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
composant int publicValue(int[] nums, int[[]] bords) {
int n = longueur nums;
// 1. Créer une liste d'adjacence
Liste<Liste<Intégrée>> adj = nouvelle liste de distribution<>(n);
pour (int i = 0; i < n; i++) adj.add(new ArrayList<>());
pour (int[] e : bords) {
adj.get(e[0]).add(e[1]);
adj.get(e[1]).add(e[0]);
}

// 2. Montant total
= 0;
pour (int v : nombres) total += v;

// 3. Obtenez tous les diviseurs du total
Liste <entier> diviseurs = getDivisors(total);

int best = 0;
pour (int k : diviseurs) {
int cible = total / k;
nombre int[] = {0};
Si (dfs(0, -1, adj, nombres, cible, nombre) == 0) { // racine devrait également terminer un composant
if (count[0] == k) best = Math.max(best, k - 1);
}
}
le meilleur retour;
}

Int privé dfs(int node, int parent, Liste<Liste<entier>> adj,
int[] nombres, cible int, nombre int[] {
la somme int = nombres[node];
pour (int nb : adj.get(node)) {
si (nb) le parent continue;
int sub = dfs(nb, noeud, adj, nombres, cible, nombre);
si (sub== cible) {
count[0]++; // un composant est terminé
} autre {
sum += sub; // se propager
}
}
la somme de retour;
}

liste privée<integer> getDivisors(int x) {
Liste <Integer> res = nouvelle liste de distribution<>();
pour (int i = 1; i * i <= x; i++) {
si (x % i) 0) {
l'alinéa i est remplacé par le texte suivant:
si (i != x / i) res.add(x / i);
}
}
retour rés;
}
}
«» "

---

4.2 Python

'`python
importations
de collections importer par défautdict
de taper l'importation Liste

sys.setrecursionlimit(200_000) # sécurité pour les arbres profonds

Solution de classe:
élément Valeur(même, nombres: List[int], bords: List[List[int]]) -> Int:
n = len(nums)

# liste d'adjacence
adj = defaultdict(list)
pour a, b dans les bords:
adj[a].appendice(b)
adj[b].append(a)

total = somme(s)
diviseurs = auto.get_diviseurs(total)

meilleur = 0
pour k dans les diviseurs:
cible = total // k
cnt = 0

def dfs(u, p):
non locaux
s = nombres[u]
pour v in adj[u]:
si v == p: continuer
sous = dfs(v, u)
si sous == cible:
cnt += 1
Sinon:
s += sous
retour s

root_sum = dfs(0, -1)
# composant racine doit également être compté
si root_sum == cible:
cnt += 1
Si cnt == k:
best = max (meilleur, k - 1)
le meilleur retour

@staticmethod
def get_divisors(x: int) -> Liste[int]:
res = []
i = 1
alors que i * i <= x:
Si x % i] 0:
res.append(i)
i != x // i:
res.append(x // i)
i += 1
retour res
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int componentValue(vecteur<int>& nombres, vecteur<vecteur<int>>& bords) {
int n = nombres.size();
vecteur<vecteur<int>> adj(n);
pour (auto &e: bords) {
adj[e[0]].push_back(e[1]);
adj[e[1]].push_back(e[0]);
}

long total = 0;
pour (int v : nombres) total += v;

vecteur<int> diviseurs = getDivisors(total);

int best = 0;
pour (int k : diviseurs) {
longue cible longue = total / k;
cnt = 0;
fonction<long long(int,int)> dfs = [&](int u, int p)->long long {
longue somme longue = nombres[u];
pour (int v : adj[u]) si (v != p) {
long sub = dfs(v,u);
si (sub) cible ++cnt;
autre somme += sous;
}
la somme de retour;
};

longue racine Somme = dfs(0,1);
si (rootSum == cible) ++cnt; // root termine un composant

si (cnt) k) le meilleur = max (meilleur, k-1);
}
le meilleur retour;
}

particulier:
vector<int> getDivisors(long long x) {
vecteur<int> rés;
pour (long long i = 1; i * i <= x; ++i) {
si (x % i) 0) {
le nom de l'autorité compétente de l'État membre d'origine;
si (i != x / i) res.push_back((int)(x / i));
}
}
retour rés;
}
};
«» "

---

- Oui. 5. Billet de blogs – Bon, Mauvais et Ugly - pour LeetCode 2440
*(SEO-Optimisé, prêt à l'entrevue, propice à l'embauche)*

---

#### 5.1 Titre (SEO)
**LeetCode 2440 – Partition des arbres Facile : stratégie de factorisation DFS (Java/Python/C++)**

*Mots clés*: LeetCode, code d'entrevue, arbre DP, DFS, factorisation, partition d'arbre, entretien de codage, conception d'algorithme, OOP, récursion, C++, Java, Python, entretien d'emploi, ingénieur logiciel senior, résolution de problèmes

---

5.2 Aperçu

Ce que vous allez apprendre Pourquoi ça compte
-- -- -- -- -- -- -- -- --
Bons #1 Diviseurs → seulement 1/3 de l'espace de recherche. Un DFS qui coupe automatiquement les sous-arbres. <br> 3=1 Nettoyez le code avec les listes d'adjacence. Gagne du temps, bat 100% dans les concours, démontre une profonde compréhension des problèmes. Autres
Mauvais Le DFS récursif peut faire sauter la pile sur des arbres énormes. <br> 2=2 Ne pas manipuler des valeurs négatives ou des indices basés sur 0 peut conduire à des bogues. *br> 3 Oublier de compter le composant racine. Ces erreurs coûtent des points d'entrevue et peuvent briser votre solution sur de grandes entrées. Autres
Ugly Sur-optimisation précoce (pirates bit, DP fantaisie) peut rendre le code illisible. L'utilisation de variables globales au lieu de passer l'état conduit à des bogues difficiles à détecter. *br> 3 Le mélange d'entier et de long conduit à un débordement. Ugly code peut passer des tests, mais ne parvient pas à impressionner les recruteurs qui apprécient la maintenance. Autres

---

5.3 Article complet

> **Commencez la lecture** si vous êtes en train de vous préparer à une interview **ingénieur logiciel**, voulez maîtriser **problèmes d'arbre**, ou tout simplement aimer des solutions algorithmiques propres.

---

Introduction

Dans le monde du codage des entrevues, les problèmes de LeetCode qui impliquent **trees** apparaissent souvent dans la difficulté **moyen–hard**.
Problème 2440 – -Créer des composants avec la même valeur – est un exemple parfait qui combine trois concepts classiques:

1. **Depth‐First Search (DFS)** – marcher sur l'arbre.
2. **Factorisation / dénombrement des diviseurs** – pour relier l'espace de recherche.
3. **Comptabilité des composants de la graisse** – pour décider où couper les bords.

Maîtriser ce problème met en évidence votre capacité à **transférer les contraintes mathématiques en étapes algorithmiques**, une compétence hautement appréciée par les gestionnaires d'embauche chez FAANG, Google, Microsoft, et d'autres entreprises de haute technologie.

---

C'est vrai. Pourquoi ce problème est Interview-Gold

- **Les arbres sont partout**: Systèmes de fichiers, organigrammes, mondes de jeux, etc.
- **Edge delete / component separation** est une opération du monde réel (p. ex., clustering, network partitioning).
- Oui. La solution nécessite ** de penser en termes de sommes et de diviseurs**, allant au-delà de la force brute naïve.
- Démontre la prise de conscience du temps-espace** (en utilisant la factorisation pour garder la complexité faible).

---

#### Step-by-Step Walkthrough (bon, mauvais, moche)

Autres La phase est bonne
- C'est quoi ?
**1. Créer un graphique**. Utiliser `ArrayList`/`vector<vector<int>>` – clair, O(n). Vérifications manuelles de l'index → erreurs hors-par-un. Adjacence codée en dur (tableau statique de taille 20000) – mémoire gaspillée. Autres
**2. Somme totale** Oublier d'utiliser longtemps dans C++ → débordement. Ne pas convertir `nums` à long en Java – pourrait déborder si les valeurs atteignent 105. Autres
**3. Énumération du diviseur**. Récursif détecteur de diviseur (débordement de la pile). Tri des diviseurs inutilement – extra O(d log d). Autres
**4. DFS** Revenir `sous` conduit directement au double comptage. Mélanger la valeur globale de compteur et de retour → difficile à déboguer. Autres
**5. Compter les composants**. Utilisez une variable locale `int[1]` ou `cnt` – thread‐safe. Oublier pour incrémenter le composant racine → mauvaise réponse pour le cas de composant unique. Dénombrement via la variable statique → état statique entre les cas d'essai. Autres

---

Cas couverts

Autres Décision Pourquoi il importe de savoir comment la solution la gère
- C'est pas vrai.
Autres **Un seul noeud**=Aucun bord à couper.=DFS retourne `cible`; racine comptée → `k=1`, réponse `0`. Autres
**Toutes les valeurs des nœuds sont égales. Les diviseurs de `S` comprennent tous les `k` jusqu`à `n`. Autres
**Valeurs élevées** "long" (C++), "int" (Java/Python) suffit parce que "n ≤ 2e4", "nums[i] ≤ 1e5". Autres

---

Les pensées finales – Pourquoi vous devriez maîtriser Cette

- **Clarté algorithmique**: Le problème est un exercice parfait pour démontrer **FDS + raisonnement mathématique**.
- **Effet d'entrevue** : Expliquer la factorisation au cours d'une entrevue montre la profondeur des connaissances au-delà du simple code. (en milliers de dollars)
- ** Style de codage**: Fonctions propres, testables, noms de variables explicites, aucun nombre magique – attributs recruteurs cherchent.

---

Prêt à coder ?

- Copiez/collez la solution **Java** dans votre boîte de soumission LeetCode.
- Essayez la version **Python** dans votre environnement local ou tout interprète en ligne.
- Compiler l'extrait **C++** avec `g++ -std=c++17 main.cpp && ./a.out`.

Bon codage ! Les

---

- Oui. 6. TL;DR pour le lecteur

1. **Somme totale → Diviseurs → DFS**
2. Pour chaque diviseur `k`, somme cible = `S / k`.
3. Couper un bord quand une somme de sous-arbres égale la cible.
4. Si vous pouvez obtenir exactement les composants `k` → réponse = `k‐1`.
5. Complexité: temps "O(n √S)", espace "O(n)".

Les trois implémentations linguistiques ci-dessus suivent ce schéma exact.

---

- Oui. 7. FAQ

C'est ce qu'il a dit.
-- -- -- -- -- --
Autres **Pourquoi utiliser des diviseurs au lieu d'essayer tous les `k` de 1 à n?**. Essayer tous `k` perdrait du temps. Autres
**La récursion est-elle sûre pour `n = 20000`?**= Oui. La plupart des langues permettent une profondeur de récursion de > 104. En Python, nous repoussons la limite. Autres
**Les valeurs peuvent-elles être négatives?** Le problème original de LeetCode utilise des valeurs non négatives, mais l'algorithme fonctionne aussi pour des sommes négatives – soyez juste prudent avec le débordement entier. Autres

---

- Oui. 8. À emporter pour les entrevues d'emploi

- **Afficher que vous pouvez réduire un espace de recherche** par le biais d'un aperçu mathématique (factorisation).
- **Expliquez votre DFS avec soin** – soulignez que couper un bord équivaut à retourner 0 vers le haut.
- **Parler des cas de bord** – un seul noeud, tous les valeurs la même, récursion profonde.
- **Durée d'exécution** – «O(n=6S)» est bien à l'intérieur des limites pour "n ≤ 2·104".

Un recruteur se souviendra que vous avez non seulement écrit le code correct, mais aussi * compris* les mathématiques sous-jacentes et codé dans **propre, idiomatique** style.

Bonne chance pour votre prochain entretien de codage ! - Oui