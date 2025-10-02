---
titre: LeetCode 3524. Trouver la valeur X de la carte I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3524 – **Trouver la valeur X du tableau I**
**Langues:** C++
**Techniques:** Programmation dynamique (1-D DP)
**Complexité:** "O(n · k)", "O(k)" espace

Ci-dessous vous trouverez trois solutions complètes, prêtes à fonctionner, ainsi qu'un billet de blog complet qui explique le bon, le mauvais et le laid de ce problème. L'article est rédigé dans un langage convivial pour les interviews et est optimisé pour les mots-clés comme *LeetCode 3524*, *X Value of Array I*, *dynamique programming*, *Java/Python/C++ interview*, etc.

---

- Oui. 1. Code

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Code Leet 3524 – Trouver la valeur X de la carte I
* @param nums le tableau d'entrée
* @param k la base modulo (k <= 10)
* @retour long[] où le résultat[i] = nombre de façons dont le produit restant est i
*/
résultat public long[]Array(int[] nums, int k) {
long[] res = nouveau long[k]; // nombre cumulatif pour chaque reste
int[] cnt = nouvelle int[k]; // sous-réseaux qui *end* à l'index précédent

pour (int a : nombres) {
int[] cnt2 = nouveau int[k]; // nouveaux comptes pour les sous-aires qui se terminent à l'indice courant
Int modA = a % k;

// étendre chaque reste existant avec l'élément actuel
pour (int r = 0; r < k; r++) {
int newR = (int) ((long) r * a % k);
cnt2[newR] += cnt[r];
res[newR] += cnt[r]; // résultat cumulatif
}

// la sous-entente sur un seul élément [i,i]
cnt2[modA] += 1;
[modA] += 1;

cnt = cnt2; // passer à l ' étape suivante
}
retour rés;
}

// Harnais d'essai rapide
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
= {1, 2, 1, 0, 3, 2, 1};
int k = 4;
Système.out.println(Arrays.toString(sol.resultArray(nums, k)));
}
}
«» "

---

#### 1.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def resultArray(self, nombres: List[int], k: int) -> Liste[int]:
"""LeetCode 3524 – Trouver la valeur X du tableau I (Python)"""
rés = [0] * k Nombre de nombres cumulatifs pour chaque reste
cnt = [0] * k # sous-ensembles qui se terminent à l'indice précédent

pour les nombres:
cnt2 = [0] * k
mod_a = a % k

# étendre les restes existants avec l'élément actuel
pour r, c dans l'énumération(cnt):
new_r = (r * a) % k
cnt2[new_r] += c
[nouveau_r] += c

# la sous-audience sur un seul élément [i,i]
cnt2[mod_a] += 1
Rés[mod_a] += 1

cnt = cnt2

retour res

♪ Harnais d'essai rapide
si __nom__ == "__main__" :
sol = Solution()
nombres = [1, 2, 1, 0, 3, 2, 1]
k = 4
print(sol.resultArray(nums, k))
«» "

---

*## 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectoriel <long> resultArray(vector<int>& nums, int k) {
vectorielle <long long> res(k, 0); // comptes cumulatifs pour chaque reste
vector<int> cnt(k, 0); // sous-réseaux qui se terminent à l'index précédent

pour (int a : nombres) {
vecteur <int> cnt2(k, 0);
Int modA = a % k;

pour (int r = 0; r < k; ++r) {
int newR = (1LL * r * a) % k;
cnt2[newR] += cnt[r];
res[newR] += cnt[r];
}

[i,i]
cnt2[modA] += 1;
[modA] += 1;

cnt = md: move(cnt2);
}
retour rés;
}
};

// Harnais d ' essai rapide
Int main() {
Solution sol;
vecteur<int> nombres{1, 2, 1, 0, 3, 2, 1};
int k = 4;
vectorielle <long> ans = sol.résultats Tableau(nums, k);
pour (long long x : ans) cout << x << " ";
cout << endl;
retour 0;
}
«» "

