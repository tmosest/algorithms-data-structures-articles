---
titre: LeetCode 2181. Fusionner des nœuds entre zéros -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2181 – Fusionner des nœuds entre zéros
*Liste liée, O(n) – Un laissez-passer, O(1) Espace*

---

Aperçu du problème
On vous donne une liste en lien unique qui commence et se termine par un noeud de valeur **0**.
Entre chaque paire de zéros il y a un bloc non vide de nombres positifs.
Pour chaque bloc, vous devez **sum** toutes ses valeurs et remplacer le bloc par un seul noeud** qui contient cette somme.
Tous les nœuds zéro sont supprimés dans la liste finale.

«» "
Entrée : 0 → 3 → 1 → 0 → 4 → 5 → 2 → 0
Sortie: 4 → 11
«» "

> **Constraints**
3 ≤ n ≤ 2·105
> 0 ≤ Node.val ≤ 1000
> • Pas de deux zéros consécutifs
> • La tête et la queue sont toujours 0

---

# # # Une perspective fondamentale

*Il vous suffit d'un seul scan de la liste. *
Passez par la liste, gardez une somme en cours d'exécution jusqu'au prochain zéro.
Quand un zéro est atteint:

1. Écrivez la somme accumulée dans le nœud * juste avant* le zéro.
2. Sautez le zéro et les nœuds suivants qui appartiennent au bloc suivant.

En utilisant une tête **dummy** (ou en commençant par `head.next`), le pointeur met à jour de façon triviale et élimine le besoin de contrôles de cas de bord.

---

##  uvres de référence

### A. Java – Style Leetcode

"Java
***
* Définition pour une liste liée.
* Liste de classe publiqueNode {
* Int val;
* ListNode suivant;
* ListNode(int val) { this.val = val; }
* ListNode(int val, ListNode next) { this.val = val; this.next = next; }
*}
*/
solution de classe {
public ListNode mergeNodes(ListNode head) {
// tête est le premier zéro, nous commençons par le noeud après
ListNode curr = head.next; // noeud où nous allons écrire la somme
ListNode runner = curr; // pointeur qui se déplace jusqu'au zéro suivant

pendant que (runner != null) {
= 0;

// accumuler jusqu'à ce que nous touchions un zéro
pendant que (runner.val != 0) {
somme += coureur.val;
coureur = coureur.suivant;
}

// remplacer la valeur du noeud actuel par la somme
curr.val = somme;

// saute le curr zéro et avance au début du bloc suivant
coureur = coureur.next; // passer le zéro
curr.next = coureur; // se connecter au bloc suivant (ou null)
curr = curr.next; // déplacer curr vers l'avant
}

// head.next est le nouveau chef de la liste fusionnée
retour tête.suivant;
}
}
«» "

---

### B. Python – Style Leetcode

'`python
# Définition pour une liste liée.
# class ListNode:
# def __init_(self, val=0, next=None):
# Self.val = val
# self.next = next

Solution de classe:
def mergeNodes(self, head: ListNode) -> Numéro de liste:
# tête est zéro, commencer par le noeud après
curr = head.next # noeud qui recevra la somme
Coureur = coureur

pendant le coureur:
Total = 0
pendant que coureur.val != 0:
Total += coureur.val
coureur = coureur.next

curr.val = total # écrire la somme
coureur = coureur.next # sauter le zéro
curr.next = coureur
curr = curr.next

retour tête.suivant
«» "

---

### C. C++ – Style Leetcode

'`cpp
***
* Définition pour une liste liée.
* struct ListNode {
* Int val;
* Numéro de liste * suivant;
* ListNode(int x) : val(x), next(nullptr) {}
* };
*/
solution de classe {
public:
ListeNode* fusionNodes(ListNode* tête) {
// tête est le premier zéro, à partir du nœud suivant
ListNode* curr = head->next; // noeud pour écrire la somme
ListNode* coureur = coureur;

pendant que (le pilote) {
= 0;
alors que (runner->val != 0) {
somme += coureur->val;
coureur = coureur->suivant;
}

curr->val = somme; // écrire la somme
coureur = coureur->suivant; // sauter le zéro
curr->next = coureur;
curr = curr->next;
}
retour tête->suivant; // nouvelle tête
}
};
«» "

---

Les bons, les mauvais, les affreux

Aspect du bien
- C'est quoi ?
Autres **Complexité du temps**
Autres **Complexité spatiale**
**Manipulation d'un boîtier d'Edge**= Le nœud dummy ou `head.next` élimine les contrôles aux frontières== L'oubli de sauter le zéro peut créer une boucle infinie== En utilisant une mémoire supplémentaire (p. ex., pile) quand elle n'est pas nécessaire==
**Readability**= Effacer les noms de variables (`curr`, `runner`, `sum`)== La gymnastique verbose pointer peut confondre==L'utilisation de la récursion sur une liste liée peut déborder la pile==
**Maintenabilité**= État minimal, mises à jour simples== Aucune=Lisez les boucles imbriquées difficiles à lire avec de nombreuses pauses==

