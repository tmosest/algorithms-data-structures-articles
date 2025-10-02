---
titre: LeetCode 2237. Compter les positions dans la rue avec la luminosité requise -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (Code Leet 2237)

> **Trouver les positions sur la rue avec l'éclat requis* *
> *Difficulté:* Moyenne

Vous recevez:
* un entier `n` (la rue est la ligne numéro `[0 ... n‐1]`);
* un tableau `lumières` où chaque élément `[position, portée]` représente un lampadaire qui éclaire l'intervalle inclusif
`[max(0, plage de position), min(n‐1, position+intervalle)]` ;
* un tableau `exigence` de longueur `n` où `exigence[i]` est la luminosité minimale qu'une position doit avoir.

**Objectif** – retourner le nombre de positions «i» de telle sorte que la luminosité à «i» soit au moins «exigence[i]».

-----------------------------------------------------------------------------------

- Oui. 2. Idées de base – Balayage de ligne / Répartition des différences

Pour chaque lampe, nous pouvons incrémenter le compteur à sa frontière gauche et le décrémenter *après* sa frontière droite.
Lorsque nous balayons de gauche à droite et que nous conservons une somme de préfixe en cours d'exécution, nous obtenons la luminosité exacte à chaque position.

«» "
diff[ gauche ] += 1
diff[ right+1 ] -= 1 (si right+1 < n)
«» "

Enfin, traverser `diff`, accumuler la somme du préfixe, et la comparer avec la `exigence correspondante[i]`.
Cela donne une solution temporelle **O(n + m)** (`m = lumières.longueur`) et **O(n)** mémoire supplémentaire, qui est optimale pour les limites données (`n, m ≤ 105`).

-----------------------------------------------------------------------------------

- Oui. 3. Mise en œuvre des références

#### 3.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
satisfaire à l'exigence(int n, int[] [] lumières, exigence int[]) {
// Tableau des différences
int[] diff = nouvelle int[n + 1]; // n+1 pour éviter les contrôles des limites

pour (int[] lampe : lumières) {
int pos = lampe[0];
int rng = feu[1];
int gauche = Math.max(0, pos - rng);
int droite = Math.min(n - 1, pos + rng);

diff[left]++; // début de l'éclairage
diff[droit + 1]--; // fin de l'éclairage (inclus)
}

préfixe int = 0; // luminosité du courant
réponse int = 0;

pour (int i = 0; i < n; i++) {
préfixe += diff[i];
si (préfixe >= exigence[i]) réponse++;
}
réponse de retour;
}

harnais d'essai rapide
public statique vide principal(String[] args) {
Solution s = nouvelle solution();

Int n1 = 5;
[] lumières1 = {{0,1},{2,1},{3,2}};
int[] req1 = {0,2,1,4,1};
Système.out.println(s.meetRequirement(n1, lumières1, req1)); // 4

Int n2 = 1;
les feux int[]2 = {{0,1}};
int[] req2 = {2};
Système.out.println(s.meetRequirement(n2, lights2, req2)); // 0
}
}
«» "

> **Pourquoi `int[n+1]`?**
> L'ajout d'une sentinelle à la fin (`diff[n]`) garantit que le décrément `right+1` ne touche jamais un indice hors limites, simplifiant la logique de boucle.

---

3.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def meetRequirement(self, n: int, lumières: List[List[int]],
obligatoire : Liste[int]) -> Int:
diff = [0] * (n + 1) # n+1 pour la sentinelle

pour pos, rng dans les feux:
gauche = max(0, pos - rng)
droite = min(n - 1, pos + rng)
diff[gauche] += 1
Diff[droit + 1] -= 1

luminosité = 0
réponse = 0
pour i dans la plage(n):
luminosité += diff[i]
si la luminosité >= est requise[i]:
réponse += 1

réponse de retour


Les tests rapides - Oui.
si __nom__ == "__main__" :
sol = Solution()
print(sol.meetRequirement(5, [[0,1],[2,1],[3,2]], [0,2,1,4,1]) # 4
print(sol.meetRequirement(1, [0,1]], [2]) # 0
«» "

> **Note** – Les listes dynamiques de Python sont parfaitement adaptées pour `n ≤ 105`.
> Éviter tout passe supplémentaire `O(m)` maintient la solution maigre.

---

### 3.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int meetRequirement(int n, vector<vector<int>>& lumières,
vecteur<int> et exigence) {
vector<int> diff(n + 1, 0); // n+1 sentinelle

pour (auto & lampe : lumières) {
int pos = lampe[0];
int rng = feu[1];
int gauche = max(0, pos - rng);
int droite = min(n - 1, pos + rng);

diff[left]++; // démarrage
diff[droite + 1]--; // fin + 1
}

préfixe int = 0;
Int ans = 0;
pour (int i = 0; i < n; ++i) {
préfixe += diff[i];
si (préfixe >= exigence[i]) ++ans;
}
le retour des an;
}
};

harnais d'essai
Int main() {
Solution s;
Cout << s.meetRequirement(5, {{0,1},{2,1},{3,2}}, {0,2,1,4,1}) << '\n'; // 4
Cout << s.meetRequirement(1, {{0,1}}}, {2}) << '\n'; // 0
}
«» "

> **Pourquoi `vecteur<int> diff(n+1)`? * *
> La sentinelle garantit `right+1` ne sort jamais hors des limites, nous laissant sauter une condition dans la boucle et garder le code rangé.

-----------------------------------------------------------------------------------

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 2237

> **Titre**
> *LeetCode 2237 – Compter les postes dans la rue avec l'éclat requis : le bon, le mauvais, le mauvais – une plongée profonde pour les personnes interviewées prêtes à travailler*

#### 4.1 TL;DR

