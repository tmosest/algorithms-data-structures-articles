---
titre: LeetCode 2588. Compter le nombre de magnifiques sous-arrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution (Java, Python et C++)

"Java
/* Java – LeetCode 2588: Comptez le nombre de belles sous-tribus */
/* Heure : O(n) Espace : O(n) */
solution de classe {
public long beau Autres
// carte de fréquence des valeurs XOR préfixées
HashMap<entier, entier> freq = nouveau HashMap<>();
freq.put(0, 1); // le préfixe vide a XOR = 0

long ans = 0;
Int pref = 0;
pour (int x : nombres) {
pref ^= x; // préfixe courant XOR
ans += freq.getOrDefault(pref, 0); // tous les préfixes précédents avec le même XOR forment un beau sous-array
freq.put(pref, freq.getOrDefault(pref, 0) + 1);
}
le retour des an;
}
}
«» "

'`python
# Python – LeetCode 2588: Comptez le nombre de belles sous-tribus
♪ Heure : O(n) Espace : O(n)
Importations provenant des collections Compteur

Solution de classe:
Def belle Subarrays(self, nombres: list[int]) -> Int:
freq = compteur({0: 1}) # préfixe XOR 0 se produit une fois (préfixe vide)
pref = ans = 0
pour x en nombres:
pref ^= x
ANS += freq[pref]
freq[pref] += 1
retour et
«» "

'`cpp
// C++ – LeetCode 2588: Comptez le nombre de belles sous-tribus
// Temps : O(n) Espace : O(n)
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue longue belle Subarrays(vecteur<int>& nums) {
non ordonné_map<int,int> freq{{0,1}};
long an = 0;
Int pref = 0;
pour (int x : nombres) {
pref ^= x;
ans += freq[pref];
++freq[pref];
}
le retour des an;
}
};
«» "

Les trois implémentations partagent la même idée : maintenir un préfixe XOR carte et compter combien de fois le même préfixe XOR est apparu avant. Chaque paire de préfixes égaux XOR définit un sous-array dont XOR est 0, c'est-à-dire un sous-array **beau**.



-----------------------------------------------------------------------------------

- Oui. 2. Article de blog – Le bon, le mauvais, et l'acharnement de beaux Subarrays

### 2.1 Titre & Meta Description (SEO)

- **Titre:** 2588 – Le bon, le mauvais et le mauvais
- **Meta Description:** Apprendre à résoudre le LeetCode 2588 avec un préfixe propre Algorithme XOR. Obtenez du code en Java, Python, C++, ainsi que des conseils de style interview pour décrocher votre prochain emploi. (en milliers de dollars)

---

Introduction

Avez-vous déjà regardé un problème LeetCode qui semble trompeurment simple mais qui s'avère être une question *trick*?
LeetCode **2588 – Comptez le nombre de beaux subarrays** est un tel puzzle. À la surface, il s'agit de manipulations de bits et de soustractions par paires, mais le calcul sous-jacent est élégamment capturé par l'opération XOR.

Dans cet article, nous disséquerons le problème, passerons par une solution propre, prête à la production, et soulignerons:

Autres Ce qu'il faut apprendre Pourquoi ça compte
- C'est quoi ?
**Bonne** – La perspicacité de "Aha" qui *beau* . *XOR = 0*.
Autres **Bad** – Pièges communs (off‐by‐one, mauvaise carte init, débordement)
**Ugly** – Cas de bords cachés (tous les zéros, grande entrée)

---

### 2.3 Énoncé du problème (version courte)

> **Don** un tableau «nums» de longueur «n» («1 ≤ n ≤ 105») où chaque élément est «0 ≤ nombres[i] ≤ 106»,
> **Count** le nombre de subarrays contigus qui peuvent être réduits à tous les zéros en sélectionnant à plusieurs reprises deux indices avec un bit commun `k` et en soustrayant `2k` des deux.

> Subarrays qui sont déjà tous les zéros comptent comme beau.

---

### 2.4 Le bon: le beau = XOR 0

Lorsque vous soustrayez `2k` de deux nombres qui ont tous les deux le "k`-th bit set, vous basculez efficacement ce bit **out** des deux nombres. Répéter cette opération pour tous les bits, vous finirez avec zéro *iff* le XOR de tous les nombres dans le sous-barrage est zéro.

** Pourquoi XOR ? **
'a XOR b = 0 ' , 'a == b '.
Si vous regardez la représentation binaire du sous-réseau, chaque opération annule un bit commun de deux numéros. La *parité* (débit/dénombrement) des bits de réglage pour chaque position doit être égale pour que tous les bits disparaissent – c'est exactement ce que XOR‐zero garantit.

