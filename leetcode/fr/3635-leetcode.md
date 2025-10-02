---
titre: LeetCode 3635. Temps d'arrivée le plus tôt possible pour les trajets terrestres et aquatiques II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## C'est l'heure la plus précoce pour les trajets terrestres et aquatiques II – la solution complète
> **Un problème d'entrevue pratique qui teste l'intuition gourmande, la manipulation du tableau et les compétences de complexité temporelle* *
> **Langues:** Java.

---

- Oui. 1. Récapitulation des problèmes

Vous avez deux listes d'attractions de parcs thématiques :

**Catégorie** Durée Autres
- C'est quoi ?
"LandStartTime[i]" "Durée de la Terre[i]" Autres
Autres Excursion de l'eau Durée de l ' eau Autres

* Vous devez rouler ** exactement un** à terre et ** exactement un** à l'eau, dans n'importe quel ordre. *

Une promenade peut commencer à l'heure d'ouverture ou à tout moment ultérieur.
Après avoir terminé un tour, vous pouvez immédiatement monter à bord de l'autre (si elle est déjà ouverte) ou attendre qu'il ouvre.

**Objectif :** Retournez le temps d'arrivée le plus tôt possible* pour les deux trajets.

> **Constraints**
> 1 ≤ n, m ≤ 5 · 104, 1 ≤ temps, durée ≤ 105

---

- Oui. 2. Intuition – Pourquoi un balayage de graisse fonctionne

Les seules décisions importantes sont :

1. Quel tour vous choisissez **premier** (terre ou eau).
2. Quelle course spécifique vous choisissez dans cette catégorie.

Le *time* vous terminez le premier tour est indépendant du second tour, parce que vous pouvez toujours attendre le deuxième tour pour ouvrir.
Ainsi, pour un **ordre donné** (Terre → Eau ou Eau → Terre) vous avez seulement besoin du temps de finition le plus avancé de la première catégorie :

* `minLandFinish = min(landStart[i] + landDurée[i]) "
* `minWaterFinish = min(waterStart[j] + waterDurée[j]) "

Une fois que vous connaissez la première fois que vous pouvez terminer le premier tour, le temps d'arrivée pour chaque tour de la deuxième catégorie devient:

