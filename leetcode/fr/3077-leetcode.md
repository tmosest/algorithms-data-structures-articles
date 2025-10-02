---
titre: LeetCode 3077. Résistance maximale des sous-arrachages de K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (Code de débit 3077)

> **Résistance maximale des sous-arrachages de K
> **Difficulté:** Dur
> **Tags:** Programmation dynamique, Préfixe Sum, Knapsack

Vous êtes donné un tableau entier `nums` (longueur `n`) et un étrange entier `k`.
Choisissez exactement les sous-partages "k" disjoints
`sub1, sub2, ..., subk` de telle sorte que le dernier indice de `subi` soit strictement avant le premier indice de `subi+1`.
La force **** d'un ensemble choisi est

«» "
résistance = k * somme(sub1) – (k‐1) * somme(sub2) + (k‐2) * somme(sub3) – ... – 2 * somme(sub{k‐1}) + somme(subk)
«» "

Retourne la force maximale possible.
`1 ≤ n ≤ 104`, `=nums[i]=109`, `1 ≤ k ≤ n`, `k` est impair et `n·k ≤ 106`.

Le problème est un problème de programmation dynamique classique avec une torsion de la somme en alternant avec la pondération.



---

- Oui. 2. Idées fondamentales

*Le problème peut être réécrit comme un DP sur les sommes préfixées. *

Pour chaque préfixe `0 ... j` nous conservons la meilleure force possible pour les premiers sous-partages `i` qui terminent **à l`intérieur** ce préfixe.
Laissez

«» "
dp[i][j] = résistance maximale que l'on peut obtenir en cueillant i sous-arrays disjoints à partir de nombres[0 ... J-1)
«» "

Transition pour la sous-requête «i» :

«» "
dp[i][j] = max( dp[i][j-1], // ne terminent pas un sous-barrage à j-1
max_{t<i-1 ... j-1} ( dp[i-1][t] + poids(i) * (pref[j] – pref[t]) )
«» "

où
«préf[x]» est la somme du préfixe `nums[0] + ... + nums[x-1]` et

«» "
poids(i) = (k - i + 1) * (-1)^(i+1)
«» "

Parce que `k` est étrange, les poids alternent `+k, -(k‐1), +k‐2, ..., +1`.
La maximisation intérieure peut être maintenue en *O(1)* par `j` en conservant la meilleure valeur de

«» "
dp[i-1][t] - poids(i) * pref[t]
«» "

pendant qu'il s'agit de "j".
Complexité globale: temps `O(k·n)` et espace supplémentaire `O(n)` (nous ne conservons que deux lignes).

---

- Oui. 3. Code

Ci-dessous sont propres, implémentations idiomatiques dans **Java, Python, et C++**.
Chaque fichier est autonome et prêt à copier-coller dans une solution LeetCode.

Autres Toutes les solutions supposent l'indexation 0 pour les "nums" et utilisent l'arithmétique longue (64 bits) pour éviter les débordements.

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {
public long maximumRésistance(int[] nombres, int k) {
int n = longueur nums;
long[] pref = nouveau long[n + 1];
pour (int i = 0; i < n; i++) pref[i + 1] = pref[i] + nombres[i];

long[] prev = nouveau long[n + 1]; // dp[i-1][*]
long[] cur = nouveau long[n + 1]; // dp[i][*]

pour (int i = 1; i <= k; i++) {
poids long = (k - i + 1) * (i & 1) == 1 ? 1 : -1); // (+,-,+,-,...)
long best = Long.MIN_VALUE; // best of (dp[i-1][t] - poids*pref[t])
pour (int j = 1; j <= n; j++) {
// Mettre à jour le meilleur pour le j actuel (t = j-1)
best = Math.max(meilleur, prev[j - 1] - poids * pref[j - 1]);

// Option 1: ne pas mettre fin à une sous-exploitation à j-1
longue pas Fin = cur[j - 1];

// Option 2: terminer un sous-partage à j-1
long terme Ici = meilleur + poids * pref[j];

cur[j] = Math.max(notEnd, finIci);
}
// swap lignes pour la suivante i
long[] tmp = prev; prev = cur; cur = tmp;
}
retour prev[n];
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def maximum Force (soi-même, nombres: Liste[int], k: int) -> Int:
n = len(nums)
pref = [0] * (n + 1)
pour i, v en énumération(nombres, 1):
pref[i] = pref[i-1] + v

Prév = [0] * (n + 1)
[0] * (n + 1)

pour i dans la plage (1, k + 1):
Poids = (k - i + 1) * (1 si i & 1 autre -1)
meilleure = flotteur('-inf')
pour j dans la plage(1, n + 1):
# mettre à jour le mieux pour t = j-1
best = max(meilleur, prev[j-1] - poids * pref[j-1])

# garder l'état précédent
not_end = cur[j-1]
# Finissez une sous-tribu à j-1
fin_ici = meilleur + poids * pref[j]

cur[j] = max(not_end, fin_ici)
prev, cur = cur, prev # tableaux de réutilisation
retour prev[n]
«» "

---

### 3.3 C++

'`cpp
solution de classe {
public:
long long maximumStrength(vecteur<int>& nums, int k) {
int n = nombres.size();
vecteur <long> pref(n + 1, 0);
pour (int i = 0; i < n; ++i) pref[i+1] = pref[i] + nums[i];

vecteur <long> prev(n + 1, 0), cur(n + 1, 0);

pour (int i = 1; i <= k; ++i) {
poids long = (long long)(k - i + 1) * (i & 1) ? 1 : -1);
longue longue meilleure = LLONG_MIN;
pour (int j = 1; j <= n; ++j) {
// mettre à jour le mieux pour t = j-1
best = max(best, prev[j-1] - poids * pref[j-1]);

longue pas longtemps Fin = cur[j-1];
long terme Ici = meilleur + poids * pref[j];

cur[j] = max(notEnd, finHere);
}
swap(prev, cur);
}
retour prev[n];
}
};
«» "

