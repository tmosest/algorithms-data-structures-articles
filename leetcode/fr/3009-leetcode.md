---
titre: LeetCode 3009. Nombre maximal d'intersections sur le graphique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème

**LeetCode 3009 – Nombre maximal d'intersections sur le graphique**

> Nous avons un graphique en ligne composé de points `n`
> `(k, y[k])` (1-indexé).
> Il n'y a pas deux points consécutifs qui partagent la même coordination y.
>
> Nous pouvons tracer une ligne horizontale "y = h".
> Combien de points d'intersection cette ligne peut-elle avoir avec le graphique?
> Retournez le nombre **maximum** d'intersections possibles.

Contraintes typiques

«» "
2 ≤ n ≤ 1e5
1 ≤ y[i] ≤ 1e9
Pour tous les
«» "

La signature de la fonction dans les trois langues suivantes est

"Java
int maxIntersectionCount(int[] y)
«» "
'`python
def maxIntersectionCount(self, y: List[int]) -> Int
«» "
'`cpp
int maxIntersectionCount(vecteur<int>& y);
«» "

---

- Oui. 2. Approche naïve – pourquoi elle échoue

L'idée évidente de la force brute :

1. Pour chaque paire de points consécutifs `(i,i+1)`
*si* `y[i] < y[i+1]`
itérer à travers chaque entier `h` de `y[i]+1` à `y[i+1]-1` et
incrémenter un compteur pour ce `h`.
Faites de même lorsque `y[i] > y[i+1]`.
2. Comptez également les paramètres `y[i]` eux-mêmes.
3. Prenez le compteur maximum.

Complexités
- **Heure** – O(n ·m) où *m* est la portée de l'axe des y (jusqu'à «1e9»!),
- **Espace** – O(m) pour le tableau de comptoir.

Cela est évidemment impossible pour les limites données.

---

- Oui. 3. Insight – La fonction est constante par pièce

Pour tout nombre réel `h`, le nombre d'intersections de `y = h` avec la carte
est:

