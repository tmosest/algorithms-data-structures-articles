---
titre: LeetCode 2095. Supprimer le nœud moyen d'une liste liée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2095 – Supprimer le nœud moyen d'une liste liée
### Énoncé du problème (court)

> **Donné** d'une liste en lien unique, supprimer son point milliaire** et retourner la nouvelle tête.
> Le nœud moyen est le -2 -ième noeud (0-basé l'indexation) où *n* est la longueur de la liste.

- Oui. Pourquoi ce problème est important

* Démontre la maîtrise de la manipulation des pointeurs et le modèle **fast/slow pointer**.
* Il montre comment penser aux problèmes de mi-point sans espace supplémentaire.
* Une question d'interview classique pour les rôles d'ingénierie logicielle (Java, C++, Python, etc.).

---

Solution en trois langues

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Chacun suit la même stratégie de deux points (tortoise et lièvre), atteignant **O(n)** temps et **O(1)** espace.

> **Cas de bord importants* *
> • Liste vide (`head == null`) → retourner `null "
> • Liste de nœuds uniques → suppression du seul nœud dans une liste vide → retour `null`

C'est pas vrai. Java

"Java
***
* Définition pour une liste liée.
* Liste de classe publiqueNode {
* Int val;
* ListNode suivant;
* ListNode() {}
* ListNode(int val) { this.val = val; }
* ListNode(int val, ListNode next) { this.val = val; this.next = next; }
*}
*/
solution de classe {
public ListNode deleteMiddle(ListNode head) {
// Edge: 0 ou 1 noeud -> liste devient vide
si (head) null (head) null (head) null (head).

ListNode lent = tête; // déplace 1 pas
ListNode fast = head.next; // déplace 2 étapes
ListNode prev = null; // noeud avant le lent

alors que (fast != null && fast.next != null) {
prev = lent;
lent = lent.next;
fast = fast.next.next;
}

// prev est maintenant le nœud juste avant le milieu
si (prev != null) prev.next = lent.next;
tête de retour;
}
}
«» "

# # # # # #

'`python
# Définition pour une liste liée.
Numéro de la classe:
def __init_(self, val=0, next=None):
autoval = val
self.next = suivant

Solution de classe:
Supprimer Moyenne(s), tête: ListNode) -> Numéro de liste:
# Edge: 0 ou 1 noeud -> liste devient vide
si pas de tête ou pas de tête. Suivant :
retour Aucune

lente = tête
rapide = tête
prev = Aucune

# se déplace vite deux fois plus vite que lent
tandis que rapide et rapide.next:
prev = lente
lent = lent.next
rapide = rapide.next.next

# prev est le nœud juste avant le milieu
prev.next = lent.next
tête de retour
«» "

C'est vrai. C++

'`cpp
***
* Définition pour une liste liée.
* struct ListNode {
* Int val;
* Numéro de liste * suivant;
* ListNode() : val(0), next(nullptr) {}
* ListNode(int x) : val(x), next(nullptr) {}
* ListNode(int x, ListNode *next) : val(x), next(next) {}
* };
*/
solution de classe {
public:
ListNode* supprimerMiddle(ListNode* tête) {
si (!head->next) retourne nullptr; // 0 ou 1 noeud

ListNode* lent = tête;
ListNode* rapide = tête;
ListNode* prev = nullptr;

alors que (rapide & & rapide->suivant) {
prev = lent;
lent = lent->suivant;
fast = fast->next->next;
}

// prev indique maintenant le noeud avant le milieu
prev->next = lent->next;
tête de retour;
}
};
«» "

---

Comment fonctionne l'approche à deux points

1. **Initialiser** `faible` et `rapide` à la tête.
2. Déplacer `rapide` deux nœuds par itération, `slow` un noeud.
3. Lorsque `fast` atteint la fin (`null` ou `null->next`), `slow` pointe vers le nœud médian.
4. Utilisez un pointeur `prev` (le noeud qui était juste avant `slow`) pour sauter le noeud médian (`prev->next = lent->next`).

Parce que nous ne traversons la liste qu'une seule fois, l'algorithme est linéaire dans le temps et constant dans l'espace auxiliaire.

---

Python (Python)

'`python
def build_linked_list(vals) :
mannequin = Numéro de liste()
cur = mannequin
pour v en vals:
cur.next = ListNode(v)
cur = cur.next
retour mannequin.suivant

def to_list(head) :
out = []
pendant la tête:
out.append(head.val)
tête = tête.next
retour

