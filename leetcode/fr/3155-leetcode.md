---
titre: LeetCode 3155. Nombre maximum de serveurs modifiables -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3155. Nombre maximal de serveurs reclassables – Solution complète
> **Type de problème:** Moyen – Recherche binaire
> **Langues:** Java 17.
> **LeetCode Link:** https://leetcode.com/problems/maximum-number-of-upgradable-servers/

---

- Oui. 1. Récapitulation des problèmes

Vous avez des centres de données `n`.
Pour le centre de données `i` vous savez:

Définition
C'est quoi ?
# de serveurs que vous possédez
"mise à niveau [i]" L'argent nécessaire à la mise à niveau **un** serveur
"vente [i]" L'argent que vous obtenez lors de la vente **un** serveur
"money[i]"" argent que vous avez déjà

Vous pouvez vendre n'importe quel nombre de serveurs (`0 ... count[i]`) **dans ce centre de données seulement**.
Après la vente, vous pouvez mettre à niveau autant de serveurs restants que votre argent le permet.

**Objectif** – Pour chaque data center affiche le nombre maximum* de serveurs pouvant être mis à jour.



---

- Oui. 2. Observations et intuition

* Si nous décidons de mettre à niveau les serveurs `x`, nous devons garder au moins les serveurs `x` invendus.
Par conséquent, `x ≤ count[i] - s`, où `s` = # vendu.

* Le montant total après la vente des serveurs `s` est `money[i] + s * sell[i]`.
Pour mettre à niveau les serveurs `x` nous avons besoin d'argent `x * upgrade[i]`.

* Nous devons trouver le plus grand `x` de sorte qu'il existe un `s` satisfaisant ** les deux**
"x ≤ count[i] - s` ** et** "money[i] + s * sell[i] ≥ x * upgrade[i]".

La clé est que pour un *fixed* `x` le plus petit `s` qui satisfait la contrainte monétaire est

«» "
s_min = ceil( (x * upgrade[i] - money[i]) / sell[i] )
«» "

Si `s_min` est négatif, nous pouvons le définir à `0`.
La contrainte `x ≤ count[i] - s` se transforme en `s ≤ count[i] - x`.

Donc pour un `x` donné nous devons juste vérifier:

«» "
max(0, ceil(x*upgrade - argent)/vendeur) ≤ nombre - x
«» "

Si l'inégalité est maintenue, les serveurs `x` peuvent être mis à niveau.
Sinon, ils ne le sont pas.

Comme la réponse est un entier entre `0` et `count[i]`, nous pouvons effectuer une recherche binaire sur `x`.
Chaque chèque est O(1). La complexité globale par centre de données est "O(log count[i]")",
et pour tous les centres de données `O(n log maxCount)` – assez rapide pour `n, compter ≤ 105`.

---

- Oui. 3. Algorithme (Pseudo)

