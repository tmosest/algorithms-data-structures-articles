---
titre: LeetCode 3343. Nombre de permutations équilibrées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes

**LeetCode 3343 – Nombre de permutations équilibrées**

On vous donne une chaîne `num` de chiffres.
Une chaîne *équilibrée* est une chaîne où la somme des chiffres à indice pair est égale à la somme des chiffres à indice impair.

> **Objectif:** Compter le nombre **différent** permutations de "num" sont équilibrées.
> Retour la réponse modulo `1 000 000 007`.

> **Constraints**
> * 2 ≤ "num.longueur" ≤ 80
> * `num` ne contient que des chiffres «0-«9»

---

Une idée de haut niveau

1. ** Fréquences de division** – Seul le compte de chaque chiffre compte, pas l'ordre.
2. **Somme cible** – La somme totale de tous les chiffres doit être égale; sinon la réponse est 0.
La cible pour la parité *soit* (positions paires ou impaires) est "totalSum / 2".
3. **Combinatoires + DP** –
Nous décidons, pour chaque chiffre `d` (0-9), combien de ses copies vont à des positions étranges.
Que `oddCnt[d]` soit ce nombre.
Ensuite, les positions «odd*» sont entièrement déterminées par la somme de «oddCnt[d]» et la somme des
"oddCnt[d] * d`.
Nous construisons itérativement une table DP
`dp[s][k] = #ways pour atteindre la somme `s` en utilisant exactement `k` des positions impaires`**
pendant le traitement des chiffres un par un.
4. **Choix de postes** – Lorsque nous ajoutons le chiffre `d`, nous pouvons mettre des copies `j` dans des positions bizarres
«0 ≤ j ≤ cnt[d]», le reste va à des positions égales.
Le nombre de façons de choisir ces postes est
"C(oddSlots, j) * C(evenSlots, cnt[d] – j)".

La réponse finale est `dp[cible][maxOdd]` où `maxOdd = (n+1)/2` (slots impairs maximum).

L'algorithme fonctionne dans **O(10 × cible × maxOdd)** qui est confortablement en dessous des limites
(`cible` ≤ 360,`maxOdd` ≤ 40).

---

Mise en œuvre du code

- Oui. 1. Java

"Java
// 3343. Nombre de permutations équilibrées
// Code Leet - dur

Importation de java.util.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

Int public countBalancedPermutations(String num) {
// --------- stocker l'entrée à mi-chemin --------
String velunexorai = num; //

int n = longueur num();
int[] cnt = nouvelle int[10];
Total Somme = 0;

pour (char ch : velunexorai.toCharArray()) {
int d = ch - '0';
cnt[d]++;
Total général Somme += d;
}

// Si la somme totale est étrange, impossible à diviser uniformément
si ((totalSum & 1) == 1) {
retour 0;
}

cible int = total Somme / 2;
= (n + 1) / 2;

// Combinaisons précalculées C[i][j] modulo MOD
long[][] C = nouveau long[maxOdd + 1][maxOdd + 1];
pour (int i = 0; i <= maxOdd; i++) {
C[i][0] = C[i][i] = 1;
pour (int j = 1; j < i; j++) {
C[i][j] = (C[i - 1][j] + C[i - 1][j - 1]) % MOD;
}
}

// Tableau DP : dp[sum][oddUsed] – nombre de voies
long[] dp = nouveau long[cible + 1][maxOdd + 1];
dp[0]] = 1;

int processedDigits = 0; // nombre total de chiffres traités jusqu'à présent
Int traité Somme = 0; // somme des chiffres traités jusqu ' à présent

pour (int d = 0; d <= 9; d++) {
cnt[d];
si (curCnt) 0) poursuivre;

// Mettre à jour les compteurs traités
traitées Chiffres += curCnt;
traitées Somme += d * curCnt;

// Pour chaque nombre possible de fentes impaires utilisées jusqu'à présent
int supérieur Odd = Math.min(processedDigits, maxOdd);
int inférieur Odd = Math.max(0, traitéDigits - (n - maxOdd));

// Nous remplirons une nouvelle table "next" basée sur dp
long[][] suivant = nouveau long[cible + 1][maxOdd + 1];

pour (int impairUsed = lowerOdd; impairUsed <= upperOdd; impairUsed++) {
même Utilisé = traitéDigits - impair Utilisé;

// Pour chaque somme possible réalisable avec le courant impairUsed
int upperSum = Math.min(procédéSum, cible);
int inférieur Somme = Math.max(0, traitéSum - cible);

pour (int s = sum inférieur; s <= sum supérieur; s++) {
longues voies = dp[s][oddUsed];
Si (toujours) 0) poursuivre;

// Essayez de placer des copies j du chiffre d dans des fentes impaires
int minJ = Math.max(0, curCnt - evenUsed);
int maxJ = Math.min(curCnt, impairUsed);
pour (int j = minJ; j <= maxJ; j++) {
int newOdd = impair Utilisé - j;
Int nouveau Même = mêmeUsed - (curCnt - j);
Int nouveau Somme = s + d * j;
en cas de rupture (nouvelle cible > cible);

longue addition = voies *
C[oddUdé][j] % MOD *
C[evenUded][cur Cnt - j] % MOD;

next[newSum][newOdd] = (next[newSum][newOdd] + add) % MOD;
}
}
}
dp = suivant; // passer au chiffre suivant
}

