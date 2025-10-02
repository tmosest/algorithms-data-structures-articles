---
titre: LeetCode 2144. Coût minimum d'achat de bonbons avec rabais -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2144. Coût minimum d'achat de bonbons avec rabais
> **Easy** – LeetCode

**Langues** – Java, C++, Python

> Ce billet vous donnera trois solutions prêtes à la production, une plongée profonde dans l'algorithme, et une écriture de style blog optimisé SEO qui peut vous aider à décrocher votre prochaine entrevue d'ingénierie logicielle.

---

- Oui. 1. Aperçu du problème

> Une boutique gère une promotion gratuite.
> Pour les deux bonbons que vous payez, vous pouvez choisir un troisième bonbon * dont le coût est ≤ le moins cher des deux bonbons payés* et obtenir gratuitement.
>
> Compte tenu du "coût" des prix de toutes les bonbons, retourner le **coût total minimum** nécessaire pour acquérir tous les bonbons.

Obstacles

Valeur des contraintes
C'est pas vrai.
"1 ≤ longueur du coût ≤ 100"
Coût [i] ≤ 100

---

- Oui. 2. Principales perspectives

La promotion est essentiellement un **greedy, prendre le moins cher possible des bonbons gratuits**.
Si nous trions toutes les bonbons dans l'ordre ** non décroissant**, alors:

