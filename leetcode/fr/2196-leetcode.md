---
titre: LeetCode 2196. Créer un arbre binaire à partir des descriptions -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de solution

Ci-dessous sont des implémentations propres et prêtes à la production pour **LeetCode 2196 – -Créer l'arbre binaire à partir des descriptions** dans **Java, Python et C++**.
Les trois solutions partagent la même idée algorithmique :

1. **Construisez une carte de nœud** – chaque valeur unique → son `TreeNode`.
2. **Lier les enfants aux parents** – en utilisant le drapeau « isLeft ».
3. **Trouver la racine** – la seule valeur qui n'apparaît jamais comme un enfant.

L'approche est **O(n)** dans le temps et l'espace où *n* est le nombre de descriptions.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
// Définition pour un nœud binaire.
classe statique publique TreeNode {
la valeur intérieure;
TreeNode gauche;
TreeNode droit;
TreeNode(int x) { val = x; }
}

public TreeNode createBinaryTree(int[][] descriptions) {
// 1. Construire la carte de la valeur au noeud
Carte<entier, TreeNode> nodeMap = nouveau HashMap<>();

// 2. Suivre tous les enfants pour trouver la racine plus tard
Définir <Integer> enfants = nouveau HashSet<>();

pour (int[] d : descriptions) {
parent int = d[0], enfant = d[1], estLeft = d[2];

// Obtenir ou créer un nœud parent
TreeNode parentNode = nodeMap.computeIfAbsent(parent,
k -> nouveau TreeNode(k)

// Obtenir ou créer un nœud enfant
TreeNode childNode = nodeMap.computeIfAbsent(enfant,
k -> nouveau TreeNode(k)

// Lien selon le drapeau isLeft
Si (estLeft) 1) {
parentNode.left = enfantNode;
} autre {
parentNode.right = enfantNode;
}

enfants.add(enfant);
}

// 3. La racine est le nœud qui n'apparaît jamais comme un enfant
racine int Val = -1;
pour (int val : nodeMap.keySet()) {
si (!enfants.contient(val)) {
racine Val = valeur;
pause;
}
}
retour nodeMap.get(rootVal);
}
}
«» "

---

Python

'`python
de taper l'importation Liste, facultative

# Définition d'un noeud d'arbre binaire.
classe TreeNode:
Def __init_(self, val:int):
autoval = val
self.left: Facultatif[TreeNode] = Néant
soi.right: Facultatif[TreeNode] = Néant

Solution de classe:
def créer Binaire Arbre(même, descriptions: Liste[Liste[int]]) -> Facultatif[TreeNode]:
node_map = {}
enfants = ensemble()

pour parent, enfant, is_left dans les descriptions:
Créer des nœuds paresseusement
si parent n'est pas dans node_map:
node_map[parent] = TreeNode(parent)
si l'enfant n'est pas dans node_map:
node_map[enfant] = TreeNode(enfant)

# Joindre l'enfant
if is_left == 1 :
node_map[parent].left = node_map[child]
Sinon:
node_map[parent].right = node_map[child]

enfants.add(enfant)

