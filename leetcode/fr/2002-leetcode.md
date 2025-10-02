---
titre: LeetCode 2002. Produit maximal de la longueur de deux sous-séquences palindromiques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2002 – Produit maximal de la longueur de deux sous-séquences palindromiques
**Langues**: Java-Python-C++
**Complexité temporelle**: **O(2n · n)** (= 50 k opérations pour *n* = 12)
**Complexité spatiale**: **O(2n)** pour les masques précalculés

> La longueur de chaîne n'est que jusqu'à 12, de sorte qu'une force brute **bit-masque** n'est pas seulement simple, c'est la solution la plus rapide en pratique.
> Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++** que vous pouvez coller directement dans votre éditeur ou soumettre sur LeetCode.

---

- Oui. 1. Solution Java

"Java
Importation de java.util.*;

solution de classe {
// Cache pour tous les masques palindromiques et leurs longueurs
carte privée<entier,entier> palMasks = nouveau HashMap<>();
Chaîne privée s;
Int. privé n;

Int public maxProduct(String s) {
s = s;
c.n = longueur();
Int pleine Masque = (1 << n) - 1;
int best = 0;

// Énumérer chaque masque sous-ensemble
pour (int mask = 0; masque <= fullMask; mask++) {
si [isPalindromeMask(masque)] {
int len1 = popcount(masque);
// paire avec masque disjoint
pour (int other = masque - 1; autres >= 0; autres {
si ((masque et autre) == 0 && palMasks.contientKey(autres) {
int len2 = palMasks.get(autre);
best = Math.max(best, len1 * len2);
}
}
}
}
le meilleur retour;
}

/* Construisez la chaîne de subséquences de ce masque et vérifiez s'il s'agit d'un palindrome. */
booléen privé estPalindrome Masque(int masque) {
si (palMasks.contientKey(mask)) retourne true; // déjà connu
StringBuilder sb = nouveau StringBuilder();
pour (int i = 0; i < n; i++) si ((mask & (1 << i)) != 0) sb.append(s.charAt(i);
Chaîne suivante = sb.toString();
int l = 0, r = longueur suivante() - 1;
pendant que (l < r) {
si (seq.charAt(l) != suite.charAt(r)) {
palMasks.put(masque, -1); // pas un palindrome
retourner faux;
}
l++; r--;
}
palMasks.put(masque, longueur suivante); // palindrome, conserver sa longueur
retour vrai;
}

/* Nombre de bits dans le masque. */
Int privé popcount(int masque) {
retour Integer.bitCount(masque);
}
}
«» "

**Pourquoi ça marche* *

1. **Tous les sous-ensembles** (4096) sont générés – trivial pour *n* ≤ 12.
2. Pour chaque sous-ensemble, nous construisons la subséquence et testons si c'est un palindrome.
3. Les masques palindromes sont mis en cache pour éviter une nouvelle vérification.
4. Chaque paire de masques de palindrome *disjoint* est inspectée; le produit maximum est stocké.

---

- Oui. 2. Solution Python

'`python
Solution de classe:
def maxProduct(self, s: str) -> Int:
n = len(s)
pleine = (1 << n) - 1
pal_len = {} # masque -> longueur (ou -1 si non palindrome)

# Helper: vérifier si le masque représente un palindrome
def is_pal(masque: int) -> C'est vrai.
si masque en pal_len:
Return pal_len[masque] != -1
chars = [s[i] pour i dans la plage(n) si masque et (1 << i)]
si des chars == Châssis:
pal_len[masque] = len(chars)
retour Vrai
pal_len[masque] = -1
Retour Faux

meilleur = 0
pour masque à portée (complet + 1):
i is_pal(masque) :
len1 = pal_len[masque]
sous = masque
# itérer sur tous les masques appropriés
sous = (masque - 1) & masque
tandis que sous:
si pal_len.get(sub, -1) != - 1 :
best = max(best, len1 * pal_len[sub])
sous = (sous - 1) & masque
le meilleur retour
«» "

> **Tip**: boucles `mask` sur tous les sous-ensembles; `sub = (mask-1)&mask` énumère ses sous-masques non vides dans un ordre décroissant.

---

- Oui. 3. Solution C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maxProduit(chaîne s) {
int n = s.size();
Int complet = (1 << n) - 1;
non ordonné_map<int, int> pal; // masque -> len ou -1

auto isPal = [&](int masque) -> Bool {
auto it = pal.find(masque);
si (it != pal.end()) retourne->seconde != -1;

sous chaîne;
pour (int i = 0; i < n; ++i)
si (masque et (1 << i))
sous.push_back(s[i]);

int l = 0, r = sous-dimension() - 1;
pendant que (l < r) {
Si (sub[l] != sous[r]) {
pal[masque] = -1;
retourner faux;
}
++l; --r;
}
pal[masque] = sous-dimension();
retour vrai;
};

int best = 0;
pour (int masque = 0; masque <= plein; ++masque) {
si (!isPal) continue;
int len1 = pal[masque];
// itérer sur tous les sous-masques disjoints
pour (int sub = masque; sub; sub = (sub - 1) & masque) {
si (pal[sub] != -1) // palindrome
best = max(meilleur, len1 * pal[sub]);
}
}
le meilleur retour;
}
};
«» "

> **C++ astuce**: `pour (int sub = masque; sub; sub = (sub - 1) & masque)` itemrate sur tous les sous-masques non-zéro du «masque».
> Nous sautons `sub==0` parce que les sous-séquences vides donnent le produit 0.

---

Article du blog : Le bon, le mauvais et le mauvais de LeetCode 2002

Introduction

> **LeetCode 2002 – Produit maximal de la longueur de deux séquences palindromiques** est un puzzle apparemment simple qui se transforme rapidement en un terrain de jeu délicieux pour le bit-masking, la récursion et la programmation dynamique.
> Avec seulement 12 caractères dans la chaîne d'entrée, l'espace de force brute de 212 = 4 096 sous-ensembles est suffisamment petit pour une recherche exhaustive, mais le problème exige toujours une manipulation soigneuse de *disjointité* et *vérification du palindrome*.
> Ce post vous guidera dans la solution la plus efficace, décomposer pourquoi il est le choix *meilleur*, et révéler les pièges que vous devriez éviter.

Le problème, corrigé

> Compte tenu d'une chaîne `s` (2 ≤ ≤ ≤ ≤ 12), trouver deux **disjoint** sous-séquences palindromiques de `s` dont le produit de longueurs est maximisé.
> * Disjoint* signifie qu'aucun indice dans `s` n'est utilisé dans les deux sous-séquences.
> Retourne ce produit maximum.

- Oui. Approches naïves

L'approche de la complexité Pourquoi c'est une mauvaise idée
- C'est quoi ?
Énumérer toutes **paires** des sous-séquences (4 0962)= O(22n)=16 millions de paires → encore faisables, mais gaspillées. Autres
Autres Attribuer récursivement chaque omble à *none*, *seq1* ou *seq2*.O(3n) -312 - 1.6 M indique → OK, mais l'utilisation de la pile lourde. Autres
Un facteur supplémentaire O(n2) n'est pas nécessaire pour ces chaînes courtes. Autres

Même si toutes ces méthodes se terminent rapidement pour *n* ≤ 12, une solution plus propre et plus optimale existe.

### La solution Bit-Mask élégante

**Idée**:
1. **Générer chaque sous-ensemble** d'indices sous forme de bitmask (0–4095).
2. Pour chaque sous-ensemble, **construisez la chaîne de subséquences** et vérifiez s'il s'agit d'un palindrome.
3. Entreposer le *longueur* de chaque masque de palindrome; si ce n'est un palindrome, le marquer `-1`.
4. Pour chaque masque de palindrome `masque`, itérer sur ses **sous-masques** (ou tous les masques qui sont disjoints) et calculer le produit avec un autre masque de palindrome. Gardez le maximum.

C'est vrai. Pourquoi cela fonctionne

- **Tous les palindromes sont identifiés**: En construisant la chaîne, nous évitons le DP complexe qui essayerait autrement de deviner les caractères.
- **La disjointité est banale**: Deux masques sont disjoints iff `mask1 & mask2 == 0`.
- **Le temps est dominé par 4 096 contrôles de masque**, chaque O(n) (n ≤ 12).
- **L'espace est négligeable**: Nous stockons au plus 4 096 entiers.

#### Code Walkthrough (Java)

"Java
// 1. Construire chaque subséquence de masque
StringBuilder sb = nouveau StringBuilder();
pour (int i=0; i<n; i++)
si ((masque & (1<<i)) != 0) sb.append(s.charAt(i);

// 2. Vérifier le palindrome à O(len)
Chaîne suivante = sb.toString();
int l=0,r=seq.longueur()-1;
alors que (l<r) si (seq.charAt(l++) != suite.charAt(r--)) nonPalindrome;

// 3. Résultat du cache
palLen.put(masque, longueur suivante); // palindrome
palLen.put(masque, -1); // pas un palindrome
«» "

Complexité

- **Temps**: "O(2n · n)` -50 k opérations pour le pire cas (`n=12`).
- **Espace**: `O(2n)` pour le cache.
- **Pratique**: Exécute en < 1 ms sur les processeurs modernes.

- Oui. Les mauvaises (éviter les erreurs courantes)

1. **Revérification des palindromes* *
*Bad*: Chaque paire de masques pourrait réévaluer le même sous-ensemble.
*Fix*: longueurs de cache ou drapeau booléen.

2. ** Désarticulation incorrecte* *
*Bad*: Utiliser `mask1 != masque2' ne suffit pas – des indices de chevauchement existent encore.
*Fix*: Utilisez bitwise ET pour tester la disjointité (`(masque1 & masque2) == 0`).

3. ** Sous-séquences concernant l'ampleur**
*Bad*: Ils sont techniquement palindromes de longueur 0, mais ils ne contribuent jamais à un produit maximum.
*Fix*: Sauter le masque `0` ou le manipuler explicitement avec le produit 0.

- Oui. Le mauvais : les pièges de la récursion et le débordement de la pile

Lors de la résolution de ce problème sur une interview de codage ou une plate-forme qui limite strictement la profondeur de récursion, l'approche d'assignation récursive (3n) peut causer un débordement de pile dans des langages comme Java ou Python.
L'utilisation d'un dénombrement **bottom-up bit-mask** élimine complètement la récursion et maintient l'utilisation de la mémoire constante.

Les pensées finales

Aspect du bien
- C'est quoi ?
**Simplicité**= Énumérer les masques → palindrome vérifier → produit. 3n récursion avec la machine d'état en désordre. DP avec des dimensions multiples et des frais généraux inutiles. Autres
**Performance **= 1 ms pour toutes les entrées. Toujours rapide mais moins propre. Risque d'atteindre des limites de temps si les contraintes étaient plus grandes. Autres
**Maintenabilité**= Boucles droites et opérations bitwise.= Plus difficiles à suivre en raison d'une récursion profonde. Code bloat avec des tables DP supplémentaires. Autres

> **Ligne de bottom**: Pour LeetCode 2002, la stratégie *bit-mask* est le gagnant clair.
> Il équilibre la brièveté, la vitesse et la lisibilité – exactement ce que les intervieweurs veulent voir.

Clôture

Que vous soyez en train de vous entraîner pour une entrevue de codage ou tout simplement aimer les puzzles algorithmiques, LeetCode 2002 offre un exemple parfait de transformer une explosion combinatoire en une routine bit-mask soignée.
Essayez-le vous-même dans votre langue préférée – sentez la satisfaction de ce résultat *maximum produit*! C'est ce qu'il a dit.

---

Bonus : Conseil d'entrevue

> Si l'intervieweur mentionne *n ≤ 12*, indiquez qu'une solution *bit-masque* sera la plus efficace.
> Expliquez que vous :
> 1. Énumérer tous les sous-groupes.
> 2. Cache palindrome masques.
> 3. Paire des masques disjoints.
> Démontrer à la fois **compétences d'analyse** et **expérience pratique de codage** vous débarque souvent l'offre d'emploi.

---

Références

- LeetCode 2002: https://leetcode.com/problèmes/produit maximal de la longueur de deux sous-séquences palindromiques/
- Tutoriels HackerRank
- Codeforces -Enumeration Submasque

Bon codage ! (en milliers de dollars)

---

*Cet article et les solutions d'accompagnement ont été conçus pour vous aider à maîtriser LeetCode 2002 et à vous préparer pour des entretiens qui valorisent l'élégance algorithmique. *