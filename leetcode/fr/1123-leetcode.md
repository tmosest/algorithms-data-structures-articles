---
titre: LeetCode 1123. Ancêtre le plus bas commun des feuilles les plus profondes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1123. Ancêtre le plus bas commun des feuilles les plus profondes
**Difficulté:** Moyenne

### TL;DR
- **Objectif:** Retourner l'ancêtre commun le plus bas (LCA) de tous les nœuds foliaires les plus profonds dans un arbre binaire.
- **Idée de base:** Faites un seul DFS qui retourne **(sous-LCA, profondeur)** pour chaque sous-arbre.
- **Complexité:** temps O(N), espace O(H) (pile de récursion).

Vous trouverez ci-dessous des solutions prêtes à passer, prêtes à la production dans **Java**, **Python** et **C++**, suivies d'un Article de blog optimisé par le SEO qui explique le bon, le mauvais, et le laid de ce problème – parfait pour impressionner les recruteurs lors de votre prochaine interview.

---

Code – 3 langues

> **Conseil:** Les trois implémentations supposent la définition standard de LeetCode `TreeNode`.
> **Soyez libre** pour copier le code dans votre boîte à sable IDE ou LeetCode locale.

### Java

"Java
// Définition pour un nœud binaire.
classe publique TreeNode {
la valeur intérieure;
TreeNode gauche;
TreeNode droit;
TreeNode() {}
TreeNode(int val) { this.val = val; }
TreeNode(int val, TreeNode à gauche, TreeNode à droite) {
ce.val = valeur;
Ça. gauche = gauche;
Ça. droite = droite;
}
}

solution de classe publique {
// Point d'entrée public
public TreeNode lcaDeepest Feuilles(racine de nœud d'arbre) {
retour dfs(root).node;
}

// Aide retourne une paire de (LCA, profondeur)
Résultat privé dfs(NodeTree) {
si (noeud == null) {
retourner le nouveau résultat(null, 0); // la profondeur de null est 0
}

Résultat gauche = dfs(node.left);
Résultat droit = dfs(node.right);

// Si un côté est plus profond, propagez l'ACL de ce côté vers le haut
si (gauche.profondeur > droite.profondeur) {
retour du nouveau Result(left.node, left.profondeur + 1);
}
si (gauche.profondeur < droite.profondeur) {
retourner le nouveau résultat(droite.node, droite.profondeur + 1);
}

// Même profondeur – le nœud courant est le LCA
retour du nouveau résultat(node, gauche.profondeur + 1);
}

// Conteneur simple pour garder la paire ensemble
classe statique privée Résultat {
Noeud arbre;
profondeur int;
Résultat(Nœud TreeNode, profondeur int) {
ce.node = noeud;
Ça. profondeur = profondeur;
}
}
}
«» "

Python

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init_(self, val: int = 0, gauche: 'TreeNode' = Aucune, droite: 'TreeNode' = Aucune):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def lcaDeepestLeaves (soi, racine: TreeNode) -> Numéro d'arbre:
retour self.dfs(root)[0] # 0 → noeud, 1 → profondeur

def dfs(self, noeud: TreeNode):
si ce n'est pas le nœud:
retour (Aucun, 0) # (LCA, profondeur)

gauche_lca, gauche_profondeur = self.dfs(node.left)
right_lca, right_profondeur = self.dfs(node.right)

si gauche_profondeur > _profondeur droite :
retour (gauche_lca, gauche_profondeur + 1 )
si gauche_profondeur < droite_profondeur:
retour (droite_lca, droite_profondeur + 1 )

# profondeurs égales => le nœud actuel est le LCA
retour (noeud, gauche_profondeur + 1 )
«» "

C++

'`cpp
***
* Définition d'un noeud d'arbre binaire.
* struct TreeNode {
* Int val;
* TreeNode * gauche;
* TreeNode *right;
* TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
* };
*/
solution de classe {
public:
TreeNode* lcaDeepestLeaves(racine TreeNode*) {
retour dfs(root).premier; // premier → LCA, deuxième → profondeur
}

particulier:
paire <TreeNode*, int> dfs(noeud TreeNode*) {
si (!node) retourne {nullptr, 0};

auto gauche = dfs(node->gauche);
auto right = dfs(node->right);

si (gauche.seconde > droite.seconde)
retour {gauche.première, gauche.seconde + 1};
si (à gauche.seconde < à droite.seconde)
retour {droit.premier, droit.deuxième + 1};

retour {noeud, gauche. deuxième + 1};
}
};
«» "

