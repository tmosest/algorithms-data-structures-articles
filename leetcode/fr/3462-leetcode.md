---
titre: LeetCode 3462. Somme maximale avec au plus des éléments K - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (code de bord 3462)

** Somme maximale avec au plus des éléments K**
Données

* une grille `n × m` d'entiers non négatifs,
* un tableau `limites[0 ... n‐1]` qui vous indique combien d'éléments vous pouvez prendre de chaque ligne,
* un entier `k` qui limite le nombre total d'éléments sélectionnés,

** déterminer la somme maximale possible** d'éléments au plus `k` sans jamais dépasser les limites par rangée.

*Contrôles*

Les limites [i]
- C'est quoi ?
≤ 500 $ ≤ 500 $ 0 ... 105 $ 0 ... m $ 0 ... min(n × m, valeurs limites)

Les valeurs sont suffisamment grandes pour qu'un entier de 32 bits puisse déborder, de sorte que la réponse est retournée comme « longue ».

---

- Oui. 2. Aperçu de la solution

La stratégie gourmande qui choisit toujours la plus grande valeur disponible actuellement est optimale.

* Chaque fois que nous voulons l'élément suivant, nous regardons le nombre **le plus grand** que nous n'avons pas encore utilisé.
* Nous pouvons utiliser une file d'attente **max-heap (priorité)** pour récupérer cet élément dans `O(log (n × m))`.
* En tirant des éléments, nous conservons un compteur `choisi[row]` qui indique combien de valeurs ont déjà été tirées de cette ligne.
* Si `choisi[row] < limits[row]` nous pouvons ajouter la valeur à notre somme.
* Sinon l'élément est rejeté et nous passons à autre chose.

Parce que nous ne regardons jamais en arrière (le tas contient toujours toutes les valeurs restantes), l'algorithme garantit la somme maximale.

---

- Oui. 3. Complexité

Étape de travail Raison
C'est pas vrai.
Construisez un tas de poussoirs `n × m` `O(n × m log(n × m)` Autres
Extracter des éléments au plus `k` pops' `O(k log(n × m)` Autres
Total **O((n × m + k) log(n × m))**
Autres Espace supplémentaire: tas + compteurs: **O(n × m)

Compte tenu des contraintes (`n,m ≤ 500` → au plus 250 000 éléments), cela s'adapte facilement dans les délais.

---

- Oui. 4. Code

Vous trouverez ci-dessous des implémentations propres et conviviales dans **Java, Python et C++**.
Tous les trois utilisent la même idée : un talon max et un tableau de compteurs par rangée.

#### 4.1 Java

"Java
Importer java.util. Priorité Demande;

solution de classe publique {
public long maxSum(int[]] grille, limites int[], int k) {
int n = longueur de grille, m = longueur de grille[0];
somme longue = 0L;

// Max-heap: valeur de l'élément, indice de ligne
PrioritéQueue<long[]> pq = nouveau PrioritéQueue<>(
(a, b) -> Long.compare(b[0], a[0]) // descendant
);

// Poussez chaque élément dans le tas
pour (int i = 0; i < n; ++i) {
pour (int j = 0; j < m; ++j) {
pq.offre(nouvelle longue[]{grid[i][j], i});
}
}

int[] pris = nouveau int[n]; // combien pour chaque ligne

pendant que (k > 0 & & & ipq.isEmpty() {
long[] top = pq.poll();
valeur longue = haut[0];
ligne int = (int) haut[1];

si (prise[ligne] < limites[ligne]) {
la somme += valeur;
pris[row]++;
k--; // une fente de moins gauche
}
}

la somme de retour;
}
}
«» "

---

4.2 Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def maxSum(self, grille: List[List[int]],
limites: Liste[int], k: int) -> Int:
n, m = len(grid), len(grid[0])
# Utilisez un poids max en poussant des valeurs négatives
pq = [(-grid[i][j], i) pour i dans l ' intervalle (n) pour j dans l ' intervalle (m)]
heapq.heapify(pq)

pris = [0] * n
Total = 0

alors que k et pq:
val, ligne = heapq.heappop(pq)
val = -val # restaurer la valeur originale
si pris[ligne] < limites[ligne]:
Total += valeur
prise[ligne] += 1
k -= 1

retour total
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long maxSum(vecteur<vecteur<int>>& grille,
vecteur<int>& limites, int k) {
int n = grille.size(), m = grille[0].size();
somme longue = 0;

//pap max: paire(valeur, ligne)
priority_queue<pair<int,int>> pq;
pour (int i = 0; i < n; ++i)
pour (int j = 0; j < m; ++j)
pq.emplace(grid[i][j], i);

vecteur<int> pris(n, 0);

pendant que (k > 0 & & & !pq.vide() {
auto [val, rang] = pq.top();
La présente décision entre en vigueur le vingtième jour suivant celui de sa publication au Journal officiel de l'Union européenne.
si (prise[ligne] < limites[ligne]) {
somme += valeur;
++prison[ligne];
--k;
}
}
la somme de retour;
}
};
«» "

