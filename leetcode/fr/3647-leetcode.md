---
titre: LeetCode 3647. Poids maximum en deux sacs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Ci-dessous se trouvent trois solutions **ready‐to‐run** – une en Java, Python et C++ – qui résolvent le LeetCode 3647.
Tous les trois utilisent la même idée de programmation dynamique : traiter les deux sacs comme deux dimensions de sac à knaps une fois.

Langue Complexité Remarques
C'est quoi, ça ?
"O(n · w1 · w2)" temps, "O(w1 · w2)" espace
"Python" "O(n · w1 · w2)" temps, "O(w1 · w2)` espace" Même DP, utilise une liste de listes
"O(n · w1 · w2)" temps, "O(w1 · w2)` espace" Utilisations "vecteur<vecteur<int>" Autres

---

#### 1.1 Java

"Java
// Fichier: Solution.java
Importation de java.util.*;

solution de classe publique {
poids (int[] poids, int w1, int w2) {
// Tableau DP: dp[a][b] = poids maximal pouvant être transporté
// avec capacité a en sac1 et capacité b en sac2
int[] dp = nouvelle int[w1 + 1][w2 + 1];

pour (en poids : poids) {
// itérer en arrière pour éviter de réutiliser le même élément
pour (int a = w1; a >= 0; a--) {
pour (int b = w2; b >= 0; b--) {
Int cur = dp[a][b];
si (a >= poids) {
cur = Math.max(cur, dp[a - poids][b] + poids);
}
si (b >= poids) {
cur = Math.max(cur, dp[a][b - poids] + poids);
}
dp[a][b] = cur;
}
}
}
retour dp[w1][w2];
}

// -------- Démo Main (facultatif) ---------
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.maxPoids(nouvelle int[[]{1, 4, 3, 2}, 5, 4)); // 9
Système.out.println(s.maxPoids(nouvelle int[[]{3, 6, 4, 8}, 9, 7)); // 15
Système.out.println(s.maxPoids(nouvelle int[]{5, 7}, 2, 3)); // 0
}
}
«» "

---

#### 1.2 Python

'`python
# Fichier : solution. py
de taper l'importation Liste

Solution de classe:
def maxPoids(self, poids: List[int], w1: int, w2: int) -> Int:
# dp[a][b] = poids maximal réalisable avec capacités a, b
dp = [[0] * (w2 + 1) pour _ dans la plage (w1 + 1)]

pour poids en poids:
pour une plage(w1, -1, -1):
pour b dans l'intervalle(w2, -1, -1):
cur = dp[a][b]
si >= poids:
cur = max(cur, dp[a - poids][b] + poids)
si b >= Poids:
cur = max(cur, dp[a][b - poids] + poids)
dp[a][b] = cur
retour dp[w1][w2]

♪ - Oui. Démonstration...
si __nom__ == "__main__" :
s = Solution()
print(s.maxPoids([1, 4, 3, 2], 5, 4)) # 9
print(s.maxPoids([3, 6, 4, 8], 9, 7)) # 15
print(s.maxPoids([5, 7], 2, 3)) # 0
«» "

---

*## 1.3 C++

'`cpp
// Fichier: solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxWeight(vector<int>& poids, int w1, int w2) {
vector<vector<int>> dp(w1 + 1, vector<int>(w2 + 1, 0));

pour (en poids : poids) {
pour (int a = w1; a >= 0; --a) {
pour (int b = w2; b >= 0; --b) {
Int cur = dp[a][b];
si (a >= poids)
cur = max(cur, dp[a - poids][b] + poids);
si (b >= poids)
cur = max(cur, dp[a][b - poids] + poids);
dp[a][b] = cur;
}
}
}
retour dp[w1][w2];
}
};

// - Oui. Démonstration...
Int main() {
Solution s;
<< s.maxPoids({1, 4, 3, 2}, 5, 4) << endl; // 9
<< s.maxPoids({3, 6, 4, 8}, 9, 7) << endl; // 15
<< s.maxPoids({5, 7}, 2, 3) << endl; // 0
retour 0;
}
«» "

