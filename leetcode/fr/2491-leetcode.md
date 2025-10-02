---
titre: LeetCode 2491. Diviser les joueurs dans des équipes d'égale compétence -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2491 – Diviser les joueurs dans des équipes d'égale compétence
**Langues**: Java, Python, C++
**Complexité**: temps O(n log n), espace supplémentaire O(1) (tri en place)

---

- Oui. 1. Récapitulation des problèmes

On vous donne un tableau **d'égale durée** «kill» («1 ≤ habileté[i] ≤ 1000»).
Vous devez coupler les joueurs (taille 2) pour que **chaque paire ait la même compétence totale**.
Si c'est possible, retourner la somme ** de la chimie** (produit des compétences de chaque paire); sinon retourner `-1`.

---

- Oui. 2. Pourquoi trier + Deux-Pointeurs fonctionne

1. **Trier** le tableau – alors la plus petite valeur est à l'avant et la plus grande à l'arrière.
2. Si une partition valide existe, la paire qui contient la valeur *la plus petite* doit également contenir la valeur *la plus grande*, car tout autre choix ferait la somme plus petite que la cible requise.
3. Après la fixation de la première paire, la plus petite et la plus grande suivante doit à nouveau s'ajouter à la même cible, et ainsi de suite.
4. Si une paire s'écarte de cette somme, une partition valide est impossible.
5. Pendant l'appariement, nous accumulons également le produit pour obtenir la chimie totale.

Ainsi, un seul balayage linéaire après tri donne la réponse.

---

- Oui. 3. Mise en œuvre du code

Voici des solutions propres et prêtes à la production pour **Java**, **Python** et **C++**.

---

#### 3.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public long écart Joueurs(int[] compétence) {
Tableau 3.
n = durée de compétence;
int cible = compétence[0] + compétence[n-1]; // somme que chaque paire doit atteindre
chimie longue = 0;

pour (int i = 0; i < n / 2; i++) {
si (compétence[i] + compétence[n-1-i] != cible) {
retour -1; // impossible
}
chimie += compétence (long)[i] * compétence[n-1-i];
}
la chimie du retour;
}
}
«» "

**Explication**
* `Arrays.sort(skill)` trie le tableau en place.
* La boucle tourne `n/2` fois – espace supplémentaire constant.
* La coulée à "long" empêche le débordement (produit maximum 1000 × 1000 = 1 000 000, sûr, mais la somme peut atteindre 10^11 pour n = 10^5).

---

3.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
déf diviser Joueurs(soi-même, compétence: Liste[int]) -> Int:
compétences.sort() # O(n log n)
n = len(skill)
cible = compétence[0] + compétence[-1] Nombre de paires requises
chimie = 0

pour i dans la plage(n // 2):
si compétence[i] + compétence[n - 1 - i] != cible:
retour -1
chimie += compétences[i] * compétences [n - 1 - i]
chimie du retour
«» "

**Pourquoi Python fonctionne**
* `list.sort()` modifie la liste en place.
* L'arithmétique entier en Python est débordé, donc pas de soucis de débordement.
* La logique est identique à Java et C++.

---

#### 3.3 C++ (GNU + +17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long et long fossé Joueurs(vecteur<int> et compétences) {
tri(skill.begin(), skill.end()); // O(n log n)
int n = compétence.size();
int cible = skill.front() + skill.back(); // somme de la paire qui doit correspondre

chimie longue = 0;
pour (int i = 0; i < n / 2; ++i) {
si (kill[i] + habileté[n - 1 - i] != cible) {
retour -1; // impossible
}
chimie += Compétence * compétences [n - 1 - i];
}
la chimie du retour;
}
};
«» "

**Notes**
* `1LL * ...` forces 64-bit multiplication.
* `sort()` utilise introsort – rapide et stable pour la plupart des entrées.

---

- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Tri de **O(n log n)**
Raccordement et somme
Total des dépenses

`n ≤ 10^5`, de sorte que la solution passe facilement tous les tests LeetCode.

---

- Oui. 5. Le bon, le mauvais, et le mauvais

Aspect du bien
- C'est quoi ?
**L'élégance algorithmique**=Le tri + deux points est *O(n log n)*, optimal pour les valeurs arbitraires==Il faut trier – ne peut pas être réduit au temps linéaire sans contraintes supplémentaires== Si l'entrée est déjà triée, nous trions encore (les frais généraux inutiles)
**Simplicité de la mise en œuvre**=Toutes les langues partagent un code presque identique== Très peu de lignes, mais oublier le casting `long` en Java/C++ provoque un débordement sur des entrées énormes=Les bogues de dépassement en C++ peuvent être subtils==
**Utilisation de la mémoire**= Tri en place – frais généraux négligeables== Nécessite une copie si nous voulons préserver le tableau original== Certains juges en ligne refusent la mutation en place– doivent quand même copier===
**Edge-cases**=Poigne les tableaux à paires uniques, les duplicatas et les grandes valeurs== Aucune – l'algorithme est déterministe==Si `skill.length` est étrange (bien que les contraintes l'interdisent) → comportement indéfini Autres
**Readability**= Noms de variables clairs (`cible`, `chimie`)== Très terse – un novice pourrait se battre=== Aucun – le code est intentionnellement court, mais la documentation est encore nécessaire==

---

- Oui. 6. Article de blog optimisé par le SEO

> **Titre**: *LeetCode 2491 – Diviser les joueurs dans des équipes d'égale compétence: Java, Python, & C++ Solutions*
> **Description détaillée**: Apprenez l'algorithme O(n log n) optimal pour LeetCode 2491. Obtenez le code Java, Python et C++ étape par étape, plus une plongée profonde dans la stratégie à deux points.

