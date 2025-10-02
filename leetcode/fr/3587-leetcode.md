---
title: LeetCode 3587. Swaps adjacents minimum à la parité alternative -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Swaps adjacents minimum à la parité alternative
**Le bon, le mauvais et le mauvais – un guide complet pour votre prochaine entrevue de codage* *

> **Mots clés**: Leetcode, interview, algorithme, parité, swaps adjacents, interview de codage, Java, Python, C++, entretien d'emploi, ingénierie logicielle

---

- Oui. 1. Pourquoi ce problème vous fait penser

- ** Sujet classique de l'entrevue** : Il teste votre capacité à raisonner sur *parité*, *indices* et *mouvement optimal*.
La solution optimale est *O(n*), mais de nombreux candidats commencent par une force brute *O(n2)*.
- **Manipulation des caisses**: Le problème vous oblige à penser à *l'impossibilité* ('-1'), *les nombres égaux* et *les cibles multiples valides*.
- **Multillingue** : Vous pouvez présenter des solutions en Java, Python ou C++ – parfaites pour un portefeuille de polyglottes.

---

- Oui. 2. Exposé des problèmes (Code de bord 3587)

Vous recevez un tableau `nums` d'entiers distincts. Dans une opération, vous pouvez échanger ** tout deux éléments adjacents**.

Un arrangement est **valide** si chaque paire d'éléments voisins a une parité différente (l'un est pair, l'autre bizarre).

**Retour** le nombre minimum de swaps adjacents requis pour transformer les "nums" en "toute" arrangement valide.
Si c'est impossible, retournez `-1`.

> **Exemples**
> - `[2,4,6,5]` → `3`
> - `[2,4,5,7]` → `1`
> - `[1,2,3]` → `0`
> - `[4,5,6,8]` → `-1`

---

- Oui. 3. Intuition – l'indice de l'Even & Odd

1. **Collectez les indices** de tous les nombres paires et de tous les nombres impairs.
2. Un tableau *valid* doit alterner la parité, de sorte que les nombres d'evens et de cotes peuvent varier au plus.
*Si ''evens - cotes' > 1` → impossible → retour `-1`*.
3. Il y a **au plus deux** modèles valides:
* Commencez avec même → evens occupent les indices `0,2,4,...`
* Commencez par impair → les cotes occupent les indices `0,2,4,...`
4. Pour un modèle donné, le nombre de swaps correspond à la somme de *distances* chaque élément doit se déplacer pour atteindre son indice cible.
Pourquoi ? Parce que chaque swap adjacent déplace un élément par exactement une position.

> **Formule clé**
> Si vous avez une liste `pos` des indices originaux et que vous voulez qu'ils soient aux indices cibles `0,2,4,...` (éléments `k`),
> le coût est de:

---

- Oui. 4. Algorithme (temps O(n), espace supplémentaire O(1))

Texte
1. Construisez deux listes : evenIdx, impairIdx.
2. If=evenIdx= -=oddIdx= > 1 → retourner -1.
3. Initialiser les ans = INF.
4. Si evenIdx peut occuper des positions égales → ans = min(ans, coût(evenIdx)).
5. Si impairIdx peut occuper même des positions → ans = min(ans, cost(oddIdx)).
6. Retourne-toi.
«» "

*`cost(list)`* implémente la formule de distance.

---

- Oui. 5. Code de référence

#### 5.1 Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe {
// Helper: somme des distances aux indices cibles 0,2,4,...
coût privé long(Liste<entier>pos) {
swaps longs = 0;
pour (int i = 0; i < pos.size(); i++) {
swaps += Math.abs(pos.get(i) - 2L * i);
}
swaps de rendement;
}

public int minSwaps(int[] nums) {
Liste <integer> même = nouvelle liste d'array<>();
Liste<entier> impair = nouvelle liste de distribution<>();

pour (int i = 0; i < nombres de longueur; i++) {
si (nombres[i] % 2] 0) même.add(i);
autres impair.add(i);
}

si (Math.abs(even.size() - impair.size()) > 1) retour -1;

long ans = long. MAX_VALEUR;

si (even.size() >= impair.size() ans = Math.min(ans, cost(even));
si (odd.size() >= even.size() ans = Math.min(ans, cost(odd));

retour (int) ans;
}
}
«» "

> **Pourquoi ? **
> Chaque coût d'échange peut aller jusqu'à `n`, et en additionnant `n` swaps donne `O(n2)` dans le pire des cas. `long` protège contre les débordements pour `n = 105`.

---

#### 5.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minSwaps(self, nombres: List[int]) -> Int:
# Positions d'un et zéros
impair_pos = [i pour i, v dans énumérate(nums) si v & 1]
n = len(nums)

# Helper: coût lorsque le modèle de démarrage est 'démarrer' (0 ou 1)
def count_swaps(départ: int) -> Int:
retour sum(abs(p - (début + 2 * i)) pour i, p dans énuméré(odd_pos))

# Essai d'impossibilité rapide
m = 2 * len(odd_pos)
si m < n ou m > n:
retour -1

si m == n: # nombres égaux – essayer les deux commence
retour min(count_swaps(0), count_swaps(1))
si m == n + 1: # cotes > evens – doit commencer par impair
retour count_swaps(0)
Si m == n - 1: # evens > cotes – doit commencer par même
retourner count_swaps(1)

retour -1
«» "

> **Note**: Les entiers de Python sont débordés, donc nous ne nous inquiétons pas du débordement.

---

