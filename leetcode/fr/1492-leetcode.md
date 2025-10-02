---
titre: LeetCode 1492. Le facteur kth de n -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Le facteur K du **n** – LeetCode 1492
**Une plongée profonde, des solutions de code en Java / Python / C++ & un article de blog prêt à travailler**

> **TL;DR** – Trouvez le *k*-ième plus petit diviseur d'un nombre *n*.
> Complexité : **O( √n)** (bien mieux que le scan naïf O(n)).
> Langues: Java, Python, C++.
> Sections de blog: le bon, le mauvais, le laid.
> Mots clés du référencement : * facteur kth de n, LeetCode 1492, entretien de codage, algorithme, solution O( √n), prép d'entrevue*.

---

Table des matières

Lien
- Oui.
Récapitulation des problèmes
Brute-Force vs Optimisé
Solution O( √n) #3-o √n-solution Autres
Code en Java Autres
Code dans Python
Code en C++ Autres
#7-the-good
Le mal #8-le mal
Le voyou #9-le voyou
Conseils pour l'entrevue
Références

---

Récapitulation des problèmes

> **LeetCode 1492 – Le facteur k de *n***
> **Don** deux entiers positifs `n` et `k`, retournez le facteur le plus petit *k*-th de `n`.
> Si `n` a moins de facteurs `k`, retourner `-1`.

> **Exemples**
> 1. `n = 12, k = 3` → facteurs `[1, 2, 3, 4, 6, 12]` → réponse `3`.
> 2. `n = 7, k = 2` → facteurs `[1, 7]` → répondre `7`.
> 3. `n = 4, k = 4` → seulement `[1, 2, 4]` → répondre `-1`.

> **Constraints**
> «1 ≤ k ≤ n ≤ 1000».

> **Suivi**: Résolvez en *inférieur à* "O(n)".

---

C'est un coup monté. Force vs optimisée

L'approche Temps L'espace Commentaires
C'est pas vrai.
**Brute-Force** – itérer i = 1...n, collecter des facteurs. Autres
**O(============================================================================================================================================================================================================================================================= Autres

---

Solution

1. **Collecter la première moitié des diviseurs* *
Itérer `i` de `1` à ` √n`.
Si `i` divise `n`, ajouter `i` à une liste `smallDivs`.

2. ** Maintenez la deuxième moitié à la volée**
Si `k` ≤ `smallDivs.size()`, la réponse est `smallDivs[k-1]`.
Autrement, les autres facteurs sont `n / i` pour chaque diviseur `i` en ordre inverse.
Calculez combien nous sautons (`k - smallDivs.size()`) et retournez le bon.

3. **Retour -1 si nous manquons de diviseurs* *

> **Pourquoi O( √n)? * *
> Chaque diviseur `d` > √n paires avec un diviseur `n/d` < √n.
> Il suffit donc de vérifier jusqu'à √n pour découvrir *toutes* paires de facteurs.

---

Code en Java

"Java
***
* 1492. Le facteur k-th de n
* https://leetcode.com/problèmes/the-kth-factor-of-n/
*/
solution de classe {
publique Facteur(int n, int k) {
// Liste pour stocker les facteurs <= sqrt(n)
Liste<Intégrée> petite = nouvelle liste d'array<>();

limite int = (int) Math.sqrt(n);
pour (int i = 1; i <= limite; i++) {
Si (n % i] 0) {
petit.add(i);
}
}

// Si k est dans la liste des petits facteurs
si (k <= small.size()) {
retour small.get(k - 1);
}

// Les autres facteurs sont n / i pour i en ordre inverse
int restant = k - petite taille();
int total = n / limite; // nombre de facteurs importants
si (rester > total) retour -1; // pas assez de facteurs

// Obtenez le (le maintien)-ième facteur le plus important
// Exemple : petit = [1,2,3], restant = 1 -> nous voulons n/3
int idx = small.size() - restant; // index dans la petite liste
retour n / small.get(idx);
}

// Main rapide pour les tests locaux
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.kthFactor(12, 3)); // 3
Système.out.println(sol.kthFactor(7, 2)); // 7
Système.out.println(sol.kthFactor(4, 4)); // -1
}
}
«» "

> **Points clés**
> * `Math.sqrt` → double; moulé à int pour la limite de boucle.
> * Nous ne stockons que les "petits" diviseurs ; les *grands* sont dérivés paresseusement.
> * Complexité: temps `O( √n)`, espace `O( √n)` pour la liste des petits diviseurs.

---

Code en Python

'`python
# 1492. Le facteur k-th de n
# Python 3

Solution de classe:
def kthFactor(self, n: int, k: int) -> Int:
petite = []
limite = int(n ** 0,5)
pour i dans la fourchette(1, limite + 1):
Si n % i] 0:
petit.annexe i)

si k <= len(petit):
retour petit[k - 1]

restant = k - len(petit)
# Nombre de facteurs importants sont des diviseurs totaux moins les petits
total_large = (len(small) * 2) - (1 si limite * limite == n autre 0)
si restant > total_large - len(petit):
retour -1

# Indice dans la petite liste pour le grand diviseur requis
idx = len(petit) - restant
retour n // small[idx]

# Test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.kthFactor(12, 3)) # 3
print(sol.kthFactor(7, 2)) # 7
print(sol.kthFactor(4, 4)) # -1
«» "

