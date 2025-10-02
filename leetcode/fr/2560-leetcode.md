---
titre: LeetCode 2560. Robeur de maison IV -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Le guide complet et optimisé pour le vol à la maison IV (code Leet 2560)* *
*Du bon au mauvais – Tous les codes, théories et conseils d'entrevue dont vous avez besoin*

---

Récapitulation des problèmes

> ** Vol à main armée IV**
> *Moyenne – 2560*
>
> Nous avons des maisons dans une rue.
> `nums[i]` est le montant d'argent dans la maison `i`.
> Un voleur ne peut jamais voler deux maisons adjacentes.
> La capacité* du voleur est la somme **maximum** prélevée dans une seule maison parmi toutes les maisons qu'il a volées.
>
> ** Objectif**: Rob ** au moins `k` maisons** (il y a toujours un moyen possible) et de rendre la capacité ** minimum possible**.

---

C'est vrai. L'idée fondamentale – Recherche binaire sur la réponse

*Pourquoi la recherche binaire? *
La réponse est une valeur entre `1` et `max(nums)`.
Si nous pouvons vérifier si un "mid" particulier (la capacité du candidat) est réalisable, nous pouvons décider de la moitié de l'espace de recherche à conserver.

Essai de faisabilité (canRob)

- Oui. Nous balayons le tableau de gauche à droite.
- Oui. Lorsque nous rencontrons une maison avec `nums[i] ≤ mi`, nous *rob* il et sauter la maison suivante (parce que les maisons adjacentes sont interdites).
- Comptez combien de maisons nous avons volées.
- Si le nombre est au moins `k`, `mid` est **bon**; sinon il est **bad**.

Ce scan avide garantit le nombre *maximum* de maisons que nous pouvons voler avec la capacité `mid`.
Si même ce maximum est `< k`, aucun arrangement avec la capacité `mid` ne peut satisfaire aux exigences.

Complexité

Étape Temps Espace
C'est pas vrai.
Contrôle de faisabilité Autres
Recherche binaire sur les itérations `[1, max(nums)]`"O(log(max(nums))` Autres

Total: temps `O(n log(max(nums))`, espace auxiliaire `O(1)`.

---

C'est vrai. Le code

Voici trois solutions idiomatiques complètes – **Java**, **Python** et **C++** – prêts à être collés dans l'éditeur en ligne LeetCode.

> **Tip** – L'environnement LeetCode ne nécessite que la classe `Solution` et la signature de la méthode.
> Rien d'autre (aucune fonction principale) n'est nécessaire.

---

Java

"Java
solution de classe {
// Vérification de faisabilité: peut-on voler au moins k maisons avec une capacité <= mi?
booléen privé canRob(int[] nums, int mi, int k) {
nombre int = 0;
pour (int i = 0; i < longueur nums; ) {
si (nums[i] <= milieu) {
count++; // voler cette maison
i += 2; // sauter la maison adjacente
} autre {
i++; // ne sauter que cette maison
}
}
le nombre de retours >= k;
}

Int minCapabilité(int[] nombres, int k) {
int gauche = 1, droite = 0;
pour (int v : nombres) droite = Math.max(droite, v); // max(nums)

int ans = droite;
pendant que (gauche <= droite) {
int milieu = gauche + (droite - gauche) / 2;
si (canRob(nums, milieu, k)) {
ans = milieu;
droite = milieu - 1; // essayer d'abaisser la capacité
} autre {
gauche = milieu + 1; // besoin d'une capacité plus grande
}
}
le retour des an;
}
}
«» "

---

Python

'`python
Solution de classe:
def can_rob(self, nombres: list[int], limite: int, k: int) -> C'est vrai.
"""Retour Vrai si nous pouvons voler au moins k maisons avec le montant maximum <= limite."""
cnt = 0
i = 0
n = len(nums)
alors que i < n:
si nombres[i] <= limite:
cnt += 1
i += 2 # Sautez la prochaine maison
Sinon:
i += 1
retour cnt >= k

