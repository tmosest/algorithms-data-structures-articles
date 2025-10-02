---
Titre: LeetCode 1244. Design A Leaderboard - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1244 – Conception d'un tableau de bord
**Java / Python / C++** – Des solutions complètes + un article de blog qui explique le bon, le mauvais et le mauvais de concevoir un classement.

---

Récapitulation des problèmes

Description
- C'est quoi ?
**Exploitations** Id, score)` – ajouter `score` au score actuel du joueur (créer si absent).<br>`top(K)` – retourner la somme des meilleurs scores `K`.<br>`reset(playerId)` – effacer le score du joueur. Autres
**Constraints**=1 ≤ playerId, K ≤ 10 000`<br>=1 ≤ score ≤ 100`<br>=1 000` total des appels de fonction. Autres
**Objectif**= Concevoir une structure de données qui supporte efficacement les opérations ci-dessus. Autres

---

- Oui. La partie supérieure de l'ajout/reset O(K)

La solution classique utilise une carte **hash** (`playerId → score`) plus un conteneur ** trié** qui conserve tous les scores dans l'ordre décroissant.

Langue Structure des données pour les scores triés Complexité
Il n'y a pas de problème.
(ou une liste personnalisée doublement liée)
Python `bisect.insort` sur une liste (O(N)) – assez bon pour les appels ≤ 1000.
* C++* "multiset<int, plus<int>>" "addScore`/`reset`: O(log N) <br> `top(K)`: O(K)

- Oui. Java – HashMap + TreeSet

"Java
Importation de java.util.*;

classe publique Leaderboard {

carte finale privée<entier, entier> scoreMap = nouveau HashMap<>();
finale privée TreeSet<entier> triéScores = nouveau TreeSet<>(Comparator.reverseOrder());

tableau de bord public() {}

public vide addScore(int player) Id, score int) {
int oldScore = scoreMap.getOrDefault(joueur Id, 0);
si (vieille note > 0) triéScores.supprimer(vieille note);
int newScore = ancien score + score;
scoreMap.put(joueur Id, NewScore);
triésScores.add(newScore);
}

haut de page (int K) {
= 0;
i = 0;
pour (int s : triés Valeurs {
i (i++ == K) rupture;
somme += s;
}
la somme de retour;
}

public vide réinitialiser(int player Id) {
int oldScore = scoreMap.remove(joueur Id);
si (vieille note > 0) triéScores.supprimer(vieille note);
}
}
«» "

### Python – Dictionnaire + Liste triée (bisect)

'`python
bisect d'importation
de collections importer par défautdict

classe Tableau de classement:
def _init_(self):
self.scores = defaultdict(int) # player Id -> score
self.sorted = [] # liste descendante des scores

def addScore(self, playerId: int, score: int) -> Aucun:
old = self.scores[joueur Id]
si ancien:
idx = bisect.bisect_left(self.sorted, old, key=lambda x: -x)
Self.sorted.pop(idx)
nouveau = ancien + score
self.scores[playerId] = nouveau
bisect.insort_left(self.sorted, new, key=lambda x: -x)

def top(self, K: int) -> Int:
somme de retour(self.sorted[:K])

def reset(self, playerId: int) -> Aucun:
vieux = self.scores.pop(joueur Id, 0)
si ancien:
idx = bisect.bisect_left(self.sorted, old, key=lambda x: -x)
Self.sorted.pop(idx)
«» "

> ** Pourquoi le bisect ? **
> La liste est triée dans l'ordre **descendant**, de sorte que `bisect_left` avec une clé de `-x` trouve l'index correct.

### C++ – Carte non commandée + Multiset

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe Tableau de classement {
unordered_map<int, int> mp; // player Id -> score
multiset<int, plus<int>> scores; // tous les scores, décroissants

public:
Tableau de classement() = par défaut;

vide addScore(int player) Id, score int) {
int old = mp.count(playerId) ? mp[playerId] : 0;
if (old) scores.erase(scores.find(old)); // remove old score
int nw = ancien + score;
mp[joueur Id] = nw;
scores.insert(nw);
}

dessus int(int K) {
= 0, cnt = 0;
pour (int s : scores) {
si (cnt++) K) pause;
somme += s;
}
la somme de retour;
}

réinitialiser le vide(int player Id) {
int old = mp[joueur Id];
scores.erase(scores.find(old));
mp.erase(playerId);
}
};
«» "

---

- Oui. Le "Bad" – Re-sort sur chaque "top"

Une approche naïve stocke tous les scores dans un vecteur et ** le trie sur chaque appel `top(K)`**.

"Java
Liste<Intégrer> tous = nouvelle liste de distribution<>();
// addScore: mise à jour de la carte, liste de reconstruction
// haut: Collections.sort(toutes, Collections.inverseCommander()); // O(N log N)
«» "

C'est *acceptable* pour les limites du problème (= 1000 appels), mais il **n'est pas échelle** – chaque "top" devient cher lorsque le classement augmente à des milliers ou des millions de joueurs.
**Éviter** cela dans des entretiens réels à moins que les contraintes le permettent explicitement.

