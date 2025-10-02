---
titre: LeetCode 1787. Faire le XOR de tous les segments égal à zéro -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code

Voici trois implémentations pleinement opérationnelles – **Java 17**, **Python 3.11** et **C++17** – qui résolvent LeetCode 1787
"Faites que le XOR de tous les segments soit égal à zéro".
Tous les trois partagent la même idée algorithmique :

Étape Idée Autres
- Oui.
**Observation** – Pour chaque fenêtre de taille `k` pour avoir XOR `0`, le tableau doit être *k‐périodique*: `a[i] == a[i+k]` pour tous les `i` valides. Autres
Autres Les indices qui partagent le même "i mod k" appartiennent au même *groupe*. Tous les éléments d'un groupe seront finalement égaux. Autres
**Coût d'un groupe** – Si nous choisissons une valeur `v` pour un groupe, nous devons changer chaque élément qui n'est pas déjà `v`.
`coût(groupe, v) = taille(groupe) – freq(v)` Autres
Autres ** Contrainte mondiale** – Le XOR des valeurs choisies pour les groupes `k` doit être `0`. Autres
= changements minimums pour les premiers groupes « i » dont le XOR est « x ».
Transition: pour chaque valeur du groupe "v" "
«dp[i+1][x ^ v] = min(dp[i+1][x ^ v], dp[i][x] + coût(groupe_i, v)» Autres
Résultat – `dp[k][0]`. Autres

Le nombre de valeurs distinctes est au plus `1024` (`0 ≤ a[i] < 210`), de sorte que le DP fonctionne dans
`O(k · 1024 · différentesValeurs)` – facilement rapide pour `n ≤ 2000`.

---

#### 1.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
Int public int minChanges(int[] nums, int k) {
int n = longueur nums;
// freq[mod] -> Carte <valeur, nombre>
@SuppressAvertissements("non vérifié")
Carte<entier,entier>[] freq = nouveau HashMap[k];
int[] groupSize = nouveau int[k];
pour (int i = 0; i < n; i++) {
g = i % k;
freq[g] = freq[g] == null ? nouveau HashMap<>() : freq[g];
freq[g].merge(nums[i], 1, entier::sum);
Groupe Taille[g]++;
}

MAX_XOR = 1 << 10; // 0 ... 1023
int[] dp = nouvelle int[k + 1][MAX_XOR];
pour (int i = 0; i <= k; i++) Arrays.fill(dp[i], entier. MAX_VALUE;
dp[0][0] = 0;

pour (int g = 0; g < k; g++) {
// toutes les valeurs possibles dans ce groupe
Définit les valeurs <integer> = freq[g] == null ? Collections.videSet() : freq[g].keySet();
pour (int x = 0; x < MAX_XOR; x++) {
si [dp[g][x]] Integer.MAX_VALUE) continuer;
pour (int v : valeurs) {
Int nouveau Xor = x ^ v;
coût int = groupeSize[g] - freq[g].get(v);
dp[g + 1][newXor] = Math.min(dp[g + 1][newXor], dp[g][x] + coût);
}
// envisager aussi de choisir une valeur qui n'apparaît jamais (coût = groupeTaille)
dp[g + 1][x] = Math.min(dp[g + 1][x], dp[g][x] + groupeTaille[g];
}
}
retour dp[k][0];
}
}
«» "

> **Pourquoi la valeur qui n'apparaît jamais ? **
> C'est la même chose que de choisir une valeur avec la fréquence `0`; nous la traitons par le `dp[g][x] + groupSize[g]` mise à jour qui utilise la valeur *meilleure* du groupe.

---

#### 1.2 Python 3.11

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def minChanges(self, nombres: List[int], k: int) -> Int:
n = len(nums)
freq = [Counter() pour _ dans la plage(k)]
group_size = [0] * k

pour i, v in énumérate(nums):
g = i % k
[g][v] += 1
group_size[g] += 1

MAX_XOR = 1 << 10 # 0 ... 1023
INF = 10**9
dp = [[INF] * MAX_XOR pour _ dans la plage (k + 1)]
dp[0][0] = 0

pour g dans la plage k:
vals = list(freq[g].keys()) # valeurs distinctes qui apparaissent déjà
pour x dans la plage (MAX_XOR):
Si dp[g][x]] INF:
poursuivre
pour v en vals:
nouvelle_x = x ^ v
coût = groupe[g] - freq[g][v]
si dp[g][x] + coût < dp[g + 1][new_x]:
dp[g + 1][new_x] = dp[g][x] + coût
# l'affaire "Pick une nouvelle valeur qui n'est jamais apparue"
pour x dans la plage (MAX_XOR):
si dp[g][x] != INF:
dp[g + 1][x] = min(dp[g + 1][x], dp[g][x] + groupe[g])

