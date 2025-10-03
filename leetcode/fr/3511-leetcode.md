---
titre: LeetCode 3511. Faites un tableau positif -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Faites un tableau positif – 3511
**LeetCode – Medium – O(n) Greedy + Prefix Sum**
*Vous pouvez remplacer n'importe quel élément par n'importe quel entier entre \(-10^{18}\) et \(10^{18}\).
Trouver le nombre minimum de remplacements nécessaires pour rendre le tableau --positif. *

---

Récapitulation des problèmes

> Un tableau est **positif** si *chaque* sous-aire de longueur **≥ 3** a une somme **positif**.
>
> Vous pouvez effectuer l'opération suivante n'importe quel nombre de fois:
> Remplacer un élément dans `nums` par un entier dans la plage \([-10^{18},10^{18}]\).
>
> **Objectif:** Retourner le nombre minimum d'opérations nécessaires.

Exemple Entrée Sortie Pourquoi ça marche
- C'est quoi ?
Le remplacement de `10` par `0` fait la somme entière `3`. Autres
Le remplacement `-2` par `1` corrige tous les sous-réseaux de 3 longueurs qui n'étaient pas positifs. Autres
{\pos(192,220)}[1,2,3] {\pos(192,220)}Déjà positif. Autres

> **Constraints**
> \(3 \le n \le 10^5\)
> \(-10^9 \le nombres[i] \le 10^9\)

---

- Oui. Aperçu clé

Chaque sous-aire de longueur **≥ 3** contient une sous-aire de longueur **exactement 3**.
Si *chaque sous-arraison de longueur‐3 a une somme positive, **chaque sous-arraison plus longue sera automatiquement positive aussi bien (puisque c'est une somme de blocs de 3 longueurs positives qui se chevauchent).

Il suffit donc d'imposer la positivité sur **toutes les fenêtres de 3 longueurs**.

---

C'est vrai. Approche de l'avidité et du préfixe

1. **Prefix sum array** `pref[i] = sum(nums[0 ... i]) "
*Nous permet de calculer la somme de n'importe quelle fenêtre dans O(1). *

2. **Scannez le tableau de gauche à droite* *
Maintenez `maxPref` = somme de préfixe maximale vue à ce jour (initialement `0`).
Pour chaque position «i» (le dernier indice d'une fenêtre 3):

- La somme des 3-fenêtres se terminant à "i" est
'fenêtre Somme = pref[i] - maxPréf.
- Si `windowSum <= 0`, nous ** devons** changer un élément dans cette fenêtre.
Compter une opération, définir `maxPref = pref[i]` (Traitez toute la fenêtre comme "fixé" en la faisant zéro), et **skip les deux indices suivants** (`i += 2)).
Sauter est sûr parce que le remplacement que nous imaginons réparerait toute sous-entente qui inclut ces positions.

3. Retournez le nombre d'opérations.

> ** Pourquoi sauter ? **
> Après avoir remplacé un élément de la fenêtre `[i-2, i]`, tout sous-ensemble qui contient encore l'un des deux indices suivants contiendrait déjà l'élément remplacé (et donc positif), de sorte qu'il ne peut pas redevenir non positif.
> Sauter les garanties que nous ne retenons jamais un remplacement nécessaire.

---

C'est pas vrai. Complexité

- **Heure**: \(O(n)\) – un passage linéaire.
- **Espace**: \(O(n)\) pour le tableau de somme de préfixe (peut être réduit à \(O(1)\) si nous conservons une somme de roulement).
Dans la pratique, l'espace supplémentaire est parfait pour \(n \le 10^5\).

---

Mise en œuvre

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

> **Note** : Les commentaires du code expliquent la logique et vous aident à l'adapter pour des entrevues ou des défis de codage d'emploi.

---

##### 5.1 Java (Code Leet)

"Java
Importation de java.util.*;

