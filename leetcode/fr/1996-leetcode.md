---
titre: LeetCode 1996. Le nombre de personnages faibles dans le jeu -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1996
**Le nombre de personnages faibles dans le jeu**

> Un jeu contient des caractères `n`.
> `properties[i] = [attack_i , defense_i]` est l'attaque et la défense du caractère *i‐th*.
> Un caractère *i* est *faible* s'il existe un autre caractère *j* tel que
> `attaque_j > attaque _i` ** et** `défense_j > défense_i`.
> Retourner le nombre total de caractères faibles.

**Contrôles* *

2 ... 105
-- -- -- -- -- --
1 ... 105

Le problème est une requête de dominance 2 dimensions classique et peut être résolu en **O(n log n)** temps avec un simple tri + balayage.

---

- Oui. 2. Idée de haut niveau – Dégustation + Plongée de graisse

1. **Trier** tous les caractères par attaque ascendante.
*Si deux personnages ont la même attaque, nous devons traiter celui avec la défense **plus élevée** d'abord* – sinon un personnage plus tard pourrait à tort être considéré faible.
Par conséquent, la clé de tri est
Texte
(attaque, défense) // attaque ascendante, défense descendante
«» "

2. Après tri, marcher sur le tableau **en arrière** (de la plus haute attaque à la plus basse).
Gardez une variable `maxDef` qui stocke la défense maximale vue jusqu'ici parmi les personnages avec une attaque *plus élevée*.

3. Pour le caractère actuel :
* si sa défense < `maxDef` → il est faible.
* autrement mettre à jour `maxDef` avec cette défense.

4. Compte tous ces personnages faibles.

L'intuition : un personnage ne peut être dominé que par un personnage plus tard (plus élevé). Parce que nous traitons en ordre inverse, `maxDef` contient déjà la meilleure défense parmi tous les caractères d'attaques supérieures. Une comparaison simple nous indique si le caractère actuel est dominé.

---

- Oui. 3. Passage du code

Vous trouverez ci-dessous **mises en œuvre prêtes à être copiées** dans :

Classe / Fonction Autres
C'est le cas.
Autres Java="Solution.numberDeWeakCaracters`=" Utilise `Arrays.sort` avec un comparateur personnalisé. Autres
Python="Solution.number_of_weak_caracters`=" Utilise `sort` avec la clé et une boucle inverse. Autres
* C++* `Solution::numberDeWeakCaracters`* Utilise `std::sort` et un seul passage. Autres

Chaque solution est **O(n log n)** temps, **O(1)** espace supplémentaire (à l'exception du tri des frais généraux).

---

#### 3.1 Java – `Solution.numberOfWakCaracters "

"Java
Importer java.util. Les tableaux;

solution de classe {
numéro d'entrée publicDeWeakCaractéristiques(int[][]propriétés) {
// Tri par attaque ascendante; si cravate, défense descendante
Tableaux.sort(propriétés, a, b) -> {
si (a[0] == b[0]) retourner Integer.comare(b[1], a[1]); // plus haute défense d'abord
retour Integer.compare(a[0], b[0]); // attaque inférieure d'abord
});

Int faible = 0;
int maxDef = 0; // meilleure défense vue jusqu'à présent parmi les attaques plus élevées
pour (int i = propriétés.longueur - 1; i >= 0; i--) {
int def = propriétés[i][1];
si (déf < maxDef) faible++;
sinon max Déf = def; // nouvel enregistrement
}
retour faible;
}
}
«» "

---

### 3.2 Python – `Solution.number_of_faible_caractères "

'`python
Solution de classe:
Numéro OfWeakCaracters(self, properties: List[List[int]]) -> Int:
Tri par attaque ascendante, défense descendante
propriétés.sort(key=lambda x: (x[0], -x[1]))

faible = 0
max_def = 0
pour _, def_val en inverse(propriétés):
if def_val < max_def:
faible += 1
Sinon:
max_def = def_val
retour faible
«» "

---

### 3.3 C++ – `Solution::numberOfWakCaracters "

