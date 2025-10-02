---
titre: LeetCode 1007. Rotation minimale de Domino pour une ligne égale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1007 – Rotations minimales de Domino pour une ligne égale
**Une passerelle complète, conviviale au référencement, code en Java, Python & C++ + le bon, le mauvais, le laid* *

---

Récapitulation des problèmes

> **LeetCode 1007 – Rotations domino minimales pour une ligne égale**
> Compte tenu de deux tableaux de longueur égale «tops» et «bottoms» (numéros indexés de 1 à 6), chaque paire représente les deux moitiés d'un domino.
> Vous pouvez faire pivoter n'importe quel domino (en haut et en bas).
> Retourner le nombre de rotations *minimum* nécessaires pour que toutes les valeurs supérieures soient égales **ou** toutes les valeurs inférieures soient égales.
> Si cela est impossible, retourner `-1`.

---

- Oui. Pourquoi ça compte

- **Favoris d'entrevue** – les tests de problèmes *manipulation d'arrachage*, *greedy* et *sensibilité aux cas de référence*.
- **Real‐world pertinence** – similaire à -make toutes les colonnes sont égales dans une matrice avec des retournements de rangée.
- **Entretien de codage** – apparaît dans Amazon, Google, Microsoft et beaucoup d'autres entreprises technologiques.
- **Avantage du référencement** – Les rotations minimales des dominos question d'interview et les dominoes uniformes des lignes sont des requêtes de recherche fréquentes.

---

C'est vrai. Les Brutes Idée de force

Vérifiez chaque valeur cible (1–6).
Pour chaque objectif:

1. Scanner tous les dominos.
2. Comptez combien de sommets ont besoin de basculer pour devenir la cible.
3. Comptez combien de fonds ont besoin de basculer pour devenir la cible.
4. Si un domino manque de cible sur les deux moitiés, jetez ce candidat.

Enfin, choisissez le plus petit nombre de rotations.

**Heure**: O(6 · n) → O(n)
**Espace**: O(1)

Parce que le domaine est minuscule (1-6), un seul passage par valeur est assez rapide, et l'algorithme est facile à raisonner.

---

######

Scénario Pourquoi il voyage beaucoup d'implémentations
C'est-à-dire
"tops[i] == fonds[i]" Quelques solutions double-compte rotations.Traitez comme un domino unique; n'ajoutez pas le même nombre deux fois. Autres
Autres La valeur candidate n'apparaît jamais dans un domino.L'algorithme doit immédiatement le sauter. Autres
Les deux valeurs peuvent être égales ou différentes. Autres

---

C'est vrai. La solution propre et prête à la production

Nous présentons la même logique gourmande dans **Java**, **Python** et **C++**. Toutes les implémentations partagent :

- Un assistant pour tester un candidat.
- Un licenciement anticipé quand un candidat est impossible.
- Retour `-1` si aucun candidat ne travaille.

---

Java

"Java
Importation de java.util.*;

solution de classe publique {
int public minDominoRotations(int[] tops, int[] bas) {
int n = longueur supérieure;
// Les candidats sont des numéros 1..6
int best = entier.MAX_VALUE;

pour (int cible = 1; cible <= 6; cible++) {
Int topRot = 0, bas Rotation = 0;
booléen possible = vrai;

pour (int i = 0; i < n; i++) {
Si (dessus [i] != cible && bas[i] != cible) {
possible = faux;
break; // ne peut pas utiliser cette cible
}
if (tops[i] != cible) topRot++; // flip to make top = cible
si (bottoms[i] != cible) bottomRot++; // flip pour faire bas = cible
}

if (possible) best = Math.min(best, Math.min(topRot, bottomRot));
}
Le meilleur retour == Entier. MAX_VALEUR ? -1 : meilleur;
}
}
«» "

> ** Points clefs**
> * La boucle `pour` sur `1..6` garantit O(n).
> * Pas de structures de données supplémentaires → O(1) espace.
> * `Integer.MAX_VALUE` est une sentinelle qui signale clairement aucune solution.

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def minDominoRotations(self, tops: List[int], bas: List[int]) -> Int:
n = len(tops)
INF = flotteur('inf')
meilleure = INF