---

- Oui. 2. Article de blog – Poids maximal dans deux sacs: le bon, le mauvais, et le mauvais

> Si vous pouvez résoudre un problème qui ressemble à un Knapsack 0-1, vous êtes essentiellement un programmeur.

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Approches naïves]
3. [Programmation dynamique – la tache douce] (#programmation dynamique-le-spot doux)
4. [Le bon, le mauvais, et le mauvais] (# le bon, le mauvais, le mauvais)
5. [Complexité temps-espace] (#complexité temps-espace)
6. [Pourquoi cela compte dans les entrevues](#pourquoi-ce-questions-dans-entrevues)
7. [Traitement final] (#Traitement final)

---

### Aperçu du problème <un nom="problème-overview"></a>

> ** Poids maximal en deux sacs* *
> *LeetCode 3647 – Moyen*

On vous donne un tableau `poids` d'entiers positifs et deux entiers `w1`, `w2` représentant les limites de capacité de deux sacs. Chaque article peut entrer dans **au plus un** sac (ou ne pas être utilisé). Le but est de **maximiser le poids total** qui finit dans les deux sacs.

*Contrôles*
- "1 ≤ poids. longueur ≤ 100'
- «1 ≤ poids[i] ≤ 100»
- `1 ≤ w1, w2 ≤ 300`

Étant donné que les capacités sont relativement petites (= 300), une solution de programmation dynamique avec un espace d'état `O(w1 · w2)` est parfaitement réalisable.

---

### Approches naïves <une approche naïve></a>

1. **Retraçage de la force brute* *
Énumérer chaque affectation de chaque article dans le sac 1, le sac 2, ou - non utilisé. (en milliers de dollars)
*Complexité*: `3^n` – complètement impossible même pour `n = 20`.

2. **Récursif haut-down avec mémoisation* *
Une récursion typique de 0-1 knapsack avec une dimension supplémentaire pour le second sac.
*Pro*: Facile à comprendre.
*Cons*: le tableau de mémoisation 3 dimensions peut devenir volumineux; risque de débordement de la pile pour une récursion profonde.

Les deux méthodes naïves ont rapidement frappé le mur dans de vrais scénarios d'interview – elles sont trop lentes et difficiles à expliquer en moins d'une minute.

---

### Programmation dynamique – Le spot doux <un nom="programmation dynamique-le-spot doux"></a>

C'est vrai. 1. Knapsack à deux dimensions

L'idée fondamentale : traiter les deux capacités comme un *grid* d'Etats.
`dp[a][b]` = poids total maximal pouvant être atteint avec *au maximum* `a` capacité dans le sac 1 et `b` capacité dans le sac 2.

C'est vrai. 2. Transition des États

Pour chaque poids «x»:

«» "
pour une de w1 à 0
pour b de w2 à 0
cur = dp[a][b]
si a >= x: cur = max(cur, dp[a - x][b] + x)
si b >= x: cur = max(cur, dp[a] [b - x] + x)
dp[a][b] = cur
«» "

*Pourquoi les boucles inversées? *
Nous mettons à jour des capacités élevées à faibles afin que chaque article soit utilisé au plus une fois. L'ordre inversé garantit que nous ne lisons jamais un état qui inclut déjà le point actuel.

C'est vrai. 3. Réponse finale

«dp[w1][w2]» détient le poids total optimal.

---

### Le bon, le mauvais, et l'horrible <un nom "le bon, le mauvais"></a>

Aspect du bien
- C'est quoi ?
**Concept**= Extension knapsack classique 0-1 – simple à expliquer. Nécessite *deux* dimensions; peut être confus pour les débutants. Un DP naïf 3-dimensionnel est souvent la solution de "gugly" les gens essaient d'abord et se coincer. Autres
**Mise en œuvre**= Boucles compactes imbriquées – faciles à lire et à déboguer. Empreinte mémoire `O(w1 · w2)` peut être grande si les capacités sont proches de 300. Récursion avec un tableau 3-D peut déborder la pile ou appuyez sur Java. Autres
**Heure**=O(n · w1 · w2)=– assez rapide pour des limites données.= Si vous bouclez accidentellement `0` vers le haut au lieu de vers le bas, vous compterez plusieurs éléments. L'arrimage ('3^n') est impossible au-delà de très petits cas d'essai. Autres
**L'espace**=Le tableau 2D seulement – pas de pile de récursion supplémentaire. Pour extrêmement grand `w1` ou `w2` vous aviez manqué de mémoire. La mémoisation en haut en bas peut utiliser une carte 3-D qui est moins facile à cacher. Autres
**Interview Impact** Démontre une attention particulière aux conditions limites. Montre la capacité de reconnaître et d'éviter les explosions exponentielles. Autres

---

### Complexité temporelle et spatiale <un nom="complexité temporelle-espace"></a>

L'approche Temps Espace
- C'est quoi ?
Brute-Force Autres
Haut de la page Autres
** O(n · w1 · w2) Autres

Pour les contraintes données (`n ≤ 100`, `w1,w2 ≤ 300`), le PDD ascendant utilise au maximum `301 × 301 ' 90 601` entiers – bien dans n'importe quelle pile moderne.

---

- Oui. Pourquoi cela compte-t-il dans les entrevues <un nom=pourquoi-ce-question-dans-entrevues"></a>

- **Showcase DP Mastery**: La plupart des intervieweurs aiment vous voir résoudre une variation du problème Knapsack. Il prouve que vous pouvez gérer l'optimisation combinatoire.
- **Explain Inverse Loops**: Une partie subtile mais essentielle de la transition, manquante, peut conduire à de mauvaises réponses. Il teste votre capacité à penser aux états de "usagé" vs "unusagé".
- ** Optimisation de l'espace**: Réduire de 3-D à 2-D démontre que vous pensez à la mémoire d'exécution et à la localisation du cache.
- **Trappes d'évitement**: La solution récursive provoque souvent des débordements de piles. Si vous reconnaissez cela et passez à une version itérative, vous impressionnerez.
- **Durée sensible**: Vous finirez dans la fenêtre de l'entrevue (30 minutes) et aurez toujours le temps de clarifier les questions.

---

### Takeaway final <un nom="Takeaway final"></a>

> Si vous pouvez résoudre cela avec un DP 2-D, vous êtes prêt à affronter *tout* problème d'emballage combinatoire. (en milliers de dollars)

Le problème *Maximum Weight in Two Bags* est un "safe-harbor" dans les piles d'interviews : il est assez complexe pour tester votre profondeur algorithmique mais assez simple pour être expliqué en moins d'une minute.
Utilisez l'approche **bottom-up 2-D DP** – c'est la solution de "good" qui évite les écueils de "bad" d'une table de mémos 3-D et contrepasse le "ugly" exponentiel backtracking.

Bon codage ! C'est ce qu'il a dit.

---

Mots clés

- LeetCode 3647
- Solution Poids maximum en deux sacs
- Questions d'entrevue sur la programmation dynamique
- 0-1 Knapsack deux sacs
- Problèmes de LeetCode moyen
- Optimisation de l'espace du PDD
- Sac à dos bidimensionnel
- Meilleures pratiques d'entretien de programmation

*(Sentez libre de copier/coller les extraits de code ci-dessus, lancez-les dans votre IDE, et modifiez la démo principale pour tester plus de cas de bord.) *

---

> **Vous voulez plus le bon, le mauvais et les articles laids** Abonnez-vous à mon bulletin et obtenez les * pièges d'entrevue les plus courants* résolus, *étape par étape*.

---

**Auteur**: *[Votre nom]* – Ingénieur à fond, contributeur open-source et évangéliste LeetCode.
LinkedIn: <https://linkedin.com/in/votre profil>
GitHub: <https://github.com/yourgithub>
Blog: <https://yourblog.com>

---


---

> *Si vous utilisez cet article pour un site personnel, n'oubliez pas de créditer LeetCode et la description officielle du problème. *