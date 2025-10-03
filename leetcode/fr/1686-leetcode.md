---
Titre: LeetCode 1686. Jeu de pierre VI -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1686: Jeu de pierre VI

> **Alice** et **Bob** prennent à tour de rôle la cueillette d'une pierre d'un tas de pierres `n`.
> Chaque pierre *i* a deux valeurs:
> * `aliceValues[i]` – points Alice reçoit si elle prend la pierre
> * `bobValues[i]` – points que Bob reçoit s'il prend la pierre
> Les deux joueurs jouent **optimally** et se connaissent les listes de valeurs.
> Après que toutes les pierres soient prises, celui qui a le plus grand score total gagne
> (`1` pour Alice, `-1` pour Bob, `0` pour une cravate).

Contraintes
«» "
1 ≤ n ≤ 105
1 ≤ aliceValues[i], bobValues[i] ≤ 100
«» "

---

- Oui. 2. Intuition – Pourquoi "Trier par a+b"?

Pensez à la différence entre les deux scores finals.
Si Alice prend la pierre `i` elle gagne `aliceValues[i]`.
Si Bob prenait la même pierre plus tard, il aurait gagné "bobValues[i]".

Au lieu d'examiner les deux valeurs séparément, observez que **le choix qui maximise la différence* `alice - bob` équivaut à maximiser la somme `alice + bob`**:

«» "
Alice prend la pierre i → +aliceValues[i] pour Alice
Bob prend la pierre i → -bobValues[i] pour Alice (parce que les points de Bob ne sont pas Alice)

Impact de différence = aliceValues[i] + bobValues[i]
«» "

Par conséquent, à chaque tour le joueur dont le tour est de saisir la pierre restante avec la plus grande ** valeur combinée** `alice + bob`.
Une fois les pierres triées par cette clé, les joueurs alternent simplement les choix :

* tourner 0 (Alice) → prendre la première pierre dans l'ordre trié
* tourner 1 (Bob) → prendre la deuxième pierre
* ... et ainsi de suite.

Parce que chaque tour enlève la pierre restante *meilleur* pour le joueur actuel, cette stratégie gourmande est optimale.

---

- Oui. 3. Algorithme

1. Créer une liste de `n` triples `(alice, bob, sum = alice + bob)`.
2. Triez la liste dans l'ordre **descendant** du «somme».
3. Simuler le jeu:
* Pour des indices égaux (`0,2,4,...`) ajouter `alice` au score d'Alice.
* Pour les indices impairs (`1,3,5,...`) ajouter `bob` au score de Bob.
4. Comparez les deux totaux et retournez `1`, `-1` ou `0`.

complexité du temps : **O(n log n)** (le tri domine).
complexité spatiale : **O(n)** pour la liste auxiliaire.

---

- Oui. 4. Mise en œuvre des références

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
classe statique privée Pierre {
alice, bob, somme;
Pierres (alices, bob int) {
ceci.alice = alice;
ce.bob = bob;
ce.sum = alice + bob;
}
}

pierre d'inte publique GameVI(int[] aliceValues, int[] bobValues) {
int n = aliceValues.longueur;
Pierre[] pierre = nouvelle pierre[n];
pour (int i = 0; i < n; i++) {
pierre[i] = nouvelle pierre(aliceValues[i], bobValues[i]);
}

Tableaux.sort(pierres, (s1, s2) -> (s2.sum, s1.sum)

long aliceScore = 0, bobScore = 0;
pour (int i = 0; i < n; i++) {
Si (i et 1)] 0) {/ A son tour
Alice Score += pierres[i].alice;
} autres { // Le tour de Bob
bobScore += pierres[i].bob;
}
}

retour Long.compare(aliceScore, bobScore);
}
}
«» "

> **Pourquoi "long"?**
> Les scores peuvent être jusqu'à `n * 100` (`107`), en toute sécurité à l'intérieur `int`, mais l'utilisation `long` élimine tout risque de débordement lorsque le compilateur optimise.

---

4.2 Python

'`python
Solution de classe:
def pierre GameVI(self, aliceValues: List[int], bobValues: List[int]) -> Int:
# Créer une liste de (somme, alice, bob)
pierres = triées(
[(a + b, a, b) pour a, b en zip(aliceValues, bobValues)],
inverse=True
)

alice, bob = 0, 0
pour i, (_, a, b) dans l'énumération (pierres):
i % 2 == 0 & #160;:
alice += a
Sinon:
bob += b

retour (alice > bob) - (alice < bob) # 1 / -1 / 0
«» "

