---
titre: LeetCode 3258. Compter des sous-chaînes qui satisferont K-Constraint Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes
**LeetCode 3258 – Compter les sous-chaînes qui satisfont K‐Constraint I**

> Une chaîne binaire satisfait à la contrainte *k* si **ou* *
> *le nombre de 0s ≤ k* **ou** *le nombre de 1s ≤ k*.
>
> Pour une chaîne binaire donnée `s` (longueur ≤ 50) et un entier `k`,
> retourner le nombre de sous-chaînes qui satisfont à la contrainte k.

> **Exemples**
> `` "
> s = "10101", k = 1 → 12
> s = "1010101", k = 2 → 25
> s = "11111", k = 1 → 15
> `` "

La solution O(n2) naïve vérifie chaque sous-chaîne; nous pouvons faire mieux avec une approche par fenêtre coulissante (deux-pointeurs) dans le temps O(n) et dans l'espace O(1).



-----------------------------------------------------------------------------------

Pourquoi glisser la fenêtre ?
Une sous-chaîne est définie par un index gauche et droit.
Si nous conservons une fenêtre *valid* `[gauche ... droite]` qui satisfait la contrainte k, puis toute sous-sous-chaîne se terminant à « droite » et commençant quelque part dans la fenêtre est automatiquement valide.

Lorsque nous étendons `à droite`, nous pouvons briser la contrainte – à ce moment nous *retirons* de la gauche jusqu'à ce que la fenêtre devienne valide à nouveau.
Le point de vue clé : le nombre de nouvelles sous-chaînes valides ajoutées lorsque `right` passe à la position suivante est égal à la taille de la fenêtre (`right – gauche + 1`). Résumant que sur toutes les positions donne la réponse.



-----------------------------------------------------------------------------------

Les trois mises en œuvre

- Oui. 1. Java

"Java
solution de classe publique {
public int countKConstraintSubstrings(String s, int k) {
int n = s.longueur();
Int gauche = 0, count0 = 0, count1 = 0, ans = 0;

pour (int right = 0; right < n; right++) {
// Élargir la fenêtre
si (s.charAt(right) == '0') count0++;
sinon compter1++;

// Réduire pendant que les deux nombres dépassent k
pendant que (compte0 > k && compte1 > k) {
si (s.charAt(gauche) == '0') nombre0--;
sinon compter1--;
gauche++;
}

// Toutes les sous-chaînes se terminant à « droite » sont valides
+= (droite - gauche + 1);
}
le retour des an;
}
}
«» "

- Oui. 2. Python

'`python
Solution de classe:
def countKConstraintSubstrings(self, s: str, k: int) -> Int:
n = len(s)
gauche = 0
cnt0 = cnt1 = 0
ans = 0

pour droite, ch en énumération(s):
si ch == '0':
cnt0 += 1
Sinon:
cnt1 += 1

# Fenêtre de rétrécissement jusqu'à ce qu'elle soit de nouveau valide
alors que cnt0 > k et cnt1 > k:
si s[gauche]] «0»:
cnt0 -= 1
Sinon:
cnt1 -= 1
gauche += 1

ans += droite - gauche + 1

retour et
«» "

- Oui. 3. C++

'`cpp
solution de classe {
public:
int countKConstraintSubstrings(string s, int k) {
int n = s.size();
Int gauche = 0, cnt0 = 0, cnt1 = 0, ans = 0;

pour (int droite = 0; droite < n; ++ droite) {
si (s[droit]] '0') ++cnt0;
autres ++cnt1;

pendant que (cnt0 > k && cnt1 > k) {
si (s[gauche] == '0') --cnt0;
autres --cnt1;
+ + gauche;
}

ans += droite - gauche + 1;
}
le retour des an;
}
};
«» "

Les trois codes fonctionnent dans le temps **O(n)** et n'utilisent qu'une poignée de variables entières – parfaites pour les contraintes (`n ≤ 50`) et pour le codage de type interview.



-----------------------------------------------------------------------------------

Le bon, le mauvais et l'acharnement de compter les sous-chaînes K-Constraint

Titre
Les sous-chaînes K-Constraint – Une classe de maîtres de fenêtres coulissantes : le bon, le mauvais et le mauvais**

* Mots-clés de référence*: `leetcode k contrainte`, `count substrings`, `sliding window`, `binary string interview`, `coding interview practice`, `Java Python C++ solution`, `leetcode 3258`, `algorithm interview questions`, `data structures interview`.

---

Introduction

Quand vous trébuchez **LeetCode 3258 – Sous-chaînes de comptage Cette Satisfy K-Constraint I**, vous êtes remis un problème trompeurment simple qui teste votre capacité à jongler deux compteurs et deux pointeurs à la fois.