«» "
pour chaque centre de données i
lo = 0
hi = nombre[i]
pendant que lo < bonjour
milieu = (lo + hi + 1) / 2 // milieu supérieur pour éviter une boucle infinie
// Calcul du montant de la vente requis
requis = max(0, ceil((mid * upgrade[i] - argent[i]) / vente[i])
si nécessaire <= nombre[i] - milieu
lo = mi/ est réalisable
Autre
Bonjour = milieu - 1
réponse[i] = lo
«» "

«ceil(a / b)» en entier arithmétique: «(a + b - 1) // b» (avec «a ≥ 0»).
Tous les produits intermédiaires sont jusqu'à `1010`, donc `long' (Java / C++) ou Python `int` est sûr.

---

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie les serveurs à mise à jour maximale pour chaque centre de données.

**Lemme 1**
Pour tout entier `x` (0 ≤ x ≤ nombre),
Les serveurs `x` peuvent être mis à niveau iff

«» "
max(0, ceil(x*upgrade - argent)/vendeur) ≤ nombre - x
«» "

*Proof. *
- Nécessité:
Soyons le nombre réel de serveurs vendus.
La mise à niveau de «x» nécessite «x ≤ count - s` < < ≤ count - x».
Monnaie après vente: `money + s*vendeur ≥ x*upgrade`
«s ≥ ceil((x*upgrade - argent)/vendeur)».
Ainsi, le plus petit "s" possible qui satisfait la condition monétaire est
`s_min = max(0, ceil((x*upgrade - argent)/vente)`.
Pour une solution réalisable, nous devons avoir `s_min ≤ s ≤ count - x`.
Par conséquent, `s_min ≤ count - x`.

- Assez.
Si `s_min ≤ count - x` choisissez `s = s_min`.
Ensuite, `s ≤ count - x`, nous conservons au moins `x` serveurs.
Et par définition de `s_min` nous avons assez d'argent:
`money + s_min*vend ≥ x*upgrade`.
Ainsi, les serveurs `x` peuvent être mis à niveau. *



**Lemme 2**
Pour chaque centre de données la recherche binaire dans l'algorithme renvoie le plus grand `x`
satisfaisant Lemma 1.

*Proof. *
Le prédicat `P(x)` défini comme -"x` est upgradable.
si les serveurs `x` sont upgradables alors tous les `y < x` sont upgradables aussi bien
(en vendant les mêmes serveurs ou plus).
La recherche binaire sur un prédicat monotone renvoie toujours le maximum `x "
avec `P(x)` true.
L'algorithme utilise la formule médiane supérieure `(lo+hi+1)/2`, de sorte qu'il converge vers le
la plus grande possible "x".



* Théorème *
Pour chaque centre de données l'algorithme produit le nombre maximum possible de
des serveurs améliorés.

*Proof. *
Par Lemma 1 le prédicat utilisé dans la recherche binaire est exactement la faisabilité
État.
Par Lemma 2 la recherche binaire donne le plus grand `x` qui satisfait cette
condition, qui par définition est le maximum de serveurs à mise à niveau. *



---

- Oui. 5. Analyse de la complexité

Opération Coût
- C'est quoi ?
Autres Par recherche binaire du centre de données Autres
Autres Tous les centres de données Autres
Mémoire extra par centre de données, `O(n)` pour le tableau de réponses

Avec `n, compter ≤ 105`, cela s'inscrit facilement dans les limites.

---

- Oui. 6. Mise en œuvre des références

> **Astuce:** Utilisez `long` (Java / C++) ou `int` (Python) pour les produits intermédiaires afin d'éviter les débordements.

---

##### 6.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
public int[] maxUpgrades(int[] count, int[] upgrade, int[] vente, int[] argent) {
int n = longueur du compte;
int[] ans = nouvelle int[n];
pour (int i = 0; i < n; i++) {
lo = 0, hi = nombre[i];
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi + 1) >>> 1; // milieu supérieur
besoin long = (long) milieu * mise à niveau[i] - de l'argent;
longue durée requise Vente = 0;
si (besoin > 0) {
vente = (nécessité + vente[i] - 1) / vente [i];
}
si (obligatoireVente <= (long) compte[i] - milieu) {
lo = milieu;
} autre {
hé = milieu - 1;
}
}
[i] = lo;
}
le retour des an;
}
}
«» "

---

6.2 Python 3

'`python
Solution de classe:
def maxUpgrades(self, compter, mettre à niveau, vendre, argent) -> liste[int]:
ans = []
pour cnt, up, sl, mo en zip(compte, mise à niveau, vente, argent):
lo, salut = 0, cnt
alors que:
milieu = (lo + hi + 1) // 2
besoin = milieu * haut
required_sell = 0 si nécessaire <= 0 autre (besoin + sl - 1) // sl
si requis_vendre <= cnt - mi:
lo = milieu
Sinon:
Bonjour = milieu - 1
Annexe(s)
retour et
«» "

---

*### 6.3 C++17

'`cpp
solution de classe {
public:
vector<int> maxUpgrades(vecteur<int>&compte,
vectorielle<int> et mise à jour,
vectorielle<int> et vente,
vecteur<int>& argent) {
int n = count.size();
vecteur <int> ans(n);
pour (int i = 0; i < n; ++i) {
lo = 0, hi = nombre[i];
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi + 1) / 2; // milieu supérieur
long long besoin = 1LL * mi * mise à niveau[i] - de l'argent;
longue durée requise Vente = 0;
si (besoin > 0) {
vente = (nécessité + vente[i] - 1) / vente [i];
}
si (obligatoireVente <= 1LL * compte[i] - milieu) {
lo = milieu;
} autre {
hé = milieu - 1;
}
}
[i] = lo;
}
le retour des an;
}
};
«» "

---

- Oui. 7. Cas de bord et pièges

Qu'est-ce que regarder ?
- C'est quoi ?
La vente est très petite, mais l ' argent est très faible. Assez de division par zéro ? "vente [i] >= 1` par les contraintes, mais garde avec `si (besoin <= 0)` Autres
Autres Produits de très grande taille (jusqu'à 1010) Autres
`count[i]` = 0= La recherche binaire fonctionne encore (0.0)= Pas de manipulation spéciale nécessaire
Autres Tous les serveurs sont déjà abordables pour la mise à niveau. La recherche binaire se termine à `hi` = `count[i]` Autres

---

- Oui. 8. Stratégie d ' essai

1. **Tests simples** – Dans l'énoncé du problème.
2. **Essais d ' immersion**
- `compte = [0]` → réponse `[0]`
- `argent` assez grand pour mettre à niveau tous → répondre `compte "
- `vente` = 1, `upgrade` = 1, `money` = 0, `count` = 10 → réponse `0` (nécessite de vendre au moins `10` à la mise à niveau `0`?)
3. **Tests aléatoires** – Générer des valeurs aléatoires (dans les limites des contraintes) et vérifier avec la force brute (petit "compte".
4. ** Tests de résistance** – Taille maximale d'entrée (`n = 105`, chaque `compte = 105`) pour s'assurer que les limites de temps/mémoire sont respectées.

---

- Oui. 9. Résumé

* **Problème:** Maximisez les serveurs améliorés par centre de données en vendant certains serveurs.
* **Idée clé:** Recherche binaire sur le nombre de serveurs mis à niveau et une simple vérification de faisabilité en utilisant l'arithmétique entier.
* **Complexité:** `O(n log maxCount)` temps, `O(1)` espace supplémentaire.
* **Résultat:** Solutions prêtes à copier en Java, Python et C++.

---

10. Takeaway optimisé pour le référencement

Si vous vous préparez à une interview **software engineer** et voulez mettre en valeur votre maîtrise de la recherche **binaire** et du raisonnement algorithmique**, ce problème est une vitrine parfaite. Utilisez les extraits de code ci-dessus dans votre portfolio, soulignez l'analyse **temps/espace**, et soyez prêt à expliquer la preuve **mathématique**, qui montrent votre profondeur de compréhension.

Bonne chance pour ce travail de rêve ! C'est ce qu'il a dit.

---

> **Mots clés**: Nombre maximal de serveurs à niveau, LeetCode 3155, Recherche binaire, solution Java, solution Python, solution C++, question d'entrevue, analyse d'algorithme, interview de codage, ingénieur logiciel, entretien d'emploi, défi de programmation, optimisation des centres de données.