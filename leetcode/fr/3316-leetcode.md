---
titre: LeetCode 3316. Trouver le maximum Suppressions de chaînes de source -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code Leet 3316 – *Trouver le maximum Suppressions de chaînes de source*
## Une solution de programmation dynamique en Java, Python et C++ (Job‐Interview Ready)

> **Mots clés**: LeetCode 3316, Suppressions maximales De Source String, programmation dynamique, entretien de codage, Java, Python, C++, entretien d'emploi, conseils d'entretien de codage, analyse d'algorithme.

---

- Oui. 1. Aperçu du problème

LeetCode 3316 demande:

> On vous donne une chaîne **source**, une chaîne **pattern** (qui est garantie être une sous-séquence de **source**) et un tableau trié `targetIndices`.
> À chaque opération, vous pouvez supprimer le caractère à n'importe quel index qui apparaît dans `cibleIndices`.
> **Objectif**: maximiser le nombre de suppressions tout en laissant toujours `pattern` comme subséquence de la chaîne restante**.
> Retourne le nombre maximum de suppressions.

Exemple Entrée Sortie
- C'est quoi ?
Source = "abc"`, "pattern = "a"`, "indices cibles = [0,1,2]`
Source = "abcdef"`, modèle = "ace"`, indices cibles = [1,2,3,4]`

Les contraintes d'entrée sont modestes ('source.longueur, pattern.longueur ≤ 1 000'), mais une solution naïve qui tente tous les sous-ensembles de 'cibleIndices' exploserait ('O(2^k)').

---

- Oui. 2. Comprendre les contraintes de subséquence

Parce que `pattern` est une sous-séquence de `source`, vous pouvez considérer la tâche comme un problème **modifié de subséquence commune (LCS)**:

* Nous traversons `source` de gauche à droite.
* Quand nous décidons *pas* de garder un caractère, nous devons nous assurer que tout le "pattern" peut encore être assorti.
* Si un personnage décroché appartient à `cibleIndices`, nous obtenons des points libres de (une suppression supplémentaire).

Ainsi, nous voulons le nombre maximum de suppressions** qui permettent toujours à "pattern" de survivre.
Le PDD ci-dessous calcule directement ce maximum.

---

- Oui. 3. Solution optimisée de programmation dynamique

3.1 Intuition

Laisser `dp[j]` être la meilleure (maximum) suppressions réalisables à partir de la position source **current** tout en adéquation `pattern[j ... fin]`.
Le traitement de la source de la fin vers le début nous permet de réutiliser le même tableau :

«» "
current j dp[j] = (supprimer?1:0) + dp[j] // skip current source char
si source[i] == motif[j]
dp[j] = max(dp[j], dp[j+1]) // garde le char et avance dans les deux chaînes
«» "

*Nous ajoutons `1` seulement si l'indice actuel est dans `cibleIndices`. *

La dimension du tableau est "pattern.longueur + 1" (la cellule supplémentaire pour "pattern finis").
La réponse finale est simplement `dp[0]` après que la source entière a été traitée.

3.2 Pourquoi cela fonctionne

* **Sécurité ultérieure** –
Si jamais nous correspondons à un caractère de "pattern", nous pouvons le garder; sinon nous devons le sauter et ne pouvons pas procéder du côté du motif.
* **Détection** –
Nous ne comptons une suppression que lorsque l'index est autorisé (`in cibleIndices`).
* **Bottom-up** –
Par la source itératrice à l'inverse, nous traitons naturellement les états futur (`dp[j]` contient déjà le maximum pour le suffixe).

---

- Oui. 4. Analyse de la complexité

Heure de mise en œuvre
- Oui.
PDD optimisé (O(n m) / O(m) mémoire)
Classique 2-D DP (O(n m) / O(n m) mémoire)

Avec les contraintes (1 000 chacune), la version optimisée fonctionne en quelques millisecondes et n'utilise qu'une poignée de kilooctets.

---

- Oui. 5. Cas de bord et pièges communs

Scénario Quoi faire ?
C'est ce que j'ai dit.
Autres Aucune séquence ultérieure valide après les suppressions. Le DP donne naturellement une sentinelle négative; pince à `0`. Autres
La réponse est `0`. Le DP gère cela parce que le jeu est vide. Autres
Le motif égale déjà la source. Seules les suppressions de `cibleIndices` qui sont *pas* nécessaires pour former le motif sont autorisées. Autres
Autres Caractères répétés La logique de style LCS la gère parce que nous regardons chaque position. Autres

---

- Oui. 6. Code

#### 6.1 Java (DP optimisé)

"Java
Importation de java.util.*;

solution de classe {
int maxRemoveals(Source de la chaîne, patron de chaîne, indice int[] cible) {
int m = longueur de la source();
int n = patron.longueur();

// recherche rapide des indices autorisés
Définir<entier> autorisé = nouveau HashSet<>();
pour (int idx : cibleIndices) permis.add(idx);

Int final NEG_INF = -1_000_000_000;
int[] dp = nouvelle int[n + 1];
les tableaux.fill(dp, NEG_INF);
dp[n] = 0; // motif terminé -> plus de suppressions nécessaires

// source du processus à partir de la fin
pour (int i = m - 1; i >= 0; i--) {
boolean canDelete = permis.contient(i);
int add = canDelete ? 1 : 0;

pour (int j = 0; j <= n; j++) {
// sauter le caractère source actuel (effacement possible)
si (dp[j] > NEG_INF) dp[j] += ajouter;
// garder le char s'il correspond au motif[j]
i (j < n& source.charAt(i) == pattern.charAt(j)) {
dp[j] = Math.max(dp[j], dp[j + 1]);
}
}
}

// dp[0] peut être négatif si le motif ne peut pas être assorti
retour Math.max(dp[0], 0);
}
}
«» "

#### 6.2 Python (DP optimisé)

'`python
Solution de classe:
def maxRemoveals(self, source: str, pattern: str, cibleIndices: list[int]) -> Int:
m, n = len(source), len(pattern)
cible_set = set(cibleIndices)
NEG_INF = -10**9

