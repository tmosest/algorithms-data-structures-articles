---
titre: LeetCode 3347. Fréquence maximale d'un élément après l'exécution des opérations II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3347. Fréquence maximale d'un élément après l'exécution des opérations II
> **Traitement du public**
> *Java • Python • C++ – solution en 3 langues + article de préparation de l'interview en référencement*

---

### TL;DR
Vous avez un tableau `nums`, une portée `[-k, k]` et un nombre limité d'opérations `numOperations`.
Chaque opération vous permet de choisir un indice *non utilisé* et d'y ajouter n'importe quelle valeur `[-k, k]`.
Vous voulez maximiser le nombre d'éléments égaux qui peuvent se retrouver dans le tableau.

La stratégie optimale est une ligne de balayage ** sur tous les paramètres d'intervalle**.
Temps: `O(n log n)` – trier les paramètres de 3 n.
Mémoire: `O(n)` – compteurs + carte de l'événement.

Ci-dessous vous trouverez des solutions de travail complètes dans **Java, Python, et C++**, plus un article complet **blog** qui explique le problème, l'algorithme, les pièges, et pourquoi il est une grande question d'interview.

---

Réévaluation des problèmes

«» "
Entrée
nombres – tableau de taille 1 ... 10^5
k – 0 ... 10^9
numOpérations – 0 ... nums.longueur

Opération (heures d'opération répétées)
1. Choisissez un index qui n'a pas été choisi avant.
2. Ajouter un entier v où -k ≤ v ≤ k aux nombres[i].

Objectif
Retourner la fréquence maximale possible (c.-à-d. combien d'éléments sont égaux) de toute valeur après avoir effectué toutes les opérations.
«» "

> **Exemple**
> `nums = [1,4,5] , k = 1 , numOpérations = 2`
> Nous pouvons transformer le tableau en `[1,4]` → fréquence de `4` = 2.

---

Remarques clés

1. **Cible accessible* *
Pour un élément `a` vous pouvez atteindre n'importe quelle cible `t` dans l'intervalle fermé `[a-k , a+k]` avec *one* opération (ou 0 si `a == t`).

2. **Intervalles sur la ligne de nombre**
Chaque entrée de tableau nous donne un intervalle de valeurs finales possibles:
«» "
une → [a-k , a+k]
«» "
Le problème devient: trouver un point `t` qui est couvert par le plus d'intervalles.

3. ** Budget opérationnel**
- Les éléments déjà égaux à "t" sont "free".
- Nous pouvons convertir au plus `numOpérations` d'autres éléments qui couvrent `t`.

Par conséquent, la meilleure fréquence à un point `t` est
«» "
cnt[t] + min(numOpérations, couverture - cnt[t])
«» "
où
* `cnt[t]` – combien d'éléments sont déjà `t`
* `couverture[t]` – combien d'intervalles contiennent `t` (c.-à-d. combien d'éléments se trouvent dans `k` de `t`).

4. **Tous les points utiles sont des paramètres**
La fonction `cover(t)` ne change qu'à l'extrémité gauche ou droite d'un intervalle.
Il suffit de balayer chaque coordonnée distincte qui apparaît comme
* `a - k` (départ intermédiaire)
* `a + k + 1` (un après la fin de l'intervalle, pour un balayage classique +1 / -1=).

5. **Sécurité hors pair**
L'événement à `a + k + 1` supprime l'intervalle **après** le dernier entier qui peut atteindre `t`.
C'est pourquoi nous ajoutons **+1** au bon paramètre.

---

Algorithme de la ligne de balayage (illustré)

«» "
pour chaque valeur a en chiffres:
cnt[a] += 1
événements[a - k] += 1 // début de l ' intervalle
événements[a + k + 1] -= 1 // fin de l'intervalle (après +1)

trier toutes les clés dans les événements → points[]
actif = 0
réponse = 0

au lieu de p dans les points [] (ordre croissant):
+= événements actifs[p] // #intervalles qui couvrent p
déjà = cnt.get(p, 0)
extra = min(active - déjà, numOperations)
candidat = déjà + supplémentaire
réponse = max(réponse, candidat)
«» "

*Le balayage garantit qu'à tout moment nous savons exactement combien d'indices peuvent être transformés en ce point. *

---

Trois implémentations de travail

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
public int maxFrequence(int[] nums, int k, int numOperations) {
Carte<entier, entier> nombre = nouvelle HashMap<>(); // fréquences de valeurs existantes
Carte<Long, entier> événements = nouveau HashMap<>(); // +1 au début, -1 après la fin

pour (int a : nombres) {
count.merge(a, 1, entier::sum);

longue gauche = (long) a - k;
longue droite = (long) a + k + 1; // après l ' intervalle
les événements. fusion (gauche, 1, entier::sum);
les événements. fusion (droite, -1, entier::sum);
}

Liste des points <Long> = nouvelle liste de points <>(events.keySet());
Collections.sort(points);

long actif = 0; // courant #intervalles couvrant le point
int best = 0;

pour (long p : points) {
active += events.get(p);
int déjà = count.getOrDefault((int) p, 0);

// Combien d'autres indices couvrant p nous pouvons encore changer?
int extra = (int) Math.min(active - déjà, numOperations);
candidat int = déjà + supplémentaire;
meilleur = Math.max (meilleur candidat);
}
le meilleur retour;
}
}
«» "

> **Complexité**
> *Time* `O(n log n)` – tri à la plupart des paramètres `3n`
> * Mémoire* `O(n)` – deux cartes de hachage

---

# # # # # #

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def maxFréquence(self, nums: List[int], k: int, numOpérations: int) -> Int:
cnt = Nombre de fréquences existantes
événements = Counter() # +1 à gauche, -1 à droite+ 1

pour les nombres:
gauche = a - k
droite = a + k + 1 # exclusif
événements[gauche] += 1
événements[droite] -= 1

points = triés(événements)
actif = 0
meilleur = 0

pour p en points:
événements actifs +=[p]
déjà = cnt.get(p, 0)
extra = min(active - déjà, numOperations)
candidat = déjà + supplémentaire
best = max (meilleur candidat)

le meilleur retour
«» "

> **Pourquoi ` droite = a + k + 1`?**
> Il maintient l'intervalle *fermé* à `a + k`.
> Après cette coordination nous arrêtons de compter cet élément.

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nt maxFréquence(vector<int>& nums, int k, int numOperations) {
unordered_map<long long, int> cnt; // valeur → freq
non ordonné_map<long long, int> ev; // event point → delta

pour (int a : nombres) {
cnt[a]++;

longue longue l = statique_cast<long long>(a) - k;
longue longue r = static_cast<long long>(a) + k + 1; // exclusive
ev[l] += 1;
-= 1;
}

points vectoriaux < longs>;
points.reserve(ev.size());
pour (auto &p : ev) points.push_back(p.first);
tri(points.degin(), points.end());

longue durée active = 0;
int best = 0;

pour (long p : points) {
actif += ev[p];
int déjà = cnt.count(p) ? cnt[p] : 0;
int extra = static_cast<int>(min(active - déjà, static_cast<long>(numOpérations)));
best = max (meilleur, déjà + supplémentaire);
}
le meilleur retour;
}
};
«» "

