---
titre: LeetCode 375. Devine numéro supérieur ou inférieur II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 375 – Devine numéro supérieur ou inférieur II
**Programmation dynamique Maîtrise en Java / Python / C++ – Un entretien de travail Guide prêt**

> **Mots-clés**: LeetCode 375, Guess Number Higher or Lower II, programmation dynamique, codage d'entretien, solution Java, solution Python, solution C++, stratégie optimale, mémorisation DP, entretien d'emploi

---

## Résumé du problème (Code Leet 375)

> Nous jouons un jeu de devinettes:
> - L'adversaire choisit un entier `x` dans `[1, n]`.
> - Pour chaque fausse idée `g` vous payez `g` dollars.
> - Après chaque supposition on vous dit si `x` est supérieur ou inférieur.
>
> **Objectif**: Calculer le montant minimum d'argent nécessaire pour *garantir* une victoire pour n'importe quel `n` (c'est-à-dire le pire des coûts de la stratégie optimale).

**Contrôles* *

- "1 ≤ n ≤ 200"

---

Pourquoi ce problème fait-il un entretien d'embauche ?

- ** Programmation dynamique (DP)** : PDD classique avec une sous-structure optimale (résultant du problème de la goutte d'oeufs).
- ** Théorie du jeu** : Nécessite un raisonnement sur les scénarios les plus défavorables.
- ** Sensibilisation à la complexité** : Il faut reconnaître qu'une solution naïve est "O(n3)" alors que le PDD optimal est "O(n2)".
- **Langue Agnostique**: Vous pouvez l'implémenter dans n'importe quelle langue ; les recruteurs apprécient le code propre et idiomatique.

---

## Aperçu de la solution

- Oui. 1. Récurrence

Let `dp[l][r]` est le montant minimum nécessaire pour garantir une victoire dans l'intervalle `[l, r]`.
Si `l == r`, aucun argent n`est nécessaire (`dp[l][l] = 0`).

Pour `l < r`, nous essayons chaque première supposition `k`:

«» "
coût(k) = k + max(dp[l][k-1], dp[k+1][r]
«» "

- On paie des k' dollars pour la première supposition.
- Si la réponse est inférieure, nous sommes partis avec `[l, k-1]`.
- Oui. Si la réponse est plus élevée, nous sommes partis avec `[k+1, r]`.

Nous prenons le minimum sur tous `k`:

«» "
Coût(k)
«» "

- Oui. 2. Stratégies de mise en œuvre

L'approche La complexité Quand utiliser
C'est pas vrai.
**Récursion du haut vers le bas + mémoisation**= Heure `O(n2)`, espace `O(n2)`=Code propre; facile à comprendre. Autres
**Temps «O(n2)», «O(n2)» l'espace Un peu plus rapide dans la pratique; bon pour les entrevues qui nécessitent un DP itératif. Autres
**O(n log n)' temps, espace `O(n2)` (toujours DP) Autres

Nous proposons **trois** solutions linguistiques spécifiques:

1. **Java** – Récursif + mémoisation (classe `Solution`).
2. **Python** – décorateur `functools.lru_cache` (classe `Solution`).
3. **C++** – «vecteur<vecteur<int>>» Tableau DP (classe `Solution`).

---

Mise en œuvre du code

- Oui. Java (récursif + mémorisation)

"Java
***
* 375. Numéro de prévision supérieur ou inférieur II
* Heure: O(n^2)
* Espace: O(n^2)
*/
solution de classe publique {
mémo privé int[];

Int public getMoney Montant(int n) {
mémo = nouvelle int[n + 2][n + 2]; //
retour dfs(1, n);
}

Int privé dfs(int bas, int haut) {
si (faible >= élevé) retourner 0;
si [memo[faible][élevé] != 0) retour de mémo[faible][élevé];

int best = entier.MAX_VALUE;
pour (int devine = low; devine <= high; devine++) {
coût int = devine + Math.max(dfs(faible, devine - 1),
dfs(devises + 1, haut)
best = Math.min (best, cost);
}
mémo[faible][élevé] = meilleur;
le meilleur retour;
}
}
«» "

> ** Pourquoi mémo ? **
> Sans elle, le même sous-intervalle serait recalculé à plusieurs reprises (soufflage exponentiel).
> La table de mémo réduit la complexité à quadratique.

---

### Python (Top-Down DP avec `lru_cache`)

'`python
"""
375. Numéro de prévision supérieur ou inférieur II
Heure : O(n^2)
Espace : O(n^2) (cache)
"""

à partir de functools importer lru_cache

Solution de classe:
def getMoneyMontant(self, n: int) -> Int:
@lru_cache(Aucun)
def dp(l: int, r: int) -> Int:
si l >= r:
retour 0
meilleure = flotteur('inf')
pour devinez dans la plage(l, r + 1):
coût = devinette + max(dp(l, devine - 1), dp(guess + 1, r))
best = min (best, coût)
le meilleur retour

retour dp(1, n)
«» "

> **Astuce**: Utilisez `@lru_cache` pour éviter les tables de mémo manuelles – garde le code court et Pythonic.

---

### C++ (Bottom-Up DP)

'`cpp
***
* 375. Numéro de prévision supérieur ou inférieur II
* Heure : O(n^2)
* Espace : O(n^2)
*/
solution de classe {
public:
Int getMoney Montant(int n) {
vector<vector<int>> dp(n + 2, vector<int>(n + 2, 0));

pour (int len = 2; len <= n; ++ len) { // longueur de l ' intervalle
pour (int l = 1; l + len - 1 <= n; ++l) {
int r = l + len - 1;
int best = INT_MAX;
pour (int k = l; k <= r; ++k) {
coût int = k + max(dp[l][k - 1], dp[k + 1][r];
best = min (best, coût);
}
dp[l][r] = meilleur;
}
}
retour dp[1][n];
}
};
«» "

> **Pourquoi en haut? **
> La boucle externe construit des intervalles de petite à grande, garantissant que tous les sous-intervalles sont déjà résolus au besoin.

---

Cas d'essai

Explication
- C'est quoi ?
Un seul numéro – aucun coût. Autres
Devinez 1 → coûter 1 si mal. Autres
2 : coût 2 + max(0,0) = 2.
Dans la déclaration. Autres
Calcul rapide – toujours rapide (= 0,01 s). Autres

> Exécuter `python -m unittest` ou similaire à valider.

---

Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
Autres **Caisse de base**= Gestion correcte `l >= r` → 0 coût==========================================================================================================================================================================================================
*Complexité * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Mémoisation**= Utilise un tableau 2-D ou `lru_cache`== Utiliser `HashMap` avec un mauvais format de clé==Collision de clé mémo ou des entrées manquantes===
**Itérative vs Recursive**= Le bas vers le haut donne un contrôle explicite de l'ordre des intervalles== Le haut vers le bas peut dépasser la profondeur de récursion dans d'autres langues==En utilisant l'état mutable global de manière incorrecte==

> **À emporter**:
> *Identifiez toujours la récurrence du PDD, implémentez la mémorisation et testez avec de petites valeurs avant de mettre à l'échelle.

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
Haut vers le bas (Java / Python)
Vers le haut (C++) Autres

> Avec `n ≤ 200`, les deux approches fonctionnent en microsecondes.

---

Conseils d'entrevue

1. **Exposer la récurrence** avant le codage. Les recruteurs aiment vous voir raisonner à travers les sous-structures.
2. **Énoncer clairement le cas de base** (`l == r → 0`).
3. **Mentionner l'échange temps/espace** – vous pouvez discuter à la fois de récursion + mémo ou de DP itérative.
4. **Afficher un exemple** (par exemple, `n = 10`) pour illustrer pourquoi la formule fonctionne.
5. **Optionnel**: parlez d'optimisations possibles (par exemple, recherche binaire pour réduire la boucle interne à `O(log n)`), même si vous ne les implémentez pas.

---

Enveloppe

- Oui. Le problème est un puzzle classique de programmation dynamique qui teste la récursion, la mémorisation et le raisonnement du pire cas.
- Oui. La solution optimale est **quadratic** en `n` et fonctionne magnifiquement pour `n ≤ 200`.
- Les extraits de Java, Python et C++ fournis sont prêts à coller dans votre éditeur ou juge en ligne LeetCode.
- Maîtriser ce problème vous donne une base solide pour de nombreuses questions d'entrevue qui impliquent ** stratégie optimale** ou ** jeu-théorique DP**.

**Bonne chance pour votre prochaine interview de codage!**

---

> **Partager** cet article sur Linked Dans ou GitHub pour aider les autres et montrer les recruteurs que vous avez ce défi de programmation dynamique sous contrôle.