Exemple 1
head = build_linked_list([1,3,4,7,1,2,6])
print(to_list(Solution().deleteMiddle(head))) # → [1,3,4,1,2,6]
«» "

Effectuer des essais similaires pour les cas de bords (`[2,1]`, `[5]`, `[]`).

---

Article du blog : Le bon, le mauvais et l'acharnement de supprimer le nœud moyen

> **Audience cible** – Junior-to- Ingénieurs logiciels de niveau intermédiaire se préparant à des entrevues de codage.
> **SEO Focus** – *Liste liée*, *Midddle Node Deletion*, *LeetCode 2095*, *Fast/Slow Pointers*, *Job Interview*, *Logiciel Engineer*, *Algorithm Interview Questions*.

---

Introduction

Lorsqu'un intervieweur vous donne un problème **linked-list**, ils sont généralement sonder deux choses:

1. **Pointer arithmétique** – pouvez-vous manipuler des références sans pile?
2. **La pensée algorithmique** – pouvez-vous trouver le moyen optimal de résoudre un problème?

Supprimer le milieu Le nœud est un problème de manuel qui touche les deux. Dans cet article, nous disséquerons ** ce qui fait le problème, et comment le résoudre de la manière la plus efficace, et comment en parler pendant une entrevue.

> **Quick TL;DR**: Utilisez une technique à deux points (`slow`/`fast`) pour trouver le milieu en un seul passage. Passer le nœud avec `prev->next = lent->next`. Cas de bord: 0/1 noeud → retour `null`.

---

- Oui. Les bonnes

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Temps linéaire**= O(n) – nous ne scannons qu'une seule fois, pas besoin de compter deux fois. Autres
**L'espace continu**= O(1) – nous utilisons seulement une poignée de pointeurs. Autres
**Single Pass**=Conserve l'utilisation de la mémoire faible et prévisible. Autres
**Widely Asked**= Apparaît dans de nombreuses interviews (Google, Amazon, Facebook). Autres
**Bon outil d'enseignement** Autres

#### Interview–Aimely Insight
Quand l'intervieweur demande *=Comment géreriez-vous cela avec un seul travers?==*, vous pouvez immédiatement soulever l'idée de pointeur rapide/lent, montrer que vous pensez déjà à la solution optimale.

---

C'est vrai. Les mauvais

Piège Explication
C'est pas vrai.
**Certains solutions supposent la *seconde* moyenne dans les listes de longueurs égales. Le problème veut explicitement de . Autres
**Déréférencement de la Null**. L'oubli de vérifier `head` ou `head->next` conduit à des défauts de segmentation (C++), des erreurs `NoneType` (Python), ou des exceptions de null-pointer (Java). Autres
**Two-Pointer Mis-setup** 2.
**Test de l'insuffisance**=De nombreux candidats ne font que des tests sur des listes de longueurs égales; les listes de longueurs impaires se comportent différemment. Autres

> **Key Takeaway**: toujours gérer la liste *vide* et *single-node* avant de lancer des pointeurs.

---

C'est vrai. L'Ugly

> Certains candidats optent pour une approche en deux étapes** :
> 1. Compter les nœuds (`O(n)`), trouver `mid = n/2`.
> 2. Traverser à nouveau vers `mid-1` et sauter.

C'est techniquement correct mais **sous-optimal** et plus difficile à expliquer sous la pression du temps. Il utilise deux passes et se sent « lazy » aux intervieweurs qui aiment l'élégance.

> **Un autre laid** – construire une nouvelle liste et copier des valeurs. Cela utilise l'espace O(n), va à l'encontre de l'objectif d'un exercice lié à une liste de références et indique souvent que le candidat ne comprend pas la manipulation des références.

---

C'est pas vrai. L'idée de base: pointeurs rapides et lents

Texte
lent → 1 → 2 → 3 → 4 → 5 → 6
rapide → 1 → 2 → 3 → 4 → 5 → 6
après 1ère étape
lent → 2
rapide → 3
après 2ème étape
lent → 3
rapide → 5
après 3ème étape
Lent → 4 (moyen)
rapide → Aucune
«» "

* `fast` bouge deux fois plus vite que `slow`.
* Quand `fast` est à la fin, `slow` est exactement à ..
* Gardez un pointeur `prev` pour contourner le nœud médian.

> **Astuce**: Dans des langues comme C++/Java, n'oubliez pas de **initialiser `prev = nullptr`** et de le placer **dans la boucle** (`prev = lent`). Cela évite un autre "check" après la boucle.

---

