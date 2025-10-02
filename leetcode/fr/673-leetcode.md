---
titre: LeetCode 673. Nombre de subséquences croissantes les plus longues -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## **LeetCode 673 – Nombre de séquences ascendantes les plus longues* *
### Une plongée profonde dans le bon, le mauvais, et l'Ugly de LIS Compter
* (Java-Python C++) – Avec un article de blog convivial pour vous aider à atterrir cette interview*

---

Résumé du problème

> **LeetCode 673 – Nombre de subséquences croissantes les plus longues* *
> **Difficulté:** Moyenne
> **Signature de fonction (Java):** "nombre de trouvailles publiquesOfLIS(int[] nums);"

> Compte tenu d'un tableau entier "nums", retourner le nombre ** de sous-séquences les plus longs en forte augmentation**.
> Un *subséquence* est une séquence qui peut être dérivée du tableau en supprimant certains ou aucun élément sans changer l'ordre des éléments restants.
>
> **Exemples**
> ```texte
> Entrée: [1,3,5,4,7] Produit: 2
> Explication : Les deux LIS sont [1,3,4,7] et [1,3,5,7].
>
> Produit: 5
> Explication : La plus longue longueur LIS est 1, et chaque élément est un LIS.
> `` "
> **Constraints**
> - 1 ≤ longueur nominale ≤ 2000
> –106 ≤ nums[i] ≤ 106
> La réponse correspond à un entier de 32 bits.

---

Pourquoi ce problème est une question d'entrevue *classique*

* **Programme dynamique** – vous apprenez comment garder l'état (tableaux `dp` + `count`).
* **Manipulation des cas d'Edge** – nombres dupliqués, séquences décroissantes, tableaux tous égaux.
* ** compromis entre le temps et l'espace** – solutions O(n2) et solutions O(n log n) potentielles pour la longueur du SIL seulement.

---

Le bien – Simple, clair et correct

Pourquoi il est grand
- Oui.
**Deux tableaux** "dp" et "count"" conservent la longueur et *compte* de LIS se terminant à chaque indice. Autres
**O(n2) temps**=20002 = 4 millions d'itérations – facilement sous 0,1 s en Java/Python/C++. Autres
**Simple passe pour le résultat** où `dp[i]= maxLen`.
Autres **Aucune bibliothèque externe** STL – facile à copier dans les entrevues. Autres

---

## Le "Bad" – Performance et scalabilité

Pourquoi ça compte ?
- C'est pas vrai.
**Temps quadriennal**= Pour `n = 2000`, les contraintes plus importantes (par exemple `n = 105`) se briseraient. Autres
**Cache-inefficient boucle intérieure**= Chaque `i` boucles sur toutes les `j` précédentes, provoquant de nombreux accès à la mémoire. Autres
Autres Même si nous avons déjà trouvé un LIS plus long, nous comparons toujours tous les éléments précédents. Autres

> *Astuce:* Si vous avez affaire à `n > 5000`, considérez une approche de clivage-et-conquer ou segment-tree, mais pour LeetCode il est inutile.

---

## -Le code « Ugly » – Quirks de l'Edge-Case et dur à lire

1. ** Erreurs hors pair** – initialisation de `dp`/`count` à `1` pour chaque indice.
2. **Débordement entier** – pas un problème ici parce que le résultat correspond à 32 bits, mais soyez prudent lors du comptage de très grands subséquences.
3. **Mise à jour en place** – le mélange des mises à jour `dp[i]` à l'intérieur de la boucle intérieure peut conduire à des bogues subtils s'ils ne sont pas traités avec soin.
4. **Peu de commentaires** – de nombreuses solutions sur LeetCode sautent les commentaires explicatifs, ce qui rend difficile à comprendre pour les nouveaux arrivants.

> *Solution:* Ajouter une petite fonction d'aide qui retourne le maximum de deux entiers, ou utiliser `Math.max()` dans Java / `max()` dans Python / `std::max()` dans C++ pour garder le code propre.

---

Mise en œuvre du code

C'est pas vrai. Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public int findNumberOfLIS(int[] nums) {
int n = longueur nums;
si (n) 0) retour 0;

int[] dp = nouvelle int[n]; // LIS longueur se terminant à i
nombre int[] = nouveau nombre int[n]; // Nombre de LIS de cette longueur se terminant à i
les tableaux.fill(dp, 1);
les tableaux.fill(compte, 1);

int maxLen = 1;

pour (int i = 1; i < n; i++) {
pour (int j = 0; j < i; j++) {
si (nombres[i] > nombres[j]) {
si (dp[j] + 1 > dp[i]) {
dp[i] = dp[j] + 1;
nombre[i] = nombre[j];
} sinon si (dp[j] + 1 == dp[i]) {
nombre[i] += nombre[j];
}
}
}
maxLen = Math.max(maxLen, dp[i]);
}

résultat int = 0;
pour (int i = 0; i < n; i++) {
si (dp[i] == maxLen) résultat += count[i];
}
le résultat du retour;
}
}
«» "

---

# # # # # #

'`python
de taper l'importation Liste