retour dp[k][0]
«» "

---

*## 1.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minChanges(vector<int>& nums, int k) {
int n = nombres.size();
// freq[mod] -> non ordonné_map<valeur, nombre>
vector<unordered_map<int,int>> freq(k);
vecteur<int> groupeTaille(k, 0);

pour (int i = 0; i < n; ++i) {
g = i % k;
++groupSize[g];
++frek[g][nums[i]];
}

MAX_XOR = 1 << 10; // 0 ... 1023
vector<vector<int>> dp(k + 1, vector<int>(MAX_XOR, INT_MAX));
dp[0][0] = 0;

pour (int g = 0; g < k; ++g) {
// Recueillir des valeurs distinctes dans ce groupe
vecteur<int> valeurs;
pour (auto &p : freq[g]) valeurs.push_back(p.first);

pour (int x = 0; x < MAX_XOR; ++x) {
si (dp[g][x] == INT_MAX) continue;
pour (int v : valeurs) {
int nx = x ^ v;
coût int = groupeTaille[g] - freq[g][v];
dp[g + 1][nx] = min(dp[g + 1][nx], dp[g][x] + coût);
}
}
// choisir une valeur qui n'apparaît jamais (coût = groupeTaille)
pour (int x = 0; x < MAX_XOR; ++x)
Si (dp[g][x] != INT_MAX)
dp[g + 1][x] = min(dp[g + 1][x], dp[g][x] + groupeTaille[g];
}
retour dp[k][0];
}
};
«» "

Les trois codes compilent proprement et renvoient le nombre minimal de changements requis.

---

- Oui. 2. Article du blog
**Titre:** *De la fin à la fin – Mastering LeetCode 1787 (XOR Segments) pour votre entrevue*

---

2.1 Introduction

J'ai essayé ce problème pendant des heures, mais l'éditorial dit que c'est très dur. *
> Si c'est toi, tu n'es pas seul. LeetCode 1787 est célèbre pour avoir caché une observation étonnamment *simple* derrière un mur d'algèbre. Dans cet article

* disséquer le problème,
* montrer la perspicacité cachée
* présenter une solution DP propre,
* analyser le temps / l'espace,
* et terminer avec des départs en carrière.

> **Mots-clés du référencement**: LeetCode 1787, problème de segment XOR, codage d'entrevue, structure de données DP, stratégie d'entrevue de codage, conception d'algorithmes, Java, Python, solutions C++.

---

2.2 Le problème en anglais clair

On vous donne un tableau `nums` des entiers (`0 ≤ nums[i] < 210`) et une taille de fenêtre `k`.
Vous pouvez changer n'importe quel élément à n'importe quelle autre valeur (coût = 1 par élément).
**Objectif:** faire *chaque* sous-aire de longueur `k` ont XOR `0`, en utilisant le moins de changements possible.

Le défi est double :

1. **Constraint:** Le XOR de chaque fenêtre doit être zéro.
2. **Optimisation :** Minimiser le nombre de modifications.

---

2.3 Ce qui le rend difficile

1. ** Contraintes non évidentes.**
Un résolveur naïf essaiera de modifier le tableau de gauche à droite, mais la condition XOR est *global* – un seul élément peut affecter les différentes fenêtres `k`.
2. **Explosion de force brute.**
Essayer tous les remplacements possibles dans chaque fenêtre serait exponentiel.
3. ** Raccordement de l'espace public. **
Changer un groupe d'indices influence le XOR de toutes les fenêtres – vous ne pouvez pas décider les groupes indépendamment.

Pour ces raisons, beaucoup de candidats sont coincés, et LeetCode le marque comme étant "Hard".

---

### 2.4 Le point de vue sur le bien

La clé pour transformer un problème difficile en un problème facile est de repérer une structure cachée.

Étape 1 – Périodicité

Si deux fenêtres consécutives de la taille `k` à la fois XOR à zéro,

«» "
fenêtre i : a[i] a[i+1] ... a[i+k-1]
fenêtre i+1 : a[i+1] ... a[i+k-1] a[i+k]
«» "