C++ (Fast & Clean)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
long coût(vecteur continu<int> &pos) {
swaps longs = 0;
pour (size_t i = 0; i < pos.size(); ++i) {
swaps += llabs(pos[i] - 2LL * i);
}
swaps de rendement;
}
public:
Int minSwaps(vector<int>& nums) {
vecteur <int> même, étrange;
pour (int i = 0; i < nums.size(); ++i) {
(nums[i] % 2 == 0 ? même : impair).push_back(i);
}

si (abs(int)even.size() - (int)odd.size()) > 1) retour -1;

long an = LLONG_MAX;

si (même.size() >= impair.size() ans = min(ans, coût(même));
si (odd.size() >= even.size() ans = min(ans, cost(odd));

retourner static_cast<int>(ans);
}
};
«» "

---

- Oui. 6. Analyse de la complexité

Métrique
- C'est vrai.
**Heure**
**Auxiliaire**= O(1) (sauf pour les listes d'entrée)= O(1)= O(1)=
L'espace

> **Pourquoi est-ce O(1)? * *
> Nous ne conservons les indices originaux que dans deux *listes* – la même que la taille des entrées. Une fois que nous calculons le coût que nous rejetons les listes, l'espace *extra* est donc constant.

---

- Oui. 7. Les pièces de la série "Bad" – Pièges communs

Pourquoi ça arrive ?
- Oui.
**Considérer `-1` comme un indice spécial**. Certains candidats traitent `-1` comme une sentinelle et l'utilisent accidentellement dans les calculs de distance. Effectuer la vérification impossible **avant** les coûts de calcul. Autres
La formule de coût est basée sur les indices 0 ('0,2,4,...'). Les erreurs hors-par-un brisent tout. Tester explicitement les deux motifs (`start = 0` ou `start = 1`). Autres
**En supposant que les deux modèles sont toujours valides**.Si les chiffres diffèrent par un seul, un seul modèle est légal. Utiliser `>=` pour déterminer le coût à calculer. Autres
**Débordement manquant**=Les distances de cumul peuvent atteindre 105 × 105 = 1010, ce qui dépasse 32 bits int.= Utiliser des entiers 64 bits (`long` en Java, `long` en C++, `int` par défaut en Python). Autres

---

- Oui. 8. Liste de contrôle des cas de bord

Qu'est-ce qu'un test
C'est pas vrai.
**Tous les uniformes**
**Toutes les cotes**
**Comptes d'égalité** Autres
Autres **Un extra impair** – doit commencer par impair → coût `0`. Autres
Autres **Un supplément de même**. Autres
**Grande alternance** Autres

---

- Oui. 9. Conseils d'entrevue – Comment faire face à cette question

1. ** Expliquer l'impossibilité tôt**.
Si la différence de nombre est supérieure à un, il n'existe aucun arrangement valide. (en milliers de dollars)
Cela montre que vous lisez attentivement la déclaration de problème.

2. ** Dessiner un diagramme** des indices.
Même les indices → `0,2,4,...` et les indices Odd → `1,3,5,...`.
Les aides visuelles convainquent les intervieweurs que vous pouvez raisonner sur papier.

3. **Parlez du coût en tant que distance**.
Chaque swap adjacent déplace un élément d'une étape. Ainsi, le nombre minimal de swaps correspond à la distance totale que les éléments doivent parcourir. (en milliers de dollars)

4. **Edge‐case à travers**.
Montrez que l'algorithme fonctionne pour les deux modèles et pourquoi nous avons besoin de la `min` sur eux.

5. ** Temps et espace**.
Le temps d'O(n) parce que nous traversons seulement le tableau un nombre constant de fois, et l'espace d'O(1) parce que nous ne gardons que quelques compteurs. (en milliers de dollars)

6. **Bonus** – Parlez des swaps *stable vs. unstable*.
Puisque tous les éléments sont distincts, l'ordre relatif des éléments de la même parité ne compte pas.

---

- Oui. 10. Résumé – Ce dont vous devriez vous souvenir

- **Collecter les indices** → `evens` & `odds`.
- **Vérifier la faisabilité** → `=2 - cotes <= 1`.
- **Comptabiliser deux coûts possibles** → `.
- **Prenez le minimum** → c'est la réponse.
- **Retour `-1`** si impossible.

> **Pratique**: Essayez de modifier le problème:
> *Et si vous pouviez échanger deux éléments (pas seulement adjacents)? *
> *Et si le tableau avait des duplicatas? *
> Cela vous permettra d'approfondir votre compréhension du concept d'indice de parité.

---

## 11. Pensée finale – Tourner C'est dans une compétence professionnelle

Les problèmes de LeetCode comme 3587 sont *micro-projets* qui présentent un candidat :

- Aiguïté algorithmique
- Codage de la fluidité dans plusieurs langues
- Attention aux cas bord
- Capacité de communiquer clairement les idées

Ajoutez le code snippets (Java, Python, C++) à votre portfolio, blog sur les aspects bons, mauvais, laids et pratiques expliquant le problème à haute voix. Les intervieweurs aiment les candidats qui * non seulement résolvent le problème, mais aussi articulent leur processus de pensée. *

> ** Prochaines étapes**
> 1. Cloner cette repo et ajouter des tests unitaires pour tous les cas de bord.
> 2. Poster la solution sur GitHub avec un README clair.
> 3. Partagez le blog sur LinkedIn/Medium avec le tag #CodingInterview.
> 4. Continuez à affiner : demandez aux pairs de revoir votre code et critiquez les explications.

Bonne chance pour votre prochaine interview – vous avez ça!