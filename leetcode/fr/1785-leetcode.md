---
titre: LeetCode 1785. Éléments minimums à ajouter pour former une somme donnée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1785 – Éléments minimaux à ajouter pour former une somme donnée
**Solve It in Java, Python & C++. *

---

Table des matières

Section Lien
C'est pas vrai.
Aperçu du problème
Autres #Intuition
#Cas de bordure
#complexité
Code (Java)
Code (Python)
Code (C++)
Nombre de tests
#interview
Lire la suite Lire la suite Autres

> ** Mots clés du référencement* *
> LeetCode 1785, Éléments minimums à ajouter, Solution Java, Solution Python, Solution C++, Algorithme gourmand, question d'entretien, interview de codage, préparation d'entretien d'emploi, pensée algorithmique

---

- Oui. 1. Aperçu du problème <a name="problem-overview"></a>

> **LeetCode #1785 – Éléments minimaux à ajouter au formulaire une somme donnée* *
> **Difficulté:** Moyenne

On vous donne un tableau entier `nums`, un entier `limite` et un entier `objectif`.
Chaque élément du "nums` satisfait à ""nums[i]" ≤ limite".
Vous pouvez ajouter ** tout nombre de nouveaux entiers** (obéissant également à la "X" ≤ limite") à "nums".
Votre tâche : **Retournez le nombre minimum d'entiers que vous devez ajouter** pour que la somme du tableau entier soit égale à « objectif ».

> **Exemple 1**
> ```texte
> Entrée : nombres = [1,-1,1], limite = 3, but = -4
> Produit: 2
> Explication : ajouter -2 et -3 → 1-1+1-2-3 = -4
> `` "

> **Exemple 2**
> ```texte
> Entrée: nombres = [1,-10,9,1], limite = 100, but = 0
> Produit : 1
> `` "

**Contrôles* *

- "1 ≤ longueur nominale ≤ 105 "
- "1 ≤ limite ≤ 106 "
- `-limite ≤ nombres[i] ≤ limite»
- `-109 ≤ but ≤ 109 "

---

- Oui. 2. Intuition & Greedy Insight <a name="intuition"></a>

1. **Somme actuelle**
Let `currentSum = sum(nums)`.
Le changement total dont nous avons besoin est `diff =="goal - currentSum=".
*Nous ne nous soucions que de la différence absolue – signe n'a pas d'importance parce que nous pouvons ajouter des nombres positifs ou négatifs. *

2. **Choix du mariage* *
Chaque nouvel élément peut contribuer au maximum à la somme (en importance).
Par conséquent, le moyen le plus efficace d'atteindre `diff` est d'utiliser des éléments avec la valeur `±limite`.
- Si `diff` est divisible par `limit`, nous pouvons l'atteindre exactement en utilisant `diff / limit` des éléments.
- Sinon, nous avons besoin d'un autre élément pour couvrir le reste.

3. ** Division des conseils**
`réponse = ceil(diff / limit) = (diff + limit - 1) / limit` (en entier).

Cette approche cupide est **optimale** parce que tout élément de magnitude `< limite` n'augmenterait que le nombre d'éléments nécessaires.

---

- Oui. 3. Cas et pièges des bords <un nom></a>

Piège Explication
C'est le cas.
**Overflow**"sum(nums)" peut dépasser la plage `int` (max. ~109 * 105). Autres
**Objectif négatif**L'utilisation de `abs(objectif - somme)` nous assure toujours de travailler avec une différence non négative. "long diff = Math.abs (objectif - somme);"
**Les plus grands nombres**= `limite` jusqu`à 106; `diff` jusqu`à 2×109 → convient toujours en 64-bit.=Utilisez `long` arithmétique pour la division et le reste. Autres
Autres **Différence de zéro**= Quand `but=somme(s)` → `diff=0`. → 0.
**Negative `limit'**. Ce n'est pas possible par contrainte, mais garde le code défensif. * Traiter la « limite » comme « Math.abs(limite) » si nécessaire. Autres

---

- Oui. 4. Analyse de complexité <un nom=complexité></a>

Étape Temps Espace
C'est pas vrai.
Calcul de la somme des nombres **O(n)**
Calculer la différence et la division du plafond

**Dans l ' ensemble**
- **Heure:** `O(n)` (n = `nums.length`)
- **Espace:** "O(1)" (espace auxiliaire constant)

---

- Oui. 5. Code (Java) <un nom (java)></a>

"Java
***
* Code Leet 1785 – Éléments minimaux à ajouter pour former une somme donnée
* Java 17, O(n) temps, O(1) espace.
*/
solution de classe {
int public int minElements(int[] nums, int limite, int but) {
longue somme = 0; // utiliser longtemps pour éviter le débordement
pour (int num : nombres) {
somme += nombre;
}

long diff = Math.abs(long) but - somme); // différence absolue
// Division du plafond: (diff + limite - 1) / limite
retour (int) ((diff + limite - 1) / limite);
}
}
«» "