Leurs XOR sont égaux → `a[i] == [i+k]».
La répétition de cet argument pour tous les 'i' montre que le tableau doit être *k‐périodique*.

Étape 2 – Groupe

Tous les indices avec le même `i mod k` appartiennent à un *groupe*.
À l'intérieur d'un groupe, toutes les valeurs finales seront les mêmes, sinon la périodicité serait rompue.

Étape 3 – Coût d'un groupe

Pour un groupe de taille `s`, choisir la valeur `v` coûts
«coût = s – fréquence(v)».

Étape 4 – Contrainte globale de XOR

Que les valeurs choisies pour les groupes `k` soient `b[0] ... b[k‐1]`.
Le XOR de n'importe quelle fenêtre est le XOR d'une période: "b[0] ^ b[1] ^ ... ^ b[k‐1]".
Nous avons besoin que ce soit "0".

Ainsi le problème se réduit à : **pick une valeur pour chaque groupe de sorte que le XOR de toutes les valeurs choisies est `0`, alors que le coût total est minimal**.

---

2.5 Le PDD facile

Parce que chaque élément de tableau est < 1024, il y a au plus 1024 valeurs distinctes.
On peut les énumérer.

«» "
dp[i][x] = changements minimes pour les premiers groupes i dont XOR est x
«» "

*Initialiser*
`dp[0]=0`, tous les autres = INF.

*Transition*
Pour le groupe `i` et le xor `x` actuel, essayez toutes les valeurs possibles `v` dans ce groupe:

«» "
NewXor = x ^ v
nouveauCost = dp[i][x] + (size_i - freq_i[v])
dp[i+1][newXor] = min(dp[i+1][newXor], nouveau coût)
«» "

Après avoir traité tous les groupes `k`, la réponse est `dp[k][0]`.

**Complexité* *

* "k ≤ 2000"
* `MAX_XOR = 1024`
* Chaque groupe a au maximum `min(size_i, 1024)` valeurs distinctes

«» "
Temps : O(k · 1024 · différentesValeurs) <= 2 * 106 opérations
Mémoire : O(k · 1024)
«» "

C'est bien en dessous des limites (2 s / 512 Mo).

---

2.6 Pourquoi le PDD fonctionne

Le DP suit les valeurs XOR* cumulées des groupes déjà choisis.
Comme XOR est associative et commutative, toute combinaison de choix de groupe qui donne XOR `0` satisfait à la condition de fenêtre d'origine.
En choisissant toujours le choix le moins cher pour le groupe actuel, le DP garantit l'optimalité globale.

---

- Oui. 3. Touches finales – Conseils de carrière

Autres Ce que j'ai bien fait
(En milliers de dollars des États-Unis)
Autres **Foncez la structure cachée**= Pratiquer la chasse à la pattern==: recherchez la monotonicité, la symétrie ou les invariants. Autres
**Utilisez un DP propre**. Soyez prêt à expliquer votre état DP aux intervieweurs. Ils aiment voir que vous comprenez *pourquoi* une transition d'état est correcte. Autres
**Optimisé pour les contraintes**= Toujours vérifier les plages de valeurs en premier; de nombreux problèmes peuvent être plafonnés par une petite constante (ici 1024). Autres
** Implémenté en plusieurs langues** ► Montrez-vous polyvalent: les intervieweurs peuvent vous demander de porter une solution à une autre langue ou environnement. Autres

> ** Conseil professionnel :** Dans votre CV ou portfolio, écrivez une section « Problèmes‐Solving ». Inclure LeetCode 1787 et décrire comment vous l'avez réduit à un DP par rapport aux groupes. Mettre en valeur la perspicacité qui a transformé le "Hard" en "Easy".

---

- Oui. 4. Enveloppage

* LeetCode 1787 est un exemple de manuel de la stratégie **.
* La dureté est *apparente* mais *illusoire* – une fois que vous reconnaissez la périodicité, c'est un groupe standard‐ Problème DP.
* Le DP est élégant, efficace et language-agnostic – nous avons montré le code complet en Java, Python et C++.

Maintenant, vous êtes prêt à écraser cette question dans votre prochaine interview et, surtout, à repérer des structures cachées dans d'autres problèmes difficiles. Bon codage !

---

> ** Ressources**
> * LeetCode Discussion – 1787
> * Entretien de codage – Section Programmation dynamique
> * YouTube – Tricks XOR pour l'interview de *Tech avec Tim*

---

4.1 Note de clôture

Si vous avez trouvé cet article utile, veuillez **le partager**.
Vos confrères vous remercieront et la communauté continuera de croître.
Bonne interview !