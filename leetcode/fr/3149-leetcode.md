---
titre: LeetCode 3149. Trouver le coût minimum Array Permutation -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3149 – Trouvez le coût minimum de permutation
**Code du leet : Interview-Ready

> **Pourquoi ce problème est important* *
> *Bit-mask DP + lexicographie tie-breaking* est un modèle d'entrevue classique.
> La maîtrise montre que vous pouvez :
> * Concevoir des solutions exponentielles avec taille.
> * Gérez des règles subtiles de rupture de cravate.
> * Écrire un code propre et idiomatique en plusieurs langues.

Ci-dessous vous trouverez:

1. Une solution complète, prête à la production** en Java, Python et C++
2. A **SEO-optimized blog post** qui marche à travers le *bon, le mauvais, et le laid* du problème
3. Conseils sur la façon d'utiliser ce défi pour poser votre prochaine entrevue de codage

---

- Oui. 1. Récapitulation des problèmes

Compte tenu d'une permutation `nums` de `[0,1,...,n‐1]` (`2 ≤ n ≤ 14`), nous devons produire une permutation `perm` du même ensemble que ** minimise* *

«» "
score(perm) ====perm[0] – nombres[perm[1]]
«» "

Si plusieurs permutations donnent le même score minimal, retournez le **lexicographiquement le plus petit**.

---

- Oui. 2. Idée de haut niveau

Nous traitons le problème comme une visite itinérante de style « vendeur » sur un graphique entièrement dirigé :

* ** Vertices** – les numéros `0 ... n‐1`.
* ** Poids moyen** de `a` à `b` – `a – nums[b].
* Nous devons trouver le cycle hamiltonien **poids minimum** qui commence à `0` (parce que tout cycle optimal peut être tourné pour commencer à `0` et le score est invariant en rotation).
* L'ordre du cycle sera la permutation "perm".

Avec `n ≤ 14`, un DP **bit-masque** ("O(n2·2n)") est assez rapide.

---

- Oui. 3. État DP

«» "
dp[last][masque] = score minimal d'un chemin qui:
• a déjà visité les sommets indiqués par 'masque'
• se termine au dernier sommet '
«» "

`mask` est un bitmask de longueur `n` (bit `i` est 1 si Vertex `i` a été visité).
Au départ, nous commençons par Vertex `0` avec seulement `0` visité (`masque = 1 << 0`).

**Transition* *

«» "
dp[next][masque] (1 << next)] =
min( dp[last][masque] +==dernier – nombres[next]==)
sur tous les suivants qui ne sont pas encore visités
«» "

**Base**

Lorsque tous les sommets sont visités (`masque == (1 << n) - 1`), nous fermons le cycle:

«» "
score = dp[dernier][masque]
«» "

Nous stockons le meilleur vertex *next* pour reconstruire la permutation optimale.

---

- Oui. 4. Léxicographie

Si deux choix donnent la même note totale, nous devons préférer l'indice plus petit parce que la permutation qui choisit le plus petit nombre plus tôt est lexicographiquement plus petite.

Dans la transition:

'`python
si candidat_score < best_score ou \
(candidate_score == best_score et suivant < best_next):
best_score = candidat_score
best_next = next
«» "

Cette règle se propage correctement à la réponse finale.

---

- Oui. 5. Code

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int[] findPermutation(int[] nums) {
int n = longueur nums;
Int FULL = (1 << n) - 1;
int[] dp = nouvelle int[n][1 << n];
int[]] suivante = nouvelle int[n][1 << n];
pour (int i = 0; i < n; i++) -1);

dfs(0, 1 << 0, nombres, dp, suivant, FULL);

// Reconstruire
int[] perm = nouvelle int[n];
masque int = 1 << 0;
int last = 0;
pour (int i = 0; i < n; i++) {
perm[i] = dernier;
int nx = suivant[dernier][masque];
masque=1 << nx;
dernier = nx;
}
retour permanent;
}

int dfs(int last, int mask, int nums,
int[][] dp, int[][] suivant, int FULL) {
si (dp[last][masque] != -1) retour dp[dernier][masque];
si (masque) Tous visités → fermer le cycle
retour Math.abs(dernier - nombres[0]);
}
int bestScore = entier.MAX_VALUE;
Int bestNext = -1;
pour (int nxt = 0; nxt < nums.longueur; nxt++) {
si ((masque et (1 < < nxt)) != 0) continuer; // déjà visité
nt cur = Math.abs(dernier - nombres[nxt]) + dfs(nxt, masque=1 << nxt),
nombres, dp, suivant, FULL);
if (cur < bestScore=" (cur == bestScore && nxt < bestNext)) {
bestScore = cur;
bestNext = nxt;
}
}
dp[last][masque] = meilleur score;
suivant[dernier][masque] =meilleurNext;
le meilleur retour Note;
}
}
«» "

---

5.2 Python

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def findPermutation(self, nombres: List[int]) -> Liste[int]:
n = len(nums)
FULL = (1 << n) - 1
best_next = [[-1] * (1 << n) pour _ dans l'intervalle(n)]

@lru_cache(Aucun)
def dp(dernier: int, masque: int) -> Int:
si masque == # fermer le cycle
abs(dernier - nombres[0])

meilleure = flotteur('inf')
best_nxt = -1
pour nxt dans la plage(n):
si masque & (1 << nxt):
poursuivre
cand = abs(dernier - nombres[nxt]) + dp(nxt, masque)
si cand < best ou (cand) == best et nxt < best_nxt):
meilleur = cand
best_nxt = nxt
best_next[dernier][masque] = best_nxt
le meilleur retour

dp(0, 1 << 0) # commencer à 0