Solution de classe:
def findNumberOfLIS(self, nombres: List[int]) -> Int:
n = len(nums)
si n] 0: retour 0

dp = [1] * n # LIS longueur se terminant à i
nombre = [1] * n # Nombre de LIS de cette longueur se terminant à i
max_len = 1

pour i dans la plage (1, n):
pour j dans la plage i:
si nombres[i] > nombres[j]:
si dp[j] + 1 > dp[i]:
dp[i] = dp[j] + 1
nombre[i] = nombre[j]
élif dp[j] + 1 == dp[i]:
nombre[i] += nombre[j]
max_len = max(max_len, dp[i])

somme de retour (cnt pour d, cnt dans zip(dp, nombre) si d == max_len)
«» "

---

C'est vrai. C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int findNumberOfLIS(std::vector<int>& nums) {
int n = nombres.size();
si (n) 0) retour 0;

std::vector<int> dp(n, 1); // LIS longueur se terminant à i
std::vector<int> cnt(n, 1); // Nombre de LIS se terminant à i
int maxLen = 1;

pour (int i = 1; i < n; ++i) {
pour (int j = 0; j < i; ++j) {
si (nombres[i] > nombres[j]) {
si (dp[j] + 1 > dp[i]) {
dp[i] = dp[j] + 1;
cnt[i] = cnt[j];
} sinon si (dp[j] + 1 == dp[i]) {
cnt[i] += cnt[j];
}
}
}
maxLen = md:max(maxLen, dp[i]);
}

résultat int = 0;
pour (int i = 0; i < n; ++i)
si (dp[i] == maxLen) résultat += cnt[i];
le résultat du retour;
}
};
«» "

---

Analyse de complexité

**Heure**
C'est le cas.
**DP (O(n2))**"O(n2)" – 4 millions de comparaisons pour "n = 2000". Autres

> *Pourquoi O(n2) est très bien :* LeetCodeS test suite caps `n` à 2000, rendant la solution confortablement rapide pour toutes les entrées.
> * Amélioration potentielle :* Si vous avez seulement besoin de la longueur LIS, vous pouvez obtenir `O(n log n)` avec le tri de patience. Cependant, le comptage du nombre de LIS nécessite intrinsèquement d'explorer toutes les combinaisons, ce qui nous ramène au temps quadratique à moins d'utiliser des structures de données plus avancées (fibre de Fenwick + compression de coordonnées) et de manipuler soigneusement les duplications.

---

Comment cela vous aide à trouver un emploi

1. **Interview : Ce problème est fréquemment posé dans les interviews techniques (Google, Amazon, Facebook, etc.). Connaître la solution DP classique montre que vous pouvez résoudre des problèmes de programmation dynamiques sous la pression du temps.
2. **Code d'affichage propre** – Les trois implémentations sont concises, bien commentées et idiomatiques pour chaque langue. Les intervieweurs apprécient la lisibilité du code.
3. **Traitement des affaires** – La solution gère correctement les tableaux d'éléments égaux, les tableaux qui diminuent strictement et la taille maximale d'entrée – un test subtil de robustesse.
4. **Discussion de complexité** – Soyez prêt à expliquer pourquoi `O(n2)` est acceptable pour ce problème et comment vous optimiseriez pour des contraintes plus grandes.

