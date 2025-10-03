---
titre: LeetCode 2580. Compter les voies de chevauchement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2580 – Compter les voies de chevauchement de groupes
** Difficulté :** Moyenne **Tags:** *Sortie, Intervalles, Greedy, Math*

---

- Oui. 1. Récapitulation des problèmes

On vous donne un tableau des intervalles entiers `ranges[i] = [starti, endi]`.
Vous devez diviser tous les intervalles en **deux** groupes (un ou l'autre groupe peut être vide) de sorte que :

* Chaque intervalle est exactement dans un groupe.
* Deux intervalles ** de chevauchement** doivent appartenir au même groupe.

Deux intervalles se chevauchent s'ils partagent au moins un entier commun.

Retourner le nombre total de fractions valides modulo `1 000 000 007`.

---

- Oui. 2. Intuition

Si nous imaginons tous les intervalles sur une ligne de nombre, les intervalles qui se chevauchent forment des composants connectés (comme une chaîne de blocs de toucher).
*À l'intérieur d'une composante* tous les intervalles **doit** aller au même groupe.
*Different components* sont indépendants: nous pouvons mettre l'ensemble du composant dans le groupe 1 ou le groupe 2.

Par conséquent, la réponse est simplement

«» "
réponse = 2 ^ (nombre de composants) (mod. 1e9+7)
«» "

Il suffit donc de compter combien de composants connectés existent.

---

- Oui. 3. Algorithme

1. **Trier tous les intervalles par leur valeur de départ («stiti»).
2. itérer la liste triée tout en maintenant le **current maximum fin** `currEnd` de la composante nous sommes bâtiment.
3. Pour chaque intervalle «[s, e]»:
* Si `s` > `currEnd` → l'intervalle commence un **nouveau composant**.
* Multiplier la réponse par `2` (mod).
* Définir `currEnd = e`.
* Autrement → l'intervalle chevauche le composant actuel.
* Mettre à jour `currEnd = max(currEnd, e)`.
4. Retourne la réponse finale.

---

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie `2^(#components)`.

**Lemme 1**
Après tri au début, deux intervalles appartiennent au même composant iff pendant le scan, nous ne rencontrons jamais un point où `s > curr Finissez entre eux.

*Proof. *
Si un intervalle commence après la fin du composant courant (`s > currEnd`), il y a un écart et les deux ne peuvent pas se chevaucher; ils sont donc dans des composants différents.
Inversement, si le scan ne voit jamais un tel écart, chaque début d'intervalle est ≤ fin du courant, ce qui signifie que chaque intervalle successif chevauche le composant courant. Ils sont donc tous connectés. *

**Lemme 2**
L'algorithme crée un nouveau composant exactement quand un trou apparaît (`s > currEnd`).

*Proof. *
L'algorithme détecte un trou exactement dans cette condition, multiplie la réponse par `2` et réinitialise `currEnd`. Aucune autre action ne multiplie la réponse. *

* Théorème *
Laissez `C` être le nombre de composants. L'algorithme renvoie `2^C mod M`.

*Proof. *
Par Lemma 1, le scan divise les intervalles en composants exactement `C`.
Par Lemma 2, la réponse est multipliée par « 2 » une fois par composant (le premier composant est compté en initialisant la réponse = 1 et en multipliant sur le deuxième composant vers l'avant).
Ainsi, après traitement de tous les intervalles, "réponse = 2^C (mod M)".

---

- Oui. 5. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Trier "O(n log n)" "O(1)" (en place)
Détection Autres
**Total** Autres

`n ≤ 105`, de sorte que la solution s'inscrit facilement dans les limites.

---

- Oui. 6. Mise en œuvre des références

> **Toutes les implémentations partagent la même logique** – la seule différence est la syntaxe spécifique au langage.
> La constante «MOD = 1 000 000 007».

---

##### 5.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

Int public countWays(int[][] gammes) {
i (longueur de gamme) 0) retourner 0; // pas nécessaire par contrainte

Trier par début
les tableaux.sort(plages, a, b) -> Integer.compare(a[0], b[0]);

long an = 1; // 2^0
long curr Fin = Long.MIN_VALUE; // fin max du composant actuel

pour (int[] intervalle : intervalles) {
long s = intervalle[0];
long e = intervalle[1];

si (s > currEnd) { // nouveau composant
as = (ans * 2) % MOD; // choisir le groupe pour ce composant
currEnd = e;
} autre { // étendre le composant actuel
si (e > currEnd) currEnd = e;
}
}

retour (int) ans;
}
}
«» "

---

5.2 Python 3

'`python
MOD = 1 000 000 007

Solution de classe:
def countWays(self, ranges: list[list[int]]) -> Int:
ranges.sort(key=lambda x: x[0]) # 1

ans = 1
_fin_curr = -1 << 60 # très petite

pour s, e dans les fourchettes:
si s > curr_end: # 2
% MOD
_fin_curr = e
Sinon : # 3-
_fin_curr = max(curr_end, e)

retour et
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue MOD = 1'000'000'007LL;

Int countWays(vecteur<vecteur<int>>&intervalles) {
si (ranges.vide()) retourne 0; // par contrainte, non nécessaire

tri(ranges.begin(), ranges.end(),
[](vectorielle Const<int>& a, vectorielle Const<int>& b){
retourner a[0] < b[0];
});

long an = 1;
long curr long Fin = LLONG_MIN;

pour (auto &iv : gammes) {
long s = iv[0], e = iv[1];
si (s > currEnd) { // nouveau composant
ans = (ans * 2) % MOD;
currEnd = e;
} autre { // même composant
si (e > currEnd) currEnd = e;
}
}
retourner static_cast<int>(ans);
}
};
«» "

