---
titre: LeetCode 3113. Trouvez le nombre de sous-barrages où les éléments de limite sont maximum - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3113 – Trouvez le nombre de sous-barrages où les éléments de limite sont maximum
Les bons, les mauvais et les affreux
> * Auditoire cible : ingénieurs de front-end, back-end, stack complet se préparant pour les entrevues de codage et les gestionnaires d'embauche. *

---

Récapitulation des problèmes

> **Grâce** à une série d'entiers positifs "nums", retourner le nombre de subarrays de sorte que le premier et le dernier élément de la subarray soient **égals à l'élément maximum** de cette subarray.

Obstacles
- "1 ≤ longueur nominale ≤ 105 "
- `1 ≤ nombres[i] ≤ 109'

La réponse peut être aussi grande que `n*(n+1)/2`, alors utilisez un entier 64 bits (`long` / `long`).

---

Pourquoi ce problème est-il intéressant ?

* **Count subarrays** – un thème d'interview classique.
* **Les élémentsoundaires doivent être le maximum** – cette propriété conduit à un motif de pile monotonique.
* ** Grandes contraintes** – la force brute (« O(n2) » ou « O(n3) » est impossible.
* **Connaissance de cas** – tous nombres égaux, augmentation/diminution stricte, élément unique, etc.

---

Les bonnes

Pourquoi ça compte ?
-- -- -- -- -- -- -- --
**O(n) temps** – Scan linéaire avec une pile monotonique
**O(n) espace** – Seule la pile est stockée.
**Logique intuitive** – Bien que le sommet soit plus petit, pop
**Cadre réutilisable** – La pile monotonique résout beaucoup de problèmes de nombre de problèmes de nombres subarray / subarray

---

Les mauvais

Sujet Atténuation
C'est pas vrai.
**Débordement entier** – La réponse peut dépasser `int32`.
**Modifier les valeurs égales** – Besoin de grouper des éléments égaux consécutifs.
** Erreurs hors-par-un** – Limites subarray inclusives ou exclusives. → 6

---

# # # Les affreux

Problème Erreur typique
- Oui.
Brute-force O(n2) compte trop lent, temps sur grande entrée
Autres Deux boucles imbriquées sans tailler
Autres Oubliant la contrainte maximale en comptant tous les subarrays au lieu de ceux qui satisfont à la condition limite
Utiliser `ArrayList` pour la pile et faire `remove`/`add` au début.
Autres Ne pas réajuster le nombre d'éléments égaux

---

## -Le point de vue clé

Nous énumérons ** la limite droite** de chaque sous-aire.
Pendant que nous déplaçons la limite droite `i` de gauche à droite, nous conservons une pile **monotoniquement décroissante** de paires `(valeur, nombre)`:

* **Valeur** – le nombre réel à ce niveau de pile.
* **Count** – combien de positions consécutives (à gauche) ont cette valeur comme maximum jusqu'à présent.

Lorsque nous rencontrons un nouvel élément `a = nums[i]`:

1. **Pop** tous les éléments de la pile dont la valeur est **plus petite** que `a`.
Ces éléments ne peuvent pas être le maximum pour toute subdivision se terminant à « i » parce que « a » est plus grand.
2. Si la pile est **vide** ou si sa valeur supérieure est **différente** de `a`, **poush** `(a, 0)`.
Cela commence un nouveau bloc d'éléments égaux.
3. **Incrément** le nombre de l'élément supérieur: `stack.top.count += 1`.
Ce nombre représente maintenant combien de subarrays se terminant à `i` ont `a` comme maximum et commencent par cette `a` (ou une valeur plus petite qui a été poped).
4. **Ajouter** qui comptent pour la réponse globale.

Pourquoi ça marche ?
Toutes les subdivisions se terminant à la position `i` qui ont `a` comme maximum doivent commencer quelque part **après** le dernier élément plus grand que `a`.
Tous les éléments après ce point, mais **avant** `i` sont ***; la pile garantit que nous ne conservons que des valeurs ≤ a, et des valeurs égales consécutives sont groupées, de sorte que nous pouvons les compter en O(1) par étape.

---

Numéro de code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous les trois partagent la même logique et fonctionnent dans le temps "O(n)".

Autres **Important** – utiliser `long` (`int64`) pour le résultat.

---

- Oui. Java (Java 17)

"Java
Importer java.util. - ArrayDeque;
Importer java.util. Deque;

solution de classe publique {
nombre public longOfSubarrays(int[] nums) {
// Élément pile : {valeur, nombre}
Deque<int[]> pile = nouveau ArrayDeque<>();
long res = 0;

pour (int a : nombres) {
// 1. Supprimer les éléments plus petits
pendant que (!stack.isEmpty() && empil.peek()[0] < a) {
pile.pop();
}

// 2. Poussez un nouvel élément si nécessaire
si (stack.isEmpty()=== empil.peek()=a) {
pile.push(nouvelle int[]{a, 0});
}

// 3. Compte d ' accroissement et addition au résultat
pile.peek()[1]++; // count++
res += pile.peek()[1];
}
retour rés;
}
}
«» "

---

### Python (Python 3,11)

'`python
de taper l'importation Liste

