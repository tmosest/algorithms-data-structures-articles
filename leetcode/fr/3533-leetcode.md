---
titre: LeetCode 3533. Divisibilité concaténée - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# C'est une plongée profonde (Java-Python C++)
> *Maîtrisez ce LeetCode Dur en 30 min → Débarrassez votre rôle d'ingénierie logicielle de rêve. *

---

- Oui. 1. Exposé des problèmes

> On vous donne un tableau "nums" de **positif** entiers (taille ≤ 13) et un entier positif `k` (= 100).
> Une *permutation* de "nums" est censée former une concaténation **divisible** si le nombre obtenu en concatérant la représentation décimale des entiers dans cet ordre est divisible par "k".
> **Retourner la permutation laxicographiquement la plus petite** qui satisfait à la condition.
> Si aucune telle permutation n'existe, retournez une liste vide.

**Exemples**

Résultats
C'est pas vrai.
[3,12,45]
[10,5]
[1,2,3]

---

- Oui. 2. Pourquoi est-ce difficile?

* L'approche naïve énumère toutes les permutations `n!` → impossibles même pour `n = 13`.
* Concaténer les numéros et vérifier la disvisibilité déborderait `int64` pour de nombreux cas.
* Nous devons garder une trace de **remainder modulo k** alors que nous construisons la concaténation.
* Nous avons également besoin de l'ordre **lexicographiquement plus petit** valide – c'est une optimisation supplémentaire.

La solution standard est un **DP + Bitmask** avec récursion + mémorisation – exactement le modèle utilisé pour les problèmes de type "Traveling Salesman" mais avec un état restant.

---

- Oui. 3. Idées de haut niveau

1. **État**
* `masque` – bitmasque des nombres qui ont déjà été placés.
* `rem` – reste du nombre formé jusqu'à présent, modulo `k`.

2. **Transition**
Pour chaque nombre inutilisé `x`:
* Calculer `len(x)` – nombre de chiffres décimaux de `x`.
* Calculer `pow10[len(x)] % k` une fois au début.
* Nouveau reste :
Texte
NewRem = (rem * pow10[len(x)] + x) % k
«» "
* Récursez sur `masque' (1<<idx)` et `newRem`.

3. **Base**
Quand tous les bits sont définis (`masque == all`):
* Si "rem". 0` → une permutation valide, retourner la liste vide.
* Sinon → impossible, retourner `null`.

4. ** Minimisation lexicographique* *
Dans la récursion, les nombres d'itération ** triés dans l'ordre ascendant**.
Dès qu'on trouve un enfant *valide*, on prélève le nombre actuel à sa solution et on s'arrête – car le premier succès sera le plus petit lexicographiquement (puisque nous avons essayé les nombres en ordre ascendant).

5. **Mémoisation**
Conservez les résultats dans une `Map<Long, List<Integer>>` ou un tableau 2-D `dp[masque][rem]` pour éviter la recomputation.
Clé = `(masque << 7)=" rem` (puisque `k ≤ 100`, 7 bits suffisent).

---

- Oui. 4. Mise en œuvre du code

Voici des solutions propres et autonomes dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même logique DP-masque, de sorte que vous pouvez choisir votre langue préférée pour l'entrevue.

