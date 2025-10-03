---
Titre: LeetCode 1120. Sous-arbre moyen maximum -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Sous-arbre moyen maximal – LeetCode 1120
**Le bon, le mauvais et le mauvais – Un guide de préparation à l'emploi (Java, Python, C++)* *

> **Mots clés:**
> *Python*, *C++*, *Algorithme*, *Problème d'entrevue*, *Entretien d'embauche*, *Codification*

---

- Oui. 1. Exposé des problèmes

Compte tenu de la racine d'un arbre binaire, retourner la valeur moyenne maximale d'un sous-arbre de cet arbre.
Un *subtree* est un nœud plus tous ses descendants.
La valeur moyenne d'un arbre est la somme de ses valeurs de nœuds divisées par le nombre de nœuds.
Les réponses dans les 10 à 5 de la réponse réelle seront acceptées.

**Contrôles* *

Valeur
-- -- -- -- -- --
Nombre de nœuds Autres
0 ≤ Nœud.val ≤ 105

---

- Oui. 2. Pourquoi ce problème est important

- **Tree traversal mastery** – les intervieweurs aiment voir si vous pouvez faire un DFS après-commande correctement.
- ** Précision du point de flot** – les moyennes de manipulation exigent une utilisation prudente du "double".
- ** compromis entre l'espace et le temps** – l'approche naïve peut atteindre des limites de récursion ou des dépassements.

---

- Oui. 3. Le bon – une solution récursive propre

La perspicacité fondamentale : **procéder chaque sous-arbre une fois** et propager deux valeurs vers le haut :

1. **sum** – total de toutes les valeurs de nœuds dans le sous-arbre
2. **compte** – nombre de nœuds dans le sous-arbre

Avec ceux-ci, la moyenne de ce sous-arbre est simplement "somme/compte".
Tout en traversant, nous gardons un maximum mondial.

Complexité

Temps Espace
C'est le cas.
Chaque noeud visité une fois. Autres

---

- Oui. 4. Les mauvaises – Pièges que vous devriez éviter

Pourquoi c'est un problème
C'est le cas.
**Modifier les valeurs des nœuds** en place. Calculer les sommes séparément. Autres
**Utiliser `int` pour la somme** → convient encore, mais plus sûr d'utiliser `long`. Autres
**Profondeur de récursifs > limite de récursions**=Python peut atteindre une limite de récursions (par défaut ~1000). Autres Utilisez le DFS itératif ou augmentez la limite de récursion (sys.setrecursionlimit). Autres
**Les erreurs de point de flottement**. Monter à "double" avant la division. Autres
**Bogues de l'état mondial** Passer `maxA moyenne` par référence ou utiliser un champ qui réinitialise. Autres

---

- Oui. 5. Les cas laids – Manipulation des bords

C'est un défi.
C'est le cas.
Autres **Tous les nœuds ont la même valeur**= Chaque sous-arbre a la même moyenne; l'algorithme fonctionne toujours. Pas besoin de manipulation spéciale. Autres
**Tree avec un seul noeud**= La moyenne est que la valeur de nœuds; la récursion doit revenir correctement. Le cas de base renvoie `sum = val`, `count = 1`. Autres
Autres **Arbre très profond** Utilisez l'optimisation queue-récursion (non disponible en Java/Python) ou la pile itérative. Autres
**Plus grand nombre de nœuds** Le DFS linéaire est garanti. Autres

---

- Oui. 6. Extraits de code

Ci-dessous sont **trois implémentations idiomatiques** qui compilent sur LeetCode et la plupart des plateformes d'entrevue.

#### 6.1 Java

