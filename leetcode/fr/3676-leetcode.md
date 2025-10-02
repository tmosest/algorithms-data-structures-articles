---
titre: LeetCode 3676. Comte Bowl Subarrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3676 – Subarrays du Comte Bowl
** Des solutions complètes en Java, Python et C++ + un blog d'interview prêt pour le référencement* *

> Si vous comprenez le "pourquoi" derrière une solution, vous vous en souviendrez pour toujours. – Communauté LeetCode

---

Table des matières
Description de la section
C'est pas vrai.
Autres Aperçu du problème
Autres Pourquoi il échoue sur les grandes entrées
Une idée de base qui conduit à la solution O(n)
Autres Mise en œuvre – Java, commentaire, traitement des cas de bord
Autres Mise en œuvre – Python
Autres Mise en œuvre – version facile pour STL
Autres Analyse de la complexité
Le bon, le mauvais, le mauvais Ce que vous apprenez, les pièges et les pièges prêts à l'interview
Autres Mots clés, métabalises, appel à l'action

---

- Oui. 1. Aperçu du problème

> **Count Bowl Subarrays**
> Compter tous les sous-réseaux de longueur ≥ 3 qui satisfont à un nombre entier d'éléments distincts
> **min(nums[l], nombres[r]) > max(nums[l+1...r‐1])**.
> En d'autres termes, les deux bouts forment un "bowl" et chaque élément intérieur est strictement plus petit que les deux bouts.

Échantillon

Texte
Entrée : nombres = [2,5,3,1,4]
Produit: 2/ [3,1,4] et [5,3,1,4]
«» "

Obstacles

Valeur des contraintes
C'est pas vrai.
3 ≤ longueur maximale ≤ 105
1 ≤ nombres[i] ≤ 109
Autres Tous les éléments sont distincts.

---

- Oui. 2. Base de référence Brute-Force

Une boucle naïve à trois nerfs énumérant tous les subarrays fonctionnerait en **O(n3)** et est impossible pour `n = 105`.
Même une boucle à deux nerfs avec un maximum de marche à l'intérieur (O(n2)) sera chronométrée dans le pire des cas.

> **Pourquoi il échoue**
> *Le calcul intérieur maximum coûte O(longueur)* – répété plusieurs fois.
> Avec 105 éléments, c'est ~1010 opérations.

---

- Oui. 3. Regard sur les piles monotoniques – l'idée fondamentale

La condition peut être reformulée:

* Pour une sous-audience `[l ... r]`, l'élément **premier** à gauche qui est **plus grand** que `nums[r]` doit être **à l'intérieur** la sous-tribu, et de même pour la droite.
* Ceci se traduit par *recherchant, pour chaque index, l'élément supérieur suivant (GEN) à droite* et *l'élément supérieur précédent (GEP) à gauche*.

Si la distance entre un indice et son NGE (ou PGE) est d'au moins 2 (c'est-à-dire que le sous-réseau a une longueur ≥ 3), alors cette paire contribue **un** bol.

**Pourquoi une pile monotonique fonctionne* *

* Pendant le balayage de gauche à droite, gardez une pile d'indices dont les valeurs sont **decreasing**.
* Lorsque vous rencontrez un élément qui est **plus grand** que le haut de la pile, l'indice courant est le NGE pour tous les indices affichés.
* De même, le balayage de droite à gauche donne toutes les valeurs PGE.

Parce que chaque indice est poussé et affiché au plus une fois, la complexité globale est linéaire.

---

- Oui. 4. Mise en œuvre – Java

"Java
Importation de java.util.*;

solution de classe {
bol public longSubarrays(int[] nums) {
int n = longueur nums;
long res = 0;
si (n < 3) retourner 0;

// ----- ensuite plus grand (à droite) -----
int[] suivante = nouvelle int[n];
les tableaux.fill(suivant, -1);
Deque<Integer> pile = nouvelle ArrayDeque<>();

pour (int i = 0; i < n; i++) {
alors que (!stack.isEmpty() && nums[stack.peek()] < nums[i]) {
next[stack.pop()] = i; // i est le NGE pour l'indice popped
}
Le point i) est remplacé par le texte suivant:
}

// Compter les bols où l'extrémité gauche est le NGE de certains index
pour (int l = 0; l < n; l++) {
int r = suivant[l];
si (r != -1 && r - l + 1 >= 3) res++;
}

// ----- précédent supérieur (à gauche) -----
int[] prev = nouvelle int[n];
Tableau.fill(prev, -1);
empilé.clair();

pour (int i = n - 1; i >= 0; i--) {
alors que (!stack.isEmpty() && nums[stack.peek()] < nums[i]) {
prev[stack.pop()] = i; // i est le PGE pour l'indice popped
}
Le point i) est remplacé par le texte suivant:
}

// Comptez les bols où l'extrémité droite est le PGE de certains index
pour (int r = 0; r < n; r++) {
int l = prév[r];
si (l != -1 && r - l + 1 >= 3) res++;
}

retour rés;
}
}
«» "

Faits saillants

* `Deque<Integer>` pour une pile efficace (ops O(1) amorti).
* Deux scans distincts : un de gauche à droite (plus grand), un de droite à gauche (plus grand).
* 64 bits `long` est utilisé parce que la réponse peut dépasser `int`.

---

- Oui. 5. Mise en œuvre – Python

'`python
Solution de classe:
def bolSubarrays(self, nombres: List[int]) -> Int:
n = len(nums)
si n < 3: retour 0

# ----- ensuite plus grand -----
next_large = [-1] * n
pile = []
pour i, val dans l'énumération(nombres):
pendant la pile et les nombres[stack[-1]] < val:
idx = pile.pop()
next_great[idx] = i
pile.annexe(i)