- Oui. Le **plus cher** bonbon doit toujours être payé pour (vous ne pouvez jamais obtenir gratuitement parce qu'il n'y a pas de bonbon moins cher pour satisfaire l'état de ..
- Oui. Le **seconde le plus cher** bonbon doit également être payé pour (il n'y a pas de bonbon moins cher que celui qui peut être pris gratuitement tout en obéissant à la règle).
- Oui. Le **troisième le plus cher** bonbon devient *libre* – il sera toujours le moins cher parmi les trois plus chers, parce qu'il se trouve exactement à la position "Troisième le plus important".

En répétant ce modèle de la fin la plus chère, nous obtenons une stratégie optimale:
> **Payez pour les deux bonbons restants les plus chers, sautez la troisième comme libre, et répétez. **

En termes d'indices (après triage ascendant), les bonbons qui sont *free* sont ceux dont l'indice satisfait
«(n – i) % 3] 0` où `n` est le nombre total de bonbons et `i` est l'indice 0.
Tous les autres contribuent au coût total.

---

- Oui. 3. L'algorithme

1. **Trier** le tableau `coût` en ordre ascendant.
2. **Itérer** à travers le tableau trié et calculer les prix de toutes les bonbons qui sont *non* libres.
*Les bonbons gratuits* sont ceux des indices où `(n - i) % 3 == 0`.
3. **Retour** la somme calculée.

L'algorithme est **O(n log n)** en raison du tri, et **O(1)** espace auxiliaire (à l'exclusion de l'espace utilisé par la routine de tri).

---

- Oui. 4. Mise en œuvre du code

#### 4.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
Int minimum public Coût(int[]) {
Tableaux.sort(coût); // O(n log n)
= 0;
n = coût/longueur;

pour (int i = 0; i < n; i++) {
// Si (n - i) % 3 == 0 → bonbons gratuits
si (n - i) % 3 != 0) {
Coût total +=[i];
}
}
le total des retours;
}
}
«» "

### 4.2 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimum Coût(vecteur<int>& coût) {
(cost.begin(), cost.end()); // O(n log n)
int n = coût.size(), ans = 0;
pour (int i = 0; i < n; ++i) {
si (n - i) % 3 != 0) ans += coût[i];
}
le retour des an;
}
};
«» "

### 4.3 Python

'`python
Solution de classe:
def minimum Coût(même, coût: Liste[int]) -> Int:
Coût.sort() # O(n log n)
n = len(coût)
somme de retour(cost[i] pour i dans l'intervalle(n) si (n - i) % 3 != 0)
«» "

> **Astuce** – Les trois extraits reposent sur le même calcul : les bonbons gratuits sont tous les trois à la fin. Cela maintient le code court, lisible et rapide.

---

- Oui. 5. Ce qui fonctionne – Le bien

* **Greedy & Simple** – La solution suit une stratégie intuitive de prise de bonbons gratuits le moins cher qui peut être prouvée optimale par l'échange argument.
* ** Faible complexité** – Un seul type est requis, pas de DP ou de récursion.
* **Language-agnostique** – Le même motif O(n log n) fonctionne en Java, C++, Python, et beaucoup d'autres langues.
* **Readability** – Condition de boucle claire `(n - i) % 3 != 0' communique instantanément la règle de la gratuité.

---

- Oui. 6. Ce qu'il faut regarder – La mauvaise

Comment éviter
- Oui.
Erreurs hors-par-un** Autres
**Les plus grandes entrées**= Même si `n ≤ 100`, l'algorithme s'élève à des millions; gardez le tri stable. Autres
**Confusion arithmétique modulaire**= Pensez aux bonbons libres comme tous les trois éléments *de la droite*, pas de la gauche. Autres

---

- Oui. 7. Erreurs courantes et débogage

Erreurs Symptômes Correction
C'est pas vrai.
Utiliser `i % 3 == 0` au lieu de `(n - i) % 3`= Mauvaises bonbons libres (première, quatrième, ...)= 0)»
Autres Sauter les deux derniers éléments lorsque `n % 3 == 1'=" Manque d'un bon marché" Utilisez l'état général, pas une boucle codée dur. Autres
Autres Ne pas trier les bonbons aléatoires sans tri Toujours trier avant d'appliquer la règle. Autres

---

- Oui. 8. Extensions et variantes

Variante Quels changements ? Autres
C'est quoi ?
**Acheter `k`, obtenir `m` gratuitement**. Autres
**Différente règle de libre-candy (-) (-)**.Ajustez l'inégalité, mais le modèle avide reste. Autres
**Grande entrée (n jusqu'à 105)**= Utiliser le tri de comptage ou le tri de radix si `cost[i]` ≤ 106 pour le temps O(n). Autres

---

- Oui. 9. Article de blog optimisé SEO

> **Titre:** *Master LeetCode 2144 – minimum Coût d'achat de bonbons avec rabais*
> **Meta Description:** *Apprenez la solution O(n log n) gourmande pour LeetCode 2144, consultez les implémentations Java, C++ et Python, et obtenez des conseils pour l'interview. *

Introduction

Le problème "Acheter deux, obtenir un problème gratuit est un défi classique LeetCode qui teste votre capacité à combiner tri avec une stratégie gourmande. Malgré sa note facile de difficulté, de nombreux candidats trébuchent sur la subtile condition de la moins chère des deux bonbons payés. Dans ce post, nous allons parcourir la solution optimale, fournir des extraits de code clairs en Java, C++ et Python, et disséquer pourquoi l'approche avide fonctionne. À la fin, vous serez prêt à accepter ce problème lors de votre prochain entretien technique.

### Déclaration de problème

(Insérer la description du problème dès le début de cet article.)

- Oui. Pourquoi Greedy fonctionne

(Expliquez l'argument d'échange : toute solution optimale peut être réordonnée pour que les bonbons les plus chers soient payés, le deuxième plus cher est payé, et le troisième est gratuit, etc.)

Balade de l'algorithme

(Détailler les étapes: trier → itérer → somme sauf un tiers de la fin.)

Extraits de code

(Insérer les codes Java, C++, Python comme indiqué ci-dessus.)

### Complexité temporelle et spatiale

(Exposer le temps O(n log n), espace O(1).)

Pièges communs

(Inclure la mauvaise table.)

Conclusion

(Rappelez-vous que la maîtrise de ce modèle aide avec de nombreuses variantes -buy‐X‐get‐Y‐free.)

Mots clés

*LeetCode 2144*, *coût minimum d'achat de bonbons*, *acheter deux obtenir un libre*, *algorithme de qualité*, *solution Java*, *solution C++*, *solution Python*, *préparation d'entrevue*, *conseils d'entrevue pour ingénieur logiciel*.

---

- Oui. 10. À emporter pour les demandeurs d'emploi

* **Showcase la solution dans l'interview** – Parler à travers la perspicacité gourmande, écrire le code sur le tableau blanc, et expliquer pourquoi le tri est la première étape optimale.
* **Extensions de peine** – Si l'intervieweur s'interroge sur les variations, soyez prêt à discuter de l'achat de "k", obtenez `m` gratuitement" ou des données à grande échelle.
* **Lisibilité lumineuse** – Une boucle concise comme `si (n - i) % 3 != 0)» est à la fois efficace et expressif.

Bonne chance, et que vos bonbons d'entrevue soient doux!