> **Résultat:** Une subarray est belle **iff** la XOR de tous ses éléments égale `0`.

---

2.5 L'algorithme – Préfixe XOR + HashMap

1. **Préfixer le tableau XOR**
«pref[i] = nombres[0] ^ nombres[1] ^ ... ^ nombres[i]».

2. **Observation**
La valeur XOR de la sous-marque `l.r` est `pref[r] ^ pref[l‐1]`.
Cela équivaut à `0` **iff** `pref[r] == pref[l‐1]`.

3. **Pairs avec préfixe égal XOR**
itérer une fois au-dessus de "nums", en maintenant une carte de fréquence des XORs aperçus.
Pour chaque nouveau préfixe `p`:
- Tous les indices précédemment vus avec le même "p" forme beau sous-arrays se terminant à l'indice courant.
- `ans += freq[p]`.
- `freq[p]++`.

4. **Edge‐Case** – Préfixe vide
Initialiser la carte avec `{0: 1}` de sorte que les sous-barrages commençant par l'index `0` soient correctement comptés.

**Complexités* *

Valeur de complexité
C'est pas vrai.
Temps **O(n)** – un scan, opérations de hachage à temps constant
Espace **O(n)** – la carte contient au plus des valeurs de préfixe distinctes `n+1`

---

2.6 Les mauvaises: erreurs courantes

À quoi ça ressemble
C'est ce qu'on dit.
Autres Oubliant de compter les sous-barrages qui commencent à l'index `0`.
Utiliser `int` pour la réponse lorsque `n = 105`. (Python gère les gros int)
"Pref ^= num` vs `pref -= num`" Garder XOR; l'opération est conceptuelle, pas une réelle soustraction.
"Off‐by‐one dans la boucle" (en utilisant `pour (int i = 1; i <= n; ++i)` avec tableau 0-basé)

---

2.7 Les plus moches : les cas de bord et les obstacles de performance

Pourquoi ça compte Comment faire
- C'est quoi ?
Autres Tous les zéros ('[0,0,]') Chaque sous-arrachage est beau; le nombre est `n(n+1)/2`. L'algorithme produit naturellement ce résultat parce que chaque préfixe XOR reste `0`. Autres
Autres Grande entrée (`n = 105`, `nums[i] = 106`) La taille de la carte passe à `n+1`, toujours bien en mémoire. Utiliser `unordered_map` (C++) ou `HashMap` (Java) – ils donnent des opérations O(1) moyennes. Autres
Autres Les valeurs XOR préfixées sont extrêmement rares (par exemple, seulement 0 et 1). Pas besoin de manipulation spéciale. Autres

---

2.8 Entretien— Conseils prêts

1. ** Expliquez le tour de XOR d'abord** – les intervieweurs adorent le moment "aha".
2. **Afficher la réduction** de la force brute O(n2) à O(n) avec une carte.
3. **Débats sur le temps et l'espace** – peut-être mentionner un arbre Fenwick ou un arbre segmentaire s'ils le demandent.
4. **Demander des questions précises** sur l'indexation à base zéro et à base unique; confirmer la définition des sous-barrages à base de «beautiful» pour les tableaux à base de zéro.
5. **Code sur un tableau blanc** – écrivez explicitement l'initialisation de la carte de hachage; il démontre l'attention au détail.

---

Code final (toutes langues)

> **Java** – Utilise `HashMap` et une réponse `long`.
> **Python** – Utilise `Counter` et le support intégré de grand-int.
> **C++** – Utilise `unordered_map` pour le cas moyen O(1).

Chaque extrait est prêt à être collé dans l'éditeur LeetCode ou une repo de production.

---

2.10 Conclusion

LeetCode 2588 est un exemple de manuel de la façon dont une profonde perspicacité mathématique (beaux 0) peut transformer un problème complexe de manipulation des bits en un exercice de comptage linéaire.

Par compréhension:

- **Le Bon** (perspective XOR),
- **Les mauvais** (les bugs communs),
- **L'Ugly** (cas de référence et performances),

non seulement as ce problème, mais aussi être en mesure de l'expliquer avec confiance dans toute entrevue de codage.

> **Étape suivante:** Essayez de mettre en œuvre la même idée dans une langue avec laquelle vous êtes moins familier, ou modifiez la carte pour utiliser une `TreeMap` et voir l'impact sur l'exécution.

Bonne chance, et que votre prochaine interview soit *beaucoup*!