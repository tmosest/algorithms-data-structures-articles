---
titre: LeetCode 2130. Somme Jumelée maximale d'une liste liée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2130 – *Somme Jumelle Maximum d'une Liste liée*
> **Champ de langage cible:** **Java, Python, C++**
> **Complexité temporelle:** `O(n)`
> **Complexité spatiale:** (en place)

---

Récapitulation des problèmes

> *On vous donne une liste en lien unique avec un nombre **même** de nœuds.
> Le nœud «i» est le nœud «n‐1‐i».
> La somme double est "valeur(i) + valeur(n‐1‐i)".
> Retournez la somme double maximale ****. *

Exemples

Entrée Sortie Explication
C'est pas vrai.
= 6, 4+2 = 6 → max = 6
4+3 = 7, 2+2 = 4 → max = 7
Un seul couple

> **Constraints**
> * `2 <= n <= 105` (n est égal)
> * `1 <= noeud.val <= 105`

---

Aperçu de l'algorithme

1. **Trouver le milieu de la liste* *
*Two-pointer (lent/rapide)*: `slow` déplace un pas, `fast` deux pas.
Lorsque `fast` atteint la fin, `slow` est au nœud `n/2`.

2. **Reverser la deuxième moitié* *
Inverser la liste à partir de `slow`.
Maintenant, chaque paire jumelle est dans les nœuds adjacents : premier noeud de demi-nœud -inversé second noeud de demi-nœud.

3. **Traverser les deux moitiés simultanément**
Marcher depuis la tête d'origine et la tête de la seconde moitié inversée, en additionnant les valeurs des nœuds et en conservant le maximum.

4. **(Facultatif) Restaurer la liste** – pas nécessaire pour la réponse LeetCode mais bonne pratique pour les intervieweurs.

L'astuce est de faire toutes les étapes *en place* afin que l'utilisation de la mémoire reste `O(1)`.

---

C'est vrai. Code de référence

> **Java**
> **Python**
> **C++**

> Les trois implémentations partagent la même logique – une syntaxe différente.

```markdown
Java 17

"Java
***
* Définition pour une liste liée.
*/
classe ListNode {
la valeur intérieure;
ListNode suivant;
ListNode(int val) { this.val = val; }
}

solution de classe publique {
paire d'inte publiqueSum(ListNode head) {
// 1
ListNode lent = tête, rapide = tête;
alors que (fast != null && fast.next != null) {
lent = lent.next;
fast = fast.next.next;
}

// 2--
ListNode prev = nul, curr = lent;
pendant que (curr != null) {
ListNode suivant = curr.next;
curr.next = prev;
prev = curr;
curr = suivant;
}

Calculer les sommes jumelles
Int maxSum = 0;
ListNode p1 = tête, p2 = prev;
alors que (p2 != null) { // p2 a n/2 nœuds
maxSum = Math.max(maxSum, p1.val + p2.val);
p1 = p1.suivant;
p2 = p2.suivant;
}
retour maxSum;
}
}
«» "

```markdown
Python 3

'`python
# Définition pour une liste liée.
Numéro de la classe:
def __init_(self, val=0, next=None):
autoval = val
self.next = suivant

Solution de classe:
def pairSum(self, tête: ListNode) -> Int:
N° 1 Trouver le milieu
lente = rapide = tête
tandis que rapide et rapide.next:
lent = lent.next
rapide = rapide.next.next

N° 2 Deuxième moitié inverse
prev = Aucune
curr = lent
alors que:
nxt = curr.next
curr.next = prév
prev = curr
pourr = nxt

N° 3 Calculer les sommes jumelles
max_sum = 0
p1, p2 = tête, prév
alors que p2: # p2 a n/2 nœuds
max_sum = max(max_sum, p1.val + p2.val)
p1 = p1.suivant
p2 = p2.suivant
_somme maximale de retour
«» "

