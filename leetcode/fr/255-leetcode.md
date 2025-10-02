---
titre: LeetCode 255. Vérifier la séquence de précommande dans l'arbre de recherche binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code Leet 255 – Vérifier la séquence de précommande dans l'arbre de recherche binaire
- Oui. « Bon, mauvais, et ugly » – Un emploi favorable à l'entrevue Plongée

> **Mots clés** – LeetCode 255, Vérifier la séquence de précommande, Recherche binaire Tree, solution O(n), espace constant, interview prep, interview de codage, algorithme, Java, Python, C++.

---

Aperçu du problème

Vous êtes donné un tableau `précommande` de **unique** entiers.
`preorder` est déclaré être un **préorderal** d'un arbre de recherche binaire (BST).
Retourner `true` si la séquence est valide, sinon `faux`.

Exemple Entrée Sortie Pourquoi
- C'est quoi ?
[5,2,1,3,6] `5` → gauche `2` → droite "6"
"[5,2,6,1,3] "" "false"" "1" apparaît après être entré dans le sous-arbre droit de "2" → viole la propriété BST"

**Contrôles* *

- `1 <= précommande.longueur <= 104`
- `1 <= précommande[i] <= 104`
- Toutes les valeurs sont distinctes

**Suivi:** Pouvez-vous le résoudre en utilisant **O(1)** espace supplémentaire?

---

### #2=1 Analyse fondamentale

Une visite de passage précommande **root → gauche → droite**.
Lors de la marche du tableau:

- Oui. Alors que la valeur suivante est **plus petite** que le dernier nœud poussé, vous êtes toujours à l'intérieur de son sous-arbre ** gauche** – il suffit de le pousser.
- Quand la valeur suivante devient **large**, vous marchez **dans un sous-arbre droit**. Tous les nœuds surgissent jusqu'à présent sont des ancêtres dont le sous-arbre droit vous êtes maintenant en visite.
La valeur *dernière popped* devient une liaison ** plus faible** : tout nœud futur doit être **plus grand** que cette liaison.

Cette simple simulation de pile donne un algorithme de temps **O(n)** et une pile d'espace **O(n)**.
L'astuce de suivi est de réutiliser le tableau d'entrée comme la pile pour ramener l'espace à **O(1)**.

---

C'est vrai. Algorithmes et code

##### 3.1 Java – O(n) avec une pile

"Java
solution de classe {
public booléen vérifier Précommande(int[] précommande) {
int lowerBound = entier.MIN_VALUE;
Deque<Integer> pile = nouvelle ArrayDeque<>();

pour (valeur int : précommande) {
si (valeur < valeur inférieureBound) retourne false; // viole la TVB

// Déplacement vers un sous-arbre droit : pop tous les ancêtres plus petits que le courant
pendant que (!stack.isEmpty() && valeur > stack.peek()) {
lowerBound = pile.pop(); // mise à jour liée
}

empil.push(valeur); // rester dans le sous-arbre gauche
}
retour vrai;
}
}
«» "

##### 3.2 Java – O(n) **O(1)** Espace supplémentaire (réutiliser le tableau d'entrée)

"Java
solution de classe {
public booléen vérifier Précommande(int[] précommande) {
int lowerBound = entier.MIN_VALUE;
i = -1; // indice du sommet de la pile simulée

pour (int val : précommande) {
si (val < lowerBound) retourne faux;

pendant que (i >= 0 && val > précommande[i]) { // pop pendant que nous allons à droite
lowerBound = précommande[ i--];
}
précommander[++i] = val; // pousser sur l'emplacement
}
retour vrai;
}
}
«» "

3.3 Python – O(n) avec une liste comme pile

'`python
Solution de classe:
def vérifier Précommander(self, précommander: List[int]) -> bool:
inférieure = flotteur('-inf')
pile = []

pour v en précommande:
si v < inférieur:
Retour Faux
pendant la pile et v > pile[-1]:
inférieure = pile.pop()
pile.append(v)
retour Vrai
«» "

##### 3.4 C++ – O(n) avec un «vecteur» comme pile

'`cpp
solution de classe {
public:
bool vérifier Précommande(vecteur<int>& précommande) {
int plus bas = INT_MIN;
vector<int> pile; // agit comme une pile

pour (int v : précommande) {
si (v < inférieur) retourner faux;
pendant que (!stack.vide() && v > pile.back()) {
inférieur = pile.back();
pile.pop_back();
}
emple.push_back(v);
}
retour vrai;
}
};
«» "

---

Analyse de complexité

L'espace supplémentaire
C'est pas vrai.
Autres Bâton Java **O(n)**
* * * * * * * *
Python **O(n)**
* * * * * * * *

- **Taille de la pile de la plus grande caisse**: `n` (par exemple, tableau ascendant trié → chaque noeud est un enfant gauche).
- **Best-cas**: Croissance constante de la pile pour un arbre équilibré.

---

C'est vrai. Bon, mauvais, et humble

**Aspect**
C'est pas vrai.
**Simplicité conceptuelle**=Utilisez l'idée naturelle de l'emplacement des ancêtres – facile à raisonner. Il faut se souvenir de l'astuce "Lower lied" ; une petite surveillance mène à une mauvaise réponse. La mise en œuvre de l'astuce O(1) nécessite une gestion prudente de l'index ; une erreur peut corrompre le tableau d'entrée. Autres
**Performance** Aucun.
**Readability**La version Stack est auto-explication. La version O(1) est moins évidente pour les débutants; les commentaires sont essentiels. Aucun.
**Tester les cas d'Edge** Autres Toutes les valeurs uniques par contrainte, donc les duplicatas ne sont pas un souci. Si la longueur d'entrée = 1, la logique de la pile fonctionne toujours. Autres
**Utilisation de la production**= Pour les défis d'entrevue ou de codage, la version de la pile est bonne. Dans les environnements critiques de mémoire, utilisez la version O(1).

---

####6--Le suivi – Pourquoi `O(1)` Travaux spatiaux supplémentaires

La clé est que nous n'avons jamais besoin du tableau original après qu'il ait lu.
En traitant les premiers éléments `k` de `précommande` comme une pile, nous évitons d'attribuer un conteneur séparé.
L'algorithme demeure logiquement le même; seule la structure des données est en place.

---

### # 7-

- **Conseil d'entrevue :** Expliquez d'abord la logique de la pile; elle montre que vous comprenez les propriétés de la BST.
- ** Compétence de préparation à l'emploi :** La maîtrise des algorithmes en place et l'optimisation de l'espace démontrent la profondeur.
- **Utilisation pratique :** Des vérifications similaires basées sur la pile apparaissent dans les analyseurs XML/HTML, les évaluateurs d'expression et les validateurs de syntaxe.

> **Rappelez-vous :** Dans une entrevue, "Bon" est "clarité" ; "bad" est "détail de mise en oeuvre" ; "ugly" est "prone logique"*.
> Si vous pouvez parcourir cette solution en moins de 5 minutes et expliquer le tour O(1), vous impressionnerez n'importe quel gestionnaire d'embauche!

---

Autres lectures

- **LeetCode 100 – Même algorithme avec une limite inférieure. **
- **Binary Search Tree – Précommande vs Incommande vs Postcommande. **
- **Optimisation de la complexité spatiale – Algorithmes en place.**

Bon codage, et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit.

---