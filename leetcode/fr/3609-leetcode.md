---
titre: LeetCode 3609. Déplacements minimums pour atteindre la cible dans la grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3609 – Déplacements minimum pour atteindre la cible dans la grille
*LeetCode – dur*

---

### TL;DR
*Renverser les mouvements* est la clé.
À partir de la cible `(tx, ty)`, plusieurs fois **soustraire** la plus petite coordonnée de la plus grande.
Lorsque la plus grande coordonnée est *au moins deux fois* la plus petite, elle doit avoir été *double* dans la direction avant – donc nous **divisons par 2**.
Si une division produit une fraction, la cible est impossible.
Lorsque nous avons finalement atteint le point de départ `(sx, sy)` nous avons la réponse.
Complexité: **O(log max(tx, ty)** temps, **O(1)** espace.

---

## 1-

> Compte tenu de quatre entiers `sx, sy, tx, ty` (avec `0 ≤ sx ≤ tx ≤ 109` et `0 ≤ sy ≤ ty ≤ 109`), vous commencez par `(sx, sy)` sur une grille infinie.
> À tout moment `(x, y)` let `m = max(x, y)`. Vous pouvez **ajouter `m`** à chaque coordonnées:
> * `(x + m, y)` ou
> * `(x, y + m)`
>
> Trouvez le nombre **minimum** de déplacements requis pour atteindre `(tx, ty)`.
> Retour `-1` si c'est impossible.

Exemples
Explication Autres
-- -- -- -- -- -- -- -- -- -- -- -- --
2 : 2 : 2 : 2 : 2 : 2 : 2 : 2 : 1 : 4 : Autres
0=1=2=3=3=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=2=2=2=2=2=2=2=2=2=2=2=2=2=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1= Autres
Voir notes

---

# # # , , Intuition

Une recherche naïve de largeur-première exploserait (la grille est infinie).
Au lieu de cela, pensez *en arrière*.

Si nous sommes à `(x, y)` et que nous connaissons le dernier mouvement qui l'a produit, nous pouvons déduire quelle était la position précédente:

Dernier déménagement
C'est quoi, ça ?
"x += max(prev)"""x" était la plus grande coordonnée, donc c'était **doubled** → "prev = x / 2"
"y += max(prev)"""y" était la plus grande coordonnée, donc c'était **doubled** → "prev = y / 2"
"x += max(prev)"""x" était la plus petite coordonnée, donc il a été **ajouté** → `prev = x - y"
"y += max(prev)"""y" était la plus petite coordonnée, donc il a été **ajouté** → `prev = y - x` Autres

L'opération inverse est toujours *déterministe* une fois que nous savons quel cas détient.

**Pourquoi la division par 2? **
Si la plus grande coordonnée est au moins deux fois la plus petite, la seule façon de l'augmenter en une seule étape est de s'ajouter (douleur).
Sinon l'augmentation est venue de la plus petite coordonnée, donc nous soustravons.

---

Algorithme (BFS révisé)

«» "
mouvement = 0
alors que tx ≥ sx et ty ≥ sy:
if tx == sx et ty == sy: retour se déplace
si tx > ty:
si tx ≥ 2 * ty:
si tx est bizarre: retourner -1
tx //= 2
Sinon:
Tx -= ty
sinon si ty > tx:
si ty ≥ 2 * tx:
si ty est bizarre: retour -1
ty //= 2
Sinon:
ty -= tx
Sinon : ty
# ne peut pas réduire davantage à moins que l'une des coordonnées de départ soit 0
if sx == tx et sy == ty: retour se déplace
sinon: retour -1
mouvements += 1
retour -1
«» "

*Pourquoi le `>=` Des chèques ? *
Si l'une ou l'autre des coordonnées de la cible devient plus petite que la coordonnée de départ correspondante, nous ne pouvons jamais atteindre la cible dès le début parce que les mouvements augmentent seulement les coordonnées.

---

- Oui. Tranche Liste de contrôle des cas

Résultat
C'est pas vrai.
(tx, ty)
"sx == 0 & & sy == 0` et cible pas `(0,0)` `-1` (ne peut pas créer de coordonnées non nulles lorsque les deux sont zéro)
Plus grande coordination bizarre quand nous avons besoin de diviser par 2
"tx == ty` mais pas égal à `(sx, sy)`" `-1` (ne peut pas réduire une paire égale à moins qu'une coordination de démarrage soit 0)
Autres Toute coordonnée devient < coordonnées de démarrage

---

Mise en œuvre

Voici des implémentations propres et prêtes à la production pour **Java**, **Python** et **C++**.
Tout fonctionne dans le temps `O(log max(tx, ty)` et n'utilise que de l'espace supplémentaire constant.

#### 5.1 Java

"Java
solution de classe {
Int minMoves(int sx, int sy, int tx, int t ty) {
si (sx) tx && sy == ty) retourne 0;
si (sx > tx=" sy > ty) retourner -1;

mouvement int = 0;
(tx >= sx && ty >= sy) {
si (tx == sx && ty == sy) retourne des mouvements;

si (tx > ty) {
si (tx >= 2 * ty) {
si ((tx & 1)) 1) retour -1; // impair
tx >>= 1; // diviser par 2
} autre {
tx -= ty; // moins
}
} sinon si (ty > tx) {
si (ty >= 2 * tx) {
Si (ty & 1)] 1) retour -1;
ty >>= 1;
} autre {
ty -= tx;
}
} autre { // tx == ty
retour -1; // paire égale ne peut pas être réduite
}
mouvements++;
}
retour -1;
}
}
«» "

