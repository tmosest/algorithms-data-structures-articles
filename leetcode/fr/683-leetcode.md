---
titre: LeetCode 683. K Fentes vides -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 683 – **K Fentes vides**
> **Hard** – 2 × 104 ≤ n, k ≤ 2 × 104

> **Objectif:**
> Trouvez le **jour le plus tôt** où deux ampoules qui sont **k + 1** positions séparées sont à la fois ON et toutes les ampoules entre elles sont OFF.

---

- Oui. 1. Idée de solution rapide
1. **Gardez la trace des ampoules qui sont déjà ON** dans un arbre de recherche binaire *équilibré* (`TreeSet` / `set` / `SortedSet`).
2. Quand une nouvelle ampoule à la position `p` est allumée:
* Regardez l'ampoule la plus proche ON sur la gauche** ('en bas(p)').
* Regardez l'ampoule la plus proche ON sur la droite** ('higher(p)').
3. Si l'un des deux voisins est exactement `k + 1` positions loin → retourner le jour actuel.
4. Si la boucle finit → retourner `-1`.

> **Pourquoi ça marche? * *
> La seule façon pour une paire d'ampoules ON peut avoir *exactement* `k` OFF ampoules entre eux est s'il n'y a pas d'autre ampoule ON dans cet intervalle.
> L'ampoule ON la plus proche de chaque côté est le *seulement* candidat pour satisfaire l'état.

> **Complexités**
> *Time*: **O(n log n)** – chaque insert et recherche est `log n`.
> *Espace*: **O(n)** – nous stockons chaque ampoule une fois.

---

- Oui. 2. Mise en œuvre du code

#### 2.1 Java 17
"Java
Importer java.util. TreeSet;

solution de classe publique {
ampoules, int k) {
TreeSet<Integer> sur = nouveau TreeSet<>();
pour (int jour = 1; jour <= bulbes.longueur; jour++) {
int pos = ampoules[jour - 1];
le.add(pos);

Entier gauche = on.lower(pos);
Entier droit = on.higher(pos);

si (gauche != null && pos - gauche - 1 == k) jour de retour;
si (droite != null && droite - pos - 1 == k) jour de retour;
}
retour -1; // jamais trouvé
}
}
«» "

2.2 Python 3 (bisec)
'`python
de bisect importer bisect_left

Solution de classe:
def kEmptySlots(self, bulbes: list[int], k: int) -> Int:
On = [] # liste triée des postes ON
pour la journée, pos dans l'énumération(bulbes, 1):
i = bisect_left(on, pos)
le.insérer(i, pos)

# voisin gauche
i > 0 et pos - on[i-1] - 1 == k:
jour de retour
# voisin droit
i+1 < len(on) et on[i+1] - pos - 1 == k:
jour de retour
retour -1
«» "

#### 2.3 C++17 (`std::set`)
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int kEmptySlots(vecteur<int>& bulbes, int k) {
set<int> on;
pour (int jour = 1; jour <= bulbes.size(); ++jour) {
int pos = ampoules [jour-1];
le.insérer(pos);

auto it = on.lower_bound(pos);

// voisin gauche
si (it != on.gin()) {
int gauche = *prev(it);
si (pos - gauche - 1 == k) le jour du retour;
}

// voisin droit
auto nxt = next(it);
si (nxt != on.end()) {
int droite = *nxt;
si (droit - pos - 1 == k) le jour du retour;
}
}
retour -1;
}
};
«» "

---

- Oui. 3. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 683

> **Mots clés**: *LeetCode 683*, *K Fentes vides*, *problème dur d'entrevue*, *Java TreeSet*, *Python bisect*, *C++ set*, *arbre de recherche binaire*, *algorithme d'entrevue d'emploi*

---

3.1 Introduction
Dans chaque entretien d'ingénierie logicielle, l'intervieweur aime mélanger un classique *problème d'array* avec un changement de structure des données*. LeetCode 683 K Les fentes vides est un tel problème. Il vous force à penser aux *mises à jour dynamiques* et aux *questions des voisins les plus proches* – compétences qui apparaissent dans les systèmes du monde réel comme l'expulsion de cache, l'ordonnancement et l'analyse de séries chronologiques.