---

- Oui. L'utilisation d'une file d'attente prioritaire sans support de mise à jour

Un petit tas de taille `K` semble attrayant, mais lorsqu'un joueur change de score, le tas ne reflète plus la bonne commande. On pourrait essayer de *supprimer paresseux* les entrées obsolètes, mais cela devient rapidement désordonné et sujet à erreur.

> **Ligne de bottom:** Un tas qui ne peut pas supprimer ou mettre à jour des éléments arbitraires est une recette pour les bogues et O(N) nettoyage des frais généraux.

---

C'est pas vrai. Aller Au-delà du bien – Options avancées

Option: Ce qu'il achète: Quand considérer:
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Fenwick / Binary Indexed Tree** (score → frequency)= Permet `top(K)` dans O(log M) où `M` est le score maximum possible (ici ≤ 106). Si vous avez besoin de **préfixer des sommes** de fréquences. Autres
**Segment Tree** Quand `score` peut être grand et vous avez besoin de requêtes de portée. Autres
**Binaire indexé Arbre de fréquences + dictionnaire**= Keeps `addScore`/`reset` O(log M), `top(K)` O(log M).== Pour des budgets de temps serrés avec de nombreuses opérations. Autres

> **Astuce:** Si vous êtes invité à implémenter une version de l'arborescence *Fenwick*, pensez d'abord à la cartographie `score → count` et comment vous avez obtenu la valeur k‐th la plus grande par recherche binaire sur les fréquences cumulatives.

---

C'est pas vrai. Points de discussion favorables aux intervieweurs

Thème Pourquoi ça compte ?
- Oui.
**Pourquoi une carte de hachage?**=Keeps **O(1)** accès au score actuel d'un joueur. Essentiel pour des mises à jour rapides. Autres
Autres **Pourquoi un ensemble trié?**=Active `top(K)` dans **O(K)** en itérant du plus grand. Évite la numérisation coûteuse des données non triées. Autres
Utiliser un `multiset` / `TreeSet` qui stocke *scores*, pas des paires `(playerId,score)`. Autres
**Cas d'Edge: réinitialiser à 0**.Supprimer le lecteur à la fois de la carte et du multiset; faire *pas* insérer `0` en arrière. Garantie que "top(K)" ne paie que les joueurs actifs. Autres
Autres **Complexité de l'espace**= `O(N)` où `N` = nombre de joueurs actifs.= Gardez cela à l'esprit lors de la discussion des compromis. Autres

---

Article de blog optimisé par le SEO

Vous trouverez ci-dessous un billet de blog complet et prêt à imprimer que vous pouvez publier sur Medium, Dev.to ou votre propre blog personnel. L'article est saupoudré de mots-clés de grande valeur que les recruteurs aiment : *Concevoir un classement*, *Java solution de classement*, *Python Leaderboard*, *C++ Leaderboard*, *LeetCode 1244*, *Entretien des structures de données*.

```markdown
# Design A Leaderboard (LeetCode 1244) – Java, Python & C++ Solutions

**Mots clés:** Concevoir un classement, LeetCode 1244, Java Leaderboard solution, Python classement, C++ classement, problème d'entrevue, structures de données, hashmap, set trié, TreeSet, multiset, arbre Fenwick

---

Aperçu du problème

LeetCode 1244, *Design A Leaderboard*, vous demande de construire une structure de données qui supporte trois opérations :
`addScore`, `top(K)` et `reset`. Les contraintes permettent jusqu'à **1 000** appels totaux, mais l'objectif de l'intervieweur est de voir votre pensée sur la conception efficace de la structure de données, pas seulement une mise en œuvre de la force brute.

---

Les bonnes pratiques – Commerce optimal Arrêt

- Oui. Pourquoi c'est bon
- **Mise à jour rapides** (`addScore`, `reset`): O(log N) pour insertion/suppression dans un arbre équilibré ou multiset.
- **Requête top-K rapide**: O(K) pour résumer les premiers éléments K.
- **Simple à mettre en œuvre** avec seulement des conteneurs de bibliothèque standard.

- Oui. Mise en œuvre Java
"Java
Importation de java.util.*;

classe publique Leaderboard {
carte finale privée<entier, entier> scoreMap = nouveau HashMap<>();
finale privée TreeSet<entier> triéScores = nouveau TreeSet<>(Comparator.reverseOrder());

public vide addScore(int player) Id, score int) {
int old = scoreMap.getOrDefault(joueur Id, 0);
si (vieux > 0) triéScores.supprimer(vieux);
int newScore = ancien + score;
scoreMap.put(joueur Id, NewScore);
triésScores.add(newScore);
}

haut de page (int K) {
= 0, i = 0;
pour (int s : triés Valeurs {
i (i++ == K) rupture;
somme += s;
}
la somme de retour;
}

public vide réinitialiser(int player Id) {
int old = scoreMap.remove(playerId);
si (vieux > 0) triéScores.supprimer(vieux);
}
}
«» "

### Mise en œuvre de Python (bisect sur une liste triée)

'`python
bisect d'importation
de collections importer par défautdict

