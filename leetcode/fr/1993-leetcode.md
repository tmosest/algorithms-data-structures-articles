---
titre: LeetCode 1993. Opérations sur arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1993 – Opérations sur arbres
> **Une plongée profonde dans la structure de données LockingTree* *
> *Comment aser l'interview, écrire le code Java / Python / C++ propre, et transformer ce problème en une vitrine de démarrage de reprise. *

---

- Oui. 1. Le problème en coque

On vous donne un arbre enraciné avec des nœuds `n` (`0 ... n-1`).
`parent[i]` est le parent du nœud `i` (`parent[0] = -1`).

Mettre en œuvre une classe "LockingTree" qui soutient trois opérations:

Opération Conditions préalables Résultat
C'est pas vrai.
Le noeud `num` est déverrouillé Le noeud `num` devient verrouillé par `user` Autres
**unlock(num, user)**
**upgrade(num, user)**= Le nœud `num` est déverrouillé, il a un descendant verrouillé, *et* aucun ancêtre verrouillé==verrouillage `num` par `user`, déverrouillage *tous* ses descendants==

Toutes les opérations doivent revenir "vraies" si elles réussissent, sinon "faux".

Contraintes:
- "2 ≤ n ≤ 2000"
- Oui. Au plus 2000 opérations totales
- `utilisateur` est un entier positif jusqu`à `10^4`

---

- Oui. 2. Pourquoi ce problème est une question d'entrevue de Nice

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Tree Traversal** Autres
**La gestion de l'État**" montre comment garder l'état mutable ('locked[]') à travers les appels. Autres
**Connaissance à la complexité**" Réalise que chaque opération peut être "O(n)" dans le pire des cas, mais qu'elle convient aux contraintes données. Autres
**API Design**= Faits saillants soigneusement les signatures de méthode et de retour sémantique. Autres

Dans une entrevue, être en mesure d'expliquer les compromis, suggérer des optimisations (p. ex., maintenir un compteur de descendant verrouillé), et produire un code propre est un plus énorme.

---

- Oui. 3. Le bien – un droit devant, Mise en œuvre lisible

L'idée fondamentale :

1. **Liste des enfants construits** à partir du tableau "parent" (O(n)).
2. Gardez un tableau « verrouillé[] » où `locked[i] = -1` signifie "déverrouillé" et stocke autrement l'identifiant de l'utilisateur.
3. Pour **» mise à niveau**:
- Vérifiez tous les ancêtres (marche vers le haut `parent[]`) – O(hauteur).
- DFS/BFS de `num` pour déverrouiller les descendants et détecter s'ils étaient verrouillés.

Parce que `n ≤ 2000` et appelle ≤ 2000, le simple O(n) par `upgrade` est parfaitement acceptable.

Voici des implémentations propres dans **Java, Python et C++**.

---

- Oui. 4. Code – Java

"Java
Importation de java.util.*;

classe publique LockingTree {

// -------- Champs
relation privée finale int[] parent; // parent
int final privé[] verrouillé; // -1 = déverrouillé, sinon id utilisateur
Liste finale privée<entier>[] enfants; // liste d'adjacence

// - Oui. Constructeur...
@SuppressAvertissements("non vérifié")
public VerrouillageTree(int[] parent) {
Ça. parent = parent;
int n = longueur parent;
ce.locked = nouveau int[n];
Arrays.fill(verrouillé, -1); // tous les nœuds commencent à être déverrouillés

// construire des listes d'enfants
Ça. enfants = nouvelle liste de répartition;
pour (int i = 0; i < n; i++) les enfants[i] = nouvelle liste de distribution<>();
pour (int i = 1; i < n; i++) {
les enfants [parent[i]].add(i);
}
}

// --------verrouillage ---------
Public boolean lock(int num, int user) {
si (verrouillé[num] != -1) retourner faux; // déjà verrouillé
locked[num] = utilisateur;
retour vrai;
}

// --------- déverrouiller ---------
public boolean unlock(int num, int user) {
si (verrouillé[num] == -1--verrouillé[num] != utilisateur) retourne false;
verrouillé[num] = -1;
retour vrai;
}

Mise à niveau
public booléen upgrade(int num, int user) {
// 1. noeud doit être déverrouillé
si (verrouillé[num] != -1) retourner faux;

// 2. aucun ancêtre verrouillé
int cur = nombre;
pendant ce temps (cur != -1) {
si (verrouillé[cur] != -1) retourner faux; // ancêtre verrouillé trouvé
cur = parent[cur];
}

// 3. DFS/BFS pour déverrouiller les descendants et vérifier s'ils ont été verrouillés
booléen aLockedDescendant = faux;
Deque<Integer> pile = nouvelle ArrayDeque<>();
le nombre de piles.push(num);

pendant que (!stack.isEmpty()) {
noeud int = pile.pop();
pour (int enfant : enfants[node]) {
si (enfant enfermé) != -1) {
hasLockedDescendant = true;
}
// Déverrouiller le descendant s'il était verrouillé
verrouillé[enfant] = -1;
pile.push(enfant);
}
}

si (!hasLockedDescendant) retourner faux; // règle 2 violée

// verrouiller le nœud lui-même
locked[num] = utilisateur;
retour vrai;
}
}
«» "

**Pourquoi c'est bon**

- **Clarité** – Une structure d'aide (« enfants ») tient l'arbre.
- **Correctness** – Les trois conditions de "upgrade" sont explicitement vérifiées.
- **Performance** – Seuls les passages linéaires sont nécessaires; `O(n)` par `upgrade` correspond aux contraintes.

---

- Oui. 5. Code – Python

'`python
classe Verrouillage Arbre :
def __init_(self, parent):
auto-parent = parent
n = len(parent)
self.locked = [-1] * n # -1 = déverrouillé, sinon identificateur utilisateur
auto.enfants = [[] pour _ dans la fourchette(n)]
pour i dans la plage (1, n):
les enfants [parent[i]].annexe(i)

