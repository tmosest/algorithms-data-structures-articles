---
titre: LeetCode 88. Array trié par fusion
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code Leet 88 – Array trié par fusion
**Difficulté:** Facile
**Langues:** C++
**Complexité temporelle:** *O(m + n)* (optimale)
**Complexité spatiale:** *O(1)* (en place)

> **Vous souhaitez poser cette entrevue sur les structures de données? * *
> Les problèmes de maîtrise comme *Merge Tried Array* montre les recruteurs que vous savez écrire un code propre et optimal et vous pouvez penser en termes de *temps* vs. *espace*. Ci-dessous, vous trouverez une plongée profonde – le bon, le mauvais et le mauvais – plus des solutions prêtes à la production en trois langues principales.
> **Mots clés:** Merge Trié Array, Leetcode 88, problème de codage d'entrevue, algorithme O(m+n), Java, Python, solutions C++, préparation d'entretiens d'emploi, entretien de structure de données, conseils d'entretiens techniques.

---

Récapitulation des problèmes

Vous recevez deux tableaux entiers qui sont déjà triés en ordre non décroissant :

Sens de la variable Taille
C'est quoi ?
`nums1`= Premier tableau, **a de l'espace pour `m + n` éléments**. Les premiers éléments `m` sont valides, les derniers `n` sont `0` et sont conçus comme "buffer".
Nombre d`éléments valides dans `nums1`.
`nums2`=2 Deuxième tableau, tous les éléments `n` sont valides.
Nombre d ' éléments dans les chiffres2

Votre tâche consiste à fusionner `nums2` en `nums1` de sorte que le tableau résultant soit trié dans un ordre non décroissant. La fusion doit se faire **en place** (pas d'allocation de tableau supplémentaire).

> **Exemple**
> ```texte
> nombres1 = [1,2,3,3,0,0], m = 3
> nombres2 = [2,5,6], n = 3
> → [1,2,2,3,5,6]
> `` "

---

Pourquoi ce problème se pose dans les entrevues

1. **Manipulation de pointeurs de Showcases** – les recruteurs aiment voir comment vous manipulez les indices.
2. **L'échange espace-temps** – le suivi demande du temps O(m + n) en soulignant votre compréhension des algorithmes optimaux.
3. **Connaissance de cas** – tableaux de longueur zéro, nombres négatifs, valeurs identiques, etc.
4. ** Erreur commune de débutant** – utilisant `Arrays.sort` sur l'ensemble du tableau (O((m+n)log(m+n))) au lieu d'une fusion linéaire.

---

Les bons, les mauvais, les affreux

Qu'est-ce qu'il faut éviter ? Pourquoi ça compte ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bonne**) *O(m + n) temps, O(1) espace* fusionner à partir du **end**. Autres
**Création d'un nouveau tableau en utilisant l'espace O(m + n) ou le temps O((m+n)log(m+n) intégré – semble flou sur un écran d'entrevue. Autres
**Bogues hors-par-un : oubliant que le tampon `nums1' est à la fin, manipulant mal les tableaux vides. Autres

---

Solution optimale (O(m + n))

Idée de base

Traverse **de la fin** des deux tableaux:

1. Maintenir trois indices :
- `i = m‐1` (dernier élément valide dans `nums1`)
- `j = n‐1` (dernier élément dans `nums2`)
- `k = m + n - 1` (dernière position en `nums1`)

2. Alors que `j >= 0':
- Si 'i >= 0` ** et** `nums1[i] > nums2[j]`, place `nums1[i]` à `nums1[k]`.
- Autre lieu "nums2[j]` à "nums1[k]".
- Déplacez le pointeur correspondant à gauche et décrochez `k`.

3. Si `j` devient négatif, les éléments `nums1` restants sont déjà en place; si `i` devient négatif, la boucle se termine tôt (le reste `nums2` est déjà copié).

Pourquoi ça marche ?

- Oui. On n'écrase jamais une valeur qui n'a pas encore été prise en compte parce que nous passons de la fin vers le front.
- Chaque élément est déplacé au plus une fois → **temps linéaire**.
- Oui. Pas de tableau supplémentaire → **espace auxiliaire constant**.

---

Mise en œuvre du code

> **Astuce:** Tester avec les cas bord des exemples, en particulier `m = 0`, `n = 0` et les nombres négatifs.

### Java

"Java
solution de classe publique {
nums1, int m, int[] nums2, int n) {
i = m - 1; // dernier indice valide en nombres1
int j = n - 1; // dernier indice en nombres2
int k = m + n - 1; // dernier indice en chiffres globaux

pendant que (j >= 0) { // seulement besoin de vérifier nombres2
Si (i >= 0 && nums1[i] > nums2[j]) {
nombres1[k--] = nombres1[i--];
} autre {
nums1[k--] = nums2[j--];
}
}
}
}
«» "

