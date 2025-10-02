---
titre: LeetCode 2400. Nombre de façons d'atteindre une position après exactement k Étapes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre de façons d'atteindre une position après exactement k Étapes – LeetCode 2400**

> **Numéro de dossier:** 2400
> **Difficulté:** Moyenne
> **Tags:** Maths, Combinatorics, Dynamic Programming, Algorithmes, Interview

---

TL;DR

Langue Heure Espace
- C'est quoi ?
* * * * * * * * * * * * * * *
**Python******O(k)** (solution math)
*C++******O(k)** (solution pour les mathématiques)

La solution *cleanest* utilise une formule combinatoire simple:

«» "
Let d = endPos - début Pos.
Si vous voulez > k → impossible → retourner 0
Si (k - d) % 2 0 → impossible → retourner 0
Sinon:
rightSteps = (k + d) / 2 // nombre d'étapes à droite
ways = C(k, rightSteps) % MOD
«» "

Le calcul du coefficient binomial modulo `109+7` dans le temps `O(k)` en utilisant des inverses multiplicatifs donne une réponse rapide.

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 2400

> ** Auditoire cible :** Ingénieurs de front/arrière-fin, passionnés d'algorithmes, recruteurs
> **Objectif :** Offrez une plongée profonde qui met en valeur vos compétences en résolution de problèmes, gagne du crédit SEO et vous aide à décrocher un travail d'ingénierie logicielle.

---

Aperçu du problème

> Nombre de façons d'atteindre une position après exactement k Étapes *
> Vous commencez par `startPos` sur une ligne entière infinie et pouvez passer **+1** ou **-1** par mouvement.
> Après **exactement** étapes `k`, combien de séquences distinctes de mouvements atterrissez-vous à `endPos`?
> Retour le compte modulo `1 000 000 007`.

C'est vrai. Principales contraintes

- `1 ≤ démarrage Pos, endPos, k ≤ 1000'
- Oui. La ligne n'est pas délimitée, de sorte que les positions peuvent être négatives.

---

C'est vrai. L'approche « Bonne » – Pourquoi l'approche mathématique gagne

Description
C'est pas vrai.
**O(k) Temps**= Pas de table ou de récursion DP – une seule boucle calculant un coefficient binôme. Autres
**O(1) Espace**= Seulement quelques variables entières. Autres
**Mathématiquement Élégant** Autres
**Fast Modulo Arithmetic** , utilise le petit théorème de Fermat pour les inverses modulaires, en évitant les factoriels précalculés coûteux. Autres
**Facile à vérifier**.Les petits cas de test peuvent être recoupés manuellement. Autres

L'observation centrale : chaque étape est soit gauche, soit droite. Supposons que nous fassions des marches `r` à droite et `l` à gauche. Nous avons besoin :

«» "
r + l = k
r – l = fin Pos – début Pos → r = (k + (endPos – startPos) / 2
«» "

`r` doit être un entier et `0 ≤ r ≤ k`. Si ces conditions échouent, la réponse est zéro.

Une fois que `r` est connu, le nombre de séquences distinctes est simplement `C(k, r)` – les moyens de choisir les positions de la droite se déplace parmi les étapes `k`.

---

C'est vrai. Pourquoi un DP direct pourrait nuire

Une solution naïve de programmation dynamique:

Texte
dp[pos][step] = moyens d'atteindre `pos` après les déplacements `step`
«» "

- **Blow-up mémoire**: `dp` a la taille `(2k+1) × (k+1)` → ~3 M entrées pour `k = 1000`.
- **Heure**: `O(k2)` en raison de boucles imbriquées ou d'appels récursifs.
- **Profondeur de récursion**: Risque de débordement de la pile pour les plus gros "k".
- **Questions relatives aux indices**: Il faut compenser les positions négatives en ajoutant la plaque de chaudière.

Bien que le PDD soit théoriquement simple et fonctionne pour les contraintes données, il est *surqualifié* pour ce problème et pourrait échouer dans des limites plus strictes ou dans une entrevue où le temps est critique.

---

C'est pas vrai. Les cas de bord et les pièges

Pourquoi il est laid Comment l'éviter
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Inadéquation de la rareté**= Si `(k - d)` est étrange, aucune séquence n'existe. Cochez explicitement `(k - d) % 2 != 0' avant de calculer le binôme. Autres
**Les tableaux DP doivent cartographier les indices négatifs pour les indices de tableau. Utilisez un offset (`+k`) ou un `HashMap`. Autres
**Les inverses de Modulo peuvent déborder s'ils ne sont pas traités comme des "longs". Autres
**Modulaire inverse** Utiliser Fermats peu théorème: `pow(a, MOD-2, MOD)` ou récursion `inv(a) = (MOD - MOD//a) * inv(MOD%a) % MOD`.
**Étapes droites de Zero**= Si `r = 0`, `C(k,0)` Loop de `0` à `r-1`; si `r == 0`, sauter la boucle et retourner 1.

---

Détails de la mise en œuvre

5.1. Inverse modulaire (Fermat)

Pour un module primaire `p`, l'inverse modulaire de `a` est `a^(p-2) mod p`. Nous pouvons calculer cela par exponentiation rapide dans le temps `O(log p)`, ou récursivement avec la propriété:

«» "
inv(a) = (p - p/a) * inv(p % a) % p
«» "

La formule récursive est efficace pour les petits `a` (= k), ce qui est tout ce dont nous avons besoin pour ce problème.

5.2 Coefficient binôme en O(k)

