---
titre: LeetCode 1926. Sortie la plus proche de l'entrée à Maze -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 1926 – Sortie la plus proche de l'entrée à Maze

**Résumé des problèmes**

Description
- C'est quoi ?
**But**= Trouvez le nombre minimum de marches d'une cellule d'entrée donnée à la sortie la plus proche (une cellule frontière vide) dans un labyrinthe `m × n`. Autres
**Déplacement**. Ne peut pas marcher dans les murs (`'+'`) ou à l'extérieur du labyrinthe. Autres
**Input**. Autres
**Extrait**= Étapes minimales jusqu'à la sortie la plus proche, ou `-1` si aucune n'existe. Autres
**Constraints**


La solution classique est **Breadth‐First Search (BFS)** – l'arbre le plus court dans un graphique non pondéré.
Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

---

- Oui. 2. Code – Trois langues

#### 2.1 Java – Un BFS propre et rapide

"Java
Importation de java.util.*;

solution de classe publique {
Int public le plus procheExit[[]] labyrinthe, entrée int[] {
rangées int = longueur du labyrinthe;
int cols = labyrinthe[0]. longueur;

// Directions: droite, gauche, en bas, en haut
int[]] dirs = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
Queue<int[]> q = nouveau ArrayDeque<>();
q.offre(entrée);
labyrinthe[entrée[0]][entrée[1]] = '+'; // marque visitée

Étapes int = 0;
alors que (!q.isEmpty()) {
pas++; // un calque = un pas
taille int = q.size();
pour (int i = 0; i < taille; i++) {
[] cur = q.poll();
pour (int[] d : dirs) {
Int r = cur[0] + d[0];
int c = cur[1] + d[1];
si (r < 0.
si (laze[r][c] == '+') continue; // mur ou déjà visité

// Sortie trouvée (à la frontière, mais pas à l'entrée)
si (r) r) les lignes 1 à 1 c)
les étapes de retour;

laze[r][c] = '+'; // marque visitée
q.offre(nouvelle int[]{r, c});
}
}
}
retour -1; // aucune sortie accessible
}
}
«» "

#### 2.2 Python – BFS simple avec `deque "

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def le plus procheExit(self, laze: List[List[str]]], entrée: List[int]) -> Int:
R, C = len(maze), len(maze[0])
dirs = [(0, 1), (0, -1), (1, 0), (-1, 0)]
q = deque([tuple(entrance)])
labyrinthe[][entrance[1]] = '+' # drapeau visité

étapes = 0
alors que q:
étapes += 1
pour _ dans la plage(len(q)):
r, c = q.popleft()
pour dr, dc en dirs:
nr, nc = r + dr, c + dc
si non (0 <= nr < R et 0 <= nc < C): # extérieur
poursuivre
Si labyrinthe[nr][nc] == '+': # mur / visité
poursuivre
# Sortie à la frontière (pas entrée)
si nr == 0 ou nr == R-1 ou nc == 0 ou nc == C-1:
étapes de retour
laze[nr][nc] = '+ '
q.annexe(nr, nc))
retour -1
«» "

#### 2.3 C++ – BFS avec "queue" (C++17)

'`cpp
#incluez <vecteur>
#incluez <queue>

solution de classe {
public:
nt le plus procheExit(std::vector<std::vector<char>>& labyrinthe, std::vector<int>&enter) {
int R = laze.size(), C = laze[0].size();
L'analyse de l'incidence de l'utilisation de l'eau sur l'environnement est fondée sur les résultats de l'évaluation de l'efficacité énergétique.
Les données suivantes sont disponibles:
};
L'annexe I du règlement (UE) no 1308/2013 est modifiée comme suit:
q.push({entrée[0], entrée[1]});
labyrinthe[entrée[0]][entrée[1]] = '+'; // pavillon visité

Étapes int = 0;
pendant que (!q.vide()) {
++étapes; // couche = étape
int sz = q.size();
pour (int i=0; i<sz; ++i) {
auto [r, c] = q.front(); q.pop();
pour (auto [dr, dc] : dirs) {
int nr = r + dr, nc = c + dc;
si (nr < 0. C) poursuivre;
si [laze[nr][nc]] == «+» continue;

// Sortie à la frontière (mais pas à l'entrée elle-même)
if (nr) Nr (nr) Nc (nr)
les étapes de retour;

laze[nr][nc] = '+';
q.push({nr, nc});
}
}
}
retour -1;
}
};
«» "

