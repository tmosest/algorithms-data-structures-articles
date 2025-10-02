---
titre: LeetCode 3345. Produit le plus petit chiffre divisible Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3345 – *Produit à chiffres les plus petits I*
## Solutions Java, Python & C++ + Une profondeur Dive Blog Post

> **Vous souhaitez obtenir votre prochain entretien d'ingénierie logicielle? **
> Cet article traite d'un véritable problème de LeetCode, passe par le *good*, le *bad* et le *ugly* des solutions typiques, et vous donne un code prêt à copier en trois langues populaires.
> Nous vous donnons également un blog prêt à l'emploi qui est pleinement optimisé pour les mots-clés comme *LeetCode 3345*, *coding interview*, *Java solution*, *Python solution*, *C++ solution* et *job interview coding*.

---

## Déclaration du problème

**LeetCode 3345 – Plus petite Produit à chiffres variables I**

On vous donne deux entiers `n` et `t`.
Retourner le plus petit entier `x` (≥ `n`) de telle sorte que le produit de ses chiffres décimaux soit divisible par `t`.

**Contrôles* *

Variable Étendue Remarques
C'est quoi ?
"N" 1 ... 100" minuscule! Autres
"T" 1 ... 10" minuscule! Autres

**Exemples**

Valeur de sortie Raison
C'est quoi, ça ?
1 × 0 = 0 et 0 % 2 = 0
1 × 6 = 6 et 6 % 3 = 0

---

Intuition

Parce que `n ≤ 100` et `t ≤ 10`, l'espace de recherche est minuscule.
Une observation soignée: **vous trouverez toujours un nombre valide dans l'intervalle `[n, n+10]`.**
Par conséquent, une boucle de force brute sur au plus 11 candidats est assez rapide et beaucoup plus facile que d'essayer de construire le chiffre par chiffre.

---

Les bons

Aspect Pourquoi c'est bon
C'est pas vrai.
**Simplicité**= Un pour la boucle, un calcul de produit à un chiffre. Autres
**Temps d'exécution déterministe** Autres
Autres **Aucune bibliothèque spéciale**= Fonctionne sur un compilateur Java, Python ou C++. Autres

---

- Oui. Les mauvais

Aspect Pourquoi c'est mal
C'est pas vrai.
**Pas généralisable**Le truc `+10` ne fonctionne qu'en raison des contraintes. Autres
**Création du produit redondant** Autres

---

- Oui. L'Ugly

Pourquoi c'est bizarre
C'est pas vrai.
Un produit de chiffres peut être zéro (tout chiffre zéro → produit zéro). Autres
Si les contraintes changent, vous briserez la solution. Autres

---

## Code complet (Prêt à copier)

### Java (style LeetCode)

"Java
solution de classe publique {
publique Numéro(int n, int t) {
pour (int i = n; i <= n + 10; i++) {
produit int = 1;
Int x = i;
pendant que (x > 0) {
produit *= x % 10;
x/= 10;
}
si (produit % t) 0) {
retour i;
}
}
// Le problème garantit une solution, mais nous gardons un recul.
retour -1;
}
}
«» "

Python 3

'`python
Solution de classe:
def le plus petit Nombre(self, n: int, t: int) -> Int:
pour i dans la plage (n, n + 11):
produit = 1
pour d en str(i):
Produit *= int(d)
si le produit % t == 0:
retour
«» "

*Python‐one‐liner (la ruse éditoriale LeetCode)*

'`python
Solution de classe:
def le plus petit Nombre(self, n: int, t: int) -> Int:
retourner next(i for i in range(n, n+11) si eval('*'.join(str(i))) % t == 0)
«» "

### C++ (style LeetCode)

'`cpp
solution de classe {
public:
int plus petite Numéro(int n, int t) {
pour (int i = n; i <= n + 10; ++i) {
int prod = 1;
Int x = i;
pendant que x) {
prod *= x % 10;
x/= 10;
}
si (prod % t) 0) retour i;
}
retour -1; // inaccessible sous les contraintes
}
};
«» "

---

Essai d'unité (Python)

'`python
def test():
s = Solution()
selon s.smallestNumber(10, 2) == 10
selon s.smallestNumber(15, 3) == 16
affirmer s.smallestNumber(1, 1) == 1
affirme s.smallestNumber(99, 10) == 100 # produit 0
print("Tous les tests ont réussi.")

essai()
«» "

---

## Analyse du rendement

