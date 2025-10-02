---
Titre: LeetCode 894. Tous les arbres binaires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Le problème**
Pour un nombre impair `n` nous devons retourner *tous* arbres binaires complets distincts qui contiennent des nœuds `n`.
Si nous construisons les arbres en réutilisant des sous-arbres que nous avons déjà créés, les arbres que nous retournons finissent par partager des nœuds (les arbres dits *Frankenstein*).
Quand un appelant mute l'un des arbres retournés, il mute silencieusement les autres – un comportement auquel la plupart des clients ne s'attendaient pas.

La seule façon sûre de satisfaire le contrat est de **cloner chaque sous-arbre avant qu'il soit attaché à une nouvelle racine**.
Vous pouvez conserver la structure originale (partagée) dans une table de mémoisation pour éviter la recomputation, mais lorsque vous formez réellement la liste que vous retournez, vous devez dupliquer la structure de l'arbre.

Voici une implémentation Python concise et entièrement documentée qui fait exactement cela.

---

- Oui. 1. Idées

1. **Numéros d'ordre seulement** – un arbre binaire complet peut avoir seulement un nombre impair de nœuds.
2. **Memoise** – une fois que nous avons produit tous les arbres pour un `n` particulier, nous stockons le résultat dans un dictionnaire afin que les appels plus tard pour le même `n` puissent retourner la liste mise en cache instantanément.
3. **Construire à partir de sous-arbres** – pour chaque scission impair `i` (nœuds à gauche) et `n‐1‐i` (nœuds à droite) nous combinons chaque arbre à gauche avec chaque arbre à droite en créant une toute nouvelle racine.
4. **Clone** – chaque fois que nous combinons une paire, nous copieons les sous-arbres gauche et droit afin que les arbres qui en résultent soient indépendants.

---

- Oui. 2. Complexité

*Laissez `T(n)` être le nombre d'arbres binaires pleins avec `n` noeuds. *

«» "
T(1) = 1
T(n) = γ_{i impair, 1φi<n} T(i) · T(n‐i‐1) (n impair)

«» "

La séquence se développe comme les nombres catalans:
«T(1)=1, T(3)=1, T(5)=2, T(7)=5, T(9)=14, ...»

* **Time** – chaque arbre est construit une fois et stocké dans la table de mémorisation.
Le nombre d'opérations asymptotiques est de 2 %.
* **Espace** – la table de mémoisation contient tous les arbres jusqu'à la taille `n`.
La profondeur de récursion la plus profonde est `n/2`, de sorte que l'espace auxiliaire est l'"n".

---

- Oui. 3. Code

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

de taper l'importation Liste, numéro

Solution de classe:
# cache: n → liste de tous les arbres binaires avec n nœuds
_cache: Dict[int, List['TreeNode']] = {}

def allPossibleFBT(self, n: int) -> Liste['TreeNode']:
# arbre binaire complet existe seulement pour impair n
si n % 2 == 0:
retour []

# résultat mémorisé
si n en soi._cache:
_cache[n]

résultat: Liste['TreeNode'] = []

si n] 1 :
# case de base – un seul arbre de nœuds
résultat.append(TreeNode(0))
Sinon:
# diviser les nœuds n‐1 restants en deux parties impaires
pour gauche_cnt dans l'intervalle(1, n, 2):
droite_cnt = n - 1 - gauche_cnt
gauche_trees = self.allPossibleFBT(left_cnt)
right_trees = self.allPossibleFBT(right_cnt)

# combiner chaque gauche avec chaque droite
pour l dans les _arbres de gauche:
pour r in right_trees:
# Copier en profondeur les deux sous-arbres avant de fixer
racine = TreeNode(0, self._clone(l), self._clone(r))
résultat.append(root)

# Souvenez-vous du résultat pour les appels futurs
self._cache[n] = résultat
résultat du retour

# --------- aide: copie profonde d'un arbre...
def _clone(self, node: 'TreeNode') -> 'TreeNode':
"""Retourne une copie profonde du sous-arbre enraciné au nœud."""
si le nœud n'est pas :
retour Aucune
# créer un nouveau noeud et des enfants clonés récursivement
retour TreeNode(0, self._clone(node.left), self._clone(node.right))
«» "

- Oui. Pourquoi le `_clone` explicite?

*Si vous l'avez fait **non** clone*:

'`python
racine = TreeNode(0, l, r) # <-- l et r réutilisés
«» "

vous attachez les objets * même* `TreeNode` à de nombreuses racines différentes.
Ces arbres ne seraient pas indépendants; ils formeraient une structure de Frankenstein.

Cloning garantit que chaque appel à `self._clone` retourne un sous-arbre neuf, de sorte que l'appelant peut modifier librement n'importe quel arbre de la liste de résultats sans affecter les autres.

---

- Oui. 4. Un bref contrôle de la santé mentale

'`python
sol = Solution()
arbres = sol.allPossibleFBT(5) # 2 arbres

# muter la feuille la plus à gauche du premier arbre
arbres[0].gauche.gauche.val = 42

# le deuxième arbre est inchangé – nous avons vraiment cloné
print(trees[1].left.val) # still 0
«» "

Si vous avez omis l'étape du clonage, le deuxième arbre montrerait la valeur mutée `42`, prouvant que les nœuds partagés avaient été brisés.

---

- Oui. 5. Pourquoi LeetCode accepte parfois des solutions non fermées

LeetCode vérifie seulement que la forme* des arbres retournés correspond au nombre prévu.
Le harnais de test ne mute jamais aucun noeud après le retour de la fonction, donc une solution qui réutilise simplement les sous-arbres en cache (« TreeNode(0, l, r) ») passe tous les tests.

Cependant, dans le code de production (ou quand vous voulez une bibliothèque robuste), vous ne pouvez pas supposer que les appelants ne modifieront jamais les arbres retournés.
La stratégie du clone avant l'attachement présentée ci-dessus est la manière correcte et sans effets secondaires de mettre en œuvre le contrat.