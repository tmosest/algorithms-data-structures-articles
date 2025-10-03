---
Titre: LeetCode 1259. Les poignées de main qui ne croisent pas -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1-
Résumé du problème (Code Leet)

> On vous donne un nombre pair de personnes `numPeople` debout dans un cercle.
> Chaque personne serre la main avec exactement une autre personne, il ya donc `numPeople/2` poignées de main au total.
> Comptez le nombre de façons distinctes d'effectuer les poignées de main ** sans que deux poignées de main ne traversent**.
> Retourner la réponse modulo **1 000 000 007**.

**Contrôles* *

NumPersonnes
C'est pas vrai.
2 ≤ numPersonnes ≤ 1000

L'exemple
- `numPeople = 4 → 2`
- `numPeople = 6 → 5`

---

- Oui. Les mathématiques derrière la réponse – Nombres catalans

Si vous dessinez les gens autour d'un cercle et reliez des paires de poignées de main avec des lignes droites, l'état de non-croisement signifie que les lignes forment un ** non-croisement parfait correspondant** sur un polygone convexe.

Le nombre de correspondances pour un polygone convexe avec des sommets `2k` est exactement le nombre de catalans **k-th**:

\[
C_k = \frac{1}{k+1}\binom{2k}{k} = \sum_{i=0}^{k-1} C_i \cdot C_{k-1-i}
\]

Donc pour le problème nous avons seulement besoin
\[
\text{réponse} = C_{\,numPeople/2} \pmod{1\,000\,000\,007}
\]

---

Solution de programmation dynamique (O(n2))

Au lieu de calculer les coefficients binômes et les inverses modulaires (ce qui est également très bien), nous pouvons construire les numéros catalans avec une récurrence DP classique:

«» "
dp[0] = 1 // polygone vide
dp[2] = 1 // une poignée de main
pour i de 4 à n étape 2:
dp[i] = 0
pour j de 2 à i-2 étape 2:
dp[i] += dp[j] * dp[i-j] (mod M)
«» "

**Pourquoi ça marche* *
- Jumeler la première personne à quelqu'un en position "j".
- Oui. Les gens entre eux forment un plus petit polygone de "j" sommets,
le reste forme un polygone de sommets "i-j".
- Multiplier le nombre de voies pour les deux parties et la somme sur tous les "j" valides.

**Complexité* *

Opération Temps Espace
- C'est quoi ?
Loop extérieur \(O(n/2)\) Autres
Loop intérieur
Total Autres

Avec `n ≤ 1000`, `O(n2)` (= 500 000 itérations) est trivial.

---

- Oui. Mise en œuvre des références

Voici des implémentations propres, prêtes à la copie dans **Java**, **Python** et **C++**.
Tous sont `O(n2)` et gèrent correctement le modulo.

> **Conseil:**
> En Java et C++ utilisez `long`/`int64_t` pendant la multiplication pour éviter le débordement.
> Dans Python `int` est la précision arbitraire, donc il est plus simple.

---

#### 4.1 Java

"Java
importation java.io.*;
Importation de java.util.*;

solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

Nombre d'entrées publiques DeWays(int n) {
// n est garanti
long[] dp = nouveau long[n + 1];
dp[0] = 1;
dp[2] = 1;

pour (int i = 4; i <= n; i += 2) {
somme longue = 0;
pour (int j = 2; j <= i - 2; j += 2) {
somme = (somme + dp[j] * dp[i - j]) % MOD;
}
dp[i] = somme;
}
retour (int) dp[n];
}
}
«» "

**Comment fonctionner (essai rapide): * *

"Java
classe publique {
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.numberOfWays(4)); // 2
Système.out.println(s.numberOfWays(6)); // 5
}
}
«» "

---

4.2 Python

'`python
MOD = 1 000 000 007

def number_of_ways(n: int) -> Int:
# N est égal
dp = [0] * (n + 1)
dp[0] = 1
dp[2] = 1

pour i dans la plage(4, n + 1, 2):
Total = 0
pour j dans la gamme(2, i, 2):
Total = (total + dp[j] * dp[i - j]) % MOD
dp[i] = total

retour dp[n]


si __nom__ == "__main__" :
print(number_of_ways(4)) # 2
print(number_of_ways(6)) # 5
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue MOD = 1'000'000'007LL;

nombre intDeWays(int n) {
vecteur <long> dp(n + 1, 0);
dp[0] = 1;
dp[2] = 1;

pour (int i = 4; i <= n; i += 2) {
long total = 0;
pour (int j = 2; j <= i - 2; j += 2) {
total = (total + dp[j] * dp[i - j]) % MOD
}
dp[i] = total;
}
retourner static_cast<int>(dp[n]);
}

