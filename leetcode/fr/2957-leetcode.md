---
titre: LeetCode 2957. Supprimer les caractères presque égaux adjacents - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

**LeetCode 2957 – Supprimer les caractères presque égaux adjacents* *
*Difficulté: moyenne*

Étant donné une chaîne de caractères «word» indexée à 0 (longueur ≤ 100, toutes les lettres anglaises minuscules), vous pouvez **changer** tout caractère à toute autre lettre minuscule en une seule opération.
Deux caractères sont *presque égaux* s'ils sont égaux ** ou** adjacents à l'alphabet (''a – b' ≤ 1').

**Objectif** – trouver le nombre minimum d'opérations nécessaires pour que la paire adjacente de caractères dans la chaîne finale soit presque égale.

---

- Oui. 2. Solution d'intuition et d'avidité

Lorsque nous balayons la chaîne de gauche à droite, la seule situation problématique est lorsque le caractère actuel `word[i]` est presque égal à la précédente `word[i‐1]`.

Si cela se produit, nous ** devons** changer `mot[i]`.
Pourquoi peut-on le changer sans se soucier du reste de la corde ?
Parce qu'il y a 26 lettres – nous pouvons toujours choisir une lettre qui est **pas** presque égale à *deux* ses voisins (avant et après).
Donc nous changeons `word[i]` à une telle lettre et puis **skip** en vérifiant le caractère suivant (`i+1`).
Pourquoi ? Parce que "mot [i]" a été changé en quelque chose qui est garanti pour être sûr en ce qui concerne le «mot[i+1]».
D'où le prochain conflit potentiel commence à "i+2".

Ceci donne un algorithme simple **simple**:

«» "
nombre = 0
i = 1
alors que i < n:
i) Mot [i] - mot [i-1] ≤ 1:
nombre += 1 # une opération
i += 2 # skip prochain char
Sinon:
i += 1
Nombre de retours
«» "

complexité du temps : **O(n)* *
complexité spatiale: **O(1)**

---

- Oui. 3. Mise en œuvre des références

#### 3.1 Java

"Java
solution de classe publique {
Entrée publique PresqueEqualCharacters(Mot en boucle) {
nombre int = 0;
pour (int i = 1; i < word.longueur(); ) {
i (Math.abs(word.charAt(i) - word.charAt(i - 1)) <= 1) {
count++; // nous allons changer de mot[i]
i += 2; // sauter le caractère suivant
} autre {
i++;
}
}
le nombre de retours;
}
}
«» "

3.2 Python

'`python
Solution de classe:
def removeAlmostEqualCaracters(self, mot: str) -> Int:
nombre = 0
i = 1
n = len(mot)
alors que i < n:
si abs(ord(word[i]) - ord(mot[i) 1)) <= 1:
nombre += 1
i += 2 # sauter le personnage suivant
Sinon:
i += 1
Nombre de retours
«» "

### 3.3 C++

'`cpp
solution de classe {
public:
int removeAlmostEqualCaracters(string word) {
nombre int = 0;
pour (int i = 1; i < (int)word.size(); ) {
si (abs[i] - mot[i - 1]) <= 1) {
++compte; // changement de mot[i]
i += 2; // sauter l'omble suivant
} autre {
++i;
}
}
le nombre de retours;
}
};
«» "

Les trois codes fonctionnent dans **O(n)** temps, utilisez **O(1)** espace supplémentaire, et correspondent à la réponse attendue sur LeetCode.

---

- Oui. 4. Article du blog – Le bon, le mauvais, et l'indulgence de supprimer les personnages presque égaux

> **Titre**: *Maîtrise du LeetCode 2957 – Le Bon, le Mauvais, et l'Ugly de l'élimination des caractères presque égaux adjacents*
> **Description détaillée**: Apprenez comment résoudre le LeetCode 2957 en temps O(n) avec un algorithme gourmand, comprendre les pièges, et obtenir l'entrevue-prêt pour les rôles FAANG.

---

### 4.1 Le problème en coque

Vous avez une chaîne de lettres minuscules.
Vous pouvez changer n'importe quelle lettre à n'importe quelle autre lettre, une opération à la fois.
Après toutes les modifications, aucune lettre consécutive ne devrait être la même ou l'une des lettres suivantes.
Retourner le nombre minimal de changements.

---

4.2 Pourquoi ce problème se sent difficile

- Oui. La taille de l'entrée est minuscule (= 100), mais la force brute moyenne est la voie à suivre; les intervieweurs s'attendent à une solution claire et optimale.
- Oui. À première vue, il ressemble à un problème de programmation **dynamique** ou **graph**.
- Vous pourriez essayer de penser à chaque remplacement possible pour chaque personnage, conduisant à un éclatement exponentiel.

---

### 4.3 Le bon – Un simple Regard sur l'avidité

La principale observation est la suivante :

> **Si deux caractères adjacents sont presque égaux, nous *devrons* changer le bon. **

