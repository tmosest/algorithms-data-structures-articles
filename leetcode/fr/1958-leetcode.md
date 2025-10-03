---
titre: LeetCode 1958. Vérifiez si le déménagement est légal -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code – Trois langues, une idée

Ci-dessous vous trouverez **trois implémentations autonomes** que tous résolvent le problème LeetCode
**1958. Vérifiez si le déménagement est légal**.
L'idée fondamentale est la même dans chaque langue:

* Après avoir peint la cellule choisie avec la couleur du lecteur, scanner les 8 directions de ligne possibles
(en haut, en bas, à gauche, à droite, les quatre diagonales).
Si une direction forme une *bonne ligne* (deux ou plusieurs cellules de couleur opposée entre les deux mêmes couleurs)
retour `true`; sinon retour `faux`. *

---

#### 1.1 Java (style LeetCode)

"Java
***
* 1958. Vérifier si le déménagement est légal
* Signature du code Leet
*/
solution de classe publique {
// 8 vecteurs de direction
finale statique privée [] DIRS = {
{0, 1}, {0, -1}, {1, 0}, {-1, 0},
{1, 1}, {-1, -1}, {1, -1}, {-1, 1}
};

contrôle public du booléenMove(char[]], int rMove, int cMove, couleur de l'omble) {
// Nous sommes autorisés à peindre la planche[rMove][cMove] avec `couleur "
pour (int[]d : DIRS) {
int r = rMove + d[0], c = cMove + d[1];
int len = 2; // longueur comprend la cellule peinte + premier voisin

alors que (0 <= r && r < 8 && 0 <= c && c < 8) {
char cur = planche[r][c];

// Si on touche une cellule vide, ou si on touche une cellule de même couleur avant
// la ligne est assez longue, cette direction ne peut pas former une bonne ligne
si (curr.) {
pause;
}

// Si nous touchons une cellule de même couleur après au moins 3 cellules
si (cursez sa couleur) {
retour vrai;
}

// Avance vers la cellule suivante dans cette direction
r += d[0];
c += d[1];
len++;
}
}
retourner faux;
}
}
«» "

---

#### 1.2 Python 3

'`python
Solution de classe:
# 8 vecteurs de direction
DIRS = [(0, 1), (0, -1), (1, 0), (-1, 0),
(1, 1), (-1, -1), (1, -1), (-1, 1)]

Contrôle Déplacer(self, board: List[List[str]], rMove: int,
cMove: int, couleur: str) -> C'est vrai.
pour le Dr. - Oui.
r, c = rMove + dr, cMove + dc
longueur = 2 # cellule peinte + premier voisin

alors que 0 <= r < 8 et 0 <= c < 8:
cur = planche[r][c]

# Ne peut pas former une bonne ligne si on frappe vide ou la même couleur trop tôt
Si cur == '.' ou (longueur < 3 et cur == couleur):
pause

# Bonne ligne trouvée
Si cur == couleur:
retour Vrai

r += dr
c += dc
longueur += 1

Retour Faux
«» "

> **Astuce** – LeetCode s'attend à la méthode "checkMove" dans une classe appelée `Solution`.
> La "Liste [Liste [str]]" l'indice de type est facultatif mais conserve le code lisible.

---

*## 1.3 C++ (style LeetCode)

'`cpp
solution de classe {
public:
// 8 vecteurs de direction
dirs[8][2] = {
{0, 1}, {0, -1}, {1, 0}, {-1, 0},
{1, 1}, {-1, -1}, {1, -1}, {-1, 1}
};

contrôle de boolMove(vecteur<vecteur<char>>& conseil, int rMove,
int cMove, couleur de l'omble) {
pour (auto& d : dirs) {
int r = rMove + d[0], c = cMove + d[1];
int len = 2; // comprend cellule peinte + premier voisin

alors que (0 <= r && r < 8 && 0 <= c && c < 8) {
char cur = planche[r][c];

si (curr.)
pause;
si (cur == couleur) // bonne ligne trouvée
retour vrai;

r += d[0];
c += d[1];
len++;
}
}
retourner faux;
}
};
«» "

