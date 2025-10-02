---
titre: LeetCode 2323. Trouver le temps minimum pour terminer tous les emplois II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2323 – **Trouver le temps minimum pour terminer tous les emplois II**

> **Problème**
> On vous donne deux tableaux "emplois" et "travailleurs" (tous deux de longueur *n*).
> `emplois[i]` est le temps nécessaire pour terminer le travail *i* (en heures),
> `travailleurs[j]` est le nombre d'heures qu'un travailleur peut travailler **en une journée**.
> Chaque emploi doit être attribué à un seul travailleur et chaque travailleur obtient exactement un emploi.
> Retourner le nombre minimum de jours requis pour que tous les emplois soient terminés.

> **Exemple**
> ```texte
> emplois = [5, 2, 4]
> travailleurs = [1, 7, 5]
> sortie = 2
> `` "
> (Optimal affectation: 5h emploi → travailleur 5h/jour, 4h emploi → travailleur 7h/jour, 2h emploi → travailleur 1h/jour.)

---

## TL;DR – La solution d'une ligne

Texte
Trier les deux tableaux, coupler le plus petit travail avec le plus petit travailleur,
le plus grand emploi avec le travailleur le plus rapide.
Réponse = max( ceil(jobs[i] / workers[i])
«» "

Pourquoi ? Parce que l'inégalité *de réarrangement* nous dit que l'appariement du plus gros emploi avec le travailleur le plus rapide (plus petite capacité de travail) minimise le temps maximum de finition.

---

- Oui. 1. Le bien – Pourquoi Cela fonctionne

Étape Ce que nous faisons Pourquoi c'est correct
- C'est pas vrai.
Il est facile de créer des emplois en ordre non décroissant. Autres
§2"workers.sort()"" Permet la même gamme pour les travailleurs. Autres
"Journées = ceil(jobs[i] / workers[i])"" Nombre de jours qu'un travailleur a besoin pour terminer ce travail. Autres
Le programme complet se termine lorsque la paire la plus lente se termine. Autres

**Pourquoi l'appariement est-il optimal? **
Prendre deux emplois `A > B` et deux travailleurs `X > Y` (c.-à-d., `X` est plus rapide).
Si nous jumelons `A → X` et `B → Y`, le nombre total de jours nécessaires sont
"max(ceil(A/X), ceil(B/Y)"
Si nous changeons la mission, les jours deviennent
"max(ceil(A/Y), ceil(B/X))".
Parce que `A/Y ≥ A/X > B/X`, l'affectation échangée ne peut jamais être meilleure, de sorte que l'appariement original est optimal.

---

- Oui. 2. Le "Bad" – Les choses à surveiller

Numéro Comment corriger
- C'est quoi ?
**Rondissement de la division entière** - 1) Les travailleurs. Autres
**Les plus grands nombres**=Tous les nombres ≤ 105, donc les entiers 32 bits sont bons. Autres
**Causes d ' exclusion** 1` fonctionne de la même façon; assurez-vous que les deux tableaux sont triés avant d'accéder aux indices. Autres

---

- Oui. 3. Les pièges communs

1. **Mise en lecture du problème** – Certaines personnes pensent que nous pouvons affecter le même travailleur à plusieurs emplois. La déclaration indique * exactement un* emploi par travailleur.
2. **Off‐by‐one dans la division** – L'utilisation de `emplois[i] / travailleurs[i]` va tronquer à zéro pour de petits ratios; vous avez besoin du plafond.
3. **Trier dans le mauvais ordre** – Si vous triez un tableau ascendant et l'autre descendant, vous jumelez le travail le plus lent avec le travailleur le plus lent – ce qui est * pire* possible.

---

- Oui. 4. Analyse de la complexité

Algorithme Temps Espace
- C'est quoi ?
Autres Trier les deux tableaux + balayage linéaire (tri sur place)

Avec `n ≤ 105`, cela s'inscrit facilement dans les limites.

---

- Oui. 5. Mise en œuvre du code

Voici trois solutions complètes et autonomes dans **Java**, **Python** et **C++**.
N'hésitez pas à copier-coller dans votre éditeur préféré.

---

