---
titre: LeetCode 464. Je peux gagner...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 464 – Puis-je gagner
**Problème**
- Oui.
[LeetCode 464 – Puis-je gagner](https://leetcode.com/problèmes/can-i-win/) Medium, "Programme dynamique", "Bitmask", "Théorie du jeu", "Retour "

---

Récapitulation des problèmes

Deux joueurs prennent à tour de rôle la sélection d'un nombre de `1 ... maxChosableIntéger`.
Nombres **ne peuvent pas être réutilisés** – une fois qu'un nombre est choisi il est parti.
Ils ajoutent le nombre choisi à un total courant.
Le joueur qui fait le premier le total **≥ désiréTotal** gagne.

Retour `true` si le premier joueur peut forcer une victoire, sinon `faux`.
Les deux joueurs jouent de façon optimale.

**Contrôles* *

«» "
1 ≤ maxChoosableEntier ≤ 20
0 ≤ désiréTotal ≤ 300
«» "

Parce que `maxChosableIntéger ≤ 20` nous pouvons encoder l'état du nombre de numéros encore disponibles avec un masque 20-bit – parfait pour une solution de mémorisation DP.

---

Une idée de haut niveau

1. ** Sortie précoce**
* Si `désiréTotal <= 0` → premier joueur gagne immédiatement.
* Si la somme de tous les nombres < `désiréTotal` → impossible d'atteindre la cible → retourner `false`.

2. **Retraçage récursif + mémorisation**
* Représenter l'ensemble des numéros disponibles avec un "mask" bitmask.
* Pour chaque nombre `i` qui est toujours libre (bit `i` est 0):
* Si vous choisissez `i` gagne immédiatement (`i >= restantTotal`), retournez `true`.
* Sinon, simulez le choix `i`, soustrayez-le du total restant, et **récursivement** demandez si le joueur *next* peut gagner avec le nouveau masque.
* Si le joueur suivant ** ne peut pas** gagner, le joueur actuel peut gagner – retourner `true`.
* Si aucun choix ne mène à une victoire, mémoriser et retourner `faux`.

3. **Complexité**
* **Espace d'état**: au plus `2^maxChoosableInteger` masques (`= 1 048 576`).
Dans le pire des cas (chaque masque explore tous les nombres restants).
* **Espace**: `O(2^n)` pour la table de mémos + pile de récursion (profondeur `=20`).

---

Mise en œuvre du code

Ci-dessous sont des solutions d'auto-documentation propres dans **Java**, **Python** et **C++**.
Chacun utilise le même motif récursif + mémorisation.

---

### Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
// Carte de mémorisation : masque -> canFirstPlayerWin
carte privée<integer, Boolean> mémo = nouveau HashMap<>();

public booléen canIWin(int maxChoosableInteger, int désiréTotal) {
// Vérifications rapides de la santé mentale
si (désiréTotal <= 0) retourner vrai;
int maxSum = (maxChosableInteger * (maxChosableInteger + 1)) / 2;
si (maxSum < désiréTotal) retourner faux;

retour canWin(0, désiréTotal, maxChoosableInteger);
}

***
* @param masque Bitmask de nombres déjà choisis.
* @param restant Combien il faut encore pour atteindre le total souhaité.
* @param maxChosable L'entier maximum qui peut être choisi.
* @return true si le joueur actuel peut forcer une victoire.
*/
booléen privé canWin (masque int, restant int, int maxChoosable) {
// Recherche de mémo
si (memo.contientKey(mask)) retourne memo.get(mask);

pour (int num = 1; num <= maxChosable; num++) {
bit int = 1 << (num - 1);
si ((masque & bit) != 0) continuer; // déjà utilisé

// Si nous pouvons gagner immédiatement en choisissant ce numéro
si (num >= restant) {
mémo.put(masque, true);
retour vrai;
}

// Essayez de choisir ce numéro et laissez l'adversaire jouer
int newMask = bit de masque;
adversaire booléen Wins = canWin(newMask, reste - num, maxChoosable);

// Si l'adversaire perd, le joueur actuel gagne
si (!oppositionWins) {
mémo.put(masque, true);
retour vrai;
}
}

// Aucun mouvement gagnant trouvé
mémo.put(masque, faux);
retourner faux;
}
}
«» "

