---
titre: LeetCode 829. Nombres consécutifs Somme -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code Leet 829 – Somme des nombres consécutifs
> Combien de façons pouvez-vous écrire un entier n comme la somme des entiers positifs consécutifs?**

Ce problème est un *Hard* sur LeetCode mais il peut être fissuré avec un seul aperçu mathématique.
Ci-dessous vous trouverez des solutions propres et prêtes à la production dans **Java**, **Python** et **C++**, suivi d'un article de blog complet qui explique l'astuce, les pièges et comment utiliser cette connaissance pour impressionner les recruteurs.

---

Aperçu de la solution

La somme des entiers consécutifs `k` commençant par `x` est

«» "
x + (x+1) + ... + (x+k-1) = k·x + k(k-1)/2
«» "

Nous voulons que cela soit égal à "n". Ainsi

«» "
k·x = n – k(k-1)/2
«» "

* `x` doit être un entier ** positif** → RHS > 0
* `k` doit être un entier positif

La boucle liée provient de l'inégalité `n > k(k-1)/2` → `k < sqrt(2n)`.
La vérification *seulement* nécessaire dans la boucle est de savoir si `n – k(k-1)/2` est divisible par `k`.

Cela donne un algorithme de temps **O( √n)** avec un espace **O(1)**.

---

Code – 3 langues

Code de la langue
C'est quoi, ça ?
NombresSum(int n) { <br> int count = 0; <br> pour (int k = 1; k * k < 2L * n; k++) { <br> int rhs = n - k * (k - 1) / 2; <br> si (rhs <= 0) pause; <br> si (rhs % k) 0) nombre++; <br> } <br> nombre de retours; <br> } <br>} ``
*Python *Python *Python <br>Solution de classe: <br> NombresSum(self, n: int) -> int: <br> count = 0 <br> k = 1 <br> alors que k * k < 2 * n: <br> rhs = n - k * (k - 1) // 2 <br> if rhs <= 0: <br> break <br> if rhs % k == 0: <br> count += 1 <br> k += 1 <br> count ``"
{ <br>public: <br> int consécutiveNumbersSum(int n) { <br> int count = 0; <br> pour (long long k = 1; k * k < 2LL * n; ++k) { <br> long rhs = n - k * (k - 1) / 2; <br> si (rhs <= 0) break; <br> si (rhs % k). 0) ++compte; <br> } <br> compte de retour; <br> } <br>}; ``

> **Pourquoi "long" en C++? **
> `k * k` peut déborder `int` lorsque `n` approche `10^9`. L'utilisation d'une longue durée nous protège.

---

Article du blog – Le bon, le mauvais, le mauvais

> **Titre:**
> Nombres consécutifs Somme – Un problème de code de leet dur résolu dans O( √n) (Java, Python, C++)* *
> **Meta Description:**
> Apprenez à casser le LeetCode 829 en quelques minutes. Obtenez des solutions Java, Python et C++, une explication approfondie, des pièges communs et des conseils prêts à l'entrevue. (en milliers de dollars)

---

Introduction

LeetCodeS **829 – Somme Consécutive Nombres** est un problème fallacieux. Il apparaît dans de nombreuses listes de prép d'entrevue parce qu'il teste la capacité d'un candidat à combiner *mathe* avec *pensée algorithmique*.
Dans cet article, nous allons:

1. Déterminez le calcul derrière la solution.
2. Fournir un code de qualité de production propre en Java, Python et C++.
3. Discutez des parties *bon*, *mauvais* et *doucement* des approches typiques.
4. Expliquez comment encadrer ce problème dans une entrevue pour obtenir ce travail.

---

C'est pas vrai. Le bon – Un trick de mathématiques à un liner

La beauté réside dans la reconnaissance que chaque *séquence longueur* `k` donne ** tout au plus** commençant entier `x`.
L'équation de base

«» "
k·x + k(k-1)/2 = n → k·x = n – k(k-1)/2
«» "

D'ici :