classe Tableau de classement:
def _init_(self):
self.scores = defaultdict(int)
self.sorted = []

def addScore(self, playerId: int, score: int) -> Aucun:
old = self.scores[joueur Id]
si ancien:
idx = bisect.bisect_left(self.sorted, old, key=lambda x: -x)
Self.sorted.pop(idx)
nouveau = ancien + score
self.scores[playerId] = nouveau
bisect.insort_left(self.sorted, new, key=lambda x: -x)

def top(self, K: int) -> Int:
somme de retour(self.sorted[:K])

def reset(self, playerId: int) -> Aucun:
vieux = self.scores.pop(joueur Id, 0)
si ancien:
idx = bisect.bisect_left(self.sorted, old, key=lambda x: -x)
Self.sorted.pop(idx)
«» "

### C++ Implémentation (carte_non ordonnée + multiset)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe Tableau de classement {
unordered_map<int, int> mp;
multiset<int, plus<int>> scores;

public:
vide addScore(int player) Id, score int) {
int old = mp.count(playerId) ? mp[playerId] : 0;
si (ancienne) scores.erase(scores.find(ancienne));
int nw = ancien + score;
mp[joueur Id] = nw;
scores.insert(nw);
}

dessus int(int K) {
= 0, cnt = 0;
pour (int s : scores) {
si (cnt++) K) pause;
somme += s;
}
la somme de retour;
}

réinitialiser le vide(int player Id) {
int old = mp[joueur Id];
scores.erase(scores.find(old));
mp.erase(playerId);
}
};
«» "

---

## Le "Bad" – Tri sur chaque "top"

"Java
// addScore: vecteur de reconstruction
// haut: Collections.sort(vecteur, Collections.inverseCommander()); // O(N log N)
«» "

Fonctionne pour le problème de petites limites, mais devient un **bottleneck** une fois que le classement contient des milliers de joueurs.
> **Conseil d'entrevue :** Demandez à l'intervieweur des contraintes avant de choisir ceci.

---

## Le "Ugly" – Heap qui ne peut pas mettre à jour

Utiliser une file d'attente prioritaire pour garder les plus grands scores `K` semble intelligent, mais quand un score de joueur=s change, le tas n'est plus valide. Vous devrez *lazy-supprimer* les entrées de l'impasse, ce qui ajoute complexité et risque de bug.

---

## 6-

Opération: Meilleur cas (notre bonne solution)
Il n'y a pas de lien entre l'état de santé et l'état de santé.
(TreeSet / multiset)
"reset" (log N) (log N)
"top(K)""" O(K)" O(N log N) (triage)"

**Traitement des clés:**
Maintenez une carte **hash pour la recherche rapide** et un conteneur **trié** qui reflète l'état actuel des scores. Ceci équilibre la vitesse de mise à jour et la vitesse de la requête, un modèle qui apparaît dans de nombreux problèmes d'entrevue (tableaux de tête, requêtes top-k, maintenance médiane, etc.).

---

Liste de contrôle du référencement (pour les recruteurs)

- **Titre**: Conception d'un tableau de bord – Solutions Java, Python & C++ (Code Leet 1244)
- **Description détaillée**: Découvrez la façon optimale de mettre en œuvre le problème Design A Leaderboard sur LeetCode 1244. Code Java complet, Python et C++, ainsi qu'une plongée profonde dans les bonnes, mauvaises et laides solutions. (en milliers de dollars)
- **En-têtes**: `#`, `##`, `###` avec mots clés.
- **Mots clés**:
- Concevoir un tableau de bord
- LeetCode 1244
- Structure des données du tableau de bord
- Solution Java Leaderboard
- Solution Python Leaderboard
- C++ Solution Leaderboard
- HashMap + TreeSet
- multiset + carte_non ordonnée
- bisect.insort
- problème d'entretien
- **Liens internes** (si sur votre blog) : lien vers des messages apparentés comme : Comment utiliser TreeSet pour l'ordre décroissant.
- **Liens externes** : référencez le problème original de LeetCode et tout fil de discussion ou éditorial officiel.

---

Mot final

- **Afficher les compromis**: Expliquez pourquoi vous avez choisi une carte + triée sur un tas ou un genre naïf.
- ** Contraintes à la peine** : L'interview porte souvent sur la compréhension des limites; mentionnez qu'avec 1 000 appels, une liste O(N) est bonne, mais pour la production, vous auriez besoin d'une structure plus évolutive.
- **Parler de cas de bord**: Réinitialiser à zéro, gérer les scores dupliqués et s'assurer que `top(K)` ne compte que les joueurs actifs.

Avec le code ci-dessus et les points d'entretien, vous serez prêt à répondre à la question *Design A Leaderboard* et impressionner tout embaucheur qui lit votre blog! C'est ce qu'il a dit.
«» "

---

Profitez de votre préparation d'entrevue et du codage heureux!