def lock(self, num: int, user: int) -> C'est vrai.
si self.locked[num] != - 1 :
Retour Faux
self.locked[num] = utilisateur
retour Vrai

def unlock(self, num: int, user: int) -> C'est vrai.
si self.locked[num] == -1 ou self.locked[num] != utilisateur & #160;:
Retour Faux
self.locked[num] = -1
retour Vrai

def upgrade(self, num: int, user: int) -> C'est vrai.
# 1. noeud doit être déverrouillé
si self.locked[num] != - 1 :
Retour Faux

2. Pas d'ancêtre verrouillé
cur = nombre
alors que cur != - 1 :
si self.locked[cur] != - 1 :
Retour Faux
cur = parent propre[cur]

3. DFS pour débloquer les descendants, détecter tout verrouillé
pile = [num]
has_locked_descendant = Faux
pendant la pile:
noeud = pile.pop()
pour enfant en soi. enfants[nœud]:
si soi-même. [enfant] verrouillé != - 1 :
has_locked_descendant = Vrai
self.locked[child] = -1 # déverrouillage
pile.append(enfant)

si ce n'est pas le cas:
Retour Faux

Serrez le nœud lui-même
self.locked[num] = utilisateur
retour Vrai
«» "

L'implémentation Python's suit la même logique que Java mais profite de **listes dynamiques** et d'une pile DFS claire**.

---

- Oui. 6. Code – C++

'`cpp
#incluez <vecteur>
#incluez <stack>

classe LockingTree {
public:
VerrouillageTree(suite::vector<int>&parent)
: parent(parent), n(parent.size()), verrouillé(n, -1) {
enfants.resize(n);
pour (int i = 1; i < n; ++i)
enfants[parent[i]].push_back(i);
}

bool lock(int num, int user) {
si (verrouillé[num] != -1) retourner faux;
locked[num] = utilisateur;
retour vrai;
}

bool unlock(int num, int user) {
si (verrouillé[num] == -1--verrouillé[num] != utilisateur) retourne false;
verrouillé[num] = -1;
retour vrai;
}

bool upgrade(int num, int user) {
si (verrouillé[num] != -1) retourner false; // doit être déverrouillé

// vérifier les ancêtres
int cur = nombre;
pendant ce temps (cur != -1) {
si (verrouillé[cur] != -1) retourner faux; // ancêtre verrouillé
cur = parent[cur];
}

// DFS/BFS sur les descendants
bool hasLocked = false;
std:stack<int> st;
push (num);
pendant que (!st.vide()) {
noeud int = st.top(); st.pop();
pour (int enfant : enfants[node]) {
si (enfant enfermé) != -1) hasLocked = true;
verrouillé[enfant] = -1; // déverrouillage
s.push (enfant);
}
}

si (!hasLocked) retourner faux; // aucun descendant verrouillé

verrouillé[num] = utilisateur; // verrouiller le noeud lui-même
retour vrai;
}

