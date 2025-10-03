---
titre: LeetCode 2156. Rechercher une sous-chaîne Avec la valeur Hash donnée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code – Trois langues

Ci-dessous, vous trouverez des solutions propres et prêtes à la production pour LeetCode **2156 – Trouver une sous-chaîne avec une valeur Hash donnée** dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même idée – un hasch* en roulis calculé *backwards* (de droite à gauche) – afin que vous puissiez choisir et coller celui qui correspond à votre pile.

> **Astuce** – Lorsque vous soumettez à LeetCode, vérifiez toujours que vous utilisez **long** (64 bits) pour le hachage intermédiaire.
> Le produit `val * power` peut facilement déborder un int 32-bit quand `modulo` 109.

---

Java – `Solution.java "

"Java
solution de classe {
chaîne publique subStrHash(chaînes, puissance int, int modulo, int k, int hashValue) {
// Nous marchons de la fin de la corde jusqu'au début.
long curHash = 0; // courant de roulage (modulo)
longue puissanceK = 1; // puissance^k % modulo (conduira en se déplaçant à gauche)
int n = s.longueur();
réponse int = 0; // index de la première sous-chaîne correspondante

// Puissance précalculée en % modulo pendant la marche
pour (int i = n - 1; i >= 0; i--) {
// Ajouter le nouveau caractère (position actuelle)
curHash = (puissance de curHash * + (s.charAt(i) - 'a' + 1)) % modulo;

// Si nous avons déjà passé des caractères k, supprimer le plus ancien
si (i + k < n) {
// char le plus ancien = s.charAt(i + k)
retrait long = ((long)(s.charAt(i + k) - 'a' + 1) * powerK) % modulo;
curHash = (curHash - supprimer + modulo) % modulo; // garder positif
}

// Une fois que nous avons atteint la première fenêtre de longueur k, enregistrez-la
si (i + k <= n) {
// Rappelez-vous cet index seulement si le hachage correspond.
// Parce que nous nous déplaçons en arrière, le dernier coup est le
// la plus ancienne sous-chaîne dans l'ordre original.
si (curHash == hashValue) {
réponse = i;
}
}

// Puissance de croissance K pour la prochaine suppression (la prochaine itération déplace une étape de plus à gauche)
powerK = (powerK * power) % modulo;
}

retourner s.substring(réponse, réponse + k);
}
}
«» "

> **Pourquoi marcher de droite à gauche? **
> La division (par "puissance") est impossible sous modulo parce que "modulo" peut ne pas être coprime avec "puissance".
> Marcher en arrière nous permet de *multiplier* au lieu de *diviser*, ce qui maintient les mathématiques simples.

---

Python – `solution. py "

'`python
Solution de classe:
def subStrHash(self, s: str, power: int, modulo: int,
k: int, hashValue: int) -> str:

cur_hash = 0 # hash courant (modulo)
power_k = 1 # power^k % modulo
n = len(s)
réponse = 0

Marche de la fin au début
pour i dans la fourchette(n - 1, -1, -1):
cur_hash = (puissance de cur_hash * + (ord(s[i]) - 96)) % modulo

si i + k < n: # nous avons une fenêtre complète, déposez la plus ancienne
supprimer = ((ord(s[i + k]) - 96) * power_k) % modulo
cur_hash = (cur_hash - supprimer) % modulo

# rappelez-vous *dernier* indice qui correspond – c'est la plus ancienne sous-chaîne
si cur_hash == hash Valeur & #160;:
réponse = i

power_k = (power_k * power) % modulo

retour [réponse:réponse + k]
«» "

> `ord(s[i]) - 96` est un moyen rapide de calculer `val(s[i]` ( `'a'` → 1, `'b'` → 2 ...).

---

