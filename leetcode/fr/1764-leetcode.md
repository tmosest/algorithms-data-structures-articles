---
titre: LeetCode 1764. Forme Array par Concaténating Subarrays d'un autre Array -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (Codeleet 1764)

> **Création d'un sous-ensemble d'un autre tableau* *
> Compte tenu d'un tableau 2-D `groupes` et d'un tableau `nums`, pouvez-vous choisir `n` *disjoint* sub-arrays à partir de `nums` de sorte que le sous-réseau *i‐th* égal `groupes[i]` et que l'ordre soit préservé?
> Retour **true** si c'est possible, sinon **faux**.

* `1 ≤ groupes longueur ≤ 103`
* `1 ≤ groupes[i].longueur, somme(groupes[i].longueur) ≤ 103 "
* `1 ≤ longueur nominale ≤ 103`
* Les éléments correspondent à un entier signé 32 bits.

---

- Oui. 2. Idées fondamentales

Nous devons scanner des "nums" une fois et essayer de localiser chaque groupe dans l'ordre.
Une simple fenêtre coulissante à deux points* suffit :

1. Gardez un index `pos` pointant vers le prochain élément non coché dans `nums`.
2. Pour le `groupe` actuel, essayez de le correspondre par caractère :
* Si l'élément actuel correspond, avancez les deux pointeurs.
* Si une erreur survient, retournez `pos` à l'élément suivant après le début initial de cette fenêtre et redémarrez en fonction du groupe actuel.
3. Si nous joignons avec succès un groupe, `pos` devient l'index juste **après** la sous-banque correspondante.
Continuer avec le prochain groupe.

Si à un moment donné un groupe ne peut être trouvé, nous retournons `faux`.
Sinon, si tous les groupes sont appariés, retourner `true`.

L'algorithme s'exécute dans "O(=nums=" *=groups=" temps (le pire, quand chaque groupe est long et correspond presque partout), mais avec les limites données, il est assez rapide.
L'utilisation de la mémoire est `O(1)` au-delà des tableaux d'entrée.

---

- Oui. 3. Mise en œuvre des références

3.1 Java – Fenêtre coulissante

"Java
Importation de java.util.*;

solution de classe publique {

// Retournez l'index en nombres juste après le groupe correspondant.
// Si elle n'est pas trouvée, retourner -1.
privé int findGroup(int[] group, int[] nums, int start) {
int n = longueur nums;
int m = longueur du groupe;
i = début, j = 0;

pendant que (i < n) {
si (nums[i] == groupe[j]) {
i++; j++;
i (j == m) retour i; // groupe entièrement assorti
} autre {
// retourner i à l'élément après le démarrage initial
i = i - j + 1;
j = 0;
}
}
retour -1; // groupe non trouvé
}

public booléen canChose(int[][] groupes, int[] nombres) {
= 0;
pour (int[] groupe : groupe) {
pos = findGroup(groupe, nombres, pos);
Si (pos) -1) retourner faux;
}
retour vrai;
}

// --- principal pour un contrôle rapide de la santé mentale ---
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
[[]] groupes1 = {{1,-1,-1},{3,-2,0}};
int[] nombres1 = {1,1,0,1,1,1,1,3,-2,0};
Système.out.println(s.can Choisir(groupes1, nombres1)); // true
}
}
«» "

3.2 Python – Fenêtre coulissante

'`python
Solution de classe:
def canChose(self, groupes: List[List[int]], nombres: List[int]) -> bool:
pos = 0 # prochain indice libre en nombres
pour groupe en groupe:
pos = self._find_group(groupe, nombres, pos)
-1:
Retour Faux
retour Vrai

def _find_group(self, groupe: List[int], nombres: List[int], début: int) -> Int:
n, m = len(nums), len(group)
i, j = début, 0
alors que i < n:
si nombres[i]== groupe[j]:
i += 1
j += 1
si j == m: # tout le groupe correspond
retour
Sinon:
i = i - j + 1 # retour
j = 0
retour -1
«» "

### 3.3 C++ – Fenêtre coulissante

'`cpp
solution de classe {
public:
int findGroup(vecteur const<int>&groupe, vecteur const<int>&nums, démarrage int) {
int n = nombres.size(), m = groupe.size();
i = début, j = 0;
pendant que (i < n) {
si (nums[i] == groupe[j]) {
++i; ++j;
i (j == m) retourne i; // correspond complètement
} autre {
i = i - j + 1; //
j = 0;
}
}
retour -1; // non trouvé
}

Bool canChose(vecteur<vecteur<int>>&groupes, vecteur<int>&nums) {
= 0;
pour (auto &g : groupes) {
pos = findGroup(g, nombres, pos);
Si (pos) -1) retourner faux;
}
retour vrai;
}
};
«» "

