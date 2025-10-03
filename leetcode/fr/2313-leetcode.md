---
titre: LeetCode 2313. Flips minimum dans l'arbre binaire pour obtenir un résultat -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2313 – Flips minimum dans l'arbre binaire pour obtenir un résultat
**Une plongée profonde dans un problème dur de LeetCode (Java, Python et C++)* *

---

Table des matières

Lien
- Oui.
Aperçu du problème
Solution rapide Autres
Algorithme détaillé
#complexité
Code – Java
Code – Python
Code – C++
Le bon, le mauvais, et l'hugly
Comment cela aide votre recherche d'emploi
Réflexions finales

---

## Aperçu du problème <a name="problem-overview"></a>

Vous êtes donné un arbre binaire enraciné où:

Valeur du nœud
C'est quoi ?
Autres La feuille, évalue à **faux**
Autres La feuille, évalue à
**2**
Autres (deux enfants)
Autres **4**************************************************************************************************************************************************************************************************************************************************************
Autres **5**

Vous pouvez **déplier n'importe quelle feuille** (0 ↓ 1).
Votre objectif : trouver le nombre minimum de flips** qui font l'évaluation de la racine à un « résultat » booléen donné.
Elle garantit qu'une solution existe toujours.

Contraintes:
- 1 ≤ #noeud ≤ 105
- 0 ≤ nœud.val ≤ 5

---

## Solution rapide <un nom="solution rapide"></a>

**Bottom-up DFS** qui retourne, pour chaque nœud, un 2-tuple:

«» "
[FlipsBeBeFalse, flipsBeFalse]
«» "

- Pour une feuille : 0 retourne si sa valeur correspond déjà au booléen désiré, sinon 1.
- Pour les nœuds internes : combiner les deux tuples enfants selon l'opération logique.

La réponse est `résultat ? root[1] : root[0]`.

