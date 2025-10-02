---
titre: LeetCode 1533. Trouvez l'index du grand entier -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1533 – Trouvez l'index du grand entier
**LeetCode**. **Moyenne**.

> **Problème:**
> On vous donne un tableau entier `arr` dans lequel *tous* les éléments sont égaux **sauf** un élément strictement plus grand.
> Le tableau est **non** exposé directement; vous pouvez seulement appeler
> ```texte
> reader.compareSub(l, r, x, y) // compare les sommes de arr[l..r] et arr[x..y]
> reader.length() // retourne la taille du tableau
> `` "
> Chaque appel à `compareSub` est O(1) et vous ne pouvez faire que **20 appels**.
> Retourne l'index de l'élément le plus important.

---

## Pourquoi ce problème (et pourquoi c'est une bonne question d'entrevue)

C'est vrai.
- Oui.
*Supérieur* – 20 appels est une limite difficile mais réaliste qui force une **log‐ Solution N**. *Vibe du monde réel* – il simule l'accès aux données via une API distante, un scénario auquel font face de nombreux ingénieurs. Autres
*Twist de recherche binaire classique* – vous devez décider d'inclure ou non l'élément intermédiaire. *Flexibilité* – peut être résolu en Java, Python, C++, etc. Autres
*Les contraintes claires* – tous les nombres sont égaux sauf un, vous pouvez donc compter sur la comparaison de la somme. *Testez votre compréhension des bugs hors-par-un* – l'écueil de la ligne de démarcation par rapport à la longueur est l'endroit idéal. Autres

---

- Oui. L'intuition

Si on divise le tableau en deux moitiés et compare leurs sommes:

* Si les sommes sont égales → l'élément spécial est exactement au milieu de l'index.
* Si la somme de gauche est plus grande → l'élément spécial doit se trouver dans la moitié gauche.
* Si la bonne somme est plus grande → il doit se trouver dans la moitié droite.

La seule subtilité : ** inclure l'élément du milieu dans la moitié gauche ou droite**.
Parce que tous les autres éléments sont identiques, l'élément au milieu est le seul qui peut pointer l'échelle lorsque les longueurs subarray sont *even*.

---

## Algorithme (Recherche binaire avec la manipulation des problèmes)

«» "
l = 0
r = longueur du lecteur() – 1

alors que l < r:
m = (l + r) // 2 // indice intermédiaire

// Lorsque la longueur du segment (r - l + 1) est impair,
// l'élément du milieu appartient au côté gauche
// à des fins de comparaison.
si (r - l + 1) % 2 == 1:
// Comparer [l.m.] avec [m+1..r]
res = reader.compareSub(l, m, m + 1, r)
Sinon:
// Comparer [l.m] avec [m.r]
res = reader.compareSub(l, m, m, r)

si res == 0:
retour m // trouvé l'index spécial
elif res == 1: // côté gauche est plus lourd
r = m
sinon: // le côté droit est plus lourd
l = m + 1

retour l // l == r est la réponse
«» "

* **Complexité temporelle**: `O(log n)` – au plus 20 appels pour `n ≤ 5·105`.
* **Complexité spatiale**: "O(1)" – seulement quelques variables.

---

## Mise en œuvre du code

> *Toutes les solutions supposent l'existence de l'interface `ArrayReader` telle que définie par LeetCode. *

C'est pas vrai. Java

"Java
solution de classe publique {
int public getIndex(Lecteur de lecture d'image) {
Int l = 0;
int r = lecteur.longueur() - 1;

pendant que (l < r) {
m = l + (r - l) / 2;

ant rés;
// (r - l + 1) est la longueur du segment actuel
si (r - l + 1) % 2 == 1) {
res = reader.compareSub(l, m, m + 1, r);
} autre {
res = reader.compareSub(l, m, m, r);
}

Si (rés) 0) {
retour m;
} sinon si (res) 1) {
r = m; // élément spécial à gauche
} autre {
l = m + 1; // élément spécial à droite
}
}
retour l; // l == r
}
}
«» "

Python (3.x)

'`python
Solution de classe:
def getIndex(self, reader: 'ArrayReader') -> Int:
l, r = 0, longueur du lecteur() - 1

alors que l < r:
m = (l + r)/ 2

si (r - l + 1) % 2 == 1:
# longueur étrange -> côté gauche inclus milieu
res = reader.compareSub(l, m, m + 1, r)
Sinon:
# même longueur -> côté droit comprend milieu
res = reader.compareSub(l, m, m, r)

si res == 0:
retour
élif rés == 1:
r = m
Sinon:
l = m + 1

retour l
«» "

C++ (GNU++17)

'`cpp
solution de classe {
public:
int getIndex(ArrayReader &reader) {
int l = 0, r = lecteur.longueur() - 1;

pendant que (l < r) {
m = l + (r - l) / 2;

ant rés;
si (r - l + 1) % 2 == 1) {/ segment impair
res = reader.compareSub(l, m, m + 1, r);
} autre { // même segment
res = reader.compareSub(l, m, m, r);
}

Si (rés) 0) retour m;
Sinon, si (res) 1) r = m;
autres: l = m + 1;
}
retour l;
}
};
«» "

---

- Oui. La bonne, la mauvaise et la mauvaise

C'est bien C'est mal
- C'est quoi ?
**La solution O(log n)** respecte la limite de 20 appels. Le fait de ne pas gérer le fractionnement occasionne une erreur **off‐by‐one**. Autres
Autres Code clair et court qui passe facilement les tests. Certains candidats écrivent une solution récursive qui fuit la pile ou mal compte les appels. L'écriture d'une maquette personnalisée `ArrayReader` pour les tests locaux peut être lourde mais est essentielle pour le débogage hors ligne. Autres

---

Variations et extensions

1. **Deux plus grands nombres** – Une seconde recherche binaire sur le segment restant après avoir trouvé le premier grand nombre localisera le second.
2. **Un grand et un petit nombre** – Divisez le tableau en trois parties et comparez deux moitiés; la différence vous indique si l'élément spécial est grand ou petit.
3. **Pas d'API, tableau brut** – La même logique se réduit à une recherche binaire classique où vous comparez les valeurs des éléments directement.

---

## À emporter pour votre chasse à l'emploi

* **Maîtrise de la recherche binaire Showcase** – Les intervieweurs aiment voir une solution O(log n) propre à un problème d'API apparemment complexe.
* ** Expliquez votre processus de pensée** – Mentionnez l'étrange/même scission; parlez de la façon dont vous manipulez la nature abstraite de l'API.
* **Faire ressortir les contraintes** – Souligner comment votre solution reste dans la limite de 20 appels.
* ** Testabilité de la concentration** – Partagez la façon dont vous vous moquez `ArrayReader` pour les tests unitaires – un conseil pratique pour coder des entrevues.

---

## SEO-Friendly Blog Titre

> Code de sortie 1533 – Trouvez l'index du grand entier : une classe de recherche binaire (Java/Python/C++)

**Meta Description:**
Apprenez la solution O(log n) à LeetCode 1533. Comprendre l'impair/même split trick, lire le code complet Java, Python et C++, et obtenir l'interview-prêt avec ce guide d'algorithme.

---

Bon codage – et que votre prochaine interview soit aussi lisse que cette recherche binaire!