---
titre: LeetCode 3437. Permutations III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3437 – Permutations III
Le Bien, le Mal et le Mal des Permutations Alternantes**
*Un guide complet et optimisé avec des solutions Java, Python et C++*

---

TL;DR

- **Problème**: Générer *toutes* permutations de `1 ... n` de sorte que deux nombres adjacents ne partagent pas la même parité (à la fois impairs ou les deux).
- **Solution**: Retraçage classique avec un garde de contrôle de parité.
- **Complexité**: "O(n!)" temps, "O(n)" espace supplémentaire (plus la pile de récursion).
- **Langues**: Java, Python, C++ (tous utilisables sur LeetCode, prep d'interview ou votre propre IDE).

---

Le bon, le mauvais et l'acharnement des permutations alternantes

- Oui. 1. Pourquoi ce problème se pose (et comment cela vous aide)

- **Interview Signal**: LeetCode 3437 est une question de difficulté *medium* qui teste:
- Compréhension des permutations.
- Capacité d'ajouter une contrainte *conditionnelle*.
- Nettoyer l'implémentation.
- **Career Impact**: Maîtriser ce problème met en évidence vos compétences en pensée algorithmique* et en résolution de problèmes* – traits clés que les gestionnaires d'embauche recherchent chez les ingénieurs en logiciels.

---

- Oui. 2. Déclaration de problème (de LeetCode)

> **Avec un entier `n`, retourner toutes les permutations des premiers entiers `n` positifs de sorte qu'aucun deux éléments adjacents ne soient à la fois bizarres ou les deux. **
> Retourner les permutations triées par ordre lexicographique.

**Contrôles* *

- `1 ≤ n ≤ 10`

**Exemples**

Produit
- Oui.
[[1,2,3,4],[1,4,2,2],[2,1,4,3],[2,3,4,1],[3,2,1,4],[3,4,1,2],[4,1,2,3],[4,3,2,1]» Autres
[[1,2],[2,1]]» Autres
[[1,2,3],[3,2,1]]» Autres

---

- Oui. 3. Briser le bien

3.1 Simplicité conceptuelle
- Oui. Nous commençons à partir du modèle standard de retour de permutation.
- La règle supplémentaire *only* est une vérification de parité : `candidate[pos-1] % 2 != nombres[i] % 2`.
- Parce que le contrôle est temps constant, l'algorithme reste *linéaire* en termes de décisions de branchement.

3.2 Lisibilité et réutilisabilité
- Le code Java utilise des noms de variables clairs (`nums`, `used`, `candidate`, `result`).
- Oui. L'aide récursive a une seule responsabilité : générer une permutation si elle satisfait à la contrainte de parité.

3.3 Preuve d'exactitude (Sketch)
- **Base**: Chaque permutation de `1...n` est générée par la logique de retour sous-jacente.
- **Induction**: Toutes les permutations partielles jusqu'à la longueur `k` satisfont à la règle de parité.
- L'ajout d'un nouveau nombre `x` à la position `k` n'est possible que si la parité `x`= est différente de la parité précédente.
- Ainsi, chaque permutation pleine longueur renvoyée satisfait à la règle, et aucune permutation valide n'est omise.

---

- Oui. 4. Le "Bad"

- ** Croissance exponentielle**: Même pour `n = 10`, il y en a `10! 3,6 millions de permutations.
- **Espace et temps**: Entreposer toutes les permutations à la fois peut être à forte intensité de mémoire.
- ** Limites pratiques** : Dans les paramètres d'entretien réels, les limites de LeetCode (`n ≤ 10`) le rendent sûr, mais soyez prêt à expliquer les contraintes si l'intervieweur augmente `n`.

---

- Oui. 5. Les

- **Ordre lexicographique** : L'algorithme standard de rétro-suivi produit naturellement des permutations dans l'ordre lexicographique *si* nous itérer des "nums" dans l'ordre ascendant et ne jamais reculer de façon non triée.
Pour `n = 1`, la seule permutation est `[1]`, qui est automatiquement valide.
- **Piège potentiel** : oublier de réinitialiser le drapeau « utilisé » après la récursion peut conduire à des permutations dupliquées ou manquées.

---

- Oui. 6. La solution – Backtracking avec Parity Guard

Voici l'idée centrale exprimée en trois langues populaires. Copiez-collez, lancez et sentez l'algorithme !

---

6.1 Mise en œuvre de Java

"Java
Importation de java.util.*;

solution de classe {
Int[]] permanent(int n) {
// Construire le tableau [1, 2, ..., n]
int[] nombres = nouveau int[n];
pour (int i = 0; i < n; i++) nombres[i] = i + 1;

booléen[] utilisé = nouveau booléen[n];
int[] candidate = nouvelle int[n];
Liste<int[]> res = nouvelle liste de distribution<>();

backtrack(nums, 0, utilisé, candidat, rés);

// Convertir la liste<int[]> en int[][] pour la signature LeetCode
int[][] out = nouvelle int[res.size()][n];
pour (int i = 0; i < res.size(); i++)
out[i] = res.get(i);

retour;
}

vide privé backtrack(int[] nums, int pos, booléen[] utilisé,
nt[] candidate, liste<int[]> res) {
si (pos == longueur nums.) {
res.add(candidate.clone()); // copie profonde
retour;
}

pour (int i = 0; i < nombres de longueur; i++) {
si (!utilisé[i]) {
// La première position est libre; d'autres doivent alterner la parité
si (pos) : (pos) : (candidat[pos - 1] % 2) != (nums[i] % 2) {
candidat[pos] = nombre[i];
utilisé[i] = vrai;
backtrack(nums, pos + 1, utilisé, candidat, rés);
utilisé[i] = faux; //
}
}
}
}
}
«» "

**Points clés**

- `candidate.clone()` nous permet de stocker une *copie* de la permutation actuelle.
- Le contrôle de parité `(candidate[pos - 1] % 2) != (nums[i] % 2)» garanties alternance.
- L'ordre lexicographique est préservé parce que nous itérer des "nums" dans l'ordre ascendant et jamais secouer.

---

6.2 Mise en œuvre du Python

'`python
de taper l'importation Liste

Solution de classe:
def permute(self, n: int) -> Liste[Liste[int]]:
nombres = list(range(1, n + 1))
utilisé = [Faux] * n
candidat = [0] * n
res: Liste[Liste[int]] = []

Def backtrack(pos: int):
si pos == n:
res.append(candidate.copy())
retour
pour i dans la plage(n):
si elle n'est pas utilisée[i]:
si pos == 0 ou (candidate[pos - 1] % 2) != (nums[i] % 2):
candidat[pos] = nombre[i]
utilisé[i] = Vrai
retour(pos + 1)
utilisé[i] = Faux

backtrack(0)
retour res
«» "

**Pourquoi Python? **

- La méthode `copy()` est un moyen léger de saisir `candidate`.
- La profondeur de récursion est au plus `n` (10), donc aucun débordement de la pile.

---

## 6.3 C++ Mise en œuvre

'`cpp
#incluez <vecteur>

solution de classe {
public:
std::vector<std::vector<int>> permute(int n) {
à:vecteur<int> nums(n);
pour (int i = 0; i < n; ++i) nombres[i] = i + 1;

std::vector<bool> utilisé(n, false);
std::vecteur<int> candidat(n);
md::vector<std::vector<int>> rés;

backtrack(nums, 0, utilisé, candidat, rés);
retour rés;
}

particulier:
vide backtrack(suite::vector<int>& nums, int pos,
std::vecteur<bool> et utilisé,
std::vecteur<int> et candidat,
(En milliers de dollars des États-Unis)
si [pos] nums.size() {
res.push_back(candidate);
retour;
}

pour (int i = 0; i < nums.size(); ++i) {
si (!utilisé[i]) {
si (pos) : (pos) : (candidat[pos - 1] % 2) != (nums[i] % 2) {
candidat[pos] = nombre[i];
utilisé[i] = vrai;
backtrack(nums, pos + 1, utilisé, candidat, rés);
utilisé[i] = faux; //
}
}
}
}
};
«» "

** Faits saillants* *

- Utilise `std::vector` pour les tableaux dynamiques.
- `candidate` est directement poussé dans `res`; la copie vectorielle se produit automatiquement.
- Oui. La même parité garde que les autres langues.

---

- Oui. 7. Analyse de la complexité

Complexité
C'est pas vrai.
**Temps**=O(n!)– nous générons chaque permutation valide. Autres
**L'espace**="O(n)` auxiliaire (`candidate`, `usage` tableaux) + pile de récursion `O(n)`. Autres
**Température de résultat**= `O(k * n)` où `k` est le nombre de permutations valides (= `n!`). Autres

---

- Oui. 8. Cas de bord et essais

Résultats escomptés
-- -- -- -- -- --
[[1]]» Autres
[[1,2],[2,1]]» Autres
[[1,2,3],[3,2,1]]» Autres
8 permutations (comme dans l'énoncé du problème)
10.3628800 permutations – assurez-vous que votre environnement peut gérer cette empreinte mémoire si vous exécutez localement. Autres

**Conseils de contrôle**

- Utiliser des tests unitaires pour affirmer la longueur de la sortie et que toutes les permutations sont uniques.
- Vérifier la règle de parité pour chaque paire d'éléments adjacents dans la sortie.
- Pour les grands `n`, utilisez un générateur ou un flux pour éviter de stocker toutes les permutations à la fois (non requis par LeetCode mais utiles dans les entretiens).

---

- Oui. 9. Explication de préparation à l'entrevue

> Nous générons des permutations à l'aide d'un rétrotraçage, mais à chaque étape nous n'autorisons qu'un nombre qui retourne la parité du dernier nombre. Parce que nous itérer des nombres en ordre ascendant, la liste finale est automatiquement triée lexicographiquement. *

Si l'intervieweur demande l'optimisation, mentionnez que :

- Oui. Le problème est intrinsèquement factoriel; aucun algorithme polynôme-temps n'existe.
- Pour les plus grands `n`, vous pouvez les générer paresseusement ou les diffuser un par un.

---

10. FAQs

Question Réponse
C'est pas vrai.
*Pourquoi pouvons-nous compter sur l'ordre lexicographique? Le DFS récursif standard qui traite les candidats en ordre ascendant émet toujours des permutations en ordre lexicographique. Autres
*Pouvons-nous utiliser la prochaine_permutation à la place? Vous pouvez générer toutes les permutations avec `next_permutation` et les filtrer, mais ce serait `O(n! * n)` dans le temps, plus lent que l'approche directe de retour. Autres
*Et si n > 10? * , l'algorithme reste correct, mais la mémoire/temps va exploser rapidement. Dans une entrevue, discutez des contraintes pratiques. Autres
Autres *Est-ce que cet algorithme équivaut à générer des permutations alternantes d'Euler? * , pas exactement; Euler , les permutations alternées se réfèrent à des séquences de "up-down" (en augmentant strictement puis en diminuant), alors que nous ne nous soucions ici que de la parité. Autres

---

11. Le référencement et la pensée finale

- **Mots-clés**: *LeetCode Permutations III, permutation alternée, backtracking, solution Java, solution Python, solution C++, algorithme d'entretien, conseils d'entretien d'emploi, interview d'ingénieur logiciel, problème algorithmique, complexité factorielle*.
- **Description détaillée**: Apprenez à résoudre le LeetCode 3437 – Permutations III – avec un retour en arrière. Code Java complet, Python et C++, analyse de complexité et aperçus d'entrevue. Maîtrisez le problème de permutation alternée aujourd'hui !

---

**Takeaway**: La solution est un algorithme propre, basé sur le rétrotraçage, qui respecte une condition de parité simple. C'est une grande vitrine de votre capacité d'adapter un algorithme de permutation classique pour répondre à une contrainte supplémentaire – exactement le genre d'intervieweurs de compétences valeur.

Bon codage ! C'est ce qu'il a dit