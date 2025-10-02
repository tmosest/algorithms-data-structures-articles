---
titre: LeetCode 1936. Ajouter le nombre minimum deungs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1936. Ajouter le nombre minimum deungs
### Les bons, les mauvais et les lugubres – Un LeetCode prêt à l'emploi

> **Mots clés:** Leetcode 1936, ajouter le nombre minimum d'échelons, problème d'échelle, algorithme gourmand, codage d'entretien, solution Java, solution Python, solution C++, algorithme O(n), conseils d'entretien de codage, structures de données, conception d'algorithme, obtenir un emploi

---

Récapitulation des problèmes

Vous êtes debout au sol ('hauteur = 0').
Une échelle a un ensemble de échelons "rungs[]".
Vous ne pouvez passer à l'exercice suivant que si la distance verticale entre votre position actuelle et cet exercice est **-Dist**.

Vous pouvez ajouter n'importe quel nombre de nouveaux échelons à n'importe quelle hauteur entière positive.
**Objectif:** Trouvez le nombre *minimum* d'échelons qui doivent être insérés pour que vous puissiez atteindre le plus haut échelon.

Exemple Entrée Sortie Explication
C'est pas vrai.
Ajouter les échelons aux hauteurs `7` et `8`. Autres
"[3,6,8,10]" ", "dist = 3"" "0" " Déjà grimpable. Autres
Ajouter un échelon à la hauteur `1`. Autres

---

C'est vrai. Pourquoi c'est un problème **Greedy**

Vous n'avez jamais besoin de regarder *ahead* pour décider s'il faut ajouter un rang.
Si l'écart entre deux échelons consécutifs est `gap`, la seule chose qui compte est combien de pas supplémentaires de la taille `= dist` vous devez traverser cet écart.

- **Observation**: La meilleure façon de combler une lacune est d'insérer les plus petits échelons possibles.
Le mieux que vous pouvez faire est toujours de placer un échelon exactement "dist" unités au-dessus de la précédente.

Ainsi, le problème se réduit à : *Pour chaque écart, compter combien d'étapes supplémentaires de longueur `dist` sont nécessaires. *

---

C'est vrai. La formule simple O(n)

Pour un écart `gap = next - current`:

«» "
extra_nécessaire = (gap - 1) // dist
«» "

Pourquoi ?
- Si `gap <= dist` → `gap - 1 < dist` → les rendements de division entier "0". Pas d'appel supplémentaire.
- Si `gap = dist + 1` → `(dist + 1 - 1) // dist = 1` → exactement un échelon nécessaire, etc.

Vous résumez simplement cette valeur sur toutes les lacunes (y compris l'écart entre le sol et le premier échelon).

---

####4=" Mise en œuvre – Code en trois langues

#### Java (style LeetCode)

"Java
// 1936. Ajouter le nombre minimum deungs
// Heure: O(n)
// Espace: O(1)
solution de classe publique {
int public addRungs(int[] échelons, int dist) {
int ajouté = 0; // accumulateur de réponse
int prev = 0; // le point de départ est le sol

pour (int rang : échelons) {
int diff = rung - prev;
si (diff > dist) {
ajouté += (diff - 1) / dist; // division entière
}
prev = échelon;
}
retour ajouté;
}
}
«» "

Python 3

'`python
# 1936. Ajouter le nombre minimum deungs
♪ Heure: O(n)
♪ Espace: O(1)
de taper l'importation Liste

Solution de classe:
def addRungs(self, ranges: List[int], dist: int) -> Int:
ajouté = 0
prev = 0
pour les échelons:
diff = rung - prev
si diff > dist:
ajouté += (diff - 1) // dist
prev = exécution
retour ajouté
«» "

C++

'`cpp
// 1936. Ajouter le nombre minimum deungs
// Heure: O(n)
// Espace: O(1)
int addRungs(vector<int>& ranges, int dist) {
Int ajouté = 0;
int prev = 0;
pour (int rang : échelons) {
int diff = rung - prev;
si (diff > dist) {
ajouté += (diff - 1) / dist;
}
prev = échelon;
}
retour ajouté;
}
«» "

---

C'est vrai. Analyse de complexité

Métrique
- C'est quoi ?
**Heure** Autres
**Espace** Autres

`n` = nombre d ' échelons existants (= 105).
L'algorithme ne scanne le tableau qu'une seule fois et effectue une quantité constante de travail par élément.

---

Pièges communs (Le "Bad")

Pourquoi il échoue
- C'est quoi ?
**Ajout les échelons un par un** (simuler chaque étape) Utilisez la formule de division ci-dessus. Autres
**Off‐by‐one erreurs**= Utiliser `gap / dist` au lieu de `(gap - 1) / dist` donne des nombres erronés lorsque `gap` est un multiple de `dist`.= Toujours soustraire 1 avant la division. Autres
**Ignorer l'écart entre le sol et le premier** Démarrer `prev = 0`. Autres
**Grande quantité d'entiers**. Dans les langues avec une taille d'entiers fixe, `gap` peut être jusqu'à 109. Autres

---

- Oui. Alternatives et variantes

1. **Fenêtre coulissante** – Surkill; l'approche gourmande donne déjà l'optimalité.
2. **PDD récursif** – Frais généraux inutiles; la sous-structure optimale est linéaire et non combinatoire.
3. **Binary Search on Answer** – Peut être utilisé pour les étapes minimales, mais ajoute de la complexité.
4. **Simulate Adding Rungs** – Fonctionne uniquement pour de petites contraintes; sera TLE sur LeetCode.

**Ligne de bottom:** La formule de division est *à la fois* propre et optimale.

---

Python (Python)

'`python
si __nom__ == "__main__" :
sol = Solution()
print(sol.addRungs([1,3,5,10], 2)) # 2
print(sol.addRungs([3,6,8,10], 3)) # 0
print(sol.addRungs([3,4,6,7], 2)) # 1
«» "

---

#### 9=" À emporter pour les entrevues

- **Lisez attentivement la déclaration.** L'écart est entre les positions *consécutives*, pas seulement le dernier échelon.
- **Une preuve de mariage :** L'emplacement optimal des nouveaux échelons est toujours séparé des unités de « dist ».
Si vous sautez un endroit potentiel, vous aurez besoin d'au moins autant d'échelons plus tard.
- ** La complexité est importante.** Les problèmes de LeetCode avec les entrées `105` nécessitent des solutions linéaires.
- **Montrer les maths.** Dérivé `(gap - 1) // dist` explicitement; les intervieweurs aiment voir le raisonnement.
- **Écrire le code propre.** Ajouter des commentaires, utiliser des noms de variables descriptives (`prev`, `gap`, `ajouté`).
- **Test cas bord.**
- Très petit `dist` (1) → vous pouvez avoir besoin de beaucoup d'échelons.
- La réponse est 0.
- Grandes lacunes (jusqu'à 109) → assurer aucun débordement.

---

La dernière pensée

Ce problème est un exemple de manuel d'un algorithme avide qui est *traightforward*, *efficace* et *idiomatic* dans les langues. La maîtriser démontre que vous pouvez :

- Traduire une contrainte du monde réel en une expression mathématique propre.
- Éviter les pièges communs qui mènent à l'EVP ou de mauvaises réponses.
- Écrire le code prêt à la production qui passe tous les cas de bord.

Ce sont exactement les compétences que les recruteurs recherchent lorsqu'ils vous demandent de résoudre l'ajout minimum de Rungs sur une entrevue de codage. Bonne chance pour ce prochain travail !