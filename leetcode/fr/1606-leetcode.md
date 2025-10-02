---
titre: LeetCode 1606. Trouver des serveurs qui ont géré la plupart des demandes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## *D'un problème à une pièce de portefeuille – Trouver des serveurs qui ont géré la plupart des demandes * *
*(Code de bord 1606 – Hard)*

> **Mots clés:**
> `Leetcode 1606`-Les serveurs les plus occupés`- `TreeSet`- `PriorityQueue`- `Java`- `Python`- `C++`- `O(n log k)`- "

---

Récapitulation des problèmes

Vous avez des serveurs **k** (numérotés 0 ... k‐1) qui peuvent gérer au plus une requête à la fois.
Pour chaque demande *i* (`arrivée[i]`, `charge[i]`):

1. Si **all** serveurs sont occupés → laisser tomber la requête.
2. Essayez de l'assigner au serveur `(i % k)`.
3. Si ce serveur est occupé, faites une recherche (enroulement) pour le prochain disponible.

Votre tâche : après toutes les requêtes, retournez les identifiants du(des) serveur(s) *busest* – celui(s) qui a(ont) traité le plus de requêtes.

---

Intuition – Le -Robin rond + Free-up Jeu

* **Free-up** – Un serveur occupé devient libre lorsque `arrival_time ≥final_time`.
* **Recherche ronde** – Nous commençons toujours la recherche à partir de `(i % k)`; une fois que nous avons atteint la fin de la liste, nous enroulons au début.
* ** Structures de données** qui nous permettent de faire les deux efficacement:

Opération Requise Structure des données
- C'est quoi ?
Autres Trouvez le plus petit serveur ≥ x (ou enveloppez vers le plus petit)
Autres Gardez les serveurs occupés triés par le temps de finition.

---

Algorithme en Pseudocode

«» "
disponible = set(0 ... k-1) // tous les serveurs démarrent gratuitement
occupé = min‐heap() // (finish_time, server_id)
cnt = tableau[k] // nombre de requêtes traitées par serveur

pour i = 0 ... n-1
// 1. Relâche tous les serveurs qui ont terminé avant l'arrivée actuelle
tout en étant occupé pas vide et occupé. peek().finish_time <= arrivée[i]
finish_time, server_id = occupé.pop()
disponible.insert(server_id)

si disponible est vide
continue // demande abandonnée

// 2. Trouver le premier serveur disponible ≥ i % k
cible = disponible. plafond(i % k)
si la cible est nulle
cible = disponible.first() //

// 3. Attribution
disponible.supprimer(cible)
buse.push( (arrivée[i] + charge[i], cible) )
cnt[cible] += 1

max_cnt = max(cnt)
liste de retour des indices j où cnt[j] == max_cnt
«» "

complexité du temps : **O(n log k)** (chaque requête fait un nombre constant d'opérations de jeu/pap).
complexité spatiale: **O(k)**.

---

Code – trois langues

Ci-dessous sont des extraits de production prêts à compiler avec les derniers compilateurs / interprètes.

---

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe {
liste publique<entier>serveurs les plus occupés(int k, int[] arrivée, int[] charge) {
int n = arrivée. longueur;

// Serveurs disponibles – triés
TreeSet<Integer> disponible = nouveau TreeSet<>();
pour (int i = 0; i < k; i++) disponible.add(i);

// Serveurs occupés – min-heap commandé par le temps de finition
PrioritéQueue<int[]> occupé = nouvelle prioritéQueue<>(Comparator.comparingInt(a -> a[0]);

int[] count = nouveau int[k];

pour (int i = 0; i < n; i++) {
heure int = arrivée[i];
int dur = charge[i];

// Serveurs de sortie terminés
pendant que (!busy.isEmpty() &&occupée.peek()[0] <= heure) {
int[] fini = occupé.poll();
disponible.add(fini[1]); // server_id
}

si (disponible.isEmpty()) continue; // demande abandonnée

// Trouver un serveur à assigner
Cible entière = disponible. plafond(i % k);
si (cible == null) cible = disponible.first(); // wrap

// Assigner
disponible.supprimer(cible);
occupé.offre(nouvelle int[]{temps + durée, cible});
count[cible]++;
}

// Trouver le maximum
= 0;
pour (int c : nombre) max = Math.max (max, c);

Liste du résultat <entier> = nouvelle liste de distribution<>();
pour (int i = 0; i < k; i++)
si (compte[i] == max) résultat.add(i);

le résultat du retour;
}
}
«» "

---

# # # # # #

'`python
bisect d'importation
importation heapq
de taper l'importation Liste

Solution de classe:
les plus occupés Serveurs(self, k: int, arrivée: List[int], charge: List[int]) -> Liste[int]:
n = len(arrivée)

# Liste triée des serveurs libres
gratuit = list(range(k))
# Min-heap de (finish_time, server_id)
occupé = []

Nombre = [0] * k

pour i dans la plage(n):
t, d = arrivée[i], charge[i]

# Release des serveurs terminés
tout en étant occupé[0][0] <= t:
fini, sid = heapq.heappop(busy)
bisect.insort(libre, sid)

si non libre:
continuer # laissé tomber

# Trouver le premier serveur gratuit >= i % k
idx = bisect.bisect_left(libre, i % k)
Si idx == len(libre):
idx = 0 # enveloppe
Sid = libre.pop(idx)

# Assigner
heapq.heappush(en service, (t + d, sid))
Nombre[sid] += 1

