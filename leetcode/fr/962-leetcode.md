---
titre: LeetCode 962. Ramp de largeur maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La façon la plus rapide de résoudre le LeetCode 962 – Ramp de largeur maximale
- Oui. C++ – 3 Solutions complètes + Blog optimisé SEO

---

Résumé du problème

**LeetCode 962 – Rampe de largeur maximale* *
Compte tenu d'un tableau entier `nums`, trouvez la largeur maximale `j - i` telle que `i < j` et `nums[i] <= nums[j]`. Si aucune rampe n'existe, retourner `0`.

**Contrôles* *

- Oui.
-- -- -- -- -- --
"nums.longueur" "2 ≤ n ≤ 5 × 104" Autres
Nombres < 0 ≤ nums[i] ≤ 5 × 104 '

---

Pourquoi ce problème est-il un incontournable pour les entrevues

* **Chiffre classique de la pile monotonique** – apparaît fréquemment lors d'entrevues de codage (p. ex.
* ** Solution linéaire** – temps O(n), espace O(n) ; battre la force brute O(n2) naïve est critique.
* **Manipulation du tableau des cas + connaissance de la structure des données** – un problème parfait pour les entrevues et les résumés.

---

La stratégie O(n) – Stack monotonique + balayage à deux points

1. **Construire une pile décroissante* *
* Traverse "nums" de gauche à droite.
* Push index `i` sur la pile **seulement si** la pile est vide ou `nums[i]` est ** strictement plus petit** que la valeur en haut de la pile.
* Après cette passe, la pile contient des indices d'une sous-séquence strictement décroissante.

2. **Scan de droite à gauche**
* Pour chaque index `j` de `n-1` vers le bas à `0`, pop de la pile pendant `nums[stack.top()] ≤ nums[j]».
* Chaque pop donne une rampe valide `(i, j)`; calculer la largeur `j - i` et garder le maximum.
* Arrêtez quand la pile devient vide.

> **Pourquoi ça marche ? **
> La pile maintient les indices de gauche candidats `i` qui sont le plus tôt possible tout en gardant `nums[i]` Assez haut pour correspondre au futur "j".
> En scannant les bonnes garanties, nous trouvons le plus loin possible `j` pour chaque `i` dans le temps amorti O(1).

---

Analyse de complexité

Temps Espace
C'est pas vrai.
Algorithme **O(n)**
O(n2)

La pile est construite une fois et sautée au plus une fois par élément, donnant du temps linéaire.

---

Numéro de code

On trouvera ci-dessous des solutions complètes et prêtes à fonctionner pour **Java**, **Python** et **C++**.

Autres **Assurez-vous d'importer les colis requis** (`java.util.*`, `typing. Liste`, `vecteur`, `stack`).

---

Java (Java 17+)

"Java
Importer java.util. Pioche;

solution de classe publique {
***
* Retourne la rampe de largeur maximale dans le tableau.
* Utilise une pile décroissante monotonique + balayage inverse.
*/
Int public maxWidthRamp(int[] nums) {
int n = longueur nums;
Pile <integer> = nouvelle pile<>();

// Étape 1: Construire une pile décroissante d'indices
pour (int i = 0; i < n; i++) {
si (stack.isEmpty()="nums[i] < nums[stack.peek()] {
Le point i) est remplacé par le texte suivant:
}
}

int maxWidth = 0;

// Étape 2 : Scanner à partir de la droite, popping pendant la validité
pour (int j = n - 1; j >= 0; j--) {
pendant que (!stack.isEmpty() && nums[stack.peek()] <= nums[j]) {
i = pile.pop();
maxWidth = Math.max(maxWidth, j - i);
}
}

retour maxWidth;
}

// Main simple pour un test rapide
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
nombres int[] = {6,0,8,2,5};
Système.out.println(sol.maxWidthRamp(nums)); // Produit: 4
}
}
«» "

---

Python 3.10+

'`python
de taper l'importation Liste

Solution de classe:
def maxWidthRamp(self, nombres: List[int]) -> Int:
"""
Pile décroissante monotonique + balayage inverse.
:noms de type: Liste[int]
:rtype : int
"""
pile = [] # indices avec des valeurs de nombres décroissants

# Construire la pile
pour i, val dans l'énumération(nombres):
s'il n'y a pas de pile ou de valeur < nums[stack[-1]]:
pile.annexe(i)

max_largeur = 0
# Scanner de droite à gauche
pour j dans la plage (len(nums) - 1, -1, -1):
pendant la pile et les nombres[stack[-1]] <= nombres[j]:
i = pile.pop()
max_width = max(max_width, j - i)

_largeur maximale de retour

# Test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.maxWidthRamp([6,0,8,2,1,5))) # 4
«» "

