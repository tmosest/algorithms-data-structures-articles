---
titre: LeetCode 2941. GCD-Sum maximum d'une sous-marque -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Problème**
Compte tenu d'un tableau «nums» (1 ≤ len(nums) ≤ 2·105) et d'un entier «k» (1 ≤ k ≤ len(nums)), trouver un sous-réseau contigu dont la longueur est au moins «k» qui maximise

«» "
(somme de ses éléments) × (CMD de ses éléments)
«» "

Retourner la valeur maximale (utiliser l'arithmétique 64 bits).

-----------------------------------------------------------------------------------

Observations

* Pour un "r" à droite fixe, tous les GCD de sous-réseaux qui se terminent à "r" forment un très petit ensemble.
Le GCD ne peut **diminuer** que lorsque nous étendons la sous-couche vers la gauche, et chaque
temps qu'il change la valeur doit diviser la précédente.
Pour les nombres qui se produisent dans le tableau, le nombre de GCDs distincts qui peuvent
apparaît à tout moment est limité par **O(log V)** où `V = max(nums)`.
Dans la pratique, pour "V ≤ 106", il ne dépasse jamais 20.

* En raison de ce qui précède, nous pouvons garder au maximum une entrée pour chaque GCD possible
lors de la numérisation du tableau.
Pour chaque GCD, nous entreposons le sous-array **le plus long** (c'est-à-dire le plus grand
somme) qui a ce GCD et se termine à la position actuelle.

-----------------------------------------------------------------------------------

### Algorithme (GCD-List + Préfixe)

«» "
max_val = 0
stockage = {} // diviseur -> (somme, longueur)

pour i, x dans le dénombrement(nombres):
nouveau = {} // état après ajout de nombres[i]

// sous-recours composé uniquement de nombres[i]
nouveau[x] = (x, 1)
Si k == 1:
max_val = max(max_val, x * x)

// étendre chaque sous-array préalablement stocké avec nums[i]
pour g, (s, l) en magasin. items():
ng = gcd(g, x) // nouveau GCD après avoir ajouté x
ns = s + x
nl = l + 1
si nl >= k:
max_val = max(max_val, ng * ns)

// ne conserver que la plus longue sous-tribution pour ce GCD
si ng n'est ni nouveau ni nouveau[ng][1] < nl:
Nouveau[ng] = (n, nl)

magasin = nouveau

_retour maxval
«» "

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le maximum possible de GCD‐sum.

---

Lemma 1
Au début de la boucle itération pour index `i`, `store` contient, pour
chaque diviseur possible `d`, une paire `(s, l)` où `s` est la somme et `l` est
la longueur de **la plus longue** subdivision se terminant à la position «i‐1» dont GCD est
"d".

*Proof. *
L'initialisation (`i = 0`) est triviale: `store` est vide.
Supposons que le lemma soit utilisé pour l'indice "i".
Au cours de la prochaine itération, nous construisons «nouveau» comme suit:

* Pour chaque entrée `(s, l)` dans `store` nous étendons cette sous-entente avec
«nums[i]». Le nouveau GCD est «gcd(d, nums[i]».
Nous conservons seulement l'entrée avec la longueur **maximum** pour chaque GCD résultant,
Ainsi, après le traitement de toutes les entrées `new` satisfait le lemma pour l'index `i`.

* Nous insérons également la sous-tribu de la longueur 1 se terminant à «i»; c'est la seule
sous-tribunal dont le GCD est égal à «nums[i]» qui se termine à "i".
Par conséquent, le lemma tient aussi après avoir défini `store = new`.



Lemma 2
Pendant le traitement de l'index `i` l'algorithme examine la valeur
`G × S` pour **chaque** sous-tribu qui se termine à `i`, où
«G = GCD(sub‐array)» et «S = somme(sub‐array)».

*Proof. *
Considérez toute sous-tribution «nums[l ... i]».
Par Lemma 1 lorsque la boucle pour `i` est entrée, `store` contient une entrée
avec GCD égal à «gcd(nums[l ... i‐1]»)» et longueur «i‐l».
Lorsque nous prolongeons cette rubrique par `nums[i]`, le GCD devient `gcd(G, nums[i]`,
qui est exactement le GCD de l'ensemble de la sous-tribu.
Sa longueur augmente à «i‐l+1» et sa somme à «S».
Ainsi, l'algorithme calculera `G × S` pour ce sous-réseau. *



Lemma 3
Pour chaque sous-aire de longueur au moins `k`, les mises à jour de l'algorithme
`max_val` avec son GCD-sum.

*Proof. *
Par Lemma 2 l'algorithme calcule `G × S` pour le sous-réseau.
Le contrôle `si nl >= k` garantit que nous ne considérons que les sous-tribus de
longueur requise avant la mise à jour `max_val`.



C'est vrai. Théorème
Après la dernière itération `max_val` égale le maximum possible
`(somme des éléments) × (CMD des éléments)` sur tous les sous-groupes contigus de
longueur au moins "k".

*Proof. *
De Lemma 3 chaque sous-entente admissible contribue à
`max_val`, donc `max_val` est ** au moins** le meilleur.
Inversement, `max_val` n'est mis à jour qu'avec des valeurs de sous-ensembles éligibles,
C'est donc ** au maximum** l'optimum.
Par conséquent, les deux sont égaux. *



-----------------------------------------------------------------------------------

Analyse de complexité

Laisser `V = max(nums)`.

* `gcd` fonctionne dans le temps `O(log V)`.
* Chaque élément est combiné avec au plus `O(log V)` des GCD distincts (le jeu
la taille ne dépasse jamais ~20 pour 106).
Ainsi, chaque itération coûte "O(log V)".

«» "
Durée : O(n · log V)
Mémoire : O(log V) (le dictionnaire des GCD)
«» "

Les deux limites satisfont facilement aux limites.

-----------------------------------------------------------------------------------

### Mise en oeuvre de la référence (Python 3)

'`python
d'importation de mathématiques gcd
de collections importer par défautdict
de taper l'importation Liste

def max_gcd_sum(nums: List[int], k: int) -> Int:
max_val = 0
stockage = {} # diviseur -> (somme, longueur)

pour x en nombres:
nxt = defaultdict(lambda: (0, 0))

# sous-arraisonnement de la longueur 1
nxt[x] = (x, 1)
Si k == 1:
max_val = max(max_val, x * x)

# Étendre tous les sous-réseaux précédemment stockés
pour g, (s, l) en magasin. items():
ng = gcd(g, x)
ns = s + x
nl = l + 1
si nl >= k:
max_val = max(max_val, ng * ns)

# Ne gardez que la plus longue sous-tribu pour ce diviseur
si nxt[ng] < (n, nl):
nxt[ng] = (n, nl)

stockage = nxt

_retour maxval
«» "

La fonction suit exactement l'algorithme prouvé correct ci-dessus et
fonctionne dans le temps requis pour les contraintes données.