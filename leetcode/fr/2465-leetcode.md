---
titre: LeetCode 2465. Nombre de moyennes distinctes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2465 – Nombre de moyennes distinctes
1 ms (Java)* *
<https://leetcode.com/problèmes/nombre de moyennes distinctes/>

---

Ce que vous apprendrez

Pourquoi ça compte ?
- Oui.
**Trier + Two-Pointer**
**HashSet pour unicité**
**Déaler avec un point flottant**
**Analyse de la complexité du temps et de l'espace**
**Mise en œuvre en langage brut**

---

Résumé du problème

Compte tenu d'un tableau **de longueur égale** «nums» (2 ≤ «nums.length» ≤ 100, chaque élément 0–100),

1. Supprimer le nombre le plus petit*
2. Supprimer le nombre *le plus grand*
3. Calculer leur moyenne `(a + b) / 2`

Retourner le nombre ** de moyennes distinctes** produites.

> Exemple
> `nums = [4,1,4,0,35]` → moyennes: 2.5, 2.5, 3.5 → réponse `2`.

---

Intuition

Le processus est déterministe jusqu'aux liens (toute min/max peut être choisi).
Si nous **sort** le tableau, les plus petits et les plus grands sont simplement `nums[0]` et `nums[n‐1]`.
Après les avoir jumelés, nous pouvons simplement nous déplacer vers l'intérieur: `l++` et `r--`.
Chaque paire donne une moyenne; nous avons juste besoin de compter combien **unique** moyennes nous obtenons.

---

## , , Brute- Force vs Optimal

L'approche Temps L'espace Commentaires
C'est pas vrai.
Autres Enlever min/max d'un multiset à chaque étape (pap, liste) Autres
**Sort + deux pointeurs + jeu de hachage** **O(n log n)** Autres

---

Mise en œuvre

Voici des solutions propres et autonomes dans **Java**, **Python** et **C++**.
Tous les trois utilisent la même idée algorithmique.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
secteur public Moyennes {
// 1. Tri pour apporter min & max aux extrémités
Tableaux.sort(nums);

// 2. Utilisez un HashSet pour garder des moyennes uniques
Set<Double> set = nouveau HashSet<>();

int l = 0, r = longueur nominale - 1;
pendant que (l < r) {
// Double est fin – les valeurs sont au plus 100, la moyenne se termine en 0 ou .5
double avg = (nums[l] + nombres[r]) / 2.0;
l'ensemble.add(avg);
l++;
R--;
}
retour set.size();
}
}
«» "

> **Pourquoi `double`?**
> Avec les limites données, la somme est ≤ 200 et la division par 2 donne soit un entier soit une décimale .5.
> La précision du double est bien au-delà de cela, il n'y a donc aucun risque de collision entre deux moyennes distinctes.

---

Python

'`python
Solution de classe:
def distinct Moyennes (soi-même, nombres : Liste[int]) -> Int:
nombres.sort()
vu = set()
l, r = 0, len(nums) - 1
alors que l < r:
avg = (nums[l] + nombres[r]) / 2,0
Voir.add(avg)
l += 1
r -= 1
retour len(see)
«» "

> **`set`** en Python est un hash‐set avec des inserts O(1) amortis.
> Le code suit le même schéma de deux points.

---

C++

'`cpp
solution de classe {
public:
Int distinct Moyennes(vecteur<int> et nombres) {
(noms.begin(), nums.end());
non ordonné_set<double> vu;
pour (int l = 0, r = nombres.size() - 1; l < r; ++l, --r) {
double avg = (nums[l] + nombres[r]) / 2.0;
voir.insérer(avg);
}
retour vu.size();
}
};
«» "

> **`unordered_set`** donne O(1) moyen insert/lookup.
> Utiliser `double` est sûr pour la même raison que Java.

---

Analyse de complexité

Étape Coût Explication
C'est pas vrai.
Classer `nums`. **O(n log n)**
Une passe, un travail constant
Les opérations HashSet sont en moyenne O(1)

**Total:** "O(n log n)" temps, "O(n)" espace.

Avec `n` ≤ 100, toutes les solutions fonctionnent en millisecondes (< 5 ms en pratique).

---

Cas et pièges

Numéro Comment éviter
C'est pas vrai.
**Égalité des points flottants**= Toutes les moyennes sont des multiples exacts de 0,5; la comparaison "double" est sûre. Autres
**Astuces pour min/max**= Tout choix fonctionne; le tri résout de façon déterministe. Autres
**Rayau d'empty**= Le problème garantit une longueur égale ≥ 2, donc pas besoin de manipulation spéciale. Autres
**Les plus grandes valeurs**=Les contraintes assurent `int` + `int` s'adapte en 32 bits. Autres
**Utilisation de la mémoire**= `HashSet` tient au plus des éléments `n/2`, minuscule pour des limites données. Autres

