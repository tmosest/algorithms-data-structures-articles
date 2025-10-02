---
titre: LeetCode 2786. Visitez Array Positions pour maximiser le score -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2786 – *Visitez les positions pour maximiser la note*
Les bons, les mauvais et les affreux
> **Vous voulez passer votre prochain entretien? * *
> Apprenez le truc DP le plus efficace, voyez-le en **Java, Python et C++**, et obtenez un billet de blog prêt à la copie que vous pouvez publier sur LinkedIn, Medium ou votre portfolio personnel.

---

### TL;DR

Langue Heure Espace Code
- C'est quoi ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
**Python******O(n)****O(1)**"def maxScore(self, nombres: List[int], x: int) -> int"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres

L'algorithme conserve **deux scores en cours d'exécution** – un pour le meilleur total si le dernier nombre visité est **even** et un pour **odd**.
À chaque position, nous décidons de venir de la même parité (sans pénalité) ou de la parité opposée (payer `x`).
La clé est la simple récurrence:

«» "
dp[parité] = max(
dp[parité] + nombres[i], // même parité
dp[parité^1] - x + nombres[i] // parité opposée
)
«» "

Parce que nous ne conservons que deux numéros, le coût de l'espace est constant.

---

Récapitulation des problèmes

> **Vous êtes debout à l'index 0 d'un tableau "nums".**
> Vous pouvez sauter vers n'importe quel index `j > i`.
> L'index de visite `i` ajoute `nums[i]` à votre score.
> Si vous sautez de `i` à `j` et `nums[i]` et `nums[j]` ont des parités différentes, vous perdez `x` points.
> **Objectif:** maximiser le score total après n'importe quel nombre de sauts (y compris rester au départ).

---

Pourquoi le DP fonctionne ?

La décision à l'index "i" dépend uniquement:

1. La note **maximum** réalisable se terminant par un nombre pair avant "i".
2. La note **maximum** réalisable se terminant par un nombre impair avant "i".

Tous les mouvements futurs sont indépendants des indices exacts visités, seulement de la parité du dernier nombre.
Un PDD à deux états est donc suffisant.

---

L'algorithme

Étape Ce que nous stockons Actualiser la règle Pourquoi ça marche
- C'est quoi ?
**Initial**= `dp[0] = dp[1] = -x`= `dp[nums[0]&1] = nombres[0]`= Nous commençons à l'index 0. L'autre parité est encore impossible, alors placez-la à une très petite valeur (`-x`). Autres
Autres **I = 1 ... n-1**= Pour le nombre actuel `cur = nombres[i]`="dp[cur&1] = max(dp[cur&1], dp[cur&1^1] - x) + cur`=" Deux options : proviennent de la même parité (aucune pénalité) ou de la parité opposée (soustraire `x`). Prends le meilleur. Autres
**Résultat**="max(dp[0], dp[1])="Le meilleur score indépendamment de la parité du dernier élément visité. Autres

> **Note:** Toutes les opérations sont 'O(1)` par élément, ce qui donne un algorithme global linéaire du temps.

---

Code en trois langues

C'est pas vrai. Java

"Java
solution de classe {
public long maxScore(int[] nums, int x) {
long[] dp = nouveau long[]{-x, -x}; // dp[0] = pair, dp[1] = impair
dp[nums[0] et 1] = nombres[0]; // commencer à l'index 0
pour (int i = 1; i < nombres de longueur; i++) {
parité int = nombres[i] & 1;
dp[parité] = Math.max(dp[parité], dp[parité ^ 1] - x) + nombres[i];
}
retour Math.max(dp[0], dp[1]);
}
}
«» "

# # # # # #

'`python
Solution de classe:
def maxScore(self, nombres: List[int], x: int) -> Int:
dp = [-x, -x] # dp[0] pair, dp[1] impair
dp[nums[0] & 1] = nombres[0] # commencer à l'index 0
pour num in nums[1:]:
p = nombre et 1
dp[p] = max(dp[p], dp[p ^ 1] - x) + num
retour max(dp)
«» "

C'est vrai. C++

'`cpp
solution de classe {
public:
long maxScore(vector<int>& nums, int x) {
long dp[2] = {-x, -x}; // dp[0] pair, dp[1] impair
dp[nums[0] et 1] = nombres[0]; // début
pour (int i = 1; i < nums.size(); ++i) {
int p = nombres[i] & 1;
dp[p] = max(dp[p], dp[p ^ 1] - x) + nombres[i];
}
retour max(dp[0], dp[1]);
}
};
«» "

---

Analyse de complexité

Complexité
C'est pas vrai.
**Heure**="O(n)" – on passe par le tableau. Autres
**Espace** – seulement deux entiers longs. Autres

Même pour `n = 10^5` cela fonctionne confortablement sous 0,1 s dans les trois langues.

---

Pourquoi ça bat Brute-Force

Une approche naïve tenterait tous les sous-ensembles ou toutes les séquences de saut – le temps exponentiel ('O(2^n)').
Même une programmation dynamique qui stocke le score maximal pour chaque indice (`dp[i]`) devrait tenir compte de tous les indices précédents, ce qui entraînerait un temps "O(n^2)".

Notre PDD à deux états effondre les possibilités exponentielles en deux nombres parce que la parité est le seul état qui compte pour les futures transitions. C'est le moment qui transforme un problème d'interview difficile en une solution propre et optimale.

---

Structure du blog optimisée par le SEO

Vous trouverez ci-dessous un squelette que vous pouvez copier dans Medium, Dev.to ou LinkedIn. Ajoutez des images ou des captures d'écran de code pour un meilleur engagement.

```markdown
♪ Visitez Array Positions pour maximiser le score – LeetCode 2786

Résumé du problème

...

Les clés à emporter

- Le PDD à deux états (même/odd) réduit la complexité de O(n2) à O(n).
- L'espace peut être réduit à O(1) en ne conservant que les derniers scores.
La récurrence est simple: `dp[p] = max(dp[p], dp[p^1] - x) + cur`.

Java / Python / C++ Code

### Java
"Java
// bloc de code
«» "

Python
'`python
# bloc de code
«» "

C++
'`cpp
// bloc de code
«» "

Résultats

Temps (ms)
- C'est quoi ?
C'est pas vrai.
Python :
C++

Pièges communs d'entrevue

1. Oublier d'initialiser l'impossible parité avec un nombre très négatif.
2. Mélanger les opérations de parité bitwise.
3. Penser à un tableau `dp[i]` est nécessaire – il n'est pas.

Comment maîtriser des problèmes similaires

- Concentrez-vous sur la compression d'état* : recherchez un minimum de variables qui saisissent les décisions futures.
- Pratiquer la parité et la manipulation bit – de nombreux problèmes DP dépendent d'eux.

Conclusion

[Vos remarques finales ici. Encourager les lecteurs à essayer le problème, à partager leurs solutions ou à poser des questions.]

«» "

---

Bonus: Explication visuelle (facultative)

Vous pouvez ajouter un diagramme simple:

«» "
Indice 0 (even/odd) ─ ► Indice 1 (even) ─ ► Indice 2 (even/odd) ─ ► ...
- Oui.
Pénalité = x Pénalité sans pénalité

«» "

Marquez les deux scores et montrez comment la transition prend le maximum des deux options.

---

Note finale

Cette solution est **prête pour les entrevues de production** – collez-la dans votre cahier, pratiquez l'expliquer dans une interview simulée, et regardez l'intervieweur hoche la tête.

Bonne chance, et le codage heureux!