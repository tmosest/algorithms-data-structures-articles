---
Titre: LeetCode 582. - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 582 – Processus Kill
**Langues:** C++
**Mots clés:** LeetCode 582, Kill Process, Java DFS, Python BFS, solution C++, algorithme d'entretien, arbre, graphique, entretien d'emploi

---

Récapitulation des problèmes

Vous recevez deux tableaux entiers:

Indice "ppid[i]" Autres
C'est pas vrai.
Numéro d'identification du processus i-th

Un seul processus a `ppid[i] = 0` (la racine).
Quand un processus est tué, ** tous ses processus descendants sont tués aussi**.
Compte tenu d'un nombre entier de "tueurs" (garantie d'être dans "pide"), retourner une liste de toutes les identifications de processus qui seront tués.

**Contrôles* *

* `1 ≤ n ≤ 5 × 104`
* Toutes les valeurs `pid` sont uniques
* "Kill" existe dans "pid" "

---

C'est vrai. Pourquoi c'est une question d'entrevue classique

Le bon Le mauvais Le mauvais
C'est quoi ?
*Shows* vous pouvez cartographier les relations et traverser des arbres/graphiques. *Souvent* caché dans le libellé – vous devez le reconnaître comme un problème de traversée d'arbre.
*Démonstrations* BFS vs DFS, file d'attente vs pile. *Certains candidats* pensent qu'ils ont besoin de construire l'arbre complet.
*Fits* dans un "one-liner" dans les interviews. *Les cas d'Edge* (tuer la racine, pas d'enfants) peuvent vous faire monter. *Le rendement est important.

---

C'est vrai. Stratégie de haut niveau

1. **Construire un parent → carte des enfants** (liste d'adjacence).
`unordered_map<int, vector<int>>` (C++), `HashMap<entier, liste<entier>>` (Java), ou `defaultdict(list)` (Python).
2. **Traverser le sous-arbre** en s'appuyant sur le "tueur".
- DFS (récursion ou pile)
- BFS (queue)
Les deux donnent la même réponse; BFS est un peu plus sûr contre les écoulements de cheminée pour les arbres profonds.
3. **Collecter et retourner** tous les identifiants de nœuds visités.

Complexité temporelle : **O(n)** – chaque processus est visité une fois.
Complexité spatiale: **O(n)** – liste d'adjacence + liste de résultats.

---

Mise en œuvre du code

> **Les trois solutions ont une logique identique, juste exprimée dans une syntaxe différente. **

Java (DFS avec une pile explicite)

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> killProcess(liste<enter> pid, liste<enter> ppid, int kill) {
// Construire la carte des parents → enfants
Carte<entier, liste<entier>> enfants = nouvelle HashMap<>();
pour (int i = 0; i < ppid.size(); i++) {
parent int = ppid.get(i);
si (parent) 0) continuer; // racine n'a pas de parent
children.computeIfAbsent(parent, k -> new ArrayList<>()
.add(pid.get(i));
}

// DFS utilisant une pile (itérative)
Liste du résultat <entier> = nouvelle liste de distribution<>();
Deque<Integer> pile = nouvelle ArrayDeque<>();
pile.push(kill);

pendant que (!stack.isEmpty()) {
int cur = pile.pop();
résultat.add(cur);
Liste <Integer> ch = children.get(cur);
si (ch != null) {
pour (int enfant : ch) empil.push(enfant);
}
}
le résultat du retour;
}
}
«» "

Python (BFS avec `collections.deque`)

'`python
de collections import defaultdict, deque
de taper l'importation Liste

Solution de classe:
def killProcess(self, pid: List[int], ppid: List[int], kill: int) -> Liste[int]:
# Créer une liste d'adjacence
enfants = par défautdict(list)
pour l'enfant, parent avec zip(pid, ppid):
si parent != 0:
enfants[parent].annexe(enfant)

# BFS traversant
file d'attente = deque([kill])
tué = []

pendant la file d'attente:
cur = file d'attente.popleft()
mort.append(cur)
file d'attente.extend(children[cur]) # children[cur] est une liste vide si aucun enfant

retour tué
«» "

#### C++ (DFS avec pile explicite)

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#incluez <stack>

solution de classe {
public:
std::vector<int> killProcess(std::vector<int>& pid,
à l'adresse suivante::vector<int>& ppid,
Int tuer) {
// Créer une liste d'adjacence
std::unordered_map<int, std::vector<int>> les enfants;
pour (size_t i = 0; i < ppid.size(); ++i) {
si (ppid[i]] 0) continuer; // racine
les enfants[ppid[i]].push_back(pid[i]);
}

// DFS utilisant une pile
std:stack<int> st;
s.push(kill);
std::vecteur<int> ans;

pendant que (!st.vide()) {
Int cur = st.top(); st.pop();
le nom et l'adresse de l'utilisateur;
auto it = children.find(cur);
si (it != children.end()) {
pour (int enfant : it->second) st.push(enfant);
}
}
le retour des an;
}
};
«» "

---

C'est vrai. Tranche Liste de contrôle des cas

Qu'est-ce qu'il faut regarder
-- -- -- -- -- -- -- -- --
Autres **Tirer la racine**=Le parent root=s est `0`; l'algorithme fonctionne toujours. Autres
**Processus sans enfants** Autres
Autres ** Arbres profonds (= 5 × 104 niveaux)**= Préférez le DFS/BFS itératif sur la récursion pour éviter le débordement de la pile. Autres
Toutes les solutions fonctionnent dans le temps O(n) et la mémoire ; gardez la liste d'adjacence compacte. Autres

---

#### 6=1 Interview-Ready Points de discussion

1. **Exposer le modèle graphique**: Nous traitons les paires `pid`‐`ppid` comme des bords dans un arbre dirigé; tuer un processus n'est qu'un sous-arbre traversant. (en milliers de dollars)
2. **Choix de la traversée**: L'utilisation de BFS parce qu'elle garantit le temps O(n) et aucun problème de profondeur de récursion, mais DFS est parfaitement bien. (en milliers de dollars)
3. ** Analyse de la complexité**: temps O(n), espace O(n). (en milliers de dollars)
4. **Cases de corner**: Que faire si le processus tué est la racine? Et si elle n'avait pas d'enfants ? (en milliers de dollars)
5. **Tests**: Ajouter des tests unitaires pour les deux cas d'échantillonnage, un seul noeud et une chaîne profonde. (en milliers de dollars)

---

### # 7-SEO-Friendly Conclusion

Si vous regardez un rôle d'ingénierie logiciel, maîtrisez **LeetCode 582 – Kill Process** démontre votre capacité à traduire un scénario de gestion de processus réel en code algorithmique propre.
- **Java** et **Python** solutions vous montrent être à l'aise avec les collections de haut niveau.
- **C++** prouve que vous pouvez gérer efficacement les structures de données de bas niveau.

Pratiquez ces modèles et vous serez prêt à discuter de l'arbre traversal et des algorithmes graphiques avec confiance dans toute interview technique. Bon codage !

---