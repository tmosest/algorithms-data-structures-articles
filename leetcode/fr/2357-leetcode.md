---
titre: LeetCode 2357. Faire arranger zéro en soustrayant des montants égaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Leetcode 2357 – Rendre Array zéro en soustrayant des montants égaux
**Un guide complet et prêt à être interviewé (Java, Python, C++ + SEO-optimized blog post)* *

---

### TL;DR
- **Problème**: Compter les nombres positifs distincts dans un tableau.
- **Pourquoi ça compte**: Il s'agit d'un parfait problème d'entrevue de type "Greedy + set" qui démontre la compréhension de **unité**, **O(n)** temps, **O(n)** espace, et ** manipulation d'array**.
- **Langues**: Java, Python, implémentations C++ fournies.

---

- Oui. 1. Aperçu du problème

> **Leetcode 2357 – Rendre la répartition zéro en soustrayant des montants égaux**
> *Avec un tableau entier non négatif `nums`, dans une opération vous pouvez choisir un entier positif `x` qui est ≤ le plus petit élément non zéro dans le tableau et soustraire `x` de chaque élément positif. Retourner le nombre minimum d'opérations requis pour faire zéro tous les éléments. *

** Principaux faits* *
- "1 ≤ longueur nums ≤ 100", "0 ≤ longueur nums[i] ≤ 100".
- L'opération vous oblige toujours à choisir la valeur *la plus petite* non nulle.
- Chaque valeur positive distincte sera la plus petite une fois, de sorte qu'au moins un élément devient zéro à cette étape.

---

- Oui. 2. Intuition – Le bon, le mauvais, le mauvais

Aspect Pourquoi ça compte ?
-- -- -- -- -- -- -- -- --
**Bon*** *Greedy + Set* La solution est un seul passage avec un `HashSet`/`unordered_set` – propre, rapide et parfait pour les entretiens. Autres
**Modalité **Modèle *Simulation de la force brute*. Autres
L'utilisation d'un `PriorityQueue` et l'effacement à plusieurs reprises ajoute des frais généraux et complique le code. Autres

---

- Oui. 3. Approche optimale – Compter des nombres positifs uniques

1. **Traverse une fois** à travers "nums".
2. Insérer chaque valeur **> 0** dans un ensemble de hachage.
3. La réponse est la taille ** de l'ensemble**.

**Pourquoi ça marche* *
- Oui. Le plus petit élément non zéro sera soustrait une fois.
- Tous les éléments égaux à cette valeur deviennent zéro.
- Oui. La plus petite valeur distincte suivante devient le nouveau minimum, et ainsi de suite.
- Par conséquent, le nombre de valeurs positives distinctes correspond au nombre d'opérations.

---

- Oui. 4. Mise en œuvre du code

#### 4.1 Java
"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe publique {
Nombre minimum d'opérations (int[] nombres) {
Définir <integer> unique = nouveau HashSet<>();
pour (int n : nombres) {
si (n > 0) {
uniquement.add(n);
}
}
retour unique.size();
}
}
«» "

4.2 Python
'`python
Solution de classe:
def minimumOperations(self, nombres: List[int]) -> Int:
# set conserve automatiquement des valeurs positives uniques
retourner len({x pour x en nombres si x > 0})
«» "

### 4.3 C++
'`cpp
#incluez <vecteur>
#inclut <unordered_set>

solution de classe {
public:
int minimumOpérations(std:vector<int>& nums) {
std::unordered_set<int> uniq;
pour (int x : nombres)
si (x > 0)
uniq.insert(x);
retourner uniq.size();
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
Temps **O(n)**
L'espace **O(n)** (ensemble de masse)

Les facteurs constants sont négligeables; le code est clair et évolutif.

---

- Oui. 6. Traitement des cas de bord

Autres Tester le résultat Pourquoi
C'est quoi ?
Pas de nombres positifs → pas d'opérations. Autres
Une seule soustraction positive distincte → une. Autres
Quatre points positifs distincts. Autres
"[]" (invalide par contrainte)

---

- Oui. 7. Esquisse alternative (forte-force) – Pourquoi l'éviter

"Java
// O(n2) – non recommandé pour l'entrevue
Int brute(int[] nums) {
Int ops = 0;
pendant que (aNonZero(nums)) {
int min = minNonZero(nums);
pour (int i = 0; i < nums.longueur; i++)
si (nombres[i] > 0) nombres[i] -= min;
ops++;
}
les opérations de retour;
}
«» "

Cette simulation fonctionne mais est sur-ingénierie pour un simple problème de comptage. Ne l'utilisez qu'à des fins éducatives.

---

- Oui. 8. Pourquoi ce problème se pose pour les entrevues

Compétence testée Explication
C'est pas vrai.
**Causes de grêle**= Identifier que chaque valeur positive unique nécessite une opération séparée. Autres
**L'utilisation de l'ensemble**" montre la familiarité avec les tables de hachage et O(1) insert/look-up. Autres
**Analyse de la complexité** Autres
**Connaissance des cas d'Edge** Autres
Une solution concise de 5 lignes dans chaque langue démontre la lisibilité du code. Autres

Si vous pouvez expliquer cela en 5-7 minutes, vous impressionnerez la plupart des intervieweurs techniques.

---

- Oui. 9. SEO-Optimized Blog Post

> **Titre**: *Code à gauche 2357 – Faire Array Zero en soustrayant des montants égaux
> **Meta Description**: Leetcode 2357 avec code Java, Python et C++. Apprenez la solution avide, les cas de bord, et des conseils d'entrevue pour as votre prochain entretien d'emploi. (en milliers de dollars)

### Rubriques & Mots-clés (pour stimuler les classements de recherche)

- "Code de bord 2357 Faire arranger zéro "
- "Problème d'entretien de l'algorithme de mariage "
- `Set vs PriorityQueue pour Leetcode "
- `Java solution Leetcode 2357 "
- `Python solution Leetcode 2357`
- `C++ solution Leetcode 2357 "
- "Conseils d'entretien pour le codage des entretiens"
- `Rayon des opérations minimales zéro "

**Extrait de poste type**

> Le problème *Make Array Zero* est trompeurment simple mais une mine d'or pour les intervieweurs. Le truc ? Comptez les nombres positifs distincts – c'est tout ce dont vous avez besoin. Ci-dessous vous trouverez des solutions propres et prêtes à la production en Java, Python et C++. (en milliers de dollars)

Utilisez ce post sur votre site de portefeuille, Linked Dans l'article, ou Medium pour présenter vos côtelettes de résolution de problèmes.

---

## 10. A emporter

- **Solution** : nombre de valeurs positives distinctes "
- **Langues**: Java, Python, C++ – tous O(n)
- **Conseil d'entrevue** : Expliquez la perspicacité gourmande et pourquoi l'ensemble est l'approche la plus simple et la plus rapide.
- **Job prêt**: Ajoutez ce message à votre portfolio, marquez-le avec le code 2357 et partagez sur LinkedIn. Les recruteurs aiment le code concis et propre!

Bonne chance pour cette interview ! C'est ce qu'il a dit