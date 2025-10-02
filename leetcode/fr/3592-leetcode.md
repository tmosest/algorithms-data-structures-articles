---
titre: LeetCode 3592. Changement de pièce inverse -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes – LeetCode 3592 Changement de pièce inverse

> **Objectif** – Avec un tableau 1-indexé `numWays` (longueur *N*), où `numWays[i]` est le nombre de façons d'atteindre la quantité `i+1` en utilisant ** dénominations de pièces inconnues**, récupérer *un* ensemble de dénominations qui pourraient produire exactement ce tableau.
> Si un tel jeu n'existe pas, retournez un tableau vide.

Terme
C'est quoi ?
"numWays[i]" Comment faire le montant `i+1` (le tableau est 0-indexé en code)
Dénomination Nombre entier positif ≤
Autres Fourniture de pièces pour chaque dénomination

Le modèle classique **forward** DP pour le changement de pièce II (LeetCode 518) est :

Texte
dp[0] = 1
pour pièces de monnaie:
pour j = pièce ... N:
dp[j] += dp[j-coin]
«» "

Notre travail est de *inverser* ce processus.

---

Intuition – Pourquoi le DP inverse fonctionne

1. ** Ajouter une nouvelle pièce 'i`**
La première fois que nous introduisons une pièce avec la valeur `i`, il contribue exactement **une** nouvelle façon de faire la quantité `i` (en utilisant une seule pièce).
Mathématiquement: `dp[i]` augmente de `dp[0] = 1`.

2. **Effet sur les autres montants**
Après l'ajout de la pièce, chaque montant `j ≥ i` est mis à jour:
«dp[j] += dp[j-i]».
Il s'agit de la même mise à jour que le PDD avancé.

3. **Observation principale**
Alors que des montants itératifs de 1 à *N*, si nous **avons ajouté la pièce `i` encore, le `dp[i]` actuel sera **exactement** un de moins que le "numWays[i-1]" requis *iff* une pièce "i" doit exister.
Dans ce cas, nous ajoutons la pièce `i`, effectuons la mise à jour DP, puis vérifions que `dp[i]` correspond maintenant `numWays[i-1]`.

4. ** Scénarios impossibles**
Si à un moment quelconque `dp[i]` est *not* `numWays[i-1]` après un ajout de pièce possible, le tableau est incohérent → retourner `[]`.

Parce que nous examinons toujours les montants par ordre croissant, la liste que nous construisons est déjà triée.

---

La solution O(*N*2) inverse

L'algorithme fonctionne dans **O(N2)** temps (chaque insertion de pièce déclenche une mise à jour sur les quantités restantes) et **O(N)** espace.

> **Pourquoi c'est bien* *
> * Logique claire* – un passage sur les montants, un seul tableau DP, facile à raisonner.
> * Sortie déterministe* – retourne toujours le plus petit ensemble de valeurs qui satisfait les données.
> *Safe for LeetCode* – satisfait aux contraintes ('N ≤ 100').

### Java

"Java
Importation de java.util.*;

solution de classe publique {
liste statique publique<entier> findCoins(int[] numWays) {
n = longueur numWays; // quantités 1 ... n
int[] dp = nouvelle int[n + 1]; // dp[0] ... dp[n]
Liste <entier> pièces = nouvelle liste d'array<>();

dp[0] = 1; // scénario de base

pour (int amt = 1; amt <= n; amt++) {
int ways = numWays[amt - 1]; // ways requis pour la quantité = amt

// Si une pièce de valeur 'amt' doit exister
Si (toujours > 0 && dp[amt]) Voies - 1) {
pièces.add(amt);
pour (int j = amt; j <= n; j++) {
dp[j] += dp[j - amt];
}
}

// Après (peut-être) l'ajout de la pièce, le nombre doit correspondre
Si (dp[amt] != ways) {
retourner la nouvelle liste de distribution<>(); // impossible
}
}
les pièces retournées;
}
}
«» "

Python

'`python
def findCoins(numWays):
"""
:param numWays: List[int] – tableau indexé 0, la quantité i+1 correspond à numWays[i]
:retour: Liste[int] – liste des dénominations (ordre croissant) ou liste vide
"""
n = len(numWays)
dp = [0] * (n + 1) # dp[0] ... dp[n]
dp[0] = 1
pièces = []

pour amt de portée(1, n + 1): # amt == 1 ... n
Voies = numWays[amt - 1]