# Trouver racine (pas un enfant)
root_val = next(val pour val dans node_map si val n'est pas chez les enfants)
retourner noeud_map[root_val]
«» "

---

C++

'`cpp
#inclut <non-ordonné_map>
#inclut <unordered_set>
#incluez <vecteur>

struct TreeNode {
la valeur intérieure;
TreeNode *gauche;
TreeNode *right;
TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
};

solution de classe {
public:
TreeNode* createBinaryTree(const std::vector<std::vector<int>& descriptions) {
std::unordered_map<int, TreeNode*> nœuds;
std::unordered_set<int> les enfants;

pour (const auto &d : descriptions) {
parent int = d[0], enfant = d[1], estLeft = d[2];

// Créer des nœuds sur demande
si (!nodes.count(parent)) nœuds[parent] = nouveau TreeNode(parent);
si (!nodes.count(child)) nœuds[child] = nouveau TreeNode(child);

// Annexe
si (estLeft)
noeuds[parent]->gauche = noeuds[enfant];
Autre
noeuds[parent]->droit = noeuds[enfant];

enfants.insert(enfant);
}

// La racine est le nœud qui n'apparaît jamais comme un enfant
racine int Val = -1;
pour (const auto &kv : noeuds)
Si (!enfants.count(kv.first)) {
racine Val = kv.first;
pause;
}

les nœuds de retour[rootVal];
}
};
«» "

> **Astuce** – N'oubliez pas de supprimer les nœuds lorsque vous êtes fait (ou utilisez des pointeurs intelligents en C++17+).
> LeetCodeS test harnais le gère, mais les projets réels devraient gérer la mémoire correctement.

---

Article du blog – Le bon, le mauvais, et le mauvais de construire un arbre binaire à partir des descriptions

> **SEO Mots-clés**: LeetCode 2196, créer arbre binaire à partir de descriptions, interview prep, arbre binaire Java, arbre binaire Python, arbre binaire C++, structures de données, interview algorithme, problèmes de structure de données

---

Introduction

Les arbres binaires sont un élément essentiel des entrevues en informatique.
Problème LeetCode **2196 – *Créer un arbre binaire À partir des descriptions*** vous demande de reconstruire un arbre lorsque vous n'avez qu'un ensemble de relations parents-enfants.

C'est un problème trompeur simple qui teste :

- **Cartographie entre valeurs et objets** (`HashMap / unordered_map`).
- **Déterminer la racine.
- **Logique de passage du graphique** (même implicite).
- ** Solutions O(n) propres** vs approches O(n2) naïve.

Dans ce billet, je vais vous guider à travers le **bon** (ce qui fonctionne), le **mauvais** (écueils communs), et le **ugly** (cases de fond que vous pourriez manquer). Le but ? Transformez ce défi LeetCode en une vitrine de vos côtelettes de résolution de problèmes sur votre CV.

---

Récapitulation des problèmes

Vous êtes donné `descriptions`, une liste de `[parent, enfant, isLeft]` triples.
`isLeft = 1` → l'enfant est l'enfant gauche, sinon c'est l'enfant droit.
Toutes les valeurs des nœuds sont uniques, et les descriptions décrivent un arbre binaire *valable*.

Retourne la racine **** de l'arbre reconstruit.

---

Le bon – propre O(n) Algorithme

1. ** Construction d'un laissez-passer**
Iterate une fois sur les "descriptions":
- Pour chaque triple, récupérer ou créer le `TreeNode` pour `parent` et `enfant`.
- Faire passer le `enfant` à `parent` `gauche` ou `droit`.
- Enregistrez chaque valeur enfant dans un "Set".

2. **Identification des lots**
La racine est la seule valeur jamais vue comme un enfant.
Après la boucle, itérer sur les touches de la carte des nœuds et choisir celui absent de l'enfant ensemble.

3. **Complexité**
- **Heure**: `O(n)` – chaque description traitée une fois.
- **Espace**: `O(n)` – pour la carte des nœuds et le jeu d'enfants.

Cette solution est la réponse d'entrevue standard. Il montre la familiarité avec les tables de hachage et la théorie des ensembles.

---

Les mauvaises – Pièges communs

Pourquoi il est un problème
- Oui.
**Création de nœuds** , créant par accident des objets `TreeNode` pour la même valeur. Autres
**O(n2) lien naïf**=Pour chaque description cherchant la liste entière des nœuds pour le parent. Utilisez une carte pour localiser directement les parents en temps constant. Autres
**En supposant que le premier élément est root**. Identifier la racine via l'ensemble enfant. Autres
**Ne pas manipuler les racines manquantes**= Si vous oubliez de chercher la racine, vous pouvez retourner `null`. Trouver et retourner explicitement la racine après la construction. Autres
Autres **Raches de mémoire (C++)**= Attribution dynamique des nœuds sans les libérer. Utilisez des pointeurs intelligents (`std::unique_ptr`) ou un nettoyage manuel. Autres

---

Les cas les plus odieux et les scénarios tricky

Scénario Pourquoi cela compte
- C'est quoi ?
Autres ** Grandes gammes de valeurs** ('1 ≤ valeur ≤ 105') Utiliser un tableau dense gaspillerait de l'espace. Se tenir aux cartes/ensembles de hachage. Autres
**Input minimal** (`n = 1`)= Un seul noeud; la racine est aussi l'enfant. Autres Fonctionne naturellement avec l'algorithme : l'ensemble racine contiendra le parent mais pas l'enfant. Autres
Autres **Tous les nœuds d'un côté** (p. ex., un arbre dégénéré à droite) Le drapeau « isLeft » est toujours appliqué; aucun cas particulier n'est nécessaire. Autres
**Descriptions dupliquées**Le problème garantit la validité, mais un test défectueux peut contenir des duplicatas. HashMap + set déduira automatiquement les nœuds. Autres
**La plus grande récursion de profondeur**.Si vous ajoutez plus tard un DFS pour sérialiser l'arbre, la profondeur de récursion pourrait atteindre la limite de la pile. Utilisez la pile itérative ou augmentez la récursion. Autres

---

Pourquoi cela compte pour votre travail de chasse

- **Capacité de la structure des données** – Démontre la maîtrise des cartes de hachage, des ensembles et de la manipulation des arbres.
**Efficacité algorithmique** – Montre que vous pouvez fournir des solutions O(n) où O(n2) serait désastreux.
- **Attention au détail** – La gestion des cas bord, la gestion de la mémoire et le code propre sont prisés par les gestionnaires d'embauche.
- **Préparation à l'entrevue** – Des problèmes comme celui-ci apparaissent dans de nombreux entretiens techniques; vous serez à l'aise de présenter votre processus de pensée.

---

Référence rapide – Pseudo monoligne

Texte
pour (p, c, l) dans les descriptions:
nodeMap[p] = nodeMap.getOrCreate(p)
nodeMap[c] = nodeMap.getOrCreate(c)
si l: nodeMap[p].left = nodeMap[c]
Autre : nodeMap[p].right = nodeMap[c]
enfantSet.add(c)

rootVal = (nodeMap.keys - childSet). unique
retour nodeMap[rootVal]
«» "

---

À emporter

Une bonne solution est une solution qui est efficace, lisible et qui tient compte de tous les cas de bord. La mauvaise solution est celle qui complique ou abuse des structures de données. Le plus moche, c'est ce qui glisse quand on oublie de penser à la mémoire, aux limites de la récursion, ou au plus simple tour de recherche des racines.

Maîtrisez ce problème, polissez votre code (Java, Python, C++), et vous aurez un exemple prêt à montrer de pensée algorithmique propre qui peut vous atterrir à la prochaine entrevue.

Joyeux codage, et bonne chance pour la chasse au travail! C'est ce qu'il a dit.

---