> **Astuce** – toujours jeté à "long long" lors de l'ajout de `k` pour éviter un débordement accidentel, même si 2 × 10^9 correspond à `int`.

---

Les bons, les mauvais, les affreux

Ce qui est grand Ce qui est dur Pièges communs
- C'est pas vrai.
• 'O(n log n)' – assez rapide pour 10^5. <br>• Utilise seulement l'arithmétique entier (pas de FFT). <br>• intuition géométrique claire. La ligne de nombre est énorme (jusqu'à 10^9), donc nous devons **compresser** coordonnées. peut conduire au débordement. <br>• Oublier que les indices sont déjà égaux au coût cible **0** opérations. Autres
La ligne de balayage est un modèle classique d'entrevue. <br>• Démontre la connaissance des sommes préfixes, du comptage des événements et de la compression par carte. Vous devez gérer la contrainte **unused‐index** – de nombreux candidats oublient que les éléments déjà égaux à la cible sont libres. . • L'utilisation d'un `TreeMap` au lieu d'un vector+sort conduit à des événements `O(n log n)` mais un facteur supplémentaire de log pour chaque mise à jour – encore fine mais moins propre. Autres
• Si `k` est 0, l'algorithme dégénère à la fréquence existante – trivial pour tester. Si vous essayez une boucle naïve "t" , vous frapperez `O(n * range)` – impossible. Autres

---

Les solutions alternatives (pourquoi mieux balayer)

Approche Complexité Remarques
C'est quoi, ça ?
Autres **Binary Search + Prefix Sum**="O(n log M)` (M = valeur max)=" Fonctionne si vous avez seulement besoin de *max* fréquence mais *sans* `numOperations` limite. Autres
**Two-Pointer / Sliding Window**=1 `O(n)`=1 Seulement applicable lorsque `k` est assez petit que la cible doit être une valeur existante; échoue lorsque `k` est grande. Autres
**Segment Tree**= O(n log M)== Poids lourd; inutile lorsque le balayage est plus facile. Autres

La ligne de balayage est la solution générale la plus propre et la plus rapide pour l'énoncé complet du problème.

---

Analyse de complexité

«» "
Let n = nombres.longueur
«» "

*Événements générés*: `3 n` (démarrage, fin+1 et points de valeur existants)
*Traitement*: "O(3n log 3n)" "
*Passer*: linéaire en nombre de points distincts, `O(n)`

Mémoire :
- `cnt` – au plus `n` clés distinctes
- "events" – au plus les touches `2n`
→ `O(n)`.

---

Pourquoi ce problème se pose-t-il pour les entrevues

1. **La pensée géométrique** – visualise les valeurs comme des intervalles, rendant la solution intuitive.
2. **Coordonner la compression** – apprendre à gérer les grandes gammes.
3. **Comptabilité des événements** – trick préfixe classique à la volée.
4. ** Budget des opérations** – force les candidats à penser aux indices *libre* par rapport aux indices *payant*.
5. **Manipulation du boîtier** – `k = 0`, valeurs négatives, grande `k` toute robustesse d'essai.

Si vous pouvez expliquer l'algorithme en *minutes*, vous montrez une profondeur de compréhension qui va au-delà du DP de niveau de surface ou des astuces de tri.

---

À emporter

*Utilisez une ligne de balayage avec les événements -1 pour compter combien d'entrées de tableau peuvent être transformées en chaque valeur finale possible. Ajoutez le budget des opérations dans le calcul et vous obtiendrez la fréquence finale optimale dans le temps `O(n log n). *

---

Bon codage ! (en milliers de dollars)

---

*Si vous avez des questions, laissez un commentaire ci-dessous ou partagez vos propres solutions. Continuons la discussion ! *