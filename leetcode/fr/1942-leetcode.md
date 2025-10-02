---
titre: LeetCode 1942. Le nombre de la plus petite chaise inoccupée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
En 1942. Le nombre de la plus petite chaise inoccupée – Solution dans **Java, Python & C++* *

Ci-dessous vous trouverez une mise en œuvre propre et prête à la production du classique LeetCode, le plus petit problème de chaise inoccupée, en trois langues.
Toutes les solutions utilisent **deux files d'attente prioritaires** – une pour les chaises disponibles et une pour les chaises occupées triées par heure de départ – donnant un **O(n log n)** temps et **O(n)** complexité de l'espace.

---

Récapitulation du problème

> Vous êtes à une fête avec **n** amis (0-based index).
> Il y a infiniment beaucoup de chaises numérotées 0...
> Quand un ami arrive, il prend la chaise la plus petite.
> Quand un ami quitte la chaise devient immédiatement libre et peut être pris par quelqu'un arrivant en même temps.
> `temps[i] = [arrivée_i, départ_i]` (les heures d'arrivée sont distinctes).
> Remettez le numéro de chaise que **cibleAmi** occupera.

---

- Oui. 1. Python 3 – 9 lignes (deux tas)

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def le plus petit Président(e, heures: Liste[Liste[int]], cibleAmis: int) -> Int:
N° 1 Trier les amis par heure d'arrivée
ordre = trié(range(len(times), clé=lambda i: times[i][0])

N° 2 Taille de chaises libres (initialement 0...n-1), taille de chaises occupées (départ, siège)
libre, occupé = list(range(len(times)), []

pour idx dans l'ordre:
arriver, laisser = temps[idx]

N° 3 Relâche toutes les chaises dont le propriétaire est parti à l'heure d'arrivée
pendant qu'ils sont occupés[0][0] <= arrivent:
heapq.heappush(libre, heapq.heappop(occupé)[1])

N° 4 Prenez la plus petite chaise libre
chaise = heapq.heappop(libre)

Si idx == cible Ami : J'ai trouvé la réponse
fauteuil de retour

N° 5 Marquez le fauteuil occupé jusqu'à ce qu'il quitte '
heapq.heappush(occupé, (à gauche, chaise))
«» "

**Pourquoi ça marche* *
- Oui. Le tas `gratuit` contient toujours toutes les chaises qui sont actuellement vides.
- Oui. Le tas "occupé" est trié par heure de départ; l'élément supérieur est la chaise qui libérera le plus tôt.
- Oui. En surgissant à plusieurs reprises de `occupé` quand son heure de départ ≤ arrivée actuelle, nous gardons `free` à jour.
- Oui. La plus petite chaise libre est toujours en haut de `free`, donc nous pouvons l'assigner dans O(log n).

---

- Oui. 2. Java – `PriorityQueue` version

"Java
Importation de java.util.*;

solution de classe {
publique Président(int[][] times, int cibleAmis) {
int n = durée;

Classer les indices amis par heure d'arrivée
Ordre entier[] = nouvel ordre entier[n];
pour (int i = 0; i < n; i++) ordre[i] = i;
Arrays.sort(ordre, Comparator.comparingInt(i -> times[i][0]);

// 2.
Priorité Queue<integer> gratuit = nouveau PriorityQueue<>();
pour (int i = 0; i < n; i++) free.offre(i);

// 3.-Levure de chaises occupées: paire (départ, siège)
PrioritéQueue<int[]> occupé = nouveau PriorityQueue<>(Comparator.comparingInt(a -> a[0]);

pour (int idx : ordre) {
int arrive = times[idx][0];
inter leave = times[idx][1];

// 4 Chaises de relâche dont le propriétaire est parti
pendant que (!occupée.isEmpty() &&occupée.peek()[0] <= arrive) {
libre.offre(occupée.poll()[1]);
}

// Prenez la plus petite chaise libre
chaise int = free.poll();

si (idx) cibleAmi) retour de la chaise;

// 6/ Mark chaise comme occupé jusqu'à 'départ '
occupation.offre(nouvelle int[]{leave, chaise});
}
retour -1; // inaccessible – cible de garantie d'entrée Un ami existe
}
}
«» "

---

- Oui. 3. C++ – `priority_queue` + `vecteur "

'`cpp
#incluez <vecteur>
#incluez <queue>
#incluez <algorithme>

solution de classe {
public:
int plus petite Président(e):vector<std:vector<int>>& times, int cibleAmi) {
int n = times.size();

Indices de commande par heure d'arrivée
point::vecteur<int> ordre(n);
à: iota(order.degin(), order.end(), 0);
à:sort(order.begin(), order.end(),
[&](int a, int b){ temps de retour[a][0] < temps[b][0]; });

// 2.
std::priority_queue<int, std::vector<int>, std::plus grand<int>> libre;
pour (int i = 0; i < n; ++i) push(i);

// 3.-Levure de chaises occupées: paire (départ, siège)
std::priority_queue<
À l'intérieur de l'Union européenne
L'annexe I est modifiée comme suit:
À l'intérieur de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition de l'aire de répartition
> occupé;

pour (int idx : ordre) {
int arrive = times[idx][0];
inter leave = times[idx][1];

// 4 Libérez toutes les chaises dont le propriétaire est déjà parti
pendant que (!occuped.vide() &&occuped.top().first <= arrive) {
libre.push(occupé.top().seconde);
occupé.pop();
}

// 5.
chaise int = free.top(); free.pop();

si (idx) cibleAmi) retour de la chaise;

Le siège de Mark est occupé jusqu'à son départ. '
occupé.emplace (leave, chaise);
}
retour -1; // ne devrait jamais arriver
}
};
«» "

---

Pourquoi ces solutions obtiennent des entrevues

Aspect Python Java C++
C'est pas vrai.
**Readability**
**Complexité du temps**= O(n log n)= O(n log n)= O(n log n)=
Autres **Complexité de l'espace**
Deux files d'attente prioritaires : libre et occupé
Autres **Cas d'escroquerie manipulés**

---

Aperçu de l'article du SEO

> **Titre**: Code Leet 1942 – La plus petite chaise inoccupée : une plongée profonde dans des solutions à deux niveaux (Java, Python & C++)

---

Introduction
- Crochet : Imaginez une fête où chaque nouvel invité doit s'asseoir sur la chaise vide la plus petite. Comment faites-vous pour suivre l'alignement de la chaise qui change constamment? (en milliers de dollars)
- Indiquer le problème, le lien avec LeetCode, mentionner les contraintes (n ≤ 104).
- Mots-clés du référencement : *LeetCode 1942*, *Petite chaise inoccupée*, *Question d'entrevue*, *Deux Heaps*, *Priority Queue*, *Java*, *Python*, *C++*.

#### 2-
- Schéma visuel des arrivées et des départs.
- Clarify chaise devient libre instantanément et les temps d'arrivée sont distincts.
- Oui. Pourquoi une simulation naïve (array de chaises) est O(n2) et peu pratique.

C'est vrai. Approches naïves et optimales
Défauts de complexité
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Brute Force Array, O(n2)
Événements triés + TreeSet O(n log n)
Deux Heaps (recommandés)

C'est pas vrai. La stratégie à deux niveaux (les bonnes)
- **Chaussure de chaise gratuite**: tient toujours la plus petite chaise disponible.
- **Chair Heap** occupé: trié par heure de départ.
- Logique de sortie: pop de occupé pendant le départ ≤ arrivée actuelle → poussez la chaise à nouveau libre.
- Affectation : faire sauter le haut de libre, pousser dans occupé avec son départ.
- Arrêtez-vous tôt quand l'ami cible est assis.

#### Code Walk-through (Python)
- Explication étape par étape avec commentaires en ligne (la solution 9 lignes).
- Mettre en évidence la boucle `while` qui libère les chaises.
- Montrez comment la sortie anticipée sauve.

C'est vrai. Traduire en Java & C++ (L'Ugly)
- Discutez des problèmes linguistiques :
- Java `PriorityQuie` est un min-heap par défaut? (Non, il s'agit d'un peu de poids mais il a besoin d'un comparateur).
- C++ `priority_queue` est max‐by‐default → utiliser `plus grand<...>` comparateur.
- Montrez comment stocker les paires (départ, chaise) en toute sécurité.
- Pièges communs : oubli de «pop» après «peek», erreurs hors-par-un dans les indices.

#### 6- Liste de contrôle des cas (Les méchants)
Qu'est-ce qu'il faut regarder
-- -- -- -- -- -- -- -- --
L'ami cible arrive en dernier. Autres
Plusieurs départs à la même heure. Autres
Le temps d'arrivée est égal au départ précédent. Autres
Autres Très grand n (104). Autres

- Oui. Conseils pour le réglage des performances
- Utiliser `heapq`=s `heappush`/`heappop` (Python) – pas besoin de `poush/pop` manuel.
- En Java, pré-remplissez le tas libre avec `IntStream.range(0, n). forEach(free::offer)` pour la lisibilité.
- Dans C++, utilisez `std::vector<int>` pour le tas gratuit si vous voulez éviter `poush/pop` pour les premiers éléments n.

Variations et extensions
- Oui. Et si les temps d'arrivée n'étaient pas distincts ? Ajoutez une règle d'égalité (p. ex., carte d'identité de l'ami).
- Oui. Comment géreriez-vous un nombre fini de chaises ? Utilisez un compteur pour le cas de la chaise disponible.
- Utilisez un arborescence segmentaire ou un arborescence binaire indexée pour des requêtes de portée minimale si vous voulez pratiquer différentes structures de données.

Conclusion et conclusion de la sortie
- Résumez pourquoi la solution à deux fois est le *spot sucré* pour LeetCode 1942.
- Encourager les lecteurs à pratiquer en implémentant les trois versions, test contre les entrées aléatoires (`unittest` / JUnit / Google Test).
- Invitez les commentaires : -Quels autres problèmes d'entrevue rencontrez-vous ? (en milliers de dollars)

Ressources supplémentaires
- Lien vers les fils de discussion de la solution LeetCode.
- Repo GitHub avec les trois implémentations.
- Visite vidéo sur YouTube pour les apprenants visuels.

---

La pensée finale

Avec ces **trois implémentations concises et efficaces** et l'explication ** structurée prête à l'entrevue**, vous serez en mesure de s'attaquer avec confiance au LeetCode 1942 et impressionner les intervieweurs avec rapidité et clarté. Bon codage !

---

> * Sentez-vous libre de déposer des questions dans les commentaires – laissez-les faire que chaque nouvel invité se sent juste à la maison! *