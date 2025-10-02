---
titre: LeetCode 3430. Sommes maximales et minimales de la plupart des subarrays de taille K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (Code de débit 3430)

> **Sommes maximales et minimales de la plupart des sous-barrages K**
> `public long minMaxSubarraySum(int[] nums, int k) "

Compte tenu d'un nombre entier (en nombres ≤ 80 000) et d'un nombre entier positif (en k ≤ 80 000), retour

«» "
[ max(subarray) + min(subarray)]
«» "

Toutes les subdivisions de longueur `1 ... k` sont considérées.
La réponse peut être très grande, donc elle est retournée en entier signé 64 bits.

---

- Oui. 2. Pourquoi ce problème est un aimant Job-Interview

* ** Pression de complexité du temps** – O(n log n) ou O(n) est nécessaire pour les éléments de 80 k.
* **Maîtrise des structures de données** – empilements monotoniques, préfixes et maths à la pièce.
* **Perspective mathématique** – Compter les sous-arrachages qui contiennent un élément particulier comme le maximum ou le minimum tout en respectant un bouchon de longueur.

Montrer un propre La solution O(n) est un moyen sûr d'impressionner les gestionnaires d'embauche sur des plateformes comme LeetCode, Rentred ou un entretien technique.

---

- Oui. 3. Aperçu de la solution de haut niveau

1. ** Comptabiliser la contribution de chaque élément comme un maximum. **
Pour chaque indice `i` nous trouvons:
* `LMax[i]` – combien d'éléments à gauche nous pouvons étendre tout en gardant `nums[i]` le *strictement* le plus grand.
* `RMax[i]` – combien d'éléments vers la droite nous pouvons étendre tout en gardant "nums[i]` le *plus grand-que- ou égal* (c.-à-d. pas plus petit).

2. **Tenir compte au minimum de la contribution de chaque élément. **
Les tableaux analogiques `LMin[i]` et `RMin[i]` sont construits avec des comparaisons opposées.

3. **Pour chaque élément, calculez le nombre de sous-réseaux de longueur ≤ k qui le contiennent en max/min.**
Le sous-barrage doit choisir une distance de gauche `x [0, L-1]` et une distance de droite `y -] [0, R-1]` avec
«x + y + 1 ≤ k».
Le nombre de paires valides `(x, y)` est la valeur retournée par la fonction helper `count(L, R, k)`.

4. **Remplir le total**:
`réponse += nombres[i] * (compte(LMax[i], RMax[i], k) + nombre(LMIN[i], RMIN[i], k))`.

Les quatre scans directionnels sont effectués avec une seule pile monotonique, donnant **O(n)** temps et **O(n)** mémoire supplémentaire.

---

- Oui. 4. La formule de comptage par pièce

Le sous-problème de base: **Combien de paires (x, y) satisfont* *
`0 ≤ x < L`, `0 ≤ y < R` et `x + y + 1 ≤ k`?

Laissez

«» "
Xmax = min(L-1, k-1) // la plus grande distance gauche possible qui peut encore s ' adapter
«» "

Pour tout `x` dans `[0, Xmax]` le côté droit peut être au plus `min(R, k - x)`.

Définir

«» "
a = min (Xmax, k - R) // limite où k - x > R (côté droit saturé)
«» "

*Si ≥ 0*:
Tous `x = 0 ... a` contribuent `R` subarrays (côté droit jamais limité).
Sum1 = (a + 1) * R.

