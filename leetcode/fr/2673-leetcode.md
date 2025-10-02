---
titre: LeetCode 2673. Faire des coûts de chemins égaux dans un arbre binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Faire des coûts de chemins égaux dans un arbre binaire – 2673 (LeetCode)

> **Titre:** Faire des coûts de chemins égaux dans un arbre binaire – Java/Python/C++ Solutions
> **Méta—description:** Résoudre le LeetCode 2673 Faire des coûts de chemins égaux dans un arbre binaire en temps O(n). Lisez notre tutoriel DFS bottom-up, des extraits de code pour Java, Python & C++, ainsi qu'une analyse « good‐bad‐ugly» pour la préparation des interviews.

---

- Oui. 1. Exposé des problèmes

On vous donne un arbre binaire parfait avec des nœuds `n` (1-based indexing).
La racine est le noeud `1`, et pour tout noeud `i` l'enfant gauche est `2*i` et l'enfant droit est `2*i+1`.

`cost[i]` (0-based array) détient le coût du nœud `i+1`.
Vous pouvez **incrément** le coût de tout noeud par `1` n'importe quel nombre de fois.
**Objectif :** Faire en sorte que le coût total de chaque chemin racine-feuille soit égal en utilisant le nombre minimum d'augmentations.

Retourne ce nombre minimum d'augmentations.

> **Exemples**
> 1. `n = 7, coût = [1,5,2,2,3,3,1]` → **6**
> 2. `n = 3, coût = [5,3,3]` → **0**

> **Constraints**
> * `3 ≤ n ≤ 10^5`
> * `n + 1` est une puissance de 2 (arbre binaire parfait)
> * `1 ≤ coût[i] ≤ 10^4`

---

- Oui. 2. Intuition et principales perspectives

Un arbre binaire parfait est *level-ordered*.
Si nous regardons n'importe quel noeud intérieur, ses deux enfants finissent par conduire à deux chemins de feuilles.
Laissez :

«» "
gauche Coût – coût total minimal de l'enfant gauche à n'importe quelle feuille
droite Coût – coût total minimal de l'enfant droit à toute feuille
«» "

Pour que les deux chemins soient égaux, nous devons élever le sous-arbre moins cher pour correspondre au cher.
Le coût de cette opération est `abs(leftCoost - leftCoost)`.

Après avoir aligné les enfants, le coût de chemin minimal actuel du nœud devient:
«» "
coût[noeud] + max(gaucheCoût, droitCoût)
«» "
parce que nous choisissons l'enfant plus lourd comme base pour le niveau supérieur.

Ainsi le problème peut être résolu *bottom-up* ou *recursivement* par DFS.
Les deux approches ont **O(n)** de temps et **O(1)** d'espace auxiliaire (ignorant la pile de récursion).

---

- Oui. 3. Solution itérative ascendante (C++, Java, Python)

3.1 Algorithme

1. Itérer du dernier noeud interne (`n/2 - 1`) jusqu'à la racine (`0`).
2. Pour le noeud `i` (0-based index):
* `l = 2*i + 1` (indice de gauche pour l'enfant)
* `r = 2*i + 2` (indice de l ' enfant droit)
* "incréments +===Cost[l] - coût[r]= "
* `cost[i] += max(cost[l], cost[r])` // mise à jour au coût de chemin minimal à partir du nœud ` Les "
3. Retour `incréments`.

3.2 Complexité

Opération Temps Espace
- C'est quoi ?
Loop au-dessus des noeuds internes **O(n)**
Pile de récursion (variante DFS)

3.3 Extraits de code

C'est vrai. Java

"Java
solution de classe {
Int minIncrements(int n, coût int) {
long res = 0; // utiliser longtemps pour éviter le débordement pour les grands n
pour (int i = n / 2 - 1; i >= 0; i--) {
Int l = 2 * i + 1;
= 2 * i + 2;
res += Math.abs(cost[l] - cost[r]);
coût[i] += Math.max(cost[l], coût[r]); // propagation coût minimal à la hausse
}
retour (int) rés;
}
}
«» "

Python 3

'`python
Solution de classe:
def minIncrements(self, n: int, coût: List[int]) -> Int:
Res = 0
pour i dans la plage(n // 2 - 1, -1, -1):
l = 2 * i + 1
r = 2 * i + 2
res += abs(cost[l] - cost[r])
coût[i] += max(cost[l], coût[r]) # mise à jour au coût de chemin minimal
retour res
«» "

C++

'`cpp
solution de classe {
public:
Int minIncrements(int n, vecteur<int>& coût) {
long res = 0; // long pour éviter le débordement
pour (int i = n / 2 - 1; i >= 0; --i) {
Int l = 2 * i + 1;
= 2 * i + 2;
res += abs(coût[l] - coût[r]);
coût[i] += max(cost[l], coût[r]); // propagation vers le haut
}
retourner static_cast<int>(res);
}
};
«» "

---

- Oui. 4. Variante récursive du DFS

Si vous préférez une implémentation récursive *clean*, la logique reste la même ; la seule différence est que nous calculons les coûts des enfants à la volée.

C'est vrai. Java

"Java
solution de classe {
Rés privée longue = 0;

Int minIncrements(int n, coût int) {
dfs(0, coût);
retour (int) rés;
}

dfs(int i, coût int[]) {
si (i >= coût.longueur) retourner 0; // feuille
Int gauche = dfs(2 * i + 1, coût);
Int droite = dfs(2 * i + 2, coût);
res += Math.abs(gauche - droite);
coût de retour[i] + Math.max(gauche, droite);
}
}
«» "

Python

'`python
Solution de classe:
def minIncrements(self, n: int, coût: List[int]) -> Int:
autorés = 0
def dfs(i):
i >= len(coût): retourner 0
l, r = dfs(2 * i + 1), dfs(2 * i + 2)
auto.res += abs(l - r)
Coût de retour[i] + max(l, r)
dfs(0)
Revenez vous-même. rés
«» "

C++

'`cpp
solution de classe {
public:
long an = 0;
int dfs(int i, vecteur<int>& coût) {
si (i >= cost.size()) retourne 0;
Int gauche = dfs(2 * i + 1, coût);
Int droite = dfs(2 * i + 2, coût);
ans += abs(gauche - droite);
coût de retour[i] + max(gauche, droite);
}

Int minIncrements(int n, vecteur<int>& coût) {
dfs(0, coût);
retourner static_cast<int>(ans);
}
};
«» "

---

- Oui. 5. Bon – Mauvais – Ugly , Analyse d'entrevue

Ce que vous devriez montrer Ce qui peut aller mal Comment l'éviter
-- -- -- -- -- -- -- -- -- -- -- -- -- --
** Bon** • Algorithme du temps linéaire (O(n)).<br>• Incréments minimaux dérivés de sous-arbres alignants.<br>• Bas-up ou DFS à la fois simple à coder.
**Bad**) • La mauvaise interprétation de l'arbre comme *non parfait* conduit à des erreurs d'index.<br>• L'utilisation de `int` pour la réponse peut déborder lorsque `n` 105. Valider l'existence d'indices pour enfants (`l, r < n`).
**Essayez de forcer tous les incréments possibles (exponentielle).<br>• Recalculer récursivement les coûts de l'enfant à partir de zéro à chaque noeud (O(n log n) si vous ne cachez pas).

- Oui. Pourquoi le modèle ascendant est une étoile dans les entrevues

1. **Clarté** – L'algorithme se lit comme une simple boucle; les intervieweurs peuvent voir la logique immédiatement.
2. **Problème de la conformité** – L'invariant "Coût" stocke le coût minimal du trajet du noeud `i` à n'importe quelle feuille est maintenu à chaque itération.
3. **Mémorie** – Les mises à jour en place évitent les tableaux supplémentaires; si la récursion est utilisée, la profondeur de la pile est seulement `log n` pour un arbre binaire parfait.
4. **Extension** – Le même modèle fonctionne pour la variante de suivi où vous pouvez *décret* aussi bien, en remplaçant simplement `abs` par `max(0, leftCost - leftCost)`.

---

- Oui. 6. Liste de contrôle des cas de bord

Pourquoi ça compte ?
- Oui.
`n` est juste le minimum (3). Autres
Autres Tous les coûts sont déjà égaux. Aucun cas particulier n'est nécessaire. Autres
Autres Très grand `n` (=105)= Potentiel de débordement 32 bits= Utiliser 64 bits (=`long`/`long`) pour `res`. Autres

---

- Oui. 7. Variante: Augmentation **ou** Décret

Si l'énoncé du problème a été modifié pour permettre à la fois des augmentations et des diminutions, la stratégie optimale change légèrement:

* Nous élèverions le sous-arbre moins cher ** jusqu'à** le plus lourd, *et* nous pourrions éventuellement baisser le plus lourd si cela mène à un nombre d'accroissements total inférieur.
* Cela réduit à ** faire les deux sous-arbres égal au maximum de leurs coûts de trajet minimum**, ce qui donne le même coût `abs(leftCoût - droitCoût)`.
* Le reste de la logique reste identique; seule l'interprétation de l'opération change.

---

- Oui. 8. A emporter pour votre prochaine entrevue de codage

* **LeetCode 2673** est un problème classique O(n)** arborescence-DP qui teste:
1. La traversée de l'arbre (DFS ou bas-up).
2. Travailler avec des représentations implicites d'arbres.
3. Penser en termes d'invariants *sous-problème* et de propagation*.

* La maîtrise de ce modèle démontre :
* **Clean, code sans bug** (la logique de base de 3 lignes).
* **Utilisation efficace de l'espace** (mises à jour en place).
* **Le raisonnement mathématique** (alignement des coûts, différences absolues).

* **L'utiliser dans votre préparation d'entrevue**:
* Ecrivez d'abord la version itérative – c'est facile à expliquer.
* Mentionnez la version récursive – les intervieweurs aiment voir les deux perspectives itératives et récursives.
* Mettre en évidence l'espace auxiliaire O(n) time & O(1) pour impressionner l'efficacité.

---

- Oui. 9. Dépôt de codes complet

Les trois implémentations linguistiques sont disponibles dans cette repo GitHub:

Texte
https://github.com/votre-nom d'utilisateur/codeleet-2673-cost-path
«» "

N'hésitez pas à copier, à adapter et à ajouter des tests unitaires.

---

10. Clôture

Résoudre **LeetCode 2673** avec un DFS ascendant non seulement vous rapporte un score parfait sur la plateforme, mais met également en valeur votre capacité à:

* Traduire un problème en un invariant propre.
* Optimisez le temps et l'espace.
* Écrire un code concis, prêt à la production en Java, Python ou C++.

Ajoutez ce problème à votre liste de lecture de la préparation d'entrevues, et vous serez bien préparé pour tout tour de structure de données qui implique ** arbres binaires** et **ajustement des coûts** logique.

Bonne chance, et le codage heureux!