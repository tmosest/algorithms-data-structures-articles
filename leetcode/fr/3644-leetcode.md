---
titre: LeetCode 3644. K maximum pour trier une permutation -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3644. **K maximum pour trier une permutation** – Solution en trois langues + SEO – Blog optimisé

> **Auteur:** *Votre nom*
> **Platforms:** LeetCode, Préparation des entrevues, Entrevues de codage
> ** Compétences mises en évidence :** Opérations bit-wise, Algorithmes de Greedy, O(n) Complexité temporelle, Codage efficace dans l'espace

---

TL;DR

- **Objectif** – Trouvez le plus grand entier non négatif **k** de sorte que nous puissions trier la permutation donnée en échangeant *any* paire d'indices **i, j** *iff* `nums[i] & nums[j] == k`.
- **Réponse** – Le k maximum est le **bitwise ET de tous les nombres déplacé**.
- **Complexité** – temps « O(n) », espace « O(1) ».
- **Pourquoi ça marche** – Chaque élément déplacé partage au moins les bits dans ce commun ET, et la propriété de permutation garantit que nous pouvons toujours atteindre l'ordre correct en utilisant seulement ces bits.

---

## Pourquoi ce problème est une médaille d'or pour les entrevues

**C'est important**
-- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bitwise Insight**=Utilisez et filtrez les bits communs – un modèle d'entrevue classique. Montrez que vous comprenez la manipulation des bits, pas seulement les boucles. Autres
**Greedy Simplicité**Le `k` optimal est obtenu par un seul passage, pas de retour en arrière. Démontre vous pouvez repérer des solutions cupides linéaires. Autres
Autres **Edge‐Case Awareness**=Déjà trié → réponse 0, tous les nombres déplacé → tous les bits. Tests de manipulation soigneuse des cas spéciaux. Autres
**Language Agnostique** Preuves que vous pouvez traduire la logique à travers les écosystèmes. Autres
**L'emploi-la pertinence**Les entreprises s'interrogent sur les permutations, le tri et les opérations bitwise. Autres

---

Les bons, les mauvais et les affreux

Les bons
- **Solution à un seul passage** – pas besoin de détection du cycle de l'union ou du graphique.
- **Deterministic k** – vous n'avez jamais à essayer de plusieurs valeurs k.
- **Proof intuitif** – le ET des éléments égarés est le *seulement* candidat qui garantit chaque échange est autorisé.

- Oui. Les mauvais
- **Incompréhension commune** – Beaucoup pensent que vous pouvez choisir différents ks pour différents swaps.
- ** Supposition de la permutation** – Si le tableau n'est pas une vraie permutation, l'Astuce ET se casse.

- Oui. L'Ugly
- **Pièges de mise en œuvre** – Commençant par `INT_MAX` (ou `~0`) et oubliant de le réinitialiser lorsqu'il n'y a pas d'erreur.
- **Diminution de la lecture La propriété de permutation garantit que l'ordre trié est `0..n‐1`; sinon, vous devrez gérer les duplicatas.

---

## Code complet (trois langues)

> Toutes les implémentations se déroulent dans le temps `O(n)` et `O(1)` espace supplémentaire.
> Utilisez la même logique dans votre langue préférée; l'idée centrale ne change jamais.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
Int tri publicPermutation(int[] nums) {
// Si trié, aucun swaps n'est nécessaire → k = 0
masque int = entier.MAX_VALUE; // toutes les 1s en binaire
pour (int i = 0; i < nombres de longueur; i++) {
si (nums[i] != i) { // ne considèrent que des éléments égarés
masque &= nombres[i]; // ne conserver que des bits communs
}
}
// Si le masque est inchangé, le tableau a été trié
masque de retour == Entier. MAX_VALUE ? 0 : masque;
}

// Principale option pour les tests rapides
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.sortPermutation(nouvelle int[]{0,3,2,1}); // 1
System.out.println(s.sortPermutation(new int[]{0,1,3,2}); // 2
Système.out.println(s.sortPermutation(new int[]{3,2,1,0}); // 0
}
}
«» "

---

Python

'`python
Solution de classe:
def sortPermutation(self, nombres: list[int]) -> Int:
masque = (1 << 31) - 1 masque tout-one 32 bits (travaille pour n'importe quel n)
pour i, val dans l'énumération(nombres):
Si val != i:
masque &= val
retour 0 si masque == (1 << 31) - 1) autre masque


