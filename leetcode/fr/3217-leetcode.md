---
titre: LeetCode 3217. Supprimer les nœuds de la liste liée présente dans le tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> **LeetCode #3217 – Supprimer les nœuds de la liste liée présente dans le tableau* *
> Compte tenu d'un tableau «nums» et de la tête d'une liste liée, supprimer les nœuds **all** dont les valeurs apparaissent dans «nums».
> Retournez le chef de la liste modifiée.

**Contrôles* *

Valeur des contraintes
C'est pas vrai.
1 ≤ longueur nominale ≤ 105
< 1 ≤ nombres[i] ≤ 105 %
Autres Tous les éléments `num` sont uniques
Taille de la liste liée «1 ... 105»
< 1 ≤ node.val ≤ 105 >
Autres Au moins un noeud est **non** enlevé

Le problème est une question d'entrevue classique qui teste:
* Utilisation du set de hachage
* manipulation de la liste liée
* compromis temps/espace

Ci-dessous vous trouverez des solutions propres et prêtes à la production dans **Java, Python et C++** – toutes en utilisant une seule traversée de la liste et un ensemble de recherche O(1).
Après le code, vous trouverez un *blog-style guide* qui explique le bon, le mauvais, et le laid de ce problème et est SEO-optimized pour vous aider à poser votre prochaine entrevue de codage.

---

- Oui. 2. Solutions de référence

Autres Les trois implémentations utilisent la même idée :
> 1. Construisez un hash‐set (`unordered_set` / `HashSet` / `set`) à partir de `nums`.
> 2. Marcher la liste liée avec une tête factice.
> 3. Sautez les nœuds dont la valeur est dans le jeu, sinon gardez-les.
> 4. Retour `dummy.next`.

### 2.1 Java

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
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe publique {
public ListNode deleteNodes(int[] nums, ListNode head) {
// 1. Construire l'ensemble de valeurs à supprimer
Définir <integer> àDelete = nouveau HashSet<>(nums.longueur);
pour (int v : nombres) àDelete.add(v);

// 2. Dummy tête simplifie les cas de bord
mannequin ListNode = nouveau ListNode(0);
mannequin.next = tête;
ListNode prev = mannequin, curr = tête;

// 3. Marcher la liste une fois
pendant que (curr != null) {
si (àSupprimer.contient(curr.val)) {
// sauter ce nœud
prev.next = curr.next;
} autre {
prev = curr; // le conserver
}
curr = curr.next;
}
retour mannequin.suivant;
}
}
«» "

---

2.2 Python

'`python
# Définition pour une liste liée.
Numéro de la classe:
def __init_(self, val=0, next=None):
autoval = val
self.next = suivant

Solution de classe:
def deleteNodes(self, nums, head):
# 1. Construisez l'ensemble de valeurs à supprimer
to_delete = set(nums)

# 2. Tête idiote pour gérer les suppressions à l'avant
mannequin = Numéro de liste(0)
factice.next = tête
prév, curr = mannequin, tête

3. Pass unique
alors que:
si curr.val dans to_delete:
prev.next = curr.next # skip
Sinon:
prev = durée de conservation
curr = curr.next

retour mannequin.suivant
«» "

---

C++

'`cpp
***
* Définition pour une liste liée.
* struct ListNode {
* Int val;
* Numéro de liste * suivant;
* ListNode(int x) : val(x), next(nullptr) {}
* };
*/
#inclut <unordered_set>

solution de classe {
public:
ListNode* deleteNodes(vector<int>& nums, ListNode* head) {
// 1. Hash-set pour les recherches O(1)
unordered_set<int> àDelete(nums.begin(), nums.end());

// 2. Noeud pour éviter les cas spéciaux
Le numéro de liste du mannequin(0);
mannequin.next = tête;
Numéro de liste *prev = &dummy, *curr = tête;

// 3. Un laissez-passer
pendant que (curr) {
si (àSupprimer.count(curr->val)) {
prev->next = curr->next; // skip
} autre {
prev = curr; // conserver
}
curr = curr->next;
}
retour mannequin.suivant;
}
};
«» "

---

- Oui. 3. Article du blog – *Le bon, le mauvais, et le lamentable de supprimer les nœuds d'une liste liée*

> **SEO Mots-clés**: supprimer les nœuds de la liste liée, questions d'entretien de la liste liée, leetcode 3217, liste liée Java, liste liée Python, liste liée C++, conseils d'entretien, ensemble de hachage, complexité du temps, complexité de l'espace, codage d'entretien d'emploi

---

3.1 Introduction

Les listes liées sont la base **** de nombreuses questions d'entrevue.
L'un des twists les plus courants : Retirez tous les nœuds qui contiennent une valeur d'un tableau donné. (en milliers de dollars)
Vous l'avez probablement vu sur LeetCode (Problème 3217) ou dans un entretien technique.
Il semble simple, mais obtenir les cas de coin droit et fournir une solution optimale peut être difficile.

Laissez tomber **le bon**, **le mauvais**, et **le laid** de ce problème.

---

3.2 Le bon : pourquoi c'est un excellent test d'entrevue

Autres Pourquoi Comment ça te teste
-- -- -- -- -- --
**Manipulation de la structure des données**Vous devez comprendre les pointeurs (ou les références) et comment changer en toute sécurité les liens `next`. Autres
Vous devez convertir un tableau en un ensemble de recherche O(1). Autres
Vous devriez réaliser que vous ne pouvez pas vous permettre de traverser la liste plusieurs fois. Autres
**Manipulation d'un boîtier d'Edge** Autres
**Scalabilité**La taille de l'entrée peut être jusqu'à 100 k – donc le temps O(n) et l'espace supplémentaire O(1) sont la tache douce. Autres

