---
titre: LeetCode 2807. Insérer les plus grands diviseurs communs dans la liste liée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2807. Insérer les plus grands diviseurs communs dans la liste liée
> *LeetCode Medium= Heure O(n)= Espace O(1)*

> **TL;DR** – Traversez la liste une fois, calculez le GCD de chaque paire adjacente avec l'algorithme euclidien, et épiez un nouveau nœud entre eux.

Ci-dessous vous trouverez une solution complète et prête à la production dans **Java, Python et C++** plus un article de blog **SEO-friendly** qui décompose le problème, ses pièges, et interview-friendly à emporter.

---

Récapitulation des problèmes

On vous donne la tête d'une liste en lien unique où chaque noeud contient une valeur entière.
Entre chaque paire de nœuds consécutifs, vous devez insérer un nouveau nœud dont la valeur est égale au **plus grand diviseur commun (GCD)** des deux nœuds.

«» "
Entrée : 18 → 6 → 10 → 3
Sortie: 18 → 6 → 6 → 2 → 10 → 1 → 3
«» "

*Si la liste n'a qu'un seul noeud, retournez-le inchangé. *

Contraintes
- `1 ≤ nombre de nœuds ≤ 5000`
- `1 ≤ nœud.val ≤ 1000`

---

Stratégie de haut niveau

Étape Que faire ? Pourquoi ça marche ?
C'est pas vrai.
**Vérification de cas** – si `head.next == null`, il suffit de retourner `head`. Aucune paire → aucune insertion. Autres
**Itérer** avec deux pointeurs `prev` (current) et `curr` (next). Permet une insertion à temps constant. Autres
Calculer GCD** de `prev.val` et `curr.val` à l'aide de l'algorithme d'Euclide. Autres
**Créer un nouveau nœud** `gcdNode` et l'épingler entre `prev` et `curr`. Autres
**Pointeurs avancés**: `prev = curr; curr = curr.next;`= Déplacer vers la paire suivante. Autres
La liste modifiée est maintenant prête. Autres

---

Analyse de complexité

Formule métrique Résultat
C'est quoi, ça ?
**Heure** traversée + "O(1)" par GCD **O(n)** Autres
**Space**. Seulement une poignée de variables. **O(1)** (à part les nouveaux nœuds qui font partie de la sortie)

---

## Coques & Gotchas

