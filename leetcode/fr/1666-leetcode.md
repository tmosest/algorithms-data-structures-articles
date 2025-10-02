---
titre: LeetCode 1666. Changer la racine d'un arbre binaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1666 – **Changez la racine d'un arbre binaire**
*LeetCode – Moyen – DFS – Manipulation de pointeurs*

> **Objectif**
> Compte tenu de la racine d'un arbre binaire et d'un noeud de feuille, l'arbre devient la nouvelle racine.
> Chaque nœud sur le chemin de la feuille à la vieille racine doit échanger ses enfants:
> * si un noeud a un enfant gauche, cet enfant devient le nœud droit;
> * l'ancien parent du noeud devient l'enfant gauche du noeud.
> Enfin, tous les pointeurs `parent` doivent être mis à jour (autrement vous obtiendrez *Wrong Answer*).

Vous trouverez ci-dessous des solutions complètes et prêtes à copier dans **Java, Python et C++**.
Après le code, j'ai écrit un court article de style blog qui couvre le **bon, le mauvais, et le laid** de ce problème – idéal pour polir vos notes d'interview et SEO optimisé pour la recherche d'emploi.

---

- Oui. 1. Solution Java

"Java
// Définition pour un noeud d'arbre binaire avec pointeur parent.
Numéro de classe {
la valeur intérieure;
À gauche;
Droit du nœud;
Parent nodal;
Noeud(int x) { valeur = x; }
}

solution de classe publique {
// root original est nécessaire uniquement pour la vérification du cas de base
privé Noeud original Racine;

publique Nœud flipBinaryTree(racine de nœud, feuille de nœud) {
originale Racine = racine;
retour helper(leaf, null); // la feuille devient une nouvelle racine
}

privé Aide au nœud(Node cur, Node newParent) {
Noeud oldParent = cur.parent; // se rappeler parent original
cur.parent = newParent; // Mettre à jour le pointeur parent

// si nous sommes en marche arrière, nous devons
// Déconnecter ce lien pour éviter les cycles
si (cur.left == newParent) cur.left = nul;
si (cur.right == nouveauParent) cur.right = nul;

// Nous avons terminé une fois que nous avons atteint la vieille racine
si (cur == originalRoot) retour cur;

// si l'enfant gauche existe, il devient le nouvel enfant droit
si (cur.left != null) cur.right = cur.left;

// Récursez le vieux parent – il devient l'enfant gauche
cur.left = assistant(oldParent, cur);

retour cur;
}
}
«» "

*Pourquoi cela fonctionne: *
La récursion marche **up** de la feuille à la racine originale.
À chaque étape, il :

1. Conserve le parent d'origine (l'ancien parent).
2. Fait `nouveauParent` le nœud actuel parent.
3. Retire le lien vers l'ancien parent pour éviter les cycles.
4. Swaps gauche → droite (si présent).
5. Récurses, faisant de l'ancien parent le nouvel enfant gauche.

Le cas de base est lorsque le nœud courant est la racine originale – la récursion s'arrête et la nouvelle racine est retournée.

---

- Oui. 2. Solution Python