---

La partie "Ugly"

- Oui. Si vous avez essayé de garder le tableau comme un multiset et plusieurs fois `pollFirst()` / `pollLast()` en utilisant un `TreeSet`, vous aurez une opération **log n** pour chaque paire – *still* acceptable pour 100 éléments, mais complexité inutile.
- L'utilisation d'un "double" dans un "HashSet" peut être risquée dans d'autres contextes (par exemple, avec de grands nombres ou de nombreuses décimales). Ici, le petit domaine garantit la sécurité.
- Certains intervieweurs s'attendent à ce que vous réalisiez le modèle **deux-pointeurs** **avant** vous écrivez du code. Faire passer ce point de vue peut entraîner une suringénierie.

---

Les bonnes choses

- **Simplicité** – Tri une fois, boucle une fois, réglé une fois.
- **Déterministe** – Pas de hasard; facile à tester.
- **Scalable** – Fonctionne pour des tableaux beaucoup plus grands si les contraintes augmentent.

---

Liste de contrôle à emporter

- [ ] Triez le tableau.
- [ ] Paire les éléments des deux extrémités (`l` et `r`).
- [ ] Calculer la moyenne en «double» (ou «float»).
- [ ] Stocker dans un hachage pour conserver des objets uniques.
- [ ] Retourne la taille de l'ensemble.

---

Article de blog optimisé (en entier)

> **Titre**: *=Nombre de moyennes distinctes (Code Leet 2465) – Java, Python, C++ Solutions + Conseils d'entrevue*
> **Moyenne Description**: *Solve LeetCode 2465 Nombre de moyennes distinctes en Java, Python et C++. Apprenez l'astuce à deux pointeurs, l'utilisation de hachage, et comment aser ce problème d'entrevue. *
> **Tags**: #LeetCode #Algorithme #TwoPointers #HashSet #InterviewPrep #Java #Python #C++

---

Introduction

Le problème « Nombre de moyennes distinctes » est un défi trompeur de LeetCode qui teste votre compréhension du tri, de la technique à deux points et du hachage. Dans cet article nous allons parcourir le problème, l'intuition derrière la solution optimale, fournir un code propre en **Java, Python, et C++**, analyser sa complexité, et discuter des pièges communs – tout en gardant l'article SEO-friendly pour vous aider à atterrir cette interview d'emploi.

---

Récapitulation du problème

> **Objectif** : Retirez le minimum et le maximum d'un tableau d'une longueur égale à plusieurs reprises, calculez la moyenne de chaque paire et calculez le nombre de moyennes distinctes produites.

**Contrôles* *

- "2 ≤ longueur nominale ≤ 100", même
- `0 ≤ nombres[i] ≤ 100`

---

- Oui. La stratégie optimale

1. **Trier le tableau.
Maintenant le plus petit est à l'index `0`, le plus grand à l'index `n‐1`.
2. Utilisez deux pointeurs (`l` au début, `r` à la fin).
Chaque étape:
- Calculer `(nums[l] + nombres[r]) / 2.0`.
- Insérez dans un hachage.
- Déplacez `l++`, `r--`.
3. Après la boucle, la taille du jeu de hachage est la réponse.

Pourquoi est-ce optimal ?
Parce que chaque paire est indépendante; le tri place chaque paire min/max en positions fixes, éliminant le besoin de structures de données coûteuses comme les files d'attente prioritaires. L'ensemble de hachage garantit l'unicité dans le temps prévu O(1).

---

Mise en œuvre du code

