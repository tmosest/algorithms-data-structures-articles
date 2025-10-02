---
titre: LeetCode 3360. Jeu de suppression de pierre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3360. Jeu de suppression de pierre – Code, théorie et entrevue‐ Prêt Blog Post
C++*

---

### TL;DR
- **Problème**: Deux joueurs retirent alternativement les pierres d'une pile.
*Alice* commence par enlever ** exactement 10** pierres.
Chaque mouvement ultérieur enlève **une pierre de moins** que le dernier mouvement de l'adversaire.
Celui qui ne peut pas bouger perd.
- **Objectif**: Retour `vrai` si Alice gagne pour un `n` donné, sinon `faux`.
- **Observation**: Le jeu est complètement déterministe – il suffit de simuler la séquence décroissante `10, 9, 8, ...`.
- **Complexité**: `O(k)` où `k ≤ 10` (depuis le premier mouvement est 10).
- **Mise en oeuvre**: boucle directe en Java, Python et C++.

> **Conseil pro**: Le motif est le premier mouvement 10, puis 9, ...
> Après chaque soustraction, retournez le joueur.
> Lorsque vous pouvez soustraire, le joueur actuel perd, de sorte que l'autre* joueur gagne.

---

## 1-

> **Stone Removal Game**
> *Alice et Bob jouent un jeu avec une pile de pierres `n`. *
> 1. Alice commence, enlevant ** exactement 10** pierres.
> 2. À chaque tour ultérieur, un joueur enlève **1 pierre moins** que le dernier mouvement de l'adversaire.
> 3. Si un joueur ne peut pas bouger (c.-à-d. que les pierres restantes sont inférieures à la suppression requise), ils perdent.
> **Retour** `true` si Alice gagne, sinon `faux`.

> **Contraintes**: «1 ≤ n ≤ 50»
> **Exemple**
> `n = 12` → Alice prend 10 → 2 pierres à gauche → Bob a besoin de 9 → ne peut pas → **Alice gagne**.

---

## 2-

Aspect du bien
- C'est quoi ?
**Simplicité**=Loop O(1) avec au plus 10 itérations. Aucun.
**Déterministe**
**Cas d'escroquerie**
*Readability**= Effacer les noms de variables (`stonesToRemove`, `turn`).
**Scalabilité**= Fonctionne pour toute liaison supérieure parce que la longueur de la boucle ≤ 10.= Si le premier mouvement a changé pour une variable `k`, toujours O(k).==

> **Pourquoi c'est "good"** – la simulation gourmande est littéralement la règle; aucun astuce mathématique n'est nécessaire.
> **Pourquoi il s'agit de "bad"** – certains pourraient essayer la suringénierie (programmation dynamique, mémoisation) lorsqu'une boucle d'un liner suffit.
> **Pourquoi il s'agit de "gugly"** – la seule astuce est de se souvenir de retourner le joueur après chaque tour; un petit glissement donnera la mauvaise réponse.

---

- Oui. Algorithme (Pseudocode)

«» "
tour = 0 // 0 → Alice, 1 → Bob
Pierres Supprimer = 10

alors que n >= Pierres Pour supprimer :
n -= pierres Supprimer
Pierres Supprimer -= 1
tour = 1 - tour // Changer de lecteur

retour du tour == 1 // si le dernier tour était Bob → Alice gagne
«» "

La boucle s'arrête lorsque le lecteur actuel ne peut pas faire le déplacement requis.
`turn` indique le *joueur qui vient de bouger*.
Si la boucle se termine parce que le joueur *next* ne peut pas bouger, le gagnant est celui qui vient de bouger (`turn`).

---

Mise en œuvre du code

### Java

"Java
solution de classe {
boîte de booléen publiqueAliceWin(int n) {
tour int = 0; // 0 = Alice, 1 = Bob
pierre d'inte Supprimer = 10;

pendant que (n >= pierresEnlever) {
n -= pierres Supprimer;
Pierres Retirer...
tour = 1 - tour; // commutateur
}
Retour du tour == 1; // Bob vient de bouger, Alice gagne
}
}
«» "

Python

'`python
Solution de classe:
def canAlice Gagner (soi-même, n: int) -> C'est vrai.
tour = 0 # 0 = Alice, 1 = Bob
pierre_à_supprimer = 10

alors que n >= stones_to_supprime:
n -= pierres_à_supprimer
pierres_à_supprimer -= 1
tourner ^= 1 # flip 0/1

Retourner le tour == 1
«» "

C++

'`cpp
solution de classe {
public:
Poudre de boolAliceWin(int n) {
tour int = 0; // 0 = Alice, 1 = Bob
pierre d'inte Supprimer = 10;

pendant que (n >= pierresEnlever) {
n -= pierres Supprimer;
--pierres Supprimer;
tourner ^= 1; // basculer 0/1
}
Retour du tour == 1; // Bob vient de bouger → Alice gagne
}
};
«» "

Les trois solutions fonctionnent dans **O(1)** temps et **O(1)** espace.
La boucle exécute au plus 10 itérations (pour `n = 50`), de sorte que l'exécution est essentiellement constante.

---

Analyse de complexité

La complexité Raison
C'est pas vrai.
Au plus 10 itérations → **O(1)** Autres
**L'espace** Autres

Même avec une limite supérieure plus élevée sur `n`, la boucle continuerait à fonctionner au plus `min(10, n)` fois parce que le nombre de suppression diminue d'un tour.

---

Essais et cas de bord

Explication
C'est pas vrai.
Alice ne peut pas enlever 10 pierres. Autres
"vraie" Alice prend toutes les pierres, Bob perd immédiatement. Autres
11.00 `false`.00 Alice prend 10 → 1 gauche → Bob a besoin de 9 → perd. Autres
Exemple de la déclaration. Autres
Faux : Alice (10), Bob (9), Alice (8), ... jusqu'à ce que Bob ne puisse pas bouger. Autres

Effectuez un test d'unité rapide dans votre langue de choix pour vérifier les cas ci-dessus.

---

## 7--Des conseils d'entrevue

Pourquoi ça aide ?
C'est quoi ?
**Exposer la règle** avant le codage. Montre que vous comprenez les contraintes du problème. Autres
** Indiquer l'invariant**: Les pierres restantes sont `n`, le prochain retrait est `k`. Autres
**Éviter le DP**. Autres
**Caisse de bord de Mention** (`n < 10`). Démontre la rigueur. Autres
Autres **Afficher la logique gagnante** (`tour == 1`). Clarifie qui gagne quand la boucle se termine. Autres

---

Conclusion optimisée du SEO

Si vous préparez pour les interviews de codage, maîtrisez *LeetCode 3360 – Stone Removal Game* prouve que vous pouvez gérer des simulations avides, des boucles simples et des analyses de cas de bord – tous essentiels pour l'embauche technique.

**Traitements clés* *
- Oui. Le jeu est déterministe; une boucle droite suffit.
- La complexité est O(1) avec au plus 10 itérations.
- Implémenter proprement dans **Java, Python et C++** pour la confiance en la langue-agnostique.

Prêt à accepter votre prochain entretien ? Montrez cette solution aux recruteurs, ajoutez-la à votre GitHub, et mentionnez-la dans votre CV sous Algorithms & Problem Solving.

---

Référence Mots clés

- LeetCode 3360
- Jeu de suppression de pierre
- Entretien de codage
- Solution Java
- Solution Python
- Solution C++
- Questions d'entretien avec l'algorithme
- Problème de théorie du jeu
- Préparation de l'entrevue
- Conseils techniques d'embauche

Bon codage – et que les chances d'entrevue d'emploi soient en votre faveur!