---

Python

'`python
Solution de classe:
def _init_(self):
memo = {}

def canIWin(self, maxChosableIntégeur: int, désiréTotal: int) -> C'est vrai.
# Cas de bord
si désiré Total <= 0:
retour Vrai
Si (maxChosableInteger * (maxChosableInteger + 1)) // 2 < désiréTotal:
Retour Faux

return self._dfs(0, désiréTotal, maxChoosableInteger)

def _dfs(self, masque: int, restant: int, max_num: int) -> C'est vrai.
# Recherche de mémo
Si masque en soi. mémo & #160;:
Revenez vous-même. mémo[masque]

pour num dans la gamme(1, max_num + 1):
bit = 1 << (num - 1)
si masque & bit & #160;:
continuer # déjà choisi

Gagner immédiatement
si num >= restant:
self.memo[masque] = Vrai
retour Vrai

# Laissez l'adversaire jouer
si ce n'est pas soi-même._dfs(masque), bit, reste - num, max_num):
self.memo[masque] = Vrai
retour Vrai

# Pas de mouvement gagnant
memo[masque] = Faux
Retour Faux
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
unordered_map<int, bool> mémo;

bool canIWin(int maxChoosableInteger, int désiréTotal) {
// Sorties anticipées
si (désiréTotal <= 0) retourner vrai;
int maxSum = (maxChosableInteger * (maxChosableInteger + 1)) / 2;
si (maxSum < désiréTotal) retourner faux;

retour dfs(0, désiréTotal, maxChosableIntéger);
}

particulier:
bool dfs(int masque, int restant, int maxNum) {
si (memo.count(mask)) retourne le mémo[mask];

pour (int num = 1; num <= maxNum; ++num) {
bit int = 1 << (num - 1);
si (masque & bit) continuer; // déjà utilisé

si (num >= restant) { // gagne immédiatement
mémo[masque] = vrai;
retour vrai;
}

// Tour de l'opposant
si (!dfs(masque, restant - num, maxNum)) {
mémo[masque] = vrai;
retour vrai;
}
}

mémo[masque] = faux;
retourner faux;
}
};
«» "

---

Article du blog – ─ Puis-je gagner? Maîtriser le LeetCode 464 avec DP & Bitmask

> **SEO Mots-clés**: LeetCode 464, Can I Win, programmation dynamique, bitmask, théorie du jeu, interview de codage, interview d'algorithme, Java, Python, C++.

---

C'est pas vrai. Le problème en coque

> *= Puis-je gagner* est un problème de jeu impartial classique. Deux joueurs choisissent un nombre unique à chaque tour, l'ajoutant à un total courant. Le premier à atteindre ou dépasser les gains totaux souhaités. Le défi ? Déterminer si le premier joueur peut forcer une victoire étant donné que les deux jouent de façon optimale.

C'est un parfait exemple de *théorie du jeu* combinée avec *programmation dynamique* et *bitmask* techniques – compétences que les intervieweurs aiment.

---

C'est vrai. Pourquoi ce problème Rocks (Bon)

- **Small Input Size** – `maxChosableInteger ≤ 20` nous permet d'explorer tous les états de jeu avec un masque de 20 bits.
- **Déterministe** – Pas de hasard; nous pouvons raisonner sur le chemin optimal.
- **Clear DP** – Chaque état peut-il être mémorisé : le joueur actuel gagne-t-il à partir de cet ensemble de nombres restants ? (en milliers de dollars)
- **Extensible** – Le même modèle s'applique aux autres jeux de "Take‐away" (p. ex. variantes Nim).

---

C'est vrai. Les pièges (Bad)