Les trois solutions fonctionnent dans **O(k · n)** temps et **O(n)** espace supplémentaire – bien en dessous des limites (`n·k ≤ 106').

---

- Oui. 4. Article de blog: -Le bon, le mauvais, et l'indulgence de LeetCode 3077

> **Titre:**
> * La force maximale de K Disjoint Subarrays – Le Bon, le Mauvais et l'Ugly (Une Masterclass)*
> **Meta Description:**
> Master LeetCode 3077 avec une programmation dynamique, un code pratique en Java, Python & C++ et des informations prêtes à l'interview.
> **Mots-clés:** LeetCode 3077, force maximale de k disjoint subarrays, programmation dynamique, codage d'entrevue, entretien d'emploi, conception d'algorithmes

---

4.1 Introduction

LeetCode 3077 vous demande de choisir *exactement* `k` disjoint sous-arrays à partir d'un tableau entier et de maximiser une somme alternative pondérée*.
À première vue, il se sent comme une variante de la somme maximale classique de `k` disjoint sub-arrays=, mais le motif de signe (+, –, +, – ...) jette une clé dans des solutions standard.

Si vous préparez une entrevue de structure de données ou d'algorithme, la maîtrise de ce problème démontre :

* ** Compétence PD** – vous pouvez formuler un PD multidimensionnel avec des transitions d'état non trivial.
* ** Optimisation de l'espace** – vous pouvez réduire `O(k·n)` à `O(n)` en réutilisant les lignes.
* **Attention au détail** – vous manipulez correctement les nombres négatifs et les grandes entrées.

Disséquer le problème en trois parties :

Autres Partie Ce que vous apprenez Pourquoi ça compte
-- -- -- -- -- -- -- -- --
**Le bon**=Clean DP formulation + complexité du temps/de l'espace
**Le mauvais**=Pièges communs (dépassement par un, erreurs de signe, débordement)== Faits saillants de ce que *pas* à faire lors d'une entrevue==
**L'Ugly**

---

4.2 Le bon – un PDD propre

État

`dp[i][j]` = meilleure force en utilisant **premier `i` sous-arrays** dans le préfixe `nums[0...j-1]`.

- gammes "i" Oui.
- Gamme "j" 0...n.
- Cas de base: `dp[0][*] = 0` (pas de sous-course → résistance 0).

4.2.2 Transition

Pour la sous-tribu `i`, son poids est

«» "
poids(i) = (k - i + 1) * (-1)^(i+1)
«» "

Si l'on termine la sous-requête `i`‐th à l'index `j-1`, la somme de sous-requête est `pref[j] - pref[t]` pour certains `t < j`.
Ainsi:

«» "
dp[i][j] = max(
dp[i][j-1], // sauter j- 1
max_{t < j} ( dp[i-1][t] + poids(i) * (pref[j] - pref[t]) )
)
«» "

Le maximum intérieur regarde *tous* les points de départ possibles de la dernière sous-tribu.
Sans optimisation, ce serait "O(n)" par cellule, donnant "O(k·n2)" – trop lent.

4.2.3 Préfixe Trick

Définir

«» "
best = max_{t < j} ( dp[i-1][t] - poids(i) * pref[t] )
«» "

Alors

«» "
dp[i][j] = max( dp[i][j-1] , meilleur + poids(i) * pref[j] )
«» "

Au cours de l'analyse sur `j`, nous tenons `meilleure` mise à jour en `O(1)` temps, donnant globalement `O(k·n)`.

4.2.4 Réduction de l'espace

Seuls les termes `dp[i-1][*]` et `dp[i][*]` sont nécessaires simultanément.
Nous conservons deux tableaux 1-D `prev` et `cur`, les échangeant après chaque `i`.
L'espace se rétrécit à `O(n)` – vital quand `k` peut être quelques milliers.

---

### 4.3 Les mauvaises – Pièges communs

1. **Sommes préfixées en off‐by‐one**
- Utiliser sans équivoque `pref[j]` au lieu de `pref[j-1]` dans la transition.
- Correction : Souvenez-vous de "pref[x]" est la somme des premiers éléments "x".

2. **La confusion des signes de poids**
- Comme `k` est étrange, les poids sont alternés à partir de `+k`.
- Une erreur de signe se propage à travers le DP, donnant une réponse négative absurdement grande.

3. **Débordement entier**
- Chaque «nums[i]» peut être 109 et il peut y avoir jusqu'à 104 éléments → préfixe somme jusqu'à 1013.
- Utiliser `long`/`long long` (64 bits) au lieu de `int`.

4. **Cas de base en faute**
- Oublier `dp[0][j] = 0` conduit à la propagation `Long.MIN_VALUE` et le plantage de l'algorithme.

5. **Non réutilisant des tableaux**
- Certaines solutions allouent des matrices `k`×`n` et dépassent la mémoire (même si `n·k ≤ 106` le facteur constant compte en Java).

6. **Diversité d'interprétation**
- Les sous-tarifs doivent être *non-overlaping*; vous ne pouvez pas sauter un index à l'intérieur d'un sous-tarif choisi.

---

#### 4.4 La dure – Modèle de poids plongée profonde

Le modèle de poids `(+k, -(k-1), +k-2, ..., +1)` est ce qui transforme ce problème en un problème de "gugly".

4.4.1 Pourquoi ça compte

Si tous les poids étaient `+1`, le DP réduit à la somme connue de ‘k` disjoint sub-arrays' – vous pouvez le résoudre avec une simple récurrence.
Les signes alternés signifient la contribution d'un sous-réseau *soustraire* du total si son indice est égal (par rapport à l'ordre choisi).