Pourquoi ?
Parce que nous ne pouvons pas garder les deux car ils violent la règle.
Et comme nous pouvons choisir n'importe quelle lettre pour le bon caractère, nous pouvons choisir celle qui ne va pas entrer en conflit avec *son bon voisin.

**Ainsi la règle avide est:**
- Scanner de gauche à droite.
- Chaque fois que vous touchez un conflit, incrémentez le compteur, changez le caractère actuel (conceptuel), et sautez l'index suivant.

Cela garantit que chaque changement résout un conflit et n'en introduit jamais un nouveau que nous aurions manqué.
L'algorithme est **O(n)** et **O(1)**, parfait pour l'entrevue.

---

4.4 Les mauvaises – Pièges communs

Pourquoi il échoue
- C'est quoi ?
**Skipping trop loin** Passer deux indices (`i += 2) parce que nous venons de changer de mot. Autres
**Changement excessif**Changement d'un personnage lorsque son voisin gauche est *pas* opérations de déchets presque égales. Ne changez que lorsque ''cur - prev' ≤ 1'. Autres
**Les bogues d'Edge-case** Utiliser une boucle `while` avec un lien sûr (`i < n`). Autres
**Confuser "presque-égale"**" Erreur "adjacent" en alphabet pour "same" seulement. Utiliser `abs(a - b) ≤ 1` (ou `a ==b="a+1==b="a-1==b=". Autres

---

4.5 L'horrible – Essayer la mauvaise structure de données

- **Liste de liens/Quue**: Surkill, ajoute de la complexité et vous ralentit.
- **Tableau PD**: `dp[i][state]` pour chaque caractère possible à la position `i` est inutile parce que nous n'avons jamais besoin de nous souvenir du caractère réel modifié — seulement que nous l'avons changé.
- **DFS récursif**: risque de débordement de la pile et du temps exponentiel pour la longueur 100.

S'en tenir au passage avide; c'est la solution la plus *propre.

---

### 4.6 Passage en code (Java)

"Java
solution de classe publique {
Entrée publique PresqueEqualCharacters(Mot en boucle) {
nombre int = 0;
pour (int i = 1; i < word.longueur(); ) {
// conflit? (presque égal)
i (Math.abs(word.charAt(i) - word.charAt(i - 1)) <= 1) {
++compte; // nous allons changer de mot[i]
i += 2; // sauter l'index suivant
} autre {
++i; // aucun changement nécessaire
}
}
le nombre de retours;
}
}
«» "

**Explication**
- La boucle `pour` est intentionnellement laissée sans `i++` dans la section incréments.
- Les(...) ≤ 1 ' capture égale ou adjacente.
- `i += 2` signifie "après avoir changé le caractère actuel, le caractère que nous venons de changer est garanti sûr avec son voisin droit"

---

4.7 Réflexions finales – Comment faire en sorte que cela se produise dans une entrevue avec les FAANG

1. **Décrivez d'abord votre intuition**: Quand je vois une paire presque égale, je dois changer la bonne. (en milliers de dollars)
2. **Écrivez une boucle concise**; vous montrez que vous comprenez les contraintes temporelles et spatiales.
3. **Talk à travers les cas de bord** (premier/dernier caractère, longueur de chaîne 1).
4. **Discute brièvement les alternatives** et explique pourquoi l'avidité est optimale.

En maîtrisant LeetCode 2957, vous démontrerez :
- **L'état d'esprit de résolution des problèmes**
- **OOP & style fonctionnel** (Java, Python, C++)
- **Social-time tradeoff sensibilisation* *
- **Compétences en communication de l'interview* *

Ce sont exactement les traits recherchés par les recruteurs dans les candidats pour **FAANG** (Amazon, Google, Apple, Netflix, Facebook) et d'autres rôles de technologie à forte croissance.

---

### 4.8 Liste de contrôle du référencement

Mot-clé
C'est quoi, ça ?
Titre, H1, premier paragraphe
Enlever les caractères adjacents presque égaux Titre, H1, corps
Le bon, le corps
H2 Le mal, le corps
Description de la méta, conclusion
H2 Pourquoi ça fait mal, le corps
Entretien de l'algorithme
Conseils d'entretien d'emploi

Ajoutez des liens internes à votre repo GitHub avec les trois implémentations, et encouragez les lecteurs à les exécuter localement.

---

4.9 Liste de contrôle à emporter

- **Lire les contraintes**: 100 chars → œuvres gourmandes.
- **Comprendre "presque égal"**: "abs(a-b) ≤ 1".
- **Scan de gauche à droite, changer de côté droit, sauter deux**.
- **Heure**: "O(n)"
- **Espace**: "O(1)"
- **Éviter la suringénierie**: Pas de PDD, pas de gymnastique datastructure.

Maintenant, vous pouvez répondre avec confiance au LeetCode 2957 lors de votre prochain entretien de codage et impressionner les gestionnaires d'embauche avec une solution propre et optimale. Bon codage !

---