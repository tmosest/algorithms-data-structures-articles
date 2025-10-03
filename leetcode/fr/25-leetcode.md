---
titre: LeetCode 25. Noeuds inversés en groupe k -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Coulisses inversées du groupe K – Un guide complet (Java-Python C++)

> **Mots clés:** Noeuds inversés dans le groupe K, LeetCode 25, Liste liée, Interview, Java, Python, C++, O(1) espace, Récursion, Itération

---

Introduction

Les listes liées sont un élément essentiel des entrevues techniques.
**Les nœuds inverses en K‐Group** (LeetCode 25) est un problème classique qui teste votre capacité à:

* Manipulez les pointeurs soigneusement
* Boîtes de bord de poignée (moins de nœuds *k* gauche)
* Optimiser pour O(1) espace supplémentaire

La solution est souvent un point tournant entre un candidat solide et un candidat juste passé. Cet article vous fait découvrir les parties **good**, **bad** et **ugly** du problème et fournit un code propre et prêt à la production en **Java, Python et C++**.

---

#### 2-

> Avec une liste liée, inverser les nœuds **k** à la fois et retourner la liste modifiée.
> *Si le nombre de nœuds n'est pas un multiple de k, les nœuds restants restent dans l'ordre original. *

Texte
Entrée : 1 -> 2 -> 3 -> 4 -> 5, k = 2
Produit: 2 -> 1 -> 4 -> 3 -> 5
«» "

Contraintes:

* 1 ≤ k ≤ n ≤ 5000
* 0 ≤ Node.val ≤ 1000

---

Analyse et stratégie

C'est bien, c'est mal.
C'est pas vrai.
**Bon** – Le problème se réduit à *=renverser chaque sous-segment de taille k=*.= **Bad** – Les erreurs hors-par-un dans les mises à jour des pointeurs sont courantes.= **Ugly** – La profondeur récursive peut exploser si k = 1, faisant usage de la pile O(n). Autres

L'opération principale est **in-place inversion** d'un sous-segment.
Nous avons deux modèles populaires:

1. **Récursif** – propre et intuitif, mais espace de pile O(n).
2. **Itératif avec tête de mannequin** – O(1) mémoire supplémentaire, un peu plus verbeux mais parfait pour les intervieweurs qui se soucient de l'espace.

Les deux modèles partagent un helper qui trouve le nœud *k‐th* d'un début donné et une routine qui inverse les pointeurs entre deux nœuds.

---

#### 4-

#### 4.1 Aide: Trouver le noeud k

Texte
début -> 1 -> 2 -> 3 -> 4 -> 5
k = 3
«» "

À partir de `start`, déplacez `k` étapes.
Si nous atteignons `null` avant de prendre `k` pas, le segment est trop court.

4.2 Réverser un segment

Nous retournons les pointeurs entre `head` (inclus) et `tail` (exclusif).
Approche typique à trois points :

«» "
prev = null
cur = tête
alors que cur != queue:
nxt = cur.next
cur.next = prev
prev = cur
cur = nxt
retour prev // nouvelle tête du segment inversé
«» "

4.3 Algorithme itératif (espace O(1))

1. Créer un nœud factice pointant vers la «tête».
2. `groupPrev` = mannequin.
3. Bien que vrai:
* Trouvez `k`-th noeud après `groupPrev`. Si aucune → pause.
* `groupeNext` = `kth.next`.
* Inverser de `groupPrev.next` jusqu'à `groupNext`.
* Reconnecter :
* `groupePrev.next` = `kth` (nouvelle tête)
* `oldHead.next` = `groupNext "
* Déplacer `groupPrev` vers `oldHead` (qui devient la queue du segment inversé).
4. Retour `dummy.next`.

---

C'est vrai. Complexité

Métrique Récursion Itération
C'est pas vrai.
Heure O(n)
L'espace O(n/k)

---

Code

#### # 6.1 Java (itératif)

"Java
***
* Définition pour une liste liée.
* numéro de classe {
* Int val;
* ListNode suivant;
* ListNode(int x) { val = x; }
*}
*/
solution de classe publique {
public ListNode inverse KGroup(ListNode head, int k) {
si (tête) 1) tête de retour;

// Noeud pour gérer les changements de tête
mannequin ListNode = nouveau ListNode(0);
mannequin.next = tête;
Groupe ListNodePrev = mannequin;

alors que (vrai) {
// Trouver le noeud k-th
ListNode kth = getKthNode(groupPrev, k);
si (kth == null) rupture;
Groupe ListNodeNext = kth.next;

// Inverser ce groupe
ListNode prev = kth.next;
ListNode cur = groupePrev.next;
pendant que (cur != groupeNext) {
ListNode tmp = cur.next;
cur.next = prev;
prév = cur;
cur = tmp;
}

// Reconnecter
ListNode tmp = groupePrev.next; // vieille tête devient queue
groupePrev.next = kth; // nouvelle tête
groupePrev = tmp; // passer au groupe suivant
}

retour mannequin.suivant;
}

// Renvoie le noeud k-th depuis le début, ou null si pas assez de nœuds
private ListNode getKthNode(ListNode start, int k) {
pendant que (démarrer != null && k > 0) {
start = start.next;
k--;
}
retour du départ;
}
}
«» "

##### 6.2 Python (itératif)

'`python
# Définition pour une liste liée.
Numéro de la classe:
def __init_(self, val=0, next=None):
autoval = val
self.next = suivant