La complexité temporelle La complexité spatiale Autres
Il s'agit d'un projet pilote.
"O(1)" (soit 11 itérations) Autres
Python Autres
"O(1)" Autres

Parce que `n ≤ 100`, la boucle ne dépassera jamais 11 itérations.
Chaque itération multiplie au plus 3 chiffres → travail constant.

---

Surmonter Liste de contrôle des cas

1. **Zero digit** – produit devient 0 → toujours divisible par n'importe quel `t`.
2. **n elle-même est valide** – la boucle reviendra immédiatement.
3. **t = 1** – tout produit fonctionne; retour `n`.
4. **Large t (10)** – toujours sans danger parce que le produit peut être de 0 ou 10-divisible.

---

Les leçons apprises

- ** Contraintes de levier**: La connaissance `n` et `t` sont minuscules transforme un problème apparemment dur en force brute triviale.
- **Éviter l'optimisation prématurée**: L'astuce +10 est une parfaite optimisation pour ce problème.
- **Toujours inclure un repli** (`retour -1`) pour satisfaire l'analyse statique même si le problème garantit une solution.
- **Ecrire un code lisible** – les intervieweurs valorisent la clarté sur l'intelligence lorsque les contraintes le permettent.

---

## SEO-Optimized Blog Post

> **Titre**: Code Leet 3345 – Plus petite Divisible Digit Product I: Solutions Java, Python & C++ + Conseils d'entretien
> **Meta Description**: Master LeetCode 3345 avec le code Java, Python et C++ propre. Apprenez l'algorithme, les cas de bord et les astuces d'entrevue pour décrocher votre prochain travail d'ingénierie logicielle.
> **Mots-clés**: LeetCode 3345, produit le plus petit divisible I, solution Java, solution Python, solution C++, interview de codage, interview d'algorithme, codage d'entrevue d'emploi, programmation compétitive, conseils d'entrevue.

- Oui. 1. Présentation

*Quoi est LeetCode 3345? *
Il s'agit d'un problème classique de petits nombres, de mathématiques simples qui teste votre capacité à traduire les contraintes en code efficace. Si vous préparez une entrevue technique, la résoudre d'une manière propre, la langue-agnostique démontre une bonne compréhension des fondamentaux de résolution de problèmes.

- Oui. 2. Répartition des problèmes

Expliquez le problème, les contraintes et pourquoi une approche naïve fonctionne ici. Mentionnez l'astuce cachée qui garantit une solution.

- Oui. 3. Pourquoi Brute- Travaux de force

Mettre en évidence le petit domaine (`n ≤ 100`, `t ≤ 10`) et montrer comment une boucle sur `[n, n+10]` est à la fois correcte et optimale.

- Oui. 4. La mise en œuvre dans 3 langues

Afficher les extraits Java, Python et C++ côte à côte. Mettre l'accent sur la lisibilité et mettre en évidence les lignes clés (calcul du produit, limites de boucle).

- Oui. 5. Cas de bord et pièges

Zéro chiffre, `t = 1`, débordement (pas un problème ici), et l'importance d'un retour de retour.

- Oui. 6. Complexité temporelle et spatiale

Tableau rapide – tous `O(1)` – idéal pour les intervieweurs.

- Oui. 7. Conseils d'entrevue

- **Demander des éclaircissements** : Y a-t-il une garantie de solution ? (en milliers de dollars)
- ** Expliquez votre logique** : Parce que `n ≤ 100`, nous n'avons besoin de vérifier que `n+10`. (en milliers de dollars)
- **Parler de cas de bord**: Si un chiffre est 0, le produit est 0, qui est divisible par un `t`.

- Oui. 8. Bonus: Un Trick Python à une ligne

Afficher le `eval('*'.join(str(i))` Trick qui est élégant mais potentiellement risqué pour le code de production.

- Oui. 9. Dernier départ

Vous avez construit une solution réutilisable, prête à l'interview, qui démontre votre capacité à lire les contraintes, à choisir l'algorithme le plus simple et à l'implémenter proprement en Java, Python et C++.

---

## Appel à l'action

Vous voulez impressionner les gestionnaires d'embauche?
- Clone cette repo.
- Faites le test.
- Ajoutez vos propres tests.
- Partagez la solution sur LinkedIn avec le hashtag `#LeetCode3345`.

Bon codage et bonne chance pour votre prochaine interview! C'est ce qu'il a dit