---

- Oui. 6. Validation par essai

Autres Test de précision
- C'est quoi ?
Un composant → 2 voies
"[[1, 4], [2, 3], [5, 6] "" "4"" Deux composants → 22"
Trois intervalles isolés → 23
[[[1, 10], [2, 3], [4, 5], [6, 7], [8, 9]] "" "2" "Tous les chevauchements → un seul élément"
[[1, 1], [2, 2], [3, 3], [4, 4]]""" "16"" Aucun chevauchement → 4 composants"
[1, 5], [2, 6], [5, 7], [8, 10]]"""4"" Deux éléments : "[1-7]" et "[8-10]"

Tous les cas de bord fonctionnent: composant unique → `2`; tous les disjoints → `2^n`; chaîne recoupante → `2`.

---

- Oui. 7. Pièges communs

Erreur
- Oui.
Autres Oublier que les deux groupes peuvent être vides. Autres
Autres Compter plusieurs fois un composant en raison d'une entrée non triée. Autres
Utiliser l'int 32-bit pour `ans` lorsque `n` peut être 105. Utiliser `long`/`long long` et appliquer le module après chaque multiplication. Autres
Erreur dans l'interprétation d'Overlap comme Intersection d'intervalles réels Le problème garantit des paramètres entiers, donc un écart de longueur 0 sépare encore les composants. Autres

---

- Oui. 8. Pourquoi cette solution est bonne

* **Simplicité** – juste tri + une passe.
* **Évoluabilité** – `O(n log n)` gère facilement 105 intervalles.
* **Mathématiquement élégant** – la réponse est une puissance de deux.

---

- Oui. 9. Lorsqu'il peut devenir odieux

* **Très grande entrée** – Les Python's intégrés «sort» peuvent atteindre des limites de récursion lors de l'utilisation des puissances. Utilisez `pow(2, composants, MOD)` (Python) ou une exponentiation rapide itérative (C++/Java).
* **Cas de test multiples** – LeetCode fournit un cas de test unique par course, mais si vous vous adaptez à un processeur par lots, n'oubliez pas de réinitialiser `ans = 1` pour chaque cas.
* ** Environnement sensible à la mémoire** – Le tri en place est parfait, mais si vous êtes contraint à `O(n)` mémoire supplémentaire, vous pouvez fusionner les intervalles à la volée en utilisant une file d'attente prioritaire, bien que le temps reste `O(n log n)`.

---

10 ans. Prise- Loin

* Trier → un pass → compter les composants → multiplier par 2 pour chaque.
* La réponse est une simple puissance de deux, pas de structures de données lourdes nécessaires.
* Le modulo arithmétique est trivial: `ans = ans * 2 % MOD`.

---

Poste de blog : Mastering LeetCode 2580 – Count Ways to Group Overlapping Ranges

> **Meta Description:**
> Solve LeetCode #2580 – Count Ways to Group Overlapping Ranges. Apprenez l'astuce d'intervalle, obtenez Java, Python, code C++ et des explications prêtes à l'entrevue.

---

- Oui. 1. Titre et en-tête

html
<h1>Code de let 2580 – Compter les voies de chevauchement de groupes</h1>
<h2>Aperçu du problème
«» "

---

- Oui. 2. Aperçu du problème

> **Que vous demande LeetCode 2580 ? **
> Vous êtes donné un tableau de gammes entières `[début, fin]`.
> Séparez-les en deux groupes de sorte que les plages de chevauchement soient maintenues ensemble.
> Compter le nombre de scissions possibles modulo 1 000 000 007.

> *Mots clés:* LeetCode, 2580, Count Ways to Group Overlapping Ranges, interview, algorithme, tri, intervalles.

---

- Oui. 3. Exemple

Texte
Entrée: [[1,3],[2,4],[5,7]]
Produit: 2
Explication :
- Intervalles [1,3] et [2,4] se chevauchent → ils doivent rester ensemble.
- [5,7] est isolé → nous pouvons le mettre dans chaque groupe.
Deux scissions valides : { [1,3],[2,4] } / { [5,7] } ou { [5,7] } / { [1,3],[2,4] }.
«» "

---

- Oui. 4. Contraintes

* "1 ≤ gammes.longueur ≤ 105 "
* `1 ≤ starti ≤ endi ≤ 109 "

Ces contraintes donnent à penser qu'un algorithme `O(n log n)'est acceptable, mais que les solutions linéaires ou quadratiques seront temporelles.

---

- Oui. 5. Intuition & Greedy Insight

Pensez à la ligne de nombre.
- Les intervalles de chevauchement forment un cluster connecté (composante de l'équation).
- Tous les intervalles à l'intérieur d'une composante doivent être dans le groupe **same**.
- Les composants sont indépendants → pour chaque composant que vous avez deux choix (groupe 1 ou groupe 2).

La réponse est donc "2^(#components)".

---

- Oui. 6. Détails de l'algorithme

Étape Action Pourquoi
C'est quoi ?
**Sort** par le début. Autres
Autres Le plus loin nous avons vu jusqu'à présent dans la composante actuelle. Autres
Pour chaque "[s, e]"
- Si `s > currEnd`: nouveau composant → multiplier la réponse par `2`, réinitialiser `curr Fin = e'.
- Else: extend component → `currEnd = max(currEnd, e)`

Toute la logique fonctionne en un seul passage linéaire après tri.

---

- Oui. 7. Pseudocode

Texte
trier les plages par début
ans = 1
pour Fin =
pour (s, e) dans les fourchettes:
si s > curr Fin :
ans = (ans * 2) mod MOD
currEnd = e
Sinon:
currEnd = max(currEnd, e)
retour et
«» "

---

- Oui. 7. Code de référence

> **Java**

"Java
solution de classe {
finale statique privée longue MOD = 1_000_000_007L;
Int public countWays(int[][] gammes) {
les tableaux.sort(plages, a, b) -> Integer.compare(a[0], b[0]);
long ans = 1;
long curr Fin = Long.MIN_VALUE;
pour (int[] r : gammes) {
long s = r[0], e = r[1];
si (s > currEnd) { ans = (ans * 2) % MOD; currEnd = e; }
sinon si (e > currEnd) currEnd = e;
}
retour (int) ans;
}
}
«» "

> **Python**

'`python
MOD = 1 000 000 007

Solution de classe:
def countWays(self, gammes):
gammes.sort(key=lambda x: x[0])
as, curr_end = 1, -10**18
pour s, e dans les fourchettes:
si s > curr_end :
% MOD
_fin_curr = e
Sinon:
_fin_curr = max(curr_end, e)
retour et
«» "

> **C++**

'`cpp
solution de classe {
public:
longue MOD = 1'000'000'007LL;
Int countWays(vecteur<vecteur<int>>&intervalles) {
tri(ranges.begin(), ranges.end(),
[](auto &a, auto &b){ retourner a[0] < b[0]; });
long an = 1, courbure Fin = LLONG_MIN;
pour (auto &iv : gammes) {
long s = iv[0], e = iv[1];
si (s > currEnd) { ans = (ans * 2) % MOD; currEnd = e; }
sinon si (e > currEnd) currEnd = e;
}
le retour des an;
}
};
«» "

---

- Oui. 8. Complexité temporelle et spatiale

* **Heure:** `O(n log n)` en raison du tri, `O(n)` pour le passage.
* **Espace:** `O(1)` auxiliaire (sauf pour le tableau d'entrée), tous en place.

---

- Oui. 9. Pourquoi ça marche – Proof Sketch

1. **Sorting** veille à ce qu'une fois le prochain départ supérieur à "currEnd", aucun intervalle ultérieur ne puisse appartenir à la composante courante.
2. Chaque fois qu'un nouveau composant commence, nous devons décider **à quel** des deux groupes il appartient.
3. Étant donné que les décisions concernant des composants distincts ne s'influencent pas mutuellement, le nombre total de façons est égal au produit de choix binaires indépendants → `2^(#components)`.

---

10 ans. Cas de bord et vérifications finales

* Tous les intervalles se chevauchent → composant unique → réponse `2`.
* Aucun chevauchement des intervalles → `n` composants → réponse `2^n`.
* Vérifier avec `ans = (ans * 2) % MOD` après chaque multiplication pour éviter le débordement.

---

11 ans. Foire aux questions

C'est ce qu'il a dit.
-- -- -- -- -- --
Autres **Puis-je utiliser un jeu ou un hashmap pour stocker des composants?**= Pas besoin – un seul `currEnd` suffit. Autres
Autres **Que faire si `ranges` est vide?**.LeetCode garantit au moins une portée, mais gardez-la si vous vous adaptez aux autres juges. Autres
Autres **Comment calculer les composantes "2^" rapidement?**= En Python, `pow(2, composants, MOD)`. Dans Java/C++, utilisez une exponentiation rapide itérative. Autres

---

- Oui. 12. Conseils d'entrevue

* ** Expliquez d'abord l'idée du composant. **
* **Afficher la justification du tri. **
* **Énoncer la complexité temporelle. **
* ** Manipulation modulée par Mention. **

L'intervieweur apprécie souvent une explication claire de pourquoi nous sommes trier.

---

13 ans. A emporter Résumé

* Tri + une passe → compter les clusters indépendants.
* Le résultat est une puissance de deux.
* Le code est court dans n'importe quelle langue.

---

14 ans. Clôture et appel à l'action

> Maintenant que vous avez fissuré le LeetCode 2580, pratiquez des problèmes similaires basés sur l'intervalle comme le Superlap, les salles de réunion ou les cloisonnements intermédiaires. Joyeux codage !

> **Partager** cet article sur LinkedIn et Twitter pour aider les autres à maîtriser les astuces d'intervalle.

---

**Auteur:** *Votre nom – Data-Structures & Algorithmes Coach*

**Date:** 2024‐09‐28

---

> *Codage heureux et bonne chance pour votre prochaine interview! *

---

> *Suivez pour plus d'articles de préparation d'entrevue et de défis de codage. *

---

Il s'agit d'une réponse technique complète, d'un code de référence dans trois langues principales et d'un billet de blog SEO-friendly, poli et prêt à être déployé.