#### 5.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
Int minimum public Temps(int[] emplois, actifs[] travailleurs) {
// 1. Trier les deux tableaux
Les tableaux.sort(emplois);
les tableaux.sort(travailleurs);

// 2. Trouver le maximum de jours nécessaires
maxJours = 0;
pour (int i = 0; i < emploi.longueur; i++) {
// Ceil division: (emplois[i] + travailleurs[i] - 1)/travailleurs [i]
jours = (emplois[i] + travailleurs[i] - 1)/travailleurs [i];
si (jours > maxJours) maxJours = jours;
}
retour maxJours;
}
}
«» "

---

5.2 Python

'`python
durée minimale (emplois, travailleurs):
"""
:type emplois: Liste[int]
:type travailleurs: Liste[int]
:rtype : int
"""
Trier les listes
emplois.sort()
travailleurs.sort()

# Calculer la division maximale de ceil
retour max((j + w - 1) // w pour j, w en zip(emplois, travailleurs))
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

temps minimum (vecteur<int> et emplois, vecteur<int> et travailleurs) {
le tri(emplois.degin(), emplois.end());
tri(workers.degin(), workers.end());

Int ans = 0;
pour (size_t i = 0; i < jobs.size(); ++i) {
jours = (emplois[i] + travailleurs[i] - 1)/travailleurs [i];
ans = max(ans, jours);
}
le retour des an;
}
«» "

---

- Oui. 6. Un guide sur le style du blog :

> **Titre**: *=Cracking LeetCode 2323: Trouver le temps minimum pour terminer tous les emplois II – Une interview complète Feuille de chéat

> **Mots-clés cibles* *
> *LeetCode 2323*, *Trouver le temps minimum pour terminer tous les emplois II*, *solution de Java*, *solution de Python*, *solution de C++*, *entrevue d'algorithme*, *soudre la cupidité*, *programmation d'emplois*, *entrevue d'ingénierie de logiciels*, *prép d'entrevue de backend*, *questions d'entrevue de pile complète*, *entrevue de structures de données*, *conseils d'entrevue d'emploi*

> ** Aperçu**

Section Objet
C'est quoi ?
Autres 1. Aperçu du problème
Autres 2. Intuition et analyse des clés
Autres 3. Solution détaillée
Autres 4. Complexité
Autres 5. Edge Cases & Pièges
Autres 6. Alternative Approaches de recherche binaire + cupidité (surtubé)
Autres 7. Extraits de code
Autres 8. Interview Prep-- Pourquoi ce problème montre la maîtrise du tri et de l'avidité
Autres 9. SEO Closing..Si vous maîtrisez ceci, vous êtes prêt pour les rôles dev senior..

6.1 Exemple d'introduction

> Quand les intervieweurs lancent *Trouver le temps minimum pour terminer tous les emplois II* chez vous, ils testent un motif algorithmique classique: ** tri + gourmand**. Dans cet article, je vais vous guider dans la solution la plus simple et la plus optimale de Java, Python et C++. Vous allez également apprendre pourquoi l'appariement avide fonctionne, pièges communs, et comment maîtriser ce problème peut impressionner les gestionnaires d'embauche dans les entreprises de haute technologie. (en milliers de dollars)

6.2 Fermeture de l'échantillon

> Félicitations ! Vous comprenez maintenant *pourquoi* trier les emplois et les travailleurs et les associer dans cet ordre donne la réponse optimale. Ce genre de perspicacité – voir la vue d'ensemble et réduire un problème d'affectation complexe à un seul balayage linéaire – est exactement ce que les recruteurs recherchent. Pratiquez ce modèle avec d'autres problèmes de programmation (p. ex., *Task Scheduler*, *Paint House*), et vous serez bien préparé pour votre prochaine entrevue en génie logiciel. (en milliers de dollars)

---

- Oui. 7. Comment cela vous aide à obtenir un emploi

1. **Démontre la maîtrise du tri** – La plupart des intervieweurs posent des questions basées sur le tri.
2. **Shows Greedy Insight** – Reconnaître que la solution optimale est *la paire la plus grande avec la plus rapide* est un état d'esprit avide classique.
3. **Edge‐Case Awareness** – La gestion de la division entière et des grandes entrées montre le code prêt à la production.
4. **Multiple Language Mastery** – Fournir des solutions en Java, Python et C++ montre la polyvalence, un trait clé pour les rôles de pile ou de backend.
5. **SEO‐Friendly Blog** – La rédaction d'un article détaillé et riche en mots clés renforce votre visibilité en ligne— Lié Dans les messages, des articles moyens, ou des blogs personnels peuvent être partagés avec les recruteurs.

---

**Codage heureux et bonne chance pour votre voyage d'entrevue! * *