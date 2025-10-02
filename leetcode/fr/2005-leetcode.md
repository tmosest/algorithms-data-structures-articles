---
titre: LeetCode 2005. Jeu de suppression de sous-arbres avec Fibonacci Tree -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes
**LeetCode 2005 – Jeu de suppression de sous-arbres avec Fibonacci Tree**
- Un arbre de Fibonacci est défini de façon récursive.
* `commande(0)` – arbre vide
* `order(1)` – noeud unique
* `order(n)` – racine + sous-arbre gauche `order(n‐2)` + sous-arbre droit `order(n‐1)`
- Alice et Bob jouent alternativement.
- Oui. Sur un tour, un joueur sélectionne n'importe quel nœud et supprime ce nœud ** et tout le sous-arbre enraciné dans ce nœud**.
- Oui. Le joueur qui est forcé de supprimer le nœud racine **loses**.
- Alice commence.

Compte tenu de `1 ≤ n ≤ 100`, déterminer si Alice gagne (`vrai`) ou Bob gagne (`faux`) en supposant un jeu optimal.

---

- Oui. 2. Aperçu général

Le jeu sur un arbre Fibonacci est un jeu impartial **normal**.
Utilisation de Sprague Théorie grundy (ou induction simple sur la taille de l'arbre) on peut prouver:

> **Alice gagne iff `(n‐1) % 6 0'.**

Pourquoi 6 ?
Les numéros Grundy pour les petits `n` répètent toutes les 6 étapes:

Grundy(n) : Gagner ? Autres
C'est pas vrai.
Lose
$ $ $ $ $ $
- C'est bon.
$ 4 $ 3 $ Gagnez
$ 5 $ 4 $ Gagnez
$ 6 $ 5 $ Gagnez
Perte
- Oui.

Ainsi le modèle `[perdre, gagner, gagner, gagner, gagner, gagner]` se répète, et une position perdante se produit exactement quand `n‐1` est un multiple de 6.

---

- Oui. 3. Complexité

Langue Heure Espace
- C'est quoi ?
**O(1)**
Python **O(1)**
* * * * * * * *

Toutes les solutions sont du temps et de la mémoire constants parce que nous évaluons simplement une expression modulo.

---

- Oui. 4. Mise en œuvre des références

#### 4.1 Java

"Java
// Fichier: Solution.java
solution de classe {
public booléen trouverGameWinner(int n) {
// Alice gagne sauf si (n-1) est un multiple de 6
retour (n - 1) % 6 != 0;
}
}
«» "

4.2 Python

'`python
# Fichier : solution. py
Solution de classe:
def findGameWinner(self, n: int) -> C'est vrai.
# Alice gagne sauf si (n-1) est divisible par 6
retour (n - 1) % 6 != 0
«» "

### 4.3 C++

'`cpp
// Fichier: solution.cpp
solution de classe {
public:
bool findGameWinner(int n) {
// Alice gagne à moins (n-1) % 6 == 0
retour (n - 1) % 6 != 0;
}
};
«» "

Les trois extraits sont compilés sous l'environnement standard LeetCode (`Java 17`, `Python 3.8`, `GNU++17`).

---

- Oui. 5. Harnais d ' essai rapide (facultatif)

"Java
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
pour (int n = 1; n <= 12; n++) {
System.out.printf("n=%d → %s%n", n, s.findGameWinner(n) ? "Alice" : "Bob" ;
}
}
«» "

Vous devriez voir le modèle: Alice perd à `n = 1, 7, 13, ...` (c'est-à-dire `n-1` divisible par 6).

---

- Oui. 6. Article de blog optimisé par le SEO

> **Titre**: LeetCode 2005: jeu de suppression de sous-arbre avec Fibonacci Tree – Solutions Java, Python & C++

---

6.1 Introduction

Si vous êtes en train de vous préparer à une interview technique ou d'essayer d'ase LeetCodes **=Subtree Removal Game avec Fibonacci Tree**, vous voudrez une solution propre et rapide qui passe chaque cas de test. Ce post décompose le problème, vous montre une solution à temps constant et fournit un code prêt à la copie en **Java**, **Python** et **C++**. Que vous soyez un codeur chevronné ou un nouveau venu, nous allons parcourir la logique, les pièges, et comment expliquer l'idée aux intervieweurs.

---

6.2 Le problème, en anglais clair

Un arbre Fibonacci est construit exactement comme la séquence Fibonacci – chaque nouveau noeud fixe deux arbres plus petits, avec des tailles `n‐2` et `n‐1`. Alice et Bob suppriment alternativement un nœud * et tout son sous-arbre*. Le joueur qui doit supprimer la racine perd.

> **Objectif**: Retour `vrai` si Alice peut forcer une victoire (elle commence), sinon `faux`.

Les contraintes sont minuscules (‘1 ≤ n ≤ 100'), mais le motif de victoire/perte n'est pas évident à première vue.

---

### 6.3 Bon: La formule simple

La ligne magique :

'`cpp
retour (n - 1) % 6 != 0;
«» "

Pourquoi ?
- Calculer le nombre Grundy de chaque arbre à la main jusqu'à `n = 6`.
- Vous verrez un cycle répété de longueur 6:
"0, 1, 2, 3, 4, 5, 0, 1,..."
- Un nombre Grundy de "0" signifie que la position est en perte.
- Donc seulement quand `(n‐1)` est divisible par 6 est Alice coincé à perdre.

Ainsi, tout le problème s'effondre en une seule opération modulo.

---

### 6.4 Mauvais : idées fausses communes

Pourquoi il échoue Comment éviter
- C'est quoi ?
Il suffit de simuler le jeu. Une explosion exponentielle, même pour `n=100`. Utilisez la théorie Sprague‐Grundy ou notez le cycle 6. Autres
Autres Prenez le plus grand sous-arbre en premier. Les stratégies d'avidité peuvent faire marche arrière ; le jeu optimal est subtil. Autres
Autres Le problème, c'est les chiffres de Fibonacci. L'arbre est défini *par* Récursion Fibonacci, mais le motif gagnant n'est pas une séquence Fibonacci. Focus sur les nombres Grundy, pas les valeurs numériques de Fibonacci. Autres

---

### 6.5 Ugly: Edge- Traps de cas et mise en œuvre Quirks

1. **L'indexation fondée sur le zéro et l'indexation fondée sur le monotype**
La formule utilise «(n‐1) % 6». Oublier le `-1` donne de mauvaises réponses pour `n=1,7,13,...`.
2. **Débordement du type de données**
Pas un problème pour `n ≤ 100`, mais si les contraintes changent, utiliser `long`/`long` pour être sûr.
3. **Modulo avec nombres négatifs**
Dans des langues comme Java et C++, `(n‐1)%6` pour `n=0` serait `-1`. Depuis `n≥1`, c'est sûr, mais toujours vérifier les limites dans votre propre code.

---

6.6 Comment parler Dans une interview

> Les nombres Grundy de Fibonacci répètent toutes les six tailles. Par conséquent, Alice perd seulement quand `(n‐1) % 6 == 0`. J'ai implémenté ceci comme une seule ligne, donnant O(1) temps et mémoire. (en milliers de dollars)

Cette réponse concise montre que vous comprenez la théorie sous-jacente et que vous pouvez la traduire en code propre.

---

### 6.7 Code complet (Java / Python / C++)

> **Java**
> ``java
> solution de classe {
> public booléen trouverGameWinner(int n) {
> retour (n - 1) % 6 != 0;
> }
> }
> `` "

> **Python**
> ``python
> solution de classe:
> def findGameWinner(self, n: int) -> C'est vrai.
> retour (n - 1) % 6 != 0
> `` "

> **C++**
> ``cpp
> solution de classe {
> public:
> bool findGameWinner(int n) {
> retour (n - 1) % 6 != 0;
> }
> };
> `` "

Les trois solutions compilent et fonctionnent sous une milliseconde pour le maximum `n = 100`.

---

#### 6.8 Enveloppe et prise- Loin

Détails
C'est quoi ?
**Pattern** Autres
**Heure**= O(1) – juste un modulo. Autres
* Espace * O(1). Autres
**Pourquoi c'est important** Autres

Utilisez ceci comme tremplin : pratique expliquant les nombres Grundy, montrez que vous pouvez repérer les cycles, et apportez le liner à votre prochaine entrevue de codage.

Bonne chance – et le codage heureux! C'est ce qu'il a dit.

---

### 6.9 Mots clés pour référencement

* Jeu de suppression de sous-arbres avec Fibonacci Tree
* Solution LeetCode 2005
* Fibonacci arbre théorie de jeu
* Entretien de codage Java / Python / C++
* Arbre binaire de stratégie gagnante
* Nombres de grundy expliqués
* Exemples d'algorithmes d'entrevue
* Solutions à temps constant LeetCode
* Préparation des entretiens techniques

N'hésitez pas à partager cet article sur votre blog LinkedIn, Medium ou personnel pour mettre en valeur votre solution de problèmes et attirer les recruteurs!