> **Pourquoi c'est génial* *
> - "quand (j >= 0)` garanties que nous terminons la copie `nums2`.
> - Le garde `i >= 0` nous protège de l'accès `nums1[-1]`.
> - Pas de `Arrays.sort`, pas de tableau supplémentaire.

---

Python

'`python
Solution de classe:
def merge(self, nums1: List[int], m: int,
nombres2: Liste[int], n: int) -> Aucun:
"""
Ne retournez rien, modifiez nums1 en place.
"""
i, j, k = m - 1, n - 1, m + n - 1
alors que j >= 0:
i >= 0 et nombres1[i] > nombres2[j]:
nombres1[k] = nombres1[i]
I -= 1
Sinon:
nombres1[k] = nombres2[j]
J = 1
k -= 1
«» "

> ** Touche pyronique**
> - Utilise des noms de variables claires `i`, `j`, `k`.
> - La condition de boucle `alors que j >= 0` garantit que tous les éléments `nums2` sont placés.

---

C++

'`cpp
solution de classe {
public:
fusion vide(vecteur<int>& nums1, int m,
vecteur<int>& nums2, int n) {
i = m - 1; // dernier élément valide dans nums1
int j = n - 1; // dernier élément dans nombres2
int k = m + n - 1; // dernier indice en chiffres globaux

pendant que (j >= 0) {
Si (i >= 0 && nums1[i] > nums2[j]) {
nombres1[k--] = nombres1[i--];
} autre {
nums1[k--] = nums2[j--];
}
}
}
};
«» "

> **C++ nuances**
> - Utilise la référence pour éviter de copier `nums1`.
> - `vecteur<int>&` garde la signature que LeetCode attend.

---

Étape par étape (exemple de Java)

Étape Action Résultat
C'est pas vrai.
1=1 `i = 2`, `j = 2`, `k = 5`= Pointeurs aux extrémités
"nums1[i] = 3`, "nums2[j] = 6` → place "6` à "nums1[5]` "nums1 = [1,2,3,0,0,6]" Autres
Déplacer à gauche
< < nums1[i] = 3`, < < nums2[j] = 5` → place < < nums1 = [1,2,3,0,56] > > Autres
* < < j = 0 > > , < < k = 3 > > ...
6.00 `nums1[i] = 3`, `nums2[j] = 2` → place `3`.00 `nums1 = [1,2,3,3,5,6]` Autres
, k = 2
8.0 `nums1[i] = 2`, `nums2[j] = 2` → place `2`"nums1 = [1,2,2,3,5,6]` Autres
= -1` → boucles

---

Liste de contrôle de l'entrevue

1. **Énoncer les contraintes** – `nums1.longueur=m + n`, `nums2.longueur=n`.
2. **Dépliquer le temps/l'espace en échange** – Temps O(m+n) et espace O(1). (en milliers de dollars)
3. **Cas de bord de poignée** – `m == 0`, `n == 0`, éléments égaux.
4. **Afficher l'approche pointeur** – mettre l'accent sur le départ de la fin pour éviter l'écrasement.
5. **Écrire un code propre** – noms de variables clairs, commentaires au besoin.
6. **Testez mentalement** – passez à travers quelques scénarios sur le tableau blanc.

> **Conseil pro**: Si l'intervieweur demande le temps de *suivi* (O(m + n), soulignez que l'algorithme ci-dessus le réalise déjà. S'ils demandent de l'espace *O(m + n), mentionnez que vous pouvez utiliser un tableau temporaire, mais cela va à l'encontre du but de la fusion en place.

---

SEO Snapshot (Meta Tags & Snippets)

html
<title>Merge Trié Array – LeetCode 88 (Java, Python, C++)
<meta name="description" content="Solve LeetCode 88 Fusionner Array trié en Java, Python et C++ avec un algorithme O(m+n) en place optimal. Apprenez les pièges, les cas de bordure et les conseils d'entrevue.">
<meta name="keywords" content="Merge Trié Array, Leetcode 88, problème d'entrevue, algorithme O(m+n), Tableau de fusion Java, tableau trié par Python, tableau de fusion C++, prép d'entrevue de codage">
«» "

> **Pourquoi ça aide* *
> Ces étiquettes font surface à votre article dans les résultats de recherche pour toute personne cherchant à maîtriser ce problème spécifique LeetCode—parfait pour les recruteurs scannant des portefeuilles candidats.

---

La dernière sortie

- **Bien**: L'approche à trois points de l'arrière est propre, linéaire et en place.
- **Bad**: L'utilisation de "sort" ou l'attribution de mémoire supplémentaire montre un manque de pensée optimale.
- **Ugly**: Oublier que le tampon est à la fin conduit à `ArrayIndexOutOfBounds`.

La maîtrise de ce problème démontre votre capacité à lire les contraintes, à concevoir un algorithme efficace et à écrire un code prêt à la production. Apportez ces connaissances à votre prochain entretien technique, et vous montrerez aux recruteurs que vous êtes prêts à relever les défis de la structure des données dans le monde réel.

Bonne chance, et le codage heureux! C'est ce qu'il a dit