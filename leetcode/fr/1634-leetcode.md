---
titre: LeetCode 1634. Ajouter deux polynômes représentés comme des listes liées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 1634 – Ajouter deux polynômes représentés comme des listes liées

> **Problème** – Fusionner deux polynômes de la liste liée qui sont déjà triés dans l'ordre **de puissance descendante stricte**, retournant un nouveau polynôme dans le même ordre.
> **Constraints** – `0 ≤ n ≤ 104`, coefficients dans `[-109, 109]`, pouvoirs dans `[0, 109]`.
> **Objectif** – temps `O(n)`, espace auxiliaire `O(1)` (la liste de sortie peut être construite en place).

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++** qui répondent aux exigences.

---

- Oui. Solution Java

"Java
***
* Définition d'une liste uni-liée représentant un terme polynôme.
*/
classe PolyNode {
coefficient int;
puissance int;
PolyNode suivant;
PolyNode(int coeff, int pow) { this.coefficient = coeff; this.power = pow; }
PolyNode(int coeff, int pow, PolyNode next) { this.coefficient = coeff; this.power = pow; this.next = next; }
}

solution de classe publique {

***
* Ajoute deux polynômes représentés par des listes liées.
* @param poly1 Chef de première liste polynôme
* @param poly2 Chef de la deuxième liste polynôme
* @retour Chef de la liste polynôme résumée
*/
PolyNode public addPoly(PolyNode poly1, PolyNode poly2) {
// La tête dummy simplifie la manipulation du premier nœud
mannequin PolyNode = nouveau PolyNode(0, 0);
PolyNode queue = mannequin;

alors que (poly1 != null && poly2 != null) {
Si (poly1.puissance > poly2.puissance) {
tail.next = poly1;
poly1 = poly1.next;
} sinon si (poly1.power < poly2.power) {
tail.next = poly2;
poly2 = poly2.suivant;
} autres { // Même puissance – coefficients de fusion
int newCoeff = poly1.coefficient + poly2.coefficient;
si (nouveau Coeff != 0) {/ Ne conserver que des termes non nuls
tail.next = nouveau PolyNode(nouveauCoeff, poly1.power);
}
poly1 = poly1.next;
poly2 = poly2.suivant;
}
queue = queue.suivante; // Déplacer la queue vers l'avant si un noeud était attaché
}

// Fixer la queue restante (poly1 ou poly2)
tail.next = (poly1 != null) ? poly1 : poly2;
retour mannequin.suivant;
}
}
«» "

**Pourquoi ça marche* *

Étape Qu'est-ce qui se passe ?
- C'est quoi ?
Autres Créer une tête de mannequin
Autres Bien que les deux listes ne soient pas vides, comparez les pouvoirs O(1) par itération
Autres 3.
Autres 4.- Sauter les résultats du coefficient zéro.
Autres Annexer la liste restante
Autres Retour `dummy.next`

Total: **O(n)** temps, **O(1)** espace auxiliaire.

---

Solution Python

'`python
de taper l'importation Facultatif

Classe PolyNode:
def __init__(self, coefficient: int, power: int, next: Facultatif['PolyNode']=Aucun):
auto.coefficient = coefficient
auto-puissance = puissance
self.next = suivant

def addPoly(poly1: Facultatif[PolyNode], poly2: Facultatif[PolyNode]) -> Facultatif[PolyNode]:
mannequin = PolyNode(0, 0)
arrière = mannequin

alors que poly1 et poly2:
si poly1.power > poly2.power:
tail.next = poly1
poly1 = poly1.suivant
elif poly1.power < poly2.puissance:
tail.next = poly2
poly2 = poly2.suivant
Autre : # pouvoir égal
new_coeff = poly1.coefficient + poly2.coefficient
si new_coeff: # sauter zéro terme
tail.next = PolyNode(new_coeff, poly1.power)
poly1 = poly1.suivant
poly2 = poly2.suivant
queue = queue. Suivant si queue. autre queue

# Joindre la liste restante
tail.next = poly1 ou poly2
retour mannequin.suivant
«» "

**Points clés**

* Utilise un noeud factice pour éviter les vérifications de bord pour le premier élément.
* Maintient un balayage linéaire et une mémoire supplémentaire constante.
* Manipulation pythonique de `Aucune` et liste de traversée.

---

C++ Solution

'`cpp
***
* Définition pour un noeud de liste uni-lié représentant un terme polynôme.
*/
struct PolyNode {
coefficient int;
puissance int;
PolyNode *suivant;
PolyNode(int coeff, int pow) : coefficient(coeff), power(pow), next(nullptr) {}
PolyNode(int coeff, int pow, PolyNode *n) : coefficient(coeff), puissance(pow), suivant(n) {}
};