Int main() {
<< nombreOfWays(4) << endl; // 2
<< nombre OfWays(6) << endl; // 5
}
«» "

---

C'est pas vrai. Billet de blog: Les poignées qui font la croix – Le bon, le mauvais, et le mauvais

---

#### 5.1 Intitulé et Méta‐Description (SEO‐Ready)

> **Titre:** Serre-mains qui font la croix – Un simple DP à Ace LeetCode 1259
> **Méta—Description:** Apprenez les maths derrière le problème de poignée de main non croisée, consultez les solutions O(n2) Java/Python/C++ et préparez-vous à l'entretien avec des extraits de code clairs. Parfait pour votre prochain entretien technique!

---

5.2 Introduction

> Imaginez un groupe d'amis debout dans un cercle, chacun se serre la main avec exactement l'un l'autre. Combien de façons peuvent-ils faire cela sans aucune des poignées de main ? Cette question faussement simple est un problème dur classique de LeetCode (#1259) et un grand piège d'entrevue.
> Dans cet article, nous disséquerons le problème, expliquerons pourquoi la réponse est un nombre catalan, montrerons une implémentation DP propre, et vous donnerons trois solutions prêtes à la copie dans **Java**, **Python** et **C++**. En chemin, nous allons parler du bon, du mauvais, et de la moche des différentes approches afin que vous puissiez choisir le bon pour votre interview ou défi de codage.

---

5.3 Le bon – Pourquoi le DP est un ajustement naturel

- **Récurrence linéaire** – Chaque paire de poignées de main divise le cercle en deux sous-cercles indépendants.
- **Évite les pièges combinatoires** – Vous ne pouvez pas simplement compter toutes les poignées de main et soustraire les croisements; la structure combinatoire est non-triviale.
- **Time-Efficace** – `O(n2)` est facilement rapide pour `n ≤ 1000`.
- **Modulaire Arithmetic Friendly** – Fonctionne avec un seul module (1 000 000 007).

---

5.4 Les mauvaises – Erreurs communes

Pourquoi il fait défaut
C'est quoi ?
**Utiliser les facteurs sans inverses modulaires**= Vous allez déborder et besoin de calculer inverses modulaires, ce qui ajoute une complexité inutile. Autres
**En supposant que tous les appariements sont valides**=Ignorer la contrainte de « non-croisement » conduit à de nombreuses configurations astronomiquement invalides. Autres
Même avec la taille, 1000 personnes donnent ~109 itérations – impossibles dans le temps. Autres
**Utilisation de `int` pour la multiplication en Java/C++** peut dépasser la plage de 32 bits; utiliser "long long" / "long".

---

#### 5.5 L'horrible – Pourquoi les nombres de catalans

- **Complexité du coefficient biologique** – Computing \(C_k\) via \(\frac{1}{k+1}\binom{2k}{k}\) nécessite des inverses modulaires et une pré-computation factorielle.
- **Potential Off‐By‐One Erreurs** – La manipulation des indices `k` vs. `k-1` peut vous faire monter.
- **Moins d'intuitifs pour les intervieweurs** – Certains intervieweurs préfèrent voir la logique du PDD se développer plutôt qu'une formule monoligne.

---

5.6 Dernier départ

Un DP concis qui reflète la structure combinatoire du problème est la solution la plus sûre, la plus rapide et la plus facile à interviewer. Il évite les pièges, reste dans les délais, et démontre clairement votre compréhension de la récursion et de l'arithmétique modulaire.

---

### 5.7 Bonus – Conseils de performance

- **Pré-allouer des tableaux** une fois; aucune attribution de mémoire répétée en boucles.
- **Utilisez `long`** (C++), `long` (Java) ou `int` intégré (Python) pour éviter les débordements.
- **Mod après chaque ajout/multiplication** pour garder les nombres petits.
- **Si vous êtes à la hauteur d'un défi**: calculez les nombres catalans dans `O(k)` en utilisant une seule boucle avec la formule \(C_{k+1} = \frac{2(2k+1)}{k+2}C_k\) et les inverses modulaires; c'est un excellent tour de l'interview.

---

Réflexions de clôture

> Le problème "Handshakes That Don't Cross" est un mélange parfait de combinatoire, de récursion et d'arithmétique modulaire. La maîtrise vous donne non seulement une solution O(n2) propre, mais démontre également une compréhension profonde de la façon dont un puzzle apparemment simple cache une structure catalane classique.
> Gardez les extraits de code à portée de main, pratiquez l'explication du raisonnement du PDD, et vous serez prêt à impressionner votre prochain recruteur ou as l'entrevue de codage. Bon codage !

---