Pour les intervieweurs, il s'agit d'une question **compact, vous comprenez-vous les pointeurs + hash‐set?

---

3.3 Les mauvaises: pièges communs

Pourquoi il casse
C'est quoi ?
**Ne pas utiliser une tête factice**= Si le premier nœud est supprimé, vous perdrez la référence à la nouvelle tête. Autres
**Modification de `next` incorrectement**. Autres
**Le type de données Wong pour l'ensemble**L'utilisation d'une liste ou d'un tableau pour la recherche donne O(n) par noeud → O(n2) temps. Autres
**En supposant que le tableau d'entrée est trié**= De nombreux candidats essaient par erreur la recherche binaire; le tableau peut être trié. Autres
**Pas de traitement de suppression de suppression de suppression de suppression de suppression de suppression de suppression de suppression Autres
**Donnez le type de retour**Le retour du noeud factice au lieu de `dummy.next` donne une liste vide. Autres

Éviter ces pièges montre que vous comprenez la mise en page de la mémoire de liste liée et la théorie des ensembles.

---

### 3.4 L'indulgence :

Variante
C'est quoi, ça ?
**Supprimer les nœuds par *value* au lieu de *index***.Vous devez convertir les valeurs en un ensemble, pas des positions. Autres
Le tableau peut contenir des valeurs allant jusqu'à 105, mais vous devez toujours garder la recherche O(1). Autres
**Delete multithreaded** (Rarely demanded) Vous devez verrouiller la liste ou utiliser une structure de données concurrente. Autres
**Liste de liens avec des pointeurs aléatoires**= S'il s'agissait d'une liste de liens *doubly* ou d'une «prev», vous devez mettre à jour les deux côtés. Autres
**Liste immuable**= Certaines langues exposent des listes immuables; vous devez construire une nouvelle liste. Autres

Dans une vraie interview, les variantes de "gugly" se présentent souvent sous la forme d'un suivi **curve-ball** Et si le tableau est énorme ? Que faire si la liste est une liste à double lien?

Montrez que vous pouvez **adapter** l'idée centrale (hash-set + un seul passage) aux nouvelles contraintes.

---

### 3.5 Solution optimale

Texte
1. Construisez un hachage à partir du tableau.
2. Créer un nœud factice pointant vers la tête d'origine.
3. Itérer avec deux pointeurs: prev (à partir du mannequin) et curr.
4. Si curr.val est dans le jeu : prev.next = curr.next // skip
Sinon: prev = curr // tenir
5. Déplacer curr = curr.next.
6. Revenir mannequin. suivant.
«» "

*Heure*: **O(n + m)** → O(n) parce que `m` = `nums.longueur "
*Espace*: **O(m)** pour le jeu, **O(1)** pointeurs supplémentaires.

Avec `m ≤ 105`, un hachage est le seul moyen réaliste de rester dans les délais.
Toutes les bibliothèques standard de langues vous donnent une structure **non ordonnée** ou **hash** qui fait exactement cela.

---

#### 3.6 Edge- Liste de contrôle des cas

Que vérifier ?
C'est quoi ?
Autres La tête est supprimée. Autres
Autres Tail est supprimé. Autres
Autres Tous les nœuds supprimés sauf un Loop continue jusqu'à ce que `curr` soit `null`. Autres
Autres Aucun noeud n'est supprimé. Autres
Tableau vide (pourvu de contraintes) Vous pouvez vous en protéger, mais la spécification garantit au moins une valeur. Autres

Tester contre un petit conducteur comme:

'`python
# liste de construction & #160;: 1->2->3->4
tête = ListNode(1, ListNode(2, ListNode(3, ListNode(4)))
nombres = [2, 4]
résultat = Solution().deleteNodes(nombres, tête)
# résultat doit être 1->3
«» "

vous assure d'être prêt pour l'étui d'angle "No-deletion".

---

### 3.6 Entretien– Conseils prêts

Motif
- Oui.
**Expliquez votre plan avant de coder** Autres
**Parler à travers les mises à jour du pointeur** Autres
**Demander des questions claires** Il faut préserver l'ordre ? Autres
**Mention temps/espace compromis** Autres
**Écrire un petit harnais d'essai** Dans l'interview, vous pouvez exécuter un test mental rapide ou même un Python REPL rapide pour prouver votre logique. Autres
**Utilisez une tête factice**C'est une protection que vous n'oublierez jamais. Autres

---

3.7 Comment cet article vous aide à trouver un emploi

* Le **code samples** vous donne une référence de copie-colle rapide.
* Les sections **blog** mettent en évidence les pièges d'entrevue courants, de sorte que vous pouvez vous vanter de *pas* tomber pour eux.
* Les tags **SEO** aident les recruteurs à trouver cet article lors de la recherche de questions d'entretien de liste liées. (en milliers de dollars)

**Next Step**: collez l'une des solutions de référence dans votre IDE, exécutez les tests d'échantillon et soyez confiant en expliquant l'algorithme dans votre prochaine interview.

---

3.8 Pensée de clôture

Les listes reliées demeureront un élément essentiel des entrevues de codage pendant des années.
Maîtriser ce problème de "supprimer les nœuds" non seulement vous donne un algorithme **winning** mais aussi démontre:

1. **Les pointeurs ne sont pas seulement un concept théorique** – ils sont un outil réel.
2. **Les ensembles deash sont votre ami le plus rapide** quand le temps compte.
3. **Les solutions monopass sont la norme d'or** pour les contraintes de taille d'entrevue.

Montrez-vous, apportez une tête factice, et vous partirez avec plus qu'une réponse juste – vous partirez avec un signal que vous *really comprendre* data-structures.

Bonne chance, et le codage heureux!