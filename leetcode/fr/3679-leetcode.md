---
titre: LeetCode 3679. Réductions minimales pour équilibrer l'inventaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3679 – Réduction minimale de l'inventaire
**Moyenne de 10 à 15 min solution de O(n) temps, espace O(n + U)**

---

- Oui. 1. Récapitulation des problèmes

Vous recevez:

* `arrivées` – une série d'entiers (`1 ≤ arrivées[i] ≤ 105`) où chaque entrée est le type **** de l'article qui arrive le jour `i` (1-indexé).
* `w` – la taille de la fenêtre coulissante (derniers jours `w`).
* `m` – le nombre maximal autorisé d'articles du même type dans n'importe quelle fenêtre.

Pour chaque jour `i` nous regardons la fenêtre
«[max(1, i – w + 1), i]».
Si nous gardons l'arrivée le jour `i` et cela ferait que le nombre de son type dans cette fenêtre à dépasser `m`, nous *doit* le jeter.
Nous voulons le nombre **minimum** de rejets nécessaires pour que *chaque fenêtre réponde à la règle.

---

- Oui. 2. Principales perspectives

La seule chose qui compte est la fenêtre *current*.
Lorsque nous passons du jour `i` à `i+1`:

1. Le jour `i+1-w` quitte la fenêtre (s'il existe).
2. Nous décidons de garder ou de rejeter l'arrivée le jour `i+1`.

Si nous ne conservons un article que lorsqu'il le fait **pas** enfreigne la règle, nous ne gaspillons jamais un rejet – cette stratégie gourmande est optimale.
Il nous faut une fenêtre coulissante avec un compteur de fréquence.

---

- Oui. 3. Algorithme

Texte
gardé[i] – tableau booléen, vrai si nous gardons l'élément le jour i
cnt[type] – carte de hachage (ou tableau) qui contient combien d'éléments conservés de ce type sont actuellement dans la fenêtre
déchets – comptoir d'articles jetés

pour i de 0 à n-1: // 0 = jour i+1
// 1. Supprimer le jour qui quitte la fenêtre
idx = i - w
si idx >= 0 et conservé[idx] vrai:
cnt[arrivées[idx]] -= 1

// 2. Essayez de garder l'arrivée actuelle
t = arrivées[i]
si cnt[t] < m:
keep[i] = true
cnt[t] += 1
Sinon:
1 // doit être éliminé
retour des déchets
«» "

* **Heure** – O(n) (chaque jour ne fait qu'une quantité constante de travail).
* **Espace** – O(n + U) où `U` est le nombre de types d'articles distincts
(Le terme `kept` est `n`, `cnt` est `U`).

---

- Oui. 4. Code

Ci-dessous, vous trouverez trois implémentations complètes – une en **Java**, **Python** et **C++**.

---

##### 4.1 Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe publique {
public int minArrivéesToDiscard(int[] arrivées, int w, int m) {
n = arrivées. longueur;
booléen[] conservé = nouveau booléen[n];
Carte <entier, entier> cnt = nouveau HashMap<>();
les déchets int = 0;

pour (int i = 0; i < n; i++) {
int idx = i - w;
Si (idx >= 0 && conservé[idx]) {
int old = arrivées[idx];
cnt.put(vieux, cnt.get(vieux) - 1);
}

type int = arrivées[i];
Int cur = cnt.get OrDefault(type, 0);
si (cur < m) {
keep[i] = true;
cnt.put(type, cur + 1);
} autre {
jeter++;
}
}
retour des déchets;
}
}
«» "

---

4.2 Python

'`python
Solution de classe:
def minArrivéesToDiscard(self, arrivées: list[int], w: int, m: int) -> Int:
n = len(arrivées)
conservé = [Faux] * n
freq = {}
Déchets = 0

pour i dans la plage(n):
idx = i - w
si idx >= 0 et conservé[idx]:
old = arrivées[idx]
freq[old] -= 1

t = arrivées[i]
cur = freq.get(t, 0)
si cur < m:
conservation[i] = Vrai
freq[t] = cur + 1
Sinon:
Rejet += 1
retour des déchets
«» "

---

*### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minArrivéesToDiscard(vecteur<int>& arrivées, int w, int m) {
int n = arrivées.size();
vecteur <char> conservé(n, 0); // 0 = jeté, 1 = conservé
non ordonné_map<int, int> cnt; // type -> compter dans la fenêtre
les déchets int = 0;

pour (int i = 0; i < n; ++i) {
int idx = i - w;
Si (idx >= 0 && conservé[idx]) {
int old = arrivées[idx];
si (--cnt[vieux]] 0) cnt.erase(ancienne);
}

t = arrivées[i];
si (cnt[t] < m) {
conservé[i] = 1;
++cnt[t];
} autre {
++découper;
}
}
retour des déchets;
}
};
«» "

