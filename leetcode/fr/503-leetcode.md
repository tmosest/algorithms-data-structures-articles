---
Titre: LeetCode 503. Suivant Élément II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 503. Prochain grand élément II – Le bon, le mauvais et le mauvais
### (A Job‐Interview Friendly, SEO‐Optimized Guide)

> **Mots-clés**: Prochain grand élément II, LeetCode 503, Array circulaire, Monotonic Stack, Java, Python, C++, Algorithme, Structures de données, Prép d'entrevue, Interview d'emploi

---

TL;DR

- **Problème** : Pour chaque élément d'un tableau entier *circulaire*, trouvez l'élément suivant. Si aucune n'existe, retourner `-1`.
- **Meilleure solution**: **Pile de tono** + ** simulation de deux passages** (temps `O(n)`, espace `O(n)`).
- **Pourquoi c'est important** : la maîtrise de ce modèle montre que vous connaissez *les astuces, *la logique circulaire* et *les algorithmes optimaux* – tous très appréciés dans les entrevues de codage.

---

Déclaration de problème (Code de bord 503)

> **Don** un tableau entier circulaire `nums` (l'élément après le dernier est le premier).
> **Retour** un tableau où chaque position contient le nombre ** suivant plus grand** de l'élément correspondant.
> Si aucun élément plus grand n'existe, mettez `-1`.

> **Exemple**
> `nums = [1, 2, 1] → [2, -1, 2]`

---

L'Algorithme optimal

####=== Stack monotonique

Une pile qui maintient les indices dans **decreasing** ordre de leurs valeurs.
Tandis qu'il est itératif, nous pop éléments plus petits ou égaux — ceux-ci ne peuvent jamais être le prochain plus grand pour un indice futur.

Simulation de deux passes

Comme le tableau est circulaire, nous itérerons *deux fois* sur les indices (ou utilisons l'arithmétique modulo).
- Premier passage : remplir la pile pour la dernière partie du tableau.
- Deuxième passe : terminer la première partie en utilisant la même logique de pile.

C'est vrai. Complexité

Java / Python / C++
-- -- -- -- -- -- -- -- --
Heure **O(n)** Autres
Espace **O(n)** (pile + résultat)

---

"Le "Bad" : Brute- Approche de la force

"Java
int[] res = nouvelle int[n];
pour (int i = 0; i < n; ++i) {
int suivante = -1;
pour (int j = 1; j <= n; ++j) { // scanner toutes les positions
idx = (i + j) % n;
si (nums[idx] > nombres[i]) {
suivant = nombres[idx];
pause;
}
}
res[i] = suivant;
}
«» "

- **Heure**: «O(n2)» - inacceptable pour «n = 104».
- **Espace**: `O(1)` – mais le coût énorme du temps l'emporte.

---

Les pièges communs

Ce qui arrive
- C'est quoi ?
**Utiliser `Stack<Integer>` (Java)**= `Stack` est synchronisé; frais généraux.= Utiliser `ArrayDeque<Integer>` ou `IntStack` pour les performances. Autres
**Ne pas manipuler les duplicata** Obtenir une mauvaise comparaison (`<=` vs `<`). Obtenir `<=` pour sauter des éléments égaux; sinon, vous pourriez manquer le correct suivant plus. Autres
**Modulo mauvais usage** Il faut passer de `2*n - 1` jusqu'à `0` et toujours utiliser `i % n` pour cartographier en arrière. Autres
Autres **Space sleep**. Oubliez de nettoyer la pile avant de la réutiliser. Effacer ou réinitialiser pour chaque cas d'essai. Autres

---

Les solutions de code

Voici des implémentations propres et prêtes à la production pour **Java, Python et C++**.

---

### Java (optimisé avec `ArrayDeque`)

"Java
Importer java.util. - ArrayDeque;

solution de classe publique {
int.[] suivanteGrands éléments(int[] nombres) {
int n = longueur nums;
int[] res = nouvelle int[n];
ArrayDeque<Integer> pile = nouvelle ArrayDeque<>();

pour (int i = 2 * n - 1; i >= 0; --i) {
int idx = i % n;
pendant que (!stack.isEmpty() && nums[stack.peek()] <= nums[idx]) {
pile.pop();
}
res[idx] = empil.isEmpty() ? -1 : nombres[stack.peek()];
le point d'entrée est remplacé par le texte suivant:
}
retour rés;
}
}
«» "

---

### Python (utiliser `list` comme une pile)

'`python
de taper l'importation Liste

Solution de classe:
def nextGreaterElements(self, nombres: List[int]) -> Liste[int]:
n = len(nums)
res = [-1] * n
pile : Liste[int] = []

pour i dans l'intervalle(2 * n - 1, -1, -1):
idx = i % n
pendant la pile et les nombres[stack[-1]] <= nombres[idx]:
Pile.pop()
si pile:
res[idx] = nombres[stack[-1]]
Annexe(idx)
retour res
«» "

---

C++ (En utilisant `std::vector` et `std::stack`)

'`cpp
#incluez <vecteur>
#incluez <stack>

solution de classe {
public:
std::vector<int> nextGreaterElements(std::vector<int>& nums) {
int n = nombres.size();
à:vecteur<int> res(n, -1);
std::stack<int> st; // indices

pour (int i = 2 * n - 1; i >= 0; --i) {
int idx = i % n;
pendant que (!st.vide() && nums[st.top()] <= nums[idx]) st.pop();
si (!st.vide()) res[idx] = nombres[st.top()];
un push st (idx);
}
retour rés;
}
};
«» "

---

L'exécution du code

### Java

"""
Javac Solution.java
java Solution
«» "

Python

"""
python -c "print(_import_('collections').deque()"
«» "

C++

"""
g++ -std=c++17 solution.cpp -o solution
./solution
«» "

> Remplacer la fonction `principale` par des cas d'essai au besoin.

---

Pourquoi cela compte dans les entrevues

1. **La pensée algorithmique** – montre que vous pouvez réduire `O(n2)` à `O(n)` en tirant parti des propriétés de la structure des données.
2. **Comprendre la logique circulaire** – De nombreux problèmes d'entrevue cachent une torsion de l'erreur.
3. **Maîtrise des piles** – Les piles monotoniques sont un élément essentiel des entrevues quotidiennes de codage.
4. ** Échanges entre le temps et l'espace** – Vous impressionnerez les intervieweurs en expliquant clairement la complexité.

---

Description de la méta

> Découvrez comment résoudre LeetCode 503 – Next Greater Element II – avec les solutions Java, Python et C++. Pile monotonique maître, logique de tableau circulaire, et optimiser votre préparation d'entrevue. (en milliers de dollars)

---

Liste de contrôle avant votre prochaine entrevue

- [ ] Comprendre ** tableau circulaire** l'indexation ('(i + 1) % n').
- [ ] Connaître la pile **monotonique** invariante.
- [ ] Écrire la solution **en deux passages** ou en utilisant le modulo.
- [ ] Expliquer clairement ** la complexité temps/espace**.
- [ ] Discutez des écueils communs (duplicata, mise en œuvre de la pile).

---

Autre lecture

- Problème de LeetCode 503 : [Prochain élément II](https://leetcode.com/problèmes/next-great-element-ii/)
- Patte monotonique:
- GeeksforGeeks : Empilement monotonique
- InterviewBit: -Suivant Grand Élément
- Techniques de représentation circulaire :
- Array Wrapping Tricks – Article moyen
- Tableau circulaire à deux points – HackerRank

---

La pensée finale

La maîtrise de l'élément II suivant est plus que la résolution d'un seul problème de LeetCode.
Il s'agit de montrer que vous pouvez **reconnaître un motif** (circulaire + prochain plus grand), **appliquer la bonne structure de données** (pile monotonique), et ** optimiser le temps et l'espace**.
Ces compétences se traduisent directement par des défis de codage réels et font de vous un candidat exceptionnel lors de toute entrevue technique. Bonne chance ! C'est ce qu'il a dit