C'est vrai. Comment discuter pendant une entrevue

1. ** Clarifier la définition de "middle"* *
> Vous voulez le nœud à l'index `floor(n/2)`? - Confirmez.

2. **Demander des contraintes**
> Toute limite supérieure sur la taille de la liste? Cela vous permettra de décider entre les approches O(n) et O(log n).

3. **Exposer la solution à deux points* *
* Dessinez les pointeurs sur un tableau blanc.
* Montrez que l'algorithme fonctionne en un seul passage.
* Discutez pourquoi nous avons besoin d'un pointeur `prev` pour déconnecter.

4. **Cas de bord des peines**
* Liste vide → `null`
* Un noeud → `null`

5. **Optionnel** – montrez la solution basée sur la longueur si l'intervieweur demande une approche différente.
* Complexité : temps O(n), espace O(1) (même que deux points).
* Plus simple à raisonner, mais nécessite une seconde traversée.

6. **Complexité temporelle et spatiale**
* "O(n)" temps, "O(1)" espace.
* Vous pouvez toujours demander : *=Une solution O(n2) est-elle acceptable ? Je ne pense pas, parce que nous pouvons le faire en un seul passage.

---

Variations pour impressionner

Qu'est-ce qu'il faut mettre en évidence
-- -- -- -- -- -- -- -- --
Autres **Retourner le nœud supprimé**= Utile pour les problèmes qui demandent =delete milieu et retourner sa valeur. Autres
Autres **Handle Doubly Linked Lists**= Légère modification: il suffit de supprimer `prev->next` et de définir `prev->next->prev = prev`.=
** Listes circulaires** Adapter les pointeurs à la détection du cycle (`fast = fast->next->next`). Autres
**Retrouver Médiane dans la liste triée**= Fusionner cette logique avec une approche de type binaire de recherche. Autres

Le fait de mentionner ces variations montre que vous n'êtes pas seulement mémoriser, mais vraiment comprendre le modèle.

---

### 7--Des conseils d'entrevue

Question: Comment répondre
C'est pas vrai.
Autres Peut-on résoudre cela sans espace supplémentaire ? Autres
Autres Qu'en est-il d'une liste vide ou un seul noeud? Retour `null`. Autres
Pourquoi deux pointeurs au lieu de compter ? Autres
Autres Et si la liste est énorme et que vous ne pouvez pas stocker tous les nœuds ? Toujours bien – l'algorithme ne garde que des références. Autres
Qu'est-ce que le pire des cas ? Linéaire; pas de boucles nichées. Autres

> **Format STAR**
> *S – Situation (problème lié à la liste)*
> *T – Tâche (supprimer le milieu)*
> *A – Action (algorithme à deux points)*
> *R – Résultat (O(n) temps, O(1) espace)*

---

Ajouter Ceci à votre CV

Texte
- LeetCode 2095 résolu Supprimer le nœud moyen d'une liste liée en utilisant le pointeur rapide/lent (temps O(n), espace O(1)).
- Manipulation efficace des pointeurs et algorithmes à passe unique optimaux.
«» "

N'hésitez pas à vous connecter à la repo GitHub où vit le code, ou à ajouter la solution à un portefeuille personnel. Les employeurs adorent voir le vrai code en plusieurs langues.

---

Appel à l'action

Si vous avez déjà fait face à une question liée à une liste dans une entrevue, vous savez à quel point elle peut vous intimider.
Mais avec la bonne approche, c'est **le genre de problème qui met en évidence vos problèmes de résolution de problèmes**.

**Vous voulez vous entraîner? **
Essayez les variations :
* Supprimer le centre *noeud* dans une liste ** doublement liée**.
* Trouvez la valeur *médiane* dans une liste triée.
* Supprimer *k-th noeud de la fin* (CodeLeet 19).

---

À emporter pour votre chasse à l'emploi

* **Afficher la technique à deux points** dans vos notes d'entrevue; c'est un modèle pour les questions de liste liée.
* **Dépliez les cas de bord** à l'avance – les intervieweurs aiment quand les candidats les traitent avec grâce.
* **Mention de l'angle spécifique à l'entrevue** – p.ex., (en milliers de dollars)
* **Lien vers votre GitHub** avec les solutions Java/Python/C++ dans le CV ou le portfolio.

Avec ces implémentations, explications et stratégies d'entrevue dans votre boîte à outils, vous êtes prêt à transformer le problème *Supprimer le nœud moyen* en une victoire d'entrevue confiante – et un article de blog convivial que les recruteurs adoreront lire!