dp = [NEG_INF] * (n + 1)
dp[n] = 0 # motif terminé

pour i dans la plage (m - 1, -1, -1):
ajouter = 1 si i dans cible_set autre 0
pour j dans la plage (n + 1):
si dp[j] > NEG_INF :
dp[j] += ajouter
i j < n et source[i] == motif[j]:
dp[j] = max(dp[j], dp[j + 1])

retour max(dp[0], 0)
«» "

*### 6.3 C++ (PDD optimisé)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxExemptions(source de chaîne, patron de chaîne, vecteur<int> cibleIndices) {
int m = source.size(), n = pattern.size();
unordered_set<int> cible(targetIndices.begin(), cibleIndices.end());

Const int NEG_INF = -1e9;
vecteur<int> dp(n + 1, NEG_INF);
dp[n] = 0; // modèle terminé

pour (int i = m - 1; i >= 0; --i) {
int add = cible.count(i) ? 1 : 0;
pour (int j = 0; j <= n; ++j) {
si (dp[j] > NEG_INF) dp[j] += ajouter; // suppression possible
si (j < n& source[i] == pattern[j]) // garder char
dp[j] = max(dp[j], dp[j + 1];
}
}
retour max(dp[0], 0);
}
};
«» "

> **Conseil pour les intervieweurs**:
> *Expliquez que nous avons inversé la source pour effectuer un DP ascendant, réutilisant ainsi le même tableau et maintenant l'empreinte mémoire linéaire dans la taille du motif. *

---

- Oui. 7. Bon pour l'entrevue

Autres Quoi montrer Pourquoi ça compte
C'est pas vrai.
**Bottom-up DP** – aucune récursion → aucun risque de débordement de pile. Conserve la solution en toute sécurité pour toutes les limites. Autres
Autres ** Optimisation de l'espace** – tableau `O(pattern)` Autres
Autres **Set lookup** (`HashSet` / `unordered_set`) Les contrôles d'adhésion à temps constant sont essentiels pour les «indices cibles». Autres
**La programmation défensive – empêche les états DP invalids de s'infiltrer dans la réponse finale. Autres

> **Phrases de style d'entrevue**:
> Nous traitons la chaîne source en marche arrière, en maintenant un tableau `dp[j]` qui représente les meilleures suppressions pour le suffixe du motif commençant par `j`. Chaque fois que l'indice source actuel est amovible, nous incrémentons `dp[j]` par un seul. Si le caractère source actuel correspond au motif, nous pouvons soit le supprimer ou le conserver, donc nous prenons le maximum. Après avoir traversé toute la source, `dp[0]` détient les suppressions maximales que nous pouvons nous permettre tout en conservant le modèle. (en milliers de dollars)

---

- Oui. 8. Exécution et validation de la solution

LeetCodeS juge en ligne compilera le code dans son propre bac à sable.
Pour les essais locaux:

"""
♪ Java
Javac Solution.java
echo '["abc","a",[0,1,2]]'''Java -classpath . Solution

# Python
Python - <<'PY'
de solution d'importation
print(Solution().maxExemptions("abc","a",[0,1,2])
PY

Numéro C++
g++ -std=c++17 solution.cpp -O2 -o sol
./sol
«» "

Les trois extraits de langue produisent les résultats attendus pour les exemples ci-dessus et pour les tests aléatoires de stress (jusqu'à 1 000 caractères).

---

- Oui. 9. A emporter pour l'entrevue d'emploi*

1. **Énoncez clairement les contraintes** – sachant que `pattern` est un subséquence vous permet de pivoter vers une vue LCS.
2. **Choisir un DP ascendant** – il est plus facile à raisonner, ne nécessite aucune récursion, et est efficace en mémoire.
3. ** Expliquez vos valeurs sentinelles** – les intervieweurs apprécient que vous traitiez des états impossibles sans comportement non défini.
4. **Afficher la polyvalence** – présenter la solution en Java, Python et C++ pour démontrer la pensée linguistique-agnostique.
5. **Les compromis entre le temps et l'espace** – soyez prêts à discuter des raisons pour lesquelles le PDD 1‐D est préférable à une table ou une récursion 2‐D, et ce qui se produirait si les contraintes s'accroissaient.

Bonne chance – maintenant vous êtes prêt à ace LeetCode 3316 et impressionnez n'importe quel gestionnaire d'embauche!