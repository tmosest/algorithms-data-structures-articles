---
titre: LeetCode 2105. Plantes d'arrosage II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes – LeetCode 2105: *Abreuvement des plantes II*

> **Objectif** – Comptez le nombre minimum de fois où Alice et Bob doivent remplir leurs canettes d'arrosage tout en arrosant une rangée de plantes.
> **Règles**
> * Alice commence à index 0 et se déplace à droite, Bob commence à index *n‐1* et se déplace à gauche.
> * Les deux boîtes sont initialement pleines (capacité A et capacité B).
> * Si une personne a assez d'eau dans le courant peut *entièrement* arroser la plante qu'elle est sur le point d'arroser, elle l'utilise simplement.
> * Dans le cas contraire, ils se rechargent immédiatement à pleine capacité puis arrosent l'usine.
> * Si tous deux atteignent la même plante, celui qui a *plus* d'eau dans leur peut l'arroser; si égal, Alice l'arrose.

**Contrôles* *

- Oui.
-- -- -- -- -- --
< 1 ≤ n ≤ 105 > 1 ≤ installations[i] ≤ 106 >
"max(plantes[i]) ≤ capacitéA, capacitéB ≤ 109 %

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Idée algorithmique**La simulation à deux points est *O(n)*, *O(1)* espace. Sans la vision à deux points, vous pourriez penser à un PD ou une force brute qui serait *O(n2)* ou pire. Si vous oubliez la règle de la même usine, vous pouvez finir par mal compter les recharges et la solution échoue sur des tests cachés. Autres
**Cas d'Edge** Beaucoup de personnes interrogées ignorent la règle de priorité de la même plante. La logique de l'usine intermédiaire peut devenir une source de bugs subtils – par exemple oublier de vérifier qui peut avoir plus d'eau avant de décider une recharge. Autres
**Mise en œuvre**=Les variables sont claires: `left`, `right`, `currA`, `currB`, `refillA`, `refillB`.=La surcomplication avec des fonctions ou des objets supplémentaires. En utilisant l'état mutable global ou en recomputant l'eau courante après chaque recharge dans les boucles (fait le code messy et error-prone). Autres

> **Ligne de bottom:** Gardez la boucle à deux points, manipulez soigneusement l'usine centrale et écrivez du code propre et commenté. C'est le bon. Le "bad" est de surpenser la simulation ou d'oublier la règle de priorité. Le "gugly" est des changements d'état désordonnés qui rendent la logique illisible.

---

## 3-- Solution à travers

1. **Pointeurs**
* `gauche` commence à l'usine la plus à gauche (index 0).
* `à droite` commence à l'usine la plus droite (index *n‐1*).
Ils se déplacent l'un vers l'autre jusqu'à ce qu'ils se rencontrent ou se croisent.

2. **Eau et renouvellements actuels**
* `currA` et `currB` tiennent le reste de l'eau dans les boîtes Alice et Bob.
* `rechargeA` et `rechargement B` compter le nombre de recharges chaque personne effectuée.

3. **Simulez une étape**
Pour chaque itération où "gauche < droite":
* **Alice** – Si `plants[left] ≤ currA`, soustrayez-le; sinon incrément `refillA` et définissez `currA = capacityA - plants[left]`.
* **Bob** – Logique analogique utilisant "right".

Puis avancez les pointeurs (`left++`, `right--`).

4. **Plante intermédiaire* *
Si la longueur du tableau est étrange, après la boucle `gauche == droite`.
* L'usine de `gauche` doit être arrosée par la personne qui dispose actuellement de plus d'eau (`currA` vs. `currB`).
* Si cette personne manque de suffisamment d'eau, elle doit recharger une fois de plus (incrémenter son compteur de recharge).

5. **Réponse** – Retour `rechargeA + rechargeB`.

---

Mise en œuvre du code

On trouvera ci-dessous des extraits de fichiers prêts à être compilés et à exécuter dans **Java**, **Python** et **C++**.

---

Java

"Java
***
* LeetCode 2105 – Plantes d'arrosage II
*
* Simulation à deux points avec temps O(n) et espace O(1).
*/
solution de classe {
Remplissage des installations, capacité intA, capacité intB
Int gauche = 0;
int droite = plante.longueur - 1;
int currA = capacitéA, currB = capacitéB;
Remplissage à l'intérieurA = 0, remplissageB = 0;

pendant que (à gauche < à droite) {
// Alice
si (plantes [à gauche] > currA) {
recharge A++;
currA = capacitéA - plantes[gauche];
} autre {
currA -= plantes[gauche];
}
gauche++;

// Bob
si (plantes [à droite] > currB) {
rechargeB++;
currB = capacitéB - plantes[droite];
} autre {
currB -= plantes[à droite];
}
droit...
}

// Une plante gauche au milieu (longueur oed)
si (à gauche) {
si (currA >= currB) {
si (plantes [à gauche] > currA) {
recharge A++;
}
} autre {
si (plantes[gauche] > currB) {
rechargeB++;
}
}
}

recharge de retourA + rechargeB;
}
}
«» "

---

Python

'`python
"""
LeetCode 2105 – Plantes d'arrosage II
Heure: O(n)
Espace: O(1)
"""

Solution de classe:
def minimumRemplissage(auto, usines: list[int], capacitéA: int, capacitéB: int) -> Int:
gauche, droite = 0, len(plantes) - 1
currA, currB = capacitéA, capacité B
rechargeA = rechargeB = 0

