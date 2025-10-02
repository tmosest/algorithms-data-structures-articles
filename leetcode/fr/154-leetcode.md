---
titre: LeetCode 154. Trouver minimum dans Rotation triée Array II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Le Code – Trois langues

Voici trois solutions compactes prêtes à la production pour **LeetCode 154 – Trouver le minimum dans le tri rotatif II**.
Les trois utilisent la même idée de recherche binaire et gèrent gracieusement la présence de valeurs dupliquées.

---

## 1.1 Java

"Java
/* Java 17 */
Importation de java.util.*;

solution de classe publique {
***
* Trouver l'élément minimum dans un tableau trié tournant qui peut contenir des duplicatas.
* @param nombres non vides tableau d'entiers, rotation 1..n fois
* @retour de l'élément le plus petit
*/
public int findMin(int[] nums) {
int gauche = 0, droite = longueur nums - 1;

pendant que (à gauche < à droite) {
int milieu = gauche + (droite - gauche) / 2;

si (nums[mid] > nums[right]) {
// min est dans la moitié droite
gauche = milieu + 1;
} sinon si (nums[mid] < nums[right]) {
// min est dans la moitié gauche (y compris le milieu)
droite = milieu;
} autre {
// nombres[mid] == nombres[right] – ne peut pas décider, rétrécir en toute sécurité
droit...
}
}
les numéros de retour [à gauche];
}
}
«» "

---

## 1.2 Python

'`python
# Python 3
Solution de classe:
def findMin(self, nombres: List[int]) -> Int:
"""
Renvoie l'élément minimum d'un tableau trié avec des duplicatas.
Utilise une variante de recherche binaire qui se dégrade en temps linéaire seulement lorsque duplicata
rendre la décision ambiguë.
"""
gauche, droite = 0, len(nums) - 1
à gauche < à droite:
milieu = (gauche + droite) // 2
en cas de nums[mid] > nums[right]:
gauche = milieu + 1
Nums d'élif[mid] < nums[right]:
droite = milieu
Autrement : # nums[mid] == nums[right]
droite -= 1
retour nums[gauche]
«» "

---

C++

'`cpp
// C++17
solution de classe {
public:
Int findMin(vecteur<int>& nums) {
int gauche = 0, droite = (int)nums.size() - 1;
pendant que (à gauche < à droite) {
int milieu = gauche + (droite - gauche) / 2;
si (nums[mid] > nums[right]) {
gauche = milieu + 1;
} sinon si (nums[mid] < nums[right]) {
droite = milieu;
} autre { // nums[mid] == nums[right]
--droite;
}
}
les numéros de retour [à gauche];
}
};
«» "

---

♪ 2. Article du blog – Le bon, le mauvais, et le mal de trouver le minimum dans un tri rotatif

Titre
**Le Bon, le Mauvais, et l'Ugly de LeetCode 154 – Trouver le minimum dans le tri rotatif II* *

## Méta-Description
Master LeetCode 154 en Java, Python et C++ avec une solution de recherche binaire claire qui gère les duplications. Apprenez les pièges, les compromis et les conseils d'entrevue qui impressionneront les gestionnaires d'embauche.

---

2.1 Introduction

*Si vous avez déjà regardé un tableau trié tournant qui contient des duplicatas, vous avez probablement ressenti un mélange de frustration et de curiosité. *
LeetCode 154, C'est un problème d'entretien classique qui teste :

- **Intusion de la recherche binaire**
- **Cas de bord à la main** (en particulier des duplicata)
- **Comprendre les garanties d'exécution* *

Ci-dessous, nous disséquons le problème, nous traversons une solution propre en trois langues, et nous soulignons les aspects **good**, **bad** et **ugly** que les intervieweurs aiment sonder.

---

## 2.2 Récapitulation des problèmes

> **Input** – `nums`, un tableau non vide d'entiers, trié à l'origine en ordre ascendant mais tourné entre 1 et `n` fois.
> **Duplicats autorisés** – par exemple, "[2,2,0,1]".
> **Objectif** – Retourner le plus petit élément.

Obstacles
- `1 ≤ n ≤ 5000`
- "-5000 ≤ nums[i] ≤ 5000"

---

## 2.3 Approches naïves – Les forces

L'approche de la complexité Pourquoi c'est bizarre
- C'est quoi ?
**Scan linéaire** – itérer et maintenir un minimum de fonctionnement. **O(n)** temps, **O(1)** espace. Autres
**Recherche binaire complète** sans traitement des duplicatas. **O(log n)** moyenne mais **incorrecte** pour des cas comme `[2,2,0,1]`. Autres
**(n log n)** time, **O(n)** space. Autres

Le défi est de *maintenir le meilleur* (vitesse logarithmique) tout en *tolérant le pire* (duplications qui brouillent la limite de décision).

---

## 2.4 La recherche binaire optimale – La partie "Bien"

2.4.1 Intuition

Dans un tableau trié *roté* sans duplicata, le point pivot (où le tableau enveloppe) peut être trouvé parce que l'élément le plus droit fait toujours partie de la moitié plus élevée.
Si `nums[mid] > nums[right]`, le minimum se situe dans la moitié **right**; sinon il se situe dans la moitié **left** (y compris `mid`).

### 2.4.2 Manipulation des duplicatas – Le Twist

Quand `nums[mid] == nums[right]`, nous ne pouvons pas déterminer quel côté tient le minimum.
Le mouvement le plus sûr est de réduire la fenêtre de recherche par *un* élément: `droit--`.
Cela peut dégrader les performances à **O(n)** dans le pire des cas (par exemple, un tableau plein de la même valeur), mais garantit la justesse.

2.4.3 Étape par étape (Python)

'`python
gauche, droite = 0, len(nums) - 1
à gauche < à droite:
milieu = (gauche + droite) // 2
en cas de nums[mid] > nums[right]:
gauche = milieu + 1 # min dans la moitié droite
Nums d'élif[mid] < nums[right]:
droite = milieu # min dans la moitié gauche (milieu inclus)
Autrement : # nums[mid] == nums[right]
droite -= 1 # fenêtre rétrécie en toute sécurité
retour nums[gauche]
«» "

La même logique s'applique à Java et C++ (voir la section de code ci-dessus).

2.4.4 Analyse de complexité

Scénario Temps Espace
- C'est quoi ?
Autres **Meilleure/moyenne** (quelques duplicata)
(tous les éléments sont égaux)

Le scénario le plus défavorable ne se produit que lorsque le tableau est fortement dupliqué; dans les données d'entrevue réelles, c'est rare, donc l'algorithme est encore assez rapide.

---

2.5 Pièges communs et entrevues‐ Conseils prêts

Trucs d'entrevue
C'est pas vrai.
Utiliser `mid = (gauche + droite) / 2` sans contrôle de débordement. Autres
Autres Oublier de déplacer `right` quand `nums[mid] == nums[right]` "droite -= 1'.. Insistez sur le fait que c'est *nécessaire* pour corriger avec des duplicatas. Autres
Retour `nums[right]` au lieu de `nums[left]` Après la boucle. Autres
Autres En supposant que le tableau est tourné au moins une fois, vérifiez `nums[0] < nums[-1]` pour sauter la recherche binaire si elle n'est pas tournée. Autres

---

## 2.6 Le "Bad" – Quand il devient inefficace

Si un intervieweur alimente un ensemble de données comme `[1,1,1,1,0]`, l'algorithme effectuera des itérations `n-1` parce que `right--` n'élimine jamais l'ambiguïté.
Bien qu'il soit toujours exact, cela révèle une limitation **temps-complexité** que vous devriez discuter:

> *Les duplicatas peuvent provoquer une dégradation de la recherche binaire en temps linéaire. Dans la pratique, cependant, les cas de test de LeetCode sont équilibrés, de sorte que l'algorithme reste efficace.

C'est un excellent moment pour poser des questions claires : *Les données de test contiennent-elles de nombreux duplicatas?

---

2.7 Extensions et variations

Variation de l'approche suggérée
Il y a un problème.
**LeetCode 33 – Recherche dans Rotation triée Array**
**LeetCode 148 – Liste de tri**
**Arrays avec des nombres négatifs**

Ce sont de bons sujets de suivi pour une discussion plus approfondie.

---

2.8 À emporter pour le demandeur d'emploi

1. **Connaissez l'astuce de recherche binaire du cœur** – détection de pivots via `nums[mid] > nums[right]`.
2. **Handle duplicates gracieusement** – «right--» est la technique la plus simple, correcte et facile à interviewer.
3. **Exposer les compromis de complexité** – montrer que le pire est linéaire, mais la moyenne est logarithmique.
4. **Fournir un code propre, commenté** – comme nous l'avons fait en Java, Python et C++.
5. **Parler des cas de bord** – comme des tableaux ou des tableaux déjà triés avec tous les éléments égaux.

Si vous pouvez articuler ces points lors d'une entrevue, vous impressionnerez n'importe quel gestionnaire d'embauche avec votre pensée algorithmique et vos compétences en communication.

---

2.9 Extraits de code final (toutes les trois langues)

"Java
// Java
public int findMin(int[] nums) {
int gauche = 0, droite = longueur nums - 1;
pendant que (à gauche < à droite) {
int milieu = gauche + (droite - gauche) / 2;
si (nums[mid] > nums[right]) gauche = milieu + 1;
sinon si (nums[mid] < nums[right]) droite = milieu;
Sinon, c'est bien...
}
les numéros de retour [à gauche];
}
«» "

'`python
# Python
def findMin(self, nombres: List[int]) -> Int:
gauche, droite = 0, len(nums) - 1
à gauche < à droite:
milieu = (gauche + droite) // 2
en cas de nums[mid] > nums[right]:
gauche = milieu + 1
Nums d'élif[mid] < nums[right]:
droite = milieu
Sinon:
droite -= 1
retour nums[gauche]
«» "

'`cpp
// C++
Int findMin(vecteur<int>& nums) {
int gauche = 0, droite = nums.size() - 1;
pendant que (à gauche < à droite) {
int milieu = gauche + (droite - gauche) / 2;
si (nums[mid] > nums[right]) gauche = milieu + 1;
sinon si (nums[mid] < nums[right]) droite = milieu;
- Oui.
}
les numéros de retour [à gauche];
}
«» "

---

## 2.10 Pensées de clôture

LeetCode 154 est plus qu'un puzzle ; c'est un **test de communication**.
Maîtrisez la logique de recherche binaire, gardez votre code lisible et soyez prêt à discuter de la façon dont les duplicatas affectent l'exécution.

C'est le mélange parfait du **bon, le mauvais, et le laid** que tout senior du génie logiciel attend.

---

* Bon codage, et bonne chance avec vos entrevues! *