si des voies > 0 et dp[amt] == Voies - 1:
pièces jointes(amt)
pour j dans la plage (amt, n + 1):
dp[j] += Dp[j - amt]

si dp[amt] != Voies : # contrôle de cohérence
retour []

pièces retournées
«» "

C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findCoins(vecteur<int>& numWays) {
int n = numWays.size(); // quantités 1 ... n
vecteur<int> dp(n + 1, 0);
vecteur<int> pièces de monnaie;
dp[0] = 1;

pour (int amt = 1; amt <= n; ++amt) {
= numWays[amt - 1];

Si (toujours > 0 && dp[amt]) Voies - 1) {
coins.push_back(amt);
pour (int j = amt; j <= n; ++j)
dp[j] += dp[j - amt];
}

si (dp[amt] != façons)
retour {}; // impossible
}
les pièces retournées;
}
};
«» "

> **Astuce** – Les trois implémentations partagent la logique *exacte même*, seule la syntaxe linguistique diffère.

---

## --Qu'est-ce que *pas* à faire

L'approche de la complexité Pourquoi c'est mauvais / mauvais
-- -- -- -- -- -- -- -- -- -- -- -- --
**Énumération de la force brute** – Essayez chaque sous-ensemble de `{1,...,N}` et lancez le DP avant pour chaque ensemble de candidats. Autres
**Recursive Backtracking with Memousing** – DFS sur les montants, choisissez les décisions de la pièce de monnaie ou de la pièce de monnaie, états de cache. Environ "O(2^N)" (explosion de l'état) Autres
"O(N2)" mais peut produire de mauvais résultats. Autres

** Leçon clé** – Les intervieweurs * apprécieront* une idée algorithmique concise sur les hacks de force brute. L'inverse DP est la solution de "good" qui est à la fois *fast* et *intuitive*.

---

Liste de vérification de la mise en oeuvre

Détails
C'est quoi ?
**Manipulation d'entrées**Le tableau `numWays` est indexé à 0; la quantité `i+1` des cartes à `numWays[i]`. Autres
**Cas de base**
**Ajouter une pièce de monnaie** ways-1` *and* `ways > 0'. Autres
**Vérification de la conformité**** Après insertion éventuelle de la pièce, le terme «dp[amt]» doit être égal à «ways». Autres
**Valeur de retour**= Liste/vecteur des dénominations par ordre croissant (automatique par construction). Autres
* Tous les zéros*, *l'augmentation*, *la diminution*, *la duplication des voies*, *les tableaux impossibles* – tous traités par la vérification de cohérence. Autres

---

Complexité

- **Time** – `O(N2)` (le pire cas : chaque pièce déclenche une mise à jour DP complète des montants restants).
Avec *N* ≤ 100 c'est trivial pour tout juge.
- **Espace** – `O(N)` pour le tableau `dp` plus `O(N)` pour la liste de sortie.

---

Essais d'échantillons

Résultats escomptés
- C'est quoi ?
Il suffit de la pièce 2. Autres
Un exemple classique de l'énoncé du problème. Autres
"[0, 0, 0]" "[]" Aucune pièce ne peut produire d'aucune façon – un tableau cohérent. Autres
Impossible : si la pièce 1 existait, le montant 1 aurait un moyen, mais l'ajouter créerait aussi des moyens pour 2,3,4. Autres

Exécutez les extraits de code fournis dans votre IDE préféré ou compilateur en ligne pour vérifier.

---

Pourquoi ça compte pour un entretien d'embauche ? *

1. **Afficher la maîtrise du DP** – Vous démontrez comment les algorithmes classiques peuvent être * inversés* ou * adaptés*.
2. **L'état d'esprit de résolution des problèmes** – Vous n'êtes pas seulement codant ; vous êtes en train de formuler une logique propre qui gère les cas d'angle.
3. **Efficacité** – Une solution O(*N*2) avec *N* = 100 est facilement dans les limites – les intervieweurs aiment les solutions à l'échelle, même pour de petites contraintes.
4. **Communication** – Expliquer l'intuition étape par étape (comme nous l'avons fait ci-dessus) est une compétence clé en entrevue.
*Pratique* : Commencez par décrire le DP avancé, puis montrez comment ajouter une pièce ne change qu'une valeur par +1, etc. (en milliers de dollars)
5. **Manipulation des caisses** – Mettre en évidence que la cohérence vérifie les captures de tableaux impossibles, ce qui montre un codage défensif.

