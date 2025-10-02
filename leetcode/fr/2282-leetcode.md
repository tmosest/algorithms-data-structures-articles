---
titre: LeetCode 2282. Nombre de personnes qui peuvent être vus dans une grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. Nombre de personnes qui peuvent être vus dans une grille
Résumé du problème
On vous donne une matrice `m x n` ` hauteurs` où chaque entrée est un entier positif.
Une personne à `(ligne 1, col1)` peut voir une autre personne à `(row2, col2)` **seulement** si

* `(row1 == range2 && col1 < col2)` **ou** `(ligne 1 < range2 && col1 == col2)`
* Chaque personne strictement entre eux est plus courte que les deux**.

Retourner une matrice `réponse` où `réponse[i][j]` est le nombre de personnes que la personne à `(i, j)` peut voir.

> **Constraints**
> - `1 ≤ hauteurs, hauteurs, longueur ≤ 400`
> - 1 ≤ hauteurs [i] [j] ≤ 105 "

---

Pourquoi ce problème se pose pour une entrevue technique
* ** Importance du monde réel** – Pensez aux caméras de surveillance ou aux problèmes de visibilité dans le jeu.
* **Plusieurs structures de données** – Combine des tableaux, des boucles et une pile **monotonique**.
* ** Points de repère** – Affiche que vous pouvez gérer les cas de bord (tailles égales) et écrire le code O(mn) propre.
* **High LeetCode – Évaluation de l'entrevue** – De nombreux recruteurs posent spécifiquement cette question.

---

L'Insight: Une pile monotonique pour les deux directions

Pour chaque rangée (de droite à gauche) et chaque colonne (de bas à haut), nous maintenons une pile **de moins en moins grande** de hauteurs.
Lorsque nous rencontrons une nouvelle hauteur `h`:

1. Alors que le haut de la pile `t` est **plus court** que `h`, la personne actuelle peut voir `t` → incrémenter le nombre et pop `t`.
2. Si la pile est **pas vide** après le saut, la personne actuelle peut également voir la ** première personne plus grande** sur la pile → incrémenter à nouveau.
3. Poussez `h` sur la pile seulement si elle est **pas égale** au haut du courant (pour éviter le double comptage des hauteurs égales).

Faire cela une fois pour toutes les lignes (de droite à gauche) et une fois pour toutes les colonnes (de bas en haut) donne la réponse finale dans le temps `O(mn)`.

---

Mise en œuvre du code

####===# Java (Stack monotonique, O(mn))

"Java
Importation de java.util.*;

solution de classe publique {
[] voirPeople(int[][] hauteurs) {
m = hauteurs. longueur;
int n = hauteurs[0].longueur;
int[]] ans = nouveau int[m][n];

// ---- Analyser chaque colonne (en bas → en haut) ----
pour (int col = 0; col < n; col++) {
Deque<Integer> pile = nouvelle ArrayDeque<>();
pour (int rang = m - 1; rang >= 0; ligne--) {
int h = hauteurs[ligne][col];
pendant que (!stack.isEmpty() && h > stack.peek()) {
ans[row][col]++; // voir une personne plus courte
pile.pop();
}
si (!stack.isEmpty()) {
ans[row][col]++; // voir le premier plus grand
}
si (stack.isEmpty()= empil.peek()) {
pile.push(h); // pousser seulement si la hauteur est nouvelle
}
}
}

// ---- Analyser chaque ligne (à droite → à gauche) ----
pour (int rang = 0; rang < m; rang++) {
Deque<Integer> pile = nouvelle ArrayDeque<>();
pour (int col = n - 1; col >= 0; col-) {
int h = hauteurs[ligne][col];
pendant que (!stack.isEmpty() && h > stack.peek()) {
ans[row][col]++; // voir une personne plus courte
pile.pop();
}
si (!stack.isEmpty()) {
ans[row][col]++; // voir le premier plus grand
}
si (stack.isEmpty()= empil.peek()) {
le point h) est remplacé par le texte suivant:
}
}
}

le retour des an;
}
}
«» "

> **Points clés**
> * Deux passes indépendantes : **rows** (de droite à gauche) et **colonnes** (de bas à haut).
> * `ArrayDeque` utilisé comme pile pour O(1) push/pop.
> * Évitez de pousser des hauteurs égales pour maintenir la pile en baisse stricte.

---

Python (Manotonic Stack, O(mn))

'`python
de taper l'importation Liste

