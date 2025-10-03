---
titre: LeetCode 2571. Opérations minimales pour réduire un entier à 0 -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Voici trois implémentations propres, **O(log n)** (Java, Python, C++) qui résolvent le problème LeetCode *2571 – Opérations minimales pour réduire un entier à 0*.
Les trois utilisent la même idée de manipulation cupide:
*Lorsque les deux bits les moins significatifs sont `11` nous ajoutons 1 (faire le bloc `00` et porter 1), sinon nous supprimons simplement un seul `1` ou quart. *
Cela donne la séquence optimale des opérations.

---

- Oui. Java (Java 17)

"Java
***
* 2571. Opérations minimales pour réduire un entier à 0
* Temps O(log n), espace O(1)
*/
solution de classe {
Activités publiques(int n) {
Int ops = 0;
pendant la période (n > 0) {
// si les deux bits les moins significatifs sont 11 (binaire 3)
si ((n & 3)] 3) {
n++; // ajouter 2^0 pour effacer la piste 1s
ops++;
} autre {
ops += n & 1; // ajouter 1 si le bit le plus bas est 1
n >>= 1; // à droite (diviser par 2)
}
}
les opérations de retour;
}
}
«» "

---

### Python (3.10+)

'`python
"""
2571. Opérations minimales pour réduire un entier à 0
Temps O(log n), espace O(1)
"""

Solution de classe:
def minOpérations(self, n: int) -> Int:
ops = 0
alors que n:
Si les deux derniers bits ont 11
si n & 3 == 3:
n += 1 # ajouter 1 à transporter
Opérations += 1
Sinon:
ops += n & 1 # compter un seul 1
n >>= 1 # à droite
retour ops
«» "

---

### C++ (C++17)

'`cpp
***
* 2571. Opérations minimales pour réduire un entier à 0
* Temps O(log n), espace O(1)
*/
solution de classe {
public:
int minOpérations(int n) {
Int ops = 0;
pendant que (n) {
si ((n & 3)] 3) { // deux LSB sont '11'
++n; // ajouter 1
++ops;
} autre {
ops += n & 1; // compter une seule 1
n >>= 1; // diviser par 2
}
}
les opérations de retour;
}
};
«» "

---

- Oui. 2. Article du blog
Le bon, le mauvais et le mauvais de LeetCode 2571 – Comment le faire dans une entrevue*

Introduction
LeetCodes **2571 – Minimum Operations to Reduce an Integer to 0** est un puzzle de manipulation de bits qui apparaît fréquemment dans les interviews techniques pour les rôles d'ingénierie logicielle. Maîtriser ce problème illustre votre compréhension de l'arithmétique binaire, le raisonnement gourmand et la programmation dynamique. Dans cet article, nous disséquerons le problème, marcherons à travers la solution la plus élégante, explorerons les pièges communs (-) et expliquerons comment les éviter (-) À la fin, vous serez prêt à impressionner les gestionnaires d'embauche avec un code propre en Java, Python ou C++.

---

#### Déclaration de problème (mots-clés de référence : *Code de débit 2571*, *opérations minimales*, *entier à 0*, * manipulation de bits*)

> **Avec un entier positif `n`, vous pouvez ajouter ou soustraire n'importe quelle puissance de 2 de lui. **
> **Retourner le nombre minimum d'opérations requis pour ramener `n` à 0.**
> **Constances**: "1 ≤ n ≤ 10^5"

---

#### Intuition – La bonne

1. **Vue binaire**
- L'ajout ou la soustraction de `2^i` retourne le `i`-th bit et peut causer un transport.
- L'objectif est d'effacer tous les bits avec le moins de flips possible.

2. **Observation générale**
- Lorsque les deux bits les moins significatifs sont `01` (simple `1`), nous pouvons les effacer en une seule opération en soustrayant `1`.
- Quand ils sont `11`, nous ne pouvons pas effacer à la fois avec une seule soustraction; le déplacement optimal est de *ajouter* `1` (porter) puis de dégager les deux zéros de la prochaine itération.
- Oui. Cette décision locale conduit à un résultat global optimal.

3. **Complexité temporelle**
- Chaque itération supprime au moins un bit, de sorte que la boucle exécute `O(log n)` fois.

---

#### La solution classique d'une seule ligne – La mauvaise

Un liner populaire, quoique moins lisible, existe :

"Java
int minOpérations(int n) {
retour Integer.bitCount(n ^ (n * 3));
}
«» "

**Pourquoi ça marche* *
- L'expression `n ^ (n * 3)` transforme chaque bloc contigu de `1`s en deux `1`s, de sorte que le pop-count du résultat égale le nombre minimal d'opérations.

**Pourquoi c'est mauvais pour les interviews* *
- **Readability**: Il cache le raisonnement derrière une identité mathématique.
- **Débogage**: Si les intervieweurs vous demandent d'expliquer chaque étape, vous devrez décomposer l'algèbre.
- ** Dépendance linguistique** : Il s'appuie sur des fonctions bit-count spécifiques à la langue.

---

C'est vrai. L'horrible – Quoi éviter

