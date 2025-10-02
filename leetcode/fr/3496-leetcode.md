---
titre: LeetCode 3496. Maximiser le score après les suppressions de paires - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Code de Leet 3496 – Note maximale après les suppressions de paires
Les bons, les mauvais et les affreux
### Un guide complet, prêt à travailler (Java, Python, C++)

---

TL;DR
* **Idée :** Gardez la partie *la moins précieuse* du tableau (un seul élément si la longueur est étrange, ou une paire adjacente si la longueur est égale) et supprimez tout le reste.
* **Résultat:**
* `d longueur` → `maxScore = somme(s) – min(s) "
* `longueur égale` → `maxScore = somme(s) – min(adjacent‐pair‐sum) "
* **Complexité:** temps «O(n)», espace auxiliaire «O(1)».
* ** Pourquoi c'est une interview parfaite :**
* Élégante preuve avide
* Mise en œuvre de zéro-alloc, un seul passage
* Convient aux modèles Java/Python/C++

---

Déclaration du problème (Code Leet 3496)

> **On vous donne un tableau entier `nums`. Bien que le tableau comporte plus de deux éléments, vous pouvez effectuer l'une des opérations suivantes : * *
> 1. Supprimer les deux premiers éléments.
> 2. Supprimer les deux derniers éléments.
> 3. Supprimer le premier et le dernier élément.
>
> Pour chaque opération, vous ajoutez la somme des éléments supprimés à votre score total.
> **Retournez le score maximum possible que vous pouvez atteindre. **

---

Exemples

Entrée Sortie Explication
C'est pas vrai.
Supprimer les deux premiers : `2+4=6` → best.
[5,-1,42] `7`- Supprimer premier+dernier: `5+2=7` → meilleur.

---

Pourquoi la stratégie fonctionne

1. **Observation**
*Chaque opération supprime exactement deux éléments. *
Par conséquent, après toutes les suppressions possibles, nous serons laissés avec soit **un** élément (longueur od) ou **deux** éléments adjacents (longueur égale).

2. **Objectif**
* Maximiser le score → minimiser la somme des éléments restants. *
Parce que la somme totale du tableau est fixe, le mieux que nous pouvons faire est de garder la partie -cheapest.

3. **Durée approximative**
Nous pouvons réduire à n'importe quel élément.
→ Gardez la valeur minimale `min(nums)`.
→ Score = `sum(nums) – min(nums)'.

4. ** Même longueur**
Nous pouvons réduire à n'importe quelle paire ** adjacent**.
→ Conserver la paire avec la plus petite somme: `min(nums[i] + nums[i+1])`.
→ Score = `sum(nums) – min_adjacent_pair_sum`.

5. **Proof Sketch**
*En induction sur la longueur* – chaque suppression réduit la longueur de 2, en préservant la capacité d'atteindre tout état final requis.
La cupidité de garder le moins cher est optimale car le score est linéaire dans les éléments supprimés et les éléments restants sont la seule chose pour laquelle nous sommes pénalisés.

---

N° # N° de l'espace O(1)

Vous trouverez ci-dessous le code complet pour **Java**, **Python** et **C++**.
Tous les trois utilisent la même logique linéaire du temps, de l'espace constant.

C'est pas vrai. Java

"Java
// Java 17
Importation de java.util.*;

solution de classe publique {
Int public maxScore(int[] nums) {
long total = 0; // utiliser longtemps pour éviter le débordement
int n = longueur nums;

// Calculer la somme totale et l'élément minimal
int minElem = entier.MAX_VALUE;
pour (int v : nombres) {
total += v;
si (v < minElem) minElem = v;
}

// Si la longueur est étrange – garder un élément minimal
si (n % 2] 1) {
retour (int) (total - minElem);
}

// Longueur égale – trouver la somme minimale de paires adjacentes
long minPair = Long.MAX_VALUE;
pour (int i = 0; i < n - 1; i++) {
longue paireSum = (long) nombres[i] + nombres[i + 1];
si (paireSum < minPaire) minPaire = paireSum;
}
retour (int) (total - minPair);
}
}
«» "

> **Pourquoi "long"?**
> Somme allant jusqu'à 1e5 éléments chacun jusqu'à 1e4 correspond à `int` (1e9), mais la soustraction peut être négative; `long` garde les choses en sécurité.

---

# # # # # #

'`python
# Python 3.10
Solution de classe:
def maxScore(self, nombres: list[int]) -> Int:
total = somme(s)
n = len(nums)

si n % 2: # longueur impair
total de retour - min(nombres)