1. **Infini Récursion** – Sans mémoisation, vous allez souffler la pile.
2. **Explosion d'État** – Le dénombrement naïf (par exemple, lister toutes les permutations) est exponentiel et impossible pour «maxChosableIntégrer = 20».
3. **Erreurs off‐by‐one** – Les erreurs off‐by‐one dans les positions bit («1 << (num-1)») sont un bogue courant.
4. **Les affaires Edge** – Oublier le "désiré" Total <= 0` raccourci ou le sum-check conduit à des réponses erronées sur des tests triviaux.

---

C'est pas vrai. La liste de contrôle de débogage rapide

Problème Symptômes Correction
C'est pas vrai.
Autres Mauvaise clé de mémos. Autres
Trop d'appels récursifs Ajouter une sortie anticipée : si `num >= restant` retourner `true` immédiatement
Autres Mauvais changement de bit.
Débordement de la cheminée La profondeur est ≤ 20, mais la protection avec le DP itératif si nécessaire.

---

####5=1 Étape par étape (L'algorithme)

1. **Conditions de base**
* `désiréTotal <= 0` → premier joueur gagne instantanément.
* Somme de `1 ... maxChosableIntégre < désiréTotal` → impossible, retourner `false`.

2. **Aide récursive**
* Parameter `mask` encodes *utilisés* nombres.
* Bouclez sur tout `num` de `1` à `maxChosableInteger`.
* Sautez si déjà utilisé (`masque & bit`).
* **Immediate Win**: si `num >= restant` → joueur actuel gagne.
* ** Opposant : Tour** : `si !canWin(newMask, reste - num)` → nous gagnons.

3. **Mémoiser et retourner** – Conservez le résultat pour chaque masque pour éviter la recomputation.

---

Analyse de complexité

- **Heure**: `O(2^n * n)` ( pire cas), où `n = maxChosableIntéger`.
*Reason*: Il y a des masques `2^n`; pour chacun, nous pouvons essayer des numéros `n`.
- **Espace**: `O(2^n)` pour la table de mémos + `O(n)` profondeur de récursion.

Avec `n ≤ 20`, c'est confortablement rapide pour tous les tests LeetCode.

---

- Oui. Et si je veux une solution plus rapide ? (en milliers de dollars)

Pour ce problème spécifique, la solution DP + bitmask est déjà optimale dans la pratique.
Si vous rencontrez plus grand `maxChosableInteger`, vous auriez besoin d'une approche différente (par exemple, les nombres Sprague–Grundy ou l'analyse combinatoire), mais ceux-ci dépassent les contraintes de LeetCode 464.

---

### # 8.

Pourquoi ça compte ?
-- -- -- -- --
**Exposer les sorties anticipées** Autres
**La visualisation de l'état 20 bits aide les intervieweurs à voir votre processus de pensée. Autres
Autres **Parlez de la récursion par rapport à l'itération**. Autres
**Mention memorization map**= Indique votre connaissance de la mise en cache pour empêcher le travail répété. Autres
**Test avec de petits nombres**= Démontre la compétence et la compréhension de l'algorithme. Autres

---

Réflexions finales

"Can I Win" est un problème de manuel qui combine la théorie **game** avec la programmation **dynamique** et la manipulation **bit**. Mastering it non seulement vous donne une solution gagnante pour LeetCode mais également vous équipe avec un modèle que vous verrez dans de nombreux puzzles d'entrevue.

- **Bien**: Espace petit état, déterministe, propre DP.
- **Bad**: Facile à glisser sur l'indexation des bits, cas de base manquants.
- **Ugly**: TLE récursif si vous oubliez la mémorisation.

Utilisez les extraits de code ci-dessus (Java, Python, C++) comme référence prête-à-coller. Ensuite, pratique expliquant à haute voix l'algorithme – votre capacité à articuler le raisonnement est tout aussi précieuse que le code lui-même.

Bon codage, et que votre premier joueur gagne toujours! C'est ce qu'il a dit.

---

** Prêt à accepter votre prochain entretien? * *
Continuez à pratiquer, lire des solutions éditoriales, et partagez votre propre analyse -Pouvez-vous gagner sur votre blog ou GitHub. Les recruteurs adorent voir des solutions propres et explicables, surtout quand vous montrez à la fois le *pourquoi* et le *comment* derrière votre code.