Code extrait Autres
C'est pas vrai.
* <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><><br><><br><><><br><><>><>><> Moyennes(int[] nombres) {<br> Arrays.sort(nums);<br> Set<Double> set = nouveau HashSet<>();<br> pour (int l = 0, r = nombres.longueur - 1; l < r; ++l, --r) {<br> double avg = (nums[l] + nombres[r]) / 2.0;<br> set.add(avg);<br> }<br> retour set.size();<br> }<br>}<br>``</details> Autres
**Python**= <details><sommaire>Cliquez pour afficher</sommaire><br>``python<br>class Solution:<br>def distinct Moyennes(self, nombres: List[int]) -> int:<br> nombres.sort()<br> vu = set()<br> l, r = 0, len(nums) - 1<br> tandis que l < r:<br> vu.add(nums[l] + nombres[r]) / 2.0)<br> l += 1<br> r -= 1<br> retour len(seen)<br>``</details> Autres
**C++**= <details><sommary>Cliquez pour afficher</sommary><br>``cpp<br>class Solution {<br>public:<br> int distinctAverages(vector<int>& nums) {<br> tri(nums.begin(), nums.end());<br> unordered_set<double> vu;<br> pour (int l = 0, r = nums.size() - 1; l < r; ++l, --r) {<br> vu.insert((nums[l] + nums[r]) / 2.0);<br><br><br> retour vu.s();<br>}<br>}<br>};<br>`</details> Autres

> **Astuce**: Dans les langues qui le supportent, vous pouvez également utiliser un `pair<int, int>` comme clé au lieu d'un `double` pour éviter toute préoccupation de point flottant.

---

Complexité

- **Heure**: `O(n log n)` (le tri domine).
- **Espace**: `O(n)` (hash set tient à la plupart des moyennes `n/2`).

---

Cas de bord et erreurs courantes

Erreur
- Oui.
Utiliser un `TreeSet` et enlever min/max via `pollFirst()/pollLast()` Triez une fois + deux pointeurs (bien plus simple). Autres
Autres Oublier de diviser par `2.0` (division entière)= Utiliser `double` ou lancer pour doubler. Autres
Enregistrer les moyennes dans un `int` ou `float` qui ne peuvent pas représenter `.5` précisément. Autres
Autres Le tri donne une réponse déterministe ; tout choix de cravate est parfait. Autres

---

- Oui. La discussion sur le bien et le bien

- **Bien**: La solution est concise, fonctionne instantanément même sur la limite supérieure, et démontre clairement la pensée algorithmique.
- **Ugly**: La sur-ingénierie (en files d'attente prioritaires, en tas personnalisé) distrait la vision à deux points de base. Dans les entrevues, mettre en valeur les idées avant le code.

---

### Conseils d'entrevue

1. **Exposer l'approche à deux points avant le codage** – montre que vous comprenez le modèle sous-jacent.
2. **Mention l'ensemble de hachage de la garantie d'unicité** – les intervieweurs apprécient la compréhension des structures de données.
3. **Montrer la confiance avec la sécurité des points flottants** – clarifier pourquoi "double" est bien compte tenu des contraintes.
4. **Discuss scalability** – si les contraintes ont augmenté à `10^5`, l'approche fonctionne encore (le tri reste O(n log n)).

---

Pensées de clôture

LeetCode 2465 est un excellent exemple de la façon dont une stratégie algorithmique claire (sort + deux pointeurs + jeu de hachage) bat des solutions de structure de données plus complexes. En maîtrisant cette astuce, vous serez prêt à résoudre des problèmes similaires basés sur la paire dans les interviews, et vous aurez un code propre, prêt à la production en Java, Python ou C++.

> **Vous voulez plus de LeetCode ?** Abonnez-vous à notre newsletter pour des analyses de problèmes hebdomadaires et des conseils de préparation d'entrevue.

---

### Appel à l'action

- **Commentaire** votre langue préférée ou un tour que vous avez utilisé.
- **Partager** cet article sur Linked Dans ou Twitter – aidez les autres à apprendre et à grandir!

---

FAQ

Question Réponse
C'est pas vrai.
*La division entière affecte-t-elle le résultat?*= Oui, `(nums[l] + nums[r]) / 2` produirait-elle un entier. Utilisez toujours `2.0` ou jetez sur `double`. Autres
*Puis-je utiliser `int` pour la clé de hachage? *= Étant donné que les sommes sont ≤ 200, vous pouvez stocker la somme *caled* (`nums[l] + nums[r]`) dans un `int` et diviser par la suite lors du retour du résultat. Autres
*Est-ce que l'algorithme est stable? * Le tri est stable, mais pas nécessaire. Deux pointeurs produisent une paire déterministe. Autres

---

### Envelopper

Le problème du nombre de moyennes distinctes est une vitrine parfaite de la façon dont une bonne compréhension des algorithmes de base – tri, bipointer traversal et hachage – peut résoudre efficacement les vraies questions d'entrevue. Armé des extraits de code ci-dessus et d'une compréhension claire de la raison pour laquelle ils fonctionnent, vous serez prêt à expliquer, mettre en œuvre et discuter de ce défi avec confiance. Bonne chance pour votre prochain entretien !

---

> **Note**: Cet article est long de 1500+ mots, utilise la hiérarchie de cap, les points de puce, et les blocs de code pour améliorer la lisibilité et la performance SEO.

---

Les pensées finales

Le défi de LeetCode : Nombre de moyennes distinctes est un problème concis mais puissant. Maîtriser la solution à deux points plus hachage démontre votre maturité algorithmique et votre capacité à écrire un code propre et trans-langue, un savoir-faire que les intervieweurs aiment. Gardez cette liste de contrôle à portée de main, pratiquez sur vos propres ensembles de données, et soyez confiant dans cette prochaine entrevue!

---

Bon codage, et bonne chance pour votre recherche d'emploi!