Les trois programmes produisent le même résultat dans la mémoire `O(n×m + k) log(n×m)` et `O(n×m)`.

---

- Oui. 5. Article de blog: -Le bon, le mauvais, et le mauvais de Leetcode 3462

#### 5.1 Pourquoi Leetcode 3462 compte

- **Interview buzz-word:** La somme maximale avec la plupart des éléments K est un problème classique *greedy + tas* qui teste votre capacité à équilibrer les contraintes par ligne et une limite globale.
- ** Compétences prêtes à l'emploi :** La solution démontre la connaissance des files d'attente prioritaires, des algorithmes gourmands et de la manipulation minutieuse des entiers (long/64‐bit).
- ** Balises de référencement**: *Leetcode 3462, somme maximale avec au plus des éléments k, algorithme d'entretien, file d'attente prioritaire, cupide, Java, Python, C++*.

Si vous voulez décrocher un rôle d'ingénierie logicielle, maîtriser ce problème impressionnera les gestionnaires d'embauche et montrera que vous pouvez transformer un problème apparemment difficile en une solution propre et optimale.

---

#### 5.2 Le bon: une approche propre de l'avidité

1. **Intuitive** – Cochez le plus grand nombre que vous pouvez encore prendre. (en milliers de dollars)
2. **Optimal** – La propriété de choix gourmande tient parce que chaque élément est indépendant des autres en dehors de la limite de ligne.
3. ** Mise en œuvre simple** – Juste un max-heap et un tableau de comptoir.
4. **Évoluable** – Fonctionne jusqu'à 250 000 cellules de grille; bien sous les limites du Leetcode.

> **Résultat**: temps linéaire, espace constant par rangée.

---

5.3 Les mauvaises: ce que vous devez surveiller

Pourquoi ça compte ?
- Oui.
**Débordement entier**= Valeurs de grille allant jusqu'à 105, et k jusqu'à 250 000 → somme peut atteindre 2,5×1010.= Utiliser 64-bit (`long` en Java, `long` en C++, `int` en Python est débordé). Autres
**Le plus gros tas**=Le stockage de tous les éléments consomme de la mémoire ('O(n*m)'). Il est inévitable pour la solution cupidité optimale, mais convient toujours dans 256 Mo pour des contraintes données. Autres
**Limites de taille**L'algorithme peut être aussi bas que 0 ou aussi haut que `min(n*m, limites de l'algorithme)'. Autres
**La limite de temps est bonne, mais si `k` `n*m`, le facteur log domine. Encore assez rapide pour les éléments de 250 k : 4 à 5 millions d'opérations de tas – < 0,2 s dans les langues modernes. Autres

---

### 5.4 Les approches de rechange (et sous-optimales)

Pourquoi c'est l'exemple de Ugly
- C'est quoi ?
**Brute-Force DP** Énumérer tous les sous-ensembles de chaque ligne → `O(n * 2^m)`. Autres
**Trier les rangées individuellement** Trier chaque ligne, puis fusionner les valeurs k supérieures avec les vérifications par ligne. Autres
**Min-heap de valeurs sélectionnées**= Logique inverse; vous devez pop le plus petit pour décider quand jeter, conduisant à plus de comptabilité. · Pousser les éléments sélectionnés sur un trou de taille minimale et les jeter au-dessus de «k». Autres

Ces méthodes font exploser dans le temps ou ajoutent une complexité inutile. La stratégie heap‐greedy reste la solution la plus propre, la plus rapide et la plus durable.

---

- Oui. 6. À emporter pour votre récit

- **Showcase** le modèle gourmand de votre portfolio.
- Mettre en évidence **la gestion des contraintes par rangée**—un scénario d'entrevue fréquent.
- Insistez sur ** types de données corrects** (`long`/`long`) pour éviter les bugs subtils.
- Mention **analyse de l'espace-temps** pour démontrer une pensée algorithmique.

Ajoutez l'extrait suivant à votre site GitHub ou personnel :

```markdown
### Somme maximale avec au plus des éléments K (code leet 3462)
*Greedy + Max-Heap solution (Java, Python, C++) – temps O((n×m + k) log(n×m)), mémoire O(n×m). *
«» "

Des mots-clés faciles à rechercher et une description concise et riche en code font que les recruteurs cessent de défiler et commencent à lire. Bonne chance pour votre prochain entretien !