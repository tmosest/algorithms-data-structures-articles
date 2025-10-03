---
titre: LeetCode 1922. Compter de bons nombres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Récapitulatif du problème – LeetCode 1922

A **bonne** chaîne à chiffres de longueur `n` satisfait

* ** Même l'index** (0-basé) → le chiffre est **even** (0, 2, 4, 6, 8)
* **Indice de début** → le chiffre est **prime** (2, 3, 5, 7)

On peut utiliser des zéros.
`n` peut être aussi grand que `10^15`, de sorte qu`une solution naïve `O(n)` ou `O(n2)` ne finira pas.
La réponse doit être retournée modulo `M = 1 000 000 007`.

---

L'idée fondamentale

Pour chaque position uniforme nous avons **5** choix, pour chaque position étrange nous avons **4** choix.

Laissez

«» "
evenCnt = ceil(n / 2) // nombre d'indices pairs (0,2,4,...)
impairCnt = plancher(n / 2) // nombre d'indices impairs (1,3,5,...)
«» "

Le nombre de bonnes cordes est

«» "
good(n) = 5^evenCnt · 4^oddCnt (mod M)
«» "

La tâche se résume donc à calculer deux puissances modulaires pour un immense exposant – nous utilisons ** l'explication binaire (rapide)** (temps « O(log n) », mémoire « O(1) »).

---

La complexité temporelle et spatiale

Opération Complexité
C'est quoi ?
Calculer "evenCnt", "oddCnt" Autres
Description modulaire (binaire) Autres
Multiplication finale et module Autres
**Total**** **«O(log n)», «O(1)» espace**

---

# # # Code Snippets

C'est pas vrai. Java

"Java
solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

nombre d'entrées publiquesGoodNumbers(long n) {
longue mêmeCnt = (n + 1) / 2; // indices 0,2,4,...
longue impair Cnt = n / 2; // indices 1,3,5,...

longue même Voies = modPow(5L, evenCnt, MOD);
long impairWays = modPow(4L, impairCnt, MOD);

retour (int) ((evenWays * impairWays) % MOD);
}

// exponentiation modulaire rapide
modPow (long base, long exp, long mod) {
longue res = 1L;
base %= mod;
pendant la période (exp > 0) {
si ((exp & 1)] 1) {
res = (rés * base) % mod;
}
base = (base * base) % mod;
Exp >>= 1;
}
retour rés;
}
}
«» "

# # # # # #

'`python
Solution de classe:
MOD = 1 000 000 007

def countGoodNumbers(self, n: int) -> Int:
even_cnt = (n + 1) // 2 # mêmes indices
_cnt impair = n // 2 # indices impairs

even_ways = pow(5, even_cnt, self.MOD)
impair_ways = pow(4, impair_cnt, self.MOD)

retour (même_ways * impair_ways) % self. MOD
«» "

> **Astuce** – Python®s intégré à « pow » avec trois arguments implémente déjà l'exposentiation binaire et gère d'énormes exposants.

C'est vrai. C++

'`cpp
solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;

nombre intGoodNumbers(long long n) {
longue et longue mêmeCnt = (n + 1) / 2; // même indices
long long impairCnt = n / 2; // indices impair

long et longEvenWays = modPow(5LL, evenCnt);
long long impairWays = modPow(4LL, impairCnt);

retourner static_cast<int>(evenWays * impairWays) % MOD);
}

