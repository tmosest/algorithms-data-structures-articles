---
titre: LeetCode 3656. Déterminer si un graphique simple existe -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3656 – Déterminez si un graphique simple existe
### Récapitulation du problème (LeetCode)

> **Grâce à un tableau entier "degrees", où "degrees[i]" est le degré souhaité de vertex *i* dans un graphique *simple* non dirigé (pas de boucles d'auto, pas de bords parallèles).
> **Retour** `true` si un graphique avec exactement ces degrés peut être construit, sinon `faux`.

**Contrôles* *

* `1 ≤ n = degrés de longueur ≤ 105 "
* < 0 ≤ degrés[i] ≤ n − 1»

La solution classique utilise le théorème **Erdős–Gallai** – une séquence de degrés est *graphique* si elle satisfait un ensemble d'inégalités.
Ci-dessous vous trouverez des implémentations de travail dans **Java, Python et C++** (O(n log n)), suivi d'un article de blog détaillé qui explique la théorie, met en lumière les pièges, et montre comment maîtriser ce problème peut booster votre CV d'interview.

---

Code – Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public booléen simpleGraphExists(int[] ds) {
int n = longueur ds;
Arrays.sort(s); // non-diminution

// 1. Contrôle de parité – le degré total doit être égal
long total = 0;
pour (int d : ds) total += d;
si (total et 1L) == 1L) retourner faux;

// 2. Préfixer les sommes – nous les réutiliserons dans la boucle
long[] préfixe = nouveau long[n + 1]; // préfixe[i] = d0 + ... + d(i-1)
pour (int i = 0; i < n; i++) préfixe[i + 1] = préfixe[i] + ds[i];

// 3. La boucle principale – l'inégalité Erdős–Gallai
pour (int k = 1; k <= n; k++) {
// Côté gauche : sum_{i=1..k} d_i (1-based)
long lhs = préfixe[k];

// Côté droit : k(k-1) + sum_{i=k+1..n} min(d_i, k)
ghs longs = (long) k * (k - 1);
// Trouver le premier indice > k
int idx = upperBound(ds, k, 0, n); // indice du premier > k
// Pour i = k+1 .. idx-1 : d_i <= k → ajouter d_i
rhs += préfixe[idx] - préfixe[k];
// Pour i = idx .. n-1 : d_i > k → ajouter k chaque
rhs += (long) (n - idx) * k;

si (lhs > rhs) retourner faux;
}
retour vrai;
}

/** recherche binaire standard: premier index en [lo,hi) avec arr[i] > val */
Int upperBound(int[] arr, int val, int lo, int hi) {
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (arr[mid] <= val) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}
}
«» "

> **Pourquoi ça marche* *
> *Sorting* apporte des degrés dans l'ordre croissant, nous permettant d'utiliser des sommes de préfixe.
> L'inégalité Erdős-Gallai indique que pour tous les «k» (1-basé)
> ^{i=1}^{k} d_i ≤ k(k-1) + "(d_i, k)"
> Si l'inégalité échoue pour un `k`, aucun graphique simple ne peut réaliser la séquence.
> Un contrôle de parité est une sortie précoce bon marché : la somme des degrés doit être égale (lemma de shake de main).

---

Code – Python

'`python
Solution de classe:
Def simpleGraphExists(self, degrees: list[int]) -> bool:
n = len(degrés)
degrés.sort() # non-diminution

1. Vérification de la parité
si somme(degrés) % 2:
Retour Faux

2. Préfixer les sommes
pref = [0] * (n + 1)
pour i, d en nombre (degrés):
pref[i + 1] = pref[i] + d

3. Boucle Erdős–Gallai
pour k dans la plage(1, n + 1):
lhs = pref[k]

# Trouver le premier indice où le degré > k
lo, salut = k, n
alors que:
milieu = (lo + hi) // 2
si degrés[milieu] <= k:
lo = milieu + 1
Sinon:
hé = milieu
idx = lo # premier indice > k

rhs = k * (k - 1)
rhs += pref[idx] - pref[k] # d_i <= k partie
rhs += (n - idx) * k # d_i > k partie

si lhs > rhs:
Retour Faux

retour Vrai
«» "

> **Notes spécifiques au python**
> * `list[int]` syntaxe requise Python 3.9+.
> * La recherche binaire est alignée pour la vitesse (aucune importation `bisect`).
> * Préfixer les sommes permet O(1) gamme des requêtes de somme.

---

Code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool simpleGraphExists(vecteur<int>& degrés) {
int n = degrés.size();
tri(degrees.begin(), degrees.end()); // non-diminution

// 1. Vérification de la parité
long total = 0;
pour (int d : degrés) total += d;
si (total & 1LL) retourner faux;

// 2. Préfixer les sommes
vecteur <long> pref(n + 1, 0);
pour (int i = 0; i < n; ++i) pref[i + 1] = pref[i] + degrés[i];

// 3. Boucle Erdős–Gallai
pour (int k = 1; k <= n; ++k) {
long lhs = pref[k];

// Trouver le premier indice où le degré > k (en haut)
int idx = upper_bound(degrees.begin() + k, degrees.end(), k) - degrees.begin();

longue durée = 1LL * k * (k - 1);
rhs += pref[idx] - pref[k]; // degrés <= k
rhs += 1LL * (n - idx) * k; // degrés > k

si (lhs > rhs) retourner faux;
}
retour vrai;
}
};
«» "