C++ – `Solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne subStrHash(chaîne s, puissance int, int modulo,
Int k, Int HashValue) {
longue courbure longue = 0; // courant de roulage (modulo)
longue puissanceK = 1; // puissance^k % modulo
n = (int)s.size();
réponse int = 0; // index de la première sous-chaîne correspondante

pour (int i = n - 1; i >= 0; --i) {
// Ajouter le nouveau caractère à la position i
curHash = (puissance de curHash * + (s[i] - 'a' + 1)) % modulo;

// Supprimer le caractère qui est maintenant hors de la fenêtre
si (i + k < n) {
long retrait long = ((long long)(s[i + k] - 'a' + 1) * powerK) % modulo;
curHash = (curHash - supprimer + modulo) % modulo;
}

si (curHash == hashValue) // rappelez-vous le dernier coup
réponse = i;

powerK = (powerK * power) % modulo;
}

retour s.substr(réponse, k);
}
};
«» "

> `substr` est équivalent à `substring` en Java – les deux prennent *zero-based* indices.

---

Article de blog – SEO-Optimisé & Job-Interview

> **Titre (H1)* *
> LeetCode 2156 – Trouver un sous-chaîne Avec une valeur Hash donnée : Solutions Rolling‐Hash + Sliding‐Window (Java, Python, C++)* *

---

Résumé du problème

Dans LeetCodes **2156**, vous recevez une chaîne `s`, un entier `power`, un entier `modulo`, une longueur de fenêtre `k` et une valeur de hachage `hashValue`.
Vous devez retourner la sous-chaîne **first** de la longueur `k` dont *hash* (défini ci-dessous) égale `hashValue`.

**Définition en espèces**

«» "
hash(s[i ... i + k – 1], puissance, modulo) =
( valeur(s[i]) * puissance
+ val(s[i+1]) * puissance^1
+ ... + valeur(s[i+k-1]) * puissance^(k-1) % modulo
«» "

`val(c)` = (`'a'` → 1, `'b'` → 2 ...).

---

Pourquoi une fuite ?

**Pour**
C'est quoi ?
• **O(n)** temps – une seule passe sur `s` (.....) • Nécessite une manipulation soigneuse de **arithmétique modulaire**; valeurs négatives après soustraction
• **O(1)** espace auxiliaire (juste quelques longs) Si vous calculez de gauche à droite, vous avez besoin d'un inverse modulaire de "puissance", qui est coûteux / compliqué.
• Fonctionne pour *any* `modulo`, même non-coprime avec `power`

---

La technique de retour à gauche

1. **Pre-compute** `power^k modulo` en marchant à gauche.
Cette valeur (`powerK`) vous permet de *soustraire* le caractère qui laisse la fenêtre dans O(1).

2. **Démarrer à partir de la fin** de la chaîne.
Pour chaque caractère `c = s[i]`:
* `curHash = (curHash * power + val(c)) % modulo` –– ajouter le nouveau caractère.
* Si nous avons déjà traité au moins des caractères `k`, soustrayez le caractère *le plus ancien* :
`remove = val(s[i+k]) * powerK % modulo "
`curHash = (curHash - supprimer + modulo) % modulo` (ajouter `modulo` avant `%` pour le garder positif).

3. **Enregistrez le dernier indice** où `curHash == hashValue`.
Parce que nous marchons à partir de la droite, le *dernier* coup dans ce passage est le *premier* sous-chaîne correspondant dans l'ordre avant.

---

Complexité

- **Heure** : `O(n)` – un passage sur `s`.
- **Espace** : `O(1)` – une poignée de longues variables.

---

Pièges et correctifs communs

Numéro
C'est quoi ?
**Overflow** (`val * power`)= Utiliser `long` (64-bit). `(long)val * power) % modulo`. Autres
**Modulo négatif** après soustraction. Autres
**Off‐by‐one** dans les indices de sous-chaîne. Autres
**Large `modulo` .... .. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . Autres

---

Cas d'essai d'échantillon

Entrée <======================================================================================================================================================================================================================================
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
""abcd"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
""abcd"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
""a"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Exécutez le code dans LeetCode ou votre IDE préféré pour vérifier.

---

## 3="Blog – "Maîtrise du LeetCode 2156: Une feuille de cheat d'interview en rolling-Hash"

