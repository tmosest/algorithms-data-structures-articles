---
titre: LeetCode 1672. Riche richesse client -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1672 – Riche richesse client
### Facile – Code Leet

---

### TL;DR
* **Objectif** – Trouvez la richesse maximale parmi tous les clients.
* **Idée** – Sommez les soldes de chaque client, conservez la somme la plus élevée.
* **Complexité** – **O(m × n)** temps, **O(1)** espace supplémentaire.
* **Pourquoi c'est important** – Un problème classique de comparaison qui montre que vous pouvez gérer des tableaux 2-D, des boucles et des maths de base – parfait pour une entrevue technique.

---

Table des matières

Ce que vous apprendrez
- Oui.
Description du problème
Contraintes Autres
Solution Simple Algorithme O(m × n)
Complexe Temps / Espace
Code Java / Python / C++
Éviter les pièges communs
Variations Comment s'adapter pour différentes torsions d'interview
Ce que l'intervieweur se soucie de:
Mots clés que les recruteurs recherchent
Pourquoi maîtriser cela aide à trouver un emploi

---

- Oui. 1. Exposé des problèmes

** La richesse la plus importante du client**
On vous donne une grille entière 2-D `comptes` où `comptes[i][j]` est le montant d'argent que le client *i‐th* a dans la banque *j‐th*.
Rendez la richesse du client le plus riche.

> ** Poids d'un client** = somme de tous ses soldes bancaires.

Exemple

Comptes plus riches
- C'est pas vrai.
[[1,2,3],[3,2,1]]» 6
[[1,5],[7,3],[3,5]» 10
[[2,8,7],[7,1,3],[1,9]

---

- Oui. 2. Contraintes et causes de bord

Contestation Raison
C'est pas vrai.
"1 ≤ m, n ≤ 50" Petite grille, mais nous visons toujours le balayage linéaire. Autres
Toutes les valeurs positives – aucun total négatif. Autres
**Edge case** – un seul client ou une seule banque. Autres

---

- Oui. 3. Aperçu de la solution

1. **Itérer** sur chaque client (ligne).
2. **Sum** tous les soldes de cette ligne.
3. **Track** la somme maximale atteinte.
4. Retourne le maximum.

Parce que tous les nombres sont positifs, pas besoin de gérer zéro ou des sommes négatives.
L'algorithme est essentiellement une « boucle de nested » – une boucle pour les clients, une boucle intérieure pour les banques.

---

- Oui. 4. Analyse de la complexité

Calcul métrique Résultat
- C'est quoi ?
**Temps***** `O(m × n)` – chaque cellule est visitée une fois
**L'espace**

---

- Oui. 5. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**. Chacun utilise la même logique mais est idiomatique pour son langage.

### Java

"Java
***
* 1672. Riche richesse client
* LeetCode problème facile
*/
solution de classe publique {
Nombre maximal de comptes de masse(int[]) {
Int maxWealth = 0;
pour (int[] client : comptes) {
richesse int = 0;
pour (int balance : client) {
richesse += solde;
}
maxWealth = Math.max(maxWealth, richesse);
}
retour maxWealth;
}
}
«» "

Python

'`python
Solution de classe:
def maximumWealth(self, comptes: List[List[int]]) -> Int:
max_wealth = 0
pour les clients dans les comptes:
richesse = somme (client) # somme intégrée est efficace
max_wealth = max(max_wealth, richesse)
_Return maxwealth
«» "

C++

'`cpp
solution de classe {
public:
Int maximumWealth(vector<vector<int>>& comptes) {
Int maxWealth = 0;
pour (const auto & client : comptes) {
richesse int = 0;
pour (int balance : client) richesse += solde;
maxWealth = max(maxWealth, richesse);
}
retour maxWealth;
}
};
«» "

Les trois codes fonctionnent dans **O(m × n)** temps et utiliser **O(1)** mémoire supplémentaire.

---

- Oui. 6. Pièges communs

Piège
- Oui.
**Utiliser `int[]` vs `int[][]` en Java**=Toujours traiter le tableau externe comme une liste de lignes. Autres
**La somme en "int" mais les valeurs peuvent déborder**. Autres
Autres **Tirer le premier client de la richesse**= Initialiser `maxWealth` avec `0` ou calculer la première somme d'abord. Autres
**Utiliser `Collections.max` sur une liste de sommes** Autres

---

- Oui. 7. Variations et extensions

Comment ajuster
C'est quoi ?
**Trouver le k-th client le plus riche** .Utilisez un mini-pap de taille `k` pendant l' itération. Autres
**Offre des soldes négatifs. Autres
Autres **Plus grande entrée (1e5 × 1e5)**= Besoin de streaming ou de somme parallèle; mais les contraintes d'entrevue typiques sont petites. Autres

---

- Oui. 8. Conseils d'entrevue

1. ** Clarifier** – confirmer si les clients et les banques peuvent être des indices de 1 ou de 0.
2. **Edge-case** – demandez quoi retourner si la matrice est vide (bien que les contraintes l'interdisent).
3. **Complexité** – expliquer le temps O(m × n) et pourquoi vous ne pouvez pas faire mieux sans informations supplémentaires.
4. **Optimisations** – discuter en utilisant un `sum()` intégré dans Python pour plus de clarté, mais garder une boucle manuelle en Java/C++ pour un contrôle fin.
5. **Testing** – proposer quelques cas de test : ligne unique, colonne unique, tous les équilibres égaux, tailles variables.

---

- Oui. 9. Résumé optimisé du SEO

- **Mots-clés**: LeetCode 1672, Richest Customer Wealth, solution Java, solution Python, solution C++, algorithme d'entretien, interview de codage, prép d'entretien d'emploi, conception d'algorithme, complexité temporelle, complexité spatiale.
- **Meta Description** (pour un billet de blog):
Code du leet 1672 – Riche richesse client en Java, Python et C++. Apprenez l'algorithme O(m×n) optimal, la manipulation des cas de bord et les conseils prêts à l'entrevue pour les entrevues de codage d'as. (en milliers de dollars)

---

10. Pensée finale

Client le plus riche La richesse peut être étiquetée "Facile", mais la maîtriser démontre les points forts de l'entrevue:

* **Matrix traversal** – une compétence essentielle pour de nombreux problèmes réels.
* ** Analyse temps/espace** – montre que vous pouvez équilibrer les performances avec simplicité.
* **Clean code** – logique claire, bugs minimes et idiomes spécifiques au langage.

Utilisez les extraits fournis comme une référence, pratiquez les écrire à partir de zéro, et vous vous sentirez confiant de résoudre des problèmes similaires dans toute entrevue technique. Bon codage et bonne chance d'atterrissage ce travail de rêve! C'est ce qu'il a dit