solution de classe {
public int makeArrayPositive(int[] nums) {
int n = longueur nums;
long[] pref = nouveau long[n];
pref[0] = nombres[0];
pour (int i = 1; i < n; i++) {
pref[i] = pref[i - 1] + nombres[i];
}

Int ops = 0;
long maxPref = 0; // meilleure somme de préfixe jusqu'à présent
pour (int i = 0; i <= n - 3; i++) {
// somme des nombres de fenêtres[i] + nombres[i+1] + nombres[i+2]
longue fenêtre Somme = pref[i + 2] - maxPref;
si (fenêtreSum <= 0) {
ops++; // remplacer un élément dans cette fenêtre
maxPref = pref[i + 2]; // prétendre que cette fenêtre est devenue 0
i += 2; // sauter les deux indices suivants
} autre {
maxPref = Math.max(maxPref, pref[i]); // mettre à jour le meilleur préfixe
}
}
les opérations de retour;
}
}
«» "

---

5.2 Python 3

'`python
Solution de classe:
def makeArrayPositive(self, nombres: List[int]) -> Int:
n = len(nums)
pref = [0] * n
pref[0] = nombres[0]
pour i dans la plage (1, n):
pref[i] = pref[i - 1] + nombres[i]

ops = 0
max_pref = 0 # meilleur préfixe vu à ce jour
i = 0
alors que i <= n - 3:
window_sum = pref[i + 2] - max_pref
si window_sum <= 0 :
Opérations += 1
max_pref = pref[i + 2]
i += 3 # sauter les deux prochains indices aussi
Sinon:
max_pref = max(max_pref, pref[i])
i += 1
retour ops
«» "

---

#### 5.3 C++ (g++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int makeArrayPositive(vecteur<int>& nums) {
int n = nombres.size();
vecteur <long> pref(n);
pref[0] = nombres[0];
pour (int i = 1; i < n; ++i) pref[i] = pref[i-1] + nums[i];

Int ops = 0;
long long maxPref = 0; // meilleur préfixe jusqu'à présent
pour (int i = 0; i <= n - 3; ++i) {
longue fenêtre Somme = pref[i+2] - maxPref;
si (fenêtreSum <= 0) {
++ops; // modifier un élément
maxPref = pref[i+2]; // fenêtre considérée comme fixe
i += 2; // sauter les deux indices suivants
} autre {
maxPref = max(maxPref, pref[i]); // garder le meilleur préfixe
}
}
les opérations de retour;
}
};
«» "

---

#### 6-- Ce que vous devriez garder à l'esprit

C'est bon C'est mauvais
- C'est quoi ?
L'avidité est **optimale** – aucun retour en arrière nécessaire. L'oubli de la plage de somme du préfixe (`long long` / `long`) conduit au débordement. Autres
Un seul balayage linéaire – s'adapte aux contraintes d'entretien. Mauvaise lecture de la longueur du sous-réseau > (certains pensent que 3. – corriger est 2). Autres
Il est facile de prouver la justesse: chaque sous-tribu longue contient une fenêtre de 3. Ne pas traiter le cas où `n < 3` (bien que les contraintes l'interdisent). Autres
Fonctionne pour les grandes valeurs négatives et positives parce que nous utilisons `long`/`long '. Si vous remplacez l'élément par un très grand nombre négatif dans l'exemple, vous pourriez avoir besoin d'une autre opération – assurez-vous de choisir une valeur qui neutralise la fenêtre (0 ou positive). Autres

---

- Oui. Pourquoi ce blog vous aide à trouver un emploi

- **Explication algorithmique claire** – les intervieweurs aiment le raisonnement concis.
- **Multiples implémentations de langage** – montrez que vous pouvez coder en Java, Python et C++.
- **SEO-friendly content** – des mots-clés comme "Faire un tableau positif", "Leetcode 3511", "greedy algorithme", "O(n) solution" se classeront haut.
- **Conseils pratiques** – le tableau ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Utilisez cet article comme référence lors de la préparation des entrevues de codage, et n'hésitez pas à adapter les extraits de code pour vos propres projets ou portefeuilles.

---

* # # # # # TL;DR

1. *Les fenêtres de 3 longueurs seulement comptent. *
2. Scanner de gauche à droite avec une somme préfixe.
3. Quand une somme de 3 fenêtres ≤ 0, compter une opération, traiter cette fenêtre comme fixe, et sauter les deux indices suivants.
4. Retourner le total des opérations – c'est le minimum.

Joyeux codage, et que les dieux d'entretien soient avec vous! C'est ce qu'il a dit