---
titre: LeetCode 2365. Calendrier des tâches II –
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Voici trois solutions **complètes, copie et pâte** pour LeetCode 2365 – *Tâche Annexe II*.
Tous les trois suivent la même idée de "next-available-day" et courent dans **O(n)** time avec **O(n)** espace supplémentaire.

Langue Structure des données clés Complexité
- C'est quoi ?
Java, "HashMap<entier, Long>, "O(n)" espace
(Python 3.6+) espace
"Temps "O(n)", "O(n)" espace

> **Astuce** – Utilisez un `long` / `long` pour le compteur de jour parce que la réponse peut dépasser `int` gamme (`tasks.longueur ≤ 105`, `espace ≤ 105`).

---

### Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
***
* LeetCode 2365 – Planificateur des tâches II
*
* Gamme de tâches @param des types de tâches
* @param espace minimum de jours avant que le même type puisse être exécuté à nouveau
* @retour minimum de jours pour terminer toutes les tâches
*/
travail public longSchedulerII(int[] tâches, espace int) {
Carte<entier, long> nextDisponible = nouveau HashMap<>();
longs jours = 0L; // jours écoulés

pour (int t : tâches) {
// Le jour actuel peut être au maximum:
// * le lendemain après la tâche précédente (jours + 1)
// * le jour où ce type de tâche est à nouveau autorisé
jours = Math.max(suivantDisponible.getOrDefault(t, 0L), jours + 1);

// Après avoir fait cette tâche, la prochaine fois que nous pouvons exécuter type `t`
// est "jours + espace + 1".
suivantDisponible.put(t, jours + espace + 1);
}
les jours de retour;
}
}
«» "

---

Python 3

'`python
de taper l'importation Liste

Solution de classe:
def taskSchedulerII(self, tasks: List[int], espace: int) -> Int:
"""
LeetCode 2365 – Planificateur des tâches II
"""
next_available = {} # type de tâche -> Le plus tôt possible, on peut le refaire.
jours = 0 nombre de jours écoulés

pour t dans les tâches:
jours = max(next_available.get(t, 0), jours + 1)
next_available[t] = jours + espace + 1

Jours de retour
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue tâcheSchedulerII(vecteur<int>&tâches, espace int) {
non ordonné_map<int, long> suivant; // type de tâche -> Le plus tôt possible, on peut le refaire.
longs jours = 0; // jours écoulés

pour (int t : tâches) {
jours = max(next[t], jours + 1);
suivant[t] = jours + espace + 1;
}
les jours de retour;
}
};
«» "

> **Rappel** : compilez avec `-std=c++17` (ou plus tard) et liez la bibliothèque standard.

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 2365

> **Concentrement des mots clés**: *Planificateur des tâches de LeetCode II*, *algorithme de planification des tâches*, *solution Java HashMap*, *solution du dictionnaire Python*, *solution C++_map non ordonnée*, *algorithme O(n)*, *conseils d'entretien d'emploi*, *entretien d'ingénierie de logiciels*, *entretien de conception de systèmes*, *questions d'entretien de LeetCode*

---

2.1 Introduction

Si vous préparez une entrevue d'ingénierie logicielle, vous avez probablement vu **LeetCode 2365 – -Task Planificateur II** dans la trousse de préparation d'entretien.
A première vue, il ressemble à un simple problème de simulation, mais il est une grande vitrine de:

- ** Pensée grêle**: - Faites la tâche suivante ou sautez si elle viole le cooldown.
- **Astuces de plan de vol** : suivre les jours *prochains-disponibles* pour chaque type de tâche.
- **Manipulation des cas** : grandes entrées, valeurs d'espace élevées et tâches minimales.

Dans cet article, nous disséquerons le problème, présenterons la solution la plus rapide** connue, explorerons les pièges communs et terminerons par des points d'entrevue.

---

2.2 Récapitulation du problème

Vous avez reçu :

Sens de l'entrée
C'est quoi ?
Chaque élément est un *type* de tâche (pas l'ordre d'exécution). Autres
« espace » – « int » – nombre minimum de **jours** qui doivent passer après avoir accompli une tâche d'un type donné avant que le même type puisse être exécuté à nouveau. Autres

Chaque jour, vous pouvez:

1. Exécuter la tâche suivante dans la liste, *si la règle de cooldown le permet.
2. Faites une pause (ne rien faire).

Retournez le nombre **minimum** de jours nécessaires pour terminer le tableau entier des "tâches".

---

### 2.3 Le bon – La simulation directe vers l'avant

Une solution naïve imite jour après jour, vérifie le refroidissement pour la tâche actuelle, et soit l'exécute ou casse.
complexité du temps: **O(total jours)**, qui peut être jusqu'à "O(n) espace)" (C'est le pire cas : 105 * 105 = 1010).
Mémoire : **O(n)** pour le suivi du dernier jour d'exécution de chaque type.

Cette approche est conceptuellement facile, mais *faux* sur les limites supérieures des contraintes. Sur LeetCode il obtient **Time‐Limit‐Excéded**.

> **À emporter**: Évitez la simulation explicite du jour lorsque l'espace peut être énorme. Nous avons besoin d'un mécanisme rapide.

---

### 2.4 La bonne solution – La carte Hash

2.4.1 Aperçu

Au lieu de se souvenir de *quand* vous avez lancé un type pour la dernière fois, rappelez-vous **quand** vous êtes *autorisé* à l'exécuter à nouveau.
Appelez cette valeur `nextDisponible[type]`.

Lorsque vous rencontrez une tâche de type `t` le jour `jours`:

- Si `jour + 1` est plus tard ou égal à `nextDisponible[t]`, vous pouvez l'exécuter.
- Sinon vous *doivez* attendre jusqu'à "nextDisponible[t]".
La seule façon efficace de le faire est de faire face directement à ce jour.