particulier:
long long modPow(long long base, long exp) {
longue rés = 1;
base %= MOD;
pendant la période (exp > 0) {
si (exp & 1) res = (res * base) % MOD;
base = (base * base) % MOD;
Exp >>= 1;
}
retour rés;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et l'acharnement de compter de bons nombres

- Oui. 1. Présentation
Lorsque vous voyez **LeetCode 1922 – Comptez de bons numéros**, votre cerveau pourrait faire une double prise. C'est un problème combinatoire apparemment simple, mais c'est en fait un piège d'interview classique : * Savez-vous gérer des exposants gigantesques ?* *
Dans ce post, nous allons disséquer le problème, explorer pourquoi des solutions naïves échouent, montrer l'approche propre `O(log n)`, et mettre en évidence les nuances prêtes à l'entrevue.

> ** Tags de référence**: `Count Good Numbers`, `LeetCode 1922`, `fast exponentiation`, `modular exponentiation`, `Python solution`, `Java solution`, `C++ solution`, `algorithme interview "

---

- Oui. 2. Réapparition des problèmes
Une chaîne à chiffres est "good" lorsque:

Position des chiffres autorisés
- C'est pas vrai.
0, 2, 4,... (même)
1, 3, 5,...

Vous devez compter toutes les bonnes chaînes de longueur `n`, modulo `10^9+7`.
Avec `n ≤ 10^15`, vous ne pouvez même pas itérer sur la chaîne – nous avons besoin de *mathématiques*.

---

- Oui. 3. Le bien – Pourquoi la solution est droite-en avant
Considérez la chaîne comme deux voies indépendantes :

1. ** Même voie** – 5 choix par place → 5 possibilités
2. **Odd lane** – 4 choix par place → 4 possibilités

Nombre de points:
- Même indices = `(n + 1)/2` (arrondi)
- Indices de tendance = `n/2` (arrondi)

Des possibilités de multiplication de chaque voie donnent:

«» "
good(n) = 5^(even) · 4^(odd) (mod. 1 000 000 007)
«» "

**Le "good"** est qu'une fois que vous voyez cette formule, le reste est de routine.

---

- Oui. 3. Le "Bad" – Pourquoi Brute La force est un cauchemar
Une réponse commune des débutants est:

'`python
# O(n) comptant chaque position
pour _ dans la plage(n):
# multiplier par 5 ou 4
«» "

Même si nous calculons simplement `pow(5, n//2)` dans une boucle, le nombre `5^10^15` a **~10^15 chiffres**.
- **Time**: `O(n)` → ~10^15 opérations → impossible.
- **Mémorie**: Les ints de Python se développeraient au-delà de la RAM.
- **Conséquence de l'entrevue**: Les intervieweurs demandent *pourquoi* vous avez choisi cela, et votre réponse sera pénalisée.

---

- Oui. 4. Les cas de bord qui vous emportent

Qu'est-ce que regarder ?
-- -- -- -- -- -- -- -- --
= 1, impair = 0 → réponse = 5
Même = 1, impair = 1 → réponse = 54 = 20
Grand `n` (10^15)=Les exposants débordent de 32 bits. Utiliser des réductions longues/longues et modulaires. Autres
"(5^x % M) * (4^y % M) " peut dépasser 64 bits dans les langues qui n'utilisent pas de grands entiers. Appliquer toujours modulo après chaque multiplication. Autres

---

- Oui. 5. La solution propre – l'exposition binaire

L'exposition binaire réduit `base^exp` à `O(log exp)` en coupant la base à plusieurs reprises et en réduisant de moitié l'exposition.
Pseudocode:

«» "
pow_mod(base, exp):
résultat = 1
base %= M
pendant l'exp > 0:
if exp impair: result = result * base % M
base = base * base % M
Exp/= 2
résultat du retour
«» "

Les implémentations **Java** et **C++** nécessitent un codage manuel, tandis que **Python** peut simplement appeler `pow(base, exp, M' – ce qui est intégré utilise le même algorithme sous le capot.

---

- Oui. 6. Conseils d'entrevue

Sujet de l'entrevue
-- -- -- -- -- -- -- ------------------
**Pourquoi l'exponentiation modulaire est importante** Demandez pourquoi le modulo est nécessaire ici. Autres
**Choisir le bon type de données**= En Java, utiliser `long`, en C++ `long`, en Python `int` (non consolidé). Autres
**Why `O(log n)` beats `O(n)`**= Discutez de la division binaire : chaque boucle réduit de moitié l'exposant. Autres
**Tests**= Vérifier avec de petites valeurs (`n = 1, 2, 3, 4, 5`). Ensuite, exécutez avec `n = 10^12` pour confirmer que l'exécution est <1 s.
** Expliquez le raisonnement** Autres

---

- Oui. 7. Code dans un seul message – Java, Python, C++

*(Les blocs de code sont identiques aux extraits ci-dessus, de sorte que le lecteur peut copier-coller.) *

"Java
// Code Java
«» "

'`python
Code Python
«» "

'`cpp
Code C++
«» "

---

- Oui. 8. Wrap-Up et ce que les recruteurs veulent
- **Clarté**: Écrire un code facile à lire.
- **Recours dans l'espace temporel**: Montrez que vous comprenez que `O(log n)` est la limite optimale pour ce problème.
- **Connaissance des cas**: Essai avec `n = 1`, `n = 2` et nombres énormes.
- **Discussion**: Dans l'entrevue, demandez si l'intervieweur veut que vous prouviez la formule ou juste livrer la mise en œuvre.

> **Si vous pouvez expliquer ce problème en 5 minutes et produire une solution sans bugs, `O(log n)`, vous êtes prêt pour le tour d'Algorithmes & Structures de données à n'importe quel entretien technique de haut niveau. **

---

- Oui. 9. Liste de contrôle à emporter

Objet
C'est pas vrai.
Autres Compter correctement les indices pair/odd
Autres Utiliser une exponentiation modulaire (`pow` en Python, binaire manuel en Java/C++)
Conserver tous les résultats intermédiaires
Éviter le débordement de 32 bits – utiliser 64 bits (`long', `long`)
Expliquer la complexité du temps/de l'espace
Autres Afficher quelques cas de test
Autres Soyez prêt à justifier pourquoi vous avez utilisé exponentiation rapide

Bon codage, et que vos chaînes de "good" soient toujours comptées avec précision ! C'est ce qu'il a dit