particulier:
const std::vector<int>& parent;
md:vector<int> verrouillé;
md::vector<std::vector<int>> les enfants;
l'élément n;
};
«» "

**Pourquoi c'est bon**

- Utilise `std::vector` pour tout – pas de frais généraux d'allocation dynamique.
- Préserve explicitement la forme de l'arbre ('enfants').
- Utilisation de la méthode "std::stack" pour la méthode de mesure des émissions de gaz à effet de serre.

---

- Oui. 6. L'approche «Bad» – une approche moins «Than‐Ideal»

Certains candidats essaient de reconstruire l'arbre sur chaque `upgrade`, ou de maintenir une carte de verrouillage globale qui est **non** indexée par noeud id.
Cela peut conduire à:

- **Utilisation de la mémoire supérieure** (cartes vs tableaux).
- **Vérifications de l'ancêtre inférieur** (analyse de toute la carte à chaque fois).
- **Pour raisonner sur** (structures de données mixtes).

**Ligne de bottom** – si vous vous voyez dans ce code de bad, il est temps de refactorer.

---

- Oui. 7. L'Ugly – Essayer d'optimiser prématurément

Une tentative typique:

- **Précalculer un compteur de descendants verrouillés** pour chaque noeud, le mettre à jour sur chaque `lock`/`unlock`.
Bien qu'il réduise le coût de la mise à niveau à "O(hauteur)" + "O(1)" pour la vérification des descendants, la mise en œuvre devient **bug-prone**:
- Vous devez propager soigneusement le compteur change dans l'arbre.
- Une seule mise à jour oubliée peut corrompre toutes les réponses ultérieures.

- **Le DFS récursif sans pile** sur Python pourrait atteindre la limite de profondeur de récursion de Python, même si `n ≤ 2000`.

Si vous devez montrer une telle optimisation, ** documenter clairement** et fournir une logique de recul pour la justesse.

---

- Oui. 8. Idées d'optimisation (pour les intervieweurs)

Idée Quand utiliser
- C'est quoi ?
**Compte-descendance Locké** (`descLocks[]`)= Si vous voulez garantir `O(hauteur)` pour chaque `upgrade`="O(hauteur)` pour verrou/déverrouillage, `O(hauteur)` pour mise à niveau="
Pour les contraintes plus grandes (par exemple, `n = 10^5`)
**Bitset pour les utilisateurs**

Parce que les contraintes ici sont minuscules, l'implémentation simple d'Option est généralement le meilleur choix – vous gagnez du temps et évitez les bugs.

---

- Oui. 9. Transformer ce problème en une histoire de rappel*

J'ai résolu LeetCode 1993 – Opérations sur arbre – en Java, Python et C++ avec une API propre, un code documenté et une analyse de complexité claire. *

Dans votre entrevue ou lettre de présentation, mentionnez :

1. **Machine d'état basée sur les arbres** – J'ai construit une liste d'adjacence et maintenu un tableau de verrouillage.
2. **Vérifications préconditionnelles claires** – Chaque méthode retourne un état booléen et ne mute jamais lorsque les conditions préalables échouent.
3. ** Conception évolutive** – Alors que ma solution de base est `O(n)` par mise à niveau, j'ai également esquissé un compteur O(1) de descente verrouillé en option pour les systèmes de production.

Ajouter le *blog* (ce post) à votre portfolio ou Linked En donnant aux recruteurs un échantillon concret et bien commenté, ils peuvent courir immédiatement.

---

10. Liste de contrôle finale pour l'entrevue

** Expliquer** la structure des données en mots d'abord.
- Écrire **propre, code tapé** (Java + annotations, conseils de type Python 3.8+, C++14+).
**Venez à travers** un appel "upgrade" d'échantillon, illustrant chaque condition préalable.
- Mentionnez une possible *optimisation* et discutez quand elle en vaut la peine.

Bonne chance – vous êtes maintenant prêt à montrer aux recruteurs que vous pouvez **design, raison et code** un problème d'arbre non trivial en trois langues principales! C'est ce qu'il a dit.

---

Lire plus

- Trèves - DFS vs BFS - un rafraîchissement rapide sur les listes d'adjacence.
- Les structures de données de l'état dans les entrevues – pourquoi les tableaux sont souvent le meilleur choix.
- Java Generics vs Python Dynamic Typing – choisir le bon outil pour le travail.

Bon codage !