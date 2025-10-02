---
titre: LeetCode 2059. Opérations minimales pour convertir le nombre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## LeetCode 2059 – Opérations minimales pour convertir le nombre
*BFS, DP, Java.

---

Résumé du problème
Compte tenu d'un tableau entier distinct `nums`, d'une valeur de départ `start` (0 ≤ start ≤ 1000) et d'une cible `get`, nous pouvons appliquer les opérations suivantes à plusieurs reprises pendant que `x` reste dans la plage `[0, 1000]`:

Description
C'est pas vrai.
Ajouter une valeur à partir du tableau
"x - nombres[i]" Soustraire une valeur du tableau
"x ^ nums[i]" avec une valeur du tableau

Si une opération prend "x" hors de la portée, nous sommes autorisés à effectuer cette opération **une fois** – après cela nous ne pouvons pas continuer.
Retourner le nombre minimum d'opérations nécessaires pour atteindre `objectif` à partir de `démarrage`, ou `-1` si impossible.

> **Constraints**
> - `1 ≤ longueur nominale ≤ 1000`
> - `-109 ≤ nombres[i], but ≤ 109 "
> - `0 ≤ début ≤ 1000`
> - "Démarrer l'objectif" "

---

Remarques clés

1. **Seules les valeurs 0 – 1000 peuvent être étendues**.
Une fois que nous sortons de cette fenêtre, le chemin se termine – nous devons juste vérifier si cette étape est égale à « objectif ».

2. **L'espace d'état est minuscule (1001 états)**.
Cela permet une recherche exhaustive comme BFS ou un DP ascendant sans soucis de mémoire.

3. **Les opérations sont réversibles**.
Le graphique n'est pas dirigé: de `x` nous pouvons atteindre `y`, et de `y` nous pouvons revenir à `x` avec le même élément.
Par conséquent, nous pouvons exécuter le BFS **à partir du but** ou **à partir du début** – les deux sont optimales.

---

Algorithme – Première recherche (BFS)

1. **Initialiser**
- `queue` avec la valeur de départ (ou but, voir note ci-dessous).
- "visité[0...1000]" pour suivre les états déjà explorés.
- "étapes = 0".

2. **Loop**
Alors que la file d'attente n'est pas vide :
- Traiter tous les nœuds du niveau courant (`size = file d'attente.size()`).
- Pour chaque "x" de ce niveau, essayez les trois opérations avec chaque "nums[i]".
- Si le résultat `y` est égal à `objectif`, retourner `étapes + 1`.
- Si '0 ≤ y ≤ 1000 ' ** et** non visités, marquez visités et demandez.

3. **Incrément** "étapes" après avoir terminé un niveau.

4. Si la file d'attente se vide sans trouver `objectif`, retourner `-1`.

> **Pourquoi BFS fonctionne** – BFS explore les nœuds en augmentant la distance depuis le début, garantissant la première fois que nous avons frappé `objectif` nous avons utilisé les moins d'opérations.

---

Code (Java, Python, C++)

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
Int minimumOperations(int[] nums, int start, int but) {
booléen[] visité = nouveau booléen[1001];
Queue<integer> q = nouveau ArrayDeque<>();
q.offre(démarrage);
Étapes int = 0;

alors que (!q.isEmpty()) {
taille int = q.size();
pour (int i = 0; i < taille; i++) {
int x = q.poll();
pour (int n : nombres) {
int[] suivante = {x + n, x - n, x ^ n};
pour (int y : suivante) {
si (y == but) étapes de retour + 1;
si (y >= 0 && y <= 1000 && !visité[y]) {
visité[y] = vrai;
q.offre(y);
}
}
}
}
étapes++;
}
retour -1;
}
}
«» "

---

# # # # # #

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def minimumOperations(self, nombres: List[int], début: int, but: int) -> Int:
visité = [Faux] * 1001
q = deque([start])
étapes = 0

