---
titre: LeetCode 3649. Nombre de paires parfaites -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3649 – Nombre de paires parfaites
**Moyenne** – temps «O(n log n)», «O(n)» espace

> **Problème**
> On vous donne un nombre entier.
> Une paire d'indices `(i, j)` (avec `i < j`) est **perfect** iff, avec
> `a = nombres[i]` et `b = nombres[j] "
> `` "
> min.a - b.a + b.) <= min.a.b.)
> max. (a) - b)
> `` "
> Retournez le nombre de paires parfaites distinctes.

> **Exemples**
> *`nums = [0,12,3]` → `2` paires parfaites*
> *`nums = [-3,2,-1,4]` → `4` paires parfaites*
> *`nums = [1,10,100,1000]` → `0` paires parfaites*

---

TL;DR – Les mathématiques derrière la solution

Si l'on regarde seulement les valeurs *absolue* `x =.a.o` et `y =.b.o` et les trier de telle sorte que `x ≤.o`, les deux inégalités au-dessus s'effondrent à une seule condition de plage:

«» "
(x + 1) / 2 ≤ y ≤ 2 * x (1)
«» "

Donc une paire est parfaite **iff** la plus grande valeur absolue se trouve dans cet intervalle.

L'algorithme est donc:

1. Convertir chaque élément en sa valeur absolue.
2. Trie la liste.
3. Pour chaque élément `x` (à l'index `i`) compter combien d'éléments suivants `y` satisfont (1) à l'aide de la recherche binaire.
4. Somme tout compte – c'est la réponse.

L'astuce est que la recherche binaire nous donne le nombre de valeurs `y` dans la plage désirée dans le temps `O(log n)`.
complexité générale : **O(n log n)**.

---

Solutions complètes

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même logique décrite ci-dessus.

---

### Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public long perfectPairs(int[] nums) {
int n = longueur nums;
long[] abs = nouveau long[n];
pour (int i = 0; i < n; i++) {
abs[i] = Math.abs(long) nums[i]); // long pour éviter le débordement
}

les tableaux.sort(abs);

réponse longue = 0;
pour (int i = 0; i < n; i++) {
longueur x = abs[i];
longue gauche = (x + 1) / 2; // ceil((x+1)/2)
longue droite = 2 * x;

// indices du premier >= gauche et premier > droite
int lo = lowerBound(abs, gauche, i + 1, n);
int hi = hautBound(abs, droite, i + 1, n);

réponse += (long) (h - lo);
}
réponse de retour;
}

// premier index dans [départ, fin) avec arr[idx] >= cible
Int privé lowerBound(long[] arr, longue cible, int start, int end) {
int l = début, r = fin;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] < cible) l = m + 1;
autres r = m;
}
retour l;
}

// premier index dans [départ, fin) avec arr[idx] > cible
int upleBound(long[] arr, longue cible, int start, int end) {
int l = début, r = fin;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= cible) l = m + 1;
autres r = m;
}
retour l;
}
}
«» "

**Pourquoi c'est bon pour les interviews* *

Pourquoi ça compte ?
- Oui.
Prévient les débordements accidentels lors du calcul de "2*x" Autres
Conserve la boucle du cœur concise et auto-explication
O-notation dans les commentaires Afficher *pourquoi* chaque étape est efficace

---

Python

'`python
bisect d'importation

Solution de classe:
def perfectPairs(self, nombres: list[int]) -> Int:
# 1. Valeurs absolues + tri
abs_vals = trié(abs(x) pour x en nombres)

n = len(abs_vals)
ans = 0

pour i, x dans l'énumération(abs_vals):
gauche = (x + 1) // 2 # ceil(x+1)/2)
droite = 2 * x

# bisect_left/right travail sur toute la liste,
# donc nous coupons la vue qui nous intéresse réellement.
lo = bisect.bisect_left(abs_vals, gauche, i + 1, n)
hi = bisect.bisect_right(abs_vals, droite, i + 1, n)

ans += salut - lo

retour et
«» "

Le module `bisect`s de Python est un fin wrapper autour de la recherche binaire C=s, donnant la même performance `O(n log n)`.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long perfectPairs(vecteur<int>& nums) {
int n = nombres.size();
vecteur <long> absVals(n);
pour (int i = 0; i < n; ++i)
absVals[i] = llabs((long)nums[i]); // llabs -> long

tri(absVals.begin(), absVals.end());

long an = 0;
pour (int i = 0; i < n; ++i) {
long x = absVals[i];
longue gauche = (x + 1) / 2; // ceil
longue droite = 2 * x;

auto lo = lower_bound(absVals.begin() + i + 1, absVals.end(), gauche);
auto hi = upper_bound(absVals.begin() + i + 1, absVals.end(), droite);
ans += salut - lo;
}
le retour des an;
}
};
«» "

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Convertir en abs. Autres
Trier par `O(n log n)`" `O(1)` extra (en place)
Recherches binaires pour chaque `x`
**Total**** Autres

L'algorithme s'équilibre confortablement jusqu'aux contraintes maximales (`n = 100 000`, `="nums[i]=" ≤ 10^9`).

---

Bon, mauvais et moche – Ce que les intervieweurs À propos

Catégorie de l'intervieweur Comment la solution Excels / Falls Short
Il s'agit d'un projet pilote.
**Bon***Clarity*, *time-optimality*, *proof of concept*La simplification mathématique (1) est élégante; la recherche binaire maintient le code propre. Autres
**Bad**. *Handling of edge-cases*. Les valeurs zéros sont correctement comptées – un boîtier de coin subtil. Autres
*Les écueils de débordement *Le multipliage `x` par `2` pourrait déborder un int 32-bit, donc nous utilisons `long / long`. En Java le casting à "long" est essentiel. Autres

**Traitements clés de l'entrevue**

1. **Toujours chercher une réduction** – transformer deux inégalités en une seule gamme est un tour commun LeetCode.
2. **La recherche binaire sur un tableau trié** vous donne un *compte* dans le temps logarithmique – un outil puissant pour les requêtes de gamme.
3. ** Méfiez-vous du dépassement** – lorsque vous multipliez jusqu'à `1e9`, utilisez des types 64 bits.

---

## TL;DR pour votre CV / Interview

J'ai résolu LeetCode 3649 en Java/Python/C++ avec un algorithme `O(n log n)` qui transforme le problème en une simple requête de portée sur les valeurs absolues triées, en tirant parti de la recherche binaire pour un comptage efficace.

- Mention `ceil((x+1)/2)` et `2*x` comme limites critiques.
- Mettre en évidence la recherche binaire (`lower_bound` / `upper_bound` / `bisect_left` / `bisect_right`).
- Souligner la complexité *temps* et *espace*

---

Tu veux t'entraîner plus ?

Lien vers le code complet (GitHub Gist)
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
Java <https://gist.github.com/votrenom d'utilisateur/abc123> Autres
Python <https://gist.github.com/votrenom d'utilisateur/def456> Autres
C++=https://gist.github.com/votrenom d'utilisateur/ghi789> Autres

N'hésitez pas à cloner, à lancer des tests et à modifier la solution de votre style.

Joyeux codage et bonne chance pour briser cette interview de LeetCode! C'est ce qu'il a dit.

---

> **Mots clés** – LeetCode Nombre de paires parfaites, LeetCode 3649, algorithme de paires parfaites, solution de recherche binaire Java, solution de bisect Python, solution C++ lower_bound, complexité temporelle, prép d'entrevue.