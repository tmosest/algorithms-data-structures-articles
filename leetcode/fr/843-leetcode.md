---
titre: LeetCode 843. Devinez le mot -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Guérissez la Parole – 843**
*(Java – interface interactive de Master)*

---

- Oui. 1. Récapitulation des problèmes

On vous donne une *liste de mots* pouvant atteindre 10 000 chaînes de 6 lettres (toutes de même longueur).
L'un d'eux est le mot **secret**.

Vous pouvez rattraper **10 devinettes**.
Après chaque supposition, l'objet `Master` vous indique combien de caractères correspondent au mot secret ** aux mêmes positions** (un entier `0 ... 6`).
Si vous devinez le mot secret, le jeu se termine avec succès; sinon vous devez continuer à deviner jusqu'à ce que vous frappez le mot secret ou fuyez les tentatives.

Votre travail est d'écrire une fonction

"Java
vide findSecretWord(String[] wordlist, Master)
«» "

qui fait la séquence de devinettes et garantit une victoire dans le nombre autorisé de tentatives.

---

- Oui. 2. Ce que l'intervieweur demande vraiment

1. **Pouvez-vous modéliser l'interaction comme un problème de recherche? * *
– Chaque devin partitionne le candidat actuel en fonction de la valeur de la rétroaction.
2. **Quelle est la prochaine idée? **
– Nous voulons réduire l'ensemble des candidats le plus rapidement possible (maximiser le gain d'information).
3. **Quels compromis voulez-vous faire? * *
– La stratégie optimale (minimax) est coûteuse; une heuristique pratique suffit souvent.

Expliquez que nous résolvons un jeu d'information *imperfect* dans le but de minimiser le plus mauvais nombre de devinettes.

---

- Oui. 3. Stratégie de haut niveau

1. **Démarrer avec un avoueur *
– Choisissez n'importe quel mot (aléatoire ou déterministe).
– Appeler `master.guess(pivot)' → obtenir des correspondances `m`.

2. **Filtrer la liste**
– Gardez seulement les mots qui donnent exactement `m` matches avec le pivot.
– Tous les autres mots sont impossibles.

3. **Cité**
– Si la liste filtrée n'a plus qu'un mot, devinez-le.
– Sinon, choisissez un autre mot dans la liste filtrée (souvent aléatoire).
– Répétez l'étape de filtrage en utilisant la nouvelle conjecture.

4. **Stop**
– Soit vous avez frappé 6 matches (trouver le secret) ou vous avez utilisé les 10 devinettes.

---

- Oui. 4. Pourquoi cela fonctionne

- **La nourriture est exacte** – Si un mot donne `k` correspond, tout candidat doit donner le même `k`.
- **Filter rétrécit l'espace de façon exponentielle** – Dans une distribution aléatoire, chaque supposition élimine à peu près une fraction constante des mots restants.
- **Random ou pivot déterministe** – Tous deux sont fins; le hasard empêche les constructions pathologiques du pire cas, déterministe (par exemple, basé sur la similitude minimax) garantit ≤ 10 hypothèses en moyenne.

---

- Oui. 5. Algorithmes pratiques

5.1 Filtrage aléatoire/greedy (simple)

"Java
solution de classe {
Int match(String a, Chaîne b) { ... } // compter les caractères de même position

public vide trouverSecretWord(String[] mots, maître) {
Liste des candidats <String> = nouvelle liste d'array<>(Arrays.asList(mots));

pour (int i = 0; i < 10 &&!candidats.isEmpty(); i++) {
// choisissez le i‐ième mot (ou au hasard dans la liste)
String devine = candidate.get(0); // déterministe
matchs int = master.guess(guess);
Si (comparaisons) 6) retour; // succès

// Filtre
Liste<String> suivante = nouvelle liste de distribution<>();
pour (String w : candidats) {
si (w.equals(guess)) continue;
si (match(guess, w) == correspond) suivant.add(w);
}
candidats = suivants;
}
}
}
«» "

*Complexité:*
- `match()` est `O(6)` → constante.
- Chaque itération scanne tous les mots restants → `O(n)` par tour.
- Dans le pire des cas "O(n2)" mais dans la pratique, la liste se rétrécit rapidement.

5.2 Greedy basé sur la similitude (meilleure chose pour les données aléatoires)

1. **Score de similitude précalculé**
- Pour chaque mot compter combien d'autres mots partagent au moins un même caractère à la même position.

2. **Trier la liste de mots descendant par ce score* *
- Le mot le plus populaire éliminera de nombreux candidats sur un retour de match de 0.

3. **Guess dans cet ordre, filtrage après chaque supposition* *
- Même étape de filtrage que ci-dessus.

*Pourquoi cela aide: *
Lorsque vous vous attendez à ce que la plupart des suppositions retournent les matches `0` (=80 % de chance), choisir un mot qui correspond à beaucoup d'autres dans au moins une position supprime une grande partie des possibilités si la rétroaction est `0`.

---

- Oui. 6. Cas de bord et discussion

Ce qui arrive Pourquoi c'est OK
C'est quoi ?
Autres Tous les mots sont complètement distincts (par exemple, ""abcdef", "ghijkl", ...)
Le pivot aléatoire pourrait encore réussir dans les 10 conjectures.
``wordlist.length` > 10 000' Filtre toujours `O(n)` Chaque tour est limité par les contraintes du problème.

---

- Oui. 7. Résumé de la complexité

- **Heure:**
«O(n2 * 6)» le cas le plus défavorable, mais le cas moyen est «O(n log n)» en raison d'un rétrécissement exponentiel.
- **Espace:**
`O(n)` pour la liste des candidats.

---

- Oui. 8. Comment présenter cela à un intervieweur

1. **Clarifier le problème:**
Nous jouons un jeu interactif ; chaque supposition nous donne le nombre de positions correctes. (en milliers de dollars)

2. **Exposer l'idée de base:**
Déplacer le jeu du candidat en utilisant la rétroaction exacte du match; toute hypothèse qui ne correspond pas élimine un grand nombre de mots. (en milliers de dollars)

3. ** Expliquer le choix algorithmique:**
- Choisissez le premier mot (ou un mot aléatoire) comme mon pivot, interrogez le Maître, puis gardez seulement les mots qui produisent le même feedback. (en milliers de dollars)
- Je répète jusqu'à ce que je trouve le secret ou que la liste soit à un. (en milliers de dollars)

4. **Discussion temps/espace compromis**
Nous balayons la liste chaque tour, donc c'est `O(n)` par devinette. Parce que la liste se rétrécit rapidement, c'est acceptable. (en milliers de dollars)

5. **Extensions de peine**
- Si nous voulons être plus intelligents, nous pourrions calculer un score de similitude et toujours choisir le mot le plus « informatif ». (en milliers de dollars)
- Cela apporte des idées minimax ou basées sur l'entropie, mais la solution simple cupidité répond à la limite des 10gues. (en milliers de dollars)

6. ** Afficher l'extrait de code* *
Voici une mise en œuvre concise qui suit les étapes ci-dessus. (en milliers de dollars)

---

Note finale

Le noyau de la solution est **iterative filtrant** basé sur des correspondances de position exacte.
Que vous choisissiez un pivot aléatoire, le premier mot ou un pivot pondéré par la similitude, l'idée reste la même : chaque supposition réduit l'espace de recherche, et après une poignée de tours vous serez toujours en mesure de frapper le mot secret dans les tentatives autorisées.