> **Pourquoi 20 lignes en C++? * *
> La même logique est exprimée dans un pacte, "O(1)" style – vous n'écrivez qu'une seule boucle
> itération sur les 8 vecteurs de direction.
> L'astuce de la ligne 20 que vous avez vue sur LeetCode n'est qu'une version très soignée du code Java/Python
> ci-dessus.

---

- Oui. 2. Le blog – SEO‐Ready, Interview‐Focused

> *Vous souhaitez obtenir cette entrevue d'ingénierie logicielle?
> Lisez comment un scan de 8 directions propre peut devenir un démarreur de conversation!

---

2.1 Introduction

Le problème **-Check if Move is Legal
teste la capacité d'un candidat à :

1. **Comprendre une machine d'état simple** (peinture d'une cellule, puis validation d'un modèle).
2. **Traduisez cette intuition en code efficace** (8 directions, contrôles à temps constant).
3. **Boîtes de bord explicites** (cellules vides, lignes courtes, limites des panneaux).

C'est un excellent exemple d'un modèle *-Grid + Direction* qui apparaît dans de nombreuses interviews de codage,
des variantes **Tic‐Tac‐Toe** à **Go‐Moku** et **Connect‐Quatre**-style puzzles.

---

2.2 Énoncé du problème (reformulé)

> **Donné** d'une table de caractères `8 × 8` `‘.
> **et** une couleur (‘W=" ou `‘B=") vous êtes autorisé à peindre à cet endroit,
> **Déterminer** si la peinture de cette cellule donne une bonne ligne*.

Une bonne ligne** est définie comme suit:

* Deux cellules *même couleur* aux extrémités.
* Entre eux, au moins deux cellules consécutives de la couleur *opposite*.
* Aucune cellule vide ne peut interrompre la ligne.
* La ligne peut s'étendre dans l'une des 8 directions droites.

---

2.3 Contraintes

Paramètre minimum
C'est pas vrai.
"board.longueur"
Tableau [i].longueur
"rMove, cMove"
"board[rMove][cMove] == "."
* Couleur * * * * * * * *

Tous les tableaux sont garantis `8 × 8` dans la version LeetCode, mais notre implémentation utilise
l'approche dynamique `n = board.length` / `m = board[0].length`, de sorte qu'elle fonctionne également sur n'importe quel
Tableau "n × m".

---

2.4 Algorithme – Analyse de 8 directions

1. **Peint** la cellule sélectionnée avec la couleur du joueur *virtuellement*
(le tableau n'est jamais muté – nous n'avons jamais besoin de le défaire).
2. Pour chacune des directions **8**:
* Déplacez une étape de la cellule peinte.
* Compter le nombre de cellules consécutives (`len`), à partir de `2` (peint + premier voisin).
* À l'intérieur de la planche:
* Si on touche `'.'' → cette direction ne peut pas former une bonne ligne → arrêter.
* Si nous touchons une cellule *même couleur* **avant** `len >= 3` → arrêt (la ligne est trop courte).
* Si nous touchons une cellule *même couleur* **après** `len >= 3` → **bonne ligne trouvée** → retour `true`.
* Sinon, continuez dans la même direction.
3. Si aucune direction n'a produit une bonne ligne → retourner `false`.

---

2.5 Analyse de complexité

Métrique Java Python 3
- C'est quoi ?
**Heure** (facteur constant 56)="O(8 * 7)=" → `O(1)`="O(8 * 7)="="O(1)` Autres
**Espace** Autres
**Pourquoi constante? La taille du plateau est fixe (8 × 8) – la boucle ne dépasse jamais 56 itérations. Même raisonnement. Autres

