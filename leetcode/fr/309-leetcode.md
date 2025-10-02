---
titre: LeetCode 309. Meilleur moment pour acheter et vendre des stocks avec Cooldown -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 309. Meilleur moment pour acheter et vendre des stocks avec Cooldown
**Difficulté:** Moyenne
**Tag:** DP, Machine d'État, Greedy, O(1) Espace

---

### TL;DR
* Utilisez un DP** d'état qui ne conserve que trois variables : `hold`, `sold` et `reste`.
* Transition dans *O(1)* par jour → **O(n)** heure, **O(1)** espace.
* La récurrence principale:

État Signification Transition
- C'est quoi ?
"Hold" , tenant un stock aujourd'hui "Hold = max (Hold, repos - prix)" Autres
"vendu"" Vendu un stock aujourd'hui" "vendu = max(vendu, tenir + prix)" Autres
"Rest" Dans le refroidissement ou ne rien faire "rest = max(rest, vendu)" Autres

---

- Oui. 1. Le Code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

---

#### 1.1 Java

"Java
solution de classe publique {
Int maxProfit(int[] prix) {
Int hold = Integer.MIN_VALUE; // bénéfice maximal lors de la détention d'un stock
Int vendu = 0; // profit maximum lors de la dernière action
repos int = 0; // bénéfice maximal en cas de refroidissement / ralenti

pour (prix int : prix) {
int prevHold = tenir;
int prevSold = vendu;

hold = Math.max(prevHold, repos - prix); // acheter aujourd'hui ou conserver
vendu = Math.max(prevSold, prevHold + prix); // vendre aujourd'hui ou garder vendu
repos = Math.max(rest, prevSold); // refroidissement ou rester au ralenti
}
retour vendu; // la dernière action doit être une vente pour réaliser le bénéfice
}
}
«» "

---

#### 1.2 Python

'`python
Solution de classe:
def maxProfit(self, prix: Liste[int]) -> Int:
cale = flotteur('-inf') # tenant un stock
vendu = 0 # juste vendu
repos = 0 # refroidissement / ralenti

pour les prix:
prev_hold, prev_sold = hold, vendu
hold = max(prev_hold, repos - prix) # acheter ou conserver
vente = max(prev_vendu, prev_hold + prix) # vente ou maintien vendu
repos = max(rest, prev_vendu) # refroidissement ou ralenti

retour vendu
«» "

---

*## 1.3 C++

'`cpp
solution de classe {
public:
int maxProfit(vecteur<int>& prix) {
hold = INT_MIN; // holding d'un stock
Int vendu = 0; // juste vendu
repos int = 0; // refroidissement / ralenti

pour (prix int : prix) {
int prevHold = cale, prevSold = vendue;
hold = max(prevHold, repos - prix); // acheter ou conserver la tenue
vendu = max(prevSold, prevHold + prix); // vendre ou conserver vendu
repos = max (rest, prevSold);/
}
retour vendu; // meilleur bénéfice se termine par une vente
}
};
«» "

Les trois implémentations fonctionnent dans **O(n)** temps et n'utilisent que **O(1)** mémoire supplémentaire – parfait pour l'entrevue et la production.

---

- Oui. 2. L'article du blog

> **Titre:*************************************************************************************************************************************************************************************************************************************************************
> **Meta Description:**
> Apprenez à fissurer LeetCode 309 en quelques minutes. Plongez dans la solution de la machine d'État du PDD, les pièges, et pourquoi l'espace O(1) importe pour les entrevues.

---

2.1 Introduction

Si vous avez frappé LeetCode 309 ☆Meilleur moment pour acheter et vendre des stocks avec Cooldown, félicitations!
C'est un problème de DP classique qui apparaît dans les pipelines d'interview du monde réel : ** transactions multiples avec un cooldown d'une journée**.

