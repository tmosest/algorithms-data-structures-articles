---
titre: LeetCode 1474. Supprimer les nœuds N après les nœuds M d'une liste liée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**LeetCode 1474 – Supprimer les nœuds N après les nœuds M d'une liste liée* *
> *Une solution O(n) propre et en place dans **Java**, **Python** et **C++** + un billet de blog prêt à être interviewé. *

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi cela importe] (# pourquoi-il-matières)
3. [Idées naïves (les mauvaises et moches)] (#idées naïves)
4. [La solution optimale (la bonne)] (#solution optimale)
5. [Code Walk‐through](#code-through)
[Java] (#Java)
* [Python] (#python)
* [C++](#c-plus-plus)
6. [Analyse de la complexité] (#complexité)
7. [Régime des cas et pièges communs] (#cas de référence)
8. [Suivi : place en place contre espace supplémentaire] (#suivi)
9. [Conseils d'entrevue et astuces](#interview-tips)
10. [SEO Liste de contrôle et mots clés](#seo-checklist)
11. [Conclusion et pensées finales] (#conclusion)

---

## <a name="problem-overview"></a>1=" Aperçu du problème

> **Supprimer les nœuds N après les nœuds M d'une liste liée* *
> **Code de gauche #1474** – *Facile*

On vous donne une liste **singly-linked** et deux entiers `m` et `n`.
À partir de la tête, garder les premiers nœuds `m`, supprimer les nœuds `n` suivants, puis répéter jusqu'à la fin de la liste.
Retournez le chef de la liste modifiée.

**Exemple**
«» "
Entrée: tête = [1,2,3,3,4,5,6,7,8,9,10,11,12,13], m = 2, n = 3
Produit : [1,2,6,7,11,12]
«» "

**Contrôles* *
- `1 <= noeuds <= 10^4`
- `1 <= valeur <= 10^6`
- `1 <= m, n <= 1000`

---

Pourquoi ça compte ?

- **Liste liée Mastery** – La plupart des interviews techniques vous demandent de manipuler les pointeurs directement.
- **Espace-Optimal** – Le problème demande explicitement une solution **en place** (O(1) espace supplémentaire).
- **Efficacité du temps** – Un seul passage dans la liste (temps O(n)) est la solution idéale.

La maîtrise de ce problème démontre que vous comprenez :
- Pointeur traversant
- Manipulation des caisses
- Structure de code propre (tête de dummy, boucles vs récursion)

---

## <a name="naïve-ideas"></a>3="Naïve-ideas (Les mauvaises et lugubres)

Idées Pourquoi c'est mauvais
- C'est quoi ?
**Recursion**= Chaque appel utilise l'espace de la pile → O(n) space="deleteNodes(head)` se fait appeler à l'intérieur de la boucle de suppression, faisant sauter la pile sur de grandes listes.
**Deux-pass**= Premier passage au compte, deuxième passage à supprimer → encore O(n) mais gaspillé== Boucle supplémentaire, complexité inutile==
**Convertissez en tableau → O(n) mémoire supplémentaire.

> **À emporter** – Gardez-le linéaire, pointeur seulement et simple passage.

---

La solution optimale (le bien)

1. **Utilisez une tête de mannequin** – simplifie les cas de bord lorsque la tête elle-même est enlevée.
2. ** Maintenir deux pointeurs** :
- `prev` – le dernier nœud qui reste après un cycle de suppression.
- 'curr' – le noeud que nous inspectons actuellement.
3. **Loop**
- Prévoir les étapes `prev` et `curr` `m` (conserver les nœuds).
- Avancer les marches `curr` `n` (supprimer les nœuds).
- Lien `prev->next = curr`.
4. **Arrêter** lorsque le «curr» devient «NULL».

Toutes les étapes sont **O(1) par noeud**, donc le temps global est **O(n)** et espace **O(1)**.

---

## <a name="code-walkthrough"></a>5="Code Walk‐through

Voici des implémentations propres et prêtes à la production dans les trois principales langues d'entrevue.

### <a name="java"></a>Java

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
public ListNode deleteNodes(ListNode head, int m, int n) {
// Noeud pour gérer les suppressions à la tête
mannequin ListNode = nouveau ListNode(0);
mannequin.next = tête;

ListNode prev = mannequin; // dernier noeud qui reste
ListNode curr = tête; // noeud courant dans la liste

pendant que (curr != null) {
// / / / / Conserver les nœuds m
pour (int i = 0; i < m && curr != null; i++) {
prev = curr;
curr = curr.next;
}

// 2
pour (int i = 0; i < n && curr != null; i++) {
curr = curr.next;
}

// Connectez la partie conservée à la partie conservée suivante
prev.next = curr;
}

retour mannequin.suivant;
}
}
«» "

### <un nom="python"></a> Python

'`python
Numéro de la classe:
def __init_(self, val=0, next=None):
autoval = val
self.next = suivant

def deleteNodes(head: ListNode, m: int, n: int) -> Numéro de liste:
mannequin = Noeud de liste(0, tête) # Noeud de mannequin
prév, curr = mannequin, tête

alors que:
Gardez les nœuds
pour _ dans l'intervalle(m):
si le curr n'est pas:
pause
prev, curr = curr, curr.next

# Supprimer n nœuds
pour _ dans la plage(n):
si le curr n'est pas:
pause
curr = curr.next

# Lien
prev.next = curr

retour mannequin.suivant
«» "

### <a name="c-plus-plus"></a>C++

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
ListNode* supprimerNodes(ListNode* tête, int m, int n) {
Le numéro de liste du mannequin(0);
mannequin.next = tête;
Numéro de liste *prev = &dummy, *curr = tête;

pendant que (curr) {
// Garder les nœuds m
pour (int i = 0; i < m && curr; ++i) {
prev = curr;
curr = curr->next;
}

// Supprimer n nœuds
pour (int i = 0; i < n && curr; ++i) {
curr = curr->next;
}

// Connexion
prev->next = curr;
}

retour mannequin.suivant;
}
};
«» "

---

## <un nom="complexité"></a>6="Analyse de la complexité

Métrique Java / Python / C++
- C'est quoi ?
**Temps** **O(n)**= Chaque noeud est visité un nombre constant de fois (au plus `m + n` mais `m + n ≤ 2000`). Autres
*Space**** **O(1)**. Seulement quelques pointeurs + tête factice; pas de tableaux auxiliaires ou de piles de récursion. Autres

Autres La solution optimale répond parfaitement à l'exigence « en place ».

---

## <a name="edge-cases"></a>7="Edge Cases & Pièges communs

Cas de ce qui se passe
- C'est quoi ?
Oui. La boucle `pour` interne saute simplement, le code fonctionne encore.
**m == 0** (invalide par des contraintes) , perdrait la liste entière , "pour (int i=0; i<m; ++i)" ne fait rien → `prev` reste mannequin, conduisant à la liste vide
**Liste plus courte que m**.
**Liste plus courte que n après avoir gardé**.
**La délétion touche la tête**

> **Astuce** – Toujours tester avec `m = 1`, `n = 1`, `m = n = 0` (si le juge relâche jamais les contraintes).

---

## <a name="follow-up"></a>8=" Follow-Up: In‐Place vs. Extra Space

**Question:** *Pouvons-nous résoudre cela avec **O(n)** mémoire supplémentaire (par exemple, en construisant un tableau ou en copiant des nœuds)? *
**Réponse:** Absolument – il suffit de convertir un tableau ou d'utiliser un helper récursif, mais vous perdez le bord de la place de la question explicitement souhaitée.
**Pourquoi rester en place? * *
- Les entrevues testent souvent si vous pouvez *réutiliser* la structure existante sans attribuer de nouveaux nœuds.
- Oui. Dans le code du monde réel, vous voulez éviter une copie de mémoire pour la performance et la prévisibilité.

---

## <a name="interview-tips"></a>9=" Conseils et astuces d'entrevue

Question : Votre point de conversation
-- -- -- -- -- -- -- -- -- -- -- -- --
Autres Que faire si `n` est 0? Afficher que le bloc `pour (int i = 0; i < n; ++i)` exécute zéro fois. Autres
Autres Pouvez-vous le faire récursivement? Pour une liste de 10 000 nœuds, c'est un débordement de pile. D'abord offrir la solution itérative, puis discuter de la récursion seulement comme une alternative théorique. Autres
Pourquoi la tête du mannequin? Il est toujours valable de mentionner qu'il garantit également `prev->next`. Autres
C'est le temps linéaire, l'espace constant. Baladez les deux boucles imbriquées : chaque noeud est traité un nombre constant de fois. Autres

**Méthode STAR** – *Situation, tâche, action, résultat*
- **Situation**: On m'a demandé de supprimer tous les nœuds `n` après avoir gardé les nœuds `m`. (en milliers de dollars)
- **Tâche** : Déplacez la liste une fois et modifiez-la en place. (en milliers de dollars)
- **Action**: -Utilisé un noeud factice, deux pointeurs et deux boucles simples. (en milliers de dollars)
- **Résultat**: temps O(n), espace O(1), aucune allocation supplémentaire. (en milliers de dollars)

---

## <un nom="seo-checklist"></a> Liste de contrôle du référencement et mots clés

Catégorie Mot-clé Pourquoi ça compte
- C'est quoi ?
**Problem Title**=LeetCode 1474 Supprimer N Nodes After M Nodes=== Les chercheurs tapent souvent le numéro de problème exact. Autres
**Interview Focus** Ce sont les expressions type recruteurs. Autres
**Langues**= Solution de Java, solution de Python, solution de C++ permet à chaque langue d'apparaître dans des résultats de recherche séparés. Autres
**Complexité**=O(n) solution de liste liée au temps=, espace constant==Les recruteurs recherchent un code efficace. Autres
*Extras****Solutions Java Python C++, interview d'algorithme. Autres

> **Méta-Tags de style Google* *
> ```html
> <title>LeetCode 1474 – Supprimer les nœuds N après les nœuds M (Java, Python, C++)</titre>
> <meta name="description" content="Clean, in-place O(n) solution to LeetCode 1474 – Supprimer les nœuds N après les nœuds M d'une liste liée. Java, Python et C++ code + guide d'entrevue.">
> `` "

---

## <a name="conclusion"></a>10=" Conclusion et pensées finales

**Ce que vous avez appris**
-- -- -- -- -- -- -- --
Maîtriser la manipulation des pointeurs dans une liste en lien unique. Autres
Un algorithme **in-place** (espace O(1)). Autres
Atteint une complexité temporelle unique O(n). Autres
La solution a été clairement communiquée dans **Java**, **Python** et **C++** – les recruteurs de trois langues adorent. Autres
Évité les récursions et les pièges à deux passages – les approches de «bad». Autres

> **Astuce finale** – Durant l'entrevue, *parler d'abord de l'idée de tête de mannequin*. La plupart des intervieweurs aiment vous voir penser à des cas de bord avant d'écrire du code.

Bon codage et bonne chance écraser votre prochaine interview! C'est ce qu'il a dit.

---

Code de référence rapide (toutes langues)

Texte
Java :
mannequin → prev → curr
pour les étapes m: prev = curr; curr = curr.next;
pour n pas: curr = curr.next;
prev.next = curr;

Python / C++ (même logique)

«» "

N'hésitez pas à copier, coller et exécuter ces extraits sur vos propres harnais de test ou juges en ligne. Joyeux hack !