solution de classe {
public:
PolyNode* addPoly(PolyNode* poly1, PolyNode* poly2) {
// Tête pour simplifier la fixation des nœuds
mannequin PolyNode(0, 0);
PolyNode* queue = &dummy;

alors que (poly1 & & poly2) {
si (poly1->puissance > poly2->puissance) {
arrière->suivant = poly1;
poly1 = poly1->suivant;
} sinon si (poly1->puissance < poly2->puissance) {
arrière->suivant = poly2;
poly2 = poly2->suivant;
} autre { // même puissance
int newCoeff = coefficient poly1-> + coefficient poly2->;
si (nouveau Coeff != 0) { // ne conserver que des termes non nuls
tail->next = nouveau PolyNode(nouveauCoeff, poly1->puissance);
}
poly1 = poly1->suivant;
poly2 = poly2->suivant;
}
queue = queue->suivant ? tail->next : tail; // déplacer seulement si nous avons attaché un noeud
}

// Ajouter le reste de la liste des non-vides
tail->next = poly1 ? poly1 : poly2;
retour mannequin.suivant;
}
};
«» "

---

- Oui. 2. Article de blog – Ajouter deux polynômes représentés comme des listes liées: le bon, le mauvais, et le mauvais

> **SEO Focus**: *Questions d'entretien de Java, Entretien de LinkedList, Solutions Leetcode, Entretien de Python, Entretien de C++, Ingénieur logiciel, Entretien d'emploi*

---

Introduction

Lors de la recherche de questions d'entrevue de Java, problèmes d'entrevue de Python, ou défis de codage d'entrevue de C++, *Ajouter deux polynômes représentés comme Listes liées* est un concurrent fréquent. Il mélange la manipulation classique de la liste liée à une torsion de l'algèbre, ce qui en fait un favori pour évaluer la fluidité de la structure des données et la pensée algorithmique.

Dans ce post, nous disséquerons le problème, explorerons les forces et les pièges des solutions communes et passerons par une mise en œuvre propre et prête à la production. À la fin, vous saurez exactement ce que les intervieweurs recherchent et comment présenter une réponse polie qui augmente vos chances d'obtenir ce travail de rêve.

---

### Le problème (LeetCode 1634)

On vous donne deux listes liées, chacune représentant un terme polynôme :

«» "
[coefficient, puissance]
«» "

Les deux listes sont déjà triées en ordre de puissance strictement descendant et ne contiennent pas de termes zéro coefficient.

**Tâche** – Fusionner les deux polynômes en une seule liste triée, additionner les coefficients avec la même puissance et omettre les termes qui donnent un coefficient zéro.

*Exemple*:
«poly1 = [[2,2],[4,1],[3,0]» 2x2 + 4x + 3)
«poly2 = [[3,2],[-4,1],[-1,0]]» (3x2 – 4x – 1)

** Sortie**: `[[5,2],[2,0]` 5x2 + 2)

---

### Le bon – Pourquoi c'est une grande question d'entrevue

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Liend-list basics**= Test de la capacité de traverser et de modifier des listes liées, une compétence de base pour tout développeur de backend. Autres
**Trier les invariants**=Les listes d'hypothèses sont pré-triées, de sorte que les candidats peuvent se concentrer sur la fusion plutôt que sur le tri. Autres
**Les cas d'Edge**=Les coefficients zéros, les puissances égales ou les listes vides forcent la manipulation prudente des conditions limites. Autres
Autres **Temps / Espace**.La solution optimale est le temps linéaire et l'espace auxiliaire constant – un spot d'interview classique. Autres
**Language agnostic**Vous pouvez le résoudre en Java, Python, C++ ou n'importe quelle langue qui supporte les listes liées. Autres

---

- Oui. Les mauvaises – pièges communs