> **Astuce** – Afficher ce code sur votre GitHub ou dans un dossier `leetcode_solution`. Les recruteurs adorent les snipets propres et vérifiables.

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {

// ----------------------------------------------------------------------
// API publique requise par LeetCode
// ----------------------------------------------------------------------
public int[] concaténatedDivisibilité(int[] nombres, int k) {
int n = longueur nums;
Total Masque = (1 << n) - 1;

// Précalculer 10^len(x) % k pour chaque nombre
int[] pow10Mod = nouvelle int[n];
pour (int i = 0; i < n; i++) {
int len = numDigits(nums[i]);
pow10Mod[i] = modPow10(len, k);
}

// Trier une fois – assure que nous essayons les candidats dans l'ordre croissant
int[][] indexé = nouveau int[n][2]; // {original Indice, valeur}
pour (int i = 0; i < n; i++) indexé[i] = nouveau int[]{i, nombres[i]};
les tableaux.sort(indexé, Comparateur.comparingInt(a -> a[1]);

// Memo table: masque → rem → solution
Liste <entier>[] mémo = nouvelle liste[1 << n][k];
Liste<entier> meilleur = dfs(0, 0, total Masque, k, nombres, pow10Mod, indexé, mémo);

si (meilleur == null) retourne une nouvelle int[0];
int[] ans = nouveau int[best.size()];
pour (int i = 0; i < best.size(); i++) ans[i] = best.get(i);
le retour des an;
}

// ----------------------------------------------------------------------
// DP récursif avec mémoisation
// ----------------------------------------------------------------------
Liste privée<entier> dfs(int masque, int rem,
Total Masque, int k,
les nombres,
Int[] pow10Mod,
int[][] indexé,
Liste<entier>[[][] note de service) {

si (masque == totalmasque) { // tous les nombres placés
return rem == 0 ? new ArrayList<>() : null;
}
si [memo[masque][rem] != null) retourner mémo[masque[rem];

Liste<entier> réponse = nul;

// Essayez chaque nombre inutilisé en ordre croissant
pour (int[] pair : indexé) {
int idx = paire[0], val = paire[1];
si ((masque & (1 << idx)) != 0) continuer; // déjà utilisé

int newRem = (int)((rem * (long)pow10Mod[idx] + val) % k);
Liste <Intégrer> enfant = dfs(masque) (1 << idx), newRem,
Total général Masque, k, nums, pow10Mod,
indexé, mémo);
si (enfant != null) { // le premier coup est lexicographiquement le plus petit
child.add(0, val); // nombre courant prépend
réponse = enfant;
pause;
}
}

mémo[masque][rem] = réponse;
réponse de retour;
}

// Utilitaire : nombre de décimales
Int privé numDigits(int x) {
cnt = 0;
pendant (x > 0) { cnt++; x /= 10; }
retour cnt;
}

// 10^len % k – calculé par multiplication répétée
Int privé modPow10(int len, int k) {
long p = 1 % k;
pour (int i = 0; i < len; i++) p = (p * 10) % k;
retour (int)p;
}
}
«» "

---

4.2 Python

'`python
Solution de classe:
def concatenatedDivisibilité(même, nombres: List[int], k: int) -> Liste[int]:
n = len(nums)
Total = (1 << n) - 1

# Précalculé (10^len(x)) % k
pow10 = [0] * n
pour i, val dans l'énumération(nombres):
chiffres = len(str(val))
pow10[i] = pow(10, chiffres, k)

# Trier les indices par valeur pour obtenir l'ordre lexicographique
idxs = trié(range(n), clé=lambda i: nombres[i])

mémo: Dict[Tuple[int, int], Facultatif[List[int]]] = {}

def dfs(masque: int, rem: int) -> Facultatif[Liste[int]]:
si masque == total:
retourner [] si rem == 0 autre Aucune
clé = (masque, rem)
si la clé dans le mémo :
retourner mémo[key]

pour i en idx:
si masque & (1 << i): # déjà utilisé
poursuivre
new_rem = (rem * pow10[i] + nums[i]) % k
child = dfs(masque) (1 << i), new_rem)
si l'enfant n'est pas Néant:
mémo[key] = [nums[i]] + enfant
retourner mémo[key]

mémo[key] = Aucun
retour Aucune

res = dfs(0, 0)
retour res si res n'est pas Aucun autre []
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> concaténéDivisibilité(vecteur<int>& nombres, int k) {
int n = nombres.size();
int allMask = (1 << n) - 1;

// Précalculer 10^len(x) % k
vecteur<int> pow10mod(n);
pour (int i = 0; i < n; ++i) {
int len = 0, tmp = nombres[i];
pendant que (tmp) { len++; tmp /= 10; }
long p = 1;
pour (int j = 0; j < len; ++j) p = (p * 10) % k;
pow10mod[i] = (int)p;
}

// Indices de tri pour l'ordre lexicographique
vecteur<int> idx(n);
(idx.begin(), idx.end(), 0);
Tri(idx.begin(), idx.end(),
[&](int a, int b){ nombres de retour[a] < nombres[b]; });

// Tableau DP : mémo[masque][rem] = permutation facultative
vecteur<vector<vector<int>>> mémo(1<n, vecteur<vector<int>>(k));
vecteur<vector<bool>> vis(1<n, vecteur<bool>(k,false));

fonction<vector<int>(int,int)> dfs = [&](int masque, int rem) -> vecteur<int> {
si (masque ) toutmasque) {
return rem == 0 ? vector<int>() : vecteur<int>{-1};
}
si (vis[masque][rem]) retourne le mémo[masque][rem];
vis[masque][rem] = vrai;

pour (int id : idx) {
si (masque et (1<<id)) continuent;
int newRem = (int)((rem * 1LL * pow10mod[id] + nums[id]) % k);
vectorielle<int> enfant = dfs(masque=1<id), newRem;
si (!child.vide() & & enfant[0] != -1) { // trouvé
enfant.insert(child.begin(), nums[id]);
mémo[masque][rem] = enfant;
retour de l'enfant;
}
}
mémo[masque][rem] = vecteur<int>{-1};
retour de mémo[masque][rem];
};

vecteur<int> ans = dfs(0, 0);
si (!ans.vide() && ans[0] == -1) ans.clear(); // aucune solution
le retour des an;
}
};
«» "