pour cible de portée(1, 7):
top_rot = bas_rot = 0
possible = Vrai

pour t, b dans le zip (tops, bas):
Si t != cible et b != cible:
possible = Faux
pause
Si t != cible:
top_root += 1
Si b != cible:
base_root += 1

si possible:
best = min(meilleur, min(top_rot, bas_rot))

retourner -1 s'il y a lieu. INF autrement mieux
«» "

> **Pourquoi c'est élégant* *
> * `zip` paires haut & bas – pas d'indexation manuelle.
> * `float('inf')` est une sentinelle naturelle de Python.
> * Le code est ~10 lignes de long – idéal pour des interviews rapides.

---

C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>
utilisant l'espace de noms std;

solution de classe {
public:
int minDominoRotations(vecteur<int>& haut, vecteur<int>& bas) {
int n = tops.size();
int best = INT_MAX; // sentinelle

pour (int cible = 1; cible <= 6; + cible) {
Int topRot = 0, bas Rotation = 0;
bool possible = vrai;

pour (int i = 0; i < n; ++i) {
Si (dessus [i] != cible && bas[i] != cible) {
possible = faux;
pause;
}
Si (dessus [i] != cible) ++topRot;
si (des bas [i] != cible) ++fond Rotation;
}

si (possible)
best = min(meilleur, min(hautRot, basRot);
}
Le meilleur retour == INT_MAX ? -1 : meilleur;
}
};
«» "

> **Notes spécifiques C++**
> * Utiliser `INT_MAX` de `<climits>`.
> * `vector<int>` est basé sur zéro; pas de `size()` hors d'un seul bug.

---

Récapitulation de la complexité du temps et de l'espace

Langue Heure Espace
- C'est quoi ?
Java O(n)
Python O(n)
O(n)

Les trois solutions partagent les mêmes garanties asymptotiques.

---

- Oui. Le bon, le mauvais et le mauvais

Aspect du bien
- C'est quoi ?
**Readability**=Les boucles claires et les pauses précoces== Code qui construit un tableau de fréquences de 7 dimensions (inutile)== Solutions qui comptent les rotations deux fois pour `tops[i]=bottoms[i]=" Autres
**Performance**=Scan O(n) unique par candidat==L'utilisation d'une carte de hachage de la taille 7 est bonne, mais ajoute ~O(1) espace=== Solutions qui vérifient tous les 6 candidats, mais aussi construisent une table de fréquence de 6 tailles → travail supplémentaire trivial==
**Manipulation de cas d'Edge** , toutes les 6 valeurs testées, sentinelle pour , aucune solution , beaucoup de solutions Python oublier de sauter les candidats impossibles → `-1` est retourné incorrectement , Java ou C++ qui retourne 0 lorsque les deux tableaux sont identiques – mauvaise réponse ,

> **Takeaway** – Le scan le plus avide n'est pas seulement rapide, il est également *robust* quand vous traitez les cas de bord correctement.

---

Réflexions finales et conseils d'entrevue

1. ** Expliquez l'idée du candidat** – les intervieweurs adorent voir le raisonnement : la cible doit apparaître dans chaque domino.
2. **Parlez de la sortie anticipée** – si un candidat échoue à l'index 4, pas besoin de terminer le scan.
3. **Mention le domaine constant** – parce que 1–6 est minuscule, nous pouvons nous permettre O(6 · n).
4. **Afficher l'aide** – en option écrire une fonction séparée `testTarget(t, b, cible)` pour garder le code modulaire.
5. **Démonstration du cas d'Edge** – donner un exemple rapide à l'intervieweur ('tops = [1,2]', 'bottoms = [2,1]' → répondre `1`).

---

Conclusion favorable au référencement

Si vous vous préparez à une entrevue technique, le problème des rotations Minimum Domino pour un rang égal** est incontournable.
- Recherches sur Google : *= Entretien minimum de rotations dominos, *=Les dominos font l'uniforme des rangées *=LeetCode 1007 solution*.
- Entreprises: Amazon, Google, Microsoft, Uber, Meta, etc.
- Solution : un scan cupide propre dans le temps O(n), espace O(1), avec manipulation soigneuse de moitiés identiques.

Bon codage et bonne chance pour votre prochaine interview! C'est ce qu'il a dit