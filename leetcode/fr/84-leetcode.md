---
titre: LeetCode 84. Le plus grand rectangle en histogramme
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Solutions de code

Ci-dessous vous trouverez trois implémentations prêtes à la production qui résolvent **LeetCode 84 – Le plus grand rectangle en histogramme**.
Tous les trois utilisent la technique classique *monotonic stack*, donnant **O(n)** temps et **O(n)** espace auxiliaire.

> **Problème** – Avec un tableau de hauteurs de barre (largeur = 1), retourner la zone du plus grand rectangle qui peut être formé à l'intérieur de l'histogramme.

La langue Signature de la fonction
- C'est quoi ?
**Java**"l'intérieur public le plus grandRectangleArea(int[] heights)" Heure: `O(n)`<br>Espace: `O(n)` Autres
**Python**"def wigth_rectangle_area(heights: List[int]) -> int`= Heure: `O(n)`<br>Espace: `O(n)` Autres
**C++**= <int la plus grande zone d'angle(vecteur<int>& hauteurs)=> Heure: `O(n)`<br>Espace: `O(n)` Autres

---

#### 1.1 Java

"Java
Importer java.util. - ArrayDeque;
Importer java.util. Deque;

solution de classe publique {
***
* Retourne la zone du plus grand rectangle d'un histogramme.
*
* @param hauteurs tableau de hauteurs de barres
* @return zone rectangle maximale
*/
public int plus grandRectangleArea(int[] hauteurs) {
// Utiliser une sentinelle -1 pour simplifier le calcul de la largeur
Deque<Integer> pile = nouvelle ArrayDeque<>();
Le paragraphe 2 est remplacé par le texte suivant:
dans maxArea = 0;

pour (int i = 0; i < hauteurs.longueur; i++) {
// Pop jusqu'à ce que le sommet de la pile soit inférieur à la hauteur du courant
pendant que (stack.peek() != -1 && hauteurs[i] <= hauteurs[stack.peek()]) {
int h = hauteurs[stack.pop()];
int w = i - empil.peek() - 1;
maxArea = Math.max(maxArea, h * w);
}
Le point i) est remplacé par le texte suivant:
}

// Effacer la pile et traiter les barres restantes
pendant que (stack.peek() != -1) {
int h = hauteurs[stack.pop()];
int w = hauteurs.longueur - empil.peek() - 1;
maxArea = Math.max(maxArea, h * w);
}

retour maxArea;
}
}
«» "

---

#### 1.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def bigest_rectangle_area(self, heights: List[int]) -> Int:
"""
Calculez la plus grande zone rectangle d'un histogramme.
: Hauteurs des barres : List[int] – hauteurs des barres
:retour: int – surface maximale
"""
pile = [-1] # sentinelle
max_area = 0

pour i, h dans l'énumération(hauteur):
pendant la pile[-1] != -1 et h <= hauteurs[stack[-1]]:
hauteur = hauteurs[stack.pop()]
largeur = i - pile[-1] - 1
max_area = max(max_area, hauteur * largeur)
pile.annexe(i)

# Traiter les barres restantes
pendant la pile[-1] != - 1 :
hauteur = hauteurs[stack.pop()]
largeur = len(hauteurs) - cheminée[-1] - 1
max_area = max(max_area, hauteur * largeur)

_zone maximale de retour
«» "

---

*## 1.3 C++

'`cpp
#incluez <vecteur>
#incluez <stack>
#incluez <algorithme>

solution de classe {
public:
Int le plus grandRectangleZone(s):vecteur<int>& hauteurs) {
std::stack<int> st; // indices
st.push(-1); // sentinelle
dans maxArea = 0;

pour (int i = 0; i < hauteurs.size(); ++i) {
alors que (st.top() != -1 && hauteurs[i] <= hauteurs[st.top()]) {
int h = hauteurs[st.top()];
la stépop();
m = m - haut() - 1;
maxZone = md::max(maxZone, h * w);
}
le point i) est remplacé par le texte suivant:
}

// Barres restantes
alors que (st.top() != -1) {
int h = hauteurs[st.top()];
la stépop();
int w = hauteurs.size() - st.top() - 1;
maxZone = md::max(maxZone, h * w);
}

retour maxArea;
}
};
«» "

---

- Oui. 2. Billet de blog: Le plus grand rectangle dans l'histogramme – Le bon, le mauvais et le mauvais

> **Meta‐Description**: Master LeetCode 84 en secondes. Apprenez l'algorithme basé sur la pile, les pièges, les cas de bord et le code d'entrevue en Java, Python et C++. Boostez vos compétences en structure de données et décrochez votre prochain emploi!

---

#### 2.1 H1 – Le plus grand rectangle de l'histogramme : maîtriser un problème difficile classique

> Chaque curriculum vitæ de l'ingénieur principal mentionne **Stacks à moteur**. Cet article vous fait découvrir le *bon*, *mauvais* et *meilleur* problème du plus grand rectangle, plus propre, le code d'interview en Java, Python et C++.

---

#### 2.2 H2 – Récapitulation des problèmes et contraintes

- **Input**: «hauteurs[0...n‐1]» – hauteurs de barre, largeur = 1
- ** Sortie** : zone du plus grand rectangle
- **Constraints**:
- `1 <= n <= 105`
- `0 <= hauteurs[i] <= 104`

Ces limites excluent les solutions quadratiques; vous avez besoin de **O(n)** temps.

---

#### 2.3 H2 – Le Bon: Pourquoi un Stack Monotonique?