> **Pourquoi "long"?**
> `nums` peut contenir jusqu'à 105 éléments chacun jusqu'à ±106 → somme jusqu'à ±1011. "int" déborderait.

---

- Oui. 6. Code (Python) <un nom="python"></a>

'`python
Code Leet 1785 – Éléments minimaux à ajouter pour former une somme donnée
# Python 3.11, O(n) temps, O(1) espace

Solution de classe:
def minElements(self, nombres: list[int], limite: int, but: int) -> Int:
total = somme(s) # Python int n'est pas lié
diff = abs(objectif - total) # différence absolue

# Division de plafond sans point flottant
retour (diff + limite - 1) // limite
«» "

> Les Python's intégrés `sum` gèrent les grands entiers automatiquement, donc aucun problème de débordement.

---

- Oui. 7. Code (C++) <a name="cpp"></a>

'`cpp
// Code Leet 1785 – Éléments minimaux à ajouter pour former une somme donnée
// C++17, temps O(n), espace O(1)

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minElements(vecteur<int>& nums, limite int, but int) {
longue somme longue = 0; // utiliser longtemps pour éviter le débordement
pour (int x : nombres) la somme += x;

long diff = llabs(long long)objectif - somme;
// Ceil(diff / limite)
retourner static_cast<int>(diff + limite - 1) / limite);
}
};
«» "

> `labs` (ou `std::labs`) donne une valeur absolue d'un `long'.
> Le casting vers `int` est sûr parce que la réponse ≤ `ceil(2e9 / 1) = 2e9`, qui correspond à l'int signé 32 bits.

---

- Oui. 8. Cas d'essais d'échantillons <un nom=tests></a>

Autres Test de "nums"
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
[1, -1, 1]» = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
"[0]"
= 10 ', `diff = 10 → ceil(10/5) = 2 ' → **Correction**: En fait `diff = 10 ' → ceil(10/5)=2.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

N'hésitez pas à exécuter ces cas dans n'importe quelle langue pour vérifier l'exactitude.

---

- Oui. 9. À prendre lors de l'entrevue <un nom></a>

Comment ce problème le met en évidence
-- -- -- -- -- -- ----------------------------------
**Le raisonnement de la grêle** Autres
Autres **Maths et division du plafond** Autres
**Connaissance des écoulements d'eau**. Autres
Autres **Optimalité du temps et de l'espace Autres
**Manipulation de cas d'Edge** Autres

**Pourquoi c'est une bonne question d'entrevue* *

- *Longueur* : difficulté moyenne, mais facile à expliquer de façon concise.
- *Common* : Fréquent dans le niveau LeetCodes -Medium, mais rarement demandé dans des entrevues complètes.
- * Versatile*: Peut être prolongée (p. ex., nombre limité d'ajouts autorisés ou coût par élément).

Le fait de mentionner ce problème dans votre portfolio d'entrevues démontre que vous pouvez :

1. Lisez attentivement les contraintes.
2. Identifier la relation mathématique de base.
3. Écrire un code idiomatique propre dans plusieurs langues.
4. Considérez les cas de bord qui pourraient trébucher des solutions naïves.

---

- Oui. 10. Lire la suite <un nom>

- [LeetCode Problème 1785 – Éléments minimums à ajouter pour former une somme donnée](https://leetcode.com/problèmes/minimum-éléments-à-ajouter-à-form-a-don-sum/)
- [Greedy Algorithms – Theory & Practice] (https://www.geeksforgeeks.org/greedy-algorithms/)
- [Division entière et plafond en C++/Java/Python](https://stackoverflow.com/questions/37330290/ceil-division-in-c)
- [Plans de codage des entretiens] (https://leetcode.com/explore/interview/card/amazon/58/array/332/)

---

TL;DR

- ** Calculer la somme courante** → `diff =="Goal - sum=".
- **Ajouts mineurs** = «ceil(diff/limite)» → `(diff + limite - 1) / limite`.
- **Complexité**: temps «O(n)», espace «O(1)».
- **Edge‐cas**: débordement → utiliser 64 bits; zéro diff → répondre 0; signe de but non pertinent.

Avec ce qui précède, vous pouvez résoudre avec confiance le LeetCode 1785 en **any** language—Java, Python ou C++. Bonne chance pour l'entrevue de codage ! C'est ce qu'il a dit.

---