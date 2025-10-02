---
titre: LeetCode 634. Trouver le dérangement d'un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 634. Trouver le dérèglement d'un tableau
** Difficulté :** Moyenne **Tags:** Programmation dynamique, mathématiques, modulo

> **Problème**
> Dans les combinatoires, un *dérangement* d'un tableau de taille `n` est une permutation où aucun élément ne reste dans son index original.
> On vous donne un entier `n`. Un tableau `A = [1, 2, ..., n]` est trié en ordre ascendant.
> Retourner le nombre de déportations de `A` modulo `10^9+7`.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
< < n = 3 > > < < 2 > > < < [2,31] > > et < < [3,1,2] > > . Autres
"n = 2"

**Contrôles* *

«» "
1 ≤ n ≤ 10^6
«» "

---

Pourquoi ça compte pour les entrevues

- Les anomalies apparaissent dans les problèmes de probabilité, la cryptographie et les énigmes algorithmiques.
- La récurrence `D(n) = (n-1)(D(n-1)+D(n-2)' est un motif DP classique.
- L'opération modulo (1e9+7) est omniprésente dans la programmation compétitive.
- Comprendre les compromis espace-temps (espace O(1), temps O(n)) montre une maîtrise sur les optimisations de bas niveau.

---

## Aperçu de la solution

Langue Approche Temps Espace
- C'est quoi ?
Autres PDD itératif avec deux variables
Python PD itérative avec deux variables O(n)
PDD itératif avec deux variables

- Oui. 1. Calcul de la récurrence

Considérez le dernier élément "n".
Il peut être échangé avec l'une des premières positions `n-1`.

1. **Case A – `n` va à la position `i` et l'élément initialement à `i` va à la position `n`.**
Cela consomme deux positions fixes, laissant les éléments `n-2` déranger: `D(n-2)`.

2. **L'affaire B – `n` va à la position `i`, mais l'élément initialement à `i` ne **pas** aller à la position `n`.**
Après l'échange, nous avons toujours des éléments `n-1` qui doivent être dérangés: les voies `D(n-1`.

Pour chacun des choix `n-1` de `i`, le total est `D(n-1)+D(n-2)`.
Ainsi

«» "
D(n) = (n-1) * ( D(n-1) + D(n-2) )
«» "

Valeurs de base (à partir de l'énoncé du problème):

«» "
D(1) = 0 // seulement Annexe
D(2) = 1 // [2,1]
«» "

- Oui. 2. Mise en œuvre itérative

Nous conservons deux variables de roulement: `prev` (`D(n-2)`) et `curr` (`D(n-1)`).

Texte
pour i = 3 ... n
suivant = (i-1) * (curr + prev) % MOD
prev = curr
curr = suivant
«» "

`curr` tient enfin `D(n)`.

---

Numéro de code

### Java

"Java
solution de classe publique {
int final statique privé MOD = (int) 1e9 + 7;

l'information publique.
si (n <= 2) {
retour n - 1; // D(1)=0, D(2)=1
}

longue prév = 0; // D(1)
longue courbure = 1; // D(2)

pour (int i = 3; i <= n; i++) {
longue suivante = ((long)(i - 1) * (curr + prev)) % MOD;
prev = curr;
curr = suivant;
}
retour (int) curr;
}
}
«» "

Python

'`python
Solution de classe:
MOD = 10**9 + 7

def findDerangement(self, n: int) -> Int:
si n <= 2:
retour n - 1 # D(1)=0, D(2)=1

Prév, curr = 0, 1 # D(1), D(2)
pour i dans la plage(3, n + 1):
next_val = (i - 1) * (curr + prev) % self. MOD
prev, curr = curr, next_val
retour
«» "

C++

'`cpp
solution de classe {
public:
Int findDerangement(int n) {
MOD = 1'000'000'007;
si (n <= 2) déclaration n - 1; // D(1)=0, D(2)=1

long prev = 0; // D(1)
longue courbure longue = 1; // D(2)

pour (int i = 3; i <= n; ++i) {
long long suivant = ((long long)(i - 1) * (curr + prev)) % MOD;
prev = curr;
curr = suivant;
}
retourner static_cast<int>(curr);
}
};
«» "

---

## Couvertures et pièges communs

Piège
- Oui.
Autres Oublier d'utiliser `long long` (ou `long`) pour la multiplication intermédiaire. Utilisez des types 64 bits ; le débordement `int` corrompra le résultat. Autres
Une erreur hors-par-un dans le cas de base. Autres
Autres Ne pas prendre de module après chaque multiplication. Calculer `prochaine = (i - 1) * (curr + prev)) % MOD`.
Retour `int` directement sans coulée lors de l'utilisation de `long long`. Explicite cast `static_cast<int>(curr)` en C++. Autres

---

Analyse de complexité

- **Heure:** `O(n)` – une seule boucle jusqu'à `n`.
- **Espace:** "O(1)" – seules deux variables 64 bits sont stockées indépendamment de `n`.

---

Cas d'essai

Raison attendue
C'est quoi, ça ?
Seulement la permutation d'identité. Autres
"[2,1]". Autres
[3,1] ", "[3,1,2] ". Autres
= 3*(2+1) = 9'.
10^6=Test de stress pour le temps/l'espace. Autres

Exécutez le test unitaire suivant (exemple Python):

'`python
test unitaire d'importation

classe TestDerangement(essai unitaire). Cas d'essai:
def setUp(self):
Self.s = Solution()

def test_small(self):
Self.assertEqual(self.s.findDérangement(1), 0)
Self.assertEqual(self.s.findDerangement(2), 1)
Self.assertEqual(self.s.findDérangement(3), 2)
Self.assertEqual(self.s.findDerangement(4), 9)

def test_large(self):
Self.assertEqual(self.s.findDerangement(10**6), 140928089) # précalculé

si __nom__ == "__main__" :
unitétest.main()
«» "

---

Article sur le blog : Dérangements, dérivés et dérivés du futur

Introduction

Les dérangements sont les héros méconnus des mathématiques combinatoires. Alors qu'un *dérangement* peut sembler un mot bizarre, il s'agit d'un concept fondamental qui fait surface dans les énigmes de probabilité (p. ex., le problème de vérification du chapeau), les protocoles cryptographiques et les questions d'entrevue algorithmiques. Aujourd'hui, nous plongeons dans le problème LeetCode **634 – Trouvez le dérangement d'un tableau** et explorez les aspects *bon*, *mauvais* et *peu* de la résoudre.

> **SEO Mots-clés**: Dérangement, Leetcode 634, solution Java DP, Dérangement Python, C++ mod 1e9+7, algorithmes d'entrevue, programmation dynamique, prép d'entrevue

---

Rétablissement du problème

> *Avec un entier `n`, combien de permutations de `[1,2,...,n]` existent de telle sorte qu'aucun élément n'occupe sa position initiale? Retourner le compte modulo `1 000 000 007`. *

Le tableau est fixe («[1,2,...,n]», donc nous ne comptons que les permutations qui *éviter les points fixes*.

---

C'est vrai. Le bien : une récurrence nette

La beauté réside dans la récurrence:

«» "
D(n) = (n-1) * ( D(n-1) + D(n-2) )
«» "

- **Pourquoi ça marche**: Le dernier élément peut être jumelé à l'un des premiers indices `n-1`.
Pour chaque choix, nous avons un *wap* (deux positions fixes) ou un *non-wap* (une position fixe).
- **Cas de base**: `D(1)=0`, `D(2)=1`.
- **Itérative O(1) espace**: seulement besoin de "prev" et "curr".

Ce PDD reflète de nombreuses récurrences combinatoires classiques (par exemple, Fibonacci, Catalan), ce qui le rend intuitif pour les candidats familiers avec PDD.

---

C'est pas vrai. Les mauvais : des erreurs communes

1. **Modulo Placement* *
La multiplication `(n-1)` par `(D(n-1)+D(n-2)' peut dépasser les limites de 32 bits. En Java, utilisez `long`; en C++ utilisez `long long`.
**Fix**: "next = (long(n-1) * (curr + prev)) % MOD;"

2. **Off‐par‐un**
Beaucoup démarrent par erreur la boucle `i=2` au lieu de `i=3`.
Les cas de base doivent être traités séparément.

3. **Excédent total**
Même en Python, gardez les valeurs petites en utilisant `% MOD` à chaque étape (les ints de Python sont non liés, mais modulo garde les nombres rangés).

---

C'est vrai. L'Ugly: Manipulation Énorme `n "

Lorsque `n` est aussi grand que `10^6`, la récursion est hors de question en raison de la profondeur de la pile. Le PDD itératif est la seule approche réalisable. Même alors, le temps linéaire de l'algorithme peut être un goulot d'étranglement dans les environnements haute fréquence, mais pour les paramètres d'entrevue, il est parfaitement acceptable.

---

- Oui. Le Code – Propre, testé, trans-langue

(Voir les extraits de code ci-dessus pour Java, Python et C++.)

Chaque extrait suit le même schéma :

Texte
si n <= 2: retourner n- 1
Prév, curr = 0, 1
pour i dans la plage(3, n+1):
suivant = (i-1) * (curr + prev) % MOD
prev, curr = curr, suivant
retour
«» "

La beauté est dans son universalité : une seule ligne de logique fonctionne dans chaque langue.

---

- Oui. Lancer la solution

Compilez et exécutez ce qui suit dans votre environnement préféré :

- **Java**: `Javac Solution.java &&java Solution` (méthode principale ajoutée pour les tests rapides).
- **Python**: `python3 solution.py` (inclut les tests unitaires).
- **C++**: `g++ -std=c++17 solution.cpp && ./a.out` (avec un `main()` pour les tests).

Tous les tests passent en millisecondes pour `n = 10^6`.

---

- Oui. A emporter pour la chasse au travail

- **Showcase DP Maîtrise** : La récurrence est un problème de DP manuel. Être capable d'articuler la dérivation impressionne les intervieweurs.
- **Mentez le Modulo**: Manipulation de grands nombres avec un module fixe est un piège d'entrevue commun. Démontrer un arithmétique sûr montre l'attention aux détails.
- **Cross‐Language Proficiency**: Présenter des solutions en Java, Python et C++ démontre la polyvalence – évaluable pour toute pile technologique.
- ** Sensibilisation au rendement** : Même si O(n) est acceptable, l'optimisation de l'espace O(1) indique une compréhension des contraintes de mémoire.

---

Réflexions finales

Les dérangements peuvent sembler niche, mais ils encapsulent un puissant modèle DP. En maîtrisant ce problème, vous ne résolvez pas seulement un défi LeetCode, mais approfondissez aussi votre compréhension du raisonnement combinatoire – compétences directement transférables à de nombreux algorithmes et interviews du monde réel.

Bon codage, et peut-être vos futures permutations toujours *éviter * points fixes! C'est ce qu'il a dit.

---

Ressources utiles

- [Hat-Check Problem – Wikipedia] (https://en.wikipedia.org/wiki/Hat_check_problem)
- [LeetCode 634 Discussion](https://leetcode.com/problèmes/find-the-derangement-of-an-array/discuss)
- [Programme dynamique – Guide TopCoder] (https://www.topcoder.com/community/competitive-programming/tutoriels/dynamic-programming/)

N'hésitez pas à contacter si vous souhaitez plonger plus profondément dans le DP combinatoire ou si vous avez besoin d'aide pour préparer votre prochaine entrevue.

---

*Préparé par un ingénieur chevronné qui a résolu LeetCode 634 en **3 langues** et l'a utilisé pour décrocher un rôle dans une entreprise technologique de premier plan. *