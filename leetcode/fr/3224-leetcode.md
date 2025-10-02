---
titre: LeetCode 3224. Changements au minimum pour faire des différences égales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**LeetCode 3224 – Moyen**
[Lien vers le problème](https://leetcode.com/problèmes/minimum-array-changes-to-make-différences-equal/)

> **Input**
> * "nums" – tableau de longueur *n* (même, 2 ≤ *n* ≤ 105)
> * `k` – entier (0 ≤ nums[i] ≤ k ≤ 105)
> **Objectif**
> Remplacer tous les éléments (chaque coût de remplacement 1) par une valeur de **0...k** de sorte que
> il existe un entier **X** satisfaisant
> `abs(nums[i] - nombres[n‐i‐1]) == X` pour tous `0 ≤ i < n`.
> Retourner le nombre minimum de remplacements requis.

---

## ----------

Pensez au tableau comme `n/2` *paires* – l'élément i‐th et son miroir `n‐1‐i'.
Pour une différence de cible fixe **X** chaque paire peut être transformée avec **0, 1 ou 2** modifications:

Changements nécessaires Condition sur la paire
-- -- -- -- -- --
Autres La différence actuelle est déjà égale à
Autres Nous pouvons changer **un** élément de la paire pour atteindre la différence **X**
Autres Nous devons changer les deux

Donc, si nous pouvons compter pour chaque possible **X**:

* combien de paires ont déjà des différences **X** (0 changements)
* combien de paires besoin **2** changements (si **X** est trop grand)
* le reste nécessite exactement **1** changement

nous pouvons calculer le coût total pour chaque **X** et choisir le minimum.

---

C'est pas vrai. Observation-clé – Le «Cut‐off» pour un changement

Laissez la paire contenir `a ≤ b`.
Changer **a** pour obtenir la différence **X** est possible sif `X ≤ b` (set `a' = b – X`).
Changer **b** est possible sif `X ≤ k – a` (set `b' = a + X`).

Par conséquent, **un changement** suffit pour tous "X" dans

«» "
0 ... max(b, k – a)
«» "

Si `X` dépasse cette limite, nous devons changer **les deux** nombres → 2 changements.

Définir

«» "
maxSingle = max(b, k – a)
«» "

Pour chaque paire, nous enregistrerons `maxSingle + 1` comme le premier `X` qui force 2 change.
Avec un tableau *différence* nous pouvons agréger ceci pour toutes les paires en **O(n + k)** temps.

---

Algorithme (O(n + k) temps, O(k) espace)

Texte
paires = n / 2
diffCount[X] = combien de paires ont déjà la différence X (0-changement)
deuxModification[i] = nombre de paires qui nécessitent 2 changements lorsque la cible X = Les
«» "

1. **Scan toutes les paires**
*Let a = min(nums[i], nombres[n‐1‐i]), b = max(nums[i], nombres[n‐1‐i]). *
* `d0 = b – a` → `diffCount[d0]++`
* `maxSingle = max(b, k – a)`
* si `maxSingle < k` alors `deux Changement[maxSimple + 1]++»
(c'est le premier X qui nécessite 2 changements pour cette paire)
2. **Préfixer la somme sur "deux changements"**
`pour i = 1 ... k: deuxChange[i] += deuxChange[i‐1] "
Après cela, `twoChange[X]` nous indique combien de paires nécessitent 2 modifications pour
une différence de cible **X**.
3. ** Évaluer chaque X (0 ... k)**
«» "
coût(X) = 2 * deux paires de changements[X] //
+ (paires – diffCount[X] – deux paires de changements[X]) // 1‐changement
«» "
4. **Rendre le moindre coût. **

Toutes les opérations sont entières – parfaites pour le codage des entrevues.

---

La complexité

Aspect
C'est pas vrai.
**Temps**="O(n + k)` – une passe linéaire sur les paires + une passe linéaire sur tous les "X". Autres
**Space**="O(k)` – tableaux de longueur `k+1`. La carte de hachage pour `diffCount` est au plus des entrées `k`. Autres

Avec "k ≤ 105", cela s'inscrit dans les limites des trois langues principales.

---

- Oui. Code – Trois langues

Ci-dessous vous trouverez l'implémentation exacte dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même logique décrite ci-dessus.

---

Java

"Java
Importation de java.util.*;

solution de classe {
Int public int minChanges(int[] nums, int k) {
int n = longueur nums;
paires d'int = n / 2;
int[] diffCount = nouvelle int[k + 1]; // 0-change map (il fonctionne pour 0...k)
int[] twoChange = nouveau int[k + 2]; // tableau de différence

pour (int i = 0; i < paires; i++) {
int a = Math.min(nums[i], nombres[n - 1 - i]);
int b = Math.max(nums[i], nombres[n - 1 - i]);

int d0 = b - a; // 0 changements
diff Nombre[d0]++;

Int maxSingle = Math.max(b, k - a); // X ≤ maxSingle → 1 changement
si (maxSingle < k) { // X > k ne peut pas se produire
deuxModification[maxSingle + 1]++; // premier X qui force 2 changements
}
}

// la somme du préfixe pour obtenir le nombre exact de paires de 2 changements pour chaque X
pour (int i = 1; i <= k; i++) {
deuxChange[i] += Deux changements[i - 1];
}

int best = entier.MAX_VALUE;
pour (int X = 0; X <= k; X++) {
int deux = deux Changement [X];
int zéro = diffCount[X];
int un = paires - zéro - deux;
coût int = deux * 2 + un; // 2-change + 1-change paires
best = Math.min (best, cost);
}
le meilleur retour;
}
}
«» "

---

Python

'`python
Solution de classe:
def minChanges(self, nombres: List[int], k: int) -> Int:
n = len(nums)
paires = n // 2
diff_cnt = [0] * (k + 1) # nombre de changement zéro
deux = [0] * (k + 2) # tableau de différence pour 2-changement

pour i dans la plage (paires):
a, b = triés((nums[i], nombres[n - 1 - i])
diff_cnt[b - a] += 1

max_single = max(b, k - a)
si max_simple < k:
deux[max_simple + 1] += 1 # premier X qui nécessite 2 changements

# Préfixe la somme
pour i dans la plage (1, k + 1):
Deux[i] += Deux [i - 1]

meilleure = n
pour X dans la plage (k + 1):
t = deux[X]
z = diff_cnt[X]
Coût = t * 2 + (paires - z - t) # 2 + 1 + 0 variations
best = min (best, coût)

le meilleur retour
«» "

---

C++

'`cpp
solution de classe {
public:
int minChanges(vector<int>& nums, int k) {
int n = nombres.size();
paires d'int = n / 2;
vectorielle<int> diffCnt(k + 1, 0); nombres de changement // 0
vector<int> deux(k + 2, 0); tableau // diff pour 2-changement

pour (int i = 0; i < paires; ++i) {
Int a = min(nums[i], nombres[n - 1 - i]);
b = max(nums[i], nombres[n - 1 - i]);

diffCnt[b - a]++; // 0 modifications

int maxSingle = max(b, k - a); // 1 changement jusqu'à ce X
si (maxSingle < k) // X > k n ' a jamais été nécessaire
deux[maxSingle + 1]++; // premier X forçant 2 changements
}

// prefix sum → nombre de paires de 2 changements pour chaque X
pour (int i = 1; i <= k; ++i) deux[i] += deux [i - 1];

int best = n; // pire cas
pour (int X = 0; X <= k; ++X) {
l'élément 2Cnt = deux[X];
Int 0 Cnt = diffCnt[X];
coût int = deux Cnt * 2 + (paires - zéroCnt - deuxCnt);
best = min (best, coût);
}
le meilleur retour;
}
};
«» "

---

Résumé de la complexité

Étape
C'est quoi ?
Paire de scan Autres
"O(k)" Autres
Dernière boucle Autres
**Total**

Tant **temps** que **mémoire** satisfont facilement aux limites de "n, k ≤ 105".

---

## # # # # # # # , # , # , # , # , # , # , # , #

C'est bien C'est mal
C'est quoi ?
**Algorithme linéaire** – évite la naïve O(n k) DP qui serait time-out. **En utilisant la récursion avec mémoisation** pour chaque paire et X est un *got-cha* – la profondeur de la pile va exploser. Autres
Autres **Expliquement piste 0-changement, 1-changement, 2-changement nombres** – clair et testable. **Ne mélangez pas la logique de préfixe à deux changements avec la carte de 0 changement** – le paramètre off-by-one du tableau de différence est subtil. Autres
**Utilisation `Math.min`/`Math.max` Une seule fois par paire** – garde le code lisible. **N'oubliez pas** que `maxSingle` peut être exactement `k`; ajouter `maxSingle+1` déborderait. Autres

---

C'est pas vrai. Pourquoi cela compte pour les entrevues

1. ** Compétence en résolution des problèmes** – Affiche que vous pouvez décomposer un problème dans des états indépendants.
2. ** intuition algorithmique** – L'idée "coup‐off" est un modèle soigné et réutilisable pour de nombreuses questions "minimaux-coût‐transform".
3. ** Sensibilisation au rendement** – Vous serez loué pour une solution **O(n + k)** au lieu d'une solution de force brute.

---

## #= 8=1 SEO & Job‐Interview Friendly Meta

- **Mots-clés**: *Codeleet 3224*, *changements minimums de tableau*, *différence d'arrachage*, *codage de l'entrevue*, *algorithme d'entrevue d'emploi*, *O(n + k) solution*, *C++*, *Java*, *Python*.
- **Description détaillée**: *Solve LeetCode 3224 : Changements mineurs pour faire des différences égales en O(n + k). Une explication complète, un algorithme intuitif et des extraits de code Java/Python/C++ – parfaits pour votre prochaine interview de codage. *
- **Chefs**: H1 – Problème, H2 – Insight, H3 – Algorithme, H4 – Complexité, H2 – Échantillons de codes, H3 – Java, H3 – Python, H3 – C++.

---

Exemple de résumé favorable au candidat

J'ai abordé LeetCode 3224 en traitant le tableau comme des paires de miroirs.
> J'ai calculé pour chaque paire le plus grand seuil de changement unique et j'ai utilisé
> préfixer la somme pour compter le nombre de paires de 2 changements pour chaque cible `X`.
> Cela a conduit à un algorithme O(n + k) que j'ai écrit en Java, Python et C++.
> Le coût final pour chaque `X` est une formule simple impliquant le nombre de changements 0/1/2.

Vous pouvez adapter cela à votre style – ajouter un peu de style personnel, mais garder le noyau technique intact.

---

Bon codage, et bonne chance avec votre interview! C'est ce qu'il a dit.

---