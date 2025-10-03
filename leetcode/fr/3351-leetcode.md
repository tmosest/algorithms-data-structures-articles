---
titre: LeetCode 3351. Somme des bons résultats -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3351 – *Sum of Good Subséquences*
- Oui. Le bon, le mauvais, et l'hugly – Une marche pratique du DP (Java-Python C++)

> **TL;DR** –
> *Une bonne subséquence* est une subséquence où la différence absolue entre chaque paire d'éléments consécutifs est égale à **1**.
> Nous voulons la somme de tous les éléments sur **chaque** bonne séquence.
> La solution classique est une programmation **dynamique** qui fonctionne dans la mémoire **O(n)** et **O(max(nums))**.

> **Mots clés:**
> *LeetCode * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

---

Récapitulation des problèmes

Texte
Entrée : nombres = [1, 2, 1]
Produit : 14
«» "

Bonnes séquences (taille ≥ 1):
- Oui. [1] → somme = 1
- Oui. [2] → somme = 2
- Oui. [1] → somme = 1
- [1,2]→ somme = 3
- [2,1]→ somme = 3
- [1,2,1]→ somme = 4
Total = 14

Contraintes
- "1 ≤ longueur nominale ≤ 10^5"
- `0 ≤ nombres[i] ≤ 10^5`
- Réponse modulo `10^9 + 7`

---

- Oui. Pourquoi la programmation dynamique?

- Chaque sous-séquence de bien se terminant par la valeur `x` ne peut être étendue que par les éléments `x‐1` ou `x+1`.
- Oui. Cette propriété locale nous permet de traiter le tableau une fois, de construire des comptes et des sommes totales par valeur.
- Sans DP, nous devrions énumérer toutes les sous-séquences → 'O(2^n)'.

---

- Oui. L'idée du PDD

Laissez
- `cnt[v]` = **nombre** de produits qui se terminent par la valeur `v`.
- `sum[v]` = **total des éléments** sur tous les bons sous-séquences qui se terminent par la valeur `v`.

Lorsque nous lisons un nouvel élément «a»:

Description Formule de mise à jour Autres
- C'est quoi ?
Démarrer une nouvelle séquence "[a]" 1 séquence "cnt[a] += C'est vrai.
Autres Prolonger la sous-séquence se terminant par `a-1`= Chaque sous-séquence donne une nouvelle sous-séquence `...,(a-1),a`= `cnt[a] += cnt[a-1]` Autres
Extendre la séquence subséquente en se terminant par `a+1` Autres
Autres Mettre à jour les montants de chaque nouvelle séquence nous ajoutons la somme de l'ancienne séquence + le nouvel élément `a` Autres
«sum[a] += sum[a-1] + sum[a+1] + a * (cnt[a-1] + cnt[a+1] + 1)» Autres

Toutes les opérations sont effectuées par modulo `M = 1 000 000 007'.

La réponse est la somme de toutes les valeurs `sum[v]` après l'analyse.

---

## 4-

Problème Qu'est-ce qui peut mal tourner ? Comment garder
- C'est quoi ?
Autres Index hors des limites = `cnt[a-1]` ou `cnt[a+1]` lorsque `a` est 0 ou `MAX_VAL`= Utiliser la taille du tableau `MAX_VAL + 3` et toujours accéder `cnt[a+1]`, `cnt[a+2]`. Autres
Autres Integer déborder "cnt` et `sum` peut dépasser `int`. Autres
Modulo après chaque ajout. Autres
Chaque apparition d'un même nombre doit être traitée indépendamment. Autres

---

C'est pas vrai. Le code

Voici les implémentations **trois** qui suivent la même logique :

*Tous les trois partagent la même complexité: "O(n + max(nums)") temps, "O(max(nums))" mémoire. *

> **Astuce:** Utilisez `int[]` pour l'entrée; tout le levage lourd est fait dans les tableaux `long`.

#### 5.1 Java

"Java
Importation de java.util.*;

classe publique SumOfGoodSubséquences {
finale statique privée longue MOD = 1_000_000_007L;
MAX_VAL = 100_000; // contrainte donnée

la somme d'intérêt public de GoodSubsequences(int[] nums) {
long[] cnt = nouveau long[MAX_VAL + 3]; // +3 pour éviter les contrôles des limites
longue[] somme = nouvelle longue[MAX_VAL + 3];

pour (int a : nombres) {
int idx = a + 1; // quart de +1 pour garder l'index 0 en sécurité

longue cntPrev = cnt[idx - 1]; // a-1
long cntNext = cnt[idx + 1]; // a+1

longue sommePrev = somme[idx - 1];
somme longueSuivant = somme[idx + 1];

longue nouvelle Cnt = (cntPrev + cntNext + 1) % MOD;
long newSum = (sumPrev + sumNext + a * newCnt) % MOD;

cnt[idx] = (cnt[idx] + newCnt) % MOD;
sum[idx] = (sum[idx] + newSum) % MOD;
}

résultat long = 0;
pour (int i = 0; i < somme longueur; i++) {
résultat = (résultat + somme [i]) % MOD;
}
retour (int) résultat;
}

public statique vide principal(String[] args) {
SumOfGoodSubséquences solveur = nouveau SumOfGoodSubséquences();
System.out.println(solver.sumOfGoodSubséquences(nouvelle int[]{1, 2, 1}); // 14
System.out.println(solver.sumOfGoodSubséquences(nouvelle int[]{3, 4, 5})); // 40
}
}
«» "

5.2 Python

'`python
de collections importer par défautdict
de taper l'importation Liste

MOD = 10 ** 9 + 7