> **Pourquoi ce problème est important* *
> • Démontre votre compréhension des ensembles ** ordonnés** et **réduction de l'espace de recherche**.
> • Testez votre capacité à **optimiser** une force brute O(n2) dans O(n log n).
> • Vous expose à la subtilité de **conditions limites** (k = 0, n = 1, etc.).

---

3.2 L'approche naïve
Une solution de manuel O(n2) est de vérifier chaque jour chaque paire d'ampoules ON et de compter les ampoules OFF entre elles.
Texte
pour la journée à 1..n:
pour i en 1. jour:
pour j en i+1..jour:
si les ampoules[i] et les ampoules[j] sont allumées:
Si count_off_entre(i, j) == k:
jour de retour
«» "
- **Heure**: O(n3) – trop lent pour n = 20 000.
- **Espace**: O(1).

> *Pourquoi ça échoue*: La double boucle fait déjà exploser l'exécution. Les intervieweurs modernes s'attendent à ce que vous améliorez cela.

---

3.3 L'approche efficace (bonne)
En utilisant une BST **équilibrée (Java `TreeSet`, C++ `std::set`, Python `bisect`) nous permet:

1. Insérez chaque position de l'ampoule dans **O(log n)**.
2. Trouvez l'ampoule *nearest* ON à gauche/droite dans **O(log n)**.
3. Comparez les distances.

> *Résultat*: **O(n log n)** temps, **O(n)** espace.
> C'est la solution simple la plus rapide que vous pouvez écrire sans recourir à des structures de données plus exotiques (arbre de segment, arbre indexé binaire, ou union‐find avec des mises à jour paresseuses).

---

3.4 Cas et pièges des bords (les affreux)

Qu'est-ce que regarder ?
- C'est pas vrai.
- Oui. Vous cherchez des ampoules ON adjacentes. Le code fonctionne toujours parce que `pos - gauche - 1` sera `0`. Autres
- Oui. 1 ''' Aucune paire n'existe → toujours `-1`.' La boucle sort avec `-1`. Autres
Le problème garantit une permutation, donc ce n'est pas arrivé, mais dans un système réel vous avez besoin de vous protéger contre elle. Autres Utilisez un `Set` pour détecter les duplicatas tôt. Autres
Autres Très grand `k` (par exemple, `k > n`) Cochez `if k >= n: retour -1`. Autres
Erreurs hors-par-un. Autres

---

3.5 Ce que les intervieweurs En fait, cherchez

1. **Correctness**: Remettez le jour le plus précoce, pas n'importe quel jour.
2. **Complexité** : expliquer pourquoi O(n log n) est acceptable pour n = 20 000.
3. ** Choix de la structure des données**: Justifier pourquoi un BST est un ajustement naturel (les plus récentes requêtes de voisins).
4. **Lisibilité du code**: Utiliser des noms de variables significatifs (`on`, `left`, `right`) et des commentaires.

---

3.6 A emporter pour votre prochaine entrevue

- Maîtrisez l'idée de *=nearest voisin dans une collection triée; elle apparaît dans la programmation, le réseautage et même le développement de jeux.
- Pratiquez la même logique en **Java, Python et C++** – vous serez prêt pour les questions linguistiques-agnostiques.
- N'oubliez pas de discuter ** cas de pointe**; les intervieweurs aiment vous voir penser à eux.

---

- Oui. 4. Pensées finales

LeetCode 683 est plus qu'un simple casse-tête "bulb-turning". C'est un microcosme de problèmes algorithmiques du monde réel : vous avez un ensemble dynamique d'éléments et devez répondre rapidement aux requêtes de gamme. En maîtrisant ce problème, vous démontrerez à la fois la compréhension théorique et le codage pratique – exactement ce que les gestionnaires d'embauche recherchent.

Bonne chance pour ta chasse au travail ! C'est ce qu'il a dit