```markdown
C++17

'`cpp
***
* Définition pour une liste liée.
*/
struct Node de la liste {
la valeur intérieure;
Numéro de liste *suivant;
ListNode(int x) : val(x), next(nullptr) {}
};

solution de classe {
public:
couple intSum(tête ListNode*) {
// 1
ListNode *slow = tête, *fast = tête;
alors que (rapide & & rapide->suivant) {
lent = lent->suivant;
fast = fast->next->next;
}

// 2--
ListNode *prev = nulptr, *curr = lent;
pendant que (curr) {
ListNode *nxt = curr->next;
curr->next = prev;
prev = curr;
curr = nxt;
}

Calculer les sommes jumelles
Int maxSum = 0;
ListNode *p1 = tête, *p2 = prev;
alors que (p2) { // p2 a n/2 nœuds
maxSum = md:max(maxSum, p1->val + p2->val);
p1 = p1->suivant;
p2 = p2->suivant;
}
retour maxSum;
}
};
«» "

---

C'est pas vrai. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Temps**=O(n) – passe unique pour trouver le milieu + inverse + calcul
Légère utilisation temporaire de la pile si la récursion est choisie.
**Readability**= Déplacement clair : trouver le milieu → inverser → calculer==============================================================================================================================================================================================================================================
Autres **Cas d'escroquerie**
**Interview Tactics**= Afficher la connaissance de la technique à deux pointeurs== Demander une alternative (pistolet, tableau) – discuter des compromis== Être prêt à restaurer la liste originale si demandé==

---

C'est vrai. Pourquoi cette solution fait-elle penser aux entrevues?

1. **Shows two-pointer mastery** – un modèle d'entrevue classique.
2. **L'inversion sur place** montre une manipulation attentive des pointeurs et une conscience de la mémoire.
3. **La passe simple (après l'inverse)** montre l'efficacité algorithmique.
4. **Clean code** – facile à comprendre, testable et évolutive.

---

#### 6--Essais & Edge- Liste de contrôle des cas

Autres Test d'entrée prévu Pourquoi
C'est pas vrai.
Autres Longueur uniforme, grande : 1,2,3,4,5,6] : 1+6, 2+5, 3+4 → max 11
Une seule paire de jumeaux
Autres Toutes les mêmes valeurs 4+4 paires
Autres Valeurs élevées
Ordre aléatoire

Utilisez-les comme tests unitaires dans votre IDE ou éditeur en ligne.

---

### # 7-SEO-Takeaway optimisé

- **Titre** – Somme jumelle maximale d'une liste liée – LeetCode 2130
- **Meta Description** – Découvrez comment résoudre LeetCode 2130 (somme jumelle maximale d'une liste liée) en Java, Python et C++. Maître à deux points, inversion en place, et code d'entrevue facile!
- **Mots clés** – LeetCode 2130, Maximum Twin Sum, Problème de liste liée, deux-pointer, liste liée inverse, question d'entrevue, solution Java, solution Python, solution C++.
- **En-têtes** – Utiliser `H1` pour le titre, `H2` pour les sections, `H3` pour les sous-thèmes.
- **Liens internes** – Lien vers d'autres problèmes de LeetCode (p. ex., Liste de liens inversés, Deux Sum) pour améliorer la rampabilité.
- **Call‐to‐Action** – Télécharger le code, pratiquer et partager vos propres solutions sur GitHub pour mettre en valeur vos cliquets de codage !

---

- Oui. Réflexions finales

- ** Gardez le code rangé** – des fonctions d'aide séparées si nécessaire.
- **Expliquez votre approche** – parlez des compromis temps/espace.
- **Afficher la prise de conscience des écueils** – par exemple, ne pas gérer la longueur bizarre (même si le problème le garantit).
- **Soyez prêt à modifier** – si vous voulez conserver la liste, vous pouvez inverser la seconde moitié avant de revenir.

Bonne chance pour votre prochain entretien ! C'est ce qu'il a dit.

Bon codage !