* Rester `x = a + 1 ... Xmax'*:
Ici, le côté droit est limité par la longueur, contribuant `k - x`.
Sum2 = K (k - x) = K * (Xmax - a) - Kx.
* (Xmax - a) / 2.

Le nombre total est `Sum1 + Sum2`.
Tous les arithmétiques correspondent à des entiers signés 64 bits parce que «L, R ≤ 80 000» et «k ≤ 80 000».

---

- Oui. 5. Mise en œuvre intégrale

Voici des solutions propres et bien commentées dans **Java, Python et C++**.
Les trois utilisent la même idée de comptage monotonique + pièce.

### 5.1 Java (style LeetCode)

"Java
Importer java.util. - ArrayDeque;
Importer java.util. Deque;

solution de classe {
public long minMaxSubarraySum(int[] nums, int k) {
int n = longueur nums;
longue[] LMax = nouveau long[n];
longue[] RMax = nouveau long[n];
longue[] LMin = nouveau long[n];
longue[] RMin = nouveau long[n];

// ----- max gauche (diminution stricte) -----
Deque<Integer> st = nouveau ArrayDeque<>();
pour (int i = 0; i < n; ++i) {
pendant que (!st.isEmpty() && nums[st.peek()] <= nums[i]) st.pop();
LMax[i] = st.isEmpty() ? i + 1 : i - st.peek();
le point i) est remplacé par le texte suivant:
}

// ----- max à droite (sans augmentation) -----
clear();
pour (int i = n - 1; i >= 0; --i) {
pendant que (!st.isEmpty() && nums[st.peek()] < nums[i]) st.pop();
RMax[i] = st.isEmpty() ? n - i : st.peek() - i;
le point i) est remplacé par le texte suivant:
}

// ----- min à gauche (augmentation stricte) -----
clear();
pour (int i = 0; i < n; ++i) {
pendant que (!st.isEmpty() && nums[st.peek()] >= nums[i]) st.pop();
LMin[i] = st.isEmpty() ? i + 1 : i - st.peek();
le point i) est remplacé par le texte suivant:
}

// ----- min à droite (sans diminution) -----
clear();
pour (int i = n - 1; i >= 0; --i) {
pendant que (!st.isEmpty() && nums[st.peek()] > nums[i]) st.pop();
RMin[i] = st.isEmpty() ? n - i : st.peek() - i;
le point i) est remplacé par le texte suivant:
}

long ans = 0;
pour (int i = 0; i < n; ++i) {
longue cntMax = nombre(LMax[i], RMax[i], k);
longue cntMin = nombre(LMIN[i], RMIN[i], k);
cntMax + cntMin;
}
le retour des an;
}

/** combien de subarrays de longueur <= k contiennent des nombres[i] comme max/min */
compte long privé(long L, long R, int k) {
long Xmax = Math.min (L - 1, k - 1);
si (Xmax < 0) retour 0; // pas de subarray possible

long a = Math.min (Xmax, k - R);
long res = 0;

si (a >= 0) { // côté droit saturé
Rés += (a + 1) * R;
}

longue gauche = a + 1; // autres distances gauche
longue droite = Xmax;
si (gauche <= droite) {
longue len = droite - gauche + 1;
long sumX = (gauche + droite) * len / 2; //
res += k * len - sumX; //
}
retour rés;
}
}
«» "

#### 5.2 Python 3 (Code Leet)

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def minMaxSubarraySum(self, nombres: List[int], k: int) -> Int:
n = len(nums)
Lmax = [0] * n
RMax = [0] * n
LMin = [0] * n
RMin = [0] * n

# max gauche (diminution stricte)
m = deque()
pour i, val dans l'énumération(nombres):
pendant que m et nombres[st[-1]] <= valeur:
()
LMax[i] = i + 1 sinon m i - m[-1]
Annexe(i)

# max à droite (sans augmentation)
st.clear()
pour i dans la fourchette(n - 1, -1, -1):
pendant que m et nums[st[-1]] < nums[i]:
()
RMax[i] = n - i sinon st[-1] - i
Annexe(i)

# min à gauche (augmentation stricte)
st.clear()
pour i, val dans l'énumération(nombres):
alors que m et nums[st[-1]] >= Valeur
()
Lmin[i] = i + 1 sinon m i - m[-1]
Annexe(i)

# min à droite (non-diminution)
st.clear()
pour i dans la fourchette(n - 1, -1, -1):
pendant que m et nums[st[-1]] > nums[i]:
()
RMIN[i] = n - i sinon st[-1] - i
Annexe(i)

def cnt(L: int, R: int, k: int) -> Int:
Xmax = min(L - 1, k - 1)
Si Xmax < 0:
retour 0
a = min (Xmax, k - R)
Res = 0
si a >= 0:
Res += (a + 1) * R
gauche = a + 1
droite = Xmax
si gauche <= droite:
len_ = droite - gauche + 1
sum_x = (gauche + droite) * len_ // 2
res += k * len_ - sum_x
retour res

ans = 0
pour i dans la plage(n):
(cnt(LMax[i], RMax[i], k) + cnt(Lmin[i], RMin[i], k))

retour et
«» "

#### 5.3 C++ (GNU ++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue minMaxSubarraySum(vecteur<int>& nums, int k) {
int n = nombres.size();
vecteur <long long> LMax(n), RMax(n), LMin(n), RMin(n);

// max gauche : pile en baisse stricte
deque<int> st;
pour (int i = 0; i < n; ++i) {
pendant que (!st.vide() && nums[st.back()] <= nums[i]) st.pop_back();
LMax[i] = m.vide() ? i + 1 : i - st.back();
st.push_back(i);
}

// max à droite : pile non croissante
clear();
pour (int i = n - 1; i >= 0; --i) {
pendant que (!st.vide() && nums[st.back()] < nums[i]) st.pop_back();
RMax[i] = st.vide() ? n - i : st.back() - i;
st.push_back(i);
}

// min à gauche : cheminée en augmentation stricte
clear();
pour (int i = 0; i < n; ++i) {
pendant que (!st.vide() && nums[st.back()] >= nums[i]) st.pop_back();
LMin[i] = m.vide() ? i + 1 : i - st.back();
st.push_back(i);
}

// min à droite : pile non décroissante
clear();
pour (int i = n - 1; i >= 0; --i) {
pendant que (!st.vide() && nums[st.back()] > nums[i]) st.pop_back();
RMIN[i] = st.vide() ? n - i : st.back() - i;
st.push_back(i);
}

nombre automatique = [&](long long L, long R, int k) -> long {
long Xmax = min(L - 1, (long)k - 1);
si (Xmax < 0) retourne 0;
long a = min(Xmax, long)k - R;
longue rés = 0;
si (a >= 0) {
res += (a + 1) * R; // côté droit saturé
}
longue gauche = a + 1;
longue droite = Xmax;
si (gauche <= droite) {
longue len longue = droite - gauche + 1;
longue somme longue = (gauche + droite) * len / 2;
res += (long)k * len - sumx;
}
retour rés;
};

long an = 0;
pour (int i = 0; i < n; ++i) {
ans += (long)nums[i] *
(compte(LMax[i], RMax[i], k) + compte(LMIN[i], RMIN[i], k));
}
le retour des an;
}
};
«» "

Les trois solutions fonctionnent dans le temps **O(n)**, utilisent la mémoire auxiliaire **O(n)** et sont entièrement compatibles avec les interfaces de soumission LeetCode Java/Python/C++.

---

- Oui. 6. Pièges communs et comment les éviter

Pourquoi ça arrive ?
- Oui.
Autres **L'utilisation d'une pile non décroissante pour les deux directions**.Les limites de gauche et de droite exigent des règles de comparaison *différentes* (`=" vs `<`). Les mélanger modifie les valeurs `L`/`R` et conduit à une surestimation. *Two* passes distinctes pour max et min, et utiliser la comparaison correcte (`<=` pour max gauche, `<` pour max droit, etc.). Autres
Même avec la taille du tableau `O(n)`, une boucle intérieure sur `L` deviendrait O(n2). Utiliser la formule par pièce dérivée ci-dessus – seulement une poignée d'opérations arithmétiques par élément. Autres
**Overflow of 32-bit integers**= La somme des subarrays peut dépasser `2^31‐1`.= Utiliser `long` (Java), `int64_t` (C++) ou Python=s arbitraire-precision integers. Autres
La condition est `x + y + 1 ≤ k`, pas `x + y ≤ k`. Autres

