---
titre: LeetCode 1776.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1776. Car Fleet II – Maîtrisez le problème de code de leet dur (Java-Python C++)

> ** Prêt à atterrir cet entretien technique? * *
> Ce post vous permet de parcourir la solution la plus efficace pour LeetCode 1776 en utilisant une pile monotonique. Nous allons vous montrer le code propre en **Java, Python et C++**, expliquer pourquoi il est O(n), et mettre en évidence le *bon, le mauvais, et le laid* de ce défi algorithmique classique.

---

Récapitulation des problèmes

> ** Voitures sur une route unidirectionnelle* *
> Il y a des voitures `n` qui voyagent dans la même direction.
> Chaque voiture `i` commence à `position[i]` avec "vitesse[i]".
> Les positions augmentent strictement (`position[i] < position[i+1]`).
> Lorsqu'une voiture plus rapide prend une voiture plus lente, ils fusionnent dans un seul --fleet, qui voyage à la vitesse de la voiture plus lente.
>
> **Retour** un tableau `réponse` où `réponse[i]` est le temps (en secondes) où la voiture `i` se heurte d'abord à la voiture suivante, ou `-1` s'il ne se heurte jamais.

> **Constraints**
> - `1 ≤ n ≤ 105`
> - `1 ≤ position[i], vitesse[i] ≤ 106 "

> **Typical Test Case* *
> ```texte
> Entrée : voitures = [[1,2],[2,1],[4,3],[7,2]]
> Produit: [1.0000,-1.00000, 3.0000,-1.00000]
> `` "

---

L'idée de base – Stack monotonique

L'observation clé :

1. **Seules les voitures plus rapides peuvent rattraper les voitures plus lentes. **
2. Lorsqu'une voiture rattrape, elle hérite de la vitesse de la voiture plus lente (celui qu'elle rencontre).
3. Par conséquent, de la voiture la plus droite à la gauche, nous maintenons une pile **monotonique** de candidats que la voiture actuelle peut potentiellement rencontrer.
*La pile stocke des indices de voitures qui sont strictement plus lents que la voiture en dessous dans la pile. *

Pour chaque voiture (traversant de droite à gauche):

- Des voitures de la pile qui :
- Sont plus rapides que la voiture actuelle (pas de collision), **ou**
- serait en collision ** après** la voiture sautée a déjà en collision avec quelqu'un d'autre (d'où leurs changements effectifs de vitesse).

- Oui. La première voiture qui reste sur la pile et qui satisfait à l'état de collision est celle que la voiture actuelle rencontrera en premier.
- Oui. Si aucune voiture de ce type ne reste, la réponse est `-1`.

Cet algorithme fonctionne dans **O(n)** temps parce que chaque voiture est poussée et sautée au plus une fois.

---

## Code Snippets

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**. Chacun suit la même logique monotonique.

---

- Oui. 1. Java (Clean, O(n) Stack monotonique)

"Java
Importation de java.util.*;

solution de classe publique {
public double[] getCollisionTimes(int[][] voitures) {
int n = voitures. longueur;
double[] ans = nouveau double[n];
les tableaux.fill(ans, -1.0);

Deque<Integer> pile = nouvelle ArrayDeque<>();

pour (int i = n - 1; i >= 0; i--) {
int posI = voitures[i][0], spdI = voitures[i][1];

pendant que (!stack.isEmpty()) {
int j = pile.peekLast();
int posJ = voitures[j][0], spdJ = voitures[j][1];

// Si la voiture actuelle est plus lente ou égale, elle n'attrapera jamais j
en cas de rupture (spdI <= spdJ);

t double = (double) (posJ - posI) / (spdI - spdJ);

// Si j ne heurte jamais, ou une collision se produit avant la collision de j
si (ans[j]] == -1.0== t <= ans[j]) {
[i] = t;
pause;
} autre {
// j changera de vitesse avant que j'attrape → jeter j
pile.pollLast();
}
}
pile.offreLast(i);
}
le retour des an;
}
}
«» "

---

- Oui. 2. Python (3,9+)

'`python
de taper l'importation Liste

Solution de classe:
def getCollision Temps(même, voitures: Liste[Liste[int]]) -> Liste [float]:
n = len(cars)
ans = [-1,0] * n
pile : Liste[int] = [] Nombre d'indices des voitures candidates

pour i dans la fourchette(n - 1, -1, -1):
pos_i, spd_i = voitures[i]
pendant la pile:
j = pile[-1]
pos_j, spd_j = voitures[j]

si spd_i <= spd_j: # ne peut pas rattraper
pause

t = (pos_j - pos_i) / (spd_i - spd_j)

-1.0 ou t <= ans[j]:
[i] = t
pause
Sinon:
pile.pop() # j change de vitesse avant que je l'attrape

pile.annexe(i)
retour et
«» "

---

- Oui. 3. C++ (GNU++17)

'`cpp
solution de classe {
public:
vector<double> getCollisionTimes(vecteur<vecteur<int>>& voitures) {
int n = voitures.taille();
vecteur <double> ans(n, -1.0);
vectorielle<int> st; // pile d'indices

pour (int i = n - 1; i >= 0; --i) {
int pos_i = voitures[i][0], spd_i = voitures[i][1];
pendant que (!st.vide()) {
int j = st.back();
int pos_j = voitures[j][0], spd_j = voitures[j][1];

si (spd_i <= spd_j) pause; // ne peut pas attraper

double t = double(pos_j - pos_i) / (spd_i - spd_j);

si (ans[j] < 0= t <= ans[j]) {
[i] = t;
pause;
} autre {
st.pop_back(); // j changera la vitesse d'abord
}
}
st.push_back(i);
}
le retour des an;
}
};
«» "

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
La boucle principale (traversant des voitures `n`)
Chaque voiture a poussé/poussés une fois

*Global:* **Time O(n), Space O(n)** – optimal pour `n ≤ 105`.

---

Bonne, mauvaise et moche

Aspect du bien
- C'est quoi ?
**Concept**. Empil monotonique élégant; temps linéaire.
**Mise en oeuvre**= Compact; facile à déboguer== Doit maintenir des conditions correctes `temps`= Erreurs hors-par-un, division par zéro si les vitesses sont égales==
La logique de la pile peut confondre les débutants.
Autres **Cases d'Edge**= Gestion de tous les cas `-1`= Besoin de vérifier `spd_i <= spd_j` pour éviter la division par zéro= L'oubli de comparer avec `ans[j]` conduit à de mauvais résultats==

> **Conseil:** Toujours marcher à travers la pile avec un petit exemple. Visualiser les états de la pile aide à prévenir les bogues.

---

Conseils pour l'entrevue

1. **Décrivez l'observation en premier.** Expliquez qu'une voiture plus rapide ne peut attraper qu'une voiture plus lente et qu'après la capture, la flotte se déplace à la vitesse plus lente.
2. **Décrire la pile monotonique.** Soulignez que la pile tient des collisions potentielles et pourquoi nous traversons de droite à gauche.
3. **Va à travers un cas d'essai.** Montrez comment la pile évolue étape par étape.
4. ** Discussion sur la complexité.** Mettre en évidence le temps `O(n)` et l'espace `O(n)`, et pourquoi aucune boucle imbriquée `O(n2)` n'est nécessaire.
5. **Manipulation de l ' eau.** Mentionnez la vérification `spd_i <= spd_j` et la comparaison avec `ans[j]`.

---

Données de métadonnées optimisées

html
<title>LeetCode 1776 Car Fleet II – Java, Python & C++ Solutions
<meta name="description" content="Master the LeetCode difficile Car Fleet II. Obtenez des solutions Java, Python et C++ propres avec une approche de pile monotonique. Apprenez l'algorithme, la complexité et les conseils d'entrevue.
LeetCode 1776, Flotte de voiture II, solution Java, solution Python, solution C++, pile monotonique, interview d'algorithme, interview de codage, problème de flotte de voiture">
«» "

---

Conclusion

Car Fleet II est un exemple de manuel de ** utilisant une pile monotonique pour transformer un problème apparemment quadratique en un problème linéaire**. L'astuce consiste à se rendre compte qu'après une collision, la vitesse se bloque à la voiture plus lente, et que toute voiture plus rapide derrière doit d'abord nettoyer toutes les voitures plus rapides avant d'envisager des collisions.

Avec les extraits de code ci-dessus et les idées dans ce post, vous êtes prêt à:

- **Solvez le problème efficacement** dans la langue choisie.
- ** Expliquez l'algorithme** de façon convaincante à un intervieweur.
- **Afficher votre propre codage** en utilisant des implémentations claires et sans bug.

Bonne chance, et que les flottes soient toujours en votre faveur! C'est ce qu'il a dit