---

C++17

'`cpp
#incluez <vecteur>
#incluez <stack>
#incluez <algorithme>

solution de classe {
public:
Int maxWidthRamp(std:vector<int>& nums) {
int n = nombres.size();
std:stack<int> st;

// Construire une pile décroissante d'indices
pour (int i = 0; i < n; ++i) {
si (st.vide()="nums[i] < nums[st.top()]) {
le point i) est remplacé par le texte suivant:
}
}

int maxWidth = 0;
// Scanner depuis la fin
pour (int j = n - 1; j >= 0; --j) {
pendant que (!st.vide() && nums[st.top()] <= nums[j]) {
i = haut de st.; st.pop();
maxWidth = md:max(maxWidth, j - i);
}
}
retour maxWidth;
}
};

// Principale option pour les essais
/*
#incluez <iostream>
Int main() {
Solution s;
std::vector<int> nombres = {6,0,8,2,5};
md::tout << s.maxWidthRamp(nums) << md::endl; // 4
retour 0;
}
*/
«» "

---

Le bon, le mauvais et le mauvais

Aspect du bien
- C'est quoi ?
La pile monotonique est élégante et linéaire. → erreurs hors-par-un ─ La mauvaise utilisation d'une pile *normale* (LIFO) au lieu d'une pile *monotonique* peut conduire à un comportement quadratique. Autres
**Complexité**= O(n) temps, O(n) espace== O(n2) force brute (faillite précoce fréquente)= O(n2) en raison de boucles imbriquées après une mauvaise logique de pile. Autres
**Readability**= Commentaires empilés + explications à deux passes== Trop de nombres magiques, de noms de variables manquants== Confissage des noms de variables (`st`, `i`, `j`) rendent difficile de suivre. Autres
**Edge Cases**=Poigne les valeurs dupliquées, les tableaux non décroissants== Oubliez de pop tous les éléments de la pile== Oubliez de casser lorsque la pile est vide → boucle infinie. Autres
**Conseils d'entrevue**= Expliquez d'abord l'intuition, puis la logique à deux passages== Affichez votre estimation de complexité temporelle== Évitez d'écrire un code complet avant de penser; soyez prêt à justifier chaque ligne. Autres

---

## Comment l'utiliser dans votre préparation d'entrevue

1. ** Expliquez l'intuition**: Parler de : Nous voulons l'index j le plus à droite pour chaque index de gauche possible i.
2. **Afficher l'invariant de la pile**: Les indices de la pile représentent les paramètres potentiels de gauche où "nums[i]` diminue strictement.
3. **Parcourir un exemple**: Utilisez l'exemple de LeetCode `[6,0,8,2,5]` pour afficher la construction et le popping de la pile.
4. **Débats sur les cas de bord**: Tous les nombres égaux, en augmentation stricte, des tableaux en baisse stricte.
5. **Mentions alternatives**: Recherche binaire sur une copie triée des indices, approche à deux points avec une liste triée – mais notez qu'ils sont habituellement O(n log n).

---

OBJECTIF ET Carrière – Takeaways

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
* **Méta-Description** (155 caractères):
> Découvrez la solution Java, Python et C++ la plus rapide à LeetCode 962 – Maximum Largeur Ramp. Comprendre l'astuce de la pile monotonique, l'analyse du temps/de l'espace, et les conseils d'entrevue pour aser votre entrevue de codage. (en milliers de dollars)
* ** Mots clés**:
* Ramp de largeur maximale – 962= O(n) Solution monotonique (Java, Python, C++)
* Solution de LeetCode 962 – Voie la plus rapide jusqu'à la largeur maximale
* **Structure**: Utilisez H1 pour le titre, H2 pour les sections (Problème, Approche, Complexité, Code, FAQ, etc.) pour aider les moteurs de recherche à indexer l'article proprement.

---

Les pensées finales

- **Pourquoi ça compte**: Maîtriser la technique de la pile monotonique non seulement vous pose un problème *Top‐30 LeetCode* dans une entrevue, mais montre aussi aux recruteurs que vous pouvez concevoir des solutions efficaces et propres.
- **Pratique** : Exécuter les trois extraits sur des cas d'essai aléatoires, y compris des cas de bord. Utilisez les instructions `assert` ou les tests unitaires pour valider l'exactitude.
- **Afficher la confiance**: Dans une entrevue, passez par l'algorithme avec un tableau blanc, puis traduisez-le en code. L'explication pèse souvent plus qu'une mise en œuvre parfaite.

Bonne chance ! C'est ce qu'il a dit.
*Si vous avez trouvé cela utile, partagez-le sur LinkedIn et commentez votre propre expérience d'entrevue avec des problèmes LeetCode. *