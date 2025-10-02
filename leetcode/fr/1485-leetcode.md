---
titre: LeetCode 1485. Clone arbre binaire avec pointeur aléatoire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. Clone arbre binaire avec pointeur aléatoire
**LeetCode 1485 – Moyen**

Code de la langue
-- -- -- -- -- --
[Voir le code](#java-code)
[Voir le code](#python-code)
[Voir le code](#cpp-code)

> **SEO Mots-clés**: Clone Binary Tree With Random Pointer, LeetCode 1485, arbre binaire copie profonde, clone de pointeur aléatoire, solution Java DFS, solution Python DFS, solution C++ DFS, entretien de structure de données, défi de codage d'entrevue, problèmes de codage d'entrevue d'emploi.

---

- Oui. 1. Résumé du problème

On vous donne un arbre binaire où chaque noeud contient un pointeur supplémentaire appelé `random`.
`random` peut pointer à **any** noeud dans l`arbre (y compris lui-même) ou être `null`.
Votre tâche est de créer une copie **deep** de l'arbre entier – c.-à-d. chaque noeud et chaque
La référence «randome» doit indiquer un nouveau nœud ayant la même valeur.

Le format d'entrée et de sortie suit la sérialisation habituelle de l'arbre binaire LeetCode :
`[value, random_index]` – `random_index` est la position du noeud dans le tableau
(ou `null` si aucun pointeur aléatoire).

> **Constraints**
> - 0 ≤ nombre de nœuds ≤ 1000
> - 1 ≤ Node.val ≤ 106

---

- Oui. 2. Idée fondamentale – Deux Passer DFS avec un HashMap

1. ** Premier col** – Clone chaque noeud (en ignorant le lien "randome") et stocker un
cartographie du nœud original à son clone.
2. **Deuxième Pass** – Traverser à nouveau l'arbre d'origine; pour chaque noeud, régler le
clones `gauche`, `droite` et `random` en regardant les champs correspondants
clone objets dans la carte.

Parce que chaque noeud est visité deux fois et nous utilisons une carte de hachage pour résoudre les pointeurs,
l'algorithme fonctionne dans **O(N)** temps et **O(N)** espace auxiliaire.

L'approche à deux passages maintient le code simple et évite les complexes
la gymnastique pointeur qu'un clone à un passage en place exigerait.

---

- Oui. 3. Mise en œuvre du code

> **Note**: Dans les trois extraits, le type de noeud *clone* est le même que le type de noeud *clone*.
> original (`Node`). L'interface `Solution` de LeetCode , attend la même classe
> pour entrée et sortie.

### <a name="java-code"></a>Java – DFS avec HashMap

"Java
***
* Définition pour un nœud.
* Noeud de classe publique {
* Int val;
* À gauche;
* Noeud droit;
* Noeud aléatoire;
* Noeud() {}
* Node(int val) { this.val = val; }
* Nœud (int val, Noeud gauche, Noeud droit, Noeud aléatoire) {
* ce.val = valeur;
* ce.gauche = gauche;
* ce droit = droit;
* ceci.random = aléatoire;
*}
*}
*/
solution de classe {
// Noeud original de la carte -> noeud cloné
carte finale privée <Node, Node> carte = nouveau HashMap<>();

clone de nœud public Arbre(racine de nœud) {
si (root) null retourne null;

// Premier passage: noeuds clones (pas encore d'enfants)
cloneNodes(root);

// Deuxième passe : à gauche, à droite, au hasard
setPointers(root);

retour map.get(root);
}

// DFS récursif qui clone chaque noeud une fois
clone privé videNodes(node node) {
si (node) null.ContientKey(node) retour;
map.put(node, nouveau Node(node.val));
cloneNodes(node.left);
cloneNodes(node.right);
cloneNodes(node.random);
}

// DFS récursif qui branche les enfants et les pointeurs aléatoires
private void setPointers(Node node) {
si (noeud == nul) retour;
Copie de nœud = map.get(node);
copy.left = map.get(node.left);
copy.right = map.get(node.right);
copy.random = map.get(node.random);
setPointers(node.left);
setPointers(node.right);
setPointers (node.random);
}
}
«» "

### <a name="python-code"></a> Python – DFS avec dictionnaire

'`python
# Définition pour un noeud.
Numéro de classe:
def __init__(self, val=0, gauche=Aucun, droite=Aucun, aléatoire=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit
auto.random = aléatoire

Solution de classe:
def clone Arbre(même, racine: 'Node') -> 'Noeud':
si ce n'est pas la racine:
retour Aucune

Self.mapping = {}
Self._first_pass(root)
Self._second_pass(root)
Revenez vous-même. mapping[root]

def _first_pass(self, noeud):
si ce n'est pas un noeud ou un noeud en soi. cartographie:
retour
self.mapping[node] = Node(node.val)
Self._first_pass(node.left)
Self._first_pass(node.right)
Première _passe(node.random)

def _second_pass(self, noeud):
si ce n'est pas le nœud:
retour
clone = auto-mapping[node]
clone.left = self.mapping.get(node.left)
clone.right = self.mapping.get(node.right)
clone.random = self.mapping.get(node.random)
Self._second_pass(node.left)
Self._second_pass(node.right)
Self._second_pass(node.random)
«» "

### <a name="cpp-code"></a>C++ – DFS avec `unordered_map`

'`cpp
***
* Définition pour un nœud.
* Numéro de structure {
* Int val;
A gauche.
Noeud droit;
Noeud;
* Node() : val(0), gauche(nullptr), droite(nullptr), aléatoire(nullptr) {}
* Node(int _val) : val(_val), gauche(nullptr), droite(nullptr), aléatoire(nullptr) {}
* Noeud(int _val, Noeud* _left, Noeud* _right, Noeud* _random)
* : val(_val), gauche(_gauche), droite(_droite), aléatoire(_random) {}
* };
*/
solution de classe {
public:
Clone de nœud*Race de nœud* {
si (!root) retourne nullptr;
unordered_map<Node*, Node*> mp;
premierPass(root, mp);
deuxièmePass(root, mp);
retour mp[root];
}

particulier:
vide d'abord Pass(Node* noeud, non ordonné_map<Node*, Node*>& mp) {
si (!node) retour mp.count(node);
mp[node] = nouveau Node(node->val);
firstPass(node->left, mp);
firstPass(node->right, mp);
premierPass(node->random, mp);
}

vide secondPass(Node* noeud, non ordonné_map<Node*, Node*>& mp) {
si (!node) retour;
clone de nœud* = mp[node];
clone->left = mp.count(node->left) ? mp[node->left] : nullptr;
clone->right = mp.count(node->right) ? mp[node->right] : nullptr;
clone->random = mp.count(node->random) ? mp[node->random] : nullptr;
deuxièmePass(node->gauche, mp);
deuxièmePass(node->right, mp);
deuxièmePass(node->random, mp);
}
};
«» "

---

- Oui. 4. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Première DFS **O(N)**
Deuxième DFS **O(N)**
Total******************

`N` est le nombre de nœuds dans l'arbre.
La profondeur de la récursion est limitée par la hauteur de l'arbre (= N).

---

- Oui. 5. Discussion – Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Clarté**=Le DFS à deux passages est simple à raisonner. La récursion peut provoquer un débordement de cheminée sur des arbres très profonds. En place, les solutions à un seul passage (relier les clones dans l'arbre original) sont difficiles à déboguer. Autres
**La carte de mémoire est acceptable pour 1 000 nœuds. Nécessite un espace supplémentaire au-delà du nouvel arbre. L'utilisation de `unordered_map` en C++ peut entraîner des collisions de hachage élevées. Autres
**Performance** Deux traversées doublent le facteur constant. La manipulation complexe des pointeurs peut introduire des bugs subtils lors de la restauration de l'arbre original. Autres
**Extensibilité** Ne gère pas les cycles qui ne sont pas couverts par le pointeur aléatoire (pas un arbre). Autres L'algorithme ne suppose pas d'autres cycles que le "random"; sinon, vous auriez besoin de détection de cycle. Autres
**Cas d'escroquerie**=Poignées `null`, pointeurs aléatoires auto-référencés, et pointage aléatoire vers n'importe quelle profondeur. Si la classe de nœuds contient des champs supplémentaires (p. ex. pointeurs parent), ils doivent être traités explicitement. Autres

---

- Oui. 6. Article sur le blog amiable

> **Titre**
> *Master LeetCode 1485: Clone Binary Tree avec pointeur aléatoire – Java, Python, & C++ Solutions pour votre entrevue*

---

#### 6.1 Pourquoi ce problème est-il à l'origine de votre entrevue

* Clone Binary Tree With Random Pointer* (1485) est une interview classique
problème parce qu'il combine deux concepts de structure de données bien-aimés:

1. **Travaux d'arbres bitumineux** (DFS/BFS)
2. **Random pointer copie profonde** – un piège caché qui peut faire même assaisonné
les développeurs trébuchent.

Il apparaît dans de nombreux dépôts d'entrevues, et les gestionnaires d'embauche aiment
l'utiliser parce qu'il teste:

- Votre capacité à penser récursivement
- Votre compétence avec les tables de hachage (`Map`, `dict`, `unordered_map`)
- Votre compréhension de la sémantique des pointeurs

---

#### 6.2 Pourquoi nous utilisons une carte HashMap (ou carte Dict / Non-ordonnée)

Le pointeur aléatoire est **pas** partie de la structure naturelle de l'arbre.
Lorsque vous clonez un noeud, vous devez savoir *que* le noeud cloné correspond au
cible originale "randome".
Une carte de hachage vous donne **O(1)** temps de recherche et garantit que chaque original
des cartes de nœuds vers un clone unique.

---

#### 6.3 Étape par étape Exemple Java

"Java
publique Clone de nœudTree(Node root) {
si (root) null retourne null;
Carte <Node, Node> carte = nouvelle HashMap<>();
cloneNodes(root, map); // 1ère passe
setPointers(root, map); // 2ème passe
retour map.get(root);
}
«» "

*First pass* fait simplement `map.put(node, nouveau Node(node.val))`.
*Deuxième passe* fils `left`, `right` et `random` via `map.get(...)`.

---

6.4 Autres approches que vous pourriez voir

Démarche
C'est quoi ?
Un peu plus de code ; il faut encore une file d'attente.
**One-pass In-place Clone**. Pas de carte de hachage supplémentaire.
**Utiliser les pointeurs parent**

La SDD à deux passages est *habituellement* l'approche recommandée pour le codage des entrevues.

---

6.5 Comment se préparer à des questions d'entrevue semblables

1. ** Pratique avec pointeurs aléatoires**
LeetCodeS *Liste de copie avec pointeur aléatoire* (version de liste liée) est une
grand échauffement.

2. **Modèles Master DFS & BFS* *
Conservez un nœud réutilisable avec un modèle de mapping dans votre carnet.

3. **Comprendre les cas de bord* *
Arbre vide, seul noeud avec "randome" pointant vers lui-même, arbres très profonds.

4. ** Échanges entre le temps et l'espace**
Soyez prêt à expliquer pourquoi vous avez choisi une solution particulière
Les compromis sont.

5. **Demander des précisions**
Dans une interview en direct, confirmez si vous êtes autorisé à utiliser la mémoire supplémentaire,
si l'arbre peut contenir des cycles via `random`, etc.

---

## 6.6 Enveloppage

- **Problème**: Copier en profondeur un arbre binaire avec un pointeur arbitraire.
- **Solution** : carte DFS + hash à deux passages (DFS, Python dict, C++ non ordonnée_map).
- **Complexité**: temps O(N), espace O(N).

Si vous êtes en train de brosser pour une interview de structures de données, préparer pour un
rôle d'ingénierie de logiciels, ou tout simplement aimer LeetCode défis, maîtriser ce
problème vous donnera confiance dans la manipulation des pointeurs, récursion, et hash
tableaux – compétences qui sont ** hautement recherchées** par les entreprises de haute technologie.

Bon codage ! C'est ce qu'il a dit