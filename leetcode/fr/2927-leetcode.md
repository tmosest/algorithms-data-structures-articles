---
titre: LeetCode 2927. Distribuer des bonbons aux enfants III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2927 – Distribuer des bonbons aux enfants III
LeetCode O(1) combinatoire**

> **Problème**
> Compte tenu de deux nombres entiers positifs `n` et `limit`, retourner le nombre de moyens de distribuer `n` les bonbons parmi **trois** enfants afin qu'aucun enfant ne reçoive plus que `limit` les bonbons.
>
> **Exemples**
> ```texte
> n = 5, limite = 2 → 3 (1,2,2), (2,1,2), (2,2,1)
> n = 3, limite = 3 → 10 (tous les 10 triples non-négatifs se résument à 3)
> `` "
>
> **Constraints**
> 1 ≤ n, limite ≤ 108

---

### Pourquoi ce problème est une question d'entrevue

* **Mathématiques pures + programmation** – Pas de structures de données, seulement combinatoires.
* **Scales aux grandes entrées** – Nécessite une solution à temps constant.
* **Elégante utilisation de l'inclusion-exclusion** – Une technique classique avec laquelle chaque ingénieur senior devrait être à l'aise.

---

- Oui. La mauvaise partie

* Les contraintes (108) vous obligent à penser au débordement entier et à l'arithmétique 64 bits.
* Si vous oubliez que `C(x, 2)` est zéro quand `x < 2`, vous obtiendrez des résultats négatifs.

---

La mauvaise partie

* La formule finale a beaucoup d'offsets (comme `limit+1`) qui sont faciles à glisser.
* Une seule typo dans le terme combinatoire peut transformer la solution de corriger à sauvagement mal.

---

## Intuition – Des étoiles et des barres à l'inclusion – Exclusion

Sans limite supérieure, le nombre de triples entiers non négatifs `(a,b,c)` avec `a+b+c = n` est le résultat classique *stars & bars*:

«» "
T = C(n + 2, 2) // choisir 2 séparateurs entre n+2 positions
«» "

La difficulté est la "limite" ** supérieure**.
Nous devons supprimer tous les triples où au moins un enfant reçoit plus de «limite».
La manière la plus simple est l'inclusion – exclusion (EIP) :

«» "
réponse = T
– 3 * (# solutions avec une limite)
+ 3 * (# solutions avec une limite ET b > limite)
– (# solutions avec une limite ET b > limite ET c > limite)
«» "

Pourquoi 3 et pourquoi +3 ?
* Il y a 3 enfants symétriques pour la première soustraction.
* Il y a 3 paires non commandées pour la deuxième addition.
* Une seule façon de dépasser les trois.

---

Calcul de chaque PIE Durée

Définir

«» "
C2(x) = x*(x-1)/2 si x >= 2
0 sinon
«» "

- Oui. 1. Tous les triples (sans lien)

«» "
T = C2(n + 2)
«» "

- Oui. 2. Un enfant dépasse la limite

Laisser `a' = a - (limite+1) ≥ 0`.
Puis `a' + b + c = n - (limite+1)`.
Nombre de solutions:

«» "
t1 = C2( n - limite + 1 )
«» "

(Si `n - limite + 1 < 2`, le terme est 0.)

- Oui. 3. Deux enfants dépassent la limite

Let `a' = a - (limite+1)`, `b' = b - (limite+1)`.
Puis `a' + b' + c = n - 2*(limite+1)` → `n - 2*limite - 2`.
Nombre de solutions:

«» "
t2 = C2( n - 2* limite )
«» "

- Oui. 4. Les trois enfants dépassent la limite

Que tout soit décalé: `a' + b' + c' = n - 3*(limite+1)` → `n - 3*limite - 3`.
Nombre de solutions:

«» "
t3 = C2( n - 3* limite - 1 )
«» "

---

## Finale Fermée- Formule

«» "
réponse = C2(n + 2)
– 3 * C2(n - limite + 1)
+ 3 * C2(n - 2* limite)
– C2(n - 3* limite - 1)
«» "

Toutes les valeurs intermédiaires correspondent à des entiers signés 64 bits parce que
`n ≤ 108` → le plus grand binôme `C(n+2,2)`

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Calculer 4 binomiaux **O(1)**

La solution est à temps constant et à espace constant – parfait pour les limites données.

---

## Mise en œuvre du code

Vous trouverez ci-dessous des solutions prêtes à coller dans **Java**, **Python** et **C++**.
Tous utilisent l'arithmétique 64 bits (`long` / `int64_t`).

---

Python 3

'`python
Solution de classe:
def distribuer Candies (self, n: int, limite: int) -> Int:
# aide: C(x, 2) (0 si x < 2)
def C2(x: int) -> Int:
retour x * (x - 1) // 2 si x >= 2 autres 0

Total = C2(n + 2)
t1 = C2(n - limite + 1) # un enfant > limite
t2 = C2(n - 2 * limite) # deux enfants > limite
t3 = C2(n - 3 * limite - 1) # les trois > limite

total de retour - 3 * t1 + 3 * t2 - t3
«» "

---

#### Java 17

"Java
solution de classe {
C2 (long x) {
retour (x >= 2) ? (x * (x - 1) / 2) : 0;
}

publique longue diffusion Boîte(int n, limite int) {
total long = C2((long) n + 2);
long t1 = C2(long) n - limite + 1); // un enfant > limite
long t2 = C2(long) n - 2L * limite); // deux enfants > limite
long t3 = C2(long) n - 3L * limite - 1);

total de retour - 3 * t1 + 3 * t2 - t3;
}
}
«» "

---

C++17

'`cpp
solution de classe {
long long C2(long long x) {
retour (x >= 2) ? (x * (x - 1) / 2) : 0;
}
public:
longue distribution Boîte(int n, limite int) {
long total = C2(static_cast<long long>(n) + 2);
long t1 = C2(static_cast<long long>(n) - limite + 1); // une > limite
long t2 = C2(static_cast<long long>(n) - limite 2LL *); // limite 2 >
long t3 = C2(static_cast<long long>(n) - 3LL * limite - 1); // tous > limite

total de retour - 3 * t1 + 3 * t2 - t3;
}
};
«» "

---

- Oui. Comment tester

Texte
Entrée: n = 5, limite = 2
Produit : 3

Entrée: n = 3, limite = 3
Produit : 10

Entrée: n = 1, limite = 1
Produit : 3 ( (1,0,0), (0,1,0), (0,0,1) )
«» "

N'hésitez pas à les brancher sur le LeetCode.

---

## Conseils à emporter pour votre prochaine entrevue de codage

1. **Rechercher des raccourcis combinatoires** – `stars & bars` donne presque toujours une formule `C(n+2, 2)`.
2. **Utilisez Inclusion–Exclusion pour les limites supérieures** – c'est un liner unique une fois que vous écrivez l'aide `C2`.
3. **Guard contre le débordement** – toujours moulé à 64 bits avant la multiplication.
4. **Valider la formule sur les cas limites** (`n` ≤ `limite`, `n` > 3*`limite`) pour attraper les bugs.

---

Référence Mots clés

- Distribuer des bonbons aux enfants "
- `code de transport 2927 "
- `O(1) solution combinatoire "
- Entretien sur l'exclusion d'inclusion "
- "Codage des conseils d'entretien "
- `algorithme d'entretien d'emploi "
- `c++ leetcode java python "

---

Codage heureux – que cette solution propre, O(1) vous débarque le travail que vous êtes après!