> ** Touches pyroniques* *
> * Utiliser la compréhension de la liste pour `petit'.
> * Calculer "limite = int(n ** 0,5)".
> * Poignez les carrés parfaits correctement (`n == limite * limite`).

---

Code en C++

'`cpp
// 1492. Le facteur k-th de n
// C++17

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int kthFactor(int n, int k) {
vecteur<int> petits;
limite int = sqrt(n);
pour (int i = 1; i <= limite; ++i) {
Si (n % i] 0)
small.push_back(i);
}

si (k <= (int)small.size())
retour petit[k - 1];

int restant = k - petite taille();
// Nombre de grands diviseurs
Total Grande = (int)petite taille() * 2
- (limite * limite == n ? 1 : 0);

si (rester > totalGrand - (int)petit.size())
retour -1;

int idx = (int)small.size() - restant;
retour n / small[idx];
}
};

Int main() {
Solution sol;
<< sol.kthFactor(12, 3) << endl; // 3
<< sol.kthFactor(7, 2) << endl; // 7
Cout << sol.kthFactor(4, 4) << endl; // -1
retour 0;
}
«» "

> **C++ Faits saillants* *
> * `sqrt` retourne double; moulé à int.
> * Utilisez `vector<int>` pour les petits diviseurs.
> * Gardez le code compact mais lisible.

---

C'est pas vrai. Les bonnes

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Complexité optimale** – `O( √n)` est idéal pour les grands `n`. Autres
**Simplicité** – Une seule boucle jusqu'à √n; aucune structure de données lourde. Autres
**Space‐Efficace** – Stocks à tout le plus de entiers. Autres
**Readability** – Effacer les noms de variables (`small`, `remaining`). Autres
**Concordance linguistique – La même logique s'applique à Java, Python, C++. Autres

---

- Oui. Les mauvais

Ce qui se passe
C'est pas vrai.
**Brute-Force** – itérer à `n` peut être lent pour `n` jusqu'à 106 ou 109. Autres
** Liste inutile** – si vous n'avez besoin que du facteur k, le stockage de tous les petits diviseurs est excessif. Autres
**Cas Edge** – oublier le chèque carré parfait peut doubler le diviseur moyen. Autres
**Code Complexité** – la nidation "if/else" peut masquer la logique. Autres

---

C'est pas vrai. L'Ugly

> La solution *ugly* est souvent la première que vous écrivez:
> 1. **Loops codées en dur**
> 2. **Mix de boucles et récursion* *
> 3. **Pas de sortie anticipée**
> 4. **Noms des variables de mesure**

"Java
// Ugly Java
int[] f = nouveau tableau int[1000]; //
cnt = 0;
pour (int i = 1; i <= n; i++) {
Si (n % i] 0) {
f[cnt++] = i;
}
}
si (k <= cnt) retourner f[k - 1];
retour -1;
«» "

> Pourquoi c'est moche ?
> * Utilise un tableau de taille fixe au lieu d'une liste dynamique.
> * O(n) temps, loin d'être optimal.
> * Aucune manipulation de carrés parfaits.
> * Mauvaise désignation (`f`, `cnt`).

---

Conseils d'entrevue

1. **Clarifier le problème** – Demandez si `k` est basé sur 1 (oui, LeetCode utilise 1-based).
2. ** Expliquez l'appariement du diviseur** – `i` et `n/i`.
3. **La complexité de l'État en amont** – O( √n) est une victoire.
4. **Cas d'Edge** – carrés parfaits, `k` plus grands que les diviseurs totaux, `n == 1`.
5. **Par exemple, «n = 36», «k = 5».
6. **Mention une sortie nette** – retour `-1` tôt si impossible.
7. **Afficher le code** – le garder concis, tester avec les entrées d'échantillon.
8. **Discuss alternatives** – force brute, listes de facteurs précomputants, mémoisation pour les requêtes répétées.

> **Rappelez-vous :** Les intervieweurs apprécient *clarité* et *efficacité* plus que la performance brute. Une solution bien structurée avec de bons commentaires donnera une note élevée aux entrevues techniques.

---

Références

1. Problème de LeetCode 1492 – <https://leetcode.com/problems/the-kth-factor-of-n/>
2. Exemples de solutions de la communauté (diverses langues).
3. Éditorial officiel – factorisation O( √n).
4. Blogs de programmation concurrentiels sur le dénombrement des diviseurs.

---

Conclusion optimale du SEO

Le facteur *k-th de n* (LeetCode 1492) est un problème d'entrevue classique qui teste la compréhension de la symétrie des diviseurs, l'optimisation de la complexité et les pratiques de codage propres. La solution optimale `O( √n)` est simple, élégante et fonctionne pour de très grands nombres, ce qui en fait une grande vitrine dans votre portefeuille.

En partageant des extraits de code dans **Java, Python et C++**, vous démontrez la polyvalence linguistique – un plus pour les gestionnaires d'embauche. Le billet de blog qui l'accompagne couvre les aspects *good*, *bad* et *ugly* et fournit aux intervieweurs un récit clair et professionnel.

Prêt à accepter votre prochaine entrevue de codage ? Plongez dans le code, pratiquez les cas de bord, et gardez la logique propre. Bonne chance – vous avez ça! C'est ce qu'il a dit.

---