Cet article décompose la solution en trois parties : le *good* (l'idée de DP propre), le *bad* (les erreurs courantes et pourquoi elles échouent), et le *ugly* (tricks pour rendre le code encore plus court sans perdre la lisibilité).
Nous saupoudrons également certains mots-clés **SEO** – *LeetCode, DP, bourse, questions d'entrevue, recherche d'emploi* – de sorte que le poste se classe bien pour les recruteurs à la recherche de candidats qui peuvent résoudre des problèmes complexes de programmation dynamique.

---

#### 2.2 Le bon – PDD de la machine d'État dans l'espace O(1)

2.2.1 Intuition

Pensez à chaque jour comme une machine **** qui peut être dans l'un des trois états:

1. **Hold** – vous possédez un stock.
2. **Vendu** – vous venez de vendre le stock.
3. **Rest** – vous êtes soit dans le cooldown (le lendemain d'une vente) ou ne faites rien.

Nous n'avons pas besoin de nous rappeler *exactement* quand le dernier achat s'est produit; nous avons seulement besoin du meilleur profit possible pour chaque État jusqu'à aujourd'hui.

2.2.2 Répétition

Formule de transition Autres
C'est quoi ?
`hold` → `hold`= Continuer à tenir: `hold` reste le même. Autres
`hold` → `sold`= Vendez aujourd`hui: `sold = hold + price`. Autres
`rest` → `hold`= Acheter aujourd`hui: `hold = repos - prix`. Autres
"vendu" → "rest" Refroidissement: "rest = vendu". Autres
"rest" → "rest" Ne rien faire: "rest" reste le même. Autres

Combiner l'option « ne rien faire » nous donne le **max** dans chaque mission :

Texte
hold = max (hold, repos - prix)
vendu = max (vendu, en attente + prix)
repos = max (rest, vendu)
«» "

Parce que chaque variable ne dépend que de sa valeur précédente (ou de la valeur précédente *rest*), nous pouvons itérer à travers le tableau une fois et garder seulement trois variables entières – **constante espace supplémentaire**.

---

#### 2.2.2 Mise en œuvre du code-Ready

Nous avons déjà montré Java, Python et C++ ci-dessus.
Un motif clé : **mise à jour en utilisant les valeurs précédentes** (`prevHold`, `prevSold`) pour éviter l'écrasement avant le calcul de l'état suivant.

---

2.3 Les mauvaises – Pièges qui vous emportent

1. ** Stockage de l'ensemble du tableau DP (mémoire « O(n) »)** –
*De nombreux candidats commencent par un tableau classique `dp[i]`. Il fonctionne mais gaspille la mémoire et est souvent signalé par les intervieweurs comme --inefficient. *

2. **Wrong valeurs initiales** –
Le fait de définir `hold = 0` (au lieu de `-----) permet incorrectement d'acheter le jour 0 sans vente, ce qui conduit à compter les bénéfices négatifs comme valables.

3. **Oubliant le refroidissement** –
Certaines solutions essaient de sauter l'état `rest` et juste définir `hold = max(hold, prix[i-2] - prix)`.
Cela oublie qu'après avoir vendu vous devez **idle** pendant un jour, donc la transition doit impliquer l'état *vendu* explicitement.

4. **Utilisation d'une boucle double-nœud** –
Une solution naïve `O(n^2)` qui scanne tous les jours d'achat précédents pour chaque jour de vente passe les tests, mais obtient marqué "TLE" sur les grandes entrées LeetCode.

**Fixes:**
* Initialisez toujours `Hold` avec `-..` (ou `INT_MIN`) pour indiquer ..
* Gardez la variable `rest`, même si vous ne faites jamais rien de rien au jour 0 – il garde la récurrence propre.
* Éviter une boucle imbriquée; utiliser le roulage `maxDiff` trick décrit dans la section *ugly*.

---

2.4 L'Ugly – raccourcir le code (tout en restant lisible)

Techniques d'aide Exemple
- C'est quoi ?
**Mise à jour Térnaire**= Combiner les appels `max` en une seule ligne="Hold = Math.max(Hold, repos - prix);`="
**Pré-calculer `rest`**="rest` est toujours le meilleur de lui-même et `vendu` → pas de var.= `rest= Math.max(rest, vendu);` Autres
**Constantes de l'inline** , via `Integer.MIN_VALUE` ou `float('-inf') `int hold = entier.MIN_VALUE;`=

> **Conseil pour Java:**
> Utiliser `Math.max` est préférable à `:` parce que c'est *type-safe* et auto-documentation.

---

2.5 Mettre tout en place – Une liste de contrôle finale

Autres Vérification Pourquoi
C'est quoi ?
**Heure** – «O(n)» La limite de temps de LeetCode est généralement de 1 à 2 secondes. Autres
**Espace** – « O(1) » Les recruteurs aiment les candidats qui peuvent écrire un code efficace en mémoire. Autres
**Readability** – Conserver les noms de variables descriptifs (`hold`, `vendu`, `reste`). Éviter les refus de révision de code. Autres
Autres **Edge Cases** – tableau vide → retour `0`. Autres
**Tests** – Écrire des tests unitaires pour: 1 jour tableau, baisse des prix, hausse des prix, mélanges aléatoires. Montre que vous ne pouvez pas juste . . . . . . . . . la solution. Autres

---

#### 2.6 Clôture – Comment cela aide votre chasse à l'emploi

* **Showcase in Resume** – Ajouter une balle : -LeetCode 309 en O(n) temps et espace O(1) à l'aide de la machine d'état DP. (en milliers de dollars)
* **En ligne** – Partagez la solution courte et les recruteurs d'étiquettes.
* **Interview Prep** – Pratiquez ce modèle sur d'autres problèmes de stock de LeetCode (p. ex. 123, 188) – le cadre PDD *state-machine* est réutilisable.

En maîtrisant LeetCode 309, vous démontrez :

1. **Comprendre les fondamentaux du PDD** – essentiel pour les rôles dans l'ingénierie des algorithmes, la fintech et les équipes de produits axées sur les données.
2. **Space‐time tradeoff sensibilisation** – les recruteurs apprécient les candidats qui peuvent produire un code propre et efficace.
3. **L'état d'esprit de résolution des problèmes** – vous pouvez aborder des scénarios du monde réel comme la planification des échanges ou l'allocation des ressources.

---

#### 2.7 SEO— Mots clés et étiquettes

Mots-clés primaires Mots-clés secondaires Autres
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
LeetCode 309 Autres
Meilleur moment pour acheter et vendre des stocks
Questions de l'interview de DP boursière
Recherche d'emploi
O(1) espace

---

### 2.8 Appel à l'action

> ** Prêt à décrocher votre prochain rôle? **
> Ajoutez cette solution à votre portfolio, postez le code sur GitHub et partagez vos propres variations dans les commentaires.
> Recrutements liés Dans l'amour de voir le code DP propre jumelé avec des explications réfléchies – assurez-vous que vos messages sont indexés avec les bons mots-clés.

---

FAQ

1. ** Pouvons-nous ignorer le refroidissement? * *
Enlever le cooldown transforme le problème en LeetCode 122 (le meilleur moment pour acheter et vendre une fois). La machine d'état fonctionne encore; il suffit de définir `rest = hold` au lieu de `max(rest, vendu)`.

2. **Et si nous voulons limiter le nombre de transactions? * *
Ajouter une autre dimension à l'état: `k` (transactions à gauche). La récurrence reste la même, mais vous aurez besoin d'un tableau de taille `k`.

3. **Pourquoi ne pas utiliser une solution avide? **
Greedy fonctionne pour la version simple de cooldown, mais échoue quand un cooldown vous force à sauter un jour. DP est le seul moyen de saisir cette dépendance.

---

2.10 Réflexions finales

*Les bonnes:* Un O(1) DP concis qui modélise élégamment les états de "Hold/sold/sold".
*Les méchants:* Boucles imbriquées, valeurs initiales incorrectes, oubliant le cooldown.
*Les voyous :* Un liner un peu moins lisible qui sacrifie la clarté pour la brièveté.

Avec cette connaissance, vous êtes non seulement prêt à ace LeetCode 309, mais vous êtes également démontrant le genre de maturité algorithmique que les employeurs recherchent chez les ingénieurs logiciels et les data scientists.

Bonne chance, et que votre pile d'interview déborde avec -Oui, je l'ai résolu !

---

2.11 Références

1. LeetCode 309 – Meilleur moment pour acheter et vendre des stocks avec Cooldown
2. * Programmation dynamique – Machine d'État* – https://www.geeksforgeeks.org/dynamic-programming-state-machine/
3. *Prép. d'entrevue: LeetCode 309* – https://leetcode.com/problèmes/best-time-to-buy-and-sell-stock-with-refroidissement/

---

> **© 2024 Votre nom – Tous droits réservés. **

---

2.12 Liste de contrôle rapide pour les intervieweurs

* [ ] Le candidat explique-t-il clairement les 3 énoncés?
* [ ] Sont-ils en mesure de tirer la récurrence de l'énoncé du problème?
* [ ] Écrivent-ils le code avec un espace "O(1)" et peuvent-ils justifier le choix?
* [ ] Peut-on identifier des pièges communs (comme oublier le refroidissement) ?

Si vous répondez **oui** à tout ce qui précède, vous êtes prêt à impressionner tout gestionnaire d'embauche. Bon codage !