> **Notes spécifiques C++**
> * `upper_bound` de `<algorithm>` est utilisé pour localiser le premier élément `> k`.
> * Long est utilisé pour éviter le débordement quand `n` peut être 105 et degrés jusqu'à n-1.

---

4. Article du blog – Déterminer si un graphique simple existe: Le bon, le mauvais, et le mauvais

---

Introduction

Dans n'importe quel **interview** pour un rôle d'ingénierie logicielle, vous allez souvent rencontrer des questions qui semblent simples à la surface mais cachent des défis algorithmiques profonds. L'un de ces problèmes est de déterminer si un graphique simple existe.** (LeetCode 3656). C'est une illustration parfaite de la façon dont la théorie **graph** peut rencontrer **coder le monde réel**.

Si vous pouvez maîtriser ce problème, vous allez non seulement impressionner les recruteurs avec votre maîtrise du théorème **Erdős–Gallai**, mais aussi démontrer:

- **La pensée mathématique** (lemma à la main, inégalités)
- ** Optimisation algorithmique** (O(n log n) vs. naïve O(n2))
- **Attention aux cas de bord** (dépassement, parité, gros intrants)

Laissez passer le **good**, le **bad** et le **ugly** de résoudre ce problème, et voyez comment la solution s'inscrit dans votre arsenal d'interviews.

---

Le bon – ce qui fait Ce problème précieux

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Concrete graph-theoretic concept**=Il vous force à appliquer le théorème Erdős–Gallai, un pilier d'analyse de séquence de degré. Autres
**Clarifier le contrat d'entrée-sortie**Les degrés sont un tableau entier, aucune représentation graphique cachée. Autres
** Contraintes évolutives**= Jusqu'à 105 sommets – nécessite un algorithme linéarithmique, et non une force brute. Autres
Autres **Riche de discussion**= Vous pouvez parler de la poignée de main lemma, la nécessité d'une somme égale, et pourquoi les graphiques simples diffèrent des multigraphes. Autres

> **À emporter**: LeetCode 3656 est un classique *d'entrevue autonome* qui teste la théorie et le codage.

---

Les mauvaises – Pièges communs

1. ** Oublier la vérification de la parité* *
La somme des degrés doit être égale (chaque bord contribue 2). Passer cette sortie précoce conduit à un travail inutile et peut vous induire en erreur en pensant qu'une séquence est valide.

2. **Excédent total**
Avec n ≤ 105 et chaque degré ≤ n − 1, la somme peut atteindre ~1010. Utilisez des entiers 64 bits («long long» en C++, «long» en Java, «int» en Python est une précision arbitraire).

3. **Mis-indexation de l'inégalité**
Erdős–Gallai est basé sur 1; oublier d'ajuster les indices après tri (ou en utilisant des tableaux basés sur 0) donne de mauvais résultats.

4. **O(n2) Mise en œuvre naïve**
Summing min(d_i, k) pour chaque k conduit à O(n2), qui fois sur la limite supérieure 105.

5. **Bon supérieur incorrect**
Trouver le premier degré supérieur à "k" est essentiel. Un balayage linéaire de chaque itération transforme l'algorithme en O(n2).

---

### Les horribles cas de bord qui sillonnent même les codeurs expérimentés