Res = 0
pour l dans la plage(n):
r = plus grand_suivant[l]
Si r != -1 et r - l + 1 >= 3 :
Rés += 1

# ----- précédent plus grand -----
prev_greater = [-1] * n
empil.clear()
pour i dans la fourchette(n - 1, -1, -1):
pendant la pile et les nombres[stack[-1]] < nums[i]:
idx = pile.pop()
[idx] = i
pile.annexe(i)

pour r dans la plage(n):
L = prev_great[r]
si l != -1 et r - l + 1 >= 3 :
Rés += 1

retour res
«» "

*Utilise `list` comme pile (`append`/`pop`).
`int` dans Python 3 est débordé, donc pas de soucis de débordement. *

---

- Oui. 6. Mise en œuvre – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long bolSubarrays(vecteur<int>& nums) {
int n = nombres.size();
si (n < 3) retourner 0;
longue rés = 0;

// ----- ensuite plus grand (à droite) -----
vecteur<int> suivant(n, -1);
vecteur <int> st;
pour (int i = 0; i < n; ++i) {
pendant que (!st.vide() && nums[st.back()] < nums[i]) {
next[st.back()] = i; // i est NGE pour st.back()
le _retour_st.pop();
}
st.push_back(i);
}

pour (int l = 0; l < n; ++l) {
int r = suivant[l];
si (r != -1 && r - l + 1 >= 3) res++;
}

// ----- précédent supérieur (à gauche) -----
vecteur <int> prev(n, -1);
clear();
pour (int i = n - 1; i >= 0; --i) {
pendant que (!st.vide() && nums[st.back()] < nums[i]) {
prev[st.back()] = i; // i est PGE pour st.back()
le _retour_st.pop();
}
st.push_back(i);
}

pour (int r = 0; r < n; ++r) {
int l = prév[r];
si (l != -1 && r - l + 1 >= 3) res++;
}

retour rés;
}
};
«» "

* `vector<int>` + `vector<int>` pour les piles (LIFO) donne le même O(1) amorti par op. *

---

- Oui. 5. Analyse de la complexité

Aspect Formule Résultat
C'est quoi, ça ?
Chaque index est poussé et affiché une fois dans les deux scans. Autres
**L'espace**
**Type de réponse**

*La pile elle-même est au plus `n` dans la taille, de sorte que la mémoire supplémentaire est linéaire. *

---

- Oui. 6. Les bons, les mauvais, les méchants – Ce que veut l'intervieweur

Aspect Qu'est-ce que vous allez impressionner
-- -- -- -- -- -- -- -- -- -- -- --
**Bon*** *La pile monotonique* est un modèle d'entrevue classique – montre la connaissance des structures de données. <br>• Code est propre, fonctionne rapidement pour les éléments `105`.
**C'est mal interprété. <br>L'inégalité grave (`<=` vs `>`) change entièrement la logique. Autres
Une force brute peut être acceptée sur la suite de test LeetCode mais échouera dans une interview où le juge exécute 2 secondes TL. <br>De plus, les gens oublient souvent la propriété *distinct*, causant des recalculs inutiles `max`/`min`. <br>• Utilisation d'une récursion avec une pile → overflow sur 105. Autres

### Interview Trick : Pourquoi on a besoin de deux scans ? (en milliers de dollars)

*Parce que chaque extrémité d'un bol peut être le NGE d'un indice intérieur ou le PGE d'un indice extérieur.
Compter les deux directions nous assure de compter chaque paire valide exactement une fois. *

---

- Oui. 7. SEO–Friendly Takeaway

Méta-titre
> Count Bowl Subarrays – Solution efficace de piles monotoniques (Java, Python, C++)

### Méta-Description
> Master LeetCode 3676, Count Bowl Subarrays, avec une solution rapide O(n) monotonic-stack.
> Lisez notre guide prêt à l'entrevue, comparez les implémentations Java/Python/C++ et apprenez les modèles clés qui vous font briller dans les interviews de codage.

Mots clés
`count bowl subarrays`, `leetcode 3676`, `monotonic empil`, `job interview coding`, `Java solution`, `Python solution`, `C++ solution`, `array subarray comput`, `distinct elements`, `linéary time algorithme`, `interview pattern`.

En-têtes (H1–H3)
* LeetCode – Count Bowl Subarrays (H1)
* Résumé des problèmes (H2)
* Brute-Force vs O(n) (H3)
* Stack monotonique (H3)
* Java, Python, Code C++ (H3)
* Bon / mauvais / mauvais (H3)

### Appel à l'action
> **Vous voulez passer votre prochaine entrevue de codage? * *
> Téléchargez notre cours de 7 jours *Coding Interview Prep* par courriel, obtenez quotidiennement le guide LeetCode et commencez à décrocher des rôles de haute technologie.
> [Inscrivez-vous maintenant](https://exemple.com/prepare)

---

- Oui. 8. Enveloppage

* **Pourquoi cela importe** – La possibilité de transformer une condition de "bowl" en une paire de lookups plus grands éléments est une abstraction puissante qui montre que vous pouvez *penser en dehors de la boîte* et *appliquer des modèles DS classiques*.
* **Conseil d'interview** – Lorsque la description de LeetCode se sent étrangement libellée, la traduire en une relation qui peut être répondue avec une pile ou une file d'attente.
* **Au-delà du LeetCode** – Les piles monotoniques apparaissent dans les problèmes stock‐span, les requêtes skyline, et même dans la géométrie computationnelle. Maîtriser cela vous donne un outil pour de nombreux défis de codage du monde réel.

Bon codage, et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit