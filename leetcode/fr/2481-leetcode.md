---
titre: LeetCode 2481. Coupes minimales pour diviser un cercle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## LeetCode 2481 – Coupes minimales pour diviser un cercle
L'espace O(1)**

---

### TL;DR
"Java
numéro d'entrée publicOfCuts(int n) {
si (n == 1) retourner 0; // déjà une tranche
retour n % 2 == 0 ? n/2 : n; // même → la moitié des coupes, impair → une par tranche
}
«» "

'`python
Solution de classe:
def numberOfCuts(self, n: int) -> Int:
retourner 0 si n == 1 autre n si n % 2 autre n // 2
«» "

'`cpp
solution de classe {
public:
nombre intOfCuts(int n) {
si (n) 1) retourner 0;
retour n % 2 ? n : n/2;
}
};
«» "

---

## Pourquoi cela compte pour votre entrevue de codage

- **Un code court et propre** qui fonctionne en temps constant – les intervieweurs aiment les solutions concises.
- Démontre *perspective mathématique* et *conscience des cas de pointe* – traits clés pour un ingénieur de moteur ou d'algorithme.
- S'adapte parfaitement à une entrevue de 60 minutes** ou comme solution *take-home* sur LeetCode.

---

## Déclaration de problème (à partir de LeetCode)

> Une coupe **valide** dans un cercle peut être:
> 1. Une ligne droite qui touche deux points sur le bord du cercle et passe par son centre (un diamètre).
> 2. Une ligne droite qui touche un point sur le bord du cercle et son centre.
>
> Compte tenu d'un entier `n` (1 ≤ n ≤ 100), retourner le nombre minimum de coupes nécessaires pour diviser le cercle en **n tranches égales**.
> La première coupe ne produira pas une nouvelle tranche (le cercle reste entier après la première coupe).

Exemples
Explication
C'est pas vrai.
Les coupes de deux diamètres donnent 4 tranches égales. Autres
Trois coupes en un seul point sont nécessaires; aucune paire de coupes de diamètre ne fonctionne. Autres

---

## Intuition et observation clé

1. **Deuxième
- Chaque coupe qui passe par le centre ne peut que couper le cercle en *deux* moitiés égales.
- Pour obtenir un nombre impair de tranches, vous ne pouvez pas compter sur un diamètre.
- Chaque coupe doit *créer une nouvelle tranche*, de sorte que vous devez exactement `n` coupes.
- Exemple: `n = 3` → 3 coupes, une par tranche.

2. ** Même `n`**
- Vous pouvez utiliser un diamètre pour diviser le cercle en deux moitiés égales.
- Après la première coupe de diamètre, chaque moitié peut être divisée plus loin en utilisant la même stratégie.
- Effectivement, vous avez besoin de la moitié autant de coupes que le nombre de tranches: `n / 2`.
- Exemple: `n = 6` → 3 coupes (`6/2`), pas 6.

3. **`n = 1`**
- Pas de coupes nécessaires – le cercle est déjà une tranche.

La solution est donc une seule ligne de logique conditionnelle.

---

Surmonter Débat de cas

Justification
C'est pas vrai.
Déjà une seule tranche. Autres
Une coupe de diamètre. Autres
Drôle, ne peut pas utiliser des paires de diamètre. Autres
" 4 / 2 " . Autres
100, 50, même, 100, 2. Autres

Tous les cas d'essai passent avec la formule O(1).

---

Algorithme (Pseudocode)

«» "
numéro de la fonctionOfCuts(n):
si n] 1 :
retour 0
sinon si n est égal:
retour n / 2
Sinon:
retour n
«» "

---

## Mise en œuvre du code

### Java
"Java
solution de classe publique {
numéro d'entrée publicOfCuts(int n) {
si (n) 1) retourner 0;
retour n % 2 == 0 ? n / 2 : n;
}
}
«» "

Python
'`python
Solution de classe:
def numberOfCuts(self, n: int) -> Int:
retourner 0 si n == 1 autre n si n % 2 autre n // 2
«» "

C++
'`cpp
solution de classe {
public:
nombre intOfCuts(int n) {
si (n) 1) retourner 0;
retour n % 2 ? n : n / 2;
}
};
«» "

Les trois extraits compilent et fonctionnent dans **O(1)** temps et utilisent **O(1)** mémoire.

---

Analyse de complexité

- **Time**: `O(1)` – quelques opérations arithmétiques, pas de boucles.
- **Espace**: "O(1)" – mémoire auxiliaire constante.

---

- Oui. Exemples de cas d ' essai

Texte
Entrée: n = 1
Produit : 0

Entrée: n = 2
Produit : 1

Entrée: n = 3
Produit : 3

Entrée: n = 4
Produit: 2

Entrée: n = 6
Produit : 3

Entrée: n = 7
Produit : 7

Entrée: n = 100
Produit : 50
«» "

Exécutez-les dans votre IDE ou la plate-forme LeetCode ; tous devraient passer instantanément.

---

Pièges communs

Pourquoi il échoue
- C'est quoi ?
"retour n / 2" pour tous les "n" , les numéros d'ordre ont besoin de plus de coupes , Ajouter un contrôle de parité
`return n` pour tous ```` Même les nombres sont surcoupés.
1 ''' Retourne 1 au lieu de 0' Cas spécial le cas de base

---

- Oui. Pourquoi cette solution est-elle prête à l'entrevue

1. **Clarté** – une branche conditionnelle, pas de boucles.
2. **Élégance mathématique** – montre la compréhension de la symétrie et de la parité.
3. **Edge‐Case Handling** – démontre la connaissance des valeurs limites.
4. **Performance** – le temps et la mémoire constants ne garantissent ni délai ni MLE.

Présenter cette solution dans une entrevue met en valeur la pensée algorithmique* et le code brivity*, tous deux très appréciés par les gestionnaires embaucheurs.

---

## SEO-Optimized Blog Titre & Meta Description

**Titre:**
LeetCode 2481 – Découpes minimales pour diviser un cercle

**Meta Description:**
Découvrez la solution O(1) la plus rapide pour le LeetCode 2481. Code Java, Python et C++ détaillé, gestion des cas de bord et explication prête à l'entrevue. Augmentez votre succès d'entrevue de codage.

---

Mots clés
- LeetCode 2481
- Coupes minimales pour diviser un cercle
- Algorithme de coupe du cercle
- Solution Java LeetCode
- Solution Python LeetCode
- C++ Solution LeetCode
- Questions sur le codage des entrevues
- Pensée algorithmique

---

Les pensées finales

Le problème « Minimum Cuts to Divide a Circle » est trompeurment simple une fois que vous réalisez le tour de parité.
- **Même `n`** → utiliser les diamètres → `n/2` coupes.
Chaque tranche doit être coupée séparément.
- **`n = 1`** → aucune coupure.

N'oubliez pas de garder votre code serré, documenter la logique de parité, et vous impressionnerez les intervieweurs à la fois avec justesse et élégance. Bon codage !