> **Mots clés** – `LeetCode 2156`, `Find Substring With Given Hash Value`, `rolling hash`, `sliding window`, `Java solution`, `Python solution`, `C++ solution`, `hash function`, `job interview algorithme`, `coding interview practice`.

---

Introduction

> *Hash it up, glissez-le vers l'avant – le défi LeetCode 2156 est un cas de manuel de hachage roulant et de fenêtre coulissante. Maîtrisez-le, et vous acquerrez un tout nouvel ensemble de questions d'entrevue.

Si vous vous préparez à une entrevue sur les structures de données ou à un rôle d'ingénierie *logiciel*, ce problème est une vitrine parfaite de votre capacité à gérer **arithmétique modulaire** et **traitement efficace des chaînes**. L'article suivant vous emmène à travers les parties **good**, **bad** et **ugly** de la résolution 2156, vous donne le code complet en trois langues, et explique pourquoi il est une grande vitrine d'interview.

---

Récapitulation des problèmes

> **Input**
> - `s` – une chaîne de lettres minuscules (`1 ≤=1 ≤ 105`)
> - `puissance` – base du hachage (`2 ≤ puissance ≤ 106`)
> - `modulo` – module (`2 ≤ modulo ≤ 109`)
> - `k` – longueur de la fenêtre de sous-chaîne (`1 ≤ k ≤=")
> - `hashValue` – valeur de hachage cible (`0 ≤ hashValue < modulo`)

> **Tâche**
> Trouvez le **premier** sous-chaîne de longueur `k` dont le hachage est égal à `hashValue`, selon la formule ci-dessus.
> Si aucune sous-chaîne n'existe, retournez une chaîne vide.

---

Pourquoi 2156 une question d'entrevue ?

1. **Score Hashing** – montre que vous pouvez transformer une chaîne en une empreinte numérique, une technique courante dans la conception de l'algorithme* (p. ex. Rabin-Karp).
2. **Modulaire Arithmétique** – Travailler avec de gros modules est une compétence subtile que beaucoup de candidats ignorent.
3. **Fenêtre coulissante** – Points saillants de votre compréhension des mises à jour de la fenêtre *O(1)*, essentielles pour de nombreux problèmes *en temps réel*.
4. **Élégance algorithmique** – La marche arrière élimine le besoin d'inverses modulaires, rendant la solution à la fois **clean** et **fast**.

---

Ce qui fonctionne si bien

1. **Linear Time** – `O(n)` garantit que même les cordes les plus longues autorisées se terminent en millisecondes.
2. **Espace continu** – Seulement quelques longues variables ; pas de tableaux supplémentaires ou de tables de hachage.
3. **Non Modulo Inverse** – Évite les maths lourds; au lieu de cela, vous multipliez, ce qui est trivial sous module.
4. ** Technique réutilisable** – Le même motif (enroulement arrière + soustraction de puissance ^k) s'applique aux requêtes *Rabin‐Karp* et *prefix‐hash*.

---

Le "Bad" – Ce qui piège les débutants

Une mauvaise pratique
C'est quoi ?
**La multiplication de gauche à droite**= Sans inverse modulaire, vous êtes coincé; la base `power` peut partager des facteurs avec `modulo`. Autres
**Ignorer les résultats négatifs**.La soustraction du caractère de sortie peut produire un nombre négatif ; l'utilisation de « % » sur un long négatif en C++/Python le laisse négatif, brisant le contrôle d'égalité. Autres
**L'utilisation d'ints 32 bits**Le produit `val * power` peut dépasser `231`; le compilateur peut enrouler silencieusement, donnant de mauvais hachages. Autres
**Confusion d'indices**= Rappelez-vous que la sous-chaîne Java utilise les indices *end‐exclusive*; la sous-chaîne C++= prend de la longueur. Une erreur courante se produit lors de la conversion entre les langues. Autres

---

Les pièges de bord

Un cas d'Edge de la manière la plus fréquente
-- -- -- -- -- -- -- -- -- -- -- -- -- --
`k` est égal à la chaîne entière. Autres Traitez la chaîne complète comme une fenêtre ; l'algorithme revient naturellement. Autres
"modulo" égale Tous les hachages deviennent zéro; mais « hashValue » peut toujours être non-zéro. Assurez-vous que l'algorithme ne se divise pas par zéro; le produit `(powerK * power) % modulo` restera zéro. Autres
Autres Très grande "puissance" (soit 106) et très petite "modulo" Autres 2).Utilisez des entiers 64 bits ; modulo réduit la valeur rapidement, empêchant ainsi la croissance de la fuite. Autres

---

### -Le code complet des extraits (trois langues)

L'article ci-dessus énumère les implémentations **Java**, **Python** et **C++** en un seul endroit. Copiez/collez-les dans LeetCode, testez sur votre machine locale ou exécutez-les dans un compilateur en ligne. La logique de base – passage en arrière + soustraction `powerK` – reste la même, juste des changements de syntaxe.

---

Pourquoi 2156 est un problème d'exposition**

- ** Démontre l'arithmétique modulaire**: Beaucoup d'intervieweurs s'interrogent sur « Hashing » ou « Rabin‐Karp ». Vous montrez que vous savez comment gérer correctement `%`, y compris le cas de coin de soustraction.
- **Fenêtre coulissante : Les fenêtres coulissantes sont un aller-retour pour les requêtes *range* et *problèmes d'intervalle*. Si vous clouez 2156, vous êtes déjà à l'aise avec ce modèle.
- **Scales**: La solution `O(n)` montre que vous pouvez résoudre les problèmes avec de grandes contraintes (105 caractères) efficacement – un must-have pour les logiciels haute performance.
- **Language-agnostique**: Avoir des solutions prêtes à l'emploi en Java, Python et C++ montre que vous pouvez changer de contextes en fonction de la pile technique du travail.

---

Comment utiliser cette feuille de chaleur

1. **Pratique** – Exécuter les trois implémentations sur tous les cas d'essai officiels sur LeetCode ; modifier le code pour plus de clarté ou ajouter des commentaires.
2. **Exposer** – Dans une entrevue, passer par l'approche en arrière, en soulignant pourquoi nous multiplions plutôt que de diviser.
3. **Afficher les variantes** – Demandez: Et si `pouvoir` était 1? Et si `modulo` était 1? Montrez que vous pouvez raisonner sur les cas de coin.
4. **Mentions compromis** – Précisez brièvement que de gauche à droite aurait besoin d'un inverse modulaire et est donc moins efficace.

---

À emporter

> *Si vous pouvez expliquer LeetCode 2156 dans une salle pleine d'ingénieurs, vous démontrerez la maîtrise des deux **chiffres de chaîne** et **arithmétique modulaire** – deux piliers de la conception d'algorithmes. *

> Qu'il s'agisse d'un poste de développeur de logiciels **, d'un poste d'ingénieur de données ** ou d'une carrière de programmation ** compétitive**, la technique de rolling-hash que vous apprenez ici sera payante pour les mois à venir.

---

Lire plus

- *L'algorithme Rabin-Karp* – l'approche classique du hachage roulant pour la recherche sous-chaîne.
- *Fenêtre coulissante* – un modèle qui apparaît dans les problèmes comme la somme de Subarray maximale de la taille K.
- *Modulaire Inverse* – quand et comment le calculer (utile pour d'autres problèmes).
- *Big O Notation* – continuer à pratiquer pour repérer rapidement si un algorithme passera de grandes entrées.

---

Clôture

> C'est le mantra de LeetCode 2156. Coder la solution, comprendre les maths, et en parler dans votre prochain entretien. (en milliers de dollars)

Joyeux codage, et que vos haches soient toujours *juste*!

---

**Fin du blog. **
(Sentez-vous libre de publier sur Medium, Dev.to, ou votre site de portefeuille personnel – la structure garantit qu'il sera bien classé pour les mots clés ciblés.)