Les trois solutions fonctionnent dans le temps **O(n)** et utilisent la mémoire **O(n + U)**, correspondant parfaitement aux contraintes (`n ≤ 105`).

---

- Oui. 5. Explication du style Blog

> **Titre**: *Inventaire de l'inventaire en O(n): Le problème de 3679 rejets minimum expliqué*

---

5.1 Introduction

Si vous êtes un ingénieur logiciel à la poursuite d'un rôle de data-structures & algorithmes, vous avez probablement vu des problèmes de LeetCode.
Le "Minimum Disards to Balance Inventory" (LeetCode 3679) est un exemple classique qui combine des décisions gourmandes avec un guichet coulissant.

Dans cet article, nous allons:

* Comprendre le problème du point de vue des entreprises.
* Marchez à travers l'algorithme gourmand pas à pas.
* Mettre en évidence les pièges (les parties de "bad" et "ugly").
* Présentez un code propre et prêt à la production en Java, Python et C++.
* Saupoudrer quelques mots-clés SEO pour aider les recruteurs à vous trouver.

---

5.2 Analogie du monde réel

Imaginez un entrepôt qui reçoit des envois tous les jours.
Le gestionnaire peut conserver ou jeter chaque expédition le même jour.
Toutefois, pour toute période récente de 7 jours, aucun type de produit ne peut dépasser un maximum de 5 articles conservés.

Si la fenêtre de 7 jours a déjà 5 unités de produit, et qu'une nouvelle expédition de , est arrivée, vous ** devez** la jeter – sinon la règle est violée.

Vous voulez jeter les envois *fewest* possibles, car chaque envoi jeté est une vente perdue.

---

5.3 La perspective de l'avidité

Pourquoi est-ce suffisant de ne discarder que quand il est forcé ?

* Supposons que nous * conservions * un élément qui ferait que le nombre de fenêtres dépasse `m`.
Cela viole la règle, donc un tel État est illégal.
* Si nous *délivrons* un article qui aurait pu être conservé, nous augmenterons inutilement le nombre de rejets.
On aurait pu le garder et rester légal.

Ainsi, la seule action en justice à chaque jour est :

«» "
si (compte courant < m)
autres déchets
«» "

Cette règle simple garantit que nous ne gaspillons jamais de déchets, donc elle produit les rejets *minimum*.

---

##### 5.4 Pourquoi une fenêtre coulissante est nécessaire (La partie "Bien")

La taille de la fenêtre `w` peut être aussi grande que `105`.
Recalculer naïvement le nombre de chaque type dans chaque fenêtre coûterait "O(n·w)", ce qui est impossible.

Une fenêtre de glissement nous permet :

1. **Ajouter** le nouvel article de jour dans O(1).
2. **Supprimer** l'article qui laisse la fenêtre dans O(1).

Nous ne conservons qu'un compteur pour les éléments *actuellement conservés*, pas pour le tableau entier.
Cela réduit la complexité temporelle du quadratique au linéaire.

---

5.5 Pièges communs (Les parties "Bad" et "Ugly")