---

Article sur le blog optimisé du SEO

> **Titre (=60 caractères)* *
> `Nombre de subséquences croissantes les plus longues (LeetCode 673) – Solution DP en Java, Python, C++ "
>
> **Meta Description (155 caractères)* *
> `Apprendre à résoudre LeetCode 673 – Nombre de subséquences les plus longues. Comprendre l'approche DP, le code en Java/Python/C++ et les conseils d'entrevue. "
>
> **Mots-clés cibles* *
> - LeetCode 673
> - Nombre de subséquences les plus longues
> - Solution LIS DP
> - Entretien de programmation dynamique
> - Problème d'entrevue de codage
> - Solution Java LIS
> - Algorithme Python LIS
> - C++ Nombre LIS
>
> **H1** – « Nombre de subséquences croissantes les plus longues (Code de cap 673) : Guide complet du PDD "
>
> **H2 Sections**
> 1. Aperçu du problème
> 2. Pourquoi ce problème compte dans les entrevues
> 3. Le «bien» – simple O(n2) DP
> 4. Les cas de retard – Quadratic Time & Edge
> 5. Les pièges communs dans le code mondial réel
> 6. Mise en œuvre Java
> 6.1. Passage du code
> 6.2. Pièges et correctifs Java communs
> 7. Mise en œuvre de Python
> 7.1. Passage du code
> 8. Mise en œuvre C++
> 9. Discussion sur la complexité
> 10. Conseils d'entrevue et points de discussion
> 11. Conclusion et lecture supplémentaire

> **Images et blocs de code** – Inclure des blocs de code syntaxiques. Utilisez une image avec un texte alt: `Code Java pour LeetCode 673 LIS DP`.

> ** Liens internes/externes* *
> - Lien vers la page de problème LeetCode.
> - Lien avec des problèmes de PDD connexes (p. ex., `Longueur maximale de l'augmentation de la subséquence`).
>
> **Score de lisibilité** – Objectif pour la classe Flesch–Kincaid 8. Gardez les phrases courtes et utilisez des listes de balles.

> **Call‐to‐Action** – Encourager les lecteurs à cloner la repo sur GitHub (`/solutions/leetcode-673`) et à pratiquer sur la section LeetCode.

> ** Extraits de médias sociaux**
* - " Master LeetCode 673 – Nombre de subséquences croissantes les plus longues! O(n2) DP + code en Java, Python, C++. Entretien prêt ! #Code de leet #DP'
> - `Amants de programmation dynamique, c'est pour vous : résolvez le comptage LIS en 3 langues. Regardez le code ! #CodageInterview #LeetCode673 "

> **Schema.org JSON‐LD** – Ajouter un schéma `BlogPosting` avec les métadonnées ci-dessus pour aider les moteurs de recherche à indexer votre article.

---

À emporter

*LeetCode 673 est un mélange parfait de programmation dynamique, de nuance et de pertinence d'entrevue. Le classique "O(n2)" La solution DP est à la fois **correcte** et **efficace** pour les contraintes. Les trois implémentations linguistiques ci-dessus illustrent des pratiques de codage propres qui impressionnent les gestionnaires d'embauche. *

> ** Prochaines étapes :**
> - Essayez de modifier la solution pour utiliser des entiers 64 bits ("long" en C++/Java "long") et testez sur de grands tableaux aléatoires.
> - Explorez une approche `Fenwick tree + coordinator compression` si vous voulez vous défier davantage.

Bon codage, et bonne chance dans votre prochaine interview! C'est ce qu'il a dit.

---



---

*Préparé par un ingénieur de l'algorithme. Tous les codes sont soigneusement testés dans un environnement hors ligne et prêts pour votre prochaine entrevue. *