La solution fonctionne en **O(N)** temps et utilise **O(H)** espace de cheminée (H = hauteur de l'arbre, ≤ N).

---

## Algorithme détaillé <un nom="algorithme"></a>

- Oui. 1. Que calculer à chaque nœud?

Pour chaque nœud, nous avons besoin de deux nombres :

Résultats désirés
- Oui.
CostFalse Autres
"Vrai" "CostTrue" Autres

Nous calculons ces nombres en un seul passage post-commande.

- Oui. 2. Cas de base – Feuille

Une feuille n'a pas d'enfants.

Valeur actuelle des feuilles
-- -- -- -- -- -- -- -- -- -- -- -- -- --
0 (faux)
1 (vrai)

Mise en œuvre

'`python
en cas de nœud. gauche est Aucun et noeud. droite est None: # feuille
costFalse = 0 si node.val == 0 autre 1
costTrue = 0 si node.val == 1 autre 1
«» "

- Oui. 3. Répétition – Noeuds internes

Que `L = [lf, lt]` et `R = [rf, rt]` soient les tuples de l'enfant de gauche et de droite
(«il»/«pas» peut être «Aucun» pour un noeud NON).

Type de nœuds
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**OR** (2) Exclusivité «LOR R» Autres
**ET** (3) , `L ET R` , `min(lf, rf)` , `lt + rt` Autres
**XOR** (4)="L XOR R"="min(lf + rt, lt + rf)="min(lf + rt, lt + rf)="? Attendez qu'on soit prudents. Autres
**NOT** (5)NOT L` (un seul enfant) Autres

Dérivés corrects

`XOR` est vrai lorsque les deux opérandes diffèrent, faux quand ils sont égaux.

«» "
costTrue = min( lf + rt, lt + rf ) # gauche faux & droite vrai OU gauche vrai & droit faux
coûtFalse = min( lf + rt, lt + rf )? Attendre la même chose ? C'est pas vrai.

coûtFalse = min( lf + rt, lt + rf )? En fait, les résultats sont égaux :

- Les deux faux: lf + rf
- Les deux vrai : lt + rt
Donc :

CoûtFalse = min( lf + rf, lt + rt)
CoûtTrue = min( lf + rt, lt + rf )
«» "

C'est la formule finale.

- Oui. 4. Conseils de mise en œuvre

- Utilisez "int" partout. Les flips maximums nécessaires peuvent dépasser le nombre de feuilles 105.
- La profondeur de récursion peut atteindre 105 dans un arbre dégénéré; la plupart des environnements d'entretien le permettent, mais vous pouvez passer à une pile explicite si nécessaire.
- Pour le nœud NON, un seul enfant est présent – vérifiez lequel n'est pas `Aucun'.

---

## Analyse de complexité <un nom="complexité"></a>

Valeur métrique
C'est pas vrai.
Temps **O(N)** – chaque noeud est traité une fois. Autres
Espace **O(H)** – profondeur de la cheminée de récursion; pire cas O(N). Autres

---

## Code – Java <a name="java"></a>

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
Int minimum public Flips(racine de nœud d'arbre, résultat booléen) {
coût int[] = dfs(root);
? coût[1] : coût[0];
}

Int[] dfs (noeud TreeNode) {
// Feuille
Si (noeud.left) null && node.right == null) {
int costFalse = noeud.val == 0 ? 0 : 1;
Int costTrue = noeud.val == 1 ? 0 : 1;
retour de nouveau int[]{costFalse, costTrue};
}

// Noeud interne
int[] left = noeud.left != null ? dfs(node.left) : null;
int[] right = noeud.right != null ? dfs(node.right) : null;

commutateur (node.val) {
Cas 2: // OU
retour nouveau int[] {
gauche[0] + droite[0], // faux
Math.min(gauche[1], droite[1]) // vrai
};
Décision 3: // ET
retour nouveau int[] {
Math.min(gauche[0], droite[0]), // faux
gauche[1] + droite[1] // vrai
};
Décision 4: // XOR
retour nouveau int[] {
Math.min(gauche[0] + droite[0], gauche[1] + droite[1]), // faux
Math.min(gauche[0] + droite[1], gauche[1] + droite[0]) // vrai
};
cas 5: // NON – un seul enfant existe
int[] child = gauche != Null ? gauche : droite;
retour de nouveau int[]{enfant[1], enfant[0]}; // coûtFalse = vrai de l'enfant, etc.
par défaut & #160;:
lancer un nouvel argument illégalException("Valeur de nœud invalide");
}
}
}
«» "

---

## Code – Python <un nom="python"></a>

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
def minimum Flips(même, racine: TreeNode, résultat: bool) -> Int:
coût = auto_dfs(root)
coût de retour[1] si le résultat est autre coût[0]

def _dfs(self, node: TreeNode) -> list[int]:
# Feuille
si nœud.left n'est ni rien. droit n'est pas:
costFalse = 0 si node.val == 0 autre 1
costTrue = 0 si node.val == 1 autre 1
retour [costFalse, costTrue]

# Récursez les enfants
gauche = self._dfs(node.left) si noeud. gauche autre Aucune
droite = self._dfs(node.right) si node.right autre Aucune

si noeud.val == 2: # OU
retour [gauche] + droite],
min(gauche[1], droite[1])]
si noeud.val == 3: # ET
retour [min(gauche[0], droite[0]),
gauche[1] + droite[1]]
si noeud.val == 4: # XOR
retour [min(gauche[0] + droite[0], gauche[1] + droite[1]),
min(gauche[0] + droite[1], gauche[1] + droite[0])]
si noeud.val == 5: # PAS
enfant = gauche si gauche n'est pas Aucun autre droit
retour [enfant[1], enfant[0]] # faux coût = enfant vrai, vrai coût = enfant faux
«» "

---

Code – C++ <a name="cpp"></a>

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
Int minimum Flips(racine TreeNode*, résultat bool) {
coût automatique = dfs(root);
résultat du retour ? coût.deuxième: coût.première;
}

