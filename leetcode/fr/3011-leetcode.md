---
titre: LeetCode 3011. Trouver si Array peut être trié -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Leetcode 3011 – *Trouver si Array peut être trié*
**Difficulté:** Moyenne
**Tags:** Manipulation bit

Récapitulation des problèmes
On vous donne un tableau 0 indexé `nums` d'entiers positifs.
Vous pouvez effectuer ** n'importe quel numéro** de l'opération suivante:

*Choisissez deux éléments adjacents qui ont **le même nombre de bits de jeu** (compte pop) et échangez-les. *

Retourner `true` si, après une séquence de tels swaps, le tableau peut être trié dans l'ordre croissant **; sinon retourner `false`.

---

- Oui. Aperçu clé
Deux numéros adjacents peuvent être échangés **seulement** lorsque leur pop-count est identique.
Cela signifie que:

1. **Dans chaque bloc contigu d'égal pop-count**, vous pouvez réorganiser librement les éléments (tout comme la bulle-sort).
2. **Entre les blocs de différents pop-count** vous *ne pouvez pas* éléments croisés.

Par conséquent, le tableau peut être trié si les blocs eux-mêmes sont déjà en ordre ascendant.
Formellement :

«» "
Bloc 1 : Bloc 2 : Bloc 3 : ...
«» "

être les groupes contigus maximaux d'égale pop-count.
Si `max(Block i) < min(Block i+1)` pour chaque paire adjacente, le tri est possible, sinon il n'est pas.

---

####=3=0 O(n) Mise en oeuvre de l'avidité
Nous pouvons faire un seul passage de gauche à droite:

Texte
prevMax = --
currMax = nombres[0]
currPop = popcount(nums[0])

pour chaque nombre suivant[1:]:
pop = popcount(next)
if pop == currPop: // même bloc
currMax = max(currMax, suivant)
Sinon: // nouveau bloc commence
si la suivante < prevMax: // viole l'ordre ascendant
Retour Faux
prevMax = currMax
currPop = pop
currMax = suivant

retour Vrai
«» "

La vérification finale (`next < prevMax`) garantit que chaque nouveau bloc commence avec une valeur **pas plus petite** que le maximum du bloc précédent.

---

Code (trois langues)

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
pulvérisateur public de booléen
si (nums.longueur <= 1) retourner vrai;

int prevMax = entier.MIN_VALUE;
la valeur d'int currMax = nombres[0];
Int currPop = Integer.bitCount(nums[0]);

pour (int i = 1; i < nombres de longueur; i++) {
Int val = nombres[i];
Int pop = Integer.bitCount(val);

si (pop == currPop) { // même bloc pop-count
currMax = Math.max(currMax, val);
} autre { // nouveau bloc commence
si (val < prevMax) retourner faux;
prevMax = currMax;
currPop = pop;
currMax = valeur;
}
}
retour vrai;
}
}
«» "

> **Complexité**:
> *Heure* – «O(n)»
> *Espace* – "O(1)" (seulement quelques variables entières)

---

3.2 Python 3

'`python
Solution de classe:
def canSortArray(self, nombres: List[int]) -> bool:
si len(nums) <= 1:
retour Vrai

prev_max = flotteur('-inf')
curr_max = nombres[0]
curr_pop = bin(nums[0]).count('1')

pour la valeur en chiffres[1:]:
pop = bin(val).count('1')
if pop == curr_pop :
curr_max = max(curr_max, val)
Sinon : # nouveau bloc pop-count
si val < prev_max:
Retour Faux
prev_max = curr_max
_pop_curr = pop
curr_max = valeur

retour Vrai
«» "

> **Complexité**:
> *Heure* – «O(n)»
> *Espace* – "O(1)"

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool canSortArray(vecteur const<int>& nums) {
si (nums.size() <= 1) retourner vrai;

int prevMax = INT_MIN;
la valeur d'int currMax = nombres[0];
nt currPop = __constructin_popcount(nums[0]);

pour (size_t i = 1; i < nums.size(); ++i) {
Int val = nombres[i];
int pop = __constructin_popcount(val);
si (pop == currPop) { // même bloc
currMax = max(currMax, val);
} autre { // nouveau bloc
si (val < prevMax) retourner faux;
prevMax = currMax;
currPop = pop;
currMax = valeur;
}
}
retour vrai;
}
};
«» "

> **Complexité**:
> *Heure* – «O(n)»
> *Espace* – "O(1)"