5.2 Python

'`python
Solution de classe:
def minMoves(self, sx: int, sy: int, tx: int, ty: int) -> Int:
Si sx == tx et sy == ty:
retour 0
si sx > tx ou sy > ty:
retour -1

mouvement = 0
alors que tx >= sx et ty >= Oui.
Si tx == sx et ty == sy:
retour

si tx > ty:
si tx >= 2 * ty:
Si tx % 2: # impair
retour -1
tx //= 2
Sinon:
Tx -= ty
ë > tx:
si ty >= 2 * tx:
si ty % 2:
retour -1
ty //= 2
Sinon:
ty -= tx
Sinon : ty
retour -1
mouvements += 1
retour -1
«» "

C++

'`cpp
solution de classe {
public:
int minMoves(int sx, int sy, int tx, int t ty) {
si (sx) tx && sy == ty) retourne 0;
si (sx > tx=" sy > ty) retourner -1;

mouvement int = 0;
(tx >= sx && ty >= sy) {
si (tx == sx && ty == sy) retourne des mouvements;

si (tx > ty) {
si (tx >= 2 * ty) {
si (tx & 1) retourne -1; // impair
tx >>= 1; // diviser par 2
} autre {
tx -= ty;
}
} sinon si (ty > tx) {
si (ty >= 2 * tx) {
si (ty & 1) retour -1;
ty >>= 1;
} autre {
ty -= tx;
}
} autre { // tx == ty
retour -1;
}
+ mouvements;
}
retour -1;
}
};
«» "

---

Analyse de complexité

Valeur métrique
C'est pas vrai.
**Temps**="O(log max(tx, ty)"– chaque boucle coupe la plus grande coordonnée en deux ou la soustrait, les deux réductions logarithmiques="
**Espace** – seulement une poignée de variables entières

Pour le cas le plus défavorable `(0,0) → (109,109)`, la boucle tourne au plus ~30 fois.

---

C'est pas vrai. Bon / mauvais / Méchant

Catégorie Que mettre l'accent sur / éviter
- C'est quoi ?
**Bon**• La logique déterministe inverse élimine le besoin de BFS. <br>• Fonctionne pour 109 bornes sans débordement (utiliser des entiers 64 bits si vous voulez une sécurité supplémentaire). Autres
**C'est mal** 2 * condition min ' peut laisser l'algorithme choisir la mauvaise opération, en retournant une réponse incorrecte. <br>• Ignorer le "odd en divisant" vérifie les résultats erronés pour des cibles comme `(3,4"). Autres
**La mise en œuvre d'un BFS ou DFS avancé est une recette pour les temps d'arrêt et les erreurs de mémoire. <br>• L'utilisation de la division flottante dans l'étape inverse (p. ex. `tx / 2.0`) introduit des erreurs d'arrondi; restez avec l'arithmétique entier. Autres

---

FAQ

Question Réponse
C'est pas vrai.
*Pourquoi la division est-elle toujours en sécurité quand `plus grande ≥ 2 * plus petite'?* La seule façon dont la plus grande coordination aurait pu augmenter à sa valeur actuelle en une seule étape vers l'avant est de s'ajouter (doublant). S'il s'agissait de la plus petite coordination, la croissance aurait été inférieure au double de la plus petite valeur. Autres
*Et si les deux coordonnées sont égales à un moment donné?* La seule façon d'atteindre une paire égale depuis le début est si l'une des coordonnées de début était zéro. Sinon nous ne pouvons pas réduire la paire plus loin, donc le chemin est impossible. Autres
*Puis-je encore utiliser BFS sur ce problème? Vous pouvez, mais vous avez besoin de stocker l'installation visitée jusqu'à 109 étapes – impossible. L'algorithme inverse est l'approche conviviale de l'entrevue. Autres
*Est-ce que cet algorithme fonctionnera pour les coordonnées négatives? Le problème garantit des coordonnées non négatives, mais si vous voulez une solution générique, vous devez gérer soigneusement les signes. Autres

---

Conclusion

*Réverser le mouvement* transforme un problème de réseau infini en algorithme cupide logarithmique.
L'idée de base—**= Diviser quand on voit un grand saut; sinon soustraire==**– fonctionne dans les trois langues et est assez simple à expliquer en 5 minutes pendant une entrevue.

Utilisez cette solution comme agrafe **code-review** ou déposez-la dans votre bibliothèque personnelle LeetCode.

---

Mots clés

- Déplacements minimum pour atteindre la cible dans la grille
- LeetCode 3609 – dur
- Algorithme du mouvement de la grille
- Solution BFS inversée
- Java, Python, implémentations C++
- Préparation de l'entrevue, entretien de codage, structures de données

---

Bon codage, et que vos futurs intervieweurs soient éblouis par votre pensée **réversive**