«» "
C(k, r) = Π_{i=0}^{r-1} (k - i) / (i + 1)
«» "

Nous effectuons la division par l'inverse modulaire:

«» "
Res = 1
pour i en r-1:
Res = res * (k - i) % MOD
res = res * inv(i + 1) % MOD
«» "

Cela garde `res` petit et respecte le module.

---

Nombre d'échantillons de code

##### 6.1. Java

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

// Inverse modulable récursive rapide (le petit théorème de Fermat)
intérieur statique long inv(long a) {
si (a) 1) retour 1;
retour (MOD - MOD / a) * inv(MOD % a) % MOD;
}

Nombre d'entrées publiques DeWays(int début Pos, int endPos, int k) {
int diff = fin Pos - début Pos;

// Impossible si la distance > k ou le décalage de parité
Si (Math.abs(diff) > k=" ((k - diff) & 1) == 1) retourner 0;

int droite = (k + diff) / 2; // nombre de +1 étapes
si (droite < 0) droite > k) retourne 0;

longue rés = 1;
pour (int i = 0; i < droite; i++) {
res = res * (k - i) % MOD;
res = res * inv(i + 1) % MOD;
}
retour (int) rés;
}
}
«» "

*Pourquoi il est facile d'interviewer:* Tout arithmétique est effectué avec `long`, et la fonction inverse est minuscule et pure.

6.2 Python

'`python
MOD = 1 000 000 007

def mod_inv(a: int) -> Int:
"""Inverse modulaire récursive pour MOD prime."""
si a) :
retour 1
retour (MOD - MOD // a) * mod_inv(MOD % a) % MOD

def number_of_ways(startPos: int, endPos: int, k: int) -> Int:
diff = fin Pos - début Pos

# Contrôles de parité et de faisabilité
si abs(diff) > k ou (k - diff) & 1:
retour 0

droite = (k + diff) // 2
Res = 1
pour i à portée (à droite):
Res = res * (k - i) % MOD
res = res * mod_inv(i + 1) % MOD
retour res
«» "

Les Python's intégrés dans de grands entiers signifient que nous ne nous soucions pas du débordement, mais nous gardons toujours l'arithmétique dans `int` pour la vitesse.

Oui. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue MOD = 1'000'000'007LL;

// Inverse modulaire récursive (Fermat)
long mod Inv (long a) {
si (a) 1) retour 1;
retour (MOD - MOD / a) * modInv(MOD % a) % MOD;
}

solution de classe {
public:
Numéro int DeWays(int début Pos, int endPos, int k) {
int diff = fin Pos - début Pos;
si (abs(diff) > k. ((k - diff) & 1)) retourne 0;

int droite = (k + diff) / 2;
longue rés = 1;
pour (int i = 0; i < droite; ++i) {
res = res * (k - i) % MOD;
res = res * modInv(i + 1) % MOD;
}
retourner static_cast<int>(res);
}
};
«» "

Les trois implémentations partagent la même structure logique ; seule la syntaxe diffère.

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
**Maths/combinatoire** (variables constantes)
**DP (si vous choisissez de mentionner)**

Avec `k ≤ 1000`, la solution mathématique est triviale à calculer, tandis que DP serait plus lent et utiliserait plus de mémoire.

---

### # 8.

Pourquoi ça fait mal
- C'est quoi ?
Retour `0` trop tôt (avant le contrôle de parité)
Utiliser `pow(a, MOD-2, MOD)` en Java sans gérer longtemps
À l'exception de l'utilisation d'un offset (`+k`) ou d'une carte de hachage
Autres Oublier le modulo après chaque addition/subtraction.

---

Entretien- Conseils de style

- **Démarrer avec les contraintes** – `k ≤ 1000` signifie que nous pouvons nous permettre des opérations `O(k)`; pas besoin de pré-computation lourde.
- **Énoncer la règle de parité d'abord** – les recruteurs aiment clairement pourquoi c'est impossible.
- ** Expliquer le petit théorème de Fermat** – démontre la connaissance de la théorie des nombres, qui impressionne souvent les ingénieurs seniors.
- **Afficher à la fois DP et mathématiques** – Si l'intervieweur demande : Qu'en est-il si les contraintes étaient de 105 ?
- **Test avec de petites caisses** – Écrire un générateur de force brute dans votre IDE pour recouper la formule. Mentionnez que lors de l'entretien vous pouvez montrer quelques exemples sur le tableau blanc.

---

#### 10- Loin

> **La solution optimale pour LeetCode 2400 est un monoligne en logique mais nécessite une implémentation arithmétique modulaire *clean*. * *
> La maîtrise de ce modèle non seulement résout le problème en millisecondes, mais montre également les recruteurs, vous pouvez repérer des structures combinatoires cachées dans des problèmes de DP apparemment simples.

Codage heureux, et que votre prochaine entrevue comporte une *combinaison* de perspicacité mathématique et de code propre – tout comme la solution ci-dessus! C'est ce qu'il a dit.

---

Liste de contrôle pour le démarrage rapide de votre entrevue

1. **Comprendre les contraintes. **
2. ** Vérifier la faisabilité**: `abs(d) ≤ k` et `(k - d) % 2 == 0`.
3. **Computer droitEtapes = (k + d) / 2.**
4. **Calculez `C(k, rightSteps)` avec les inverses modulaires en O(k). **
5. **Retour `ways % MOD`.**

Imprimez le code, passez à travers un cas de test, et expliquez la logique de parité – faite!

---

* Bonne chance, et que votre recherche d'emploi soit aussi rapide que l'algorithme ci-dessus! *