---

- Oui. 7. Analyse de la complexité

Étapes Temps Espace supplémentaire
C'est pas vrai.
Autres Quatre scans monotoniques de la pile **O(n)**
Compter avec "count()" par élément
**O(n)**
**O(n)**

Avec `n ≤ 80 000`, toutes les solutions s'intègrent confortablement dans les limites strictes de LeetCode.

---

- Oui. 8. A emporter

La clé pour résoudre efficacement le "Sum of Subarray Ranges" (LeetCode 2104) repose sur deux idées :

1. **Précalculer** la portée maximale gauche/droite de chaque élément comme sous-aire *maximum* et *minimum* à l'aide de deux passes monotoniques.
2. **Count** les sous-réseaux admissibles à l'aide d'une formule arithmétique **forme fermée** («compte()») qui élimine le besoin de boucles imbriquées.

Une fois ces deux éléments de construction en place, la somme finale est une simple passe linéaire.

---

Récapitulation rapide pour les intervieweurs

- Expliquez la nécessité d'établir des comparaisons *différentes* de la pile par côté.
- Afficher la formule `count()` dérivée et mettre l ' accent sur sa nature `O(1)`.
- Mentionnez que la réponse finale est la somme de "nums[i] * (cntMax + cntMin)".

Cette approche démontre la maîtrise des piles monotoniques, le raisonnement préfixe/suffixe et l'arithmétique soignée – compétences très appréciées dans les entrevues de codage.

---

- Oui. 8. TL;DR

- **Problème**: Somme de "max(subarray) - min(subarray)" sur tous les sous-arrachages de longueur `= k`.
- **Solution**: Quatre passes monotoniques pour calculer les limites `L`/`R` pour max et min, puis utiliser une formule compacte pour compter les sous-arrays éligibles par élément.
- **Heure**: "O(n)", **Espace**: "O(n)".
- **Langues**: solutions pleinement opérationnelles en **Java**, **Python** et **C++**.

Bon codage ! C'est ce qu'il a dit.

---

*Si vous avez trouvé ce guide utile, envisagez de le mettre en vedette sur GitHub et de le partager avec des amis se préparant pour le **-Sum of Subarray Ranges (LeetCode 2104)** interview question! *