Solution de classe:
def sumOfGoodSubsequences(self, nombres: List[int]) -> Int:
cnt = par défautdict(int)
total = par défautdict(int)

pour les nombres:
c_left, c_right = cnt[a - 1], cnt[a + 1]
t_left, t_right = total[a - 1], total[a + 1]

new_cnt = (c_left + c_right + 1) % MOD
new_sum = (t_left + t_right + a * new_cnt) % MOD

cnt[a] = (cnt[a] + nouveau_cnt) % MOD
total[a] = (total[a] + nouveau_somme) % MOD

(total.valeurs()) % MOD

♪ Démo
si __nom__ == "__main__" :
sol = Solution()
print(sol.sumOfGoodSubséquences([1, 2, 1])) # 14
print(sol.sum OfGoodSubséquences([3, 4, 5))) # 40
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nt sumOfGoodSubséquences(vecteur<int>& nums) {
MOD = 1'000'000'007;
const int MAX_VAL = 100000;
vecteur <long> cnt(MAX_VAL + 3, 0);
vecteur <long> somme (MAX_VAL + 3, 0);

pour (int a : nombres) {
int idx = a + 1; // quart de +1
longue c_left = cnt[idx - 1]; // a-1
long c_right = cnt[idx + 1]; // a+1
long t_left = somme[idx - 1];
long t_right = somme[idx + 1];

long long nouveau Cnt = (c_left + c_right + 1) % MOD;
long long newSum = (t_left + t_right + 1LL * a * newCnt) % MOD;

cnt[idx] = (cnt[idx] + newCnt) % MOD;
sum[idx] = (sum[idx] + newSum) % MOD;
}

long an = 0;
pour (auto v : somme) ans = (ans + v) % MOD;
retour (int)ans;
}
};

// Démo
Int main() {
Solution sol;
cout << sol.sum OfGoodSubséquences({1, 2, 1}) << '\n'; // 14
Cout << sol.sum OfGoodSubséquences({3, 4, 5}) << '\n'; // 40
}
«» "

---

Analyse de complexité

Métrique
- C'est quoi ?
Heure (n + MAX_VAL) (n + MAX_VAL) Autres
Mémoire (pour mémoire de 100k) (hash-maps mais effectivement taille du tableau) Autres
Autres Pourquoi `MAX_VAL`? Valeurs jusqu'à `10^5`; nous allouons `100003` slots. L'utilisation de `defaultdict` maintient la mémoire proportionnelle à des valeurs distinctes. Comme Java. Autres

Tous fonctionnent confortablement dans les limites de 1 s et 512 Mo.

---

## 7=" SEO-Ready Blog: "Sum of Good Subsequences – The Good, The Bad & The Ugly"

> *Si vous préparez une entrevue d'ingénierie logicielle, LeetCode 3351 est un problème à résoudre**. Ci-dessous est une plongée profonde qui décompose l'astuce DP, affiche le code Java/Python/C++ propre, et explique chaque écueil auquel vous pourriez faire face. *

7.1 Intro

> Aujourd'hui, nous nous attaquons **LeetCode 3351: Summ of Good Subséquences** – un problème qui teste votre compréhension de la programmation dynamique, de l'arithmétique modulaire et de la manipulation des cas de bord. (en milliers de dollars)

7.2 Le bien

- **Simplicité** – DP avec tableaux est **traightforward** et échelles linéaires.
- **Modularité** – L'algorithme gère naturellement les valeurs répétées et les valeurs de bord `0`/`MAX`.
- **Réutilisabilité** – Le même motif (`cnt` + `sum`) s'applique à de nombreux problèmes de subséquence adjacents (par exemple, les subséquences de style Fibonacci).

### 7.3 La mauvaise

- **Index Off‐by‐One** – L'oubli du déplacement par `+1` conduit à `ArrayIndexOutOfBounds` en Java/C++ ou à un `KeyError` en Python.
- **Overflow** – Utiliser `int` au lieu de `long` en Java ou `int` en C++ provoque des débordements silencieux.
- **Modulo Mis-placement** – Ajouter d'énormes nombres avant de prendre du modulo peut dépasser `64-bit` et donner de mauvaises réponses.

# ### 7.4 Le "Ugly"

- ** Limites** – Quand `a` est `0` ou `100000`, le DP naïf essaie d'accéder `cnt[-1]` ou `cnt[100001]`.
- **Hash-Map Overhead** – Le "defaultdict" de Python est élégant mais peut gâcher la mémoire si de nombreuses valeurs distinctes.
- **Readability vs. Performance** – Trop d'instructions « % MOD » peuvent encombrer le code, mais elles sont essentielles.

7.5 Dernier départ

> LeetCode 3351 n'est pas juste un jouet. Il s'agit d'un micro-cosme de problèmes d'entretien réel où une seule ligne de DP peut transformer un cauchemar exponentiel en algorithme linéaire. Maîtrisez ce modèle et vous acquerrez de nombreuses questions basées sur les subséquences. (en milliers de dollars)

---

Les pensées de clôture

- Le DP ci-dessus est la solution **canonique**; si vous la présentez clairement dans une entrevue, vous montrerez une compréhension profonde de *la définition de l'état*, *la transition* et *l'arithmétique modulaire*.
- Variantes de la pratique: changer `cnt` en `int` et `sum` en `long`, ou utiliser `unordered_map` pour les données rares.
- Gardez à l'esprit l'astuce de +1 : c'est un sauveteur pour la sécurité des frontières dans toutes les langues.

Bonne chance avec votre interview, et que les **bonnes séquences** soient toujours en votre faveur! C'est ce qu'il a dit.

---

*Bon code ! *