particulier:
couple<int,int> dfs(nœud TreeNode*) { // {costFalse, costTrue}
si (!node->left &&!node->right) { // feuille
Int costFalse = (noeud->val) 0) ? 0 : 1;
Int costTrue = (node->val) 1) ? 0 : 1;
retour {coût Faux, CostTrue};
}

couple<int,int> L = noeud->gauche ? dfs(node->gauche) : paire<int,int>{0,0};
couple <int,int> R = noeud->droit ? dfs(node->droit) : paire<int,int>{0,0};

interrupteur (noeud->val) {
Cas 2: // OU
retour {L.first + R.first,
min(L.seconde, R.seconde)};
Décision 3: // ET
retour {min(L.first, R.first),
L.seconde + R.seconde};
Décision 4: // XOR
retour {min(L.first + R.first, L.seconde + R.seconde),
min(L.first + R.seconde, L.seconde + R.first)};
Cas 5: // NON
retour {L.second, L.first}; // un seul enfant n'est pas null
par défaut & #160;:
lancer invalide_argument("Valeur de noeud invalide");
}
}
};
«» "

---

## Le bon, le mauvais, et le mauvais nom <un nom</a>

Qu'est-ce qui a marché ?
- C'est quoi ?
**Bon**=1=1=1 Le PDD ascendant élimine le besoin de tables de mémo. Un passage donne *deux* réponses (faux/vrai) donc le dernier `si (résultats)` est trivial. Toutes les formules sont O(1) par noeud → temps linéaire.
La profondeur de la récursion peut atteindre 105 – débordement de la pile sur de très vieux juges. Les formules XOR sont un écueil commun* ; beaucoup de candidats écrivent la mauvaise logique de "same vs. different".
**Les valeurs de nœuds codés à code dur (2–5) masquent l'intention; une carte des valeurs enum peut rendre le code plus propre. En oubliant que les nœuds NOT ont *un* enfant peut conduire à des exceptions de null-pointer.

> **Ligne de bottom:** L'algorithme est élégant et rapide, mais le diable est dans les formules. Testez la logique XOR avec quelques arbres fabriqués à la main avant de soumettre.

---

## Comment cela aide votre recherche d'emploi <un nom="chasse d'emploi"></a>

1. **Interview-Ready Pattern**
- *Binaire + fond-up DP* est un modèle d'entrevue classique. Maîtriser les signaux vous permet de gérer les problèmes de transition d'état récursif.

2. **LeetCode Maîtrise dure* *
- Résoudre ce problème vous rapporte un badge dur** sur LeetCode, boostant votre CV et votre profil GitHub.

3. **Java/Python/C++ Présentation**
- Trois implémentations montrent une pensée linguistique-agnostique – un plus pour les rôles **complet** ou **design-système**.

4. ** Clarté algorithmique**
- Une analyse claire du pseudocode + de la complexité montre que vous pouvez communiquer des idées aux gestionnaires et aux coéquipiers.

5. ** Mots clés du référencement* *
- Si les recruteurs recherchent des problèmes d'arborescence binaires d'interview de Java* ou de LeetCode des solutions dures de Java*, cet article se classe au premier rang grâce à des rubriques ciblées et des explications riches en mots clés.

---

## Réflexions finales <un nom="final"></a>

*Flips mineurs dans l'arbre binaire pour obtenir le résultat* est plus qu'un défi de codage – c'est un micro-écosystème de récursion, de programmation dynamique et de raisonnement logique.
Le modèle DFS‐DP que nous avons utilisé est réutilisable pour de nombreuses questions d'entrevue basées sur les arbres (p. ex., *Profondeur minimale*, *Path Sum maximale*, *House Robber III*).

** Continuer à pratiquer** :

- Essayez les variations (p. ex., les feuilles K au maximum, les flip sets distincts).
- Optimisez l'espace : implémentez une traversée itérative post-commande si la profondeur de la pile vous inquiète.
- Expliquez votre processus de pensée à haute voix; cela reflète les conditions réelles d'entretien.

Bon codage – et bonne chasse! C'est ce qu'il a dit