> L'expression `(alice > bob) - (alice < bob)` est un moyen concis de retourner `1`, `-1` ou `0`.

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int stoneGameVI(vecteur<int>& aliceValues, vecteur<int>& bobValues) {
int n = aliceValues.size();
vecteur<tuple<int,int,int>> pierres; // (somme, alice, bob)
réserve(n);
pour (int i = 0; i < n; ++i)
pierre.emplace_back(aliceValues[i] + bobValues[i],
aliceValues[i], bobValues[i];

tri(stones.begin(), stones.end(),
[](const auto& x, const auto& y) {
retour obtenir <0>(x) > obtenir <0>(y); // descendant par somme
});

longue alice longue = 0, bob = 0;
pour (int i = 0; i < n; ++i) {
Si (i % 2 == 0) // Tour d'Alice
alice += obtenir <1>(pierres[i]);
Autre/ Le tour de Bob
bob += obtenir <2>(pierres[i]);
}

si (alice > bob) retourne 1;
si (alition < bob) retour -1;
retour 0;
}
};
«» "

---

- Oui. 5. Article de blog – Le bon, le mauvais, et l'atroce de la pierre jeu VI

> **Mots clés:** Stone Game VI, LeetCode 1686, algorithme gourmand, tri, théorie de jeu, codage d'entrevue, pensée algorithmique, complexité du temps, complexité de l'espace, entretien d'emploi, prép d'entrevue de codage

---

5.1 Introduction

Dans les entrevues de codage, les problèmes qui mêlent la théorie du jeu et les structures de données classiques sont fréquents. **Stone Game VI** est un tel problème. Bien que sa déclaration puisse sembler intimidante, la solution optimale est étonnamment simple : *sortez par la somme des deux joueurs, et jouez avidement*. Cet article passe par cette perspicacité, les pièges que vous pourriez rencontrer, et pourquoi cette approche est une grande vitrine pour votre portfolio d'entrevues.

---

5.2 Le bon – Ce qui fonctionne et pourquoi

Autres Pourquoi ça marche ?
C'est pas vrai.
La valeur combinée d'une pierre est l'avantage exact qu'elle donne au joueur actuel sur l'adversaire. Choisir la somme maximale maximise le différentiel de score à chaque tour. Autres
**Alternation des virages**= Après tri, le jeu se réduit à une séquence déterministe: Alice prend les indices 0, 2, 4...; Bob prend 1, 3, 5.... Aucune autre décision n'est nécessaire. Autres
**O(n log n) Temps**=Le tri domine, mais avec `n ≤ 105` l'algorithme s'inscrit confortablement dans les limites de temps sur n'importe quelle plate-forme. Autres
**O(n) Extra Space**= Nous stockons une gamme légère de tuples (ou de structures). Il n'est pas nécessaire d'avoir un tas lourd ou une récursion. Autres
**Code clair**La solution est quelques lignes longues dans n'importe quelle langue, ce qui facilite l'explication sur place. Autres

> **À emporter :** Lorsque le problème se réduit à un choix *mondial* optimal, une stratégie gourmande bat souvent des formulations de programmation dynamique plus complexes.

---

5.3 Les mauvaises – erreurs courantes et cas de bord

Pourquoi ça se casse
C'est pas vrai.
**Désormais par `alice` ou `bob` seul** Une pierre qui semble bonne pour Alice peut être terrible pour Bob. Autres
**Utiliser un min-heap et toujours sauter le plus petit** Utilisez un max-heap ou triez en descendant. Autres
**En supposant que `int` est sûr pour les scores**. Bien que `int` peut contenir jusqu'à ~2 milliards, il est plus sûr d'utiliser `long`/`long long` pour les sommes à protéger contre les modifications futures. Autres Utilisez des entiers 64 bits pour obtenir des scores cumulatifs. Autres
**Ignorer la manipulation des cravates** Comparaison explicite des scores : `scoreA > scoreB ? 1 : (scoreA < scoreB ? -1 : 0);` Autres
Le mélange d'indices 0 et 1 conduit à des tours échangés. 0' pour Alice's tourne si les indices commencent à 0. Autres

> **Conseil de débogage:** Imprimer l'ordre trié et simuler les premiers tours manuellement pour confirmer la logique d'alternance.

---

#### 5.4 L'horrible – Quand l'avidité pourrait échouer (et comment le repérer)

La solution avide *toujours* fonctionne pour Stone Game VI parce que le jeu est **zero-sum** avec des informations parfaites et aucun état caché. Cependant, il est facile de mal interpréter le problème comme un jeu classique de la valeur la plus élevée (comme Nim). Si les valeurs de pierre étaient dynamiques (p. ex., en changeant après chaque choix) ou si les joueurs avaient des informations cachées, une stratégie gourmande pourrait être suboptimale.