Conséquences Évitement
C'est pas vrai.
**Ignorer les coefficients nuls** Vérifier explicitement si (somme != 0)» avant l'ajout. Autres
**Logique de comparaison des défauts** Utiliser clairement `if/else if/else` ou un seul `if (p1->power > p2->power) ... Sinon si... Autres
**Ne pas utiliser de tête factice** Créer un nœud factice et retourner `dummy.next`. Autres
**L'allocation de mémoire externe** Réutiliser les nœuds existants; n'attribuer que lorsqu'un nouveau nœud est nécessaire pour un terme fusionné. Autres
**Skipping `poly1.next` ou `poly2.next`**. Autres

---

### Les approches odieuses – trop compliquées

Parfois, les candidats implémentent **les fusions récurrentes** ou **l'agrégation de cartes hash**. Bien qu'ils soient corrects, ils rompent la règle d'espace "O(1)" (la pile de récursion compte comme mémoire). De plus, la création de nouveaux nœuds pour chaque terme (même si le terme existe dans l'une des listes d'entrées) gaspille du temps et peut entraîner des fuites de mémoire** dans des langues comme C++.

> **Astuce**: Une simple fusion itérative et in-place est la réponse « propre et maigre » qui impressionne les intervieweurs.

---

### Une mise en œuvre propre et idiomatique (Java comme référence)

Ci-dessous se trouve la solution Java que nous allons parcourir pas à pas. Il utilise un noeud factice, fusionne en un seul passage, et n'attribue jamais des nœuds inutiles.

"Java
PolyNode public addPoly(PolyNode poly1, PolyNode poly2) {
mannequin PolyNode = nouveau PolyNode(0, 0);
PolyNode queue = mannequin;

alors que (poly1 != null && poly2 != null) {
Si (poly1.puissance > poly2.puissance) {
tail.next = poly1; // Puissance plus grande – garder le nœud original
poly1 = poly1.next;
} sinon si (poly1.power < poly2.power) {
tail.next = poly2;
poly2 = poly2.suivant;
} autre {
int newCoeff = poly1.coefficient + poly2.coefficient;
si (nouveau Coeff != 0) {/ Ne joindre que si le résultat est non-zéro
tail.next = nouveau PolyNode(nouveauCoeff, poly1.power);
}
poly1 = poly1.next;
poly2 = poly2.suivant;
}
tail = tail.next; // avance si un noeud est fixé
}

tail.next = (poly1 != null) ? poly1 : poly2; //
retour mannequin.suivant;
}
«» "

*Pourquoi l'interview est prête: *

1. ** Logique claire** – la chaîne `if/else` reflète le raisonnement mathématique : - puissance plus grande → garder ce terme ; puissance égale → coefficients de somme.
2. **Manipulation à terme** – le "si (nouveau Coeff != 0) ' garde assure le respect de la règle -No zéro.
3. **O(1) espace auxiliaire** – nous allouons seulement quand un nouveau nœud fusionné est nécessaire; toutes les autres opérations réutilisent des nœuds existants.
4. **Scan linéaire** – chaque noeud est traité une fois; aucune boucle ni aucun tri en hauteur.

---

### Python & C++ Variantes

- **Python**: Utilisez une boucle poly1 et poly2; le noeud factice est un seul objet `PolyNode(0,0).
- **C++**: Préférez un `PolyNode factice(0,0)` sur la pile et retournez `dummy.next`.
- **Java**: La même logique s'applique, juste avec des références de frappe et de pointeur explicites.

---

### Conseils de présentation de l'entrevue

1. **Énoncez vos hypothèses** – Les deux listes sont triées en descendant par puissance et ne contiennent aucun coefficient zéro. (en milliers de dollars)
2. **Expliquez l'échange temps/espace** – Nous allons fusionner dans le temps linéaire, réutiliser des nœuds de sorte que nous restons dans 'O(1)' Plus d'espace. (en milliers de dollars)
3. **Montrer la manipulation des caisses de bord** – Si les coefficients s'annulent, nous sautons simplement le nœud; si une liste s'épuise, nous ajoutons le reste. (en milliers de dollars)
4. **Ecrire le code propre** – Conserver la logique dans une seule méthode; éviter les fonctions d'aide imbriquées sauf si nécessaire.
5. **Venez dans un cas d'essai** – Simulez `poly1 = [[2,3],[1,1]` et `poly2 = [[2,3],[4,0]`; montrez comment les décisions du pointeur mènent à la liste finale.

---

### Réflexions finales – Ce que veulent les intervieweurs

Les intervieweurs cherchent :

Produit désiré Ce qu'il reflète
- Oui.
**Temps linéaire**=Utilisation efficace des structures de données. Autres
**L'espace continu** Autres
**Manipulation de lisière de bust**= Attention aux détails et à la programmation défensive. Autres
**Claire, code commenté**= Capacité de communiquer une logique complexe à un coéquipier ou à un gestionnaire. Autres

Mastering *Ajouter deux polynômes représentés comme des listes liées* vous donne un point de conversation polyvalent. Il met en valeur votre compréhension des listes liées, le tri des invariants et l'optimisation algorithmique – tout en vous laissant fléchir un peu de maths.

Ainsi, la prochaine fois que vous verrez cela sur LeetCode, sur un défi de codage d'entreprise, ou dans un PDF recruteur, entrez en confiance, gardez votre code propre, et rappelez-vous: les meilleures réponses sont celles qui **merger, somme, et skip**, tout en un seul passe rangé.

---

À emporter

- **Mise en oeuvre** la tête factice, en place fusionnent dans votre langue préférée.
- ** Expliquer** la linéarité de l'algorithme et l'espace constant.
- **Faits saillants** manipulation de cas de bord (puissances égales, zéro somme, listes vides).

En maîtrisant ce problème, vous aurez non seulement la portion de codage de votre entrevue, mais aussi le style de codage clair et efficace que les entreprises de haute technologie valorisent. Bon codage, et que vos entretiens de travail se terminent sur une note élevée! C'est ce qu'il a dit.

---

* Sentez-vous libre de commenter avec votre propre mise en œuvre linguistique ou partagez où vous avez rencontré ce problème dans une interview réelle. *