##### 2.4.2 Greedy Étape par étape

1. **Initialiser** « jours = 0 » (aucun jour n'a encore été passé).
2. Pour chaque tâche « non » dans « tâches » :
- `jours = max(nextDisponible.get(t, 0), jours + 1);`
- Après la finition, set `nextDisponible[t] = jours + espace + 1;`
3. Retour "jours".

La magie est le `max()` appel: il garantit que nous ne *diminuer* jamais le compteur de jour, de sorte que l'algorithme respecte toujours l'ordre de tâche original.

2.4.3 Pourquoi c'est O(n)

Nous visitons chaque tâche exactement une fois.
Toutes les opérations sur un `HashMap` / `dict` / `unordered_map` sont amorties **O(1)**.
Par conséquent, le temps total = `O(n)` (n ≤ 105).
Espace = `O(k)`, où *k* est le nombre de types de tâches distincts (= n).

C'est l'algorithme **fast** accepté sur LeetCode et est généralement la solution *attendue* dans les interviews.

---

### 2.5 L'erreur commune qui envoie la réponse

Erreurs dans les résultats
- C'est quoi ?
Utiliser un `int` pour le compteur de jour.
Autres Oubliant le `+1` dans `jours + espace + 1`- Le même type peut fonctionner trop tôt (viole la règle) - Ajoutez toujours le `+1` pour le *jour* vous exécuterez effectivement la tâche -
Hors-par-un dans la boucle ('jours + 1' vs. 'jours') Il donne 1 jour de moins ou plus. Clarifiez que `jour` compte *complète* jours, donc le premier jour est `1` (ou vous pouvez commencer par `0` et retourner `jour`). Autres
Autres Pas d'initialisation des clés manquantes. Autres
Autres Traiter l'espace comme des jours "cool-down" au lieu de "days" que *must* pass" , formule incorrecte , "nextDisponible[t] = courantJour + espace + 1". Autres

---

#### 2.6 Les variantes et les extensions

LeetCode fournit souvent des questions *hard* de suivi. Pour 2365 vous pourriez rencontrer:

- ** Travailleurs multiples** : Chaque travailleur peut traiter *une* tâche par jour. Comment change l'algorithme ? (Réponse : toujours O(n) en utilisant un poids minimal par type.)
- **Tâches prioritaires** : Certains types sont plus importants et devraient être programmés plus tôt.
Vous pouvez ajouter une file d'attente prioritaire qui affiche le *cheapest* le jour suivant.
- **Different units**: Au lieu de jours, on pourrait vous dire : heures ou minutes. La solution reste identique ; il suffit de renommer la variable.

> **Pourquoi parler de variantes?** Les intervieweurs aiment vous voir penser au-delà de la déclaration exacte.

---

2.7 Entretien— Points de discussion prêts

Lorsque l'intervieweur demande la solution:

1. **Énoncer l'approche**: -Je garde une carte de hachage du lendemain chaque type de tâche est à nouveau autorisé. Pour chaque tâche, je saute à la fin de la journée en cours ou à la prochaine journée disponible. (en milliers de dollars)
2. **Expliquez la preuve gourmande**: Parce que nous accomplissons toujours une tâche dès qu'elle est permise, nous ne pouvons pas améliorer le calendrier en la reportant. (en milliers de dollars)
3. **Complexité des mentions**: temps O(n), espace O(k), ce qui est optimal étant donné que nous devons examiner chaque tâche au moins une fois. (en milliers de dollars)
4. ** Mettre en évidence la sécurité du boîtier de bord**: -J'ai utilisé "long" pour éviter le débordement. J'ai géré correctement les tableaux vides et `espace = 0`. (en milliers de dollars)
5. **Extension facultative**: Si nous avions plusieurs travailleurs, nous pourrions utiliser une file d'attente prioritaire par type au lieu d'une carte simple. (en milliers de dollars)

> **Pourquoi cela compte**: LeetCode 2365 est *pas seulement sur les tableaux; il teste votre capacité à penser en termes de *états* (cool-down) et de *bondage* (fast-forward). Montrer ce raisonnement impressionnera les intervieweurs à la recherche d'une solution propre et évolutive.

---

Conseils pratiques pour la chasse à l'emploi

Pourquoi ça aide ?
C'est pas vrai.
** Pratique avec grand- Les intervieweurs veulent que vous justifiiez pourquoi une solution est assez rapide. Autres
**Écrire le code d'abord, puis copier-coller**. Autres
**Expliquez à haute voix votre processus de pensée** Autres
Autres **Inclure les tests de cas de bord**. Autres
**Lien avec votre repo GitHub**Les recruteurs apprécient une base de code propre et documentée. Autres

> *Tip Pro*: Lorsque vous affichez votre solution sur votre CV ou LinkedIn, marquez le problème. Les recruteurs qui analysent votre curriculum vitae repèreront ce mot-clé instantanément.

---

2.9 Mot final

LeetCode 2365 est un puzzle d'entrevue *classique* qui combine une stratégie gourmande avec la comptabilité de hash-map.
La solution **fast** est étonnamment courte — seulement quelques lignes de Java, Python ou C++ — mais elle contient une profonde perspicacité algorithmique.

Utilisez ce problème comme une vitrine sur votre CV ou dans une entrevue technique :
J'ai transformé une simulation naïve qui prendrait des années en solution linéaire avec une carte de hachage simple. *

Bon codage, et que vos journées d'entrevue soient gratuites! C'est ce qu'il a dit.

---

> ** Prêt à plonger plus profondément?** Consultez la discussion officielle du LeetCode, ou essayez le suivi le plus difficile.