Solution de classe:
def seePeople(self, heights: List[List[int]]) -> Liste[Liste[int]]:
m, n = len(hauteurs), len(hauteurs[0])
ans = [[0] * n pour _ dans l ' intervalle(m)]

# Scannez chaque colonne en bas -> haut
pour le col dans la plage(n):
pile = []
pour la ligne de range(m - 1, -1, -1):
h = hauteurs[ligne][col]
pendant la pile et h > pile[-1]:
[ligne] [col] += 1
Pile.pop()
si pile:
[ligne] [col] += 1
si pas empiler ou h != pile[-1]:
pile.annexe(h)

# Scanner chaque ligne droite -> gauche
pour la ligne de range(m):
pile = []
pour le col dans la plage (n - 1, -1, -1):
h = hauteurs[ligne][col]
pendant la pile et h > pile[-1]:
[ligne] [col] += 1
Pile.pop()
si pile:
[ligne] [col] += 1
si pas empiler ou h != pile[-1]:
pile.annexe(h)

retour et
«» "

> **Pourquoi ce code Python est propre**
> * Les listes (`stack`) agissent comme une pile avec `append` / `pop`.
> * Deux for‐loops maintiennent la logique symétrique et facile à lire.

---

####3-C++ (Manotonic Stack, O(mn))

'`cpp
#incluez <vecteur>
#incluez <stack>

solution de classe {
public:
std::vector<std::vector<int>> voirPersonnes(std::vector<std::vector<int>&hauteurs) {
int m = hauteurs.dimension();
int n = hauteurs[0].taille();
m:vector<std::vector<int>> ans(m, m:vector<int>(n, 0));

// Column pass: bas -> haut
pour (int col = 0; col < n; ++col) {
std:stack<int> st;
pour (int rang = m - 1; rang >= 0; --row) {
int h = hauteurs[ligne][col];
pendant que (!st.vide() && h > st.top()) {
++ans[ligne][col];
la stépop();
}
si (!st.vide()) ++ans[row][col];
si (st.vide()= st.top()) st.poush(h);
}
}

// Passage en ligne : à droite -> gauche
pour (int rang = 0; rang < m; ++row) {
std:stack<int> st;
pour (int col = n - 1; col >= 0; --col) {
int h = hauteurs[ligne][col];
pendant que (!st.vide() && h > st.top()) {
++ans[ligne][col];
la stépop();
}
si (!st.vide()) ++ans[row][col];
si (st.vide()= st.top()) st.poush(h);
}
}
le retour des an;
}
};
«» "

> ** Faits saillants**
> * `std::stack<int>` donne des opérations O(1).
> * La même logique que les solutions Java/Python, mais avec des idiomes C++.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Carte de la colonne "O(mn)" "O(m)"
Carte de la ligne
**Total******"O(mn)"****"O(m + n)"** (matrice de sortie)

Avec `m, n ≤ 400`, l'algorithme fonctionne confortablement en < 1 ms sur les machines modernes.

---

Liste de contrôle des cas de bord

Pourquoi ça compte Comment le code le gère
C'est ce qu'on dit.
**Égales hauteurs**=Ils bloquent la vision l'un pour l'autre. On ne pousse jamais une hauteur qui égale le haut de la pile actuelle. Autres
Une seule direction existe. Les boucles tournent toujours, mais les autres passes de direction sont insignifiantes. Autres
**Toutes les hauteurs sont égales** Le sac reste vide après chaque poussée; chaque personne voit exactement 1 personne (le cas échéant). Autres
**Augmenter strictement les hauteurs**=Chaque personne peut voir tout le monde devant. Autres Alors que la boucle pops tous les gens plus courts, puis compte le plus grand. Autres

---

Article de blog optimisé par le SEO

Titre
Code de Leet 2282 – Nombre de personnes que l'on peut voir dans une grille – Java, Python, C++ Solution monotonique + Conseils d'entrevue**

Description de la méta
> Résolvez le LeetCode 2282 en **O(mn)** avec une pile monotonique.
> Implantations Java, Python et C++ complètes + aperçus d'entretien.
> Découvrez pourquoi ce problème est un incontournable pour les entrevues sur la structure des données.

---

Article du blog

Introduction

Si vous visez un rôle d'ingénierie de logiciel, le **Nombre de personnes qui peuvent être vus dans un problème de Grid** est une base d'entrevue classique.
Il teste :

* Compréhension de la traversée du réseau 2-D.
* Capacité de concevoir une pile monotonique.
* Style de codage propre entre les langues.

Ci-dessous, nous traversons le problème, l'astuce **monotonic-stack**, fournissons **full code en Java, Python, et C++**, et partagez des idées conviviales d'interview.

---

Récapitulation des problèmes

- **Input**: "m x n" matrice "hauteurs".
- **Règle de visibilité**: Une personne à `(i, j)` ne peut voir que les personnes à droite ** ou** ci-dessous, à condition que chaque personne intermédiaire soit strictement plus courte.
Pour chaque cellule, compter les personnes visibles.

---

C'est vrai. L'idée de base : deux passes avec une pile monotonique

1. **Scan de colonne (Bottom → Top)* *
* Traitez chaque colonne comme un tableau 1-D.
* Maintenez une pile de **baisse** de hauteurs.
* Lorsque la hauteur actuelle `h` est plus élevée que le sommet de la pile, nous pouvons voir que la personne → incrément compte & pop.
* Après avoir sauté, si la pile n'est pas vide, la personne actuelle peut également voir la première personne plus grande → un autre accroissement.
* Poussez `h` sur la pile seulement si elle est *différente* du haut du courant pour éviter le double comptage des hauteurs égales.

2. **Scan de la courbe (à droite → à gauche)**
* Répétez la même logique sur chaque ligne.
* Les deux scans sont indépendants – la matrice de sortie est mise à jour cumulativement.

La combinaison nous permet de compter en temps linéaire toutes les personnes bien visibles et moins visibles.

---

####4-Specific Implementations

*Nous avons déjà inclus les extraits de Java, Python et C++ dans la section "Applications de code". *
N'hésitez pas à les déposer dans votre IDE local et à courir avec les exemples de cas.

---

C'est vrai. Pourquoi cette solution fait-elle penser aux entrevues?

* **Efficacité du temps** – O(mn) est optimal; les intervieweurs aiment le raisonnement asymptotique clair.
* **Efficacité de l'espace** – Seulement une pile par rangée/colonne – démontre la conscience de la mémoire.
* ** Agnosticisme linguistique** – Montre que vous pouvez traduire la même logique à n'importe quelle langue, une compétence très précieuse pour diverses piles de technologie.

---

#### 6-

Conseil Explication
C'est pas vrai.
**Expliquez l'invariant de la pile** Autres
**Discuss égal hauteurs**===Les hauteurs égales se bloquent l'une l'autre; ce qui explique pourquoi nous sautons pousser les duplicatas.=== Autres
**Visualisez avec un diagramme**= Dessinez une petite grille et marchez à la main l'algorithme; c'est un excellent moyen de convaincre l'intervieweur de votre compréhension. Autres
**Cas du bord de la mention**= Afficher la sensibilisation aux scénarios de ligne/colonne et de hauteur uniforme. Autres
Autres **Parler de la complexité**=État `O(mn)` temps et `O(m + n)` espace explicitement – les intervieweurs apprécient une analyse rapide et précise. Autres

---

- Oui. Prise- Loin

- **Les piles monotoniques** sont le pain et le beurre pour la visibilité 1-D/prochaine-plus grande-éléments.
- **Deux passes** (colonnes en premier, rangées en second) assurent une couverture complète en 2-D.
- Gardez la pile **de manière à réduire considérablement** et sautez des hauteurs égales – c'est la subtilité qui rend l'algorithme correct.

La maîtrise de ce problème signifie que vous êtes bien préparé pour un large éventail de questions sur les questions posées lors des entrevues de la première journée.

---

- Oui. Réflexions finales

Qu'il s'agisse de Java backend dev, de Python data-scientifique ou de C++, LeetCode 2282 vous offre une victoire rapide pour impressionner les recruteurs.
Implémenter le code, tester avec des matrices aléatoires, et la pratique expliquant la logique à haute voix – l'entrevue vous remerciera.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

Appel à l'action

*Déposer un commentaire ci-dessous si vous souhaitez une plongée plus profonde dans d'autres problèmes de visibilité LeetCode! *

---

**Auteur**: [Votre nom] – Passionné de la structure des données et embauche‐chef technologique.
**Tags**: #LeetCode, #DataStructures, #MonotonicStack, #Java, #Python, #CPlusPlus, #InterviewPrep, #LogicielEngineering

---

Et c'est ça !

Avec ces implémentations et explications prêtes à l'entrevue, vous êtes tous configurés pour ace LeetCode 2282 et démontrez vos compétences de pile à tout gestionnaire d'embauche. Bon codage !