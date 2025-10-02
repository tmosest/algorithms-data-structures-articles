---
titre: LeetCode 2096. Instructions étape par étape d'un noeud d'arbre binaire à un autre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Résoudre les directions étape par étape d'un noeud d'arbre binaire à un autre

Ci-dessous sont trois solutions complètes, prêtes à la copie – une en **Java**, **Python** et **C++**.
Tous les trois utilisent la même approche fondée sur la DSV :

1. Construire le chemin de la racine vers le noeud *start* (`sPath`).
2. Construire le chemin de la racine vers le nœud *destination* (`dPath`).
3. Supprimer le suffixe commun (la partie qui appartient à l'ancêtre commun le plus bas).
4. Convertir le reste de `sPath` en `U`s et ajouter le `dPath` inversé.

Chaque implémentation est entièrement commentée et suit la signature de la méthode LeetCode.

---

#### 1.1 Java (Signature de code à gauche)

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
/** Aide DFS qui ajoute 'L' ou 'R' à sb comme il recule. */
Trouvé booléen privé (noeud TreeNode, cible int, StringBuilder sb) {
si (node.val == cible) retourne vrai;
si (node.left != null && findPath(node.left, cible, sb) {
sb.annexe('L');
retour vrai;
}
si (node.right != null && findPath(node.right, cible, sb) {
sb.annexe('R');
retour vrai;
}
retourner false; // cible non trouvée dans ce sous-arbre
}

public Chaîne getDirections(Rot TreeNode, int start Valeur, int destValue) {
StringBuilder sPath = nouveau StringBuilder();
StringBuilder dPath = nouveau StringBuilder();

findPath(root, début Valeur, sPath);
findPath(root, det Valeur, dPath);

// Supprimer le suffixe commun (partie LCA)
i = 0;
pendant que (i < Math.min(sPath.longueur(), dPath.longueur())
&& sPath.charAt(sPath.longueur() - 1 - i) == dPath.charAt(dPath.longueur() - 1 - i)) {
i++;
}

// Partie restante du chemin de départ → 'U's
StringBuilder up = nouveau StringBuilder();
pour (int j = 0; j < sPath.length() - i; ++j) up.append('U');

// Partie restante du chemin du destin → inversé
dPath.reverse();
Résultat StringBuilder = nouveau StringBuilder(up);
result.append(dPath.substring(i));

retour résultat.àString();
}
}
«» "

> **Pourquoi cette implémentation Java est-elle rapide ? * *
> * Le DFS fonctionne en **O(n)** – il visite chaque nœud au plus deux fois.
> * Le `StringBuilder` pousse linéairement avec la profondeur de l'arbre, n'affectant jamais de grandes chaînes intermédiaires.

---

#### 1.2 Python 3 (Signature de code leet)

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init__(self, val=0, gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def _find_path(self, noeud: TreeNode, cible: int, chemin: list) -> C'est vrai.
"""DFS qui ajoute 'L' ou 'R' à la trajectoire arrière."""
si noeud.val == cible:
retour Vrai
i node.left et self._find_path(node.left, cible, chemin):
chemin.append('L')
retour Vrai
i node.right et self._find_path(node.right, cible, chemin):
chemin.append('R')
retour Vrai
Retour Faux

def getDirections(self, root: TreeNode, start Valeur: int, destValue: int) -> str:
s_path, d_path = [], []

Self._find_path(root, démarrage Valeur, s_path)
Self._find_path(root, destValue, d_path)

# Supprimer le suffixe commun (partie LCA)
alors que s_path et d_path et s_path[-1] == d_path[-1] :
_path.pop()
d_path.pop()

retourner 'U' * len(s_path) + ''.join(reversed(d_path))
«» "

> **Python tip** – Utiliser une liste pour le chemin garde la mutation bon marché et évite la concaténation coûteuse des chaînes à l'intérieur de la récursion.

---

*## 1.3 C++ (LeetCode Signature)

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
// helper DFS : retourne true si la cible est trouvée, ajoute la direction au chemin
bool dfs(Nœud TreeNode*, cible int, chaîne &path) {
si (!node) retourner faux;
si (node->val == cible) retourne true;

si (dfs(node->gauche, cible, chemin)) {
path.push_back('L');
retour vrai;
}
si (dfs(node->right, cible, chemin)) {
path.push_back('R');
retour vrai;
}
retourner faux;
}

string getDirections(TreeNode* root, int start Valeur, int destValue) {
démarrage de la chaîne Chemin, destPath;
dfs(racine, démarrage) Valeur, startPath);
dfs(root, destValue, destPath);

// Supprimer le suffixe commun (partie LCA)
i = 0;
alors que (i < min(startPath.size(), destPath.size()) &&
startPath[startPath.size() - 1 - i] == destPath[destPath.size() - 1 - i] {
++i;
}

chaîne up(startPath.size() - i, 'U');
inverse(destPath.begin(), destPath.end());
detPath.erase(0, i); // ne conserver que la partie non commune

retour + départ Voie;
}
};
«» "

> **Note C++** – L'utilisation de `reverse` en place maintient l'utilisation de la mémoire minimale et garantit le temps `O(n)`.

---

- Oui. 2. Article de blog – Cracking the LeetCode Binary‐ Puzzle de chemin d'arbre: bon, mauvais et ugly

> **Titre (optimisé par le SEO): **
> *Cracking LeetCodes - Directions étape par étape d'un nœud d'arbre binaire – DFS, LCA & Interview– Conseils prêts*

> **Description de la substance (optimisée par le référencement):**
> *Découvrez comment résoudre le puzzle du chemin binaire du LeetCode en Java, Python & C++. Plongez dans DFS, LCA, complexité de l'espace-temps, pièges communs et astuces d'entrevue pour décrocher votre prochain emploi technologique. *

---

Introduction

Les entrevues avec des entreprises technologiques de premier ordre commencent souvent par une question classique sur les arbres binaires : Trouvez un chemin entre deux nœuds.
LeetCodeS (ID 1409) est un exemple parfait.
Dans cet article, nous allons:

- ** Expliquez le problème en anglais.
- Passez à travers une solution basée sur les DFS** qui est rapide, adaptée à la mémoire et facile à coder.
- Signalez les aspects bons, mauvais, laids de cette approche.
- Oui. Partagez la complexité **temps/espace** et pourquoi cela compte dans un contexte d'entrevue.
- Offrez ** tips** sur la façon de parler de ce problème dans une entrevue de codage (et augmentez vos chances d'obtenir un emploi).

> **Mots clés du référencement**: *arbre binaire, LeetCode, interview de codage, DFS, LCA, instructions étape par étape, entretien d'emploi, structures de données, questions d'entrevue, algorithme, Java, Python, C++ *

---

- Oui. 1. Récapitulation des problèmes

Étant donné le **root** d'un arbre binaire, la **valeur d'un noeud de départ** et la **valeur d'un noeud de destination**, retournez une chaîne qui décrit la séquence des directions nécessaires pour marcher du noeud de départ au noeud de destination.

- "L" – déplacer vers l'enfant gauche.
- "R" - passer à l'enfant droit.
- "U" – passer au parent.

**Exemples**

Démarrage Destination Sortie
- C'est quoi ?
[5,1,2,0,3,null,4] Autres
[2,null,3,null,4]

---

- Oui. 2. Intuition

Si nous pouvions écrire le chemin du **root** à chaque nœud, la solution serait triviale:

1. Voie vers *démarrer*: `L R L R ...`
2. Voie vers la *destination*: `L R ...`

Le suffixe commun de ces deux cordes est exactement le chemin **au plus bas ancêtre commun (LCA)** des deux nœuds.
Enlever cette partie laisse:

- Oui. La partie du chemin *start* que nous devons marcher **up** ('U's).
- Oui. La partie du chemin *destination* que nous devons marcher **vers le bas** (inverser le suffixe).

C'est tout le problème.

---

- Oui. 3. Bon – Pourquoi le DFS fonctionne

Caractéristique Raison
C'est pas vrai.
**Heure linéaire** – Chaque DFS touche chaque noeud une fois → `O(n)` Fonctionne pour les arbres jusqu'à des nœuds `104` confortablement. Autres
Autres **Pas de structure de données supplémentaires** – Il suffit d'un constructeur de chaînes de caractères / list. Autres
**Profondeur de la récursion ≤ hauteur** – Sans danger pour les arbres équilibrés. Autres

---

- Oui. 4. Mauvais – Ce qui pourrait mal tourner

Sujet Impact Atténuation
C'est quoi ?
**Renversement de la chaîne** (commun dans certaines solutions) (Extra linear pass); peut attribuer une nouvelle chaîne de caractères. Autres
**Recursion profonde** sur arbres biaisés. Autres
**État global mixte** (p. ex. chaîne statique en C++) Autres

---

- Oui. 5. Ugly – Le bug "Slick" mais subtil

> **Le motif Ugly** – Construire la chaîne de résultats en concaténant des caractères à l'intérieur de la récursion (par exemple, `retour chemin + 'L') peut conduire à **exponentielle** temps dans le pire des cas parce que chaque concaténation copie toute la chaîne.

**Pourquoi c'est moche**:
- Oui. Il va à l'encontre du but d'un algorithme `O(n)`.
- Oui. Dans les entrevues, les candidats peuvent faire exactement cela et se faire pénaliser pour la complexité de temps médiocre. (en milliers de dollars)

** Conseil professionnel** – Conserver le chemin dans un conteneur *mutable* (liste ou `StringBuilder`) et ne convertir en chaîne que lorsque le DFS a terminé.

---

- Oui. 5. Complexité temporelle et spatiale

Description de la complexité
- C'est quoi ?
**Temps** $ `O(n) ́ $ Deux traversées DFS, travail constant supplémentaire sur les cordes. Autres
**Space**="O(h)` où `h` est la hauteur de l'arbre=" La chaîne de chemin grandit au maximum à la profondeur de l'arbre; tous les autres travaux sont constants. Autres

Lors d'un entretien d'embauche, vous avez explicitement indiqué cette complexité et vous avez compris *pourquoi* votre solution est efficace.

---

- Oui. 6. Parler de ce problème dans une entrevue

1. ** Clarifier l'entrée** – Confirmer que toutes les valeurs des nœuds sont uniques (garanties de problèmes).
2. **Exposer le tour de LCA** – Écrire l'idée d'enregistrer deux chemins root-to-node et de tailler le suffixe commun.
3. **Mention DFS vs. LCA library** – .. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . (en milliers de dollars)
4. **Afficher le code** – Mettre en évidence l'aide qui recule pour construire le chemin.
5. **Complexité de l'État** – temps « O(n) », espace « O(h) ».
6. **Les cas de l'Edge** – Et si un noeud est l'ancêtre de l'autre ? → Tous les mouvements `U`s ou pas.
7. **Test** – Exécuter sur de petits arbres personnalisés, puis sur les exemples fournis.

> **Interview Hack** – Si j'avais un environnement interactif, j'aurais en fait imprimé l'arbre et parcouru visuellement l'algorithme. Il démontre une compréhension profonde de la traversée des arbres. (en milliers de dollars)

---

- Oui. 7. Extraits de code final

> (Insérer les extraits Java, Python, C++ de la section 1.)

> **Pourquoi chaque extrait est prêt à l'entrevue** –
> • Court, clair, et suit l'interface LeetCode.
> • Utilise des fonctions de bibliothèque standard (StringBuilder, liste, inverse).
> • Contient des commentaires qu'un gestionnaire d'embauche peut skim et comprendre.

---

- Oui. 8. Liste de contrôle sur l'approche à suivre

- **DFS Path** – Construire deux chemins de racine vers les nœuds.
- **Trim LCA** – Supprimer le suffixe commun.
* Ajouter "U`s égal à la longueur restante du chemin de départ.
* Ajouter le suffixe de destination inversé.
- **Complexité** – Mention "O(n)" temps, "O(h)" espace auxiliaire.

---

- Oui. 9. Enveloppage

Le problème des directions étape par étape est une vitrine de la pensée algorithmique ** propre**.
La maîtrise vous donne :

- Confiance dans la gestion de tout *path entre noeuds* problème.
- Un exemple concret de **DFS + LCA** que vous pouvez décrire aux intervieweurs.
- Preuve de votre capacité à écrire du code **time‐efficace** en Java, Python ou C++.

> **Prêt pour la prochaine entrevue? * *
> 1. Examiner les extraits de code ci-dessus.
> 2. Pratique sur des problèmes similaires de LeetCode: *Binary Tree Inorder Traversal*, *Lowest Common Ancêtre*, *Construire l'arbre binaire de Préorder & Inorder*.
> 3. Partagez cet article sur LinkedIn ou un blog personnel – il vous montre comment apprendre activement et optimiser.

Codage heureux, et que les `U' soient nombreux et les bugs peu!

---

10 ans. Lecture supplémentaire

- *Introduction aux algorithmes* – Chapitre sur les arbres binaires.
- *Cracking the Coding Interview* – Section sur les croisements d'arbres.
- LeetCode Discussions pour ID 1409 – différentes solutions, performances hacks.

---

**Profitez du défi, et bonne chance pour votre prochaine interview! * *

---

*Auteur: Votre nom – Ingénieur logiciel senior, Structures de données Enthousiaste. *

---

**Fin de l'article**

---

* Se sentir libre de copier, adapter ou publier cet article (avec attribution). C'est une excellente façon de mettre en valeur vos connaissances algorithmiques tout en aidant la communauté. *

---

*--*

---

**Suivi**

> Si vous vous préparez à jouer un rôle dans une entreprise de technologie, nous vous recommandons également de vous poser sur **graph traversal**, **stack-based DFS** et **recursive design patterns**—tous utiles pour des problèmes d'entrevue similaires.

---

** Bonne chance, et codage heureux!**



---

**Note** – Tous les extraits de code ci-dessus sont entièrement fonctionnels et peuvent être collés dans l'IDE en ligne LeetCode ou votre environnement local pour des tests rapides.