1. **Récursion de la force brute**
- Le dénombrement de toutes les combinaisons de puissances de 2 est exponentiel et sera time-out sur `n = 10^5`.
- La mémorisation aide, mais le facteur constant est encore élevé.

2. **Cas de bord de graisse incorrecte* *
- Le fait d'oublier le cas `11` (par exemple, toujours soustraire `1`) conduit à des comptes sous-optimaux.
Exemple: `n = 3 (112)` → soustraire `1` deux fois donne 2 ops, mais l'optimal est d'ajouter `1` première (1 op) → `4 (1002)` → soustraire `4` (1 op) → total 2 ops.
- L'étape de transport va gonfler la réponse.

3. **L'utilisation de la division au lieu des quarts de travail
- `n / 2` est plus lent et moins idiomatique en C++/Java.
- Préférez `n >>= 1» pour la clarté et la performance.

---

#### Step‐by‐Step Walkthrough – Le Bon (Java)

"Java
pendant la période (n > 0) {
si ((n & 3)] 3) { // bits: ...??? 11
n++; // ajouter 1 → ...??? 00 avec transport
ops++;
} autre {
ops += n & 1; // effacer une seule 1
n >>= 1; //
}
}
«» "

**Ce que signifie chaque branche* *
- **"(n & 3) == 3'**: Les deux LSB sont `11'.
- Ajout des tours `1` `11` → `00` (après le transfert) et la boucle supprimera deux bits dans le changement suivant.
- **Autres**: Soit nous avons `01` ou `00`.
- Si `01`, `ops += 1' c'est ça.
- Si 00, on se déplace et on ne fait rien.

---

#### Analyse de la complexité – Le bon

Langue Heure Espace Commentaire
C'est pas vrai.
"O(log n)" "O(1)" Utilise bitwise ops et une boucle de temps
Python "O(log n)" "O(1)" Même logique gourmande, entier arithmétique
* C++ * O(log n) * O(1) * La manipulation directe du bit, pas de frais généraux de bibliothèque.

* L'empreinte mémoire est constante car nous ne conservons que le nombre actuel et un compteur d'opération. *

---

#### Conseils de préparation à l'entrevue

1. **Expliquer la vue binaire d'abord** – Commencez par dessiner la représentation binaire de `n`.
2. **Énoncer la règle de l'avidité** – Montrez que vous allez regarder les deux LSB; clarifier les deux cas ( '01` vs `11`).
3. **Écrire des boucles propres** – Éviter les liners obscurs sauf si vous êtes certain que l'intervieweur est à l'aise avec eux.
4. **Montrer la manipulation des caisses de bord** – Et si `n` était déjà une puissance de 2? Votre algorithme le gère naturellement.
5. **Discuss alternatives** – Mentionnez l'approche PDD et pourquoi l'avidité est préférable pour `n <= 10^5`.

---

#### Code Showcase – Le Bon

*(Insérer les trois extraits de code de la section 1 ci-dessus, chacun avec des commentaires en ligne.) *

---

C'est vrai. Comment utiliser cette connaissance dans une recherche d'emploi

1. **Ajouter la solution à votre logiciel GitHub README* *
- Créer un dépôt *`leetcode-2571`* et documenter le problème, la solution et la complexité.
- Inclure les trois implémentations linguistiques.

2. **Écrire un billet de blog technique**
- Publier sur Medium, Dev.to, ou votre propre site.
- Utilisez les titres SEO (=LeetCode 2571 Solution en Java, Python, C++) et les balises.
- Partagez le message sur LinkedIn et Twitter avec un bref crochet: Vous voulez avoir votre prochain entretien de codage ? Voici une solution de 4 minutes pour LeetCode 2571.

3. **Showcase pendant les entrevues**
- Apportez une copie de votre README ou un lien vers votre repo GitHub.
- Mettez en évidence que vous comprenez le raisonnement algorithmique, pas seulement le code.

---

Appel à l'action

- **Clouer le repo**: `git clone https://github.com/votre nom d'utilisateur/leetcode-2571.git`
** Effectuer les essais**: Chaque fichier contient un `main` pour les tests manuels rapides.
- **Partager**: postez votre solution sur les réseaux sociaux avec les hashtags #LeetCode #CodingInterview #Java #Python #C++.

**Prenez la prochaine étape**: Maître *LeetCode 2571*, écrivez un code propre, et laissez votre billet de blog servir de preuve de vos prouesses de résolution de problèmes. Bonne chance – votre prochaine interview ne saura pas ce qui l'a frappé!

---

#### Méta‐ Données pour le référencement

- **Titre**: Code Leet 2571 – Opérations minimales pour réduire un entier à 0, Java, Python, C++
- **Mots-clés**: LeetCode 2571, opérations minimales, entier à 0, manipulation de bits, algorithme avide, question d'entretien, entretien de codage, solution Java, solution Python, solution C++, entretien d'ingénierie logicielle, conseils d'entretien d'emploi
- **Description**: - Apprenez à résoudre le LeetCode 2571 avec un algorithme de manipulation de bits O(log n). Obtenez le code Java, Python et C++, comprenez la logique gourmande, évitez les pièges communs et stimulez vos performances d'entrevue. (en milliers de dollars)

---