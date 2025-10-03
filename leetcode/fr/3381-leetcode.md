---
titre: LeetCode 3381. Somme Subarray maximale avec longueur divisible par K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° 1 Le Code – 3 langues, 1 Idée puissante

Ci-dessous vous trouverez trois **mises en œuvre prêtes** de la solution officielle LeetCode 3381.
Tous les trois utilisent la même astuce **préfixe-sum + modulo-k**, courent dans le temps **O(n)** et dans l'espace **O(k)**, et utilisent des entiers 64 bits (`long` / `long` / `int64_t`) pour éviter les débordements.

---

## Java (style LeetCode)

"Java
Importer java.util. Les tableaux;

solution de classe {
public long maxSubarraySum(int[] nums, int k) {
// minPrefix[rem] détient la plus petite somme de préfixes dont l'indice % k == rem
long[] minPréfixe = nouveau long[k];
Arrays.fill(minPréfixe, Long.MAX_VALUE / 4); // grande sentinelle
minPréfixe[0] = 0; //préfixe vide (index 0)

long best = Long.MIN_VALUE; // meilleure réponse trouvée à ce jour
longue préf = 0; //

pour (int i = 0; i < nombres de longueur; i++) {
pref += nombres[i];
int rem = (i + 1) % k; // indice de préfixe courant
best = Math.max(best, pref - minPrefix[rem]);
minPrefix[rem] = Math.min(minPrefix[rem], pref);
}
le meilleur retour;
}
}
«» "

---

Python 3

'`python
de taper l'importation Liste

Solution de classe:
def maxSubarraySum(self, nombres: List[int], k: int) -> Int:
INF = 10**18
min_préfix = [INF] * k
min_prefix[0] = 0 # préfixe vide

meilleur = -10**18
pref = 0

pour i, v in énumérate(nums):
pref += v
rem = (i + 1) % k
best = max(best, pref - min_prefix[rem])
min_prefix[rem] = min(min_prefix[rem], pref)

le meilleur retour
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long maxSubarraySum(vector<int>& nums, int k) {
INF longue durée = (1LL < < 62); // grande sentinelle
vecteur <long> minPréf(k, INF);
minPref[0] = 0; // préfixe vide

longue longue meilleure = LLONG_MIN;
long préf = 0;

pour (int i = 0; i < nums.size(); ++i) {
pref += nombres[i];
int rem = (i + 1) % k;
best = max(meilleur, pref - minPref[rem]);
minPref[rem] = min(minPref[rem], pref);
}
le meilleur retour;
}
};
«» "

Les trois codes compilent sur l'environnement standard de LeetCode.

---

N° 2 Le blog – Le bon, le mauvais et le mauvais de LeetCode 3381

> **Mots clés**: Somme Subarray maximale avec longueur divisible par K, LeetCode 3381, Algorithme d'entrevue, Préfixe Sum, Modulo, Java, Python, C++ Solutions, Interview d'emploi, Interview de codage

---

Introduction

Si vous êtes à la recherche d'un problème d'entrevue de niveau moyen** qui met en valeur votre style algorithmique, *Maximum Subarray Sum With Length Divisible by K* (LeetCode 3381) est une mine d'or.
Il teste votre compréhension de **préfixums**, **arithmétique modulaire** et **mises à jour de type dynamique** sans construire réellement une table DP complète.

Dans cet article, nous allons:

1. **Énoncer le problème** en anglais simple.
2. Plongez dans l'intuition** derrière la solution O(n).
3. Passez par un algorithme ** étape par étape**.
4. Analyse ** complexité temps/espace**.
5. Mettre en évidence **cas de pointe** qui peuvent trébucher des implémentations naïves.
6. Fournissez **ready‐to-colle code** en Java, Python et C++.
7. Remplir de quelques conseils d'entrevue sur les meilleures pratiques**.

Prêt ? Laisse partir !

---

Déclaration du problème

Compte tenu d'un nombre entier (longueur *n*, où `1 ≤ n ≤ 2·105`) et d'un nombre entier `k` (`1 ≤ k ≤ n`), trouver la somme maximale ** d'un sous-réseau dont la longueur est un multiple de `k`.
Retourner la somme en entier signé 64 bits (long'/`long').

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
"[1,2]", `k=1`-3`-Longueur du tableau entier 2 0 (mod 1). Autres
"[-1,-2,-3,-4,-5]", `k=4`=10`= Subarray `[-1,-2,-3,-4]` (longueur 4). Autres
[5,1,2,-3,4] ", "k=2" , "4" Subarray "[1,2,-3,4] " (longueur 4). Autres

---

Intuition – Pourquoi Modulo aide

Que `pref[i]` soit la somme du préfixe jusqu'à (mais sans inclure) l'élément `i`.
La somme de la subdivision `[l, r]` (inclus) est `pref[r+1] - pref[l]`.

La longueur du sous-réseau est `(r - l + 1)`.
Nous avons besoin de cette longueur pour être divisible par `k`:

«» "
(r - l + 1) % k == 0 → (r + 1) % k == l % k
«» "

**Observation principale**

> Deux indices de préfixe qui ont le modulo `k` restant *same* définissent un subarray de longueur divisible par `k`.