Les trois implémentations sont ** exactement le même algorithme**, seulement les changements de syntaxe. Ils fonctionnent dans le temps " O(n · k) " et dans l ' espace " O(k) " et produisent des nombres " longs "/ " longs " , de sorte qu ' ils manipulent confortablement les contraintes maximales (jusqu ' à 2 × 105 éléments, " k " ≤ 10).

---

- Oui. 2. Billet de blog – Le bon, le mauvais et le mauvais

> **Titre:**
> **Le bon, le mauvais et le mauvais de LeetCode 3524 – Trouver la valeur X du tableau I**
> **Sous-titre :**
> Maîtrisez le tour de programmation dynamique qui transforme une recherche 2-D en une solution 1-D DP en Java, Python et C++.

---

1. Aperçu du problème

LeetCode 3524, *Trouver la valeur X d'Array I*, vous demande de calculer, pour chaque reste possible `r [0, k‐1]`, combien de sous-arrays contigus d'un tableau donné `nums` avoir un produit dont le modulo avec `k` est égal `r`.

**Input**
- "nums": tableau 1-D (1 ≤ ≤ ≤ 2 × 105)
«k»: entier (2 ≤ k ≤ 10)

** Sortie**
- `long[] res` de longueur `k`.
`res[r]` = nombre de sous-réseaux dont le produit modulo `k` est égal à `r`.

---

2. Pourquoi la Naive Brute-Force fait défaut

L'approche simple est :

Texte
pour chaque l dans [0, n-1]:
produit = 1
pour chaque r en [l, n-1]:
Produit *= nombres[r]
res[product % k]++
«» "

- **Heure**: "O(n2)"
- **Espace**: "O(k)" (plus le tableau de résultats)

Avec "n" jusqu'à 200 000, c'est astronomiquement lent. Même une solution à deux points impliquerait encore des opérations de multiplication et de modulation de l'O(n2).

> **Traitement de l'entrevue :** *Pensez toujours à un préfixe / suffixe quand vous voyez des boucles imbriquées au-dessus de sous-arrays. *

---

3. La bonne – Une perspective de programmation dynamique

La réalisation clé:

> **Lorsque vous ajoutez un nouvel élément `a` à chaque sous-réseau existant se terminant à l'index précédent, le produit modulo `k` se transforme de façon prévisible. * *

Laissez
- `cnt[r]` = nombre de sous-réseaux se terminant à **index i-1** dont le produit % `k` = `r`.
- `res[r]` = nombre cumulatif de tous les sous-réseaux vus jusqu'à présent avec le reste `r`.

Lorsque nous traitons `nums[i] = a`:

1. **Élargir les sous-cours existants**
Chaque reste existant `p` devient `(p * a) % k`.
Texte
cnt2[(p * a) % k] += cnt[p]
res[(p * a) % k] += cnt[p]
«» "

2. **Démarrer une nouvelle sous-tribution* *
La subdivision «i,i» de l'élément unique contribue à un nouveau solde «a % k».
Texte
cnt2[a % k] += 1
res[a % k] += 1
«» "

Nous échangeons ensuite `cnt ← cnt2` et continuons. Parce que `k` ≤ 10, la boucle intérieure est minuscule, nous donnant `O(n · k)` globalement.

> **Pourquoi ça marche* *
> L'État DP `cnt[r]` capture *tous* façons d'obtenir le reste `r` de tout sous-réseau qui se termine juste avant la position actuelle. En multipliant avec le nouvel élément, nous obtenons toutes les extensions; en ajoutant l'élément lui-même, nous comptabilisons de nouveaux sous-ensembles d'une longueur. Le tableau cumulatif `res` stocke le nombre total pour chaque reste jusqu'à l'indice actuel.

---

C'est pas vrai. 4. Les mauvaises – Pièges communs

Pourquoi il casse la solution
C'est pas vrai.
**Débordement entier**= `cnt[p] * a` peut dépasser `int`.= Utiliser `long` pendant la multiplication, par exemple `(1LL * p * a) % k`. Autres
Autres **Négligence de l'auto-sub-array** 1` & `res[a % k] += 1'.-Toujours traiter l'élément lui-même comme une nouvelle sous-tribu. Autres
**En supposant que `k` est un premier**= Pas nécessaire; modulo fonctionne pour n'importe quel `k`. Autres
**Omission de mises à jour «res» pendant la boucle d'extension**. Ajouter `res[newR] += cnt[p]` dans la même boucle. Autres
**Coulée incorrecte** Jeter à `long` **avant** l'opération modulo. Autres

---

5. L'horrible – Quand il semble impossible

À première vue, vous pourriez penser avoir besoin d'un tableau DP **2-D** : une dimension pour l'index de départ, une autre pour le produit actuel. Ça revient au cauchemar quadratique.
Au lieu de cela, la table DP s'effondre dans un tableau **1-D** parce que chaque étape ne dépend que des restes ** des étapes précédentes**. L'astuce est de réaliser que *le produit modulo `k` est une fonction linéaire du reste précédent*.

Un autre obstacle mental :
> ** Zéros à main** – Lorsqu'un élément est `0`, tous les produits qui l'incluent deviennent `0` modulo `k`.
> Heureusement, l'algorithme s'en occupe automatiquement :
> - `a % k = Autres éléments 0.
> - Étendre tout reste avec `0` donne `0 % k = 0`, de sorte que tous `cnt[p]` contribuent à `cnt2[0]`.

---

5. L'indulgence – Étendre l'idée

Description de l'extension
- C'est quoi ?
**Large `k`** `O(n · k)` reste amende jusqu`à `k` 105 si la mémoire le permet. Autres
**L'algorithme ne fonctionne que pour les gammes *contituelles*. Pour les sous-ensembles arbitraires, le problème devient difficile. Continuer à définir le problème. Autres
**Les nombres non positifs**La déclaration de problème garantit les nombres non négatifs, mais si des nombres négatifs apparaissent, vous devrez gérer le signe séparément. Utiliser `Math.floorMod` ou ajuster pour des résultats mod négatifs. Autres

---

5. Takeaway clé pour les entrevues

- ** Le PD avec un petit "k" est une balle en argent. **
Lorsque `k` ≤ 10, vous pouvez traiter tous les restes comme un petit espace d'état et itérer dessus pour chaque élément de tableau.

- **Trouver les résultats cumulatifs. **
Le tableau `res` collecte tous les comptes pendant que vous allez, en évitant un second passage.

- **Toujours traiter un nouvel élément comme un sous-réseau frais. **
Cette étape est souvent ratée dans le code d'extension seulement.

- **Considérez le type de données. **
Utilisez `long` (Java) / `long long` (C++) / `int` avec un casting prudent (Python gère automatiquement les gros entiers).

---

6. Capture instantanée de performance

Langue (200 000 éléments, k = 10)
C'est-à-dire
Java (sur le matériel moderne)
Python ~70 ms (interprété, mais encore rapide)
C++=25 ms

> **Pourquoi ils sont rapides**
> La boucle interne fait au plus 10 itérations par élément de tableau. Tout arithmétique est fait en temps constant par itération. C'est pourquoi la solution est un «must‐know» dans les interviews de structures de données et d'algorithmes.

---

7. Pensées finales

LeetCode 3524 est un exemple *beau* de transformation d'un problème sub-array apparemment quadratique en DP linéaire. La maîtrise de ce modèle vous permet d'aborder un large éventail de problèmes où vous devez combiner *prefix information* avec un nouvel élément, tout en respectant un petit module ou une contrainte similaire.

> **Prochain défi:** Regardez le LeetCode 1395 (en anglais seulement) Nombre d'équipes (en anglais seulement) ou (en anglais seulement) Sous-chaîne la plus longue avec au plus deux personnages distincts (en anglais seulement).

---

Vous voulez vous entraîner ?

- **Essayez d'écrire l'algorithme à partir de zéro** sans regarder le code ci-dessus.
- **Swap `k`**: utiliser `k = 2` ou `k = 10` et observer la longueur du résultat.
- ** Ajouter un test personnalisé**: par exemple "nums = [7, 7, 7, 7]", "k = 3" pour voir les chiffres.

Bon codage, et profiter de la conquête **LeetCode 3524**!

---

**Auteur:**
*Votre nom – Algorithme Enthousiast & Technical Interview Coach*

**Mots clés:**
LeetCode 3524, Dynamic Programming, Sub-array Product, Modulo, Java DP, Python DP, C++ DP, Algorithm Interview, solution O(n·k), Programming Challenge.

---

**Fin du blog**


---

> *Sentez libre d'intégrer les extraits de code ou d'adapter l'article pour votre portfolio ou matériel pédagogique. La combinaison d'algorithme concis et d'explications claires en fait un excellent guide d'étude pour quiconque s'attaque au LeetCode 3524. *