---

## Comment les éviter

1. **Éliminer le dernier zéro**
*Si vous arrêtez avant la queue zéro, vous manquerez le dernier bloc. *
**Solution** – Toujours vérifier `runner != null` dans la boucle extérieure et terminer la boucle intérieure quand `runner->val == 0`.

2. **Concevoir des nœuds avant de terminer un bloc* *
*Mettre à jour `curr->val` trop tôt va perdre des données pour la prochaine somme. *
**Solution** – Calculer `sum` d'abord, puis l'écrire après la fin de la boucle intérieure.

3. **Déréférencement du pointeur nucléaire**
*Running `runner->val` quand `runner` est "nullptr". *
**Solution** – Surveillez la boucle externe avec `alors que (runner != nullptr)`.

4. **Non mise à jour `curr->next` correctement* *
*Passer trop ou trop peu de nœuds. *
**Solution** – Après avoir calculé la somme, faire `runner = coureur->next` (déplacer le zéro) et ensuite `curr->next = coureur`.

---

Pourquoi ce problème se pose-t-il pour les entrevues

* **La maîtrise de la liste liée** – Chaque développeur senior doit être à l'aise manipulant des pointeurs.
* **One-pass, solution O(1)** – Démontre l'efficacité algorithmique.
* **Connaissance au cas par cas** – Il est facile de passer à côté des règles « 0 » sans deux zéros consécutifs.
* **Traitement** – Vous pouvez discuter des compromis temps/espace et justifier votre approche fictive-noeud.

---

Comment montrer ça sur votre CV

Texte
- Mise en œuvre de solutions O(n) pour les nœuds de fusion entre zéros (Leetcode #2181), un défi algorithmique lié à la liste.
- Optimisé la complexité de l'espace à O(1) en effectuant des mises à jour en place des nœuds et en éliminant les structures auxiliaires de données.
- Démonstration de compétences robustes en manipulation de pointeurs en Java, Python et C++ sur plusieurs plateformes.
«» "

> Mettre en évidence *temps/espace*, *en place*, *simple-pass*, *pointer gymnastique*, *simple-pass*, les recruteurs de mots clés dans les entreprises technologiques aiment.

---

Liste de contrôle de la préparation de l'entrevue

1. ** Expliquer le problème** (utiliser la description et les contraintes).
2. **Settch l'algorithme** sur un tableau blanc ou un papier:
*Traverse → Somme → Écrire → Passer à zéro → Répéter. *
3. **La complexité de l'État** et pourquoi elle est optimale.
4. **Run à travers les caisses de bord** (bloc unique, longue liste, etc.).
5. **Afficher le code** dans au moins une langue, puis mentionner que vous pouvez le porter.
6. **Réponse: Et si nous avions plus de zéros? Utilisez la même approche, elle sera toujours O(n).

---

##== SEO–Friendly Takeaway

> Si les recruteurs sont à la recherche de questions d'entrevue liées à la liste, de codes 2181 ou de numéros de fusion dans les solutions Entre zéros en Java, Python ou C++, cet article est parfait.
> Utilisez les mots-clés **Liste de liens, Merge Nodes, Leetcode 2181, Java, Python, C++, One Pass, O(n), O(1) Space** dans les titres de blog, les méta descriptions et les rubriques pour améliorer la découverte.

---

Démarrage rapide de l'harnais de test (Python)

'`python
def build_list(nums) :
mannequin = Numéro de liste(0)
arrière = mannequin
pour n en nombres:
tail.next = ListNode(n)
queue = queue.next
retour mannequin.suivant

def print_list(head):
vals = []
pendant la tête:
Vals.append(str(head.val))
tête = tête.next
print(" → ".join(vals))

# Exemple
tête = build_list([0,3,1,0,0,4,5,2,0])
print("Avant:", fin de ")
print_list(head)

fusion = Solution().mergeNodes(head)
print("Après :", fin")
print_list(fusionné)
«» "

---

Autre lecture

Problème Qu'est-ce qu'il enseigne Lien
- C'est quoi ?
Leetcode 234 – **Palindrome Linked List** Autres
Leetcode 2 – **Ajouter deux nombres** Autres
Leetcode 443 – **Compression de la chaîne de données** Autres

---

La pensée finale
Maîtrise **Merge Nodes in Between Zeros** met en évidence votre capacité à penser en termes de **pointeurs**, d'optimisation de l'espace** et de manipulation de l'espace sur les bords de buste**.
Ce sont les qualités exactes que les gestionnaires d'embauche dans les équipes de génie logiciel recherchent.
Ajoutez les extraits de code ci-dessus à votre portfolio, lancez-les sur Leetcode ou votre propre IDE, et soyez prêt à discuter des compromis lors de votre prochaine entrevue. Bonne chance, et que le code soit avec vous!