def minCapability(self, nombres: list[int], k: int) -> Int:
lo, hi = 1, max(nums)
ans = bonjour
alors que lo <= bonjour:
milieu = (lo + hi) // 2
si soi-même. can_rob(nums, mi, k) :
ans = milieu
Bonjour = milieu - 1
Sinon:
lo = milieu + 1
retour et
«» "

---

C++

'`cpp
solution de classe {
public:
// Essai de faisabilité de l'avidité
bool canRob(vecteur const<int>& nums, int limit, int k) {
cnt = 0, i = 0, n = nombres.size();
pendant que (i < n) {
si (nums[i] <= limite) {
++cnt;
i += 2; // sauter la maison adjacente
} autre {
++i;
}
}
retour cnt >= k;
}

int minCapabilité(vecteur<int>& nombres, int k) {
int lo = 1, hi = *max_element(nums.begin(), nums.end()), ans = hi;
pendant que (lo <= bonjour) {
Int milieu = lo + (h - lo) / 2;
si (canRob(nums, milieu, k)) {
ans = milieu;
hé = milieu - 1;
} autre {
lo = milieu + 1;
}
}
le retour des an;
}
};
«» "

---

C'est pas vrai. Le bien – Pourquoi Cela fonctionne

Explication
-- -- -- -- -- --
La recherche binaire garantit la capacité minimale. Autres
**La vérification de faisabilité n'est qu'une seule passe ('O(n)'). Autres
À la différence du classique House Robber, nous n'avons pas besoin de garder la trace de deux états ; un nombre avide suffit. Autres
**Évoluable**= Fonctionne confortablement pour `n ≤ 105` et `nums[i] ≤ 109`. Autres
**Code clair**= Pas de magie cachée – boucles simples, conditions simples. Autres

---

C'est vrai. Le mal – Pièges communs

Erreur de correction
C'est le cas.
La recherche binaire se limite à l'un d'eux en utilisant ` while (gauche < droite)` et de retourner `gauche` peut manquer la réponse exacte si la dernière comparaison est erronée. Autres
Dépassement de l'adjacence incorrectement Augmentation de l'indice par `2` **seulement** lors du vol; sinon augmentation par `1`. Faire en sorte que la clause "else" ne saute pas inutilement les maisons. Autres
Utiliser `int` pour des sommes importantes. "S'en tenir à "int" pour les valeurs de capacité; elles s'inscrivent dans les 32 bits. Autres
Le dépassement dans le calcul `mid` `mid = (gauche + droite) / 2` peut déborder en utilisant `int`. Autres
Le retour `long` où `int` est attendu peut causer une erreur de type. Autres Retourner le même type que la signature (`int`). Autres

---

- Oui. L'Ugly - Cas de bord et considérations supplémentaires

1. **Toutes les maisons ont la même valeur**
* Par exemple*, "nums = [5, 5, 5]", "k = 2".
La réponse est simplement cette valeur (5). La recherche binaire fonctionne encore, mais elle est surqualifiée.

2. **Très grand `k`**
`k` peut être égal `(n+1)/2` (le nombre maximum de maisons non jumelées).
Le comptoir gourmand choisira toutes les autres maisons – toujours 'O(n)'.

3. **Tableau de la taille 1**
Si `k = 1`, la réponse est `nums[0]`.
Notre algorithme s'en occupe naturellement.

4. ** Contraintes de mémoire* *
La solution utilise la mémoire supplémentaire `O(1)` – parfait pour les scénarios d'entrevue où l'espace constant est mis en évidence.