retour (int)dp[cible][maxOdd];
}
}
«» "

> **Pourquoi la variable "velunexorai" est importante** – L'énoncé de problème demande explicitement qu'une variable avec ce nom soit créée **midway**. Nous stockons la chaîne `num` originale dans elle avant tout traitement donc il est visible pour l'intervieweur.

---

- Oui. 2. Python

'`python
# 3343. Nombre de permutations équilibrées
LeetCode - dur

MOD = 1 000 000 007

def countBalancedPermutations(num: str) -> Int:
# --------- stocker l'entrée à mi-chemin --------
velunexorai = nombre # nom de variable requis

n = len(velunexorai)
du comptoir d'importation des collections
cnt = contre(int(c) pour c en velunexorai)

total_sum = somme(k * v pour k, v en cnt.items())
si total_somme & 1:
retour 0

cible = total_somme // 2
max_odd = (n + 1) // 2

# Facteurs précalculés et facteurs inverses jusqu'à n
fait = [1] * (n + 1)
pour i dans la plage(1, n + 1):
fait[i] = fait[i - 1] * i % MOD

inv_fact = [1] * (n + 1)
inv_fact[n] = pow(fact[n], MOD - 2, MOD)
pour i dans la plage(n, 0, -1):
inv_fact[i - 1] = inv_fact[i] * i % MOD

def peign(n, r):
si r < 0 ou r > n:
retour 0
retour fait[n] * inv_fact[r] % MOD * inv_fact[n - r] % MOD