'`cpp
solution de classe {
public:
nombre intDeWeakCaracters(vecteur<vector<int>>&propriétés) {
tri(properties.begin(), properties.end(),
[](const vector<int>& a, const vector<int>& b) {
si (a[0] == b[0]) retourne a[1] > b[1]; // défense supérieure d'abord
retour a[0] < b[0]; // attaque inférieure d'abord
});

Int faible = 0;
Int maxDef = 0;
pour (int i = propriétés.size() - 1; i >= 0; --i) {
int def = propriétés[i][1];
si (déf < maxDef) ++faible;
sinon max Déf = def;
}
retour faible;
}
};
«» "

---

- Oui. 4. Analyse de la complexité

**Métrique**
-- -- -- -- -- --
Temps **O(n log n)** – dominé par l'étape de tri. Autres
Espace supplémentaire **O(1)** – seulement quelques variables entières. (Le tri lui-même peut utiliser l'espace de la pile O(log n). Autres

---

- Oui. 5. Cas de bord et pièges

Problème
C'est le cas.
Autres Deux caractères ont la même attaque. Trier seulement par attaque peut marquer la seconde faible incorrectement. Trier par défense descendante quand attaque liens.
Autres Très grande `n` (105).L'utilisation d'une boucle imbriquée O(n2) provoque.
Valeurs défensives aux limites Aucune manipulation spéciale nécessaire – l'algorithme fonctionne pour toutes les valeurs
Les contraintes garantissent `n ≥ 2`, mais le code défensif peut gérer `n==0`

---

- Oui. 6. Le bien, le mal et le mal

Aspect du bien
C'est pas vrai.
Une solution O(n log n) simple – facile à raisonner et à implémenter.
**Sorting Key**="(attack, -defense)" est un modèle bien connu pour la dominance 2-D=" Oublier l'égalité de défense-break → mauvaise réponse=" Trier par attaque seulement puis scanner à l'envers conduit à des bugs subtils="
L'utilisation de tableaux supplémentaires de taille 105+2 est inutile
**Readability**=Clean comparateur or key function=== Loops imbriquées, trop de variables== Code à un liner qui sacrifie la clarté===

---

- Oui. 7. Ébauche d'un billet de blog optimisé par le SEO

> **Titre:**
> LeetCode 1996 – Le nombre de caractères faibles: Java, Python & C++ Solutions + Conseils d'entrevue
> **Méta—Description:**
> Master LeetCode 1996 en moins de 15 minutes. Apprenez le tri O(n log n) + solution de balayage gourmand en Java, Python et C++. Préparez-vous à l'entrevue avec des pièges, des cas de bord et des conseils de référencement pour la recherche d'emploi.

---

7.1 Introduction

Si vous préparez une interview d'ingénierie logicielle, vous aurez presque certainement à traverser **LeetCode 1996 – Le nombre de personnages faibles**. Ce problème de difficulté moyenne teste votre compréhension de la dominance 2-D et des astuces de tri. Voici une plongée profonde dans la solution la plus efficace, ainsi que des implémentations prêtes à coller en Java, Python et C++. Je vais aussi marcher à travers des pièges communs, pourquoi le balayage avide fonctionne, et comment cette connaissance peut stimuler votre CV.

---

#### 7.2 Énoncé du problème (reformulé)

Vous êtes donné un tableau 2-D `propriétés`, chaque élément `[attaque, défense]`. Un caractère *i* est **faible** si un autre caractère *j* a **attaque strictement supérieure ET défense strictement supérieure**. Comptez combien de personnages sont faibles.

---

7.3 Pourquoi le O(n log n) Greedy Sweep fonctionne

1. **Dominance en 2-D** – Un personnage ne peut être dominé que par un personnage qui est à sa droite lorsqu'il est trié par attaque.
2. **Clause de tri** – Lorsque les attaques se recoupent, le personnage avec une défense *plus élevée* domine celui avec une défense *plus faible*. Le tri par `(attack, -defense)` permet d'obtenir d'abord le bon.
3. **Passer en arrière** – En marchant du personnage le plus droit au personnage le plus gauche, nous maintenons `maxDef`, la meilleure défense parmi les personnages déjà vus (attaque plus élevée).
4. **Comparaison unique** – Si la défense actuelle < `maxDef`, le caractère courant est faible; sinon, mettre à jour `maxDef`.

Aucune structure de données supplémentaire n'est nécessaire, rendant l'algorithme propre et rapide.

---

7.4 Mise en œuvre des codes

> **Astuce:** Collez ces extraits directement dans votre éditeur de solution LeetCode.

C'est vrai. Java

"Java
Importer java.util. Les tableaux;

solution de classe {
numéro d'entrée publicDeWeakCaractéristiques(int[][]propriétés) {
Tableaux.sort(propriétés, a, b) -> {
si (a[0] == b[0]) retourne Integer.compare(b[1], a[1]);
retour Integer.compare(a[0], b[0]);
});

Int faible = 0;
Int maxDef = 0;
pour (int i = propriétés.longueur - 1; i >= 0; i--) {
int def = propriétés[i][1];
si (déf < maxDef) faible++;
sinon max Déf = def;
}
retour faible;
}
}
«» "

