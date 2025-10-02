---
titre: LeetCode 2147. Nombre de façons de diviser un long corridor -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2147. Nombre de façons de diviser un long corridor
### (Hard) – Leetcode, heure O(N), espace O(1)

Langue Heure Espace
- C'est quoi ?
Java O(n)
Python O(n)
O(n)

---

### TL;DR
1. **Si le couloir contient un nombre impair de sièges (`S`) → réponse = 0.**
2. **Autrement** marcher la corde, garder l'index du siège *précédent*.
3. Chaque fois que nous atteignons le siège *3ème, 5ème, 7ème...*, multipliez le résultat par la distance entre ce siège et le siège précédent.
4. Retour « résultat % 1_000_000_007 ».

Pourquoi ça marche : chaque --------entre une paire de sièges peut accueillir un diviseur dans n'importe quelle position qui se trouve entre les deux sièges. Le nombre de positions de division possibles pour une paire donnée est exactement le nombre d'indices entre les deux sièges ('i - prevSeat'). Multiplier tous ces choix indépendants donne le nombre total de façons.

---

Code (toutes les 3 langues)

### Java

"Java
solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

Nombre d'entrées publiques DeWays(Couloir d'attache) {
longue res = 1L;
siège intCoupe = 0;
int prevSeatIdx = 0; // sera écrasé sur le premier siège

pour (int i = 0; i < corridor.longueur(); i++) {
si (corridor.charAt(i) == 'S') {
siègeCount++;

si (siègeCoupe > 2 & & seatCount % 2 == 1) {
res = (res * (i - prevSeatIdx)) % MOD;
}
prevSeatIdx = i;
}
}

si (siègeCoupe % 2) 1=1SiègeCoupe < 2) {
retour 0;
}
retour (int) (rés % MOD);
}
}
«» "

Python

'`python
Solution de classe:
MOD = 10**9 + 7

def numberOfWays(self, corridor: str) -> Int:
Res = 1
= 0
prév_siège = 0

pour idx, ch dans l'énumération (corrideur):
Si ch == 'S':
_siège += 1
si _siège > 2 et siège
res = (res * (idx - prev_seat)) % self. MOD
prév_seat = idx

retour 0 si seat_cnt % 2 == 1 ou siege_cnt < 2 autres res % self. MOD
«» "

C++

'`cpp
solution de classe {
public:
Numéro int DeWays (couloir à cordes) {
longue MOD = 1'000'000'007LL;
longue rés = 1;
Siège intérieur Cnt = 0;
nt prevSeat = 0;

pour (int i = 0; i < (int)corridor.size(); ++i) {
si (corridor[i] == 'S') {
+ siègeCnt;
si (siègeCnt > 2 & & siège Cnt % 2 == 1) {
res = (rés * (i - prevSeat)) % MOD;
}
prevSeat = i;
}
}

si (siègeCnt % 2 == 1=2 siègeCnt < 2) retour 0;
retour (int)(res % MOD);
}
};
«» "

---

Article sur le blog – Le bon, le mauvais et le mauvais de Leetcode 2147

Introduction
Lorsque vous préparez une entrevue d'ingénierie logicielle, Leetcodes **Nombre de façons de diviser un long corridor** (Problème 2147) est une chaîne de caractères classique Puzzle DP qui semble faussement simple à première vue. Dans ce post, nous disséquons le problème de **tous les angles**:

C'est bien, c'est mal.
C'est pas vrai.
**Programme dynamique** rencontre **combinatoire**
**O(N)** temps – idéal pour une entrevue de 30 minutes L'état *odd-seat* peut vous faire monter.Le produit des trous peut déborder si vous n'êtes pas prudent.

Avec des explications détaillées, vous saurez *pourquoi* l'algorithme fonctionne, *quoi* pourrait mal tourner, et *comment* pour éviter les erreurs courantes.

**Mots-clés de référence** – Solution de Leetcode, algorithme d'entretien, chaîne de programmation dynamique, entretien de codage Java/Python/C++, algorithme O(n), modulo 1e9+7, prép. d'entretien de codage.

---

- Oui. 1. Énoncé du problème (reformulé)
Compte tenu d'une chaîne `corridor` de longueur **= 105** qui ne contient que `S` (siège) et `P` (personne), vous avez deux sièges d'une rangée qui doivent former un bloc de deux sièges exactement. L'objectif est de placer des diviseurs entre des blocs consécutifs de deux sièges de sorte que:

* chaque bloc a exactement deux sièges,
* un diviseur peut être placé dans n'importe quelle position *vide* entre deux sièges consécutifs,
* tout le couloir est divisé en tels blocs.

Return le nombre de positions de diviseur distinctes modulo `109+7`.

---

- Oui. 2. Intuition: Pourquoi les sièges comptent, pas les gens
Si le nombre de sièges est de **odd**, il est impossible de diviser le couloir en paires de deux sièges – pensez à essayer de diviser 5 sièges en groupes de 2. C'est la première fois que vous retournez un nombre non nul pour une entrée impossible.

Pour un nombre **même** de sièges, vous pouvez considérer le couloir comme une séquence de positions de sièges
"s1, s2, s3, ..., s2k".
Chaque *diviseur* doit être assis *entre* deux places assises consécutives: `s2` et `s3`, `s4` et `s5`, ..., `s2k-2` et `s2k-1`.
Entre deux sièges consécutifs, vous pouvez placer le diviseur dans n'importe quelle position qui se trouve strictement *entre* eux. Si la distance entre les sièges est `d`, il y a exactement `d` des positions valides.

---