Problème
C'est ce qu'on dit.
Autres **L'utilisation d'une file d'attente pour la fenêtre**=Une file d'attente ajoute/supprime O(1) mais stocke *tous* jours, rendant la solution mémoire-lourd. Utilisez un tableau booléen (`kept`) au lieu de stocker chaque jour dans une file d'attente. Autres
**Mutables compteurs dans un dictionnaire**. Rechercher `0` et `erase` la clé. Autres
L'utilisation d'une logique basée sur 1 sur des tableaux basés sur 0 conduit à des bogues subtils. Convertissez explicitement le jour `i` en index basé sur 0 et calculez `idx = i - w`. Autres
**Création de tableaux inutiles**= Attribution d'un tableau de taille `n` juste pour savoir si nous avons gardé un article est gaspillé quand `n` est énorme.=Utilisez un `boolean[]` (ou `char`) – il est minimal et rapide. Autres

---

##### 5.4 Passage du code (Java)

"Java
pour (int i = 0; i < n; i++) {
int idx = i - w; // jour qui quitte la fenêtre
si (idx >= 0 && keep[idx]) { // il a été conservé, alors nous enlevons son compte
int old = arrivées[idx];
cnt.put(vieux, cnt.get(vieux) - 1);
}

type int = arrivées[i]; // jour actuel
Int cur = cnt.get OrDefault(type, 0);
si (cur < m) { // sans danger à conserver
keep[i] = true;
cnt.put(type, cur + 1);
} autre { // forcé de jeter
jeter++;
}
}
«» "

* **Pourquoi est-ce O(n)? * *
Chaque itération effectue un nombre constant d'opérations de hash-map.
* **Pourquoi ça marche ? * *
Parce que la seule violation possible est traitée immédiatement.

---

5.5 Résumé de la complexité

Valeur métrique
C'est pas vrai.
**Temps** **O(n)** (linéaire)
**Espace******O(n + U)** (paire + plan de hachage)
**Pourquoi c'est important** Autres

---

##### 5.6 SEO & Crochets de recrutement

* **Mots-clés**: Algorithme de fenêtre coulissante, Minimum de rejets, Algorithme de grès, Java Sliding window, Structures de données de python, Carte de hachage C++, Code de leet 3679, Problème de gestion de l'inventaire, Stratégie de rejet optimale.
* **Tagline**: Vous souhaitez ace LeetCode? Découvrez la solution 3679 Minimum Disards – Java, Python, C++ – O(n) time, des rejets optimaux !
* **Méta-description** (pour les moteurs de recherche):
*Découvrez comment résoudre LeetCode 3679 – Éliminer au minimum l'inventaire – avec une approche cupide à guichet coulissant. Obtenez le code Java, Python et C++ propre, plus une explication en profondeur qui est parfait pour les recruteurs.

---

##### 5.7 Liste de contrôle à emporter

( ) **Greedy est optimal** – garder seulement quand vous êtes *non* forcé de jeter.
( ) **Coulez la fenêtre** – supprimez le jour qui sort ('i - w').
**Carte de fréquence** – nombre de pistes des types conservés à l'intérieur de la fenêtre.
**Éviter les bugs hors-par-un** – convertir les numéros de jour correctement.
( ) **Utilisez une mémoire minimale** – un tableau booléen pour -kept-- + une carte de hash pour les fréquences.

---

5.8 Clôture

Qu'il s'agisse d'un entretien de codage, de la construction d'un micro-service de gestion d'entrepôt ou simplement d'affiner vos compétences en matière de structure de données, le problème 3679 est une excellente vitrine de la fenêtre coulissante **Gredy +.

Déposez un point sur le problème LeetCode, partagez cet article et n'hésitez pas à modifier le code de votre propre pile.

** Bon codage ! **

---

- Oui. 6. Référence rapide

Lien
- Oui.
Solution de Java Autres
** Solution de python** Autres
Solution **C++ Autres
**Article complet *Copier-coller dans votre blog ou article moyen*

---