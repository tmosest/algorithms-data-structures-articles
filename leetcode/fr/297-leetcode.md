---
Titre: LeetCode 297. Sérialiser et désérialiser l'arbre binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Serialize & Desérialize Arbre binaire – Solution en trois langues

Voici trois implémentations prêtes à coller qui passeront le LeetCode 297.
Les trois utilisent la stratégie *précommande* (DFS) – nous visitons le nœud, puis le sous-arbre gauche, puis le sous-arbre droit.
Les nœuds `null` sont encodés comme la chaîne `"null"` et séparés par des virgules.
Lors de la désérialisation, nous lisons les valeurs d'une liste (ou d'un flux de chaînes) dans le même ordre, reconstruisant l'arbre de façon récursive.

---

#### 1.1 Java

"Java
Importation de java.util.*;

// Définition pour un nœud binaire.
classe TreeNode {
la valeur intérieure;
TreeNode gauche;
TreeNode droit;
TreeNode(int x) { val = x; }
}

Classe publique Codec {

- Oui. Code -------- */
chaîne publique sérialise (racine TreeNode) {
StringBuilder sb = nouveau StringBuilder();
buildString(racine, sb);
retour sb.toString();
}

construction privée videString(NodeTreeNode, StringBuilder sb) {
si (noeud == null) {
sb.append("null",");
retour;
}
sb.append(node.val).append(',');
buildString(node.left, sb);
buildString(node.right, sb);
}

- Oui. Décoder -------- */
public TreeNode désérialize(données de positionnement) {
si (data.isEmpty()) retourne null;
Chaîne[] vals = data.split(",");
Queue<String> q = nouvelle liste liée<>(Arrays.asList(vals));
construction de retourTree(q);
}

construction privée TreeNodeTree(Queue<String> q) {
val chaîne = q.poll();
si (val.equals("null") retourne null;
TreeNode noeud = nouveau TreeNode(Integer.parseInt(val));
noeud.left = buildTree(q);
noeud.right = buildTree(q);
noeud de retour;
}
}
«» "

> **Test sur LeetCode**
> ``java
> Codec ser = nouveau Codec();
> Codec des = nouveau Codec();
> racine TreeNode = nouveau TreeNode(1);
> root.left = nouveau TreeNode(2);
> root.right = nouveau TreeNode(3);
> root.right.left = nouveau TreeNode(4);
> root.right.right = nouveau TreeNode(5);
> Données de chaîne = ser.serialize(root);
> TreeNode copy = des.désérialize(données);
> // copie représente maintenant l'arbre original
> `` "

---

#### 1.2 Python

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init_(self, x):
autoval = x
auto.gauche = Aucune
soi.right = Aucune

classe Codec:
Oui. Encoder ------------------
def serialize(self, root: TreeNode) -> str:
"""Encode un arbre à une seule chaîne."""
out = []
auto_dfs(root, out)
retour ','.join(out)

def _dfs(self, node: TreeNode, out: list):
si le nœud n'est pas :
out.append('null')
retour
out.append(str(node.val))
Self._dfs(node.left, out)
Self._dfs(node.right, out)

Oui. Décoder ------------------
def desérialize(self, data: str) -> Numéro d'arbre:
"""Décode vos données codées à l'arborescence."""
si ce n'est pas des données:
retour Aucune
vals = data.split(',')
auto.idx = 0
return self._build(vals)

_build(self, vals: list) -> Numéro d'arbre:
Si vals[self.idx] == 'null':
Auto.idx += 1
retour Aucune
noeud = TreeNode(int(vals[self.idx])
Auto.idx += 1
noeud.left = self._build(vals)
noeud.right = self._build(vals)
noeud de retour
«» "

> **Utilisation**
> ``python
> codec = Codec()
> arbre = arbreNode(1)
> arbre.left = arbreNode(2)
> arbre.right = TreeNode(3)
> sérialisé = codec.serialize(tree)
> désérialisé = codec.désérialisé(sérialisé)
> `` "

---

*## 1.3 C++

'`cpp
#incluez <string>
#incluez <sstream>
#incluez <queue>

/* Définition d'un noeud d'arbre binaire. */
struct TreeNode {
la valeur intérieure;
TreeNode *gauche;
TreeNode *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

Codec {
public:
- Oui. Code -------- */
chaîne serialize(TreeNode* root) {
les chaînes de caractères;
dfs(racine, ss);
retour ss.str();
}

vide dfs(nœud TreeNode*, chaîne de caractères &ss) {
Si (!noeud) {
ss << null,;
retour;
}
ss << noeud->val << ',';
dfs(node->gauche, ss);
dfs(node->right, ss);
}

- Oui. Décoder -------- */
TreeNode* désérialise(chaîne de caractères et données) {
si (data.vide()) retourne nullptr;
file d'attente <string> q;
jeton à chaîne;
stringstream ss(données);
pendant que (veuillez indiquer, jeton, ',') {
q.push(token);
}
construction de retourTree(q);
}

TreeNode* buildTree(queue<string> &q) {
chaîne val = q.front(); q.pop();
si (val == "null") retourner nulptr;
TreeNode* noeud = nouveau TreeNode(stoi(val));
noeud->gauche = buildTree(q);
noeud->droit = buildTree(q);
noeud de retour;
}
};
«» "

> **Exemple**
> ``cpp
> Codec;
> TreeNode *root = nouveau TreeNode(1);
> root->left = nouveau TreeNode(2);
> root->right = nouveau TreeNode(3);
> chaîne s = codec.serialize(root);
> TreeNode *copy = codec.désérialize(s);
> `` "

---

- Oui. 2. Article de blog – Serialize & Deserialize Binary Tree: The Good, The Bad et The Ugly

> **Meta Titre**: Serialize & Desérialize Arbre binaire – LeetCode 297 expliqué (Java, Python, C++)
> **Meta Description**: Master LeetCode 297 – sérialiser & désérialiser l'arbre binaire. Lisez notre plongée profonde, des échantillons de code en Java, Python, C++, et des informations prêtes à l'interview.

2.1 Introduction

Lors d'une entrevue pour un rôle d'ingénierie logicielle, **LeetCode 297 – Serialize and Desérialize Binary Tree** est une question fréquente. Le problème vous oblige à penser **tree traversal**, **string manipulation**, et **récursion** – compétences de base que les gestionnaires d'embauche aiment voir.

Dans ce post, nous allons disséquer le problème, explorer pourquoi la solution DFS pré-commande est élégante, montrer le code prêt-à-coller en **Java, Python et C++**, puis parler des aspects **good**, **bad** et **ugly** que les intervieweurs sondent souvent.

> **Mots-clés**: sérialisation de l'arbre binaire, désérialisation de l'arbre binaire, LeetCode 297, DFS, pré-commande transversale, prép d'entrevue, interview de codage, sérialisation d'arbre binaire, Java, Python, C++.

---

2.2 Récapitulation du problème

> **Donné** d'un arbre binaire, *sérialisez-le* dans une chaîne pour qu'elle puisse être transmise ou stockée.
> **Donné** de la chaîne, *désérialisez-la* dans la structure originale de l'arbre.

**Contrôles* *

* 0 ≤ noeuds ≤ 104
* Valeurs des nœuds [–1000, 1000]

La sérialisation canonique LeetCode utilise des virgules et le mot `"null"` pour les enfants vides. Mais le problème permet explicitement *toute* format de sérialisation qui est invertible. Cela nous donne une liberté créative.

---

#### 2.3 Pourquoi le DFS pré-commande fonctionne si bien

1. **Déterministe** – L'ordre -node, gauche, droite , garantit que pendant la désérialisation nous savons toujours si nous créons un enfant gauche ou droit.
2. **Récursion simple** – Un seul assistant récursif construit la chaîne; un autre aide consomme la liste pour reconstruire l'arbre.
3. **Linear Time & Space** – Chaque noeud est traité exactement une fois ; la longueur de chaîne résultante est O(n).

2.3.1 Manipulation "null" "

Il est crucial d'utiliser le jeton « null » pour les enfants absents. Sans cela, l'algorithme serait ambigu : étant donné "1,2,3", c'est l'arbre :

«» "
1
/
2
Autres
3
«» "

ou

«» "
1
Autres
2
Autres
3
«» "

La "null" les jetons brisent l'ambiguïté:

«» "
1,2,null,3,null,null,null
«» "

Maintenant, la structure est unique.

---

2.4 Le code – une rapide traversée

Principales étapes Faits saillants Autres
C'est quoi ?
**Java**= `StringBuilder` + récursion pour `serialize`; `Queue<String>` pour `desérialize`= Utilise une file d'attente pour consommer des valeurs dans l'ordre. Autres
**Python**= List and index pointer for `serialize`; recursive `desérialize`== Élégant index-tracking sans bibliothèques externes. Autres
**C++**="stringstream" pour la chaîne de construction; `queue<string>` pour l'analyse="Memory-efficace avec `std::queue`. Autres

Les trois implémentations partagent le même squelette algorithmique, assurant une complexité cohérente temps/espace:

* **Heure**: O(n) – chaque noeud visité une fois.
* **Espace**: O(n) – chaîne de sortie + pile de récursion ou file d'attente.

---

2.5 Les bonnes – Pourquoi Cette solution est Interview‐ Amiable

1. **Clarité** – Récursion reflète l'énoncé du problème; un candidat peut expliquer chaque ligne.
2. **Robustness** – Fonctionne pour des arbres équilibrés ou biaisés; gère jusqu'à 104 nœuds sans débordement de la pile (profondeur de récursion : 104 est très bien pour Java/Python; C++ peut avoir besoin d'une récursion de queue ou de DFS itérative si la profondeur de la pile est préoccupante).
3. **Échelle** – L'algorithme s'étend naturellement aux arbres *n‐ary* si nous changeons le séparateur.
4. **Readability** – Des méthodes d'aide propres (`buildString` / `_dfs`) isolent la logique.

---

#### 2.6 Les mauvais – échange et gotchas

Qu'est-ce qui se passe ?
- C'est quoi ?
Pour un arbre binaire complet, la chaîne sérialisée contient 2n + 1 jetons `"null"`, qui peuvent être ~20 KB pour n = 104. Autres
**Parsage répété**=Le fractionnement de la chaîne (`data.split(',')') crée une liste de tailles n.= Les intervieweurs peuvent demander un décodeur *in-place* basé sur le flux. Autres
**Emplacement récursif**= Des arbres profondément déséquilibrés peuvent atteindre des limites de profondeur de récursion en Python ou causer un débordement de la pile en C++. Autres
**La conversion `stoi` / `int()` se produit pour chaque nœud. Pas significatif pour 104 nœuds, mais à noter pour les micro-optimisations. Autres

*Conseil pour les intervieweurs:* Si vous voulez montrer une compétence *avancée*, vous pouvez implémenter un pré-commande itératif basé sur la file** pour éliminer complètement la récursion, la complexité du code de trading pour la sécurité de la pile.

---

#### 2.7 L'horrible – Cas de bords cachés et erreurs courantes

1. **Commande de formation**
*Java/Python/C++ ci-dessus* terminer la chaîne par une virgule supplémentaire (`"1,2,null",`). Certains intervieweurs testent si vous gérez avec grâce.
**Fix** – Strip la virgule finale avant de revenir, ou l'ignorer pendant l'analyse ("getline" produira un jeton vide qui est inoffensif).

2. ** Chaîne d'entrée vide**
LeetCodeS test harnais appelle parfois `désérialize("")`. Votre code doit retourner `nullptr`/`Aucun` gracieusement.

3. **Grands nombres négatifs**
Le jeton de chaîne `"null"` ne doit jamais être confondu avec une valeur négative. Toujours vérifier l'égalité avant de convertir en `int`.

4. **Séparateurs non-comma**
Si vous décidez d'utiliser des espaces ou des nouvelles lignes au lieu de virgules, assurez-vous que le codeur/décodeur utilise *exactement* le même délimiteur.

5. **Seuils de mémoire (C++)**
Dans la version C++, nous allouons de nouveaux `TreeNode` mais ne les libérons jamais. Dans un vrai réglage d'interview, vous avez soit donné la propriété à l'appelant ou écrire un aide `deleteTree`.

---

### 2.8 Tâches particulières d'entrevue

Sujet Question que vous pourriez entendre
C'est ce qu'on dit.
**Complexité algorithmique** Pourriez-vous faire mieux ? Autres
**Format de sérialisation**= Pourquoi avez-vous choisi la précommande? Pourriez-vous utiliser la commande de niveau à la place? Autres
Comment votre code gère-t-il un arbre vide ou un arbre biaisé ? Autres
**Cas d'Edge** Seulement laissé des enfants? Autres
**Gestion de la mémoire** Autres

---

2.9 Conclusion

LeetCode 297 est un problème *canonique* d'entrevue qui teste votre prise de travers et de récursion d'arbres.
La solution précommande DFS** est :

* **Efficace** – temps linéaire et espace.
* **Simple** – une paire de petites aides récursives.
* **Reliable** – reconstruction déterministe grâce aux marqueurs "null".

En étudiant les aspects **good**, **bad** et **ugly**, vous serez en mesure d'expliquer *pourquoi* l'algorithme fonctionne et *comment* le défendre contre les questions de bord—qui impressionnent tous les gestionnaires d'embauche.

> **Conseil pratique** – Écrivez le code sur un tableau blanc, puis copiez-le dans votre IDE et exécutez les tests officiels LeetCode.
> **Partager** – Si vous avez trouvé cela utile, déposez un commentaire ou un tweet `@YourHandle` et faites savoir à votre réseau que vous avez conquis LeetCode 297!

---

- Oui. 3. Liste de contrôle sur l'approche à suivre (entrevue à l'avance)

C'est pas vrai.
C'est le cas.
Sériez en utilisant la récursion de 1 liner DFS dans Java/Python/C++.
Utiliser les jetons `"null"` pour les enfants absents
La désérialisation consomme la liste dans l'ordre
O(n) temps et espace
Code prêt-à-coller en 3 langues

Joyeux codage – et heureux entretien!