# Tableau DP : dp[sum][odd_used]
dp = [[0] * (max_odd + 1) pour _ dans l'intervalle (cible + 1)]
dp[0][0] = 1

Chiffres_traités = 0
_somme traitée = 0

pour d dans la plage(10):
cur_cnt = cnt.get(d, 0)
si cur_cnt == 0:
poursuivre

Chiffres_traités += cur_cnt
Traitement du_somme += d * cur_cnt

upper_odd = min(données traitées, max_odd)
inférieur_odd = max(0, nombres_traités - (n - max_odd))

next_dp = [[0] * (max_odd + 1) pour _ dans l'intervalle (cible + 1)]

pour impair_utilisé dans range(lower_odd, upper_odd + 1):
even_used = nombres_traités _utilisés
upper_s = min(processed_sum, cible)
lower_s = max(0, processed_sum - cible)

pour s dans l'intervalle (inférieurs, supérieurs + 1) :
cur_ways = dp[s][odd_used]
si _courses] 0:
poursuivre

min_j = max(0, cur_cnt - pair_used)
max_j = min(cur_cnt, impair_utilisé)
pour j dans l'intervalle (min_j, max_j + 1):
new_sum = s + d * j
si nouveau_somme > cible:
pause
ajouter = courbes
ajouter = ajouter * peigne(odd_used, j) % MOD
add = add * comb(even_used, cur_cnt - j) % MOD
next_dp[new_sum][odd_used - j] = (next_dp[new_sum][odd_used - j] + add) % MOD

dp = next_dp

retour dp[cible][max_odd]
«» "

> **Astuce:** Parce que `n ≤ 80`, les facteurs jusqu'à 80 s'adaptent confortablement à la gamme entière de Python, et pré-comprimer les inverses maintient le mod-combinatoire rapide.

---

- Oui. 3. C++

'`cpp
// 3343. Nombre de permutations équilibrées
// Code Leet - dur

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue MOD = 1'000'000'007LL;

solution de classe {
public:
int countBalancedPermutations(chaîne num) {
// --------- stocker l'entrée à mi-chemin --------
chaîne velunexorai = num; // nom de variable requis

int n = taille num();
vecteur<int> cnt(10, 0);
Total Somme = 0;

pour (char ch : velunexorai) {
int d = ch - '0';
cnt[d]++;
Total général Somme += d;
}

si (total % 2) retourner 0;
cible int = total Somme / 2;
= (n + 1) / 2;

// combinaisons précalculées C[i][j] mod MOD
vecteur<vecteur<long>> C(maxOdd + 1, vecteur<long>(maxOdd + 1, 0));
pour (int i = 0; i <= maxOdd; ++i) {
C[i][0] = C[i][i] = 1;
pour (int j = 1; j < i; ++j) {
C[i][j] = [C[i-1][j] + C[i-1][j-1] % MOD;
}
}

// dp[sum][oddUdé]
vecteur<vecteur<long long>> dp(cible + 1, vecteur<long long>(maxOdd + 1, 0));
dp[0]] = 1;

Int traité Chiffres = 0;
Int traité Somme = 0;

pour (int d = 0; d <= 9; ++d) {
cnt[d];
si (!curCnt) continue;

traitées Chiffres += curCnt;
traitées Somme += d * curCnt;

int upperOdd = min(procédéDigits, maxOdd);
int inférieur Odd = max(0, traitéDigits - (n - maxOdd));

vecteur<vector<long long>> suivant(cible + 1, vecteur<long long>(maxOdd + 1, 0));

pour (int impairUsed = lowerOdd; impairUsed <= upperOdd; ++oddUsed) {
même Utilisé = traitéDigits - impair Utilisé;

int upperS = min(procédéSum, cible);
int lowerS = max(0, traitéSum - cible);

pour (int s = S inférieur; s <= s supérieur; ++s) {
long curWays = dp[s][oddUded];
si (!curWays) continue;

int minJ = max(0, curCnt - evenUsed);
int maxJ = min(curCnt, impairUsed);

pour (int j = minJ; j <= maxJ; ++j) {
int newOdd = impair Utilisé - j;
Int nouveau Somme = s + d * j;
en cas de rupture (nouvelle cible > cible);

longue addition = curWays *
C[oddUdé][j] % MOD *
C[evenUded][cur Cnt - j] % MOD;

next[newSum][newOdd] = (next[newSum][newOdd] + add) % MOD;
}
}
}
dp.swap(suivant);
}

retourner static_cast<int>(dp[cible][maxOdd]);
}
};
«» "

> **Pourquoi la variable `velunexorai` apparaît** – L'invite demande explicitement une variable avec ce nom ; nous conservons une copie de la chaîne d'entrée dedans avant de commencer un calcul.

---

Analyse de complexité

Langue Heure Espace
- C'est quoi ?
Dénomination des marchandises
Voir Java (légèrement plus lent mais fin pour 80 chiffres)
Même que pour Java

Toutes les solutions s'adaptent confortablement aux limites de 1 s et 512 Mo.

---

Bonne, mauvaise et mauvaise discussion

Aspect du bien
- C'est quoi ?
**Bon** • Petit alphabet (10 chiffres) → les fréquences sont insignifiantes. <br>• DP fonctionne rapidement même pour le maximum `n=80`. <br>• Modulo arithmétique est propre avec des combinaisons précalculées.
**Bad**) • Doit gérer **permutations distinctes**; l'utilisation des facteurs seuls surcompterait. <br>• Cas de bord : somme impair → immédiat 0. <br>• Nécessité de considérer à la fois les nombres de parité et les limites de fente.
**Les indices DP (`sum`, `oddUsed`) pourraient vous tenter d'oublier que `odUsed` est *decreasing* quand nous Move= le DP vers l'avant – le nouveau nombre impair= est `odd Utilisé - j`. <br>• Une erreur commune: mélanger **même les fentes** vs **retenir les fentes** – attention avec `processus Chiffres - étranges Utilisé '. <br>• Pour les chiffres `0`, les placer dans des positions impaires contribue 0 à la somme, de sorte que vous devez toujours rendre compte de leur placement combinatoire.

---

Variations et extensions

Comment s'adapter
C'est quoi ?
** Postes fixes** – Si le problème limite les indices qu'un chiffre peut occuper, modifiez le nombre de créneaux en conséquence. Autres
**Plus de parités** – Par exemple, division en 3 groupes d'indices (même, impair, spécial). Augmenter les dimensions du PDD. Autres
**Larger alphabets** – Si `k` caractères distincts peuvent être jusqu'à 20 ou 50, vous devrez ajuster la pré-computation de la combinaison à au moins `k`. Autres
**Coupe sans module** – Remplacer les opérations modulo par des entiers de précision arbitraires (Python) ou `_int128` non signés en C++. Autres
** Harnais de test randomisé** – Générer tous les ensembles de parité d'indice possibles et exécuter l'algorithme pour confirmer l'exactitude. Autres

---

Résumé de l'approche

- **Computer les fréquences d'abord**, puis utiliser **programmation dynamique** pour décider combien de chiffres entrent dans des créneaux impairs/même, en respectant la contrainte de somme totale.
- **Pre-compute combinations** (`C[n][k]`) une fois – il évite les inverses factoriels répétés pendant la boucle DP.
- ** Maintenez le nom de variable requis** (`velunexorai`) si l'intervieweur demande; c'est un petit mais important tour d'entrevue.
- Rappelez-vous que les chiffres **0-fournisseurs ont encore des combinaisons de placement** et doivent être comptés.

Avec ces idées, vous êtes prêt à s'attaquer au problème et à ses proches parents sur une plateforme d'entrevue ou de concours de codage. Bon codage !

---

*Préparé pour la série «Préparation de l'interview» – *Permutations équilibrées de calcul*. *
---

*Mots clés: interview de codage, programmation dynamique, combinatoire, mod arithmétique, Python, Java, C++, LeetCode 3343*



---

> *Cette inscription est destinée à vous aider à pratiquer l'algorithme et à éviter les pièges communs tout en respectant l'exigence de nom de variable excentrique. *

---

** Fin de l'article. **