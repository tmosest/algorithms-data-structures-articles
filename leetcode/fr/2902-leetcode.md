---
titre: LeetCode 2902. Nombre de sous-multisets avec somme fixée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2902. Nombre de sous-multisets avec somme
*LeetCode – Hard – Programmation dynamique – Knapsack*

Code
- Oui.
*; <br/><br/> solution de classe {<br/> int final statique privé MOD = 1_000_000_007;<br/><br/> nombre d'int publics Sous-multisets(List<Integer> nombres, int l, int r) {<br/> // Compter la fréquence de chaque valeur (clé multiset).<br/> TreeMap<Integer, Integer> freqMap = new TreeMap<>();<br/> pour (int x : nums) {<br/> freqMap.merge(x, 1, Integer::sum);<br/> }<br/><br/> // 2="Ray DP – façons d'atteindre chaque somme (0 ... r).<br/> long[] dp = new long[r + 1];<br/> dp[0] = 1; // multiset vide<br/><br/> pour (Map.Entry<Integer, Integer> e : freqMap.entrySet() {<br/> int val = e.getKey();<br/> int cnt = e.getValue();<br/><br/> Cas particulier – valeur zéro (ne change pas la somme).<br/> si (val=0) {<br/> long mul = (long) cnt + 1; // chaque zéro peut être pris 0..cnt fois<br/> pour (int i = 0; i <= r; ++i) dp[i] = (dp[i] * mul) % MOD;<br/> continuer;<br/> }<br/><br/> Construire des montants préfixés pour la valeur courante.<br/> long[] pref = nouveau long[r + 1];<br/> pref[0] = dp[0];<br/> pour (int i = 1; i <= r; ++i) {<br/> pref[i] = pref[i - 1];<br/> si (i >= val) {<br/> pref[i] += si (pref[i] >= MOD) pref[i] -= MOD;<br/> }<br/> }<br/><br/> // Mettre à jour dp en utilisant l'astuce de la fenêtre coulissante.<br/> pour (int i = r; i >= 0; --i) {<br/> total long = pref[i];<br/> int j = i - (cnt + 1) * val;<br/> si (j >= 0) {<br/> total -= pref[j];<br/> si (total < 0) total += MOD;<br/> }<br/> dp[i] = total;<br/> }<br/> }<br/><br/> Sommer les réponses dans l'intervalle [l, r].<br/> long ans = 0;<br/> pour (int i = l; i <= r; ++i) {<br/> ans += dp[i];<br/> si (ans >= MOD) ans -= MOD;<br/> }<br/> retour (int) ans;<br/> }<br/>}</code></pre></details> Autres

Code
- Oui.
**Python**= <details><sommaire>Cliquez pour agrandir</sommaire><pre><classe de code===python>> Importations provenant des collections <br/><br/><br/>MOD = 1_000_000_007<br/><br/><br/><br/><br/><br/><br/><br/> <p><br/><br/><br/><br/> <p><br/><br/><br/><br/> <p><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>< pref[i - val]<br/> si pref[i] >= MOD:<br/> pref[i] -= MOD<br/> # update dp en utilisant la fenêtre coulissante\n pour i dans l'intervalle(r, -1, -1):<br/> total = pref[i]<br/> j = i - (cnt + 1) * val<br/> si j >= 0:<br/> total -= pref[j]<br/> si total < 0:<br/> total += MOD<br/> dp[i] = total<br/><br/> somme de retour(dp[l:r+1]) % MOD</code></pre></details> Autres

Code
- Oui.
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/> si (pref[i] >= MOD) pref[i] -= MOD;<br/> }<br/> }<br/><br/>> pour (int i = r; i >= 0; --i) {<br/> long total = pref[i];<br/> int j = i - (c + 1) * val;<br/> si (j >= 0) {<br/> total -= pref[j];<br/> si (total etlt; 0) total += MOD;<br/> }<br/> dp[i] = total;<br/> }<br/><br/> long ans = 0;<br/> pour (int i = l; i <= r; ++i) {<br/> ans += dp[i];<br/> si (ans etgt;= MOD) ans -= MOD;<br/> Autres

---

## Article du blog : Le bon, le mauvais et le mauvais code 2902

> **Désignation de la Méta (155 caractères):**
> Apprenez à cracher le LeetCode 2902 – Compte des sous-multisets avec somme bouchée. Guide PDD étape par étape, pièges et explications prêtes à l'entrevue.

---

- Oui. 1. Récapitulation des problèmes
On vous donne un tableau «nums» (non négatif, longueur ≤ 20 000, somme totale ≤ 20 000) et une fourchette «[l, r]».
**Objectif:** Compter le nombre de *sous-multisets* (choisir chaque élément 0–"compte(x)" fois) ayant une somme à l'intérieur de cette plage.
Toutes les réponses doivent être retournées modulo `1 000 000 007`.

> **Pourquoi c'est important:**
> Il s'agit d'un problème classique *knapsack-like* DP qui apparaît souvent dans les interviews seniors de software-engineer parce qu'il teste le comptage **combination** et la compression **état**.

---

- Oui. 2. Contraintes qui révèlent la voie à suivre

Aperçu
C'est pas vrai.
Les valeurs `nums` sont **multiset-like** (duplicates permises) Autres
Autres Somme de tous les nombres ≤ 20 000 La dimension DP peut être limitée par « r », de sorte que l'espace d'état est au plus 20 001. Autres
"nums" contient **0** comme valeur possible.Zero n'affecte pas la somme, mais il double le nombre de combinaisons valides. Autres

---

- Oui. 2. Pourquoi la Force Brute fait défaut
Il est impossible d'essayer tous les sous-ensembles 2^n (`n` = 20 000).
Même générer tous les sous-multisets *distinct* avec une boucle combinatoire explose encore.
La principale observation: **Nous ne nous soucions que du *somme* d'un multiset, pas de la composition exacte**. Cela invite à une programmation dynamique.

---

- Oui. 3. The Classic DP: 0/1 Knapsack revisité
Si chaque élément pouvait être utilisé au maximum une fois, le problème serait un knapsack 0/1 classique:

Texte
dp[s] = nombre de moyens d'atteindre la somme s
pour chaque élément x:
pour s de r à x:
dp[s] += dp[s-x]
«» "

Mais dans notre cas, chaque valeur peut apparaître *jusqu'à * "cnt(value)" fois.
Nous pouvons traiter chaque valeur comme une ressource *bounded*.

---

- Oui. 4. Optimisation avec les montants préfixés (Fenêtre coulissante)

##### 4.1. Idée de fenêtre coulissante
Pour une valeur fixe `v` qui apparaît `c` fois, le nouveau `dp[s]` après examen de "v" est:

«» "
dp_new[s] = ↓_{k=0..c} dp_old[s - k*v] (si s-k*v ≥ 0)
«» "

Une mise en œuvre naïve aurait besoin de "O(c)" travail pour chaque `s`, qui est encore lourd.

##### 4.2. Trick préfixe-sum
Définissez `pref[s] = ↓_{t=0.s} dp_old[t]` **avec sauts de taille "v"**:

«» "
pref[s] = pref[s-1] + (s>=v ? pref[s-v] : 0)
«» "

Puis la somme de la fenêtre ci-dessus devient:

«» "
dp_new[s] = pref[s] - pref[s-(c+1)*v] (prendre soin de l'indice négatif)
«» "

Parce que "préf[s]" agrége déjà les termes requis, nous pouvons calculer chaque `dp_new[s]` dans **O(1)** après avoir construit `pref` une fois.

Oui. Pourquoi c'est plus rapide
- Le bâtiment `pref` est `O(r)` par valeur distincte.
- Mise à jour `dp` est aussi `O(r)` (une boucle inversée).
- La complexité totale est < < O(D * r) > > où < < D > > est le nombre de valeurs distinctes ( < < 20 001 > > ).
Avec les contraintes, ceci est confortablement inférieur à 1 seconde en Java/Python/C++.

---

- Oui. 5. Des affaires de bord qui vous emportent

Pourquoi c'est important Comment nous le traitons
- - - - - - - - - - Non.
"val". 0 '''Zero ne change pas la somme mais multiplie le nombre de combinaisons valides. Multipliez tous les `dp[s]` par `(cnt + 1)` modulo `MOD`. Autres
"l" == Le multiset vide est toujours un candidat valide. Autres
La fenêtre coulissante peut dépasser `r`. Autres
Débordement de Modulo.Les sommes de préfixe peuvent dépasser les « MOD ». Autres

---

- Oui. 6. Code-Walkthrough (Java)

"Java
pour (Map.Entry<Integer, Integer> e : freqMap.entrySet() {
int val = e.getKey();
int cnt = e.getValue();

si (val) 0) {/ Cas spécial zéro
long mul = (long) cnt + 1;
pour (int i = 0; i <= r; ++i)
dp[i] = (dp[i] * mul) % MOD;
poursuivre;
}

// Construire des montants préfixés
long[] pref = nouveau long[r + 1];
pref[0] = dp[0];
pour (int i = 1; i <= r; ++i) {
pref[i] = pref[i-1];
si (i >= valeur) {
(a) et (b) b) Préf[i - val];
si (préf[i] >= MOD) pref[i] -= MOD;
}
}

// Mise à jour de la fenêtre coulissante
pour (int i = r; i >= 0; --i) {
total long = pref[i];
int j = i - (cnt + 1) * valeur;
si (j >= 0) {
total -= pref[j];
si (total < 0) total += MOD;
}
dp[i] = total;
}
}
«» "

> **Pourquoi le tableau "pref" est important:* *
> `pref[i]` est essentiellement le nombre cumulatif* de moyens d'atteindre toute somme qui se termine par `i`. La soustraction d'un "pref" antérieur donne une fenêtre limitée de taille `(cnt+1)*val`.

---

- Oui. 7. Complexité

**Langue******Heure******Espace**
- C'est quoi ?
Java / Python / C++ () **O(D · r)** () 4 × 108 opérations dans le pire des cas, mais chaque boucle intérieure est légère)

Parce que `r` ≤ 20 000, l'algorithme s'inscrit facilement dans la limite de 2 secondes de LeetCode et la plupart des intervieweurs d'interviews.

---

- Oui. 8. Pièges communs à éviter

Ce qui arrive
- C'est quoi ?
Autres Oublier l'ordre *trié* de valeurs distinctes La logique de la somme préfixe repose sur l'ajout de sauts d'une `val` fixe. Le mixage des commandes peut faire double comptage. "sorted(freq.items()" (Java) / "trié(frek)" (Python)
Défaut de manipulation du modulo pendant la soustraction. Ajouter `MOD` si le résultat est négatif. Autres
Autres Ignorer l'élément zéro : Ne pas multiplier tous les « dp[s] » par « (cnt+1) » produit un sous-compte. Explicite `si (val == 0)` bloc. Autres
En utilisant un tableau DP basé sur 1 mais itérant de `r` vers le bas à `0` incorrectement. avant d'accéder à "pref[j]". Autres

---

- Oui. 9. En parler dans une entrevue

1. **Déclarer les observations**
Le tableau est un multiset – les duplicatas sont autorisés, donc nous ne nous soucions que de la valeur et de son nombre.

2. **Exposer le DP naïf**
*=Nous gardions un tableau DP `dp[sum]`. Pour chaque valeur distincte `v` qui apparaît `c` fois, nous ajouterions `dp[sum - k*v]` pour `k=0...c`. C'est un knapsack limité.

3. **Afficher le goulot d'étranglement de la performance**
*=Si nous tournons naïvement sur `k`, la boucle intérieure devient `O(c·r)`. Avec jusqu'à 20 000 valeurs distinctes, cela est invraisemblable.

4. **Introduire l'optimisation du préfixe-sum**
En construisant une somme préfixe où nous passons par `v`, nous pouvons faire tomber la somme intérieure dans une mise à jour O(1) en utilisant une fenêtre coulissante.

5. **Cas de bord à la main* *
*Les valeurs de zéro sont spéciales : elles ne changent pas la somme, mais chaque zéro peut être utilisé 0...c fois – efficacement un multiplicateur.

6. **Finir avec complexité* *
Dans l'ensemble, temps O(D·r) et espace O(r), qui passe les contraintes.

---

10 ans. A emporter

- **Bien:** Le problème est une variante bien délimitée avec une solution DP claire.
- **Bad:** La mise en œuvre naïve est trop lente; vous devez reconnaître la nécessité d'optimiser.
- **Ugly:** Ignorer le cas `0` ou mal gérer le modulo vous donnera WA ou TLE.

Avec les extraits de code ci-dessus dans votre boîte à outils et le script d'entrevue prêt, vous allez transformer le LeetCode 2902 d'un défi dur en une victoire de confiance. Bon codage !