---

Billet de blog – *Le bon, le mauvais et le mauvais: Mastering Leetcode 3011 pour votre prochaine interview*

> **Title de la Meta**
> **Meta Description**= Apprenez la solution O(n) slick pour Leetcode 3011. Comprendre l'astuce de block-check, voir le code Java/Python/C++ et préparer votre prochain entretien d'emploi.

---

- Oui. Le Bon – Pourquoi Ce problème est un Gold-Mine pour les entrevues

Aspect Pourquoi c'est bon
C'est quoi, ça ?
**Simplicité conceptuelle**= Une seule analyse linéaire, pas de structures de données supplémentaires. Autres
**Manipulation de bits**= Sujet populaire dans les entrevues; montre un aperçu de bas niveau. Autres
**Greedy / Block Reasoning**= Affiche la capacité de réduire un problème à ses contraintes *core*. Autres
**Performance**=Patige 100 % sur le Leetcode; parfait pour les questions sur le temps. Autres
**Langues multiples**=Illustre la fluidité du codage en plusieurs langues (Java, Python, C++). Autres

**Takeaway**: Maîtriser ce problème prouve que vous pouvez lire les contraintes, repérer l'indépendance cachée, et concevoir une passe cupide propre – tous les traits embauche managers aiment.

---

- Oui. Les mauvaises – pièges communs

Comment éviter
C'est quoi ?
**Remise en œuvre du compte pop**=Utiliser le compte pop intégré `Integer.bitCount`, `bin().count('1')` ou `_builtin_popcount`. Autres
**Tracking min & max par bloc**= Nous n'avons besoin que du *maximum* de chaque bloc parce que le premier élément du bloc suivant est le seul qui compte. Autres
**Two-pass bubble tri** Autres
**Oublier le bloc final**La boucle assure déjà l'exactitude; aucun contrôle post-boucle supplémentaire n'est nécessaire. Autres

---

### Les cas de sur-ingénierie et de bord

- **Utiliser une carte de pop-count → vector** → O(n) espace, facteurs constants plus lents.
- **Désorption explicite de chaque bloc** (par exemple, "Arrays.sort(subarray)") → O(n log n) par bloc → pas nécessaire.
- **Handling nombres négatifs ou zéro**: le problème garantit `nums[i] > 0`, mais si vous obtenez un cas de test avec `0`, `popcount(0) == 0`, fonctionne toujours.

**Bottom Line**: Gardez la solution maigre – pas de tableaux inutiles, pas de boucles supplémentaires, seulement quelques variables entières.

---

## OBJET DE L'ENQUÊTE

Terme de recherche
C'est-à-dire
*Leetcode 3011 solution*
*question d'entrevue de tri d'array*
*bit count algorithme avide Souligne les compétences techniques
*C++ Java Python Leetcode*
*Algorithme d'entretien d'emploi*= Attire les recruteurs à la recherche d'un entretien prép=

** Aperçus**
1. Leetcode 3011: Trouver si Array peut être trié – le bon, le mauvais, et le mauvais
2. Solution pour trier les tableaux par Pop-Count

**Étiquettes Meta* *
html
<meta name="title" content="Leetcode 3011 – Trouver si Array peut être trié (Java, Python, C++)">
<meta name="description" content="Apprenez l'astuce cupide pour le Leetcode 3011. Voir le code O(n) Java, Python et C++. Préparez-vous à votre prochaine entrevue de codage.">
<meta name="keywords" content="Leetcode 3011, tri de tableaux, manipulation de bits, question d'entretien, algorithme, Java, Python, C++">
«» "

**Extrait**
> Master Leetcode 3011 en 10 minutes. Découvrez pourquoi pop-count bloque la matière, voyez une solution O(n) croustillante en Java, Python et C++, et lisez un blog prêt à travailler expliquant l'astuce derrière le succès de ce problème apparemment difficile. (en milliers de dollars)

---

Résumé

* **Problème** – trier via des swaps autorisés uniquement dans des blocs pop-count égaux.
* **Solution** – un passage, suivre le dernier bloc maximum.
* **Complexité** – temps "O(n)", espace "O(1)".
* **Langues** – Java, Python, C++ (toutes montrées).

Avec cette connaissance, vous serez prêt à ace Leetcode 3011, impressionner les recruteurs, et déplacer un pas plus près de votre travail de rêve. Bon codage 