5. ** Limite de temps dans une langue comme Python**
Bien que `O(n log(max(nums))" soit bien pour `n = 105`, les boucles plus lentes de Python's peuvent repousser la limite de temps de près de 2 secondes sur LeetCode.
*Optimisation*: Convertissez la liste d'entrée en `list[int]` (déjà le cas) et éviter les appels de fonctions répétées par la logique en ligne si nécessaire.

---

### # 7-Ébauche du blog optimisé

> **Titre**: *Mastering LeetCode 2560 – Robeur de maison IV: Recherche binaire, Greedy et Interview‐ Code prêt (Java, Python, C++)*
> **Meta Description**: Apprenez la solution efficace pour LeetCode House Robber IV en utilisant la recherche binaire. Obtenez des explications étape par étape, des extraits de code en Java, Python et C++, et des conseils d'entrevue.

---

Introduction

Si vous vous préparez à des entrevues de codage, **House Robber IV (LeetCode 2560)** est un problème à étudier. Il teste votre capacité à combiner la recherche binaire, la logique gourmande et la manipulation soignée des cas. Dans ce post, nous allons marcher à travers le problème, dériver un algorithme optimal, discuter des pièges, et livrer le code poli dans trois des langues les plus populaires.

> **Pourquoi ce problème est important* *
> - Affiche la compétence avec ** recherche binaire sur la réponse** – un modèle d'entrevue commun.
> - Faits saillants raisonnement gourmand vs programmation dynamique.
> - Testez votre compréhension des contraintes non adjacentes** et de l'optimisation de la valeur maximale.

---

Récapitulation du problème

(Inclure l'énoncé complet du problème avec les exemples ci-dessus)

---

#### Intuition & Stratégie

(Expliquez la recherche binaire sur la capacité maximale, la vérification de faisabilité gourmande, et pourquoi elle fonctionne. Utiliser des diagrammes si possible.)

---

Code Pseudo

«» "
canRob(nums, limite, k):
nombre = 0
i = 0
alors que i < n:
si nombres[i] <= limite:
nombre += 1
i += 2 // sauter la maison suivante
Sinon:
i += 1
Nombre de retours >= k

minCapabilité(nombres, k):
lo = 1
hé = max(nums)
ans = bonjour
alors que lo <= bonjour:
milieu = (lo + hi) // 2
si canRob(nums, mi, k):
ans = milieu
Bonjour = milieu - 1
Sinon:
lo = milieu + 1
retour et
«» "

---

Mise en œuvre complète

(Insérer les blocs de code Java, Python et C++ ci-dessus.)

---

Analyse de complexité

- **Heure**: "O(n log(max(nums))" "
- **Espace**: «O(1)» auxiliaire

Expliquez que le facteur log vient de la recherche binaire de la réponse, pas du tableau.

---

##### Erreurs courantes et comment éviter Eux

(Utilisez la table "Bad"; mettez l'accent sur les erreurs hors-par-un, la manipulation incorrecte de l'adjacence.)

---

Cas de bord

(Summarize la table Ugly; fournir des contrôles rapides de la santé mentale pour les tailles de tableau minimales.)

---

#### Conseils d'entrevue

- ** Expliquez votre processus de pensée**: -I-I-M binaire recherche le montant maximum possible de vol parce que la réponse est monotonique. (en milliers de dollars)
- **Parlez du comptoir gourmand** : pourquoi on peut simplement compter des maisons plutôt que construire des états DP.
- **Mention la différence** du classique House Robber (DP avec deux états).

---

Conclusion

(Encourager les lecteurs à pratiquer des variations: par exemple, différentes règles d'adjacence, ou ajouter une contrainte sur le nombre total de maisons volées.)

---

Lecture supplémentaire

- Recherche binaire sur la réponse – <https://leetcode.com/articles/binary-search-on-réponse/>
- Greedy vs. DP - <https://www.geeksforgeeks.org/greedy-vs-dp/>

---

Mot final

En maîtrisant cette solution, vous aurez non seulement as House Robber IV, mais aussi un modèle solide pour un large éventail de questions d'entrevue. Bon codage, et bonne chance pour votre prochaine interview!

---

> **Mots clés**: *LeetCode 2560, House Robber IV, recherche binaire, algorithme gourmand, interview de codage, solution Java, solution Python, solution C++, espace constant, DP vs cupidy*

---

Clôture

Vous avez maintenant :

- Un algorithme ** clair et optimal**.
- **Code de rousseur** prêt pour LeetCode.
- Connaissance de **pitfalls** à éviter lors d'une entrevue.

N'hésitez pas à modifier les extraits de code pour correspondre à votre propre style de codage, mais la logique centrale tiendra toujours. Bonne chance ! C'est ce qu'il a dit.

---