---
titre: LeetCode 2305. Distribution équitable des cookies -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 2305 – *Répartition équitable des cookies*
> **Le bon, le mauvais et le mauvais – Un profond Guide de plongée pour la réussite des entrevues**

> *Si vous préparez une entrevue d'ingénierie logicielle, ce post est votre feuille de tricheur pour l'un des problèmes LeetCode les plus populaires qui teste la récursion, la taille et le DP bitmask. *

---

Table des matières
1. [Résumé du problème] (#résumé du problème)
2. [Observations et contraintes clés](#observations clés)
3. [Stratégie de résolution] (#solution-stratégie)
4. [Applications de référence] (#applications de référence)
- [Python 3] (#python-3)
- [Java 17] (#Java-17)
- [C++17] (#c-17)
5. [Complexité temporelle et spatiale](#complexité)
6. [Pièges communs et pièges] (#pièges)
7. [Optimisations & [Bonnes]
8. [Interview Take-aways](#interview-takeaways)
9. (#meta)

---

## Résumé des problèmes <un nom="résumé des problèmes"></a>
Vous êtes donné un tableau `cookies` où `cookies[i]` est le nombre de cookies dans le sac *i*-th.
Vous devez distribuer **tous** sacs parmi les enfants `k`. Un sac ne peut pas être fendu; chaque enfant reçoit des sacs entiers.

** Inéquité** d'une distribution = maximum de cookies reçus par un seul enfant.
Votre tâche : **Rendre le minimum d'injustice possible**.

Obstacles
Variable
C'est pas vrai.
"cookies.longueur" , 2 , 8 , très petit – parfait pour le retour
"cookies"[i]"" 1" 105" Grandes sommes → utiliser 64-bit entiers"
"k"" 2" "cookies.longueur"

---

## Principales observations et contraintes <un nom="observations clés"></a>

Observation Pourquoi ça compte
C'est-à-dire
Autres ** Jusqu'à 8 sacs seulement. Autres
**Le sum peut être grand**= Utiliser `long` / `long long` pour éviter le débordement. Autres
**L'objectif est le problème d'équilibre de charge classique. Autres
**Symmétrie**= L'attribution de l'enfant `i` au sac `j` est la même que l'attribution de l'enfant `j` au sac `i`. On peut créer des états identiques. Autres
**Monotonicité**= Si le courant max dépasse un meilleur connu, abandonnez la branche. Autres
**Bitmask DP**= Avec `n=8` nous pouvons garder un bitmask de sacs déjà assignés. Autres

---

## Stratégie de solution <a name="solution-strategy"></a>

1. **Trier les sacs par ordre décroissant**.
- Sacs plus grands placés en premier → taille précoce (le facteur de branchement baisse plus rapidement).
2. **Suivi** avec élagage :
- Maintenir un tableau `childSum[k]` des cookies actuels par enfant.
- Attribuer récursivement le sac actuel à tout enfant dont l'addition ne dépasse pas la meilleure injustice constatée jusqu'à présent.
- Si à un moment quelconque `max(childSum) >= best`, backtrack.
3. **Bitmask DP (facultatif)** – pour éviter de répéter le travail lorsque le même jeu de sacs est distribué dans des ordres différents.
- DP[masque] = charge maximale minimale possible pour le sous-ensemble de sacs représenté par «masque».
- Itérer au-dessus des sous-masques; complexité "O(3n)" ce qui est bon pour "n=8".
4. **Rendre le meilleur cas d'injustice**.

Cette approche est le modèle standard de suivi arrière + taille qui est fortement favorisé sur les discussions de LeetCode.

---

## Mise en oeuvre des références <un nom="mise en oeuvre des références"></a>

### Python 3 <un nom="python-3"></a>
'`python
de taper l'importation Liste

Solution de classe:
def distribuer Cookies(self, cookies: List[int], k: int) -> Int:
cookies.sort(reverse=True) # plus gros sacs d'abord
n = len(cookies)
best = somme(cookies) # limite supérieure

enfant = [0] * k

def dfs(idx: int, cur_max: int):
non local meilleur
Si idx == n:
best = min(meilleur, cur_max)
retour
if cur_max >= best: # taille
retour
sac = cookies[idx]
utilisé = set()
pour i dans la plage(k):
# sauter des sommes d'enfants identiques pour éviter les états symétriques
si l'enfant est utilisé:
poursuivre
utilisé.add(enfant[i])

enfant[i] += sac
dfs(idx + 1, max(cur_max, enfant[i])
enfant[i] -= sac

Dfs(0, 0)
le meilleur retour
«» "

**Pourquoi ça marche* *
- Oui. L'ensemble `utilisé` saute en plaçant un sac dans un enfant qui a déjà le même total, ce qui élimine les permutations qui produisent le même état.
- `cur_max` est mis à jour paresseusement; dès qu'il atteint ou dépasse le plus connu, la branche est abandonnée.

---

### Java 17 <a name="java-17"></a>
"Java
Importation de java.util.*;

solution de classe {
Int privé le mieux;
enfant privé;
cookies privés int[];

diffusion publique des cookies(int[] cookies, int k) {
Tableau.sort(cookies); // ascendant
inverse(cookies); // descendant
Ça. cookies = cookies;
enfant = nouveau int[k];
best = Arrays.stream(cookies).sum(); // lien supérieur

dfs(0, 0);
le meilleur retour;
}

vide privé dfs(int idx, int curMax) {
si (idx) cookies.longueur) {
best = Math.min(best, curMax);
retour;
}
si (curMax >= meilleur) retour; // taille

sac int = cookies[idx];
Set<integer> utilisé = nouveau HashSet<>();
pour (int i = 0; i < durée enfant; i++) {
si (!used.add(child[i])) continue; // saute les états symétriques

enfant[i] += sac;
dfs(idx + 1, Math.max(curMax, enfant[i]);
enfant[i] -= sac;
}
}

vide privé inverse(int[] arr) {
pour (int i = 0; i < arr.longueur / 2; i++) {
int tmp = arr[i];
[i] = arr[longueur arrière - 1 - i];
arr[longueur arrière - 1 - i] = tmp;
}
}
}
«» "

** Faits saillants* *
- Utilise un `Set` pour sauter les sommes symétriques de l'enfant.
- l'aide `reverse` transforme le tableau trié en ordre décroissant.
- Le "meilleur" est le minimum d ' injustice constaté jusqu ' à présent.

---

### C++17 <a name="c-17"></a>
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int distribuer Cookies(vecteur<int>& cookies, int k) {
tri(cookies.rbegin(), cookies.rend()); // descendant
int best = accumule(cookies.begin(), cookies.end(), 0);
vecteur<int> enfant(k, 0);
dfs(0, 0, meilleur, cookies, enfant);
le meilleur retour;
}

particulier:
vide dfs(int idx, int curMax, int &best,
végétatif de const<int> &cookies, vectoriel<int> &child) {
si (idx == cookies.size()) {
best = min(meilleur, curMax);
retour;
}
si (curMax >= meilleur) retour; // taille

sac int = cookies[idx];
non ordonné_set<int> vu;
pour (int i = 0; i < enfant taille(); ++i) {
si (!seen.insert(child[i]).seconde) continue; // symétrie

enfant[i] += sac;
dfs(idx + 1, max(curMax, child[i]), meilleur, cookies, enfant);
enfant[i] -= sac;
}
}
};
«» "

**Pourquoi c'est efficace* *
- `unordered_set<int>` élimine rapidement les états symétriques.
- `accumuler` calcule la limite supérieure initiale en un seul passage.

---

## Complexité temporelle et spatiale <un nom=complexité></a>

L'approche de la pire affaire
- Oui.
"O(kn)" Autres
Reprise avec élagage (les trois implémentations) Autres
"O(3n)" (~ 6561 quand n=8)" Autres

Compte tenu de "n ≤ 8", toutes les solutions fonctionnent confortablement en < 10 ms sur les juges modernes.

---

## Pièges communs & ##Pièges <un nom="pièges"></a>

Pourquoi il casse
- Oui.
**Ne pas trier en descendant** Trier les «cookies» dans l'ordre inverse. Autres
**L'utilisation de `int` pour les sommes**=Le cookie compte jusqu'à 105, et `k` jusqu'à 8 → la somme peut dépasser 231‐1. Autres
Autres **Aucun élagage** Comparer `curMax` avec le meilleur actuel. Autres
**Ignorer la symétrie** Tracez la somme des enfants vus dans chaque profondeur. Autres
**Bitmask DP erreur d'énumération du sous-ensemble** "Itérer correctement les sous-masques ("pour (int sub = masque; sub; sub = (sub-1)&mask)"). Autres

---

## Optimisations & ##Bon=Tricks <un nom="optimisations"></a>

1. **Démarrer avec le plus grand sac** – réduit les ramifications tôt.
2. **Mémoisation sur les sommes pour enfants** – stocker "dp[mask] = meilleure injustice" pour réutiliser les états.
3. **Désistement précoce** – si un enfant a déjà une somme égale au meilleur, d'autres affectations à cet enfant sont inutiles.
4. **Approfondissement itératif** – commencer à chercher avec un lien serré et se détendre progressivement.
5. **Bitmask DP** – pour les intervieweurs qui veulent voir les connaissances du PDD, c'est une bonne alternative.

---

## Interview Take‐aways <a name="interview-taways"></a>

Comment ce problème le démontre
Il y a lieu de se reporter au présent document.
**La pensée récursive**Le fait de se résoudre à la rétrotraque montre la capacité de construire une recherche approfondie. Autres
**Élagage et optimisation**= Discutez pourquoi le tri et la taille symétrique sont critiques. Autres
**Analyse de la complexité** Autres
**Manipulation des caisses** La manipulation de sommes importantes («long»/«long») montre l'attention portée au débordement. Autres
**Lisibilité du code**=Les fonctions d'aide propres (`reverse`, `dfs`) et les commentaires impressionnent les intervieweurs. Autres

**Conseil:** Lors d'une entrevue, posez toujours des questions claires sur les contraintes. Ici, savoir `n ≤ 8` est le pivot pour le recul.

---

## SEO Méta Description <a name="meta"></a>
> Master LeetCode 2305 – Distribution équitable des cookies. Lisez le guide complet, les solutions Python/Java/C++, l'analyse de complexité et les conseils d'entrevue. Boostez vos scores d'entrevue de codage!

---

Les pensées finales

*Le problème de la distribution équitable des cookies est trompeurment simple, mais il teste votre capacité à combiner la récursion, l'élagage et le DP bitmask – tous cruciaux pour une entrevue de codage de niveau supérieur. En maîtrisant les trois implémentations de référence ci-dessus et en comprenant les pièges, vous serez prêt à aser ce problème et démontrer une grande fluence algorithmique. *