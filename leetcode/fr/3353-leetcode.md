---
titre: LeetCode 3353. Total des opérations -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le Code – 3 langues

Voici des implémentations propres, prêtes à la production pour **Java**, **Python** et **C++** qui résolvent LeetCode 3353 – *Opérations minimales*.
Tous les trois suivent la même logique : scanner le tableau de droite à gauche et compter combien de fois un élément diffère de son voisin droit. Ce nombre est le nombre minimal d'opérations de préfixe-addition nécessaires.

> **Pourquoi ça marche* *
> Une opération ne peut que modifier un préfixe. Si vous marchez de la fin du tableau à l'avant, chaque fois que vous touchez une nouvelle valeur, vous devez effectuer une opération *on* pour transformer la partie gauche en cette valeur. Aucune opération supplémentaire n'est jamais nécessaire, et vous ne pouvez jamais faire moins que cela parce que chaque nouvelle valeur force un changement.

---

### Java

"Java
solution de classe publique {
Services d'information
// Les tableaux vides ou à éléments uniques satisfont déjà à la condition.
si (longueur du nombre <= 1) retourner 0;

opérations int = 0;
// Scanner du deuxième élément vers l'avant.
pour (int i = longueur nominale - 2; i >= 0; i--) {
si (nums[i] != nombres[i + 1]) {
opérations++;
}
}
les opérations de retour;
}
}
«» "

---

Python

'`python
Solution de classe:
def minOperations(self, nombres: List[int]) -> Int:
si len(nums) <= 1:
retour 0

ops = 0
# itérer de droite à gauche, comparer chaque élément avec son voisin droit
pour i dans la gamme (len(nums) - 2, -1, -1):
si nombres != Nombres[i + 1]:
Opérations += 1
retour ops
«» "

---

C++

'`cpp
solution de classe {
public:
les opérations (vecteurs<int> et nombres) {
si (nums.size() <= 1) retourner 0;

Int ops = 0;
pour (int i = (int)nums.size() - 2; i >= 0; --i) {
si (nums[i] != nombres[i + 1]) ++ops;
}
les opérations de retour;
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps et utiliser **O(1)** espace supplémentaire.

---

Article du blog – Le bon, le mauvais et le mauvais : maîtriser les opérations totales minimales sur le leetCode 3353

> **Titre:** Le bon, le mauvais et le mauvais: Mastering LeetCode 3353 – Total minimum des opérations
> **Meta Description:** Découvrez comment résoudre LeetCode 3353 en Java, Python et C++ en 30 secondes. Comprendre l'astuce, voir les pièges, et obtenir des conseils prêts à l'entrevue pour obtenir votre prochain emploi.

---

Introduction

Si vous êtes à la chasse pour un rôle d'ingénierie de logiciel, vous avez probablement frappé la section *. Un problème trompeurment simple qui apparaît fréquemment dans les entrevues est **LeetCode 3353 – Minimum Total Operations**.

A première vue, la description ressemble à un candidat à la programmation dynamique ou à un balayage gourmand, mais la vraie solution est un *passe linéaire unique*. Dans cet article, nous disséquons le problème, montrons la solution *bonne* simple, découvrons les pièges *mauvais* sur-ingénierie, et vous avertissons des cas de bord *meilleure* qui peuvent vous faire trébucher lors d'une entrevue.

> **Mots clés**: LeetCode, Minimum Total Operations, Codage interview, Java, Python, C++, algorithme, entretien d'emploi, résolution de problèmes

---

Récapitulation des problèmes

> **Don** un tableau "nums" (longueur jusqu'à 105, valeurs en [−109, 109]).
> **Opération**: Choisissez un préfixe, ajoutez un entier `k` (peut être négatif) à *chaque élément de ce préfixe.
> **Objectif** : Faire en sorte que tous les éléments soient égaux en utilisant le nombre minimum d'opérations.

---

Le bien – Un seul Solution de comptage des passages

Pourquoi ça marche ?

* Chaque opération ne peut changer que le *préfixe*.
* A partir de l'élément le plus droit, le tableau à sa droite est déjà -fixé.
* Chaque fois que vous rencontrez une nouvelle valeur qui diffère de la valeur immédiatement à sa droite, **exactement une** opération est obligatoire pour amener le côté gauche à cette valeur.
* Aucune opération supplémentaire ne peut réduire le nombre.

Algorithme

1. Si la longueur du tableau ≤ 1 → 0 opérations.
2. Il faut passer de l'indice `n-2` à `0`.
3. Si `nums[i] != nums[i+1]`, compteur d'accroissement.
4. Compte de retour.

Complexité

* **Heure**: O(n) – un passage linéaire.
* **Espace**: O(1) – seulement quelques variables.

---

### -Les pièges de l'Ingénierie

Erreurs Ce qui arrive Comment réparer
- C'est quoi ?
**Modélisation du PD/Graph** Collez au balayage linéaire. Autres
Autres **L'utilisation d'une pile ou d'un ensemble de données** Un simple compteur suffit. Autres
**Désormais quitter le premier duplicata**. Comptez toutes les transitions, pas seulement la première. Autres

> **Leçon**: Toujours se demander si une structure de données plus complexe est vraiment nécessaire. Pour ce problème, la structure d'exploitation élimine le besoin de structures avancées.

---

### Les cas de bord et les erreurs courantes

Pourquoi ça se brise ?
- C'est quoi ?
Autres Tableau d'élément unique=Loop commence à `n-2` → index négatif. La poignée `n <= 1` séparément. Autres
Autres Tous les éléments identiques doivent retourner 0, pas n-1. Autres
Autres Valeurs alternantes : `[1,2,1,2]` → 3 opérations. Autres
De grands nombres négatifs. Utilisez `long` en Java si vous voulez être en sécurité. Autres

---

Conseils pour l'entrevue

1. ** Expliquez l'intuition**: Parlez de fixer de droite à gauche et pourquoi un changement force une opération.
2. **Afficher un exemple** sur le tableau blanc: `[1,42]` → marcher à travers le scan.
3. **Complexité des phrases** à l'avant.
4. **Discuses contraintes**: 105 longueur → temps linéaire est obligatoire; pas de DP ou de récursion.
5. **Demander des éclaircissements**: (Oui, c'est autorisé).
6. **Mentionnez le code final** et faites un test rapide.

---

À emporter

LeetCode 3353 est un problème *clean* qui vous enseigne deux choses:

1. **Les opérations de préfixe peuvent être réduites à un problème de comptage. **
2. **Rechercher toujours une solution linéaire avant de construire un DP ou d'utiliser des structures de données lourdes. **

Cette connaissance vous aide non seulement à résoudre le problème en quelques secondes, mais démontre également aux intervieweurs que vous pouvez repérer le chemin le plus simple vers une solution correcte et efficace.

---

Bonus: Galerie de codes

(Voir la section de code en haut pour les implémentations Java, Python et C++.)

---

Prêt à décrocher ce job ?

*Pratiquer ce problème et des problèmes similaires de préfixe. *
*Ajouter la solution à votre portefeuille GitHub. *
*Partagez votre explication sur LinkedIn avec les hashtags #LeetCode #CodingInterview #Algorithm. *

Si vous avez trouvé cet article utile, donnez-lui un pouce vers le haut, laissez un commentaire avec votre propre solution, et partagez-le avec des amis qui se préparent également pour les entrevues de codage.

Bon codage ! Les

---