"Java
***
* Définition d'un noeud d'arbre binaire.
* classe publique TreeNode {
* Int val;
* TreeNode gauche;
* TreeNode droit;
* TreeNode() {}
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode gauche, TreeNode droite) {
* ce.val = valeur;
* ce.gauche = gauche;
* ce droit = droit;
*}
*}
*/
solution de classe {
privé double maxMoyenne = Double. _INFINITÉ NÉGATIVE;

public double maximum Sous-arbre moyen(racine de nœud d'arbre) {
dfs(racine);
retour maxMoyenne;
}

// Retourne {sum, compter}
privé long[] dfs(noeud TreeNode) {
si (noeud == null) retourne un nouveau long[]{0, 0};

long[] gauche = dfs(node.gauche);
longue[] droite = dfs(node.right);

somme longue = gauche[0] + droite[0] + noeud.val;
longueur = gauche[1] + droite[1] + 1;

double avg = (double) somme / nombre;
maxMoyenne = Math.max(maxMoyenne, avg);

retourner un nouveau long[]{sum, compter};
}
}
«» "

6.2 Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
def maximum MoyenneSous-arbre(même, racine: TreeNode) -> flotteur:
auto.max_avg = flotteur('-inf')
Auto.dfs(racine)
retour self.max_avg

def dfs(self, noeud: TreeNode):
si ce n'est pas le nœud:
retour 0, 0 # somme, nombre

gauche_sum, gauche_cnt = self.dfs(node.left)
right_sum, right_cnt = self.dfs(node.right)

total_sum = gauche_sum + droite_sum + noeud.val
total_cnt = gauche_cnt + droite_cnt + 1

Self.max_avg = max(self.max_avg, total_sum / total_cnt)
retourner total_sum, total_cnt
«» "

*### 6.3 C++

'`cpp
***
* Définition d'un noeud d'arbre binaire.
* struct TreeNode {
* Int val;
* TreeNode * gauche;
* TreeNode *right;
* TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
* };
*/
solution de classe {
public:
double maximum Sous-arbre moyen(racine TreeNode*) {
maxAvg = -std::numérique_limits<double>::infini();
dfs(racine);
retour maxAvg;
}

particulier:
double maxAvg;

// retourne la paire <somme, nombre>
md::pair <long long, int> dfs(noeud TreeNode*) {
si (!node) retourne {0, 0};

auto gauche = dfs(node->gauche);
auto right = dfs(node->right);

somme longue = gauche. premier + droite.premier + noeud->val;
int count = gauche. deuxième + droite.deuxième + 1;

maxAvg = md:max(maxAvg, static_cast<double>(sum) / nombre);
retour {somme, nombre};
}
};
«» "

---

- Oui. 7. Comment les intervieweurs pourraient demander

Question: Qu'est-ce qu'ils probent vraiment?
-- -- -- -- -- --
Autres Pouvez-vous expliquer comment vous évitez de recalculer les sommes du sous-arbre? Attendez DFS avec mémoisation de la somme et du nombre. Autres
Autres Et si l'arbre est biaisé ? La récursion va-t-elle exploser ? Connaître la profondeur de récursion = hauteur, discuter des alternatives itératives. Autres
Pourquoi avez-vous utilisé `double` au lieu de `float`? Précision et tolérance au LeetCode. Autres
Autres Comment l'adapter pour trouver le sous-arbre avec la moyenne minimale ? La logique miroir avec `min`. Autres

---

- Oui. 8. Fermeture optimisée par le SEO

Si vous vous préparez pour votre prochain **entretien d'ingénierie logiciel**, la maîtrise du problème **Moyenne maximale du sous-arbre** montre que vous pouvez:

1. **Arbres binaires inversés** efficacement (DFS, post-commande).
2. ** Précision numérique manuelle** avec soin.
3. **Écrire un code propre et durable** en Java, Python et C++.

N'hésitez pas à copier les extraits ci-dessus, à les exécuter sur LeetCode et à les modifier pour obtenir de la vitesse.
N'oubliez pas d'expliquer l'intuition, la complexité et les cas de bord pendant votre entrevue – ce sont les *bonnes* parties qui impressionnent les gestionnaires d'embauche.

Bon codage, et la meilleure chance d'atterrir ce travail de rêve! C'est ce qu'il a dit.

---