Pourquoi il rompt des solutions naïves Comment le manipuler
Il y a un problème.
**Tous les zéros**= La somme totale est 0 (même), mais chaque inégalité est insignifiante. Aucun code spécial n'est nécessaire. Autres
**Tous les "n-1"** graphe complet, somme totale = n(n-1), même si n n est pair. L'inégalité se réduit à `k(k-1) + ...`. Autres
Un vertex avec le degré n-1 oblige tous les autres à avoir au moins 1, mais si beaucoup sont zéro, l'inégalité échoue tôt. C'est vrai. L'algorithme détecte cela dans les premiers `k`. Autres
**Dupliquer les degrés**Le théorème se soucie seulement du multiset, pas de la spécificité. Le tri prend soin de commander; les duplicatas sont très bien. Autres
**Diplômes négatifs**= L'entrée garantit 0 ≤ degré ≤ n−1, mais certaines langues (par exemple, les anciens compilateurs C++) peuvent accepter des ints négatifs. Valider l'entrée ou compter sur les contraintes. Autres

> ** Ligne de bottom** : Une solution robuste doit traiter *chaque* entrée gracieusement – ne jamais assumer une distribution ..

---

Comment expliquer Ceci à un gestionnaire d'embauche

1. **Énoncer clairement le problème** – une séquence de degrés, simple graphique non dirigé, demander l'existence.
2. **Mention la poignée de main lemma** – degré total même, rejet rapide.
3. **Introduire Erdős–Gallai** – le théorème clé; montrer l'inégalité graphiquement.
4. **Extrait l'algorithme** – trier, préfixer les sommes, rechercher la limite supérieure, boucler sur k.
5. **Complexité** – temps O(n log n), espace O(n).
6. **Options possibles** – Tri pour le temps O(n) si les degrés sont limités.
7. **La robustesse du boîtier d'Edge** – montre comment votre code gère le dépassement et la parité.

Ce récit démontre *profondeur de résolution de problèmes* et *pragmatisme d'ingénierie de logiciels* – exactement ce que veulent les intervieweurs.

---

Conseils pratiques de mise en œuvre

Mots clés Pourquoi ça aide
- C'est quoi ?
Utiliser `long` pour préfixer les sommes, `Arrays.sort`. Autres
**Python** Pas d'importations supplémentaires, assez rapides pour 105. Autres
**C++**="upper_bound`" de `<algorithm>`, `long long`.=" Utilisation très concise et optimale de STL. Autres

---

### - Bonus – Dénombrement-Trier Variante (O(n))

Si les valeurs de degré sont garanties dans `[0, n-1]`, vous pouvez remplacer `Arrays.sort` (O(n log n)) par un tri de comptage:

1. Compter les fréquences de chaque degré.
2. Construire le tableau trié par itération sur les comptes.
3. Toutes les autres étapes restent les mêmes.

La complexité temporelle tombe à **O(n)**, mais le code devient un peu plus long. Pour les paramètres d'entrevue, la solution `O(n log n)` est généralement suffisante et plus facile à discuter.

---

Comment cela peut-il aider votre recherche d'emploi?

* **Afficher la largeur** – théorie des graphiques + conception de l'algorithme.
* ** Démontre la profondeur** – compréhension des théorèmes et des preuves.
* **Surligne les compétences de codage** – manipulation soigneuse des boîtiers de bord, boucles optimisées, structure propre.

Lorsque vous atterrissez une conversation autour de LeetCode 3656, vous vous sentirez confiant présenter une solution qui est ** à la fois mathématiquement saine et pratiquement efficace**. C'est ce que cherchent les intervieweurs.

---

Lire plus

- * Théorie des Graphiques* de Reinhard Diestel – chapitre sur les séquences de degrés.
- *Algorithme Design* de Kleinberg & Tardos – section sur les problèmes de graphiques linéaires.
- Discussions LeetCode pour 3656 – clarifications du monde réel et approches alternatives.

---

Verdict final

**LeetCode 3656** peut ressembler à une simple question de vérification, mais c'est en fait une passerelle vers le raisonnement algorithmique profond**. Maître, présentez-le clairement, et vous ouvrirez des portes à des rôles qui valorisent la théorie et la pratique.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

* Sentez-vous libre de copier les extraits de code ci-dessus dans votre propre projet ou interview prep repo. Les implémentations en trois langues illustrent que le même noyau mathématique se traduit de façon transparente entre les écosystèmes. *