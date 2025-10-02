---
Titre: LeetCode 2219. Score maximum de la somme de la représentation -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le Code – 3 langues en une seule fois

Vous trouverez ci-dessous des solutions **ready‐to‐paste** pour le LeetCode 2219.
Tous les trois utilisent un algorithme *simple-pass* O(n) avec un espace supplémentaire O(1) – la façon la plus efficace de résoudre ce problème.

Description de la langue Autres
- C'est quoi ?
**O(n)** temps, **O(1)** espace. Autres
Python **O(n)** time, **O(1)** space. Autres
**O(n)** temps, **O(1)** espace. Autres

---

### Java

"Java
// LeetCode 2219 - Maximum Score du tableau
solution de classe {
public long maximum SumScore(int[] nums) {
long total = 0;
pour (int v : nombres) total += v; // 1ère passe: total

préfixe long = 0;
long best = Long.MIN_VALUE;

pour (int v : nombres) {
préfixe += v; // exécutant la somme du préfixe
long suffixe = total - préfixe + v; // somme des derniers éléments n-i
best = Math.max (best, Math.max (préfixe, suffixe));
}
le meilleur retour;
}
}
«» "

> **Pourquoi `total - préfixe + v`?**
> «préfixe» est la somme des «nums[0..i]».
> La somme des derniers éléments `n-i` est `total - préfixe + nums[i]` (soustrayez tout avant `i`, gardez `i` lui-même).

---

Python

'`python
Code Leet 2219 - Maximum Score du tableau
Solution de classe:
def maximum SumScore(même, nombres: Liste[int]) -> Int:
total = somme(s) # total en O(n)

préfixe = 0
best = -10**18 # suffisamment petite sentinelle

pour v en chiffres:
préfixe += v
suffixe = total - préfixe + v
best = max(meilleur, préfixe, suffixe)

le meilleur retour
«» "

---

C++