max_cnt = max(compte)
retour [i pour i, c dans le dénombrement(compte) si c == max_cnt]
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> Serveurs les plus occupés(int k, vectorielle<int>& arrivée, vectorielle<int>& charge) {
int n = arrivée.size();
vecteur<int> cnt(k, 0);

// Tous les serveurs commencent gratuitement
set<int> free_servers;
pour (int i = 0; i < k; ++i) free_servers.insert(i);

// Min‐heap: paire<finish_time, server_id>
priority_queue<pair<long long,int>,
vecteur<pair<long long,int>>,
plus grande <pair<long long,int>>> occupés;

pour (int i = 0; i < n; ++i) {
long cur = arrivée[i];
longue durée = charge[i];

// Serveurs de sortie terminés
pendant que (!busy.vide() && occupé.top(). premier <= cur) {
int sid = occupé.top().seconde;
occupé.pop();
free_servers.insert(sid);
}

si (free_servers.vide()) continue; // est tombé

// Trouver un serveur à assigner
auto it = free_servers.lower_bound(i % k);
if (it == free_servers.end()) it = free_servers.begin(); // wrap
int sid = *it;
free_servers.erase(it);

// Assigner
occupé.emplace(cur + dur, sid);
++cnt[sid];
}

int mx = *max_element(cnt.begin(), cnt.end());
vecteur<int> rés;
pour (int i = 0; i < k; ++i)
si (cnt[i] == mx) res.push_back(i);
retour rés;
}
};
«» "

---

Récapitulation de la complexité

Métrique
- C'est quoi ?
**Heure**="O(n log k)="="O(n log k)="="O(n log k)=" Autres
**Mémoire** Autres
**Pourquoi log k?**= `TreeSet.ceiling / lower_bound`= `bisect_left` + `bisect.insort` "set.lower_bound" Autres

---

Bonne, mauvaise, mauvaise – Lentille d'entrevue

Aspect du bien
- C'est quoi ?
**Bon**Shows mastery of *ordered set* & *heap* – les deux agrafes dans les interviews de codage. Démonstration de la capacité de combiner Python, `bisect` + `heapq` sans libs externes. – propre, idiomatique C++. Autres
**Bad**.Éviter de libérer des serveurs avant que l'affectation n'entraîne de mauvais nombres (bogue commun). En utilisant une liste simple pour `free` (O(k)) au lieu d'une structure triée peut se dégrader en `O(nk)`. Le fait de négliger l'enroulement (`lower_bound`) donne lieu à des requêtes abandonnées incorrectement. Autres
Utiliser un `HashMap` pour simuler un ensemble trié – O(k) scanner chaque fois → `O(nk)`. En utilisant une `list` et `index()` pour la recherche – toujours `O(n log k)` mais avec des constantes élevées. Un tableau naïf de booléens + scan linéaire pour le prochain serveur libre – le pire cas de `O(nk)`. Autres

**Astuce:** Toujours *premier* **libérer** serveurs avant de rechercher; sinon vous allez garder -"busy" serveurs qui sont en fait libres, conduisant à plus de requêtes abandonnées que nécessaire.

---

## -- Interviews à emporter

1. **Afficher le combo de set-heap** – les intervieweurs adorent vous voir choisir la bonne structure de données pour chaque opération.
2. **Manipulation des caisses** – mention de ce qui se passe lorsque `k = 1`, lorsque toutes les charges sont énormes, ou lorsque `arrivée` temps sont égaux.
3. **Exposer la logique d'enroulement** – `lower_bound` + -if end → begin= est un truc qui peut être demandé dans un suivi.
4. **Discussion des solutions de remplacement** –
* Bucket‐array + pointeur suivant pour la recherche O(1) (mais toujours O(n)).
* Arbre indexé binaire / Fenwick si vous voulez maintenir le nombre de préfixes.
5. **Parler des parallèles du monde réel** – équilibrage de la charge, théorie de la file d'attente, planificateurs ronds.

---

Comment ce message vous aide à trouver un emploi

1. ** Preuve de portefeuille :** Intégrez l'extrait dans votre repo GitHub intitulé `Leetcode1606_BusestServers`.
2. **Blog + LinkedIn:** Écrire un court article (comme celui-ci) et le partager – recruteurs spot auteurs de blog qui discutent des algorithmes.
3. **Préparation de l'entrevue:** Utilisez le format "bon, mauvais, laid" pour discuter de la solution dans des interviews simulées; cela montre que vous pouvez *raison*, *debug* et *optimiser*.
4. **Questions complémentaires:** Soyez prêt à expliquer *pourquoi* un peu de poids est utilisé, *comment* vous géreriez `k = 10^5`, ou *quoi si* charges sont 0.
5. **Agilité linguistique de la vitrine:** Avoir le même algorithme en trois langues démontre la polyvalence – un point de vente fort pour les rôles multiplateforme ou multiplateforme.

---

Liste de contrôle finale

- Compile sur `javac 17`, `python3.10`, `g++ 17`.
- Il gère jusqu'à 10^5 requêtes et 10^5 serveurs.
- Temps "O(n log k)` – bien en dessous de la limite de 3 s Leetcode.
- Code propre, bien commenté – prêt pour la production ou la copie-colle d'entrevue.

---

Lire plus

- *Structures de données et algorithmes* par Goodrich, Tamassia et Goldwasser – chapitre sur `TreeSet` et `PriorityQuue`.
- *Cracking the Coding Interview* – Section sur les problèmes de file d'attente prioritaire + Set.
- *Leetcode Discuter – 1606* – regardez les vidéos des 3 meilleures solutions pour en savoir plus.

Bonne chance, et rappelez-vous: **Chaque entretien est une chance de montrer que vous connaissez le bon outil pour le travail**! Bon codage !