* `x` doit être positif → `n > k(k-1)/2`.
* La boucle liée devient `k < sqrt(2n)`.
* Le seul essai: `(n – k(k-1)/2) % k == 0`.

Tout cela est **O( √n)**, beaucoup plus rapide que la force brute.

---

C'est vrai. Les mauvais – les pièges de la force brute

Beaucoup essaient de simuler tous les points de départ :

'`python
pour commencer dans la plage(1, n):
somme = 0
longueur = 0
alors que la somme < n:
somme += début + longueur
longueur += 1
si somme == n:
nombre += 1
«» "

* **Temps:** O(n2) – impossible pour n = 109.
* **Espace:** trivial, mais le nombre de boucles est astronomiquement élevé.
* ** Maintenabilité :** Difficile à raisonner sur la justesse.

L'approche de la force brute se transforme rapidement en un cauchemar** sur LeetCode et est un drapeau rouge pour les recruteurs.

---

C'est vrai. L'Ugly – Sur-Ingénierie avec les structures de données

Certaines solutions tentent de précalculer tous les numéros triangulaires ou d'utiliser des cartes de hachage :

"Java
Définir <integer> triangulaire = nouveau HashSet<>();
pour (int k = 1; k < Math.sqrt(2*n); k++) {
l'alinéa a) est remplacé par le texte suivant:
}
«» "

* Ajoute une mémoire superflue.
* Complexité reste O( √n) mais les facteurs constants soufflent.
* Pas aussi lisible pour les intervieweurs.

À emporter : * Restez simple. Une seule boucle avec un contrôle de division bat un ensemble ou une carte dans la clarté et la vitesse.

---

C'est pas vrai. Interview-Ready Narrative

J'ai résolu LeetCode 829 en observant d'abord que chaque longueur de nombres consécutifs donne au plus une séquence valide. J'ai dérivé la formule `k·x + k(k-1)/2 = n`, délimité k par `sqrt(2n)`, puis seulement vérifié la disvisibilité. Cela donne un algorithme O( √n), qui fonctionne en millisecondes pour `n = 109`. Je l'ai implémenté proprement en Java, Python et C++. *

Les recruteurs de points clés aiment :

* **Perspective mathématique** – montre que vous pouvez transformer un problème en équations.
* **Conscience de la complexité** – vous savez pourquoi O( √n) est rapide.
* ** Compétence en langage brut** – vous pouvez coder dans la pile qu'ils utilisent.
* **Code propre** – pas de magie, pas de suringénierie.

---

####5-SEO-Aimely Highlights

Mot-clé
C'est quoi ?
Titre, introduction, exemples
Consécutive Nombres Sum.
Autres Java, Python, C++.
Difficile à résoudre
Description de la méta, conclusion
Algorithme O( √n)

> **Rappelez-vous:** Google aime le contenu structuré. Utilisez les balises H2/H3, les listes de balles et les clôtures de code. L'article ci-dessus suit déjà cette structure.

---

- Oui. Réflexions finales

- **Gardez le devant et le centre des mathématiques. **
- **Trim boucles à la limite minimale. **
- **Éviter les structures de données inutiles. **
- ** Expliquez clairement votre logique dans les interviews. **

En maîtrisant LeetCode 829, vous démontrerez un puissant mélange de pensée analytique et de codage pratique – exactement ce que les gestionnaires d'embauche recherchent.

---

Bonus – Cas d'essai

Résultats attendus Explication
- Oui.
2+3, 5 (numéro unique)
Pour plus d'information, veuillez lire la description anglaise.
1+2+3+4+5, 15
Il s'agit de 1
100000000?Utilisez < 1 ms sur Java

---

### -Envelopper

Vous avez maintenant :

* **Trois solutions prêtes à la production** (Java, Python, C++).
* Un article de **blog** qui explique l'astuce, les pièges et le cadre d'entrevue.
* Une écriture **optimisée** qui sera bien classée pour les recherches de chercheurs d'emploi.

Bon codage et bonne chance pour votre prochaine interview!