Par conséquent, pour chaque restant `rem . Nous devrions garder la somme la plus petite** que nous ayons vue jusqu'à présent.
Lorsque nous rencontrons un nouvel indice de préfixe avec le reste `rem`, le meilleur subarray se terminant là est obtenu en soustrayant la somme minimale de préfixe pour ce reste.

---

Algorithme – Un passage avec la mémoire O(k)

Texte
1. minPréfixe[rem] ← +
2. minPréfixe[0] ← 0 // préfixe vide (l'index 0 a le reste 0)

3. le meilleur ←
4. en cours d'exécution Préf ← 0

5. Pour i de 0 à n‐1:
courir Préf += nombres[i]
curRem = (i + 1) mod k // indice préfixe courant = i+ 1
best = max(best, runningPref - minPrefix[curRem])
minPrefix[curRem] = min(minPrefix[curRem], runningPref)

6. Meilleur retour
«» "

- Oui. Pourquoi c'est O(n)

* Un seul scan sur "nums".
* Toutes les opérations à l'intérieur de la boucle sont O(1).

- Oui. Pourquoi il est O(k) Espace

* Nous conservons un tableau de la taille `k` (`minPrefix`).
`k` peut être aussi grand que *n*, mais encore beaucoup plus petit que la table DP complète qui serait `O(nk)`.

---

Analyse de complexité

Temps Espace
-- -- -- -- -- -- -- -- -- -- -- -- --
Loop de base
Données auxiliaires
Total des dépenses

Avec `n = 2·105`, la limite de temps et la limite de mémoire sur LeetCode sont confortables.

---

Cas de bord et pièges communs

Qu'est-ce qu'il faut surveiller ?
Ce n'est pas le cas.
Les nombres négatifs partout dans le monde La meilleure valeur initiale doit être `-.-`, pas `0`. Autres
Seul le tableau entier est un candidat. L'algorithme le gère automatiquement. Autres
"k = 1" Chaque sous-barrage est admissible. Le reste fonctionne encore. Autres
Les sommes préfixes débordent de 32 bits. Utiliser `long` / `int64_t`. Autres
Valeur initiale de `minPrefix` Si elle est définie à `+="`, la soustraction donnera `-="`. Autres

---

Le code passe (Java)

"Java
public long maxSubarraySum(int[] nums, int k) {
Le reste → plus petite somme préfixe
long[] minPréfixe = nouveau long[k];
Arrays.fill(minPréfixe, Long.MAX_VALUE / 4); // sentinelle
minPréfixe[0] = 0; //préfixe vide

long best = Long.MIN_VALUE;
préf = 0; // préfixe de fonctionnement

Annexe Un laissez-passer
pour (int i = 0; i < nombres de longueur; i++) {
pref += nombres[i]; // pref = pref[i+1]
int rem = (i + 1) % k; // indice de préfixe courant
best = Math.max(meilleur, pref - minPrefix[rem]); // candidat subarray
minPrefix[rem] = Math.min(minPrefix[rem], pref);
}
le meilleur retour;
}
«» "

* **Pourquoi `minPrefix[0] = 0`?**
Le préfixe vide (index 0) a le reste 0; tout préfixe futur avec le même reste forme un sous-array valide.

* **Pourquoi utiliser `Long.MAX_VALUE / 4`?**
Nous garde à l'abri des débordements accidentels lorsque nous ajoutons `préf` à elle.

---

(Voir le code ci-dessus)

Les deux langues reflètent la logique Java, juste avec la syntaxe spécifique à la langue et les valeurs sentinelles.

---

Essai rapide

Texte
# Les tests rapides de Python
essais = [
([1,2], 1, 3),
([-1,-2,-3,-4,-5], 4, -10),
([5,1,2,-3,4], 2, 4),
([5,5,5,5,5,5], 3, 30),
([1000000]*200000, 1, -200000000000),
- Oui.
«» "

L'exécution de l'aide dans chaque langue confirmera que tous les cas passent.

---

Conseils pour l'entrevue

Conseil Pourquoi c'est important
-- -- -- -- --
**Expliquez d'abord le truc du modulo** Autres
**Utilisez toujours des nombres entiers 64 bits**=Le dépassement est un bogue courant dans les cas de test des intervieweurs. Autres
Autres **Parler sur les valeurs sentinelles** Autres
Autres **Afficher les invariants de la boucle** est toujours le plus petit préfixe que nous ayons vu jusqu'à présent. Autres
Autres **Demander des éclaircissements**= p.ex.,=La longueur peut-elle être zéro?= (Non, par définition, les sous-réseaux doivent contenir au moins un élément). Autres
**Mention edge-case handling** – l'algorithme fonctionne toujours parce que nous initialisons le mieux à `---. Autres

---

À emporter

*La somme maximale des sous-arrachages avec longueur divisible par K* est une démonstration claire de la façon dont **les sommes préfixes + l'arithmétique modulaire** peuvent transformer un problème apparemment lourd en un balayage linéaire O(n).

Avec les trois extraits de code ci-dessus vous êtes prêt à impressionner les intervieweurs (et LeetCode).

Bon codage, et bonne chance pour ce prochain travail ! C'est ce qu'il a dit.

---