'`cpp
// LeetCode 2219 - Maximum Score du tableau
solution de classe {
public:
long long maximum SumScore(vecteur<int>& nums) {
long total = 0;
pour (int v : nombres) total += v; // 1ère passe

préfixe long = 0;
longue longue meilleure = LLONG_MIN;

pour (int v : nombres) {
préfixe += v;
long suffixe long = total - préfixe + v;
best = max(meilleur, max(préfixe, suffixe);
}
le meilleur retour;
}
};
«» "

---

- Oui. Le blog – Le bon, le mauvais et l'hommage de LeetCode 2219

Introduction
Si vous êtes à la recherche d'un emploi en génie logiciel, la maîtrise *LeetCode 2219 – Score maximum de la somme d'Array* brillera sur votre CV d'entrevue. Il teste la manipulation du tableau, préfixe les sommes et la manipulation subtile des cases. Dans cet article, nous disséquons le problème, nous expliquons pourquoi un algorithme de préfixe de passage unique est le roi, et nous mettons en évidence les pièges (les "bad" et les "ugly") qui peuvent voyager les candidats. Mots clés du référencement : **Leetcode 2219, Score de somme maximum de Array, interview de codage, solution Java, solution Python, solution C++, somme de préfixe, algorithme O(n)**.

---

Énoncé du problème (reformulé)

Compte tenu d'un tableau entier `nums` (longueur `n`), le score **sum** à l'index `i` est:

«» "
max( somme(nums[0 .. i]), somme(nums[i .. n-1])
«» "

Retourne la somme maximale pour tous les indices.

*Contrôles*
- `1 ≤ n ≤ 10^5`
- `-10^5 ≤ nums[i] ≤ 10^5`

---

Pourquoi une stratégie préfixe-sum est de l'or

1. **Éviter O(n2)* *
La solution naïve compare chaque paire de sommes préfixes/suffixes, ce qui conduit à un temps O(n2) – impossible pour 105 éléments.

2. **Pass unique O(n)**
En calculant la somme totale d'abord, chaque itération peut déduire la somme suffixe en O(1):
`suffix = total - préfixe + nombres[i]`.

3. ** Espace supplémentaire continu**
Seules quelques variables "long`/`long` sont nécessaires - répond à la contrainte spatiale.

4. ** Négatif avec grâce* *
Parce que nous suivons le maximum de deux sommes en cours d'exécution, les valeurs négatives réduisent automatiquement le score.

---

Algorithme

«» "
total = somme(s) // 1er passage
préfixe = 0
réponse =

pour chaque élément v en chiffres:
préfixe += v
suffixe = total - préfixe + v
réponse = max(réponse, préfixe, suffixe)

réponse de retour
«» "

**Key Insight** – `suffix` n'est pas `total - prefix` parce que `prefix` inclut déjà `v`.
Nous devons tout soustraire *avant* `i` mais garder `i` lui-même.

---

Code dans toutes les langues principales

(voir rubrique 1 pour la source complète).
Les trois codes partagent la même logique, ne différant que dans la syntaxe et le type entier (`long`, `int`, `long`).

---

Les mauvaises – Pièges communs

Pourquoi ça arrive ?
- Oui.
**L'excès de flux en Java/C++** Autres
**Utiliser `sum - prefix` au lieu de `sum - prefix + v`**.
**Non à la manipulation des tableaux négatifs**
**Two-pointer wrong loop limits**= Off‐by‐one conduit à une mauvaise somme suffixe== Préférez une formule préfixe pour éviter de telles erreurs==

---

### -Le mauvais – Sur-ingénierie

- **Deux-pointeurs
Certaines solutions déplacent deux pointeurs des deux extrémités pour mettre à jour le préfixe/suffix à la volée.
Bien que toujours O(n), il ajoute une tenue de livres supplémentaire (gauche/gauche) qui est facile à boguer.

- **Pre-computing full prefix array**
Stocker toutes les sommes de préfixe double l'utilisation de la mémoire et rend l'algorithme inutilement lourd.

- **Différence récursive et conquête**
La division du tableau et les résultats de fusion sont surqualifiés; il ajoute la profondeur logarithmique et l'utilisation de la pile.

**Ligne de bottom:** La simplicité bat l'intelligence. La solution de préfixe à un passage propre est à la fois plus rapide et plus facile à vérifier.

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
O(n2)
Préfixe-Sum (1-pass)

Pour `n = 100 000`, le préfixe-sum fonctionne en < 0,01 s en Java et Python sur les juges modernes.

---

### --Tendance pour les intervieweurs

1. **Demander pour les cas de bord** – négatifs, élément unique, tous négatifs.
2. **Vérifiez la gestion des débordements** – de nombreux candidats utilisent `int`.
3. **Le raisonnement du son** – pourquoi `suffix = total - préfixe + nombres[i]`?
4. **Test avec de grands tableaux aléatoires** – pour confirmer la linéarité.

---

Réflexions finales

LeetCode 2219 est un problème classique de "prefix-sum, one-pass".
Son élégance réside dans la conversion d'une comparaison apparemment quadratique en une seule boucle avec un espace constant.

La maîtrise de ce modèle vous donne confiance pour beaucoup d'autres questions d'entrevue (par exemple, la somme de subarray maximale, le plus grand rectangle dans l'histogramme).

**Vous voulez avoir l'entrevue de codage?** Continuez à pratiquer les problèmes qui dépendent de **préfixer les sommes**, **deux pointeurs** et **passes linéaires optimales**. Ajoutez les solutions ci-dessus à votre repo GitHub, écrivez un court blog, et laissez les recruteurs vous voir briller!

Bon codage ! C'est ce qu'il a dit.

---

**Balises de référence**:
- Leetcode 2219
- Score de la somme maximale de la représentation
- Solution de préfixe Java
- Solution Python 2219
- C++ Algorithme O(n)
- Codage de la préparation de l'entrevue
- Structures de données et algorithmes
- Questions d'entretien
- Entretien en génie logiciel
- Reprendre les problèmes de codage

---

**Références**
- Page du problème LeetCode: https://leetcode.com/problèmes/maximum-sum-score-of-array/
- Solutions officielles et liens de discussion (fournis dans l'invite) – utiles pour les plongées plus profondes.