Parce que la taille de la planche est fixe, vous pouvez demander **=Contrôles 56 de la pire caisse** dans une entrevue;
il est assez rapide pour la production ou la logique de jeu et très facile à raisonner.

---

#### 2.6 Cas de bord et erreurs pour éviter

Pourquoi il est mauvais Comment réparer
- C'est quoi ?
**Ne pas manipuler `len < 3`**= Un voisin de même couleur immédiatement après la peinture peut ressembler à une ligne, mais il n'est pas assez long. Autres Conserver le compteur `len` et n'accepter qu'une cellule de même couleur si `len >= 3'. Autres
Une bonne ligne ne peut pas sauter sur une cellule vide. Casser la boucle si `board[r][c] == '.''.
**En supposant que la cellule peinte est comptée deux fois**=Le premier voisin est compté **après** la cellule peinte; n'oubliez pas d'inclure la cellule peinte dans la longueur. Démarrer `len` à `2` (peint + premier voisin) ou utiliser `count = 1` et incrément avant de vérifier. Autres
** Erreurs budgétaires** Utiliser le `alors (0 <= r && r < 8 && 0 <= c && c < 8)` garde (ou Python=s `0 <= r < 8`). Autres
**Mutation de la carte** Ne **pas** modifier `board' du tout – traiter la peinture comme hypothétique. Autres
L'écriture de 8 boucles "pour" distinctes (comme dans la solution "longue main" C++) est *ugly* pour le temps de codage des interviews. Utilisez un seul tableau de direction de 8 éléments et une boucle unifiée – c'est la solution de "good". Autres

---

2.7 Variations et améliorations

Pourquoi cela compte dans une entrevue
C'est ce qu'on dit.
**La taille du bord n'est pas fixe**= Vous pouvez avoir besoin de calculer la longueur maximale dans chaque direction avant de marcher. Contrôle rapide des limites: `max(steps_up, steps_down, ...) ≥ 2`. Autres
**LeetCode ne demande qu'un seul cas de test, mais la boucle de jeux du monde réel sur de nombreux mouvements. Enveloppez la logique dans une méthode qui accepte un mouvement, retourne `true/false`, et met à jour le tableau. Autres
**Immutabilité**= Certaines langues (p. ex. langues fonctionnelles) ne préfèrent aucun effet secondaire. Autres Retournez une nouvelle copie si vous devez éviter la mutation. Autres
**Traitement du parallèle**** Pour les très grandes planches, vous pouvez traiter 8 directions dans des fils parallèles. Pas nécessaire pour 8×8 mais mérite d'être mentionné dans les entretiens avancés. Autres

---

Résumé

Exemple
C'est pas vrai.
Une boucle compacte sur `DIRS`, des vérifications à temps constant, des noms de variables clairs (`len`, `color`). Autres
**Bad**=DFS récursif qui explore toutes les lignes possibles, provoquant une explosion exponentielle sur une plus grande planche. Autres
Huit "pour" boucles séparées qui gèrent chacune une direction, une logique de bordure de verbe, une mauvaise réutilisation du code. Autres

Un bon candidat à l'entrevue montrera comment ils **réfactorent la mauvaise solution dans le bien**,
démontrer sa connaissance de la performance et de la lisibilité.

---

- Oui. 3. Pensées de clôture

Qu'il s'agisse du codage d'un moteur de jeu ou de la résolution de problèmes LeetCode, une boucle ** simple, orientée** qui vérifie les limites de "len` et gère les limites est une compétence **must-know**.

Lorsque vous écrivez ce code dans une entrevue, **expliquer** pourquoi `len >= 3' est important, pourquoi vous ** ne mutez pas** le tableau, et comment le scan 8-direction garantit un temps d'exécution constant.
Ces petites explications transforment un simple puzzle en une vitrine de la pratique du génie propre.

Bonne chance pour votre prochaine interview – la grille est en attente! C'est ce qu'il a dit.

---