♪ Harnais d'essai rapide
si __nom__ == "__main__" :
s = Solution()
print(s.sortPermutation([0, 3, 2, 1]) # 1
print(s.sortPermutation([0, 1, 3, 2]) # 2
print(s.sortPermutation([3, 2, 1, 0]) # 0
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Type intPermutation(vecteur<int>& nums) {
masque int = INT_MAX; // ensemble de bits
pour (int i = 0; i < (int)nums.size(); ++i) {
i (nums[i] != i) // uniquement pour les éléments égarés
masque &= nombres[i]; // ne conserver que des bits communs
}
masque de retour == INT_MAX ? 0 : masque;
}
};

Int main() {
Solution s;
<< s.sortPermutation({0,3,2,1}) << endl; // 1
<< s.sortPermutation({0,1,3,2}) << endl; // 2
Cout << s.sortPermutation({3,2,1,0}) << endl; // 0
}
«» "

---

## Preuve étape par étape (Pourquoi le ET fonctionne)

1. **Tous les éléments sont de «0 ... n‐1».**
Cela garantit que chaque entier a au plus `=log2 n=1= bits, et l'ensemble de tous les nombres est *fermé* sous bitwise AND.

2. **Que `M` soit l'ensemble d'indices égarés**:
`M = { i.i.i.i }`.

3. **Définir `k* = nombres[i1] & nombres[i2] & ... & nombres[im]`** (bitwise ET sur tous les nombres égarés).
Par construction, `k*` est le sous-ensemble ** commun de bits** présent dans chaque élément mal placé.

4. **Tout échange entre deux éléments égarés** "a, b, b, M" satisfait
`a & b` contient tous les bits de `k*` (puisque `k*` est le ET de tous).
Par conséquent, échanger `a` et `b` est autorisé *si nous choisissons* `k = k*`.

5. **Bridging via des éléments correctement placés* *
Même si certains nombres déplacé ne partagent pas directement bitwise ET égal à `k*`, nous pouvons parcourir un élément `c` * correctement placé* qui contient déjà les bits requis.
Parce que `c` est `c = i` (son propre indice), il partage toujours au moins les bits de `i` avec n`importe quel élément `x` qui contient ces bits.
Cela garantit que nous pouvons déplacer n'importe quel élément déplacé à sa position correcte en utilisant une séquence de swaps tout en respectant `k = k*`.

6. ** Maximalité** – Supposons que tout plus grand `k` (`k' > k*`) puisse trier le tableau.
Ensuite `k'' devrait être un bitwise commun ET de **chaque** nombre déplacé (car chaque swap doit satisfaire `x & y == k'`).
Mais `k*` est déjà le *maximum* tel bitset commun: ajouter n'importe quel bit supplémentaire l'éteindreait dans au moins un élément déplacé, brisant l'égalité.
Par conséquent, « k* » est le « k » maximum possible.

7. **Edge Cases** – Si aucun élément n'est déplacé, la boucle ne change jamais `masque`, donc nous retournons `0`.
Si tous les éléments sont égarés, `mask` devient l'AND de tous les nombres dans `0 ... n‐1`, qui est `0` pour `n ≥ 2` (puisque certains nombres manquent chaque bit). Ainsi, la réponse est `0`, correspondant à l'intuition.

---

- Oui. Comment tourner Cela dans un récit d'emploi gagnant

1. **Démarrer avec l'énoncé de problème** – Résumer en une phrase : -Trouver le plus grand `k` qui permet de trier une permutation en n'échangeant que des paires avec `nums[i] & nums[j] == k`.

2. **Afficher votre processus de pensée** – Expliquez pourquoi vous avez d'abord considéré une approche gourmande ET, pourquoi les cycles étaient inutiles, et comment la propriété de permutation simplifie les choses.

3. **Présenter le code** – Mettre en évidence la passe linéaire et l'utilisation subtile de `INT_MAX`/`~0` comme masque initial. Mentionnez que la solution fonctionne dans n'importe quelle langue.

4. **Exposer la preuve** – Partager le raisonnement (comme ci-dessus) pour démontrer une compréhension profonde. Les intervieweurs aiment les candidats qui peuvent expliquer pourquoi une solution fonctionne.

5. **Mention Edge Cases & Test** – Afficher les harnais de test dans chaque langue et vérifier l'exactitude pour des exemples typiques.

6. **Enveloppez-vous avec Takeaways** – Bitwise ET peut souvent effondrer les contraintes en un seul entier. Dans ce problème, le ET commun des éléments égarés est la clé magique du tri. (en milliers de dollars)

L'ajout de cette histoire à votre curriculum vitæ ou à votre portfolio vous donnera un *standout* pour les interviews techniques.

---

## SEO-Optimized Blog Post Draft

> **Titre**: *Master LeetCode 3644 – -Maximum K pour trier une permutation – Solution One-Pass, O(n) (Java, Python, C++)*
> **Meta Description**: Apprenez le moyen le plus rapide pour résoudre LeetCode 3644. Un guide étape par étape, une preuve, et des extraits de code Java/Python/C++ pour le tri d'une permutation.

---

### Introduction (=200 mots)

> Dans les interviews de codage, LeetCodeS (ID 3644) est un favori pour tester votre maîtrise des opérations bitwise et des algorithmes gourmands. Le défi demande : *Donné d'une permutation de 0...n‐1, trouver le plus grand entier k de sorte que nous puissions trier le tableau en n'échangeant que des paires où le ET égal k.*
> De nombreuses solutions perdent du temps à explorer les cycles graphes ou à utiliser la recherche syndicale. La vraie clé est un tour simple et élégant. Cet article vous fait découvrir l'intuition, la preuve formelle et le code prêt à la copie en Java, Python et C++.

> À la fin de ce post, vous saurez non seulement mettre en œuvre la solution, mais aussi pourquoi elle est optimale – une compétence cruciale pour impressionner les intervieweurs à Google, Amazon et Microsoft.

---

- Oui. 1. Récapitulation des problèmes (150 mots)

- Définition de la permutation
- Contrainte d'échange `nums[i] & nums[j] == K'
- Objectif: maximum `k` pour trier le tableau

---

- Oui. 2. Force brute vs Optimisé (=200 mots)

- Discutez de l'approche naïve (essayez chaque k) → O(n · 2^bits)
- Pourquoi les cycles/syndicats sont inutiles en raison de la permutation
- Conduisez dans l'avidité ET

---

- Oui. 3. Idée de base: ET des éléments égarés (de 300 mots)

- Introduire `masque = tous les bits`
- Oui. Une boucle : si `nums[i] != i` → `mask &= nums[i] "
- Retour `0` si masque inchangé

Inclure la preuve dans une barre latérale de « Pourquoi ça marche ».

---

- Oui. 4. Galeries de codes (de 250 mots chacune)

- Extrait de Java
- Extrait de python
- Extrait C++

Affichez une plaque de chaudière minimale, mettez en évidence toutes les quirks linguistiques (par exemple, `~0` en Python).

---

- Oui. 5. Cas de bord et cas d ' épreuve (de 200 mots)

- Déjà trié → 0
- Tous déplacé → 0 pour n≥2
- Fournir des sorties de harnais et d'échantillons rapides.

---

- Oui. 6. Preuve d'optimisation (de 400 mots)

- Une explication formelle.
- Utilisez des diagrammes ou une table simple de bits pour illustrer.

---

- Oui. 7. Takeaways for Interviews (=200 mots)

- Bitwise ET comme une contrainte qui s'effondre.
- La propriété de permutation assure le réglage fermé.
- Oui. Aucun cycle ou graphique nécessaire – un scan linéaire pur et gourmand.

---

### Fermeture (150 mots)

> Que vous soyez en train de vous préparer pour un rôle d'ingénieur logiciel senior ou tout simplement de brosser sur des tours bitwise, LeetCode 3644 est un problème incontournable. La solution monopass, `O(n)` en Java, Python et C++ est aussi élégante qu'efficace. Déposez le code dans votre prép d'entrevue, marchez votre intervieweur à travers la preuve, et vous allez montrer que vous pouvez résoudre des contraintes non triviales avec une complexité minimale. Bon codage !

---

### Appel à l'action

> *Vous souhaitez des solutions LeetCode plus rapides? Abonnez-vous à des messages hebdomadaires, ou contactez-moi pour revoir votre préparation d'entrevue. *

---

La dernière pensée

*L'option "Maximum K" pour trier un problème de permutation" n'est pas seulement un test de codage. L'Astuce ET transforme une contrainte apparemment complexe en un seul entier, permettant une solution propre et unique. Maîtrisez-le, partagez-le, et regardez les intervieweurs reconnaître la profondeur de votre pensée algorithmique. *

---

Bon codage – et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit