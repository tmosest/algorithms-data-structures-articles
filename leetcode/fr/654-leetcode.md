---
titre: LeetCode 654. Arbre binaire maximum -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Arbre binaire maximum – Le bon, le mauvais, et le mauvais
**LeetCode 654 – Une plongée profonde dans l'algorithme Pensée* *

---

Table des matières

Ce que vous apprendrez
- Oui.
Remarque sur le problème Comprendre le défi et les contraintes
Approche naïve Autres
Récursion classique – clair mais lent
Solution optimale O(n)
Le temps et la complexité de l'espace
Faites votre code à l'épreuve des balles
Éviter les erreurs les plus fréquentes
Pourquoi maîtriser ceci est important pour les entrevues
D'autres ressources D'approfondir vos connaissances

> **SEO Mots-clés**: *Maximum Binary Tree, LeetCode 654, algorithme, pile monotonique, construction d'arbre, prep interview, solution Java, solution Python, solution C++, diviser et conquérir, complexité temporelle, complexité spatiale. *

---

## 1-

> **Arbre binaire maximal**
> Vous êtes donné un tableau `nums` d'entiers distincts.
> Construire un arbre binaire en utilisant les règles suivantes :
> 1. La racine est l'élément maximum de "nums".
> 2. Le sous-arbre gauche est l'arbre binaire maximal du sous-aire gauche du max.
> 3. Le sous-arbre droit est l'arbre binaire maximal du sous-aire droit du max.

Retourner le nœud racine de l'arbre construit.

> **Constraints**
> * `1 ≤ longueur nominale ≤ 1000`
> * `0 ≤ nombres[i] ≤ 1000`
> * Tous les nombres entiers sont uniques.

---

- Oui. Approche naïve – Force brute

La solution la plus simple reflète la description:

Texte
trouver l'indice maximum en nombres
créer un noeud avec cette valeur
récurse sur la tranche gauche
récurse sur la tranche droite
«» "

Complexité
* Trouver le maximum* prend `O(k)` où `k` est la longueur de la tranche.
A chaque niveau, nous partitionnons le tableau, donc le travail total devient

«» "
T(n) = T(k1) + T(k2) + O(n) -> O(n2)
«» "

Pour `n = 1000`, c'est encore très bien pour LeetCode, mais il devient rapidement inévoluable et une interview classique.

---

## 3-- Diviser & Conquer – Récursif O(n2) Solution

Une implémentation plus propre utilise la récursion avec un helper qui accepte une plage d'index.

"Java
solution de classe {
public TreeNode constructionMaximBinaryTree(int[] nums) {
aide au retour(nums, 0, nombres.longueur - 1);
}
aide privée TreeNode(int[] nombres, int l, int r) {
si (l > r) retourne null;
Int maxIdx = l;
pour (int i = l + 1; i <= r; i++)
si (nums[i] > nombres[maxIdx]) maxIdx = i;
TreeNode noeud = nouveau TreeNode(nums[maxIdx]);
noeud.left = aide(nombres, l, maxIdx - 1);
noeud.right = assistant(nums, maxIdx + 1, r);
noeud de retour;
}
}
«» "

> **Le Bon** – *Clear, concis, et correspond parfaitement à la description du problème. *
> **Le mauvais** – *Temps complexe `O(n2)`. *
> **L'Ugly** – *Les balayages linéaires répétés, l'utilisation inutile de la mémoire et la profondeur de la pile peuvent exploser pour de plus grandes entrées. *

---

## 4-- Stack monotonique – L'O(n) Optimal Solution

- Oui. La perspective clé

Tout en construisant l'arbre, **l'ordre relatif des éléments est ce qui compte**.
Lorsque vous traitez `nums` de gauche à droite, vous devez seulement connaître l'élément **dernier plus grand** – l'élément qui deviendra le parent du nœud actuel.

Une pile **monotonique décroissante** maintient des nœuds dont les valeurs diminuent strictement de bas en haut.
Quand une nouvelle valeur `x` arrive :

1. Tous les nœuds de la pile avec la valeur `< x` deviennent l'enfant *left* de `x`.
2. Si la pile n'est pas vide après l'apparition, le nouveau haut *enfant droit* devient `x`.
3. Poussez `x` sur la pile.

A la fin, le **bottom de la pile** est la racine de l'arbre binaire maximum.

Complexité
*Chaque noeud est poussé et sauté au plus une fois* → **'O(n)' temps**.
Espace de rangement: **'O(n)'**.

Mise en œuvre de Java (Manotonic Stack)

"Java
solution de classe {
public TreeNode constructionMaximBinaryTree(int[] nums) {
si (nombres) null (longueur) num) 0) retour nul;

Deque<TreeNode> pile = nouvelle ArrayDeque<>();

pour (int num : nombres) {
TreeNode cur = nouveau TreeNode(num);

// Tous les nœuds avec plus petite valeur deviennent l'enfant gauche de cur
pendant que (!stack.isEmpty() && stack.peek().val < num) {
cur.left = pile.pop();
}

// Le haut actuel (s'il existe) devient l'enfant droit
si (!stack.isEmpty()) {
empil.peek().right = cur;
}

Le point d'entrée est remplacé par le texte suivant:
}

// Le bas de la pile est la racine
retour pile.peekLast();
}
}
«» "

> **Le Bon** – *Run dans le temps linéaire et est facile à comprendre une fois que l'idée de pile surfaces. *
> **La mauvaise** – *Courbe d'apprentissage initiale; la manipulation de la pile peut être sujette à erreur. *
> **L'Ugly** – *Dans les langues sans types de piles intégrés (p. ex., C), vous devez gérer manuellement les pointeurs. *

Mise en œuvre de Python (Manotonic Stack)

'`python
de taper l'importation Liste, facultative

classe TreeNode:
def __init_(self, val: int = 0, gauche: 'TreeNode' = Aucune, droite: 'TreeNode' = Aucune):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def constructionBinaire maximal Tree(self, nombres: List[int]) -> Facultatif[TreeNode]:
pile = []
pour num in nums:
noeud = TreeNode(num)
pendant la pile et la pile[-1].val < num:
noeud.left = pile.pop()
si pile:
pile[-1].right = noeud
pile.append(node)
retourner la pile[0] si la pile n'est pas
«» "

### C++ Mise en œuvre (Manotonic Stack)

'`cpp
struct TreeNode {
la valeur intérieure;
TreeNode *left, *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

solution de classe {
public:
TreeNode* construireMaximumBinaryTree(vector<int>& nums) {
vecteur <TreeNode*> m;
pour (int num : nombres) {
TreeNode* noeud = nouveau TreeNode(num);
pendant que (!st.vide() && st.back()->val < num) {
noeud->gauche = st.back();
le _retour_st.pop();
}
si (!st.vide())
st.back()->right = noeud;
st.push_back(node);
}
retour st.vide() ? nulptr : st.front();
}
};
«» "

---

## 5-

Autres Description de l'essai
- C'est quoi ?
"[]"" Tableau vide ""
Élément unique Autres
"TreeNode(5)" avec tous les enfants gauches
"[5,4,3,2,1]""Décroissant strictement" "TreeNode(5)" avec tous les enfants droits"
"[3,2,1,6,0,5]"" Mixte" "TreeNode(6)" avec des sous-arbres par exemple

**Astuce**: Utilisez un helper pour traverser l'arbre et le sérialiser en tableau (ordre de niveau) pour comparer avec la sortie attendue de LeetCode.

---

## 6-

Pourquoi il échoue
- C'est quoi ?
Autres ** État de la pile de défauts** (`<=` au lieu de `<`) Les valeurs dupliquées ne sont pas autorisées, mais l'utilisation de `<=` peut faire apparaître trop de nœuds.
**Pas de réglage `left` après le saut**Le nœud poppé devient l'enfant *right* incorrectement. Attribuer `cur.left = poppedNode` dans la boucle. Autres
Autres **Returning the wrong empilement element**.Returning `stack.peek()` donne le nœud le plus récent, pas la racine. Retour `stack.peekLast()` (fond de la pile). Autres
Autres **Les fuites de mémoire dans C++** Utilisez des pointeurs intelligents (`std::unique_ptr`) ou un destructeur. Autres
**La solution récursive utilise la profondeur de la pile `O(n)`. Autres

---

C'est pas vrai. Pourquoi maîtriser Ce qui compte

* **L'esprit algorithmique** – Transformer une description en une structure de données efficace est une compétence d'entrevue de base.
* ** Fluence de la structure des données** – Les arbres binaires et les piles monotoniques sont des sujets d'entrevue fréquents.
* **Les compromis entre l'espace-temps** – Être capable de repérer la partie quadratique et l'améliorer démontre la profondeur de résolution des problèmes.
* ** Polyvalence en langage brut** – Vous impressionnerez les recruteurs si vous pouvez résoudre le même problème en **Java, Python et C++** (ou toute autre langue que vous aimez).

> **Traitement de la carrière**:
> *LeetCode 654 est un problème de cas de présentation – il semble facile, mais la solution optimale cache un motif subtil.
> Résoudre avec élégance vous donnera un coup de pouce pour les entrevues sur la structure des données et vous aidera à établir des rôles qui valorisent le code propre et efficace. *

---

Autres ressources

1. **Monotonic Stack Pattern** – *LeetCode discussion thread*
2. **Construction d'arbres récursifs** – *CS‐Academy="Construire l'arbre de précommande et d'ordre*
3. ** Gestion de mémoire en C++** – *=Unique_ptr et pointeurs intelligents sur GeeksforGeeks*
4. **Interview Prep Books** – *=Cracking the Coding Interview==– Chapitre sur les arbres binaires et la pile*
5. **YouTube Walk-through** – *Ben Awad="Stickers de musique (Python + JavaScript)*

---

Dernier départ

> *L'arbre binaire maximal est un problème trompeur simple qui récompense une perspicacité algorithmique plus profonde. *
> En passant d'une analyse de force brute à une pile **monotonique**, vous transformez une solution `O(n2)` en une solution propre `O(n)` qui se démarquera dans les entrevues.

Continuez à pratiquer le modèle – il apparaît dans d'autres problèmes de LeetCode comme **. Maîtriser cette idée est une petite étape qui peut élever l'ensemble de vos compétences d'entrevue de codage.

Bonne chance, et le codage heureux! C'est ce qu'il a dit