Solution de classe:
arrière KGroupe(même, tête: ListNode, k: int) -> Numéro de liste:
si ce n'est pas la tête ou k == 1 :
tête de retour

mannequin = ListNode(0, tête)
group_prev = mannequin

alors que Vrai:
kth = self.get_kth_node(group_prev, k)
si non kth:
pause
group_next = kth.next

# Groupe inversé
prev, cur = kth.next, groupe_prev.next
alors que cur != _suivant de groupe :
nxt = cur.next
cur.next = prev
prev = cur
cur = nxt

# Reconnecter
tmp = groupe_prev.next
group_prev.next = kth
group_prev = tmp

retour mannequin.suivant

def get_kth_node(self, start: ListNode, k: int) -> Numéro de liste:
pendant le début et k:
start = start.next
k -= 1
retour du début
«» "

*### 6.3 C++ (Itératif)

'`cpp
/* Définition pour une liste liée. */
struct Node de la liste {
la valeur intérieure;
Numéro de liste *suivant;
ListNode(int x) : val(x), next(nullptr) {}
};

solution de classe {
public:
ListNode* inverseKGroup(ListNode* tête, int k) {
Si c'est le cas ! 1) tête de retour;
Le numéro de liste du mannequin(0);
mannequin.next = tête;
Groupe ListNode*Prev = &dummy;

alors que (vrai) {
ListNode* kth = getKthNode(groupPrev, k);
si (!kth) pause;
Groupe ListNode*Next = kth->Next;

// Inverser
ListNode* prev = groupeNext;
ListNode* cur = groupePrev->next;
pendant que (cur != groupeNext) {
ListNode* nxt = cur->next;
cur->next = prev;
prév = cur;
cur = nxt;
}

// Reconnecter
ListNode* tmp = groupePrev->next; // vieille tête
groupePrev->next = kth; // nouvelle tête
groupePrev = tmp; // passer au groupe suivant
}
retour mannequin.suivant;
}

particulier:
ListNode* getKthNode(ListNode* start, int k) {
pendant que (démarrer && k) {
start = start->next;
--k;
}
retour du départ;
}
};
«» "

---

### # 7-

Pourquoi ça arrive ?
- Oui.
**Off‐by‐one** pour trouver le nœud kth Prev` peut retourner `null` même si le segment est valide. Utiliser une boucle *dummy* et **strict** (pendant ce temps (k--) 0)') pour assurer un décompte correct. Autres
**Dangling pointer** après inversion. Toujours reconnecter le groupe après inversion; utiliser des variables temporaires. Autres
**Profondeur de récursion**= k = 1 = chaque appel traite un noeud → n appels. Préférez une solution itérative si les intervieweurs mentionnent l'espace O(1). Autres
**Modification de la liste d'entrées en dehors de la fonction** Retour `dummy.next` (ou la tête d'origine si aucun renversement). Autres
Autres **Déréférencement du pointeur de la Null**. Autres

---

### 8-- Interview-Amis Conseils

1. **Démarrer avec un nœud factice** – Il élimine la manipulation spéciale pour la tête.
2. **Écrire un assistant pour `getKthNode`** – Garde la boucle principale propre.
3. **Utilisez un retournement à trois points** – Démontre la maîtrise de la manipulation du pointeur.
4. ** Expliquez votre logique de reconnection** – Les intervieweurs aiment vous voir expliquer pourquoi `groupe Préc` se déplace vers la queue du segment inversé.
5. **Afficher la complexité** – Mention O(1) espace et pourquoi la version itérative est préférable pour les grandes listes.

---

Variantes et extensions

Variante Les changements Comment s'adapter
C'est pas vrai.
**Réverser dans l'ordre inverse (k = n)**
**L'inversion du lot avec la variable k**
Vous pouvez utiliser `.prev` pour simplifier l`inversion.

---

Conclusion

*Les nœuds inverses dans K‐Group* n'est pas seulement un exercice de pointeur – c'est un **diagnostic** de la façon dont vous pensez aux structures de données, aux cas de bord et à la gestion de la mémoire.
En maîtrisant la solution itérative O(1) spatiale (voir ci-dessus) et en étant prêt à discuter de l'alternative récursive, vous démontrerez à la fois **code propre** et **sensibilité à l'ingénierie** – exactement ce que les gestionnaires d'embauche recherchent.

**Suivant:** Autres LeetCode liés– Les défis de la liste comme *=Supprimer Nth Node From End of List=25 et *==Merge k Tried Lists==23 s'appuient sur les mêmes fondamentaux. Continuez à vous entraîner !

---

Références

* Problème de LeetCode 25 : <https://leetcode.com/problèmes/reverse-nodes-in-k-group/>
* Tutoriel YouTube par l'OP (bon, mauvais, laid): <https://yooutu.be/votre_video_link_ici>
* Définitions officielles Java/Python/C++ – <https://leetcode.com/problems/reverse-nodes-in-k-group/solutions/>

---

** Bon codage et bonne chance pour votre prochaine entrevue! * *