Pourquoi ça compte ?
- Oui.
Autres Nœud simple : aucune paire adjacente : retour précoce (`head.next == null`) Autres
Autres Toutes les valeurs égales du GCD sont égales au même nombre.
Valeurs négatives (non autorisées par les contraintes) si nécessaire
Grandes chaînes (jusqu'à 5000 nœuds)

---

##  uvres d'entretien

1. **Euclid** – Les intervieweurs adorent voir la fondation mathématique.
2. **Manipulation du pointeur de fusion** – Affiche que vous pouvez modifier en toute sécurité une liste liée en O(1) par opération.
3. **Discussion du temps/de l'espace** – Toujours aborder l'analyse de complexité.
4. **Parler de cas de bord** – Démontre le codage défensif.

---

Code complet

Voici des solutions propres et autonomes en Java, Python et C++.
Les trois utilisent une fonction transverse **itative** à deux points et une fonction d'aide pour calculer le GCD.

---

### Java

"Java
// 2807. Insérer les plus grands diviseurs communs dans la liste liée – Java

classe ListNode {
la valeur intérieure;
ListNode suivant;
ListNode() {}
ListNode(int val) { this.val = val; }
ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

solution de classe {
Liste publiqueInsert de nœudGrandeCommonDiviseurs(tête de noeud de liste) {
si (head) null (head) null (head) null (head) null (head).

ListNode prev = tête;
ListNode curr = head.next;

pendant que (curr != null) {
int gcdVal = gcd(prev.val, curr.val);
Numéro de liste gcdNode = nouveau numéro de liste(gcdVal);

// Tranche gcd Noeud entre prev et curr
prev.next = gcd Numéro;
gcdNode.next = curr;

// avancer
prev = curr;
curr = curr.next;
}
tête de retour;
}

// Algorithme euclidien – O(log min(a,b))
Int privé gcd(int a, int b) {
pendant que (b != 0) {
tmp = b;
b = a % b;
a = tmp;
}
retour a;
}
}
«» "

---

Python

'`python
# 2807. Insérez les plus grands diviseurs communs dans la liste liée – Python

Numéro de la classe:
def __init_(self, val=0, next=None):
autoval = val
self.next = suivant

Solution de classe:
def insertGreatestCommonDivisors(self, head: ListNode) -> Numéro de liste:
si pas de tête ou pas de tête. Suivant :
tête de retour

prev = tête
curr = tête.next

alors que:
gcd_val = auto._gcd(prev.val, curr.val)
gcd_node = Numéro de liste(gcd_val)

# Tranche
prev.next = gcd_node
gcd_node.next = curr

# avance
prev = curr
curr = curr.next

tête de retour

def _gcd(self, a: int, b: int) -> Int:
tandis que b:
a, b = b, a % b
retour a
«» "

---

C++

'`cpp
// 2807. Insérez les plus grands diviseurs communs dans la liste liée – C++

#incluez <cstddef>

struct Node de la liste {
la valeur intérieure;
Numéro de liste *suivant;
ListNode() : val(0), next(nullptr) {}
ListNode(int x) : val(x), next(nullptr) {}
ListNode(int x, ListNode *n) : val(x), next(n) {}
};

solution de classe {
public:
ListNode* insertGreat CommonDivisors(ListNode* head) {
si la tête de retour (!head->next)

Numéro de liste *prev = tête;
Numéro de liste *curr = tête->suivante;

pendant que (curr) {
int gcdVal = gcd(prev->val, curr->val);
Numéro de liste *gcdNode = nouveau numéro de liste(gcdVal);

// Tranche
prev->next = gcd Numéro;
gcdNode->next = curr;

// avance
prev = curr;
curr = curr->next;
}
tête de retour;
}

particulier:
// Algorithme euclidien
int gcd(int a, int b) {
pendant que b) {
tmp = b;
b = a % b;
a = tmp;
}
retour a;
}
};
«» "

---

Article de blog optimisé par le SEO

> **Titre:** *LeetCode 2807 – Insérez les plus grands diviseurs communs dans la liste liée: Java / Python / C++ Solutions pour les entrevues*
> **Lug:** leetcode-2807-insert-gcd-in-linked-list
> **Meta Description:** Apprenez la meilleure façon de résoudre LeetCode 2807. Un guide étape par étape, des extraits de code en Java, Python et C++, et des idées conviviales pour les interviews.

---

# LeetCode 2807: Insérer les plus grands diviseurs communs dans la liste liée
*Un guide complet pour les développeurs Java, Python et C++*

---

Aperçu du problème

Le problème vous demande de **insérer un nœud GCD entre chaque paire de nœuds consécutifs** dans une liste liée.
Si la liste n'a qu'un seul noeud, rien ne devrait changer.

---

Les contraintes méritent d'être notées

- 1 ≤ #noeud ≤ 5 000
- 1 ≤ nœud.val ≤ 1 000

Ces limites rendent l'algorithme du GCD euclide pratiquement à temps constant, et une solution itérative garantit l'espace auxiliaire O(1).

---

La feuille de chaleur complexe

Opération Complexité
C'est quoi ?
*(n)**
GCD (Euclid) **O(log min(a,b))** – constante efficace pour ≤ 1 000
Total
Espace supplémentaire

---

Approche étape par étape

1. **Retour rapide** pour les listes vides ou uniques.
2. **Two-pointer itération** (`prev` et `curr`) pour connaître toujours la paire actuelle.
3. **Computer GCD** en utilisant l'algorithme Euclid.
4. **Splice** un nouveau `ListNode` entre `prev` et `curr`.
5. **En avant** vers la prochaine paire et répéter.

Cette stratégie permet de ne toucher chaque nœud qu'un nombre constant de fois et d'éviter le débordement de la pile.

---

Pièges communs

Pourquoi ça arrive
- Oui.
Utilisation de la récursion → débordement de la pile sur de longues listes
Aucune paire adjacente. Autres
Utiliser une mise en œuvre naïve de GCD (division par 0) 0 ' boucle
Défaut d'utiliser les pointeurs `next` après l'épissage.

---

Entretien Débat amical

> * Expliquer Euclid.
> L'intervieweur vérifiera si vous comprenez pourquoi `gcd(a,b)` est trouvé via `a % b`.

> Pourquoi avez-vous utilisé deux pointeurs ? *
> Il montre que vous pouvez modifier une liste liée en place avec O(1) par insertion.

> Quelle est la complexité ? *
> Soulignez que la solution est linéaire dans le nombre de nœuds, et utilise une mémoire supplémentaire constante.

> Des cas de bord? *
> Mentionnez un seul noeud, toutes les valeurs égales et les entrées négatives potentielles.

---

Détails de mise en œuvre par langue

### Java
- Utilise `class ListNode` tel que défini par LeetCode.
- GCD mis en œuvre avec une méthode d'aide "gcd(int a, int b)".
- Une boucle itérative pour éviter les problèmes de profondeur de récursion.

Python
- "ListNode" miroirs de constructeur LeetCode.
- GCD via `_gcd` helper en utilisant le déballage de tuple.
- Des commentaires précis.

C++
- "ListNode" est une structure simple.
- Utilise la manipulation du pointeur (`prev->next = gcdNode; gcdNode->next = curr`).
- La fonction `gcd` utilise la même boucle euclidienne.

---

Conseils pour la maîtrise

1. **Écrire une fonction GCD d'aide d'abord** – elle maintient la boucle principale propre.
2. **Test avec de petites listes** (1, 2, 3 nœuds) pour vérifier la logique du pointeur.
3. **Utilisation de la mémoire du fichier** – LeetCode limite la taille de sortie totale, mais notre algorithme ne stocke jamais plus que la taille d'entrée et les nouveaux nœuds.
4. **Pratique expliquant l'algorithme** – Les intervieweurs veulent que vous articuliez la logique, pas seulement livrer le code.

---

Résumé (bon, mauvais, mauvais)

Catégorie Ce que nous avons fait
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bon**Scan linéaire, espace constant, Euclid simple. Autres
**Les solutions récursives sont faciles à écrire mais soufflent la pile pour 5 000 nœuds. Remplacer la récursion par l'itération. Autres
**Ugly**. Sur-ingénierie en précomputant tous les GCD dans un tableau puis en réorganisant la liste. Éviter; épancher en place. Autres

---

À emporter

*LeetCode 2807* est un problème** qui teste votre compréhension de la manipulation de liste liée et de la théorie des nombres de base.
Avec les extraits de code ci-dessus, vous pouvez aborder ce problème avec confiance en **Java, Python ou C++**, discuter de l'approche dans un entretien d'embauche et présenter une solution propre et prête à la production.

Bon codage – et bonne chance pour la prochaine interview! C'est ce qu'il a dit.

---

**SEO Mots-clés**: *LeetCode 2807, Insérez les plus grands diviseurs communs dans la liste liée, Liste liée GCD, solution Java, solution Python, solution C++, défi de codage d'entrevue, interview technique, prép. *