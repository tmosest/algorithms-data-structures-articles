---
titre: LeetCode 3299. Somme des séquences consécutives -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Récapitulation des problèmes – Somme des séquences consécutives (Code Leet 3299)

Compte tenu d'un tableau entier `nums` (1 ≤ `nums[i]` ≤ 105, 1 ≤ `nums.longueur` ≤ 105), une subséquence **consécutive** est une subséquence non vide dont les éléments forment une progression arithmétique qui augmente ou diminue strictement avec la différence ±1.
La *valeur* d'une subséquence est la somme de ses éléments.

**Objectif** – retourner la somme des valeurs de **all** consécutifs non vides subséquences modulo 109+7.

> **Exemple**
> `nums = [1, 4, 2, 3]`
> Sous-séquences consécutives:
> `[1]`, `[4]`, `[2]`, `[3]`, `[1,2]`, `[2,3]`, `[4,3]`, `[1,2]``
> Somme des valeurs = 31

---

Aperçu de la solution

Le dénombrement naïf d'O(2n) est impossible.
Observer :

* Une séquence consécutive peut être divisée en une course croissante et une course décroissante.
* Si nous traitons le tableau **forward** nous pouvons calculer, pour chaque valeur `v`,
*`cntInc[v]`* – combien de subséquences croissantes finissent avec la valeur `v "
*`sumInc[v]`* – la valeur totale de ces subséquences
* De même, un **backward** passe donne les parties décroissantes.

Avec ces deux passes nous pouvons combiner les comptes et les sommes pour obtenir la réponse finale en **O(n + maxValue)** temps et **O(maxValue)** mémoire (maxValue ≤ 105).

- Oui. Pourquoi ça marche ?

Pour une valeur fixe `x` qui apparaît à la position `i`:

1. **Augmentation du côté** – toute subséquence se terminant à «x» doit avoir été étendue d'une subséquence se terminant à «x‐1» immédiatement avant «i».
*Nouveau nombre* = `cntInc[x‐1] + 1` (`+1` pour la sous-séquence consistant uniquement en `x`).
*Nouvelle somme* = "sumInc[x‐1] + x * (cntInc[x‐1] + 1)".

2. **Côté décroissant** – symétrique, utilisant `x+1` comme valeur précédente.

La contribution totale de tous les sous-séquences se terminant à "x" est la somme des deux côtés, moins la sous-séquence à élément unique comptée en double (traitée naturellement par les équations DP).

Le même DP travaille sur le passage arrière pour la direction décroissante. Enfin, pour chaque valeur `v` nous ajoutons les sommes des deux passes et soustrayez la sous-séquence d'élément unique surcomptabilisée.

Toutes les opérations sont effectuées modulo **M = 1 000 000 007**.

---

Mise en œuvre du code

- Oui. 1. Java (O(n) DP sur les valeurs)

"Java
Importer java.util. HashMap;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

public int sumOfConsecutiveSubséquences(int[] nums) {
= 0;
pour (int v : nombres) maxVal = Math.max(maxVal, v);

long[] cntInc = nouveau long[maxVal + 2];
long[] sumInc = nouveau long[maxVal + 2];
long[] cntDec = nouveau long[maxVal + 3];
long[] sumDec = nouveau long[maxVal + 3];

// Passage vers l'avant – direction croissante
pour (int v : nombres) {
long c = cntInc[v - 1] + 1;
long s = somme Inc[v - 1] + v * c;
cntInc[v] = (cntInc[v] + c) % MOD;
sumInc[v] = (sumInc[v] + s) % MOD;
}

// Passage en arrière – direction décroissante
pour (int i = longueur nominale - 1; i >= 0; --i) {
int v = nombres[i];
long c = cntDec[v + 1] + 1;
long s = sommeDec[v + 1] + v * c;
cntDec[v] = (cntDec[v] + c) % MOD;
sumDec[v] = (sumDec[v] + s) % MOD;
}

long ans = 0;
pour (int v = 1; v <= maxVal; ++v) {
as = (ans + sumInc[v] + sumDec[v]) % MOD;
// soustraire la subséquence d'un seul élément doublement compté
as = (ans - v + MOD) % MOD;
}
retour (int) ans;
}
}
«» "

