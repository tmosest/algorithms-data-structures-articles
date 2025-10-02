---
titre: LeetCode 1434. Nombre de façons de porter différents chapeaux à l'autre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1434
**Nombre de façons de se porter des chapeaux différents**

* Il y a `n` personnes (`1 ≤ n ≤ 10`).
* Il y a 40 types de chapeaux (1 ... 40).
* "hats[i]" liste les numéros de chapeau que la personne `i` aime.
* Chaque personne doit porter ** exactement un** chapeau et pas deux personnes peuvent porter le même chapeau.
* Retourner le nombre d'affectations valides modulo **1 000 000 007**.

La solution classique est un "bit-mask DP" qui itère sur les 40 chapeaux au lieu des gens, parce que le nombre de chapeaux est fixe (40) alors que le nombre de personnes est minuscule (10').

---

- Oui. 2. L'idée – bonne, mauvaise, moche

L'aspect de la bonne mauvaise mauvaise
- C'est quoi ?
*Traitez les chapeaux comme la boucle *outer*; les gens sont l'état *. *Sans taille, vous exploreriez les états `40 * 2n` – encore minuscules, mais la profondeur de récursion peut exploser. Si vous oubliez le modulo ou le débordement, la réponse peut devenir négative / incorrecte
Pour `n = 10`, 2n = 1024 → ~40 000 cellules DP – parfaitement fine.
**Mise en œuvre** Les gens n'aiment peut-être pas le chapeau actuel – de nombreuses «continue» déclarations.

---

- Oui. 3. L'algorithme (étape par étape)

1. **Pré-processus**
Construire un tableau `people[41]` où "peuple [h]" est la liste des personnes qui aiment chapeau `h`.
C'est l'inverse de l'entrée et nous permet d'itérer sur les chapeaux efficacement.

2. **État du PD**
`dp[hat][masque]` – nombre de façons d`attribuer des chapeaux de `hat` à `40` ** étant donné** que les personnes représentées par la "masque" sont toujours ** non signées**.
*`masque`* est un peu de longueur `n`.
Exemple: si `n = 3` et `masque = 0b101` → les personnes 0 et 2 sont toujours libres.

3. **Transition**
Pour un "hat" et un "masque" donnés:
* **Passer** le chapeau: `ways = dp[hat+1][masque]`.
* Pour chaque personne `p` qui aime ce chapeau (`p=" people[hat]`) et est toujours libre (`mask & (1<<p)`):
* Attribuer le chapeau à `p` → nouveau masque `masque ^ (1<<p)`.
* Récurse: "ways += dp[hat+1][masque ^ (1<<p)]".
Tout arithmétique est modulo "MOD".

4. **Affaires de base**
* Si "masque". 0` → toutes les personnes sont déjà assignées → retourner `1`.
* Si `hat > 40` et `masque != 0` → pas de chapeau gauche → retour `0`.

5. **Résultat**
Commencez par `hat = 1` et masque complet `(1<<n)-1`).

La profondeur de récursion est au plus `41` (hats + 1) – sûr pour toutes les langues.

---

- Oui. 4. Analyse de la complexité

Mesure Formule Valeur pour `n = 10`
- Oui.
Durée des opérations
Mémoire: 40 960 entiers (~160 KB)

Les deux sont bien dans les limites pour la programmation concurrentielle ou LeetCode.

---

- Oui. 5. Mise en œuvre du code

Ci-dessous sont **propre, prêt à la production** solutions pour **Java**, **Python** et **C++**.
Tous partagent la même idée algorithmique ; les seules différences sont la syntaxe et les structures de données.

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe {
int final statique privé MOD = 1_000_000_007;
// dp[hat][masque] où le chapeau [1, 40] (basé sur l'index 1)
Int[][] dp;
Int privé n; // nombre de personnes
Liste privée <Integer>[] personnes; // personnes qui aiment chaque chapeau

Nombre d'entrées publiques Ways(Liste<Liste<entier>> chapeaux) {
n = chapeaux.taille();
// personnes[1..40] – liste des indices de personnes qui aiment le chapeau h
personnes = nouvelle liste de répartition[41];
pour (int i = 0; i <= 40; i++) les personnes[i] = nouvelle liste de distribution<>();
pour (int p = 0; p < n; p++) {
pour (int h : chapeaux.get(p)) personnes[h].add(p);
}

// dp dimensions: 41 chapeaux + 1 (1 à base), 1 < < n masques
dp = nouvelle int[41][1 << n];
pour (int[] rang : dp) Arrays.fill(row, -1);

retour dfs(1, (1 << n) - 1);
}

Int privé dfs(int chapeau, masque int) {
si (masque) 0) retour 1; // toutes les personnes affectées
si (hat > 40) retourner 0; // aucun chapeau restant

int &res = dp[hat][masque];
Si (res != -1) retour rés;

int ways = dfs(hat + 1, masque); // sauter ce chapeau
pour (int person : people[hat]) {
si ((masque et (1 << personne)) != 0) {
les voies += dfs(hat + 1, masque ^ (1 < < personne));
si (ways >= MOD) façons -= MOD;
}
}
retour res = voies;
}
}
«» "

5.2 Python

'`python
Solution de classe:
MOD = 10**9 + 7

Numéro Ways(self, chapeaux: List[List[int]]) -> Int:
Self.n = len(hats)
Les gens liste de personnes qui aiment ce chapeau
personnes = [[] pour _ dans l'intervalle(41)]
pour p, h_list dans l'énumération(hats):
pour h dans h_list:
people[h].append(p)

# dp[hat][masque] avec chapeau à base de 1
self.dp = [[-1] * (1 << self.n) pour _ dans l'intervalle(41)]
full_mask = (1 << self.n) - 1
return self._dfs(1, pleine_masque)

def _dfs(self, chapeau: int, masque: int) -> Int:
si masque == 0:
retour 1
si chapeau > 40:
retour 0

si self.dp[hat][masque] != - 1 :
retour self.dp[hat][masque]

ways = self._dfs(hat + 1, masque) # skip current hat
pour personne dans les gens[hat]:
si masque & (1 << personne):
ways += self._dfs(hat + 1, masque ^ (1 << personne))
ways %= self. MOD

auto.dp[hat][masque] = voies
retour
«» "

> **Astuce** – Dans Python, vous pouvez utiliser `lru_cache` pour une implémentation légèrement plus propre, mais le tableau manuel ci-dessus vous donne le contrôle de la mise en page de la mémoire.

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
static const int MOD = 1'000'000'007;
l'élément n;
vector<vector<int>> dp; // dp[hat][masque], chapeau à base de 1
vectorielle<vector<int>> personnes; // personnes[hat] -> liste des indices des personnes

nombre intWays(vecteur<vecteur<int>>& chapeaux) {
n = chapeaux.taille();
l'attribution de personnes(41, {});
pour (int p = 0; p < n; ++p) {
pour (int h : hats[p]) people[h].push_back(p);
}

dp.assign(41, vecteur<int>(1 << n, -1));
retour dfs(1, (1 << n) - 1);
}

particulier:
Int dfs(poitrine, masque int) {
si (!mask) retourne 1; // toutes les personnes affectées
si (hat > 40) retourner 0; // aucun chapeau restant

int& res = dp[hat][masque];
Si (res != -1) retour rés;

longues distances = dfs (hat + 1, masque); // chapeau de saut
pour (int person : people[hat]) {
si (masque et (1 << personne)) {
les voies += dfs(hat + 1, masque ^ (1 < < personne));
Voies %= MOD;
}
}
retour res = (int)ways;
}
};
«» "

---

- Oui. 6. Harnais d'essai rapide (toutes langues confondues)

Texte
Entrée : chapeaux = [[3,4], [4,5], [5,6]]
Produit : 6
Explication : 3 personnes, 3 chapeaux – chaque personne aime un chapeau différent, tous 3 ! = 6 façons.

Entrée : chapeaux = [[3,5], [3,5], [3,5]]
Sortie : 0
Explication : 3 personnes veulent tous des chapeaux 3 ou 5 – seulement deux chapeaux disponibles, impossible.

Entrée : chapeaux = [[2], [1, 2], [1, 3]]
Produit : 2
Explication : Personne0 → 2; Personne1 → 1; Personne2 → 3 OU Personne1 → 2, Personne2 → 1.
«» "

Vous pouvez coller n'importe lequel des éléments ci-dessus dans l'éditeur de LeetCode. L'exécution est généralement < 100 ms sur toutes les langues.

---

- Oui. 7. Que dire à l'intervieweur

1. **Pourquoi les chapeaux comme la boucle extérieure? * *
Parce que l'ensemble de chapeaux est fixe (40) alors que le nombre de personnes est minuscule, itérer sur les chapeaux garde l'état petit (2n) et garantit que nous ne reculons jamais sur les gens.

2. **Définition de l'État** – "mask" = "unassigned people".
Afficher un diagramme simple: `masque = 0b101` → personnes 0 & 2 ont encore besoin de chapeaux.

3. **Transition** – Il faut sauter le chapeau ou l'assigner à une des personnes libres qui l'aime. (en milliers de dollars)
Mentionnez l'opération modulo pour garder la réponse positive.

4. **Edge Cases** – Si toutes les personnes sont déjà assignées nous sommes fait; si nous manquons de chapeaux tôt nous retournons 0. (en milliers de dollars)

5. **Complexité** – temps et mémoire d'O(40·2n); avec `n=10` qui est ~4 × 104 cellules – trivial pour les machines actuelles. (en milliers de dollars)

6. **Pourquoi pas un simple retour en arrière? * *
Le suivi serait toujours « 40 · 2n », mais sans mémoisation, vous recalculeriez les sous-problèmes plusieurs fois. DP le réduit à un calcul par paire `(hat, masque)`.

---

- Oui. 8. Pièges courants et comment les éviter

Piège
- Oui.
**Missing modulo** – les résultats enveloppent autour des nombres négatifs.
**1-based / 0-based confusion**. Pas besoin de soustraire 1 n'importe où. Autres
Autres **Grand tableau du PDD** En sécurité. Autres
**Profondeur de la récursion**=Profondeur maximale 41 – sûre en Java, Python, C++. Autres
En Java, n'oubliez pas d'initialiser les indices «people[0]» (non utilisés) ou «garde». Autres

---

- Oui. 9. A emporter pour votre prochaine entrevue

* ** Expliquez clairement l'état** – beaucoup de candidats sautent directement pour revenir en arrière et se coincer.
* **Afficher la mise en page de la table DP** – dessiner une matrice minuscule ('hat` vs `masque`).
* ** Démontrer un cas de base** – -masque == 0 → 1-.
* **Mention le modulo tôt** – les intervieweurs aiment voir que vous êtes conscient du débordement entier.
* **Time/Space** – un rapide 40·2n = 40 960.

Avec cela, vous impressionnerez les gestionnaires d'embauche qui apprécient la pensée algorithmique propre et la capacité de coder dans plusieurs langues.

---

## 10. Mot final

La partie **good** : un DP concis qui tourne en quelques millisecondes.
La partie **mauvais** : beaucoup de candidats oublient le tour de chapeau ou le modulo.
La partie **ugly** : une seule cellule de tableau mal indexée peut briser toute la solution.

En maîtrisant ce modèle, vous serez prêt à as non seulement LeetCode 1434 mais aussi ** toute question d'entrevue** qui implique l'attribution d'un petit nombre d'entités à un plus grand bassin de catégories.

Bonne chance pour votre entretien de codage, et hacking heureux!