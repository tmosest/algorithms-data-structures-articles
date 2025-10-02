---
titre: LeetCode 2764. Est-ce qu'Array une Précommande de quelques Arbres Binary -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La solution 3-Way pour la précommande d'un arbre binaire

Vous trouverez ci-dessous une implémentation **complète, prête à la production** dans **Java, Python et C++**.
Chaque version suit la même idée basée sur la pile, fonctionne dans **O(N)** temps et **O(N)** espace, et est prête à coller dans toute soumission LeetCode ou interview blanc-board.

---

Récapitulation des problèmes

> **Don** une liste de «nodes» indexée à 0 où chaque élément est «[id, parent» Id] "
> **Déterminez** si cet ordre pourrait être le **passage précommande** de l'arbre binaire *some*.

> *Précommande*: visite noeud → précommande(à gauche) → précommande(à droite)

> L'entrée garantit que les paires forment un arbre binaire valide (une racine, aucun cycle).

---

L'idée fondamentale

Nous simulons le passage de précommande en passant par le tableau donné:

1. **Démarrer** avec la racine (la première paire – son `parent Id` doit être `-1`).
2. Maintenez une pile de *ancêtres actifs* – ces nœuds qui ont encore des enfants inexplorés.
3. Pour chaque noeud suivant `(id, parent)`:
* Conservez **popping** de la pile jusqu'à ce que le haut égal `parent`.
* Si la pile devient vide avant de trouver `parent`, la séquence ** ne peut** être un précommande.
* Poussez le `id` actuel sur la pile – il est maintenant un ancêtre actif.

Parce que le précommande visite un nœud avant tous ses descendants, le parent actuel doit toujours être l'ancêtre **le plus proche** qui n'a pas encore terminé son sous-arbre gauche – exactement le sommet de la pile.

---

Code

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe {
booléen public est Preorder(Liste<Liste<entier>> noeuds) {
int n = noeuds.size();
si (n) 0) retourner vrai; // cas trivial

// Le premier noeud doit être la racine
si (nodes.get(0).get(1) != -1) retourner faux;

Deque<Integer> pile = nouvelle ArrayDeque<>();
stack.push(nodes.get(0).get(0)); // push root id

pour (int i = 1; i < n; i++) {
int id = nœuds.get(i).get(0);
int parent = nœuds.get(i).get(1);

// Montez la pile jusqu'à ce que nous trouvions le parent
pendant que (!stack.isEmpty() && stack.peek() != parent) {
pile.pop();
}

si (stack.isEmpty()) retourne faux; // parent non trouvé
ftil.push(id);
}
retour vrai;
}
}
«» "

# # # # # #

'`python
de taper l'importation Liste

Solution de classe:
def isPreorder(self, noeuds: List[List[int]]) -> bool:
si non des nœuds:
retour Vrai

# La racine doit avoir un parent -1
si noeuds[0][1] != - 1 :
Retour Faux

pile = [nœuds[0][0] # commencer par l'identifiant racine

pour id, parent en nœuds[1:]:
# pop jusqu'à ce que le parent soit au top
alors que pile et pile[-1] != parent:
Pile.pop()

si pas pile: # parent non trouvé
Retour Faux

pile.append(id) # noeud courant devient ancêtre actif

retour Vrai
«» "

C'est vrai. C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
bool isPreorder(const vector<vector<int>>& noeuds) {
int n = noeuds.size();
si (n) 0) retour vrai;

// Le premier nœud doit être la racine
si (nœuds[0][1] != -1) retourner faux;

vecteur<int> pile;
pile.push_back(nodes[0]]; // push root id

pour (int i = 1; i < n; ++i) {
int id = noeuds[i][0];
parent int = noeuds[i][1];

pendant que (!stack.vide() && empil.back() != parent) {
pile.pop_back();
}

si (stack.vide()) retourner faux; // parent non trouvé

pile.push_back(id);
}
retour vrai;
}
};
«» "

> **Pourquoi ça marche** – La pile représente toujours l'actuel chemin, depuis la racine jusqu'au nœud le plus profond qui a encore besoin de son bon enfant traité.
> Lorsque le prochain nœud est visité, son parent doit être l'ancêtre le plus récent qui attend encore un enfant → le haut de la pile.
> Si nous ne pouvons pas trouver ce parent, l'ordre viole les propriétés de précommande.

---

Le bon, le mauvais et le mauvais de la validation précommande

> **Description détaillée**:
> Apprenez la solution basée sur la pile à LeetCode 2764 -Is Array a Preorder of Some Binary Tree. Plongez dans l'algorithme, les cas de bord, les alternatives, et pourquoi cette approche est une victoire d'entrevue.

---

Introduction