«» "
Finale = durée de la seconde
+ max( premier_finish_de_première_catégorie,
_temps_d'ouverture de_seconde_ride )
«» "

Le `max` gère le temps d'attente si le deuxième tour n'est pas encore ouvert.

Donc nous pouvons:

1. Précalculer `minLandFinish` et `minWaterFinish` dans **O(n+m)**.
2. Pour chaque conduite d'eau calculez le temps d'arrivée pour la commande *Land→Water*.
3. Pour chaque trajet terrestre calculez le temps d'arrivée pour la commande *Eau→Land*.
4. La réponse est le minimum de tous ces candidats – toujours **O(n+m)**.

Aucun tri ou recherche binaire n'est nécessaire – scans linéaires purs.
Cette perspicacité gourmande nous donne une solution spatiale **O(n+m)**, **O(1)**.

---

- Oui. 3. Le Code – 3 langues

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int le plus tôtFinishTime(
int[] landStartTime, int[] landDurée,
int[] eauDémarrage, int[] eauDurée) {

int minLandFinish = entier.MAX_VALUE;
pour (int i = 0; i < landStartTime.longueur; i++) {
minLandFinish = Math.min(minLandFinish,
landStartTime[i] + landDurée[i];
}

int minWaterFinish = entier.MAX_VALUE;
pour (int i = 0; i < waterStartTime.longueur; i++) {
minWaterFinish = Math.min(minWaterFinish,
eauDémarrage[i] + eauDurée[i];
}

réponse int = entier. MAX_VALEUR;

/* Terrains d'abord → Eau de seconde */
pour (int j = 0; j < waterStartTime.longueur; j++) {
finition int = eauDurée[j] + Math.max(minLandFinish,
l'eauDémarrage[j]);
réponse = Math.min (réponse, fin);
}

/* Eau d'abord → Land second */
pour (int i = 0; i < landStartTime.longueur; i++) {
finition int = terrainDurée[i] + Math.max(minWaterFinish,
landStartTime[i];
réponse = Math.min (réponse, fin);
}

réponse de retour;
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def le plus tôtFinishTime(
soi-même,
terre Heure de démarrage: Liste[int],
LandDuration: Liste[int],
eau Heure de démarrage: Liste[int],
eauDurée: Liste[int]
-> Int:
min_land_finish = min(l + d pour l, d en zip(landStartTime, landDuration)
min_water_finish = min(w + d pour w, d dans zip(waterStartTime, waterDuration))

ans = flotteur('inf')

# Terre première → Eau seconde
pour w, d en zip(eauDémarrage, eauDurée):
finition = d + max(min_land_finish, w)
ans = min(ans, finition)

# Eau d'abord → Land second
pour l, d en zip(landStartTime, landDurée):
fini = d + max(min_water_finish, l)
ans = min(ans, finition)

retour et
«» "

---

#### 3.3 C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>
#incluez <limites>

solution de classe {
public:
int le plus tôtFinishTime(
std::vector<int>& landStartTime,
Durée,
à:vector<int>&waterStartTime,
std::vector<int>&waterDurée) {

int minLandFinish = INT_MAX;
pour (size_t i = 0; i < landStartTime.size(); ++i)
minLandfinish = md:min(minLandfinish,
landStartTime[i] + landDurée[i];

int minWaterFinish = INT_MAX;
pour (size_t j = 0; j < waterStartTime.size(); ++j)
minWaterFinish = md::min(minWaterFinish,
eauDémarrage[j] + eauDurée[j]);

int ans = INT_MAX;

// Terrain premier → Eau deuxième
pour (size_t j = 0; j < waterStartTime.size(); ++j) {
fini int = eauDurée[j] +
à:max(minLandFinish, eauDémarrage[j]);
ans = md::min(ans, finition);
}

// Eau d'abord → Land second
pour (size_t i = 0; i < landStartTime.size(); ++i) {
finition int = terrainDurée[i] +
md:max(minWaterFinish, landStartTime[i]);
ans = md::min(ans, finition);
}

le retour des an;
}
};
«» "

---

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais

> **Référencement optimal :**
> *Temps d'arrivée le plus rapide pour les trajets terrestres et aquatiques II – Un problème d'entrevue pratique (Java, Python, C++)*

---

4.1 Introduction

Les intervieweurs aiment les problèmes qui testent le raisonnement avide, le code de passage de réseau et propre.
C'est un défi de LeetCode qui fait exactement cela.

Dans ce billet, nous passons par:

1. Compréhension des problèmes & contraintes
2. L'intuition gourmande qui transforme une tâche combinatoire apparemment complexe en un balayage **O(n+m)**
3. Une solution complète en Java, Python et C++
4. Les pièges communs (le "Bad") et comment les éviter
5. Extensions que vous pouvez discuter pour montrer la profondeur (le "Ugly")

À la fin, vous aurez une référence *prête à coller* pour chaque langue et un point de conversation qui démontre votre capacité à simplifier dans des délais serrés.

---

4.2 Récapitulation des problèmes (bon)

- **Ce que vous devez choisir:** exactement une terre et un tour d'eau.
- **La commande n'a pas d'importance** – vous pouvez choisir d'abord.
- **Grandes entrées**: 50 000 tours par catégorie → nous avons besoin de temps linéaire.

---

##### 4.3 Pourquoi l'approche naïve fails (Bad)

Une première tentative naturelle est :

Texte
pour chaque trajet
pour chaque balade en eau
Essayez les deux ordres
«» "

Ce serait **O(n·m)**, beaucoup trop lent pour 5 × 104 tours par catégorie.
Les intervieweurs vont rapidement repérer le bluff quadratique et s'attendre à ce que vous trouviez une meilleure stratégie.

---

4.4 Le point de vue sur l'avidité (bon)

- **Connaissance clé :** le temps final de la première catégorie* est indépendant de celui que vous prendrez plus tard.
- Calculer la *finition la plus ancienne* de la première catégorie une fois (`minLandFinish`, `minWaterFinish`).
- Pour la deuxième catégorie, le temps d'arrivée devient une formule simple utilisant `max` pour l'attente.
- Scanner tous les tours de la deuxième catégorie → mettre à jour le minimum mondial.

Tout cela est **one pass** par tableau – pas de tri, pas de tas, pas de recherche binaire.

> **Pourquoi c'est super pour les interviews* *
> *Scans linéaires* montrent que vous pouvez identifier le vrai goulot d'étranglement.
> *Le raisonnement génétique* vous démontre que vous n'êtes pas une force brute, mais plutôt l'exploitation de la structure du problème.
> *Clean code* (noms variables, boucles séparées pour chaque commande) affiche la maintenance.

---

4.5 Cas de bord et codage défensif

- **Single ride** par catégorie: notre formule fonctionne toujours parce que `min()` sur un élément est très bien.
- **Grandes sommes entières**: "startTime + durée" peut atteindre 200 000, toujours à l'intérieur de l'int signée 32 bits.
- **Initialisation des réponses** : utiliser `Integer. MAX_VALUE` (Java), `INT_MAX` (C++), ou `float('inf')` (Python).

---

##### 4.6 – Des choses que les intervieweurs pourraient demander

1. ** Pouvons-nous le résoudre en place? * *
*Oui – la solution ci-dessus n'utilise qu'un espace supplémentaire constant. *

2. **Et si les tableaux n'étaient pas triés? **
*Aucun impact – nous ne faisons que des scans linéaires. *

3. **Et plus de deux catégories? * *
*La même idée se généralise : garder le temps minimal de finition de la première catégorie, itérer sur le reste. *

4. **Proof d'optimalité** – vous pouvez donner un bref argument:
*Avec une commande, choisir le premier tour avec le plus petit temps d'arrivée ne peut pas retarder le deuxième tour, car l'attente est permise. *

5. **Alternative optimisée pour l'espace** – utiliser le streaming (java 8 flux, générateurs de Python).

Les intervieweurs peuvent tester votre capacité à **prouver** pourquoi le choix avide est optimal; être prêts à articuler que l'expression `max` modèle exactement le temps d'attente et que le choix d'une arrivée plus tard pour le premier tour ne peut jamais aider le deuxième tour.

---

#### 4.7 Prise- Liste de contrôle pour l ' éloignement

• Comprendre la décision en deux étapes (commande + trajet spécifique).
- Pré-calculer `minLandFinish` et `minWaterFinish`.
- - Scanner l'autre catégorie et calculer le temps de finition en utilisant "max".
- Gardez le minimum mondial.
- Écrire un code propre, auto-documentant (noms de variables clairs, commentaires).
- C'est la complexité du temps : **O(n+m)**, La complexité spatiale: **O(1)**.

---

4.8 Comment cela vous aide à être embauché

* Les intervieweurs veulent des candidats qui peuvent :
- Réduire une explosion combinatoire à un balayage linéaire.
- Raison de l'attente d'une opération "max".
- Produire un code propre, langue-agnostique.

* Afficher cette solution sur votre GitHub, inclure la discussion ci-dessus, et taper votre profil avec `Java`, `Python`, `C++`, `LeetCode`, `Greedy`, `Array`.

> **Mots clés**: temps d'arrivée le plus tôt, trajets à terre, trajets à l'eau, algorithme avide, problème d'entrevue, LeetCode moyen, Java coding interview, Python interview, C++ interview.

---

##### 4.9 TL;DR

«» "
1 Calculer la première finition de la première catégorie
Autres Pour chaque trajet de la deuxième catégorie :
Finale = durée + max( premier_finish_de_première, heure d'ouverture)
Autres Répéter pour les deux commandes et prendre le minimum global
«» "

> **Heure:** O(n+m)
> **Espace:** O(1)

Bon codage, et que votre prochaine interview se sente comme une balade en douceur! (en milliers de dollars)

---



- Oui. 5. Essai rapide – Entrées d'échantillons

Contribution attendue
C'est pas vrai.
"LandStartTime=[1,2,4]`<br>`LandDuration=[5,4,2]`<br>`waterStartTime=[3,5,1]`<br>`waterDurée=[6,3,4]`"
"LandStartTime=[5]`<br>`LandDurée=[5]`<br>`waterStartTime=[1]`<br>`waterDurée=[1]`

Exécutez l'un des extraits ci-dessus dans votre IDE préféré pour vérifier.

---

- Oui. 6. Mot final

Ce problème est une excellente vitrine pour:

- *Algorithmes cupides linéaires*
- *Claire, code à maintenir*
- *Mauvaise maîtrise de la langue*

Ajoutez l'implémentation de référence à votre feuille de triche personnelle et vous aurez un point de discussion solide pour toute entrevue technique. Bonne chance ! C'est ce qu'il a dit