1. **Temps linéaire** – Chaque barre est poussée/poupée au plus une fois.
2. ** Géométrie élégante** – Lorsque vous scannez de gauche à droite, la pile conserve les indices de barres dans un ordre *d'augmentation stricte* de hauteur.
3. **Computation de largeur simple** – Lorsque vous faites apparaître une barre `h`, l'index suivant sur la pile (`stack.top()`) indique la limite gauche; l'index courant `i` est la limite droite.
4. ** Preuve claire d'exactitude** – L'invariant de la pile garantit que chaque rectangle possible est considéré exactement une fois.

---

2.4 H2 – Les mauvaises: les pièges communs

Pourquoi ça arrive ?
- Oui.
**Défaut-par-Une erreurs**=Largeur décomptable (`i - stack.peek() - 1` vs `i - empil.peek()`)= Utiliser une sentinelle `-1` pour éviter les largeurs négatives=
**Vérification de la pile d'imperméabilisation** Autres
**Grande entrée**=En utilisant des boucles O(n2) naïve ou récursion
**Offlissement**

---

#### 2.5 H2 – L'Ugly: Cas de bord et performance Pièges

Description de la stratégie
C'est quoi ?
**Tous les zéros**= Hauteur = 0 → surface = 0== L'embout va tout sauter immédiatement; max séjours 0
**L'augmentation de la taille de la pile n'est pas terminée parce qu'il n'y a pas de pop jusqu'à la fin
**Monotoniquement en baisse**
** Grandes hauteurs égales** Obtenir des barres égales Consécutifs L'état `<=` vous assure de sauter *tous* hauteurs égales pour éviter les rectangles manqués.
**Limites de mémoire**

---

#### 2.6 H2 – L'algorithme (étape par étape)

1. **Initialiser** une pile avec sentinelle `-1`.
2. **Itérer** pour chaque indice "i" :
- Tandis que la hauteur du courant `h` ≤ hauteur au sommet de la pile:
- Indice pop 'idx'.
Hauteur = "hauteurs[idx]".
- Largeur = `i - pile.top() - 1'.
- Mettre à jour "maxArea".
- Poussez `i` sur la pile.
3. **Nettoyez** les indices restants après la boucle ( logique pop similaire avec `n` comme limite droite).
4. **Retour** "maxArea".

---

#### 2.7 H2 – Extraits de code (toutes langues)

> *Java*
> ``java
> public int plus grandRectangleArea(int[] heights) { ... }
> `` "

> *Python*
> ``python
> def le plus grand_rectangle_area(self, heights: List[int]) -> int: ...
> `` "

> *C++*
> ``cpp
> la plus grande zone de tectangle(vecteur <int>& hauteurs) { ... }
> `` "

*(Code complet ci-dessus – voir section 1.)*

---

2.8 H2 – Complexité temporelle et spatiale

- **Heure**: `O(n)` – chaque indice est poussé/poché une fois.
- **Espace**: `O(n)` - la pile peut grandir à `n` dans le pire des cas.
- **Les facteurs constants** sont petits : quelques opérations entières par itération.

---

####2.9 H2 – Conseils d'entrevue

1. ** Expliquer l'invariant de la pile**: La pile contient des indices de hauteurs croissantes, ce qui garantit que nous connaissons la limite gauche pour toute barre soufflée. (en milliers de dollars)
2. **Parcourir un petit exemple**: `[2,1,5,6,2,3]` – montrer les poussées/pops et les calculs de zone.
3. **Cas de bord de Mention** vous avez testé – tous les zéros, augmentant, diminuant.
4. **Demander des éclaircissements**: p.ex. – montre aux intervieweurs que vous vous souciez des contraintes.
5. ** Optimisations de la largeur**: évitez les boucles supplémentaires; utilisez sentinelle pour simplifier le calcul de la largeur.

---

2.10 H2 – A emporter

- **Les piles monotoniques** sont un outil puissant pour les problèmes d'histogramme 1-D.
- Éviter les bugs courants hors-par-un avec une sentinelle.
- Même dans un problème de type "Hard", une pile à un seul passage donne la solution optimale.
- Oui. Le même modèle s'applique aux autres défis LeetCode : *Le plus grand rectangle dans une grille*, *Le plus grand rectangle de 1s*, etc.

---

### 2.11 H2 – Appel à l'action

> ** Prêt à accepter votre prochain entretien? * *
> - Pratiquez cette solution sur LeetCode, HackerRank et vos propres projets.
> - Partagez vos solutions sur GitHub avec le tag `#millar-rectangle-histogramme`.
> - Abonnez-vous pour plus d'entrevues et d'explications vidéo.

> * Le code, l'interview et la terre qui rêvent ensemble ! * *

---

### 2.12 H2 – Références et lectures supplémentaires

1. LeetCode: [Le plus grand rectangle dans l'histogramme](https://leetcode.com/problèmes/le plus grand-rectangle-in-histogram/)
2. YouTube: [Explication vidéo – Niits38862Jun 27, 2024](https://www.youtube.com/watch?v=...)
3. Billet de blog : *Manotonic Stack – A Deep Dive* (https://example.com/monotonic-stack)
4. GitHub Repo: `https://github.com/yourhandle/leetcode-84` – Implantations et tests complets

---

> **SEO Mots-clés**: Le plus grand rectangle dans l'histogramme, LeetCode 84 solution, L'algorithme de la pile de la monotonie, L'O(n) histogramme rectangle, L'interview de Java Python C++, La structure de données interview prep, L'entrevue de codage d'emploi, Comment résoudre les problèmes difficiles

---

Bon codage ! C'est ce qu'il a dit