Ci-dessous, je marcherai à travers le **bon** (pourquoi l'approche de la fenêtre coulissante brille), le **mauvais** (ce qui écume les gens quand ils écrivent une solution de force brute), et le **ugly** (pièges de cases qui peuvent briser même le code le plus élégant).
En cours de route, je vous propose des solutions Java, Python et C++ que vous pouvez déposer dans votre éditeur de code en quelques secondes.

> ** Conseil professionnel :** Parce que la longueur de chaîne d'entrée est au plus 50, vous pouvez tricher avec la force brute si vous êtes pressé. Mais pour une interview *real* ou un concours LeetCode, O(n) time est le seul chemin vers le succès.

---

### La bonne: Fenêtre coulissante – O(n) dans un Snap

1. **Heure linéaire** – Vous traversez la corde une fois, en faisant avancer le pointeur droit.
2. **Espace continu** – Seulement quelques entiers suivent les nombres de 0 et 1.
3. **Le raisonnement intuitif** – Toute sous-chaîne qui se termine à l'index `right` et démarre n'importe où dans la fenêtre valide `[left ... right]` est garantie pour satisfaire la contrainte.
4. **Pas de boucles cachées** – La boucle interne rétrécit la fenêtre *seulement* si nécessaire, ne dépassant jamais le nombre total de caractères.

* Pourquoi ça compte :* Dans les panneaux d'entrevue, la démonstration d'une solution de fenêtre coulissante montre que vous pouvez penser à l'état et aux conditions limites de l'algorithme.

---

### Le mauvais: Force brute – O(n2) C'est une traînée

La mise en œuvre la plus naïve ressemble à :

'`python
pour i dans la plage(n):
zéros = 0
pour j dans la plage(i, n):
si s[j] == '0': zéros += 1
autres : ceux += 1
si zéros <= k ou ceux <= k: ans += 1
«» "

** Problèmes :**

- **Temps quasi** – Pour `n = 50`, vous terminez encore rapidement, mais pour les entrées plus grandes, il souffle.
- **Travaux répétés** – Chaque boucle intérieure recompute à partir de zéro, ignorant les informations que vous avez déjà.
- **Trouver la raison** – La logique devient encombrée; un recruteur verra un code de style «copie-colle».

* À emporter :* Même si les contraintes sont petites, examinez toujours si vous pouvez réduire la complexité avec un meilleur algorithme.

---

- Oui. L'horrible : des cas de bord qui vous emportent

Pourquoi ça compte ?
- Oui.
`k` égale la longueur de la chaîne. Autres
Tous les « 0 » ou tous les « 1 » s » Un compteur reste 0 » La fenêtre coulissante fonctionne toujours – l'autre compteur ne dépasse jamais « k ». Autres
Autres Alternant le motif `010101...`.Les deux compteurs peuvent frapper `k+1` simultanément. L'état intérieur pendant la boucle `cnt0 > k && cnt1 > k` garantit cela. Autres
La sous-chaîne doit avoir *non* 0s **ou** *non* 1=1s=1 La fenêtre coulissante est toujours valide; vous comptez essentiellement les tirages de caractères identiques. Autres

> ** Mission pour éviter :** Utiliser `cnt0 >= k && cnt1 >= k` dans la boucle de rétractation. Cela continuerait à rétrécir, même lorsqu'un compteur est exactement "k".

---

Code de travail complet (trois langues)

> **Copier les extraits ci-dessous dans votre IDE préféré ou éditeur en ligne. **

**Java**

"Java
solution de classe publique {
public int countKConstraintSubstrings(String s, int k) {
int n = s.longueur();
Int gauche = 0, cnt0 = 0, cnt1 = 0, ans = 0;

pour (int right = 0; right < n; right++) {
si (s.charAt(right) == '0') cnt0++;
autres cnt1++;

pendant que (cnt0 > k && cnt1 > k) {
si (s.charAt(gauche) == '0') cnt0--;
autrement cnt1--;
gauche++;
}

ans += droite - gauche + 1;
}
le retour des an;
}
}
«» "

**Python**

'`python
Solution de classe:
def countKConstraintSubstrings(self, s: str, k: int) -> Int:
n = len(s)
gauche = 0
cnt0 = cnt1 = 0
ans = 0

pour droite, ch en énumération(s):
si ch == '0': cnt0 += 1
autres: cnt1 += 1

alors que cnt0 > k et cnt1 > k:
si s[left] == '0': cnt0 -= 1
sinon: cnt1 -= 1
gauche += 1

ans += droite - gauche + 1

retour et
«» "

**C++**

'`cpp
solution de classe {
public:
int countKConstraintSubstrings(string s, int k) {
int n = s.size(), gauche = 0, cnt0 = 0, cnt1 = 0, ans = 0;
pour (int droite = 0; droite < n; ++ droite) {
si (s[droit]] '0') ++cnt0;
autres ++cnt1;

pendant que (cnt0 > k && cnt1 > k) {
si (s[gauche] == '0') --cnt0;
autres --cnt1;
+ + gauche;
}

ans += droite - gauche + 1;
}
le retour des an;
}
};
«» "

---

À emporter pour l'entrevue

1. **Énoncer clairement le problème** – Sous-chaînes de comptage où soit le nombre de 0 ≤ k, soit le nombre de 1 ≤ k.
2. **Expliquez l'invariant** – Notre fenêtre est toujours valide; rétrécissant seulement lorsque les deux compteurs dépassent k.
3. **Complexité** – temps O(n), espace O(1). (en milliers de dollars)
4. **Edge Cases** – Tous zéros, tous alternés, k = 0 – tous traités par la même logique. (en milliers de dollars)

Être capable d'articuler cela vous fera des marques élevées.

---

Bonus: SEO-optimisé Meta Description (pour votre blog)

> Master LeetCode 3258 avec une solution de fenêtre coulissante. Apprenez le code Java, Python et C++, plus comment éviter les pièges communs et expliquer l'algorithme dans les interviews. (en milliers de dollars)

---

La pensée finale

La technique de la fenêtre coulissante transforme un problème apparemment quadratique en un problème linéaire élégant. Une fois que vous internalisez l'idée que chaque sous-chaîne se terminant au pointeur droit actuel à l'intérieur de la fenêtre valide est valide.

Bon codage, et bonne chance pour ce travail !