**Complexités* *

* Temps: `O(n + maxValeur)` (= O(n) dans la pratique)
* Mémoire: `O(maxValue)` (=4 × 105 longs → < 3 Mo)

---

- Oui. 2. Python (O(n) DP avec dictionnaires)

'`python
MOD = 1 000 000 007

def sum_of_consecutive_subsequences(nums) :
max_val = max(nums)
cnt_inc = [0] * (max_val + 2)
sum_inc = [0] * (max_val + 2)
cnt_dec = [0] * (max_val + 3)
sum_dec = [0] * (max_val + 3)

# Passer vers l'avant
pour v en chiffres:
c = cnt_inc[v - 1] + 1
s = (sum_inc[v - 1] + v * c) % MOD
cnt_inc[v] = (cnt_inc[v] + c) % MOD
sum_inc[v] = (sum_inc[v] + s) % MOD

Passage en arrière
pour v en sens inverse(nombres):
c = cnt_dec[v + 1] + 1
s = (somme_dec[v + 1] + v * c) % MOD
cnt_dec[v] = (cnt_dec[v] + c) % MOD
sum_dec[v] = (sum_dec[v] + s) % MOD

ans = 0
pour v dans la plage(1, max_val + 1):
ans = (ans + sum_inc[v] + sum_dec[v]) % MOD
ans = (ans - v + MOD) % MOD # supprimer le double élément compté
retour et
«» "

---

- Oui. 3. C++ (O(n) DP avec vecteur)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

MOD = 1'000'000'007;

int sumOfConsecutiveSubséquences(vecteur<int>& nums) {
int maxVal = *max_element(nums.begin(), nums.end());
vecteur<long> cntInc(max.Val + 2, 0), sumInc(max.Val + 2, 0);
vecteur <long> cntDec(maxVal + 3, 0), sumDec(maxVal + 3, 0);

// Passer vers l'avant
pour (int v : nombres) {
long c = cntInc[v - 1] + 1;
long long s = (sumInc[v - 1] + 1LL * v * c) % MOD;
cntInc[v] = (cntInc[v] + c) % MOD;
sumInc[v] = (sumInc[v] + s) % MOD;
}

// Passage en arrière
pour (int i = nombres.size() - 1; i >= 0; --i) {
int v = nombres[i];
long c = cntDec[v + 1] + 1;
long s = (sommeDec[v + 1] + 1LL * v * c) % MOD;
cntDec[v] = (cntDec[v] + c) % MOD;
sumDec[v] = (sumDec[v] + s) % MOD;
}

long an = 0;
pour (int v = 1; v <= maxVal; ++v) {
as = (ans + sumInc[v] + sumDec[v]) % MOD;
as = (ans - v + MOD) % MOD; // supprimer le double élément compté
}
retourner static_cast<int>(ans);
}
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de résoudre le leetCode 3299

Titre
**Sum of Consecutive Subsequences – The Good, The Bad, and The Ugly (O(n) DP on Values)* *

Description de la méta
Apprenez comment cracker LeetCode 3299 en temps prêt à l'entrevue. Nous traversons le tour DP, les pièges et le code en Java, Python et C++. Obtenez des conseils d'interview que les recruteurs aiment!

- Oui. Pourquoi cela compte
Si vous préparez une entrevue d'ingénierie **logiciel** ou cherchez à présenter vos côtelettes de résolution de problèmes sur votre CV, LeetCode 3299 est un *grand point de discussion*. Il teste :

* ** Aperçu PD** – vous devez voir la valeur ** d'une sous-séquence comme une somme d'un tour de valeurs `±1`.
* **Les compromis entre l'espace et le temps** – gérer 105 valeurs efficacement.
* ** L'arithmétique modulo – un classique pour beaucoup de candidats.

Voici un guide complet qui gardera les intervieweurs impressionnés.

---

- Oui. 1. Le PDD bon – élégant sur l'espace de valeur

* **Heure linéaire** – Une fois que vous pensez en termes de *valeurs* plutôt que de positions, la solution s'effondre à deux passe.
* **Récurrence intuitive** – `cnt[v] = cnt[v-1] + 1` et `sum[v] = sum[v-1] + v * cnt[v]`.
Ils sont simples à dériver et faciles à retenir.
* ** Mémoire basse** – un vecteur de taille `max(nums)+2` est minuscule par rapport à l'entrée.

**Take‐away**: Si vous pouvez réécrire un problème complexe de "subséquence" dans une récurrence sur les valeurs des éléments, vous débloquez souvent une solution linéaire.

---

- Oui. 2. Les mauvaises – pièges communs qui rompent votre code

Pourquoi ça arrive
- Oui.
**Utiliser `int` pour les sommes** (Java `long`, Python `int` est sans limite, C++ `long`) Autres
**Missing modulo** Autres
**Double comptage des éléments simples** Soustraire `x` une fois à la fin
**Indexage hors limites**="cntInc[v-1]` quand `v==1="Afficher la taille `maxVal+2` et partir de `v-1 >= Pas de problème.
**Time-outs on large `maxValue`**= Si vous attribuez un tableau pour 109 valeurs== Capturez la taille à `max(nums)+2` (= 105) ou utilisez `unordered_map`==

---

- Oui. 3. L'horrible – Quand l'idée de la force brute se trompe

Beaucoup de candidats commencent par énumérer tous les sous-séquences, en espérant que la taille aidera. Même après la taille, le facteur de ramification reste énorme. La partie "gugly" se rend compte que **vous ne pouvez pas itérer sur les sous-séquences** – vous devez itérer sur **valeurs**.
Quand vous avez enfin trouvé le DP, le code semble compact, mais la vraie lutte est de se rappeler les termes *plus‐1* pour la nouvelle séquence mono-élément et de gérer correctement la direction décroissante.

---

Récapitulation de la complexité (mots clés du référencement)

Langue Heure Espace
- C'est quoi ?
Java O(n)
Python O(n)
C++= O(n)= O(105)=

*=O(n) DP sur les valeurs* et *=modulo 109+=7* sont les termes que les recruteurs demandent souvent dans les entrevues de codage.

---

Conseils d'entrevue

1. **Passer la récurrence** sur un tableau blanc. Dessinez un petit exemple, écrivez `cntInc[v]`, `sumInc[v]` sur le tableau, et montrez comment ils sont mis à jour.
2. ** Expliquer les deux passes** : vers l'avant pour augmenter, vers l'arrière pour diminuer. Cela démontre que vous pouvez penser à la symétrie.
3. **Mentionnez le tour du modulo**: Toutes les opérations sont faites mod M, nous devons donc ajouter `M` avant de prendre `% M` pour éviter les négatifs. (en milliers de dollars)
4. **Afficher votre code** – mettre en évidence les deux boucles. Les intervieweurs aiment le code propre et autocommenté.
5. **Parler de cas de bord** – tableaux d'éléments uniques, tous les éléments égaux, motifs alternants. Cela indique une compréhension profonde.

---

Comment utiliser cet article dans votre recherche d'emploi

* **SEO Mots-clefs** – Sum of Consecutive Subsequences, -LeetCode 3299 solution, -LeetCode sur les valeurs, -Java DP interview, -Python coding interview, -C++ Solutions LeetCode, -software ingénierie interview conseils.
* **Hook de médias sociaux** – LeetCode Cracked 3299 en O(n) – voici le tour qui a fait des recruteurs un signe de tête!
* **Call‐to‐Action** – Invitez les lecteurs à déposer un commentaire avec leurs propres solutions ou à demander une session de programmation paire.

---

La pensée finale

Le *Good* est le DP propre qui fonctionne dans le temps linéaire.
Le *Bad* est la tentation de forcer ou de surestimer la définition de subséquence.
Le *Ugly* est le subtil maniement off-by-one et modulo qui voyage même les ingénieurs chevronnés.

La maîtrise de ce problème montre que vous pouvez **abstraire un problème apparemment combinatoire dans une simple récurrence** – un recruteur de compétences cherche dans chaque ingénieur logiciel senior. C'est ce qu'il a dit.

---

Bon codage, et bonne chance pour votre prochaine interview!