'`python
# Définition d'un noeud d'arbre binaire avec pointeur parent.
Numéro de classe:
def __init_(self, val: int, gauche=Aucun, droite=Aucun, parent=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit
auto-parent = parent

Solution de classe:
def flipBinary Arbre (même, racine : 'Node', feuille : 'Node') -> 'Noeud':
auto.original_root = racine
retourner self._dfs(feuille, Aucun)

def _dfs(self, cur: 'Node', nouveau_parent: 'Node') -> 'Noeud':
old_parent = cur.parent
cur.parent = nouveau_parent

# Déconnecter l'ancien lien s'il pointe toujours vers new_parent
si cur.left est nouveau_parent :
cur.left = Aucune
si cur.right est nouveau_parent :
c. droite = Aucune

if cur is self.original_root:
retour cur

si cur. gauche:
cour. droite = cour. gauche

cur.left = self._dfs(old_parent, cur)
retour cur
«» "

*La même logique que Java, juste adaptée au style Python. *
Tous les pointeurs sont des références, de sorte qu'ils doivent être utilisés pour les contrôles d'identité.

---

- Oui. 3. Solution C++

'`cpp
/* Définition pour un nœud. */
Numéro de classe {
public:
la valeur intérieure;
A gauche;
Noeud* droit;
Noyau* parent;
Node(int _val) : val(_val), gauche(nullptr), droite(nullptr), parent(nullptr) {}
};

solution de classe {
public:
Noeud* flipBinaryTree(Noe* racine, Noeud* feuille) {
originale Racine = racine;
retour dfs(leaf, nullptr); // la feuille devient une nouvelle racine
}

particulier:
Noeud* originalRoot;

Noeud* dfs(Noe* cur, Noeud* nouveauParent) {
Noeud* vieuxParent = cur->parent;
cur->parent = nouveau parent;

// lien de déconnexion vers l'ancien parent
si (cur->left) cur->left = nullptr;
si (cur->right) cur->right = nullptr;

si (cur == originalRoot) retour cur;

si (cur->left) cur->right = cur->left; // gauche devient droite

cur->left = dfs(oldParent, cur); // l'ancien parent devient l'enfant gauche
retour cur;
}
};
«» "

C++ utilise des pointeurs bruts; la même logique de manipulation des pointeurs est appliquée.

---

- Oui. 4. Article de blog: *Le Bon, le Mauvais, et l'Ugly de -Changez la racine d'un arbre binaire

> **Mots clés du référencement:** Changer la racine d'un arbre binaire, LeetCode 1666, reracinement d'arbre binaire, manipulation de pointeur, DFS, conseils d'entretien, entretien d'emploi, Java, Python, C++

---

- Oui. 1. Présentation

Les arbres binaires sont le pain-and-butter de nombreuses questions d'entrevue, mais le problème *rerooting* (LeetCode 1666) jette une touche : vous devez **changer la racine** d'un arbre **en place**, mettant à jour les liens enfants et les pointeurs `parent`. C'est un test parfait de:

- Compréhension de la traversée des arbres
- Capacité de raisonner sur la manipulation des pointeurs
- Design récursif propre

Que vous soyez en train de vous préparer pour une entrevue de codage ou de polir votre boîte à outils algorithmique, ce problème est une mine d'or.

---

- Oui. 2. Récapitulation des problèmes

On vous donne un noeud racine `root` et un noeud feuille `leaf`. L'arbre a les champs habituels `val`, `left`, `right` **plus** un pointeur `parent`.
Objectif: Faire `leaf` la nouvelle racine et ajuster tous les nœuds sur le chemin de `leaf` jusqu'à l'ancienne racine de sorte que:

- Oui. L'enfant gauche (le cas échéant) devient l'enfant droit.
- Oui. Le parent original devient l'enfant gauche.
- Tous les pointeurs `parent` sont mis à jour en conséquence.

Si vous oubliez d'ajuster un lien parent, l'arbre contiendra un cycle et vous obtiendrez la réponse de votre choix.

---

- Oui. 3. Le bien – Pourquoi C'est un beau problème

Aspect Pourquoi c'est génial
-- -- -- -- -- --
Un assistant récursif de ~20 lignes retourne l'arbre entier. Autres
Autres **Case de base claire**= La récursion s'arrête naturellement lorsque la racine originale est atteinte. Autres
**Pas d'espace supplémentaire** Autres
**Language-agnostique**La logique de base est identique à travers Java, Python et C++. Autres
**Insight into Parent Pointers**=Il montre comment les liens parent=2 peuvent être traités comme le pointeur suivant d'une liste liée, donnant une nouvelle perspective sur la traversée des arbres. Autres

---

- Oui. 4. Les pièges communs

Comment l'éviter
C'est-à-dire
Autres **Cycle Formation***** Toujours **déconnecter** l'ancien parent avant de l'assigner comme un nouvel enfant ('if (cur.left == newParent) cur.left = null;'). Autres
Autres **Cas de base incorrect**= Si vous vous arrêtez à la feuille au lieu de la racine originale, vous perdrez la partie supérieure de l'arbre. Autres
**Missing `parent` Mises à jour**= Oublier de définir `cur.parent = newParent` laissera des pointeurs de saut. Autres
Autres Dans les langues avec références d'objet, comparez par identité (`is` dans Python, `==` pour les pointeurs en C++). Autres
Avec jusqu'à 100 nœuds ce n'est pas un vrai problème, mais soyez toujours conscient de la profondeur de récursion pour les entrées plus importantes. Autres

---

- Oui. 5. Les scénarios moins directs

Scénarios Pourquoi ça devient ringard
Il y a un problème.
**Tree with Multiple Leaves**= Vous devez vous assurer que vous avez passé la feuille *exact* que vous comptez faire la nouvelle racine. Autres
**Cycles préexistants**= Si l'arborescence d'entrée est mal formée (ce qui est peu probable sur LeetCode), l'algorithme continuera de traverser jusqu'à ce qu'elle touche une boucle. Autres
**Memory‐Leak en C++**= Si des nœuds sont attribués sur le tas et que vous ne gérez pas la propriété, vous pourriez fuir la mémoire. Autres
**Arbres déséquilibrés**=Dans les arbres fortement biaisés, la profondeur de récursion est égale à la hauteur de l'arbre; toujours acceptable ici, mais à noter. Autres
**Les pointeurs parents ne sont pas définis au départ. Dans ce cas, vous auriez besoin de pré-calculer les pointeurs parent avant de reraciner. Autres

---

- Oui. 6. Marche pas à pas

L'algorithme est tracé sur un petit exemple :

«» "
3
/ \
5 1
/ \ / \
6 2 0 8
\ /
7 4
«» "

«feuille = 7».
Nous commençons à 7 → vieux parent 2 → nouveau parent `null` (puisque 7 est une nouvelle racine).

- 7=s `parent` = `null`.
- L'enfant gauche est "null", l'enfant droit est "null".
- 7° reste "null".
- 7's à droite reste "null".

Récidive jusqu'à 2 :

- L'ancien parent = 5, le nouveau parent = 7.
- L'enfant gauche devient l'enfant gauche ? N°: 2S gauche est 4 → devient l'enfant droit.
- 2's gauche devient résultat de récursion ('7').
- Mettez à jour les pointeurs en conséquence.

Continuer jusqu'à 3. L'arbre final correspond à la sortie LeetCode.

---

- Oui. 7. Analyse de la complexité

Métrique Temps Espace
- Oui.
**Temps**="O(n)" – chaque noeud sur le chemin d'une feuille à l'autre est visité une fois.="
**Espace auxiliaire**
**Cachet récursif**="O(h)" – hauteur de l'arbre (=100 pour ce problème). C'est vrai.

---

- Oui. 8. Conseils d'entrevue amis

1. ** Expliquez votre intuition d'abord** – traitez le chemin d'une feuille à l'autre comme une liste liée où le pointeur `parent` est le lien « next» .
2. **Settch le pointeur change** sur un tableau blanc ou un papier; de nombreux candidats sautent l'étape qui déconnecte l'ancien parent, conduisant à des bugs subtils.
3. **Afficher clairement le boîtier de base** : lorsque vous touchez la racine originale, arrêtez la récursion.
4. **Les cas de bordures de mention** tels que des arbres biaisés ou une feuille qui est la racine elle-même (bien que LeetCode garantisse au moins deux nœuds).
5. **Énoncer la complexité** à l'avant-garde; les intervieweurs apprécient un grand‐ O explication.

---

- Oui. 9. Conclusion

LeetCode 1666 est trompeurment simple mais riche en opportunités d'apprentissage.
En maîtrisant la manipulation des pointeurs dans les arbres, vous ne vous contentez pas de résoudre un seul problème – vous aiguisez un ensemble de compétences qui s'applique à :

- Algorithmes basés sur le chemin (p. ex., Ancêtre commun le plus bas avec pointeurs parent)
- Restructuration des arbres dans le code de production
- Mise en œuvre de structures de données avancées comme Link‐ Arbres coupés

Utilisez les solutions clean Java, Python et C++ ci-dessus comme référence d'implémentation, et gardez la liste de contrôle « Good, Bad, Ugly » à portée de main pour les futurs entretiens.

Bonne chance, et le codage heureux!

---

> * Prêt à accepter votre prochaine entrevue de codage? *
> Pratiquez LeetCode 1666 et ajoutez-le à votre ensemble de compétences de manipulation d'arbre en place. Le problème peut être de petite taille, mais les concepts que vous apprenez sont énormes.

---

* Fin de l'article. *

---

Ceci complète la réponse complète et prête à la production : code en trois langues, une explication solide et un article convivial pour les entrevues. Joyeux entretien !