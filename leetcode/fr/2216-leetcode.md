---
titre: LeetCode 2216. Suppression minimale pour rendre l'array magnifique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2216 – Suppression minimale pour rendre l'array beau
**Solution en Java, Python et C++******O(1) Greedy**

---

- Oui. 1. Récapitulation des problèmes

> **Beau tableau**
> * `nombres.longueur` est même
> * Pour chaque indice pair `i`, `nums[i] != nombres[i+1] "

Nous pouvons supprimer n'importe quel nombre d'éléments (les éléments restants conservent leur ordre relatif).
Retournez les suppressions **minimum** nécessaires.

«» "
Entrée: nombres = [1,1,2,3]
Sortie: 1 // supprimer une des deux 1s
«» "

---

- Oui. 2. Principales observations

Lorsque nous construisons le tableau de gauche à droite, nous avons seulement besoin de savoir:

* **Ce que le dernier élément à un indice pair est** (`pre`).
- Si le nombre suivant est égal à `pre`, nous devons le supprimer (autrement `nums[i] == nums[i+1]`).
- S'il diffère, nous pouvons le garder et *reset* le marqueur "even index" (la prochaine fente est étrange).

L'algorithme n'a jamais besoin d'aller plus loin – une décision gourmande est optimale.

---

- Oui. 3. Greedy, O(1) Algorithme spatial

Étape
C'est quoi ?
Démarrage : "res = 0" (compte de suppression), "pre = -1" (pas encore d'élément d'indice pair)
*Si `a == pre` → supprimer (`res++`).*<br>*Else* → set `pre = (pre < 0 ? a : -1)«=» Lorsque nous conservons un nombre à une position uniforme, nous remettons `pre` à `-1` afin que l'élément suivant puisse être placé à la position étrange. Autres
Après la boucle.Si `pre >= 0` (la longueur du tableau est étrange) → `res++` (supprimer le dernier élément) Autres

---

- Oui. 4. Preuve de l ' exactitude

*Nous prouvons par induction que l'algorithme produit un beau tableau valide avec le nombre minimal de suppressions. *

1. **Base**: Avant de traiter un élément, le tableau vide est beau.
2. **Étape d'introduction**:
* Supposons que le préfixe traité (après « k » itérations) est le **le plus court** beau subséquence des premiers « k » nombres. *
* Pour le numéro `k+1`-th `a`:
*Si `a == pre`*: garder `a` violerait la règle d'adjacence à un index pair → toute belle séquence doit supprimer `a`. L'algorithme le supprime, conservant la propriété minimale.
*Si `a!= pre`*:
- Si `pre` est négatif, `a` peut occuper en toute sécurité la fente même actuelle → l'algorithme le garde.
- Si `pre` est non-négatif, cela signifie que l'élément précédent a été placé à une fente étrange, de sorte `a` peut occuper en toute sécurité la fente suivante, réinitialisant `pre`.
Dans les deux cas, l'algorithme garde `a` lorsqu'il ne nuit pas à la faisabilité, en préservant des suppressions minimales.

3. **Après traitement**: Si `pre >= 0` après la boucle, la longueur du courant est impair. Tout tableau beau doit être de taille égale, de sorte que le dernier élément doit être supprimé. L'algorithme le supprime, encore minime.

L'algorithme fournit ainsi la solution optimale.

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
Temps **O(n)**
Espace

`n` ≤ 105, donc le balayage linéaire est assez rapide.

---

- Oui. 6. Mise en œuvre des références

> **Note**: Les trois versions suivent la même logique gourmande et peuvent être copiées dans LeetCode.

##### 6.1 Java (Signature de code à gauche)

"Java
solution de classe {
public int minDeletion(int[] nums) {
= 0; // réponse jusqu'à présent
int pre = -1; // dernier élément à un indice pair (-1 signifie aucun)

pour (int a : nombres) {
si (a == pre) { // enfreindrait la règle de beauté
suppressions++;
} autre {
// conserver une
pre = (pre < 0) ? a : -1; // si nous venons de placer un élément pair, réinitialiser
}
}

// Si nous avons terminé avec un tableau de longueur impair, supprimer le dernier élément
si (pré >= 0) {
suppressions++;
}
les suppressions de retour;
}
}
«» "

6.2 Python 3

'`python
Solution de classe:
def minDeletion(self, nombres: List[int]) -> Int:
suppressions = 0
pre = -1 # dernier élément d'indice uniforme

pour les nombres:
si une == pre: # violerait la règle
suppressions += 1
Sinon:
pre = a si pre < 0 autre -1 # conserver ou réinitialiser

si pré >= 0: # longueur impair à la fin
suppressions += 1
retourner les suppressions
«» "

*### 6.3 C++17

'`cpp
solution de classe {
public:
Int minDeletion(vecteur<int>& nums) {
les suppressions d'int = 0;
int pre = -1; // dernier élément indice pair

pour (int a : nombres) {
si (a) avant {
++suppression; // doit supprimer
} autre {
Pré = (pré < 0) ? a : -1; // conserver ou réinitialiser
}
}

si (pré >= 0) {/ longueur impair
+suppressions;
}
les suppressions de retour;
}
};
«» "

---

- Oui. 7. Bien, mal, et lugubre – quoi surveiller

Aspect du bien
- C'est quoi ?
**Logique**= Pure cupidité, pas de DP ou de pile requis== Défaut de penser au drapeau =reset== → boucle infinie== Oublier de gérer le cas final de longueur impair (Bogue commun)==
Autres **Cas d'Edge**= Tableau vide → 0 suppressions== Élément unique → 1 suppression (doit supprimer)== Très long terme de nombres égaux → tous sauf un doivent être supprimés===
**Testation** , `[1,1]`, `[1,2]`, `[1,1]` , "[1,1]` , Des motifs mixtes égaux/inégaux. vitesse

---

- Oui. 8. Conseils d'entrevue prêts

1. ** Expliquez l'invariant** : « pré » détient la valeur qui, si elle était répétée, violerait la règle de beauté. (en milliers de dollars)
2. **Afficher la preuve**: Utilisez l'induction ou un petit contre-exemple.
3. **Parler de l'espace**: O(1) est un point de vente fort.
4. **Manipulation des bords de mention**: La suppression finale de la longueur étrange est la subtilité qui voyage souvent les candidats.
5. **Afficher les séries d'échantillons**: Passez par `[1,1,2,2,3,3]` et soulignez où chaque suppression se produit.

---

- Oui. 9. Dernier départ

La solution O(1) cupide pour **LeetCode 2216** est propre, rapide et parfaite pour une entrevue de codage.
Son élégance consiste à reconnaître que *seul le dernier élément indexé est important* et que la parité du tableau décide si une suppression supplémentaire est nécessaire à la fin.

Bon codage ! C'est ce qu'il a dit.

---

**Mots-clés**: LeetCode 2216, Suppression minimale pour rendre l'array beau, O(1) Greedy, Solution Java, solution Python, solution C++, prep interview, beauté du tableau, complexité temporelle, complexité spatiale.