4.4.2 Perspectives d'optimisation

Considérez la maximisation intérieure:

«» "
max_{t} ( dp[i-1][t] + poids * (pref[j] – pref[t]) )
«» "

Élargissement :

«» "
= poids * pref[j] + max_{t} ( dp[i-1][t] - poids * pref[t] )
«» "

Le terme à l'intérieur du `max` est *indépendant* de `j` après que nous avons corrigé `t`.
Par conséquent, tout en scannant `j` de gauche à droite, nous pouvons maintenir la meilleure valeur de

«» "
Dp[i-1][t] - poids
«» "

dans une variable "meilleur".
Chaque nouveau `j` a juste besoin `prev[j-1] - poids * pref[j-1]` pour mettre à jour le "meilleur".
C'est le truc algébrique qui transforme le DP en temps *linéaire* par 'i'.

---

4.5 Entretien Conseils prêts

Conseil Exemple de code Extrait Autres
-- -- -- -- -- -- ------------------ -- --
** Expliquez votre diagramme DP** – tableau "dp" sur papier. `dp[i][j]` – premier `i` sub-arrays à l'intérieur `0...j-1`. Autres
**Parcourir un petit exemple** (par exemple, "nums = [1,-2,3,4]", "k=3". Afficher comment `meilleur` met à jour chaque étape. Autres
**Montrer la manipulation du débordement** – utiliser `long`.
**L'espace est optimisé** – mentionner l'échange de lignes. "swap(prev, cur);" Autres
** Expliquez pourquoi k est bizarre** – veille à ce que le poids final soit la formule `+1`. Autres

---

### 4.6 Conclusion

LeetCode 3077 est un beau mélange de *classic DP* et *non-trivial optimisation*.
Vous pouvez le résoudre proprement, éviter les pièges d'entrevue courants, et surtout montrer aux intervieweurs que vous pouvez *voir* la structure sous-jacente et la traduire en code.

> *Solvez le problème, puis demandez: à quoi ressemblerait une question d'entrevue de suivi?
> Cette curiosité vous garde devant la courbe.



---

- Oui. 5. Pensées finales

La solution DP ci-dessus est à la fois **efficace** et **extensible**.
Si vous n'êtes pas sûr comment l'aborder à l'entrevue, essayez de construire la table DP à la main pour une petite entrée – vous verrez le modèle du meilleur jusqu'à présent.

Bon codage, et bonne chance pour ce travail ! C'est ce qu'il a dit.



---



5.1 Références

* LeetCode 3077 – Résistance maximale des sous-arrachages de K
* La somme maximale de `k` non-overlapping Subarrays - classique LeetCode 689
* Programmation compétitive 3 – techniques de programmation dynamique



---



* Se sentir libre de commenter ci-dessous si vous souhaitez une plongée plus profonde dans l'une des optimisations DP ou des stratégies d'entrevue! *