---

6.1 Introduction

Si vous êtes à la recherche de ce prochain **LeetCode question d'interview**, le problème 2491 est un défi *medium* classique qui teste le tri, la logique à deux points et la manipulation soigneuse du débordement entier.
Dans ce post, nous allons marcher à travers une solution propre et prête à la production, fournir des implémentations dans **Java**, **Python** et **C++**, et mettre en évidence les aspects *good*, *bad* et *ugly* de l'approche.

> **Mots clés**: LeetCode 2491, diviser les joueurs en équipes, compétence égale, solution Java, solution Python, solution C++, deux pointeurs, algorithme de tri, programmation compétitive, conception d'algorithmes

---

#### 6.2 Énoncé du problème (reformulé pour clarté)

Vous êtes donné un tableau `skill[]` de longueur uniforme.
La tâche : jumeler les joueurs de telle sorte que *chaque paire possède la même compétence totale*.
Si cette partition est possible, retourner la somme de chaque paire de *chimie* (produit des compétences).
Sinon, retourner `-1`.

*Constraints* :
- "2 ≤ longueur de compétence ≤ 10^5" (même)
- `1 ≤ compétences[i] ≤ 1000`

---

#### 6.3 Pourquoi trier + Deux-Pointeurs est la clé

1. Après tri, la plus petite (`skill[0]`) et la plus grande (`skill[n-1]`) doit former la somme de la paire de cibles ****.
2. La suivante plus petite et plus grande ('skill[1]' & `skill[n-2]`) doit aussi s'ajouter à cette cible, et ainsi de suite.
3. Une seule passe linéaire valide la partition *et* accumule la chimie.

La beauté : l'algorithme est **O(n log n)** en raison du genre, et **O(1)** mémoire supplémentaire.

---

#### 6.4 Pseudocode étape par étape

«» "
tri(s)
cible = compétence[0] + compétence[dernière]
chimie = 0
pour i en 0 .. N/2 − 1
si compétence[i] + compétence[n-1-i] != cible
retour -1
chimie += compétences[i] * compétences[n-1-i]
chimie du retour
«» "

---

6.5 Code complet – trois langues

> *Les extraits suivants sont prêts à être collés dans l'éditeur de LeetCode. *

**Java**
"Java
Importer java.util. Les tableaux;
solution de classe publique {
public long écart Joueurs(int[] compétence) {
les tableaux.sort(skill);
int n = compétence.longueur, cible = compétence[0] + compétence[n-1];
chimie longue = 0;
pour (int i=0;i<n/2;i++) {
si (compétence[i] + compétence[n-1-i] != cible) retourne -1;
chimie += compétence (long)[i] * compétence[n-1-i];
}
la chimie du retour;
}
}
«» "

**Python**
'`python
Solution de classe:
déf diviser Joueurs(soi-même, compétence: Liste[int]) -> Int:
compétences.sort()
n, cible = len(skill), compétence[0] + compétence[-1]
chem = 0
pour i (n//2):
si compétence[i] + compétence[n-1-i] != cible: retour -1
chem += compétences[i] * compétences[n-1-i]
retour
«» "

**C++**
'`cpp
solution de classe {
public:
long et long fossé Joueurs(vecteur<int> et compétences) {
tri(skill.begin(), skill.end());
int n = skill.size(), cible = skill.front() + skill.back();
longue chem longue = 0;
pour (int i=0;i<n/2;i++) {
si (compétence[i] + compétence[n-1-i] != cible) retourne -1;
chem += 1LL * compétence[i] * compétence[n-1-i];
}
la chimie de retour;
}
};
«» "

---

6.6 Cas de complexité et de bord

* **Time**: `O(n log n)` – dominé par le genre.
* **Espace**: "O(1)" – trier en place, seulement quelques variables primitives.
* **Overflow**: Dans Java/C++, utilisez `long`/`long'; Les ints de Python sont une précision arbitraire.

---

##### 6.7 Les bons, les mauvais et les mauvais

Aspect du bien
- C'est quoi ?
Algorithme Simple, optimum O(n log n)
Code Presque identique dans les langages.
Littérabilité : noms clairs (`cible`, `chimie`) Extrêmement courts – les novices peuvent manquer le 'longue` cast.

---

6.8 A emporter pour les entrevues

* Mettre en avant l'intuition **deux-pointeurs** : le plus petit + le plus grand doit correspondre à la cible.
* Mention **débordement entier** manipulation en langage statique.
* Montrez que l'algorithme est *déterministe* et *rapide* – des points de conversation parfaits pour un entretien d'ingénierie logicielle.

---

Mot final

Problème 2491 est une grande vitrine de la façon dont un classique * tri + deux-pointeurs* tour peut transformer un problème d'appariement apparemment combinatoire en un seul passage linéaire.
Avec les extraits de code Java, Python et C++ au-dessus de vous, vous serez prêt à **solve** sur LeetCode ou **crush** dans une interview en direct.

Bon codage ! C'est ce qu'il a dit.

---

**Balises pour moteurs de recherche* *
`#LeetCode2491`, `#DividePlayersIntoTeamsOfEqualSkill`, `#JavaSolution`, `#PythonSolution`, `#CppSolution`, `#TwoPointers`, `#SortingAlgorithm`, `#Compétitive Programmation, entretien Prép`, `#AlgorithmDesign "

---

Joyeux entretien !