> **Pourquoi la sentinelle `-1`? * *
> C'est un drapeau léger qui évite les contrôles "nullptr" en C++.

---

- Oui. 5. Analyse de la complexité

L'espace
C'est quoi ?
** Récursif + Mémo** (toutes les 3 langues) **O( 2n · k · n )** – chaque État vérifie chaque nombre inutilisé.
Pour les opérations `n ≤ 13`, `k ≤ 100`, qui est au maximum `8192 · 100 · 13 ↓ 107` – facilement < 0,1 s sur les processeurs modernes. Autres
**Espace**: `dp[masque][rem]` → `2n · k` états, chacun stockant une liste de `n` ints:
`O( 2n · k · n )` quelques mégaoctets. Autres

*L'astuce triée-premier-succès réduit l'embranchement réel: dès que nous touchons un enfant valide nous arrêtons de boucler, donc en pratique l'algorithme est *linéaire dans le nombre d'états*. *

---

- Oui. 6. Liste de contrôle des cas de bord

Autres Essai Pourquoi c'est important
-- -- -- -- -- --
Autres **Tous les nombres d'un chiffre** – par exemple `[11,22,33]`, `k = 3`= ` `pow10Mod` devient `10 % 3 = 1` → transition simplifie. Autres
Autres **Grands nombres (≥ 109)** – par exemple `[999999999, 123456]` , Nous ne construisons jamais l'entier entier concaténé – seuls les restes sont conservés. Autres
Autres **k = Chaque permutation est valide – la réponse n'est que le tableau trié. Autres
**Aucune solution**S'assurer de retourner `[]` au lieu de `[null]` ou `-1`. Autres
**Les valeurs dupliquées**=Le problème garantit *les entiers distincts*, donc aucune manipulation particulière n'est requise. Autres

---

- Oui. 7. Comment tester

"""
♪ Java
Javac Solution.java
# Python
Python - <<'PY'
de solution d'importation
print(Solution().concatéDivisibilité([3,12,45],5))
PY
Numéro C++
g++ -std=c++17 solution.cpp && ./a.out
«» "

Assurez-vous d'ajouter des tests unitaires pour les trois exemples ci-dessus et quelques cas aléatoires (`random.seed(0)` pour la reproductibilité).

---

- Oui. 8. Foire aux questions d'entrevue

Question Réponse courte
C'est pas vrai.
* Pouvons-nous faire cela sans trier? Oui, mais vous auriez besoin de générer toutes les permutations dans l'ordre lexicographique, ce qui va à l'encontre du but. Le tri est O(n log n) et trivial. Autres
*Et si `k` n'est pas premier? Cela n'a pas d'importance – l'arithmétique modulaire fonctionne pour tout entier `k`. Autres
*Pourquoi ne pas utiliser DP sur le nombre de chiffres au lieu de nombres? Parce que l'espace de l'état exploserait – le nombre de longueurs de chiffres possibles est beaucoup plus grand que le nombre de nombres (`n`). Autres
*Et si les duplicatas étaient autorisés? Vous devriez stocker les nombres de chaque nombre dans le masque; encore faisable mais pas dans ce problème. Autres
*Y a-t-il une solution gourmande? Non – le problème est le NP-hard en général; DP est l'approche standard. Autres

---

- Oui. 9. Comment cette déclaration pose le problème

> *On vous donne un tableau d'entiers distincts `nums` et un entier `k`. Trouvez le plus petit (dans l'ordre lexicographique) tableau qui peut être obtenu en permutant "nums` de sorte que l'entier concaténé est divisible par "k". *

Le DP fourni trouve la permutation **lexicographiquement la plus petite** qui satisfait la contrainte de divisibilité, ou retourne un tableau vide si impossible – exactement ce que le problème exige.

---

- Oui. 9. Pourquoi cela compte pour vous

*Vous avez vu un problème qui à première vue semble comme une recherche de force brute sur toutes les permutations `n!`. Le point de vue clé est de travailler avec **remainders** et d'utiliser **bitmask DP** pour tailler l'espace de recherche de façon spectaculaire. *

Maîtriser ce modèle vous permettra d'aborder toute une classe de problèmes de concaténation et de division, et le code ci-dessus est un modèle prêt à l'emploi que vous pouvez adapter pour les concours d'entrevues.

Bonne chance – maintenant allez clouer cette interview! C'est ce qu'il a dit.

---

*Préparé par : [Votre nom]*
*Date: 2023‐08‐08*