---

- Oui. 4. Variante: KMP (O(n + m) par groupe)

> **Lorsque vous avez besoin de vitesse absolue** (par exemple `nums.length` jusqu'à `105`), remplacez le balayage linéaire interne par l'algorithme Knuth–Morris–Pratt:
> 1. Construisez le préfixe le plus long qui soit, qui est aussi le tableau Suffix* (LPS) pour `groupe`.
> 2. Numérisez `nums` de `pos` en utilisant la recherche standard KMP.
> 3. Retournez l'index après le match ou `-1`.

KMP garantit que chaque élément de "nums" est examiné au plus deux fois par groupe, ce qui rend toujours la complexité totale "O"nums * #groups", mais avec une très petite constante.
La solution de fenêtre coulissante est souvent plus simple à lire et déjà assez rapide pour les contraintes de ce problème LeetCode.

---

- Oui. 5. Article de blog – LeetCode de maîtrise 1764: Le bon, le mauvais, et le mauvais

> **Mots clés**: LeetCode 1764, tableau de formulaires par sous-arrachages concaténateurs, technique à deux points, algorithme KMP, prép d'entrevue, interview de codage, explication d'algorithme, solution Python, solution Java, solution C++, sous-arrachages disjoints, complexité temporelle, complexité spatiale

---

5.1 Introduction

> Dans le monde du codage des interviews, les problèmes qui testent vos compétences de manipulation *array* et *sub-array appariement* sont communs. Un tel défi est **LeetCode 1764 – Forme Array par Concaténatating Subarrays d'un autre Array. *
> Aujourd'hui, nous allons disséquer ce problème, marcher à travers une élégante solution de fenêtre coulissante, toucher sur une variante KMP plus optimale, et découvrir les pièges cachés qui peuvent trébucher même les développeurs chevronnés.

---

5.2 Exposé des problèmes (en anglais clair)

Vous avez reçu :

* `groupes` – une liste de *n* petits tableaux.
* `nums` – un tableau plus long.

Vous devez décider si vous pouvez **pick `n` non-overlaping segments de `nums`** de telle sorte que:

1. Le segment *i-th* est *exactement* "groupes[i]".
2. Les segments apparaissent dans le même ordre que les groupes.

Si vous pouvez faire cela, retourner `true`; sinon, `faux`.

---

5.3 Contraintes et pourquoi elles comptent

Limites des paramètres
C'est quoi ?
"Groupes.longueur"
1 ... 1 000
"sum(groups[i].longueur)"
1 ... 1 000

Ces chiffres nous disent :

* Tout le problème est ** assez petit** pour une solution \(O(n^2)\) pour passer confortablement.
* Les tableaux d'entrée s'adaptent en mémoire avec **constante espace auxiliaire**.
* Cependant, une interview peut vous demander de *scale* l'algorithme, donc il est bon de connaître l'option KMP plus efficace.

---

### 5.4 La bonne solution – Une solution propre pour glisser

L'idée de base : **scan une fois, avidement correspondre à chaque groupe, puis passer à autre chose. **

5.4.1 Étape par étape

1. Gardez un pointeur `pos` dans `nums` – le premier élément non vérifié.
2. Pour chaque «groupe»:
* Tentative de faire correspondre à partir de `pos`.
* Si un personnage correspond, déplacez les deux pointeurs.
* En cas d'inadéquation, *rollback* `pos` à l'élément juste après le début original de ce groupe et redémarrer.
* Si vous atteignez la fin du groupe, `pos` pointe maintenant juste *après* le segment correspondant.
3. Si un groupe ne peut pas être jumelé, retourner immédiatement «faux».

Parce que nous ** ne retirons jamais** sur des groupes déjà appariés, l'algorithme est linéaire en "nums" pour chaque groupe. Avec au plus 1 000 groupes, le travail total reste minuscule.

Code (Java)

* (voir l'implémentation Java ci-dessus)*

5.4.3 Temps et espace

* **Temps**: \(O(="nums=" \times="groups=")\) dans le pire des cas, mais limité par `1 000 * 1 000` .
* **Espace**: \(O(1)\) extra (seulement quelques indices).

---

Les erreurs communes

Une erreur Pourquoi ça fait défaut
- C'est quoi ?
En utilisant des boucles *nested* qui redémarrent depuis le début des "nums" pour chaque groupe. Maintenir un pointeur mobile (`pos`) et ne jamais recommencer à `0`. Autres
En supposant que les groupes sont uniques ou que le tableau entier peut être partitionné.Les groupes peuvent se chevaucher en valeurs, et vous pouvez sélectionner un sous-réseau qui contient plusieurs groupes (comme dans l'exemple). Traiter chaque groupe de façon indépendante ; l'algorithme assure automatiquement la disjointité. Autres
Autres Ne pas gérer le **edge** quand un groupe est à la fin de "nums" Vous pouvez indexer hors limites. Le temps de boucle vérifie `i < n`; sur l'inadéquation vous retournez, ne jamais dépasser les limites du tableau. Autres

---

### 5.6 Les cas de bord qui survivent même à la bonne solution

Ce qui arrive à regarder
- C'est quoi ?
Les "groupes" contiennent un "sub-array" qui est lui-même une concaténation de deux groupes plus petits. L'approche avide peut prendre tout pour le premier groupe, ne laissant rien pour le second. Autres Puisque l'algorithme correspond aux groupes **exactement**, il ne les fusionne pas par inadvertance. Autres
"nums" est rempli d'un motif répétitif (par exemple, tous les 1s) L'appariement intérieur continuera de rouler beaucoup en arrière, potentiellement menant au cas le plus défavorable \(O(n \times m)\). Acceptez que cela soit encore rapide pour les contraintes, mais si vous êtes poussé vers des données plus grandes, passez à KMP. Autres
Utiliser la concaténation `String` ou convertir des tableaux en chaînes Cela introduit des frais généraux énormes et peut conduire à des comparaisons erronées en raison du formatage des nombres (leading zéros, signes négatifs). Utiliser les tableaux entiers directement. Autres

---

5.7 Quand la vitesse est la question – KMP

Si vous interrogez pour un rôle qui exige une correspondance de chaîne ** linéaire-temps** (p. ex. *recherche d'un motif ADN dans un génome*), l'algorithme **Knuth–Morris–Pratt** est un must-know.

* Construisez un tableau LPS pour chaque groupe une fois – \(O(=group=)\).
* Exécutez la recherche classique KMP sur `nums` à partir de `pos`.
* Vous ne toucherez toujours que chaque élément de `nums` une poignée de fois.

**Pourquoi toujours linéaire?** Parce que la contrainte *order* vous permet de traiter chaque groupe comme un motif séparé ; la complexité globale reste \(O(=nums= \times #groups)\) mais avec une constante beaucoup plus petite que le scan naïf.

*(Le code Pseudo pour KMP est omis pour la brièveté mais est facilement disponible sur les pages de discussion LeetCode.) *

---

#### 5.7 En bas- A emporter en ligne

* **Sliding-window** est la solution *go-to* pour LeetCode 1764.
* **KMP** est la mise à jour *scalable* pour les intervieweurs qui aiment les grandes tailles d'entrée.
* Éviter de redémarrer les scans depuis le début, toujours suivre la position actuelle, et rappelez-vous que *ordre* + * disjointité* sont les deux piliers du problème.

---

5.8 Problèmes pratiques

1. **LeetCode 1448 – -Count Good Ways to Choose a Line of Students** – partition de tableau similaire avec des contraintes.
2. **LeetCode 438 – Trouver tous les Anagrammes dans une chaîne** – un hybride classique KMP/Kadane.
3. **LeetCode 1048 – Le chemin le plus court avec des couleurs alternantes** – pratique de maintenir plusieurs pointeurs à travers des traversées graphiques.

---

### 5.9 Conclusion

> Mastering LeetCode 1764 est plus que résoudre un seul problème ; il s'agit de **comprendre comment les pointeurs de tableau se comportent**, reconnaître les pièges, et apprécier la puissance des algorithmes classiques de couplage de chaînes.
> En combinant une solution propre à la fenêtre coulissante avec la torsion optionnelle KMP, vous serez prêt à aborder le problème dans n'importe quel contexte d'entretien – d'un ensemble de données de 1 000 éléments à un ensemble de données réel massif.

Bon codage, et continuez à résoudre !

---

- Oui. 6. Notes de clôture

* N'hésitez pas à adapter le code de référence à votre langue préférée.
* Pour la préparation d'entrevue réelle, pratiquez le traçage à travers l'algorithme sur papier – cela aide à attraper la logique de retour en arrière.
* Gardez la discussion sur KMP à portée de main – elle démontre votre connaissance de la correspondance *temps-optimisation* et peut vous gagner des points supplémentaires dans une entrevue technique.

---

> **Fin du blog**.