# longueur uniforme – somme minimale de paires adjacentes
min_pair = min(nums[i] + nombres[i + 1] pour i dans l'intervalle(n - 1))
total de retour - min_pair
«» "

> **Pythonique monoligne* *
> `sum(nums) - (min(nums) si len(nums)%2 sinon min(nums[i]+nums[i+1] pour i dans la plage(len(nums)-1)) "

---

C'est vrai. C++

'`cpp
// C++17
solution de classe {
public:
Int maxScore(vecteur<int>& nums) {
long total = 0;
int n = nombres.size();

Int minElem = INT_MAX;
pour (int v : nombres) {
total += v;
minElem = min(minElem, v);
}

si (n & 1) { // impair
retourner static_cast<int>(total - minElem);
}

long minPair = LLONG_MAX;
pour (int i = 0; i < n - 1; ++i) {
longue paire longue = static_cast<long long>(nums[i]) + nombres[i + 1];
minPair = min(minPair, paire);
}
retourner static_cast<int>(total - minPair);
}
};
«» "

---

La complexité temporelle et spatiale

Langue Heure Espace
- C'est quoi ?
* * * * * * *
Python **O(n)**
* * * * * * * * *

Tous les trois fonctionnent dans le temps linéaire et utilisent un espace auxiliaire constant – parfait pour les repères d'entrevue.

---

## --Pièges communs et cas de bord

Piège
- Oui.
Utiliser `int` pour la somme totale → déborder sur les grandes entrées Autres
Autres Oubliant que nous conservons la paire * adjacente* pour une longueur égale.
Dépréciation de la première fois versus la dernière fois → besoin de penser globalement, pas localement La solution avide contourne le besoin de simuler les suppressions.
Un contrôle de longueur uniforme (`n % 2 == 0` vs `n & 1`) est cohérent; les deux fonctionnent mais sont clairs.
Nombres négatifs → `min` fonctionne toujours, mais test avec tous les négatifs

---

Essai rapide

### Java (JUnit)

"Java
@Test
test de vide publicExemples() {
Solution s = nouvelle solution();
assertionEquals(6, s.maxScore(nouvelle int[]{2,4,1});
assertionEquals(7, s.maxScore(nouvelle int[]{5,-1,4,2})
}
«» "

### Python (test unitaire)

'`python
test unitaire d'importation

classe TestSolution(unittest.TestCase):
def test_examples(self):
sol = Solution()
Self.assertEqual(sol.maxScore([2,4,1]), 6)
Self.assertEqual(sol.maxScore([5,-1,42]), 7)

si __nom__ == "__main__" :
unitétest.main()
«» "

C++ (Test Google)

'`cpp
ESSAI (Solution) Essai, exemples) {
Solution s;
EXPECT_EQ(6, s.maxScore({2,4,1}));
EXPECT_EQ(7, s.maxScore({5,-1,4,2}));
}
«» "

---

Pourquoi ce blog vous aidera à trouver un emploi

1. ** Clarté algorithmique** – La preuve gourmande montre de la profondeur dans la compréhension des contraintes de problèmes.
2. **Maîtrise multilingue** – Affiche que vous pouvez traduire la logique à travers Java, Python et C++, un must-have pour les rôles complets et systèmes.
3. **SEO – Contenu optimisé** – Mots-clés comme *LeetCode, interview, algorithme, cupidité, C++, Java, Python, maximiser la note, l'entretien d'emploi* attirer les recruteurs à la recherche de candidats qui ont abordé de vrais problèmes LeetCode.
4. **Readible, Production- Ready Code** – Extraits de code propres et bien commentés que vous pouvez coller dans votre portfolio ou GitHub.
5. **Discussion des cas de bord** – Démontre que vous pensez au-delà de la voie heureuse – un recruteur de caractères cherche.

---

Prochaines étapes de votre entrevue

1. **Mise en oeuvre à partir de zéro** sur un tableau blanc: écrire le passage linéaire, discuter du raisonnement gourmand.
2. **Exposer la complexité** verbalement; montrer pourquoi `O(n)` est optimal.
3. **Montrer la manipulation des cas de bord** (nombres négatifs, tous positifs, tableau à éléments uniques).
4. **S'il est demandé** sur les compromis temps-espace, proposez une variation qui utilise une file d'attente prioritaire pour gérer les suppressions dynamiques, mais expliquez pourquoi il est inutile ici.
5. **Remplissez** en soulignant comment ce problème met en évidence le raisonnement avide, la pensée linéaire et la conception linguistique-agnostique, tous les signaux clés de l'entrevue.

---

À emporter

> *Lorsque vous pouvez réduire un problème à .. garder la partie la moins chère et supprimer tout le reste, la solution avide est presque toujours la plus simple et la plus rapide. Appliquer cet état d'esprit à des problèmes similaires de suppression ou de suppression de paires. *

Bon codage, et que votre LeetCode stries et CV brillent! C'est ce qu'il a dit