---

Article du blog
Titre
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

---

### Introduction (méta description optimisée par le SEO)

> *Vous cherchez à recevoir votre prochaine entrevue d'ingénierie logicielle? Cette plongée profonde dans le LeetCode 1123 (Lowest Common Ancêtre of Deepest Leaves) explique l'algorithme le plus efficace, vous fait passer par le code Java/Python/C++ et décompose les nuances du problème. Que vous soyez un développeur junior ou un architecte senior, maîtrisez ce guide bon, mauvais, moche et stimulez votre succès d'entrevue. *

---

Table des matières

1. [Présentation du problème](#problème-aperçu)
2. [Le bon – Pourquoi c'est un défi qui vaut le coup] (#le bon)
3. [Les mauvaises – Pièges communs et idées fausses] (#les mauvaises)
4. [Les horribles – les cas d'Edge et les Gotchas] (#le-gros)
5. [Insight algorithmique – Profondeur-Première recherche + Paire](#algorithmique-insight)
6. [Analyse de la complexité] (#complexité)
7. [Code Walkthrough – Java, Python, C++](#code)
8. [Approches alternatives et pourquoi elles sont moins efficaces] (#alternatives)
9. [Conseils d'entrevue et points de discussion](#interview-tips)
10. [Traitement final et lecture supplémentaire](#finale)

---

#### Aperçu du problème <a name="problem-overview"></a>

LeetCode 1123 vous demande de **retourner l'ancêtre commun le plus bas de toutes les feuilles les plus profondes** dans un arbre binaire.
- **Leaf**: Noeud sans enfants.
- **Depth de la racine**: 0.
- **LCA**: Noeud le plus profond dans l'arbre qui contient toutes les feuilles les plus profondes dans son sous-arbre.

La tâche est une torsion sur le problème classique de LCA parce que l'ensemble de nœuds cibles n'est pas connu à l'avance – il est le *deep* feuilles.

---

C'est vrai. Le bon <un nom=le bon></a>

Autres Qu'est-ce qui est bon Pourquoi ça compte
C'est-à-dire
Autres **Single Pass Solution**.Un DFS vous donne à la fois la profondeur la plus profonde et la LCA en O(N). Autres
Autres **Elégante utilisation de la récursion**. Autres
**Échelles avec hauteur**= Fonctionne pour les arbres biaisés (profondeur O(N) du pire cas). Autres
Le même motif résout le LeetCode 865 (le plus petit sous-arbre avec tous les nœuds les plus profonds). Autres

> *Dans les interviews, les recruteurs aiment les solutions concises mais puissantes. Ce problème est une vitrine parfaite. *

---

#### Le mauvais <un nom="le mauvais"></a>

Erreurs courantes
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Feuilles d'assemblage au lieu de profondeurs**.La profondeur est la clé, pas le nombre de feuilles. Autres
**Utiliser deux passes DFS distinctes**= Vous pouvez obtenir de la profondeur et de la LCA dans une traversée. Autres
**En supposant que la profondeur de la récursion peut être jusqu'à N (1000), encore fine mais mise en garde empiler déborde dans des langages comme Python avec des limites de récursion faibles. Autres
Autres **Retour d'une valeur erronée pour un sous-arbre vide**. Autres

---

#### L'Ugly <a name="the-ugly"></a>

Comment manipuler les cas de bord
C'est quoi ?
**L'arbre à nœuds simples est la racine elle-même. Autres
**Toutes les feuilles à la même profondeur**=Le noeud actuel devient LCA si les profondeurs gauche/droite sont égales. Autres
La pile de récursion peut atteindre la limite par défaut (~1000). Utilisez `sys.setrecursionlimit()` si nécessaire. Autres
**La plus grande profondeur mais petite largeur** Autres

---

#### Algorithmic Insight <a name="algorithmic-insight"></a>

1. **DFS(node)** → retourne **(sous-LCA, profondeur)**.
2. Pour chaque nœud, calculer les résultats à gauche et à droite.
3. **Trois affaires**:
* Gauche plus profonde → propager gauche LCA vers le haut.
* Plus profond → propager droite LCA vers le haut.
* La profondeur égale → noeud courant est le LCA.
4. **Cas de base**: `null` → `(null, 0)`.

Pourquoi ça marche ?
- La *profondeur* vous dit *à quelle distance* vous êtes des feuilles les plus profondes.
- Lorsque deux sous-arbres sont également profonds, l'ancêtre commun le plus bas doit être le nœud courant parce que les deux feuilles les plus profondes sont dans des sous-arbres séparés.

---

#### Analyse de complexité <un nom="complexité"></a>

Calcul métrique
C'est pas vrai.
Chaque nœud visité une fois → **O(N)**
**L'espace**= empilement de la récursion jusqu'à la hauteur de l'arbre **H** → **O(H)** (= N pour le plus mauvais arbre biaisé). Autres

---

#### Code Walkthrough – Java, Python, C++ <a name="code"></a>

> *Les trois échantillons de code ci-dessus sont annotés. Choisissez la langue avec laquelle vous êtes le plus à l'aise, faites les tests et vous passerez en 15 minutes. *

- **Java** utilise une classe intérieure statique `Résultat` pour garder `(noeud, profondeur)` ensemble.
- **Python** retourne un tuple ; la profondeur de récursion est automatiquement gérée par l'interprète de Python.
- **C++** retourne un `std::pair<TreeNode*, int>` pour des frais généraux minimes.

---

#### Autres approches et pourquoi elles sont moins efficaces <un nom="alternatives"></a>

Défaut de complexité
- C'est quoi ?
**Two-pass BFS**. Premier passage pour trouver la profondeur maximale, deuxième pour trouver LCA via l'ancêtre ensemble. O(N) temps *mais* mémoire supplémentaire O(N) pour stocker les chemins d'ancêtre. Autres
**Level-by-level traversal**= Rassemblez toutes les feuilles les plus profondes, puis lancez un LCA générique sur cette liste. Nécessite des structures de données supplémentaires, plusieurs passages, O(N) espace supplémentaire. Autres
**Itérative Post-order**Éviter la récursion, mais a besoin d'une pile qui tient la paire pour chaque nœud. Plus de verbosité de code; aucun avantage réel sur la récursion pour N ≤ 1000. Autres

> *Un seul DFS qui retourne une paire est le standard d'or.

---

#### Conseils d'entrevue et points de discussion <un nom></a>

1. **Expliquer l'idée de la paire d'abord** – les recruteurs apprécient une carte de résolution de problèmes claire.
2. **Énoncez explicitement le cas de base** – la profondeur de `null` est `0`.
3. **Montrer que vous comprenez les limites de récursion** – dans Python, mention `sys.setrecursionlimit(2000)` pour la sécurité.
4. **Alignement du temps O(N)** – contraste avec des solutions naïves.
5. **Connecter au problème 865** – s'il est demandé, « Connaissez-vous un problème similaire ? » Vous pouvez mentionner la réutilisation de l'algorithme.

---

#### Take-away final & Lecture supplémentaire <a name="final"></a>

- **On passe DFS** qui retourne une paire vous donne à la fois la profondeur la plus profonde * et* la LCA en temps linéaire.
- Oui. Ce modèle est un élément de construction réutilisable pour de nombreux problèmes de type «deepest‐node».
- Maîtrisez la nuance entre *leaf count* et *profondeur* – c'est là que la plupart des intervieweurs repèrent des solutions faibles.
- **Pour en savoir plus** :
- LeetCode 865 – Le plus petit sous-arbre avec tous les nœuds les plus profonds
- Cracking the Coding Interview – Chapitre 4 (Trees & Graphs)
- Algorithmes + Structures de données par Goodrich & Tamassia (modèles DFS)

> *Maintenant, vous êtes prêt à entrer dans cette interview, expliquer les points bons, mauvais, laids, et partir avec la LCA de toutes les feuilles les plus profondes sous votre ceinture. *

---

** Bon codage, et que votre prochaine entrevue soit parfaite pour votre ensemble de compétences! * *