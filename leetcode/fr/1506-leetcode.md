---
titre: LeetCode 1506. Trouver la racine de l'arbre N-Ary -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Article de blog – Trouver la racine d'un arbre N-ary : le bon, le mauvais et le mauvais

> ** Mots-clés du référencement**: Trouver la racine de l'arbre N-ary, LeetCode 1506, arbre N‐ary, problème d'interview, Java, Python, C++, algorithme, hashset, XOR, solution O(n), espace constant, entretien d'emploi

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Comprendre l'entrée et la sortie] (#entrée-sortie)
3. [Pièges communs (les affreux)] (#pièges)
4. [Approche no 1 – HashSet (le bon)] (#hashset)
5. [Approche n°2 – XOR (le méchant, mais élégant)] (#xor)
6. [Complexité temporelle et spatiale](#complexité)
7. [Causes de sauvegarde et validation] (#cases de référence)
8. [Code Walkthrough (Java, Python, C++)](#code)
9. [Conseils d'entrevue prêts](#tips)
10. [Enveloppe] (#Enveloppe)

---

- Oui. 1. Aperçu du problème <un nom="problème-overview"></a>

> **LeetCode 1506 – Trouver la racine de l'arbre n‐aire**
> **Difficulté**: Moyenne

On vous donne *tous* noeuds d'un arbre N-ary dans un ordre arbitraire.
Chaque nœud a une valeur entière unique et une liste d'enfants.
Votre tâche : **Retourner le nœud racine** (le seul noeud qui n'apparaît jamais comme un enfant).

> **Suivi**: Pouvez-vous le résoudre dans **l'espace auxiliaire constant** et le temps linéaire?

---

- Oui. 2. Comprendre l'entrée et la sortie <a name="input-output"></a>

Le pilote crée un arbre à partir d'une sérialisation de niveau* (enfants séparés par « null ».
Il mélange ensuite les objets `Node` et passe le tableau/liste résultant à votre fonction `findRoot`.

**Ce que vous recevez**:
`Liste<Node> arbre` (Java) / `Liste[Node] arbre` (Python) / `vecteur<Node*> arbre` (C++)

**Ce que vous devez retourner**:
L'objet *root* `Node` lui-même.

*Si votre fonction retourne la bonne racine, le pilote sérialise cet arbre et le compare avec l'entrée originale. *

---

- Oui. 3. Pièges communs (les odieux) <un nom="pièges"></a>

Pourquoi ça fait mal ? Comment éviter ?
C'est pas vrai.
**Si le premier élément est la racine**, l'ordre d'entrée est aléatoire. Il faut passer sur tous les nœuds. Autres
**L'utilisation de `Node.equals` incorrectement** Comparer en utilisant des références de nœuds ou en stockant des objets de nœuds dans un ensemble. Autres
**O(n2) solutions**= Double boucle sur les enfants → TLE sur 5 × 104 nœuds.= Utilisez un jeu de hachage ou un tour de XOR (O(n)). Autres
**Utiliser des structures de données supplémentaires inutilement** Préférez l'astuce XOR pour O(1) espace supplémentaire. Autres
**Ignorer les enfants nuls** La liste `enfants` ne contient jamais `null`. Autres

---

- Oui. 4. Approche no 1 – HashSet (Le Bon) <un nom="hashset"></a>

1. **Collectez tous les enfants** dans un `HashSet<Node>`.
2. **Scan à nouveau** – le nœud qui est *pas* dans l'ensemble est la racine.

**Pourquoi c'est bon**
- Simple à raisonner.
- Fonctionne pour toute forme d'arbre (binaire, ternaire, etc.).
- Temps linéaire, espace supplémentaire O(n) (acceptable pour le problème d'origine).

"Java
publique Node findRoot(Liste <Node> arbre) {
Ensemble <Node> enfants = nouveau HashSet<>();
pour (Node n : arbre) {
enfants.addAll(n.enfants);
}
pour (Node n : arbre) {
si (!enfants.contient(n)) retour n;
}
retour null; // ne devrait jamais arriver
}
«» "

---

- Oui. 5. Approche no 2 – XOR (L'Ugly, mais Élégant) <un nom=xor></a>

Observation:
Toutes les valeurs des nœuds sont des entiers uniques.
Si nous XOR **chaque valeur de nœud** ensemble et XOR **chaque valeur d'enfant** ensemble, les paires s'annulent, ne laissant que la valeur de racine.

** Mise en œuvre* *
- Utiliser `long` pour éviter les débordements (valeurs jusqu'à 5 × 104).
- Exécuter XOR en traversant la liste une fois.

"Java
publique Node findRoot(Liste <Node> arbre) {
xor long = 0;
pour (Node n : arbre) {
xor ^= n.val;
pour (nœud enfant : n.enfants) xor ^= child.val;
}
// Trouver le nœud avec la val correspondante
pour (Node n : arbre) {
si (n.val == xor) retourner n;
}
retour nul;
}
«» "

**Pourquoi c'est ça *
- S'appuie sur l'unicité de la valeur; si le problème change, cela rompt.
- Moins intuitif qu'un jeu, peut soulever les sourcils de l'intervieweur.
- Toujours temps O(n) mais espace auxiliaire O(1) – satisfait le suivi.

---

- Oui. 6. Complexité temporelle et spatiale <un nom=complexité></a>

Démarche Temps Espace supplémentaire
- C'est quoi ?
**O(n)** (deux passes)
**O(n)** (passe unique)

Tous deux satisfont aux exigences de temps linéaire. L'astuce XOR est la seule qui rencontre le suivi de l'espace constant.

---

- Oui. 7. Cas de bord et validation <un nom>

Le comportement attendu
- C'est pas vrai.
Autres Un seul noeud La racine est ce noeud. Autres
Autres Arbre linéaire de profondeur (chaque noeud a un enfant) Autres
Autres Grand arbre peu profond (la racine a beaucoup d'enfants) Autres
Dupliquer les valeurs (non autorisées par les contraintes) Dupliquer le problème invalide; XOR échoue. Autres
Autres Null enfants dans la sérialisation d'entrée.Ignoré par le conducteur; les listes d'enfants ne sont jamais nulles. Autres

Vérifiez toujours que la racine retournée par votre fonction se sérialise en retour à l'entrée originale.

---

- Oui. 8. Passage du code (Java, Python, C++) <un nom="code"></a>

#### 8.1 Java (HashSet + XOR)

"Java
Importation de java.util.*;

Numéro de classe {
Int val public;
liste publique <Node> des enfants;
Nœud public() { enfants = nouvelle liste de distribution<>(); }
Nœud public(int _val) { val = _val; enfants = nouvelle station de radio<>(); }
Noeud public(int _val, liste <Noeud> _enfants) {
val = _val; enfants = _children;
}
}

solution de classe {
- Oui. Approche HashSet
public Node findRootHashSet(Liste <Node> arbre) {
Set<Node> vu = nouveau HashSet<>();
pour (Node n : arbre) vu.addAll(n.enfants);
pour (Node n : arbre) si (!see.contient(n)) retour n;
retour nul;
}

- Oui. Approche XOR
publique Noeud trouvéRootXOR(Liste <Noe> arbre) {
xor long = 0;
pour (Node n : arbre) {
xor ^= n.val;
pour (nœud enfant : n.enfants) xor ^= child.val;
}
pour (Node n : arbre) si (n.val == xor) retour n;
retour nul;
}
}
«» "

#### 8.2 Python (HashSet + XOR)

'`python
de taper l'importation Liste

Numéro de classe:
def __init_(self, val: int = 0, enfants: Liste['Node'] = Néant):
autoval = val
enfants = enfants ou []

Solution de classe:
# HashSet
def findRootHashSet(self, arbre: Liste[Node]) -> Numéro:
child_set = set()
pour noeud en arbre:
child_set.update(node.children)
pour noeud en arbre:
si le noeud n'est pas dans le_set d'enfant:
noeud de retour
retour Aucune

# XOR
def trouver RootXOR(même, arbre: Liste[Node]) -> Numéro:
xor_val = 0
pour noeud en arbre:
xor_val ^= noeud.val
pour enfant en nœud. enfants:
xor_val ^= child.val
pour noeud en arbre:
si noeud.val == xor_val :
noeud de retour
retour Aucune
«» "

#### 8.3 C++ (HashSet + XOR)

'`cpp
#incluez <vecteur>
#inclut <unordered_set>

Numéro de structure {
la valeur intérieure;
md::vecteur <Node*> enfants;
Noeud(int _val = 0) : val(_val) {}
};

struct NodeHash {
size_t operator()(const Node* n) const noexception {
retour à la ligne::hash<int>()(n->val);
}
};

solution de classe {
public:
// HashSet
Noeud* findRootHashSet(suite std::vector<Noe*>&arborescence) {
std::unordered_set<Node*, NodeHash> vu;
pour (Node : arbre)
pour (nœud* enfant : nœud->enfants)
voir.insert(enfant);
pour (Node : arbre)
si (seen.find(node)) == vu.end()
noeud de retour;
retour nullptr;
}

// XOR
Noeud* findRootXOR(const std::vector<Noe*>&arborescence) {
long xor_val = 0;
pour (Node : arbre) {
xor_val ^= noeud->val;
pour (nœud* enfant : nœud->enfants)
xor_val ^= enfant->val;
}
pour (Node : arbre)
si (noeud->val == xor_val)
noeud de retour;
retour nullptr;
}
};
«» "

> **Astuce** – Si vous écrivez pour LeetCode, la classe `Solution` est requise; le pilote va l'actualiser et appeler `findRoot`.

---

- Oui. 9. Conseils de préparation à l'entrevue <a name="tips"></a>

1. ** Préciser les contraintes* *
*Valeurs uniques?* *Nombre maximum de nœuds ? *
Cela vous aidera à décider entre hasch-set ou XOR.

2. ** Expliquez votre raisonnement**
Montrez que vous comprenez *pourquoi* la racine est le nœud qui n'apparaît jamais comme un enfant.

3. **Déclarer les compromis**
- HashSet: *O(n)* espace, plus facile à lire.
- XOR: *O(1)* espace, ne fonctionne qu'avec une unicité entière.

3. **Cas de bord des peines**
Demandez s'ils s'attendent à ce que vous traitiez des arbres à nœud unique ou dégénérés.

4. **La complexité du temps d'abord**
Si vous pouvez prouver O(n) tout en faisant un passage, vous avez déjà satisfait à l'interviewer.

5. **Préparez-vous pour une question sur XOR?
Pouvez-vous montrer la propriété d'annulation en action?
Pratiquez l'écriture de la logique XOR sur un tableau blanc.

6. **Si vous n'êtes pas sûr de l'unicité de la valeur**, commencez par la solution de hachage.
Vous pouvez toujours ajouter un commentaire sur l'astuce XOR de suivi.

---

#10. Enveloppe <un nom="enveloppe"></a>

*Le noyau du problème est simple: identifier le noeud parent unique. *
- La solution **HashSet** est **robust** et facile à expliquer.
- La solution **XOR** est **facinante** et répond au suivi de l'espace constant.

Les deux courent dans le temps **O(n)**, et le tour XOR vous donne **O(1)** espace auxiliaire.
Choisissez celui qui correspond à votre style d'entrevue, ou montrez les deux pour démontrer la profondeur.

** Bon codage !**

---

**Vous souhaitez améliorer votre pratique LeetCode? **
- Explorez des problèmes similaires à ceux de l'élément unique : 213 `House Robber III`, 297 `Serialize and Deserialize Binary Tree`.
- Study bit-wise tricks – ils conduisent souvent à des solutions O(1) élégantes.

Bonne chance – vous avez ça!