Reconstruire
perm = []
masque = 1 << 0
dernier = 0
pour _ dans la plage(n):
(dernier)
nxt = best_next[last][masque]
masque= 1 << nxt
dernier = nxt
retour permanent
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findPermutation(vecteur<int>& nums) {
int n = nombres.size();
Int FULL = (1 << n) - 1;
vecteur<vector<int>> dp(n, vector<int>(1 << n, -1));
vecteur<vector<int>> nxt(n, vector<int>(1 << n, -1));

fonction<int(int,int)> résoudre = [&](int last, int mask) -> Int {
si (dp[last][masque] != -1) retour dp[dernier][masque];
si (masque) fermer le cycle
abs de retour (derniers - nombres[0]);

Int bestScore = INT_MAX;
Int bestNext = -1;
pour (int next = 0; next < n; ++next) {
si (masque & (1 << suivant)) continuer; // visité
int cur = abs(dernier - nums[next]) + resoudre(next, masque) (1 << next));
if (cur < bestScore=" (cur == bestScore && next < bestNext)) {
bestScore = cur;
bestNext = next;
}
}
dp[last][masque] = meilleur score;
nxt[dernier][masque] = meilleurNext;
le meilleur retour Note;
};

résoudre(0, 1 << 0); // commencer à partir de 0

// Reconstruire
vecteur<int> permanente;
masque int = 1 << 0;
int last = 0;
pour (int i = 0; i < n; ++i) {
perm.push_back(dernier);
int next = nxt[last][masque];
masque= 1 << suivant;
dernier = suivant;
}
retour permanent;
}
};
«» "

---

- Oui. 6. Complexité

Temps Mémoire
- C'est quoi ?
Java / Python / C++ () **O(n2 · 2n)** → ~ 2 × 106 opérations lorsque `n = 14' () **O(n · 2n)** entiers (~ 1 MiB)

Les deux fonctionnent confortablement sous la limite de 2 secondes de LeetCode.

---

- Oui. 7. Bien, les méchants, les méchants

Autres Phase Qu'est-ce qui s'est passé ?
-- -- -- -- -- -- -- -- -- -- --
**Bon**. • `n ≤ 14` → PDD exponentielle est viable. <br>• La rupture léxicographique est un petit ajout. <br>• Le cycle est invariant de rotation, donc fixer le début à `0` simplifie la reconstruction.
**C'est sans espoir. <br>• Oublier les "nums[next]` terme fait le poids de bord mal. La mauvaise transition conduit à ** scores incorrects** et une mauvaise réponse. Autres
• Certains intervieweurs utilisent le *revers* de "nums" ou un tableau basé sur 1. <br>• Les poids de bord peuvent être négatifs si vous oubliez la valeur absolue. <br>• La rupture de la cravate est facile à ignorer – vous pouvez retourner un cycle minimal *sub-lexicographiquement*. Nous l'avons résolu en ajoutant le tie-break `(candidate == best && next < best_next)` pendant DP. Autres

---

- Oui. 8. Cas de bord à tester

Autres Décision Pourquoi ça compte ?
-- -- -- -- -- -- -- -- --
Nombres = [0,1] Autres
"nums = [3,0,1,2,2]""" Cycle le plus petit avec des liens. Autres
Autres Tous les nombres identiques aux indices (`nums[i] = i`)) Autres
"nums" dans l'ordre décroissant. [0,1,2,...]

---

- Oui. 9. Comment utiliser ce problème dans votre préparation d'entrevue

1. **Showcase Multi-Language Skills** – Copier la même logique en Java, Python et C++ (ou toute autre langue).
2. **Discute de la Les intervieweurs aiment entendre votre intuition avant le code.
3. **Mettre en lumière la Lexicographie Tie‐Break** – De nombreux candidats manquent à cette règle subtile; expliquez-la clairement.
4. **Mention la deuxième limite** – Il montre que vous vous souciez de la performance et de l'analyse de la complexité.
5. **Préparer les questions de suivi** – Qu'en est-il si `n` avaient 20? – prêts à plonger plus profondément.

---

10. Appel à l'action

> **Vous voulez passer la prochaine entrevue de codage? * *
> Ajouter **LeetCode 3149** à votre demande.
> Poussez la solution vers une repo publique (GitHub, GitLab) et partagez le README avec le code exact pour Java, Python et C++.
> Écrivez un billet de blog (comme celui ci-dessus) et épinglez-le à **LinkedIn**, **Medium** ou **Dev.to**.
> Les recruteurs aiment voir des postes polis qui passent par votre processus de pensée.

---

Mots clés pour référencement

- LeetCode 3149 Trouver le coût minimum Array Permutation
- Bitmask DP problème de vendeur voyage
- Solution Java Python C++ LeetCode 3149
- Question d'entrevue de programmation dynamique bitmask
- Comment résoudre LeetCode 3149 en 5 minutes
- Optimiser le cycle hamiltonien avec la rupture du lien lexicographique
- Codage problème d'entrevue 3149
- Déposez un emploi avec LeetCode 3149

---

11. Réflexions finales

*Bit-mask DP* se sent intimidant, mais une fois que vous cassez le problème en états de quoi faire-next, la solution est systématique.
Le lien lexicographique** n'est qu'une minuscule règle supplémentaire qui maintient l'algorithme déterministe.

Maîtrisez ce défi, ajoutez les extraits de code propres ci-dessus à votre portfolio, et vous aurez un exemple concret, prêt à l'entrevue, de manipulation d'algorithmes exponentiels *avec finesse*.

Bon codage, et bonne chance pour votre prochaine interview! (en milliers de dollars)