Les trois solutions fonctionnent en **O(m × n)** temps, en utilisant un drapeau visité en place (en convertissant les cellules en `‘+=").
Ils s'occupent de chaque cas de bord – entrée à la frontière, cellules isolées, grandes zones ouvertes – en toute sécurité.

---

- Oui. 3. Article de blog – Le bon, le mauvais, le mauvais de LeetCode 1926

---

La sortie la plus proche de l'entrée à Maze – LeetCode 1926
### L'approche BFS expliquée en Java, Python et C++
> * Prêt pour votre prochain entretien technique? Maîtrisez ce problème de chemin le plus court et brillez sur votre prochaine chasse au travail. *

---

## 3.1 Méta-Description
**Vous voulez ace LeetCode 1926?** Apprenez la solution BFS, voyez le code Java/Python/C++ propre, et découvrez le *bon, mauvais et laid* de ce problème d'interview classique. Idéal pour la préparation d'entrevues d'ingénierie logicielle.

---

## 3.2 Récapitulation des problèmes

> **La plus proche sortie de l'entrée à Maze* *
> Trouvez les quelques marches de l'entrée donnée à une cellule de bordure vide dans une grille 2-D où `'+'` sont des murs et `'.` sont des cellules à pied.

- **Taille brute:** «1 ≤ m, n ≤ 100»
- **Mouvement:** 4-directionnel (pas de diagonale)
- **Objectif:** Étapes minimales → `-1` si aucune sortie

---

Pourquoi BFS ? Le point de vue fondamental

* Tous les bords ont un poids 1* – le labyrinthe est un graphe ** non pondéré**.
BFS élargit les nœuds niveau par niveau; la première fois que nous avons touché une cellule frontière (sauf l'entrée), nous savons que nous avons la distance la plus courte.
Pas besoin de Dijkstra, pas de DP, pas d'heuristique – BFS simple est optimal.

---

3.4 Algorithme

1. **Mark Entrance** – Set `laze[entrance]` à un mur (`‘+") afin que nous ne le revisions jamais.
2. **Initialize Queue** – Poussez la coordonnée d'entrée.
3. ** Offsets directs** – `[(0,1),(0,1),(1,0),(1,0)]`.
4. **Élargissement de niveau par niveau**
- `steps++` avant le traitement du calque actuel.
- Pour chaque noeud de la couche, explorez les 4 directions.
- Sauter les cellules ou les murs.
- Si la nouvelle cellule se trouve à la frontière → **return** current `steps`.
- Autre marque telle qu'elle a été visitée («+» et enqueue).
5. **Pas de sortie** – Queue vide → retour `-1`.

---

## 3.5 Coin— Liste de contrôle des cas

Pourquoi ça compte ?
- Oui.
L'entrée sur la frontière peut être considérée comme une sortie → **ne doit pas** être comptée. Marquez l'entrée telle que visitée immédiatement. Autres
Autres Toutes les cellules sont des murs. Autres
Une grande zone ouverte La file peut grossir → utiliser `ArrayDeque`/`deque` (pas de frais généraux liés à la liste). Utiliser `ArrayDeque` en Java / `deque` en Python. Autres
Taille de l'entrée 100 × 100: 10 000 cellules max → fine pour la mémoire. Le marquage en place maintient le tableau visité hors de l'image. Autres

---

## 3.6 Bonne, mauvaise et mauvaise – Analyse en profondeur

Qu'est-ce qui est bon Qu'est-ce qui est mauvais
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**La force algorithmique**=Le BFS garantit l'optimalité, le temps O(mn), la mémoire O(mn). Nécessite une file d'attente – surcharge de l'attribution des objets en Java, liste dans Python. Aucun si vous oubliez de marquer visité → boucle infinie. Autres
**Codage Simplicité**=Place à quatre directions, comptage des couches, simple boucle. Très lisible, pas de récursion. Le marquage en place modifie l'entrée; si l'appelant réutilise le labyrinthe, cela est destructeur. Autres
**Performance** Le pire des cas visite chaque cellule → 10 000 ops (trivial). L'utilisation de `'+`' pour marquer la visite peut causer une erreur de cache si le labyrinthe est grand; une matrice séparée de `bool` pourrait être plus claire. Autres
**Robustness**=Poigne toute entrée valide, y compris la frontière. Il faut ignorer explicitement l'entrée comme sortie. Oublier de vérifier `si (r=0=)` peut donner une mauvaise distance lorsque l'entrée est déjà à la frontière. Autres
**Espace**= O(mn) avec drapeau visité en place; taille maximale de la file d'attente ~ périmètre.= Si vous utilisez une matrice `visite` séparée, vous doublez la mémoire. Si le labyrinthe est énorme (pas dans les contraintes), la profondeur de récursion/pique pourrait souffler dans les alternatives DFS. Autres

---

3.7 Performances et espace Échelles

Quand utiliser Impact
C'est pas vrai.
**In-place visited flag** (`maze[i][j] = '+')= Lorsque vous êtes autorisé à muter l'entrée (la plupart des problèmes de LeetCode). Enregistre le tableau booléen `O(mn)`. Autres
**Pré-alloquer le tableau des directions**= Empêche la création de 4 nouveaux `int[]` par noeud. Autres
**`ArrayDeque` au lieu de `LinkedList`** Autres
**Utilisez `deque` dans Python**=Python 3=1 `popleft()` est O(1) – plus rapide que la liste pop(0). Autres
**Layer-counting** (`steps++` hors boucle intérieure) Évite de suivre une distance par noeud. Autres
Autres **Vérification de sortie précoce** (si à la frontière) Arrête quand la première sortie est trouvée. Gagne du temps dans les labyrinthes clairsemés. Autres

---

## 3.8 Conseils d'entrevue – Comment faire face à cette question

1. ** Clarifier la définition d'une sortie**
*Une sortie est une cellule frontière vide qui est **pas** l'entrée elle-même. *

2. **Énoncez vos hypothèses**
*L'entrée est accessible à pied (''.'').
*Vous ne pouvez pas marcher dans les murs (`'+''). *

3. **Panier le graphique**
* Traitez chaque cellule comme un nœud; les bords relient les cellules adjacentes à pied. *

4. **Choisir BFS**
* Expliquez pourquoi BFS est le choix optimal : graphique non pondéré, chemin le plus court.
*Afficher que le DFS serait incorrect (pourrait trouver un chemin plus long). *

5. **Complexité**
*Temps: O(m × n).
*Espace: O(m × n) pour la file d'attente + drapeau visité. *

6. **Délibérations**
*Venez à travers l'entrée à la frontière.
* Expliquez comment vous évitez de le compter comme une sortie. *

6. **Écrire un code propre**
*Utilisez des boucles concises, évitez les structures de données redondantes.
*Dans Java, utilisez `ArrayDeque`. *

7. **Test sur votre téléphone**
*Si possible, lancez manuellement un exemple 3×3 pour illustrer le comptage des niveaux. *

---

## 3.9 Conclusion – Le départ

LeetCode 1926 peut ressembler à un simple puzzle de labyrinthe, mais il teste *l'intuition graph transverse* et *la manipulation bornaire*.
En maîtrisant la solution BFS – et en connaissant les bons, les mauvais et les mauvais détails – vous allez non seulement résoudre ce problème efficacement mais aussi démontrer:

- Une bonne compréhension des fondamentaux algorithmiques**.
- Oui. La capacité d'écrire **propre, le code prêt à la production**.
- Connaissance pratique des optimisations de performance**.

Bonne chance pour votre prochain entretien ! Les

---

## 3.10 Partager et discuter

> Vous avez trouvé cet article utile ? Laissez un commentaire ci-dessous avec vos propres hacks ou demandez de l'aide sur d'autres problèmes de LeetCode.
> **Codage heureux!**

---

* (fin de l ' article)*

---

- Oui. 4. Enroulement

Vous avez maintenant :

- **Trois implémentations testées** prêtes pour n'importe quel langage d'entrevue.
- Une plongée profonde dans *pourquoi BFS fonctionne*, comment éviter les pièges, et comment gérer chaque cas de bord.
- Un guide de style blog qui cadre le problème d'une manière que les intervieweurs aiment : hypothèses claires, raisonnement étape par étape, discussion de complexité et conseils sur le monde réel.

Utilisez ces connaissances pour renforcer votre portefeuille, impressionner les recruteurs et sécuriser ce rôle d'ingénierie logicielle de rêve. Joyeux hacking !

---

Bonne chance, codeur ! *