> ** Conseil professionnel :** Lorsqu'on leur demande de résoudre un nouveau problème de PDD, pensez toujours :
> *Qu'est-ce que l'invariant qui change lorsque vous ajoutez un nouvel élément? *
> Pouvez-vous détecter ce changement en regardant le prochain état ? *
> Ce modèle fonctionne dans de nombreux problèmes d'entretien inverse-DP (p. ex., Ajouter minimal pour rendre les parenthèses valides dans une forme retournée).

---

Aperçu du blog optimisé du SEO

> **Titre**: *Ingénierie inverse Changement de pièce – LeetCode 3592 – Un guide complet pour les entrevues de codage*
> **Méta-description**: Apprenez l'astuce inverse-DP pour résoudre le LeetCode 3592, comprendre la théorie sous-jacente, et voir prêt à copier les implémentations Java, Python et C++. Parfait pour la préparation de l'entrevue d'ingénierie logicielle.

- Oui. 1. Introduction (300 mots)

- Hook: Vous avez vu un puzzle où vous êtes donné le résultat, mais doit trouver le processus caché? (en milliers de dollars)
- Mentionnez LeetCode 3592 et sa popularité dans le codage des entrevues.
- Indiquez le problème en anglais.

- Oui. 2. Pourquoi le changement de pièce inverse est une grande question d'entrevue

- En relation avec la programmation dynamique classique (Coin Change II).
- Teste la capacité de *penser à l'envers*, une compétence rare.
- Vous donne l'occasion de parler de l'offre infinie, des contraintes entières et de l'indexation des tableaux.

- Oui. 3. Bien – La solution PDD inversée (de 400 mots)

- Présentez l'intuition (voir ci-dessus).
- Parcourez l'algorithme étape par étape sur un exemple concret.
- Soulignez que la liste est construite en ordre ascendant et que le tableau DP n'a jamais besoin d'être réinitialisé.

- Oui. 4. Extraits de code (de 200 mots par langue)

- Afficher Java, Python, C++ côte à côte.
- Ajouter des lignes de commentaires `#` expliquant chaque bloc.
- Encourager le lecteur à copier-coller et à tester.

- Oui. 5. "Bad" & "Ugly" – Qu'est-ce que *pas* à faire (250 mots)

- Décrivez brièvement la force brute et le recul.
- Expliquez pourquoi ils sont inefficaces.
- Encourager plutôt la concentration sur le PD inverse O(N2).

- Oui. 6. Complexité du temps et de l'espace (de 200 mots)

- Donnez les maths.
- Discutez pourquoi il est acceptable pour *N* ≤ 100.

- Oui. 7. Cas de bord et codage défensif (=200 mots)

- Énumérez tous les scénarios de la vérification de cohérence.
- Mentionnez comment éviter les bogues off-by-one avec l'indexation des tableaux.

- Oui. 8. Préparation de l'entrevue

- Pratique expliquant la logique à haute voix.
- Écrire un petit harnais d'essai pour vérifier la cohérence.
- Mettre en évidence comment adapter la solution à d'autres problèmes de PD inversé.

- Oui. 9. Conclusion (de 200 mots)

- Résumez l'astuce, mettez en valeur les principaux à emporter.
- Invitez les lecteurs à essayer le problème sur LeetCode.
- Offrez un dernier appel à l'action : Partager votre solution dans les commentaires ou sur Twitter avec #LeetCode3592. (en milliers de dollars)

10 ans. Références et lectures complémentaires

- Lien vers le fil de discussion LeetCode.
- Proposer des problèmes similaires (p. ex., Minimum Add to Make Parentheses Valide, -Make Palindrome).
- Recommendation de Cracking the Coding Interview pour des concepts DP plus profonds.

---

> ** Pensée perdue* *
> Maîtriser l'astuce inverse-DP non seulement résout LeetCode 3592 mais vous équipe également pour résoudre tout problème d'entrevue qui vous demande de déduire des structures cachées des sorties. Gardez l'intuition vivante, pratiquez l'explication, et vous transformerez un puzzle délicat en une vitrine de vos prouesses de codage. Joyeux hacking !

---

Mot final

Vous avez maintenant :

- Un algorithme propre et éprouvé pour résoudre LeetCode 3592.
- Trois implémentations linguistiques.
- Une esquisse de blog prête à poster SEO optimisée pour impressionner les recruteurs sur LinkedIn ou un portefeuille personnel.

Bon codage et bonne chance pour votre prochaine interview!