Lors d'une entrevue, l'intervieweur peut vous demander de **valider** si une liste donnée de paires `(noeud, parent)` pourrait être la traversée pré-commande de l'arbre binaire *any*.
Cela semble simple, mais l'astuce consiste à gérer efficacement les relations parentales sans construire l'arbre entier.

> **Mots clés**: LeetCode 2764, précommande transversale, arbre binaire, algorithme de pile, prép.

---

Récapitulation des problèmes

On nous donne `nodes = [id, parentId], ...]` – une liste 0-indexée qui représente déjà un arbre binaire *valide* (une racine unique, aucun cycle).
La tâche : **Retour `true` si l'ordre est un passage précommande valide. **

- Précommande : noeud → sous-arbre gauche → sous-arbre droit.
- La racine a "parent" Id = -1'.

---

C'est vrai. Le bien – Pourquoi la pile est parfaite

Explication
C'est pas vrai.
**O(N) Temps**= Chaque noeud est traité une fois; la pile apparaît au plus une fois par noeud. Autres
**O(N) Espace**=La pile tient la chaîne d'ancêtres actuelle; la pire profondeur du cas N (arbre dégénéré). Autres
**Nous n'avons pas besoin de listes d'adjacence ou d'objets de nœuds – juste des indices. Autres
**Intuition claire**=Dans le précommande, vous faites toujours un retour à l'ancêtre le plus proche qui a encore besoin d'un enfant. La pile simule ce retour en arrière. Autres

---

C'est pas vrai. L'Écart – Cas et pièges

Numéro
C'est quoi ?
**Raisines multiples**Le premier élément de l'"ID parent" doit être `-1`. Sinon, retournez "faux". Autres
**Missing parent in stack**=Si la pile se vide avant de correspondre à l'ordre parent → invalide. Autres
**Dupliquer les ID**Le problème garantit l'unicité, donc pas de vérification supplémentaire nécessaire. Autres
Utiliser une pile rapide (ArrayDeque en Java, liste en Python, vecteur en C++). Évitez la récursion pour rester dans les limites de la pile. Autres

---

C'est vrai. Le "Ugly" – Pourquoi le DFS plus simple pourrait induire en erreur

Un DFS naïf qui reconstruise l'arbre et simule ensuite la précommande peut être :

- **O(N2)** dans le pire des cas si des listes d'adjacence sont construites en scannant tous les nœuds pour chaque parent.
- **Memory-heavy** – stocker toute la structure de l'arbre lorsque vous n'avez besoin que de l'ordre de traversée.

Cette approche est tentante dans une interview, mais perd du temps et des ressources précieuses.

---

Stratégies alternatives

Démarche Complexité
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
** Simulation récursive**= Temps O(N), espace O(N) (profondeur de récursion)= Très intuitif= Risque de débordement de cheminée pour les arbres profonds=
**Hash-Map Carte des parents + Stack**= O(N) time, O(N) space= Évite les indices de liste==
**Parent-Index Mapping + Two-Pointer**

> Dans la plupart des interviews, la méthode **stack** est le bon endroit.

---

### # #=" SEO-Ready à emporter

- **Identification du problème**: 2764 – Est-ce que le précommande d'un arbre binaire
- **Modalités principales**: `preorder traversal`, `binary arbore validation`, `stack algorithme`, `LeetCode solutions`, `interview prep "
- **Titre** : Valider une trajectoire pré-commande : Solution à base de piles pour le LeetCode 2764

---

Conclusion

La solution à base de piles est ** propre, rapide et évolutive**. Il reflète la mécanique naturelle de la traversée de précommande et s'écarte de la construction des arbres. Que vous soyez en train de coder sur LeetCode ou d'écrire sur un tableau blanc, ce modèle est un agrafe dans votre boîte à outils algorithme.

> **Conseil pro**: Dans les entrevues, commencez par dessiner la logique de la pile, puis écrivez le code. Tenez l'intervieweur au courant – Je vais pousser la racine sur la pile, puis pour chaque noeud Je vais sauter jusqu'à ce que je trouve son parent...

---

Appel à l'action

> Essayez de mettre en œuvre la solution dans **Java, Python ou C++** (voir le code ci-dessus).
> Puis, créez une repo **GitHub** et ajoutez un README avec l'explication.
> Partagez sur LinkedIn avec les tags **#Algorithm #LeetCode #InterviewPrep** et regardez les recruteurs remarquer!

---

Mot final

- **Bon**: Logique de pile rapide, efficace en mémoire.
- **Bad**: Doit gérer explicitement les cas parent et racine manquants.
- **Ugly**: Reconstruire l'arbre est surqualifié et risqué.

Avec cette connaissance, vous n'êtes pas seulement la solution d'un problème, vous maîtrisez un modèle qui est utile pour de nombreuses questions d'entrevue binaire. Bon codage, et que votre prochaine entrevue soit un *précommande* de succès!