---
titre: LeetCode 3337. Total des caractères dans les chaînes après les transformations II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Objectif**

Après les transformations `t` la chaîne peut être astronomiquement longue (jusqu'à 25n).
Nous avons seulement besoin de sa longueur – c'est le nombre total de caractères présents après tout
Les transformations.
La principale observation est que l'arrangement *exacte* des caractères n'est pas pertinent,
seulement combien de chacune des 26 lettres existent.
Si nous pouvons calculer la fréquence finale de chaque lettre, les résumer donne le
répondre.

-----------------------------------------------------------------------------------

- Oui. 1. Compter les lettres dans la chaîne de départ

«» "
cnt[i] = nombre d'occurrences de la lettre i-e (a → 0, ... , z → 25)
«» "

Cela nécessite "O(=)" temps et est le seul endroit où la chaîne d'origine est
inspecté.

-----------------------------------------------------------------------------------

- Oui. 2. Comment une lettre change-t-elle?

Pour une lettre `c` (0...25), on nous donne `nums[c] = k`.
Lors d'une transformation, `c` est remplacé par les lettres `k` suivantes
alphabet (enroulement autour).
Donc en une seule étape:

«» "
c → (c+1) mod 26
c → (c+2) mod 26
...
c → (c+k) mod 26
«» "

-----------------------------------------------------------------------------------

- Oui. 3. Matrice de transition

Nous construisons une matrice 26 × 26 **T** où

«» "
T[i][j] = nombre de lettres j produites à partir d'une seule lettre i en une seule étape
«» "

Pour chaque `i` (lettre) et chaque `x = 1 ... nombres[i] "

«» "
suivant = (i + x) mod 26
T[i][suivant] += 1
«» "

La matrice contient déjà l'effet de l'enroulement, et chaque entrée
est 0 ou 1 (parce que chaque lettre produite est unique en une seule étape).

-----------------------------------------------------------------------------------

- Oui. 4. Plusieurs étapes – exponentiation rapide

Après les étapes `t` une seule lettre `i` produit une distribution donnée par le
`i`-ième rangée de **T(t)** (la matrice T est montée à la puissance `t`).
Toute la transformation de la chaîne est

«» "
_comptes définitifs = cnt · T(t)
«» "

(«cnt» est traité comme un vecteur de rangée).

Pour calculer `T(t)` nous utilisons une exponentiation binaire:

«» "
résultat = matrice I // identité
puissance = t
alors que puissance > 0
si la puissance est un résultat impair = résultat · T
T = T · T
puissance = puissance / 2
«» "

La taille de la matrice est seulement 26, donc une multiplication prend
`263 ☆ 17 576` opérations scalaires – trivial pour un ordinateur.
Nous l'exécutons `O(log t)` fois, qui est au plus 30 multiplications pour
«t ≤ 109».

Tout arithmétique est effectué modulo `MOD = 1 000 000 007` pour éviter les débordements.

-----------------------------------------------------------------------------------

- Oui. 5. Appliquer la matrice alimentée aux fréquences initiales

«» "
pour i en ...25
pour j en ...25
_comptes finals[j] += cnt[i] * T(t)[i][j] (mod MOD)
«» "

Seules les opérations " 262 " sont nécessaires.

-----------------------------------------------------------------------------------

- Oui. 6. Résultat

La réponse est le nombre total de lettres après toutes les transformations :

«» "
réponse = somme (comptes définitifs) mod MOD
«» "

-----------------------------------------------------------------------------------

- Oui. 7. Complexité

Étape Temps Mémoire
C'est ce qu'on dit.
Compter "cnt" Autres
Bâtiment
Description de la matrice
Vecteur × matrice Autres
Montant final

Le terme dominant est l'expression de la matrice; tout le reste est négligeable.

-----------------------------------------------------------------------------------

- Oui. 8. Pourquoi cela fonctionne

- **Linéarité** – Le nombre de chaque lettre après une étape est linéaire
combinaison des nombres avant l'étape; matrices codent exactement que
transformation linéaire.
- **Pouvoir d'une matrice** – Répéter la même étape linéaire "t" temps est le
la même chose que l'application de la matrice `t` times, c'est-à-dire la multiplication par `T(t)`.
Une exponentiation rapide calcule `T(t)` dans le temps logarithmique.
- **Modulo** – Les nombres grandissent de façon exponentielle; l'utilisation du module maintient tout
résultats intermédiaires limités.
- **Pas de construction de cordes** – Nous ne construisons jamais la corde gigantesque; nous ne faisons que
Gardez 26 compteurs.

-----------------------------------------------------------------------------------

**Résultat:**
En comptant les lettres initiales, en construisant la matrice de transition, en l'élevant à
le pouvoir `t`, en l'appliquant aux nombres initiaux, et en additionnant le résultat
fréquences, nous obtenons la longueur de la chaîne après les transformations `t`,
modulo «1 000 000 007».