**Quoi regarder:**

- ** Valeurs de la pierre dynamique** – Si le choix d'une pierre modifie l'alice + bob' des autres, vous auriez besoin d'une approche DP ou minimax.
- **Information incomplète** – Si un joueur ne connaît pas les autres valeurs, vous pouvez calculer le différentiel de score exact.
- **Plusieurs mouvements par tour** – Si un joueur peut prendre plus d'une pierre par tour, la logique de l'alternance se brise.

Lorsque vous rencontrez de telles variations, commencez par énumérer quelques états manuellement et vérifier si choisir le meilleur mouvement local peut conduire à un résultat mondial pire. Cela révélera rapidement si une solution plus sophistiquée (DP, minimax ou game‐tree search) est nécessaire.

---

#### 5.5 Pourquoi ce problème est un must-Have sur votre Playbook d'entrevue

1. **Démonstrations Game‐Theoretic Insight** – Vous impressionnerez les intervieweurs avec votre capacité de voir au-delà de l'évidence et de capturer l'avantage de l'adversaire.
2. **Agnostisme linguistique** – Le même algorithme traduit sans effort en Java, Python, C++, Allez, ou même JavaScript. Montrez que vous pouvez coder la même logique dans la langue préférée de l'interview.
3. **Scales to Contraintes** – Les intervieweurs aiment les solutions qui manipulent les contraintes de bord avec élégance; notre algorithme `O(n log n)` ne fait que cela.
4. **Facile à communiquer** – En 3-5 minutes, vous pouvez décrire le problème, l'astuce `a+b` et la simulation de tour, laissant la personne interrogée se concentrer sur votre raisonnement plutôt que le codage de plaque de chaudière.

> **Conseil pro :** Dans une interview en direct, expliquez d'abord l'idée de *score différentiel*. Écrivez la valeur combinée d'une pierre et montrez que le plus grand "somme` maximise l'avantage. Alors laisse tomber le code.

---

5.6 Pensées de clôture

Stone Game VI est une vitrine parfaite de l'élégance algorithmique*. Sa solution est :

1. **Conceptuellement propre** – Une ligne de tri et un seul passage.
2. **Robust** – Gère toutes les contraintes, les liens et les sommes importantes.
3. **Interview-friendly** – Brève, explicable et linguistique-agnostique.

La maîtrise de ce problème vous donne un bon exemple de pensée gourmande, de perspicacité théorique et de pratique de codage efficace.

---

5.7 Appel à l'action

- **Pratique** l'approche gourmande dans un bac à sable (LeetCode, HackerRank, ou votre propre compilateur).
- **Partager** votre solution sur GitHub avec un README concis expliquant le "alice + bob".
- **Discuss** les pièges que nous avons mis en évidence lors de votre prochaine simulation d'entrevue.

> Une solution propre au jeu de pierre VI est un badge de qualité *code* qui dit : « Je peux résoudre des problèmes complexes avec des algorithmes élégants et efficaces. (en milliers de dollars)

---

- Oui. 6. FAQ

Question Réponse
C'est pas vrai.
*Puis-je utiliser un genre stable?* La stabilité n'est pas requise, mais elle ne fait pas de mal si vous voulez une sortie déterministe. Autres
*Et si `aliceValues[i] + bobValues[i]` est le même pour plusieurs pierres?* Leur ordre relatif n'a pas d'importance, car toutes ces pierres produisent le même différentiel de score. Autres
*Y a-t-il une solution linéaire?* Avec des valeurs limites (=100), vous pouvez utiliser le tri en **O(n + M)** où `M = 200`. Toutefois, les frais généraux des tableaux de comptage peuvent l'emporter sur l'avantage pour `n = 105`. Autres

---

- Oui. 6. Pensées finales

Le cadre "bien, mauvais et laid" transforme une question d'entrevue apparemment délicate en un moment d'apprentissage. En comprenant *pourquoi* trier par la somme fonctionne, vous évitez les pièges communs et présentez une solution claire et optimale qui démontre une pensée algorithmique forte.

Bon codage – et que votre prochaine entrevue se déroule aussi bien qu'une valeur combinée de pierre! C'est ce qu'il a dit.

---

*Préparé par : Votre ami Tuteur Algorithme*
*Sentez-vous libre d'adapter les extraits de code ou d'article à votre marque personnelle et à votre portfolio. *