Python

'`python
Solution de classe:
Numéro OfWeakCaracters(self, properties: List[List[int]]) -> Int:
propriétés.sort(key=lambda x: (x[0], -x[1]))
faible, max_def = 0, 0
pour _, def_val en inverse(propriétés):
if def_val < max_def:
faible += 1
Sinon:
max_def = def_val
retour faible
«» "

C++

'`cpp
solution de classe {
public:
nombre intDeWeakCaracters(vecteur<vector<int>>&propriétés) {
tri(properties.begin(), properties.end(),
[](const vector<int>& a, const vector<int>& b) {
si (a[0] == b[0]) retourne a[1] > b[1];
retourner a[0] < b[0];
});

Int faible = 0, maxDef = 0;
pour (int i = propriétés.size() - 1; i >= 0; --i) {
int def = propriétés[i][1];
si (déf < maxDef) ++faible;
sinon max Déf = def;
}
retour faible;
}
};
«» "

---

### 7.5 Edge- Cas que vous devez couvrir

Pourquoi ça compte? Votre code.
C'est le cas.
"propriétés = [[2,1],[2,1]]""" Deux stats identiques – ni l'un ni l'autre n'est faible"
Autres Liens d'attaque avec la défense décroissante ─ Mauvais ordre → dominance erronée
Large `n`=" Brute force O(n2) fois out

---

7.6 Questions à poser au niveau de l'entrevue

Lors d'un entretien réel, l'intervieweur pourrait sonder :

* Et si vous devez compter les caractères *non-faibles* à la place? (en milliers de dollars)
* Pouvez-vous atteindre le temps O(n) en utilisant un arbre Fenwick? (en milliers de dollars)
* Et si la taille d'entrée est 106? Des solutions pour la mémoire ? (en milliers de dollars)

Ces questions mesurent votre profondeur de compréhension et d'adaptabilité.

---

7.7 Ajouter la solution à votre curriculum vitae

> **Pourquoi c'est important:** Les intervieweurs aiment des solutions concises et optimales.
> **Reprendre l'exemple du libellé :**
> • Implémenté une solution **O(n log n)** pour le problème de LeetCode.
> • Expertise démontrée en dominance 2D, en conception d'algorithmes et en compromis dans l'espace temporel.

Inclure le lien GitHub ou l'extrait de code dans un portfolio ou comme référence de projet.

---

7.8 Pensées de clôture

LeetCode 1996 est un petit problème avec une grande leçon : * commander des choses.* Souvenez-vous du truc `(attaque, -défense)`, balayez de droite à gauche, et vous passerez ce problème en un éclair. Appliquer le même modèle à n'importe quel problème de dominance que vous voyez dans les entretiens. Bonne chance – et continuez à coder!

---

- Oui. 8. Mots définitifs

Vous possédez maintenant :

* Une solution **robuste, optimale**.
* ** Trois extraits spécifiques au langage** qui fonctionneront rapidement sur LeetCode.
* **Pièges communs** à protéger.
* A **histoire** vous pouvez tisser dans votre récit d'entrevue.

Joyeux entretien !

---

* Se sentir libre d'adapter le post de blog à votre propre voix ou plate-forme. *