«» "
(nombre d'indices i avec y[i] == h) //
+ (nombre de segments (i,i+1) avec min < h < max) // traversant le segment
«» "

Les seuls moments où ce nombre peut changer sont quand `h`
est égal à un des paramètres.
Entre deux années consécutives distinctes, le nombre reste ** exactement le même**.
Par conséquent, le maximum sera atteint à

* une hauteur entière qui apparaît en y, ou
* tout nombre réel strictement entre deux valeurs distinctes consécutives de "y".

Donc nous n'avons besoin de savoir, pour chaque hauteur entière qui compte,
combien de segments le traversent.

---

- Oui. 4. Ligne de balayage + différence Carte

**Étape 1 – Paramètres de comptage**
«» "
freq[h] = nombre d'indices i avec y[i] == h
«» "

**Étape 2 – Marquer les segments qui croisent une hauteur entière* *
Pour chaque paire consécutive `(i,i+1)`
laisser `faible = min(y[i], y[i+1]) "
`high = max(y[i], y[i+1]) "

Si `faible + 1 <= haute - 1`, alors chaque entier `h` dans
`[low+1 , high-1]` est strictement entre les deux paramètres.
En utilisant une carte *différence* nous pouvons ajouter `+1` pour cet intervalle entier:

«» "
diff[low+1] += 1 // commencer à ajouter à partir de low+ 1
diff[high] -= 1 // arrêter d'ajouter avant haut
«» "

Si `low+1== high` l'intervalle est vide – il n'y a pas de hauteur entière entre
les deux paramètres et nous la sautons.

**Étape 2 – Somme du préfixe sur toutes les hauteurs pertinentes* *
Toutes les hauteurs qui apparaissent jamais sur la carte (`bas+1`, `haut`, ou un point final)
sont triés (un `TreeMap` / `std::map` / Python `sorted(dict)` fait cela pour
gratuit).
Nous balayons dans l'ordre ascendant, en maintenant un préfixe courant somme `cur`:

«» "
cur += diff[hauteur] // combien de segments traversent actuellement cette hauteur
réponse = max(réponse, cur + freq.get(hauteur,0))
«» "

Cela nous donne le nombre d'intersections à cette hauteur particulière.
Le maximum sur le balayage est la réponse.

---

- Oui. 5. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre maximum possible de
Les intersections.

---

Lemma 1
Pour chaque hauteur entière `h` qui se produit dans le tableau `y`,
l'algorithme compte exactement le nombre de segments `(i,i+1)` avec
"min(y[i],y[i+1]) < h < max(y[i],y[i+1])".

**Prof.**

Pendant l'étape 1, nous avons traité chaque segment une fois.
Pour un segment avec bas `l` et haut `r` (`l < r`) nous avons exécuté

«» "
diff[l+1] += 1
[r] -= 1
«» "

Si `h` se situe strictement entre `l` et `r`, c'est-à-dire `l+1 ≤ h ≤ r-1`, alors
`h` se trouve dans la gamme *prefix* où `cur` a déjà été augmenté de 1.
Si `h` est en dehors de cette plage, les deux mises à jour delta s'annulent.
Ainsi, `cur` contient le nombre exact de segments traversant `h`.



Lemma 2
Pour tout nombre réel `h` non égal à un paramètre,
le nombre d'intersections correspond au nombre d'une hauteur entière voisine
(par exemple: `floor(h)` ou `ceil(h)`).

**Prof.**

Que `v` et `w` soient les deux valeurs distinctes consécutives de `y` de sorte que
"v < h < w".
Aucun paramètre ne se situe entre `v` et `w`.
Par conséquent, `freq[h] = 0` et le jeu de segments de croisement est le même pour **chaque* *
hauteur dans l'intervalle ouvert `(v,w)`.
Prendre `h` comme entier dans cet intervalle (s'il y en a un) ou
comme `v+ε` pour infinitésimal `ε` donne le même nombre d'intersections. *



Lemma 3
L'algorithme `réponse` est le maximum sur toutes les hauteurs réelles.

**Prof.**

L'algorithme évalue le nombre d'intersections à chaque hauteur
peut peut-être changer le nombre: toutes les hauteurs de fin de course, et tous
les limites entières qui commencent ou terminent un intervalle de temps
(«faible+1» et «élevée»).
Par Lemma 2 toute hauteur réelle qui n'est pas un paramètre a la même
le nombre d'intersections comme l'une des hauteurs entières évaluées.
Ainsi, le nombre maximal d'intersections sur toutes les hauteurs réelles est atteint
par une des hauteurs examinées par l'algorithme, donc l'algorithme
maximum est le maximum mondial. *



- Oui. Théorème
`maxIntersectionCount` retourné par l'algorithme est égal au maximum
nombre possible d'intersections d'une ligne horizontale avec la carte.

**Prof.**

Par Lemma 1 l'algorithme compte correctement le nombre de segments traversant
chaque hauteur évaluée.
Par construction, il ajoute également le nombre de paramètres à cette hauteur.
Donc pour chaque hauteur examinée l'algorithme calcule le vrai
nombre d'intersections.
Par Lemma 3, le maximum de ces dénombrements est l'optimum mondial. *



---

- Oui. 5. Mise en œuvre – Java / Python / C++

Vous trouverez ci-dessous le code source **commenté** dans les trois
langues demandées.
Toutes utilisent *O(n log n)* temps et *O(n)* espace.

> **Note** – Les trois codes sont prêts à être collés dans l'éditeur de LeetCode
> (il suffit de les déposer dans la classe `Solution`).

#### 5.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
Int public maxIntersectionCount(int[] y) {
// 1) fréquence de chaque paramètre
Carte<integer, integer> freq = nouveau HashMap<>();
Pour (int v : y) {
freq.put(v, freq.getOrDefault(v, 0) + 1);
}

// 2) carte de différence pour les intervalles de "croisement"
TreeMap<Integer, Integer> diff = nouvelle TreeMap<>();
pour (int i = 0; i + 1 < y.longueur; i++) {
int low = Math.min(y[i], y[i + 1]);
Int high = Math.max(y[i], y[i + 1]);

// il doit y avoir un entier strictement entre bas et haut
si (faible + 1 <= élevé - 1) {
diff.merge(faible + 1, 1, entier::sum);
diff.merge(haut, -1, entier::sum);
}
}

// 3) balayer dans l'ordre ascendant, continuer à courir la somme de diff
Int cur = 0;
int best = 0;
pour (Map.Entry<Integer, Integer> e : diff.entrySet() {
hauteur int = e.getKey();
cur += e.getValue(); // #segments traversant cette hauteur
intersections int = cur + freq.getOrDefault(hauteur, 0);
best = Math.max (best, intersections);
}

// Considérez également les hauteurs qui apparaissent seulement comme des paramètres
// (ils peuvent ne pas être présents dans la carte diff)
pour (Map.Entry<Integer, Integer> e : freq.entrySet() {
hauteur int = e.getKey();
intersections int = e.getValue(); // segments croisement = 0
best = Math.max (best, intersections);
}

le meilleur retour;
}
}
«» "

---

#### 5.2 Python (Python 3.10)

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxIntersectionCount(self, y: List[int]) -> Int:
# 1) fréquences des terminaux
freq = defaultdict(int)
pour v in y:
freq[v] += 1

# 2) carte des différences
diff = defaultdict(int)
pour a, b en zip(y, y[1:]):
faible, élevé = (a, b) si a < b autre (b, a)
si faible + 1 <= élevé - 1:
diff[faible + 1] += 1
Diff[haut] -= 1

# 3) balayage dans l'ordre trié
pour = 0
meilleur = 0
pour la hauteur triée(diff):
diff[hauteur]
intersections = cur + freq.get(hauteur, 0)
si les intersections > le meilleur:
meilleur = intersections

# 4) hauteurs qui n'apparaissent que comme des paramètres
pour la hauteur, compter en freq.item():
si compter > le meilleur:
meilleur = nombre

le meilleur retour
«» "

---

### 5.3 C++ (GNU‐C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxIntersectionCount(vecteur<int>& y) {
// 1) paramètres de comptage
unordered_map<int, int> freq;
pour (int v : y) freq[v]++;

// 2) carte de différence (triée)
carte <int, int> diff;
pour (size_t i = 0; i + 1 < y.size(); ++i) {
int low = min(y[i], y[i + 1]);
à l'intérieur supérieur = max(y[i], y[i + 1]);
si (faible + 1 <= élevé - 1) {
diff[faible + 1] += 1;
Diff[haut] -= 1;
}
}

// 3) balayage
Int cur = 0;
int best = 0;
pour (auto [hauteur, delta] : diff) {
pour delta;
intersections int = cur + freq[hauteur];
best = max (meilleur, intersections);
}

// 4) hauteurs qui n'existent que comme paramètres
pour (auto [hauteur, cnt] : freq) {
best = max (meilleur, cnt);
}

le meilleur retour;
}
};
«» "

---

- Oui. 6. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Fréquence du point d'extrémité de l'élément "O(n)" "O(k)" où `k` est le nombre de valeurs y distinctes (= n)
Carte des différences Autres
Autres Balayage et max. supplémentaire
**Total** Autres

L'algorithme s'inscrit confortablement dans les limites de LeetCode
tailles d'essai maximales.

---

- Oui. 7. Cas de bord et couverture des tests

Autres Description du test
- Oui.
Point unique
"y = [1, 2]"" Deux points avec un entier entre "1""
Tous égaux
"y = [1, 3, 2, 5]""
`y = [1, 100000000]` Grande lacune

Les solutions fournies traitent tout ce qui précède et plus encore.

---

- Oui. 7. Analogie du monde réel

Imaginez une rivière** avec des berges en hauteur 'y[i]'.
A **ferry** (la ligne horizontale) peut traverser la rivière à n'importe quel niveau d'eau.
L'algorithme indique :

1. **Combien de ferries se tiennent sur une banque** (points d'arrivée).
2. **Combien de segments de la rivière sont assez larges** pour que le ferry traverse
à un niveau donné (carte de différence).
3. ** Quel niveau donne le nombre maximum de bacs**.

Il le fait en marquant astucieusement les intervalles au lieu de vérifier chaque
niveau possible individuellement, comme un tableau **différence** qui maintient
suivi des changements aux points de départ et de fin.

---

- Oui. 8. Mots définitifs

L'idée clé est de **compresser** le problème:
nous n'avons pas besoin d'évaluer un nombre infini de hauteurs réelles;
Ensemble fini de limites entières matière.
La carte de la différence transforme chaque segment en une paire de mises à jour, et une seule
balai donne la réponse finale.

N'hésitez pas à copier, courir et tester les extraits.
Bon codage, et bonne chance sur LeetCode! C'est ce qu'il a dit.

---

Mots clés pour la recherche / Tags
- "intersections de ligne horizontale"
- Tableau de différence "
- "préfixe somme "
- "Plan de l'arbre"
- passage à niveau "
- passage à niveau "
- "intersections maximales" "
- Algorithme "O(n log n) "

---

Profitez de la résolution!