Solution de classe:
Numéro De Subarrays(même, nombres: Liste[int]) -> Int:
pile : Liste[List[int]] = [] # chaque élément est [valeur, nombre]
Res = 0

pour les nombres:
# Pop valeurs plus petites
pendant la pile et la pile[-1][0] < a:
Pile.pop()

# Poussez un nouveau bloc si nécessaire
si elle n'est pas empilée ou empilée[-1]] > a:
Annexe(a), 0])

Nombre d'accroissements et accumulation
pile[-1][1] += 1
res += pile[-1][1]

retour res
«» "

---

### C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long nombreOfSubarrays(vector<int>& nums) {
// Élément de la pile : paire<valeur, nombre>
vectorielle<vector<int>> st; // pile stockée comme vectorielle<valeur, nombre>
longue rés = 0;

pour (int a : nombres) {
// 1. Pop petits éléments
pendant que (!st.vide() && st.back()[0] < a) {
le _retour_st.pop();
}

// 2. Poussez un nouvel élément si nécessaire
si (st.vide()) {
st.push_back({a, 0});
}

// 3. Nombre d ' accroissements et accumulation
() [1]++; // count++
res += st.back()[1];
}
retour rés;
}
};
«» "

> Dans C++, nous utilisons un `vector<vector<int>>` pour imiter la paire `(value, count)`.
> L'accessor `back()` donne des opérations de pointe à temps constant.

---

Essais et cas de bord

Autres Test d'entrée d'entrée d'entrée d'entrée d'entrée
- C'est pas vrai.
Chaque sous-arrachage commence et se termine par `3` et `3` est le maximum. Autres
Seuls les termes `[1,2]`, `[2,3]` et `[3]` sont éligibles. Autres
"[3,2]" "[3,2]" "[3,2] ". Autres
= 10
[10^9] * 100000 ' , `n*(n+1)/2` (=5e9) , " S'assurer qu'il n'y a pas de débordement; " long " le gère. Autres

Exécutez le script simple suivant pour vérifier :

'`python
sol = Solution()
print(sol.numberOfSubarrays([3,3,3])) # 6
print(sol.numberOfSubarrays([1,2,3,2,1])) # 7
«» "

---

Analyse de complexité

Étape Coût Raison
C'est pas vrai.
Numérisez `nums` une fois Une traversée linéaire
Opérations d'embouteillage
La complexité finale **L'espace O(n)**

Le seul ajout "long` qui pourrait déborder est la réponse finale; "long` peut stocker jusqu`à `9×1018`, ce qui est bien au-dessus du nombre maximal possible de sous-arrachages (`- 5×109` pour `n = 105`).

---

Conseils d'entrevue

1. ** Expliquer l'invariant de la pile**: *=Les valeurs de la pile sont en ordre décroissant, et chaque paire détient le nombre de sousarrays se terminant à la position actuelle qui commence par cette valeur.
2. **Pourquoi pop petits éléments?** – Un élément plus grand du côté droit domine, de sorte que les plus petits ne peuvent pas être maxima. (en milliers de dollars)
3. **Pourquoi grouper des valeurs égales?** – Évite de recomptabiliser chaque événement séparément.
4. **Vérifier les débordements** – Mention en utilisant `long` / `int64`.
5. **Discuss edge cases** – Toutes valeurs égales, éléments uniques ou tableaux strictement monotoniques.

> * Conseil professionnel :* Lorsque vous êtes coincé, essayez d'écrire une version **brute-force** pour `n ≤ 10` et comparez les sorties. Cela révélera des bugs subtils tôt.

---

À emporter

La pile monotonique donne une solution propre et linéaire qui :

* **Fast** – gère la taille maximale d'entrée.
* **Amical** – seulement la pile compte.
* **Préparé à l'entrevue** – vous pouvez expliquer l'invariant en moins de 5 minutes.

Éviter les pièges du débordement, de la manipulation à valeur égale et des pièges à force brute. Montrez que vous comprenez le modèle de base, et vous impressionnerez les gestionnaires d'embauche qui aiment réutilisable, code élégant.

---

# # # OBJET Mots clés

- **LeetCode 3113**
- ** Limite maximale de la sous-période**
- ** Nombre maximal de sous-tarifs**
- **algorithme de la pile monotonique**
- **O(n) solution**
- Entretien de Java Python C++**
- **Codage des modèles d'entrevue**
- **Conseils d'entretien d'emploi**
- ** défi de codage de l'ingénieur logiciel**

---

La pensée finale

Un problème qui à première vue se sent comme un cauchemar de comptage se résume en fait à une belle danse de pile monotonique. Maître ce modèle et vous allez non seulement écraser LeetCode 3113, mais vous allez également débloquer un outil puissant pour votre prochaine interview technique. Bon codage 