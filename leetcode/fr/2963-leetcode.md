---
titre: LeetCode 2963. Nombre de bonnes partitions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# 2963 – **Comparer le nombre de bonnes partitions**
> **Tarif**= Code du leet **Job-Interview-Ready**
> **Langues**: Java-Python-C++

---

TL;DR
> Une *bonne partition* est un moyen de diviser les "nums" en sous-arrays contigus de sorte que ** aucune valeur n'apparaît dans deux parties différentes**.
> Pour chaque tableau, la réponse est
> `` "
(nombre de segments non dissouts) – 1 )
> `` "
> Les segments d'unbreakable sont les gammes maximales où chaque élément *dernier* occurrence se trouve à l'intérieur de la gamme.
> Tout le problème peut être résolu en **O(n)** temps et **O(n)** espace supplémentaire (ou O(1) extra avec un hashmap) – parfait pour une entrevue de codage.

---

Table des matières

Ce que vous apprendrez
- Oui.
Définition exacte et exemples
Pourquoi la réponse est un pouvoir de deux
Algorithme Solution linéaire à deux passages
Pourquoi c'est rapide
Edge‐Cas et pièges Erreurs courantes
Code Java, Python, C++
Mots clés & angle d'entrevue
La suringénierie, pièges à éviter
Le bon code propre et convivial pour l'entrevue
Les mauvais modèles communs

---

- Oui. 1. Remise en état des problèmes

> **Donné** d'un tableau 0 indexé «nums» de ** entiers positifs** (longueur ≤ 105).
> **Définir** une partition comme un ensemble d'un ou de plusieurs sous-réseaux contigus qui couvrent ensemble des «nums».
> **Bonne partition**: aucun sous-réseau ne contient le même entier.
> **Tâche**: Comptez toutes les bonnes partitions possibles de "nums".
> **La réponse** doit être retournée modulo 109 + 7.

**Exemples**

De bonnes partitions Sortie
- C'est quoi ?
8 (voir l'énoncé du problème)
[1,1,1,1]
[1,2,1,3]

---

- Oui. 2. Intuition – segments incassables

1. **Chaque valeur doit rester unie**.
Si une valeur apparaît plus d'une fois, toutes ses occurrences *doivent* appartiennent à la même sous-tribu.

2. **Regardez l'occurrence *dernier* de chaque valeur**.
Pendant le balayage de gauche à droite, maintenez l'indice le plus éloigné de droite que toute valeur vue jusqu'à présent doit rester à l'intérieur.

3. **Lorsque l'indice actuel est égal à celui qui s'éloigne le plus de l'indice droit**, nous avons trouvé un segment « autonome » : toutes les valeurs à l'intérieur ont leur dernière occurrence à l'intérieur du segment.
Ce segment ** ne peut pas être divisé davantage** sans enfreindre la règle.

4. **Entre deux de ces segments, nous avons le choix** : soit les séparer, soit les fusionner.
Chaque limite donne une décision binaire → possibilités totales = 2^(#boundaires).

5. **Nombre de limites** = (# segments incassables) – 1.
La réponse est donc 2^(# segments incassables – 1) modulo 1 000 000 007.

> **Pourquoi c'est correct**:
> * Si nous essayons de diviser dans un segment incassable, au moins une valeur de la dernière occurrence se trouve à l'extérieur → viole la règle.
> * Si nous conservons deux segments incassables consécutifs ensemble, la partie résultante est toujours bonne parce que toutes les valeurs sont toujours à l'intérieur de leur dernière occurrence.
> Ainsi, chaque combinaison de limites de fusion/non fusion donne une bonne partition unique.

---

- Oui. 3. Algorithme – Scan linéaire bipass

1. **First pass** – build a hash map `last` where `last[x]` = index of the *last* occurrence of value `x`.
Complexité: O(n).

2. **Deuxième passe** – balayage à nouveau, en maintenant deux pointeurs:
* `i` – indice actuel.
* `maxRight` – l'index le plus éloigné que tout élément vu à ce jour doit rester à l'intérieur. Au début, 0.

Pour chaque «i»:
* Mettre à jour `maxRight = max(maxRight, last[nums[i]])`.
* Si `i == maxRight`, nous avons terminé un segment incassable → incrément contre `cnt`.

3. **Résultat** = "pow(2, cnt-1, MOD)" (MOD = 1 000 000 007).
Cas de bord : si "cnt". 0` (seulement possible lorsque le tableau est vide, mais les contraintes disent n ≥ 1), retourner 1.

Toutes les opérations sont O(1) par élément → global O(n).

---

- Oui. 4. Analyse de la complexité

Étapes Temps Espace supplémentaire
C'est pas vrai.
Premier pass.
Deuxième laissez-passer
**O(n)**

Avec `n ≤ 105` cela passe facilement sous 50 ms dans les trois langues.

---

- Oui. 5. Cas de bord et pièges communs

Numéro
C'est quoi ?
**Les plus grands entiers** (Java, C++), `int`/`int64` (Python). Autres
**Débordement de Modulo** en multipliant par 2 → utiliser 64-bit intermédiaire (`long` en Java/C++). Autres
**Empty array** → contraintes l'interdisent, mais le code défensif peut retourner 1.
Autres **Module incorrect** (`10**9 + 7`) vs. `1e9 + 7` littéral en C++ → n'oubliez pas de lancer en `int`. Autres
**Utiliser `pow(2, cnt-1)`** directement peut déborder → utiliser une exponentiation modulaire ou le doublement itératif. Autres

---

- Oui. 6. Code

> **Astuce**: Utilisez `fast-exposentiation` ou simple gauche avec modulo quand `cnt` est petit (jusqu'à 105, donc le doublement répété est très bien).
> Les implémentations suivantes sont faciles à interviewer, propres et entièrement testées.

---

### Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

Nombre d'entrées publiquesDeBienPartitions(int[] nombres) {
int n = longueur nums;
// 1er passage : dernier événement
Carte<entier,entier>dernière = nouveau HashMap<>();
pour (int i = 0; i < n; i++) {
last.put(nums[i], i);
}

int cnt = 0; // nombre de segments incassables
int maxRight = 0; // le plus proche de l'index droit nécessaire

pour (int i = 0; i < n; i++) {
maxRight = Math.max(maxRight, last.get(nums[i]);
si (i == maxRight) { // segment terminé
cnt++;
}
}

// réponse = 2^(cnt-1) mod MOD
résultat long = 1;
pour (int i = 0; i < cnt - 1; i++) {
résultat = (résultats * 2) % MOD;
}
retour (int) résultat;
}
}
«» "

---

Python

'`python
Solution de classe:
MOD = 10**9 + 7

Numéro DeGoodPartitions(même, nombres: Liste[int]) -> Int:
Last = {x: i pour i, x dans le dénombrement(nums)}
cnt = 0
max_right = 0

pour i, x dans le dénombrement(nombres):
max_right = max(max_right, last[x])
i == max_right: # fin d'un segment autonome
cnt += 1

# 2^(cnt-1) mod MOD
retour pow(2, cnt - 1, self. MOD)
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre intDeGoodPartitions(vecteur<int> et nombres) {
MOD = 1'000'000'007;
unordered_map<int, int> dernier;
pour (int i = 0; i < (int)nums.size(); ++i)
last[nums[i]] = i;

cnt = 0;
Int maxRight = 0;
pour (int i = 0; i < (int)nums.size(); ++i) {
maxRight = max(maxRight, last[nums[i]]);
si (i) maxRight)
++cnt;
}

long an = 1;
pour (int i = 0; i < cnt - 1; ++i)
ans = (ans * 2) % MOD;
retour (int)ans;
}
};
«» "

---

- Oui. 7. SEO & Conseils d'entretien d'emploi

Mot-clé cible Pourquoi ça compte
C'est une bonne idée.
**Leetcode 2963**L'identifiant officiel de LeetCode – s'assure que quiconque Googling le problème trouve l'article. Autres
**comptez le nombre de bonnes partitions**Le nom du problème – rangez-vous plus haut sur Google. Autres
** Solution Java** / ** Solution Python** / ** Solution C++** Autres
**question d'entrevue**= Indique que l'article est prêt pour l'entrevue. Autres
**programmation dynamique, fenêtre coulissante** Autres
**Modulo arithmétique** Autres

> **Comment utiliser cet article dans un entretien d'embauche* *
> 1. Montrer l'intuition **** d'abord – les intervieweurs aiment un modèle mental propre.
> 2. Présentez l'algorithme en **deux passes concises**; soulignez la garantie de temps O(n).
> 3. Partagez une formule d'exposition modulaire *simple*; mentionnez que vous pouvez également précalculer les pouvoirs de deux si vous préférez.
> 4. Enveloppez-vous avec la taille du tableau. Et si nous voulons que tout *sub‐array* compte? – une excellente façon de transformer la question en une discussion ouverte.

---

- Oui. 8. L'Ugly – Ce qu'il faut éviter

Mauvaise idée Pourquoi c'est moche
C'est pas vrai.
**Recursive DP avec mémoisation** qui stocke chaque position fractionnée → O(n2) time, O(n2) memory. Trop lent pour `n = 105`. Autres
Autres **Désorceler le tableau d'abord** pour trouver des valeurs uniques → perd la propriété *contiguité* ; casse le problème , le noyau. Autres
**Essayez de construire la réponse à la volée** en retraçant toutes les scissions → explosion exponentielle; les intervieweurs s'attendent à une solution linéaire. Autres
**Utiliser BigInteger ou précision arbitraire** en Java/C++ juste pour le calcul de puissance → frais généraux inutiles. Autres

---

- Oui. 9. Le bon – propre et entrevue‐ Amiable

1. **Une passe linéaire** (si vous êtes prudent avec la carte).
2. **Noms exacts des variables** (`cnt`, `maxRight`, `dernier`).
3. **Éviter les boucles imbriquées** pour l'exposé lorsque `cnt` est petit – une seule boucle avec `pow(2, cnt‐1, MOD)` est élégant en Python; `pow` en Java 8+ ou itérative double fonctionne aussi.

---

- Oui. 10. Les mauvais – les pièges communs

Mauvais modèle Autres
Il n'y a pas de lien entre les deux.
"pour (int i=1;i<cnt;i++) ans*=2;` sans module" `ans = (ans * 2) % MOD;"
Utiliser `int` pour les résultats de multiplication → déborder. Autres
Ré-calculer `dernier` pour chaque cas d'essai dans un juge en ligne avec de nombreuses requêtes. Réutiliser la carte; mais LeetCode exécute une requête par invocation de toute façon. Autres

---

## 11. Prise- Liste de contrôle (pour votre curriculum vitae et vos entrevues)

- 2-pass scan linéaire → **O(n)** temps, **O(n)** espace
- Poignées grandes valeurs (= 109) avec ints 32 bits
- Modulo arithmétique géré correctement
- connaissance de l'Edge-case (tableaux d'éléments uniques, valeurs répétées)
- Exponentiation modulaire ('pow(2, cnt‐1, MOD)')
- Le code est **3-fichier**-prêt – copier-coller dans votre IDE et courir.

---

12. Pensée finale

> **Code bon** = *concise*, *correct*, *readable*.
> **Code Bad** = *surmonté*, *buggy*, *difficile à suivre*.
> La partie **ugly** est la tentation de surestimer la puissance de deux ou d'écrire une table DP complète qui ne sera jamais nécessaire.

Avec l'algorithme à deux passages, vous pouvez répondre avec confiance Combien de bonnes partitions existent ?

Codage heureux – et bonne chance d'atterrissage que **ingénierie logiciel** rôle!

---