alors que q:
pour _ dans la plage(len(q)):
x = q.popleft()
pour n en nombres:
pour y in (x + n, x - n, x ^ n):
i y == but:
étapes de retour + 1
si 0 <= y <= 1000 et non visité[y]:
visité[y] = Vrai
q.annexe(s)
étapes += 1
retour -1
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minimumOperations(vecteur<int>& nums, int start, int but) {
vecteur<bool> visité(1001, faux);
file d'attente <int> q;
q.push(démarrage);
Étapes int = 0;

pendant que (!q.vide()) {
int sz = q.size();
pour (int i = 0; i < sz; ++i) {
int x = q.front(); q.pop();
pour (int n : nombres) {
int ops[3] = {x + n, x - n, x ^ n};
pour (int y : ops) {
si (y == but) étapes de retour + 1;
si (0 <= y && y <= 1000 && !visité[y]) {
visité[y] = vrai;
q.push(y);
}
}
}
}
+ étapes;
}
retour -1;
}
};
«» "

---

Analyse de complexité

**Métrique**
C'est pas vrai.
Temps "O(1001) *"nums"" (plus mauvais cas ~ 1 million d'opérations)
"O(1001)" pour le tableau visité + file d'attente

L'espace d'état minuscule rend l'algorithme essentiellement constant pour les contraintes d'entrevue.

---

Bon, le méchant et le méchant

L'aspect de la bonne mauvaise mauvaise
- C'est quoi ?
**Le choix de l'algorithme**
**Espace de l'État**= Seulement 1001 états → facile à raisonner== Le `objectif` peut se trouver à l'extérieur `[0,1000]` – n'oubliez pas de le vérifier avant de jeter==_______________________________________________________________________________________________________________________________________________________________________________________________________________
**Mise en œuvre**= Tableau booléen de taille 1001 au lieu d`un `HashSet` → O(1) lookup== Si vous oubliez de vérifier `y == but` avant le `[0,1000]` garde, vous manquerez les solutions qui sautent hors de portée== En utilisant la récursion ou DFS sans suivi de niveau peut conduire à empiler trop ou mauvaise réponse==

---

## Coques de bord à couvrir dans vos tests

1. **Objectif à l'intérieur de la plage** – trajectoire normale du BFS.
2. **Objectif à l'extérieur de la portée** – la dernière opération doit être celle qui atterrit exactement sur le «objectif».
3. **Toutes les opérations vous maintiennent dans `[0,1000]`** – chemin ne sort jamais.
4. **Négative "nums[i]` valeurs** – la soustraction peut devenir positive, XOR n'est pas affectée.
5. **Grandes valeurs `nums[i]`** (proche de `109`) – s'assurer que int ne déborde pas (en Java/C++ la somme maximale reste < 231).

---

Variante du PDD (facultatif)

Si vous préférez une saveur de programmation *dynamique*, lancez le BFS **du but** et construisez une table de distances. Le code ci-dessous est une version plus compacte de la solution Java; il fonctionne de façon identique.

"Java
booléen[] dist = nouveau booléen[1001];
int[] file d'attente = nouvelle int[1001];
tête d'inte = 0, queue = 0;
file[tail++] = but;
dist[objectif] = vrai;
...
«» "

---

Comment utiliser ces solutions dans votre entrevue

1. **Exposer le modèle graphique** – Les états sont des nombres, les bords sont les trois opérations. (en milliers de dollars)
2. **Justifier BFS** – il garantit des étapes minimales.
3. **Afficher le code** – mettre en évidence la boucle niveau par niveau et la vérification hors gamme.
4. **Discuse la complexité** – il fonctionne en temps constant pour la fenêtre 0–1000.

---

Résumé

- Oui. Le problème est une recherche sur un graphe 1001-noeud**.
- Un simple **BFS** de `start` (ou `objectif`) trouve les opérations minimales instantanément.
- Oui. Le code fonctionne correctement en Java, Python et C++, ce qui en fait une excellente base d'interview.

Prêt à relever ce défi LeetCode et impressionner vos responsables d'embauche ? C'est ce qu'il a dit.

---

Appel à l'action

- **Essayez la solution BFS vous-même** – modifier les "nums" pour voir comment le chemin change.
- **Posez votre propre version** sur GitHub ou votre plateforme de blog préférée.
- **Partagez cet article** avec un ami qui prépare des interviews en algorithme.

> **Mots clés**: LeetCode 2059, Minimum Operations to Convert Number, BFS, algorithme d'entretien, solution Java, solution Python, solution C++, entretien d'emploi, entretien de codage, structure des données, préparation d'entretien d'emploi.