à gauche < à droite:
# Alice
si la plante[gauche] > currA:
RemplirA += 1
currA = capacitéA - plantes[gauche]
Sinon:
currA -= plantes[gauche]
gauche += 1

♪ Bob
si les plantes [à droite] > currB:
rechargeB += 1
currB = capacitéB - plantes[droite]
Sinon:
currB -= plantes[droite]
droite -= 1

# Plante moyenne (longueur humide)
si gauche == à droite:
si currA >= - Oui.
si la plante[gauche] > currA:
RemplirA += 1
Sinon:
si la plante[gauche] > currB:
rechargeB += 1

recharge de retourA + rechargeB
«» "

---

C++

'`cpp
***
* LeetCode 2105 – Plantes d'arrosage II
* Solution à deux points, temps O(n), espace O(1)
*/
solution de classe {
public:
int minimumRemplissage(vecteur<int>&usines, capacité intA, capacité intB) {
int gauche = 0, droite = plants.size() - 1;
int currA = capacitéA, currB = capacitéB;
Remplissage à l'intérieurA = 0, remplissageB = 0;

pendant que (à gauche < à droite) {
// Alice
si (plantes [à gauche] > currA) {
++recharge A;
currA = capacitéA - plantes[gauche];
} autre {
currA -= plantes[gauche];
}
+ + gauche;

// Bob
si (plantes [à droite] > currB) {
+rechargeB;
currB = capacitéB - plantes[droite];
} autre {
currB -= plantes[à droite];
}
--droite;
}

// Il reste une plante (nombre de plantes)
si (à gauche) {
si (currA >= currB) {
si (plantes[gauche] > currA) ++refillA;
} autre {
si (plantes[gauche] > currB) ++rechargeB;
}
}

recharge de retourA + rechargeB;
}
};
«» "

---

C'est pas vrai. Comment utiliser ces solutions dans une entrevue technique

Où coller Que mettre en évidence
Il y a un problème.
**Java**"class Solution" dans l'éditeur de LeetCode.
*Python * Solution "class" avec "def minimumRefill" Afficher la boucle propre et le garde "middle-plant"
**C++**= Solution de classe avec `public:` Souligner l'espace constant – les intervieweurs l'adorent

**Conseil:** Au cours d'une entrevue, marcher l'intervieweur à travers la boucle sur un petit exemple (`[1, 2, 3, 2, 1]`) et pointer la règle de priorité à l'usine centrale.

---

Article de blog optimisé du SEO
> *Titre: Le bon, le mauvais, et le mauvais de l'arrosage des plantes II – Java, Python, et C++ LeetCode 2105 Solution*

> *Meta‐Description:* Master LeetCode 2105 .Utiliser les plantes II avec une solution à deux points propre en Java, Python et C++. Apprenez les pièges, la manipulation des caisses et pourquoi ce problème est un favori dans les entrevues techniques.

---

Pourquoi ce problème est un billet d'or* pour votre préparation d'entrevue

** Clarté conceptuelle** – Le modèle de "deux points" est un must-know pour les entrevues par algorithme.
- **La pertinence du monde réel** – C'est un excellent exemple de simulation de l'état* (comme les problèmes d'aspirateur de robots ou de parking de voitures).
- **agnostique de la langue** – Vous pouvez le résoudre en **Java, Python ou C++**, prouvant la polyvalence avec les gestionnaires d'embauche.

> **Mot-clé de référence**: *technique à deux points LeetCode*, *solution d'arrosage des plantes II*.

---

Les mauvais** – Les pièges communs

- **Oublier la priorité de la même plante** – mène à une mauvaise réponse sur les entrées de longueurs impaires.
- **Mixer les pointeurs** – par exemple, augmenter le "droit" avant de diminuer le "currB".
- **Utiliser une mémoire supplémentaire** – par exemple, créer un vecteur de recharges qui n'est jamais nécessaire.

> **Mot-clé du référencement**: *Bugs d'arrosage des plantes II*, *règle de priorité LeetCode 2105*.

---

**La mise en œuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en oeuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de la mise en œuvre de

- **Mutant plusieurs variables en une seule ligne** – rend la logique illisible.
- **Récursion ou DP** – solutions `O(n2)` ou `O(n log n)` qui TLE ou MLE sur de grandes entrées.
- **Ignorer le trop-plein entier** – en particulier lorsque `capacité` et `plantes[i]` sont tous deux proches de `109`.

> **Mot-clé de référence**: *Réussir l'entrevue avec les Plantes d'eau II*, *délai-complexité LeetCode 2105*.

---

Liste de contrôle finale avant la soumission

1. **Lisez attentivement l'invite** – surtout la règle de la même plante.
2. ** Courir dans tous les cas exceptionnels** :
* Une seule usine.
* Drôle de longueur.
* Capacités plus grandes que toutes les eaux végétales.
* Capacités exactement égales à l'eau de la plante.
3. **Vérifier avec les exemples de cas** de LeetCode.
4. **Ajouter quelques tests personnalisés** (par exemple, `plants=[10,10,10], capacitéA=10, capacitéB=10` → réponse `2`).
5. **Temps de votre solution** – Il devrait être O(n) dans toutes les langues; pas de boucles ni de structures de données supplémentaires.

---

Enveloppe

* **Plantes d'arrosage II** est un exemple *textbook* d'une simulation à deux points.
* La clé est de manipuler correctement l'usine centrale.
* Le code propre en Java, Python et C++ met en évidence votre capacité à traduire un énoncé de problème en code prêt à la production.

Bonne chance pour votre prochain entretien technique – ce problème est un excellent élément -show‐off )