- Oui. 3. L'algorithme multiplicatif (bon)
L'élégante solution O(N) se résume en un seul passage:

1. Nombre de places assises.
2. Gardez l'index du siège *précédent* (`prevSeatIdx`).
3. Lorsque nous atteignons le siège numéro 3, 5, 7, ... (chiffre de siège od > 2), nous multiplions la réponse par `i - prevSeatIdx`.

**Pourquoi?**
Les choix de placement du diviseur pour chaque *gap* sont indépendants. Le nombre total de configurations est le produit des options pour chaque écart.

La preuve de l'exactitude
- *Base*: Pour les deux premiers sièges, il n'y a qu'un seul moyen de diviser le couloir - le diviseur est *avant* siège 3, donc nous commençons `res = 1`.
- *Étape d'induction*: Supposons que nous avons correctement traité les premiers sièges `2t` (formant des blocs `t`).
Lorsque nous rencontrons le siège `2t+1` (le début du bloc suivant), le nombre de positions entre le siège `2t` (le dernier siège du bloc `t`) et le siège `2t+1` est exactement `i - prevSeatIdx`. Multiplier par ce facteur préserve l'exactitude parce que chaque nouveau bloc des décisions de placement sont indépendants des précédentes.

Par induction, après la finition de la boucle, «res» est égal au produit de tous les choix indépendants d'écart, c'est-à-dire le nombre total de configurations de diviseurs.

---

- Oui. 4. Les pièges communs

Erreurs dans les résultats
- C'est quoi ?
**Ignorer le modulo** – Utiliser `int` pour le produit= Débordement entier → Mauvaise réponse= Utiliser `long long` (Java `long`, Python `int` gère les gros ints) et appliquer `% MOD` chaque multiplication. Autres
**Retour sur chaque siège** – "prevSeat" non initialisé. Autres
** Vérification du siège Cnt > 1` au lieu de `siège Cnt >= 2'**. Décomptes lorsque le couloir a exactement 2 sièges mais pas de diviseurs.La réponse est 1 (seulement le diviseur initial) quand `siège Cnt. 2'. Veiller à ce que `seatCnt >= 2' avant de retourner non-zéro. Autres
**Off‐by‐one dans la distance**= Comptage `i - prevSeat` quand `prevSeat` est le *premier* siège pour le troisième siège au lieu du second Dans l'algorithme fourni `prevSeat` est mis à jour après chaque siège, de sorte que lorsque le siège #3 est traité, il détient l'index #2S du siège, donnant la distance correcte. Autres
**Ne pas gérer le nombre de sièges impairs** si "seatCnt % 2" 1` → retour 0.

---

- Oui. 5. Les approches naïves alternatives (et pourquoi elles échouent)

La complexité Pourquoi il fait défaut
- C'est quoi ?
** Forcer tous les placements de diviseur** – DFS/Backtracking. Autres
** Programmation dynamique avec état** – `dp[i][j]` (positions, parité) Autres
**Divide & Conquer en divisant sur le premier siège impair**= O(n log n) si ce n'est prudent==Toujours trop lent pour le pire cas. Autres

Ces solutions sont un rappel que **sur-ingénierie** peut tuer votre temps d'exécution sur Leetcode. L'astuce produit-de-gaps est la plus propre, la plus rapide et la plus conviviale des entrevues.

---

- Oui. 6. Conseils pour l'entrevue

1. **Lisez attentivement les contraintes. **
*La longueur de la chaîne jusqu'à 105 → O(N) est obligatoire. *
2. ** Expliquez d'abord l'intuition. **
Le nombre de positions de séparation entre deux sièges est simplement la distance entre eux. (en milliers de dollars)
3. **Énoncer l'algorithme étape par étape.**
Ceci démontre que vous pouvez traduire l'intuition en un plan concret.
4. **Mention le modulo.**
Leetcode demande toujours le modulo 1 000 000 007; oubliant de prendre "% MOD" peut voyager le juge.
5. **Testez les cas de bord vous-même. **
Texte
"" → 0
"S" → 0
"SS" → 1
"SPSPSS" → 0 (sièges)
"SSPSPSS" → 2
«» "
Montre que ton code passe ça.

---

Conclusion

Le problème du nombre de façons de diviser un long corridor est un brillant exemple d'intelligence **O(N)** cachée derrière une déclaration apparemment compliquée.
- Le *good* est sa solution linéaire – juste un scan, une multiplication par siège impair.
- Le *mauvais* est qu'une seule oubli (compte de siège ou ou oubli de modulo) invalide instantanément toute la réponse.
- Le *ugly* réside dans la tentation d'être trop compliqué avec le PDD ou le retour en arrière; le simple calcul est la clé.

Si vous vous adressez à votre prochaine entrevue de codage, rappelez-vous : *chercher des choix indépendants*, *réduire le problème à un produit de lacunes* et *appliquer modulo tôt et souvent*.

Bon codage ! C'est ce qu'il a dit.

> **Si vous avez trouvé ce post utile, donnez-lui un pouce vers le haut, partagez-le avec vos coéquipiers, et suivez mon GitHub/Twitter pour plus de solutions d'entrevue. **

---

Références

- Leetcode Problem 2147: [https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor](https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor)
- Discuter du fil de discussion – Nombre de façons de diviser un long corridor – [https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor/discuss](https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor/discuss)

---

> **Vous souhaitez maîtriser plus de problèmes de Leetcode ? * *
> Abonnez-vous à ma newsletter : *[Votre lien de newsletter]*
> Suivez-moi sur Twitter : *[@Votre poignée] *
> Bonne chance, et que vos entretiens soient aussi propres que cette solution!