---
titre: LeetCode 3667. Trier les tableaux Par valeur absolue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3667 – Débarrassez-vous par valeur absolue
**LeetCode**

---

### TL;DR
> Réorganiser un tableau entier pour que les éléments soient triés en augmentant la valeur absolue.
> Toute commande qui satisfait à la condition est acceptable.

---

Déclaration de problème

On vous donne un tableau entier "nums" (1 ≤ nombres.longueur ≤ 100, –100 ≤ nombres[i] ≤ 100).
Retourner toute permutation de "nums" qui est **non-diminution par valeur absolue**.

> **Exemple**
> `nums = [3, -1, -4, 1, 5]` → `[-1, 1, 3, -4, 5]`
> (Les deux `[-1,1,3-4,5]` et `[1,-1,3,-4,5]` sont valables.)

---

Solutions simples et concises en trois langues

Ci-dessous sont propres, des extraits de production prêts qui résolvent le problème en **O(n log n)** temps en utilisant le langage des utilitaires de tri intégrés.

Code de la langue
C'est quoi, ça ?
*Java**
Importation de java.util.*;
importation statique java.lang. Math.abs;

solution de classe {
public int[] sortByAbsoluteValue(int[] nums) {
// Convertir en flux → encadré → trié par Math::abs → retour à int[]
retour Arrays.stream(nums)
.boxé()
.sorted(Comparator.comparingInt(Math::abs))
.mapToInt(entier::intValue)
.à Array();
}
}
«» Autres
*Python**
Solution de classe:
def tri ByAbsoluteValue(self, nombres: List[int]) -> Liste[int]:
# Le tri de Python utilise Timsort – stable, O(n log n)
retour trié(nums, key=abs)
«» Autres
*C++ *Cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> sortByAbsoluteValue(vecteur<int>& nums) {
sort(nums.begin(), nums.end(),
[](int a, int b){ retourner abs(a) < abs(b); });
les numéros de retour;
}
};
«» Autres

---

Analyse de complexité

Étapes Complexité Notes
- C'est quoi ?
Trier **O(n log n)** Autres
L'espace supplémentaire **O(n)** Autres
Coffrets de bord Aucun Poignées vides ou à simple élément gracieusement. Autres

> **Pourquoi O(n log n) est bien* *
> Avec *n* ≤ 100, toute approche O(n2) passerait également. Le tri maintient la solution courte, claire et évolutive pour les entrées plus importantes.

---

Alternative (Traitement de la compilation) – Quand vous avez besoin O(n)

Comme la plage de valeurs est minuscule (–100 à 100), vous pouvez trier en temps linéaire :

'`python
def sortByAbsoluteValue(nums):
seau = [[] pour _ dans l'intervalle (201) # 0 cartes à abs(0)
pour x en nombres:
seau[abs(x)] .appendice(x)
retour [x pour le groupe dans le seau pour x dans le groupe]
«» "

Ceci utilise **O(n)** temps et **O(1)** espace supplémentaire (201 seaux).
Utile pour les intervieweurs qui demandent : Pouvez-vous faire mieux que O(n log n) ? (en milliers de dollars)

---

Le bon, le mauvais, le mauvais

Aspect du bien
- C'est quoi ?
**Clarté**=Traitement intégré + lambda maintient le code court. La suroptimisation (dénombrement) peut cacher l'intention. Une mauvaise utilisation de `abs()` sur `Integer.MIN_VALUE` (Java) ou `LLONG_MIN` (C++) peut déborder. Autres
**Performance**= O(n log n) est suffisant pour les contraintes. Le tri peut être excessif pour les petits tableaux. Utiliser `Math.abs(Integer.MIN_VALUE)` déclenche `ArithmeticException` en Java. Autres
**Robustness**=Poignées négatives, positives, zéro sans couture.== Aucune.= Oublie d'importer `java.util.*` ou `static java.lang. Math.abs en Java. Autres

> ** À emporter :** La solution la plus simple et la plus durable gagne la plupart des entrevues. Plongez seulement dans des tours linéaires si vous le demandez explicitement.

---

Comment cela aide votre travail de chasse

1. **Breadth algorithmique** – Démontre la familiarité avec le tri, les fonctions lambda et les API de flux – les intervieweurs de compétences aiment.
2. **Codage des meilleures pratiques** – Le code propre, commenté et linguistique-idiomatique montre l'attention au détail.
3. **Narratif de résolution des problèmes** Dans votre entretien, marchez à travers l'objectif "bonne, mauvaise, laid" ; il met en valeur votre pensée critique.
4. **Conscience des cas** – La mention des risques de débordement reflète la conscience réelle de la production.

---

Article de blog optimisé du SEO

Titre
*Master LeetCode 3667: Tri Par valeur absolue – Java, Python, C++ Solutions + Conseils d'entretien**

Description de la méta
Résoudre le LeetCode 3667 par Valeur absolue en Java, Python et C++ avec un code clair, une analyse de complexité et des stratégies prêtes à l'entrevue. Boostez votre score d'entrevue de codage aujourd'hui!

Mots clés suggérés
- LeetCode 3667
- Triez le tableau Par valeur absolue
- Valeur absolue de tri Java
- Python trié par abs
- Tri de valeur absolue C++
- codage des algorithmes d'entretien
- questions sur le codage des entretiens d'emploi
- complexité des algorithmes

---

Aperçu du blog

Section du contenu
C'est pas vrai.
**Introduction**=Récapitulation succincte du problème + pourquoi cela compte dans les entrevues. Autres
**Déclaration de problème**=Exact contraintes, exemples, cas de bord. Autres
**Approche naïve** Autres
**Approche optimale**= Afficher les trois extraits concis; expliquer le comparateur/la « clé ». Autres
** Discussion sur la complexité** Autres
**Linear-time Comptage Tri**= Quand vous pouvez aller au-delà `O(n log n)`. Autres
**Bon, mauvais, mauvais** Autres
**Interview Angle**= Ce que recherchent les intervieweurs : clarté, manipulation de cas de bord, solutions alternatives. Autres
**Testing & Edge Cases** Autres
**Take‐away & Career Advice**= La maîtrise de ce curriculum vitæ augmente votre CV. Autres
**Appeler à l'action** Obtenir des commentaires, suggérer de suivre pour plus d'entrevues. Autres

---

Dépôt de code final

Créer une petite repo avec la structure suivante:

«» "
leetcode-3667/
- Java/
Une solution. java
Python/
│ Solution. py
- Cpp/
Solution.cpp
- README.md (copie de ce blog)
«» "

Push to GitHub, ajoutez le hash commit à votre CV ou LinkedIn, et liez-le dans votre portfolio.

---

- Oui.

Vous avez maintenant :

1. **Trois solutions prêtes à la production** prêtes à être collées dans LeetCode ou une entrevue d'emploi.
2. Un post de blog **complet** qui explique le problème, plonge dans les compromis algorithmiques, et vous positionne comme un candidat réfléchi.
3. **SEO-friendly content** qui peut aider votre site personnel de classement pour la valeur absolue et les questions d'entrevue connexes.

Bon codage – et bonne chance pour ce travail! C'est ce qu'il a dit