* **Solution** – Balayage linéaire (balayage linéaire).
* **Complexité temporelle** – "O(n + m)" (`n = longueur de la rue`, `m = #lampes`).
* **Complexité spatiale** – auxiliaire « O(n) ».
* **Pourquoi c'est important** – La maîtrise de ce modèle montre que vous pouvez transformer un problème apparemment quadratique en un élégant « O(n) » – une compétence précieuse pour la conception de systèmes et des entretiens par algorithme.

---

4.2 Le problème, recadrer

Imaginez une route droite avec des intersections `n` (0-based).
Chaque lampadaire illumine un segment contigu des intersections.
Vous êtes donné une exigence de luminosité **minimum** à chaque intersection et doit compter combien d'intersections le rencontrent.

> **Pourquoi la difficulté? * *
> Une approche naïve itère sur chaque lampe pour chaque intersection → `O(n·m)` → trop lent pour `105`.
> La clé est de traiter chaque lampe comme une contribution *intervalle* et de les combiner intelligemment.

---

### 4.3 La bonne – Balayage de ligne + répartition des différences

1. **Intervalles → Préfixer les mises à jour**
*Pour chaque feu:*
Texte
diff[l] += 1 // début de l'éclairage
diff[r+1] -= 1 // après la fin
«» "
Parce que la lampe couvre `[l, r]` inclusivement.

2. ** Pass unique pour calculer la luminosité* *
L'exécution de la somme du préfixe sur `diff` donne la luminosité exacte à chaque position.
Pendant le balayage, comparez avec l'exigence et mesurez la réponse.

3. **Pourquoi ça marche**
Le tableau *différence* stocke le changement *net* à chaque index.
La somme cumulative reconstitue la gamme originale de nombres de luminosité.

4. **Résultat**
* Temps linéaire, travail supplémentaire constant par lampe et par intersection. *
Fonctionne pour les pires limites facilement.

---

4.4 Les mauvaises – Pièges et causes de bord

Pourquoi ça fait mal ?
- C'est quoi ?
**Off‐by‐one à la limite droite**=Les lampes couvrent les gammes *inclus*; oubliant les pauses «right+1» à la fin. Détérioration explicite à la valeur `right+1` (ou utilisation `n` sentinelle). Autres
**L'indice hors limites**Le terme `right+1` peut être `n`; si la taille du tableau est `n`, `diff[n]` est invalide. Ajouter un garde avant de décrémenter. Autres
**Taux négatifs**= Pas dans les contraintes, mais si `la fourchette` était négative, le calcul serait faux. Gammes de pinces à `[0, n-1]` avec "max/min". Autres
**Les grandes valeurs débordent**= `range` jusqu`à `105`; l`utilisation `int` est sûre, mais si elle est étendue, utiliser `long`.== Utiliser `long` ou casting prudent si nécessaire. Autres

---

### 4.5 L'horrible – Quand plus simple est assez

- **Mémory-Bounded Systems** – Le tableau `O(n)` peut encore être lourd si `n` ↓ `109` (hors limites de LeetCode).
*Alternative:* compresser les coordonnées ou utiliser une BST équilibrée des événements.
Pas besoin ici, mais il vaut la peine de savoir.

- **Demandes multiples** – Si vous deviez répondre à de nombreux tableaux d'exigences sur le même ensemble de lampe, recalculer le balayage chaque fois serait gaspillé.
*Optimisation:* Précalculez le tableau de luminosité une fois; chaque requête est une comparaison `O(n)`.

- **Les problèmes de précision dans d'autres langues** – Dans JavaScript ou Python, l'utilisation accidentelle de `float` peut causer des bugs subtils avec de grands entiers.
*Fix:* S'en tenir à l'arithmétique entier et éviter les conversions implicites de type.

---

#### 4.6 SEO— Résumé amical

> *À la recherche d'une solution **Java**, **Python** ou **C++** à LeetCode 2237 – -Décollez les positions sur la rue avec l'éclat requis.
> Maîtrisez la technique **line balay** et **difference array** pour résoudre ce problème en **O(n + m)** temps et **O(n)** espace.
> Découvrez comment éviter les pièges communs comme les erreurs hors-par-un et les indices hors-de-bounds, et voyez pourquoi ce modèle est un must-know pour la conception du système et les entrevues par algorithme. *

---

4.7 Mot final

LeetCode 2237 est plus qu'un puzzle d'éclairage de la route ; c'est un microcosme de problèmes d'agrégation d'intervalle que vous rencontrerez dans les systèmes de production (p. ex., mises à jour de gamme dans les bases de données, modélisation du trafic).
Être en mesure d'identifier et de mettre en œuvre le balayage de la divergence** démontre :

* **La flexibilité algorithmique** – transformer un problème quadratique apparent en temps linéaire.
* ** Discipline de codage** – manipulation prudente des limites et boucles concises.
* **Préparation pour l'embauche technique** – les intervieweurs de modèle adorent voir.

Pratiquez les implémentations ci-dessus, les cas de bord de test, et vous serez prêt à discuter de ce modèle avec confiance lors de votre prochaine entrevue de codage ou conversation de conception système.

---

**Fin de l'article**

---

- Oui. 5. Pensées finales

Le balayage de ligne *différence-array* est un modèle classique qui apparaît dans de nombreuses questions d'entrevue (p. ex., nombre d'intervalles de chevauchement, personnes dans un parc, rectangle maximal, etc.).
En le maîtrisant maintenant, vous serez équipé pour relever les mêmes défis d'agrégation par intervalles dans les systèmes réels, ce qui vous fera un candidat plus fort pour les rôles d'ingénierie logicielle.

Bonne chance pour vos entretiens de codage – et rappelez-vous: une solution propre `O(n)` est toujours une victoire!