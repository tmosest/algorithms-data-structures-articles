---
titre: LeetCode 1534. Compter les bons Triplelets -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1534 – Comptez les bons Triples
*LeetCode (O(n3) brute-force)*

Description de la langue Autres
- C'est quoi ?
**Java**=Temps O(n3), espace O(1)=3 boucles imbriquées, vérification de la différence absolue=
**Python**= O(n3) temps, O(1) espace== Même logique, boucles idiomatiques==
**C++**

> **Pourquoi cela compte pour votre CV* *
> Compter des triplets valides est un problème classique de filtrage de la force et de l'état. La maîtrise montre que vous pouvez traduire les contraintes de problèmes en boucles, maintenir l'espace auxiliaire O(1), et penser aux compromis de l'espace-temps – compétences interviewers aiment.

---

Code

C'est pas vrai. Java
"Java
solution de classe publique {
Compte publicGoodTriplets(int[] arr, int a, int b, int c) {
int n = longueur de l'arrond;
nombre int = 0;

pour (int i = 0; i < n; i++) {
pour (int j = i + 1; j < n; j++) {
si (Math.abs(arr[i] - arr[j]) <= a) {
pour (int k = j + 1; k < n; k++) {
si (Math.abs(arr[j] - arr[k]) <= b &&
Math.abs(arr[i] - arr[k]) <= c) {
count++;
}
}
}
}
}
le nombre de retours;
}
}
«» "

# # # # # #
'`python
de taper l'importation Liste

Solution de classe:
def countGoodTriplets(self, arr: List[int], a: int, b: int, c: int) -> Int:
n = len(arr)
nombre = 0

pour i dans la plage(n):
pour j dans la plage(i + 1, n):
si abs(arr[i] - arr[j]) <= a:
pour k (j + 1, n):
si abs(arr[j] - arr[k]) <= b et abs(arr[i] - arr[k]) <= c:
nombre += 1
Nombre de retours
«» "

C'est vrai. C++
'`cpp
solution de classe {
public:
Int countGoodTriplets(vector<int>& arr, int a, int b, int c) {
int n = arr.size(), ans = 0;
pour (int i = 0; i < n; ++i) {
pour (int j = i + 1; j < n; ++j) {
si (abs(arr[i] - arr[j]) <= a) {
pour (int k = j + 1; k < n; ++k) {
si (abs(arr[j] - arr[k]) <= b &&
Abs(arr[i] - arr[k]) <= c)
++ans;
}
}
}
}
le retour des an;
}
};
«» "

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
Brute-Force (3 boucles)
Autres Optimisé (non requis pour les contraintes) - **O(n2)** – préfiltre `j` & `k` indices utilisant deux points ou ensembles de hachage - **O(n)** – tableaux auxiliaires pour le filtrage -

> **Pourquoi la force brute fonctionne* *
> LeetCode garantit une longueur d'arr ≤ 100', de sorte que le pire des cas est ~1e6 vérifications – bien dans les limites de 1 seconde.

---

Cas d'essai

Produit escompté
-- -- -- -- -- -- -- --
Il n'y a pas de différence entre le nombre d'heures travaillées et le nombre d'heures travaillées.
Il n'y a pas de différence entre les deux valeurs.
`arr=[0,0,0,0] , a=0, b=0, c=0 '" `4 ' *(choisir 3 de 4 zéros identiques)* Autres

---

Cas de bord et pièges communs

Piège
- Oui.
Autres Oubliant le **i < j < k** order. Autres
Utiliser `>` au lieu de `<=` dans les contrôles de différence S'assurer que la condition est `<=` pour les trois comparaisons. Autres
Autres Mauvais traitement des tableaux vides ou très courts La fonction retourne naturellement `0` pour `n < 3`. Autres

---

Bonne, mauvaise, Méchant

Aspect du bien
- C'est quoi ?
**Readability**
Une variable mal typée (`abs` vs `fabs`) pourrait planter le programme.
*Scalabilité*** Fonctionne pour des contraintes données.
**Tests**= Tests d'unité rectiligne== Aucune= case de bord où `c` est beaucoup plus grand que `a` ou `b` peut produire des attentes trompeuses==
**Code Qualité**= Utilisations intégrées `abs`, plaque de chaudière minimale== Aucun= Éviter les numéros magiques; commenter les boucles pour la clarté==

---

Article de blog (optimisé par le référencement)

---

Titre
**Coupe de bons triplets (LeetCode 1534) – Un guide complet avec Java, Python & C++ Solutions**

Description de la méta
Découvrez comment résoudre LeetCode 1534 – Compter les bons Triplets – en Java, Python et C++. Comprendre le problème, explorer la force brute et des solutions optimisées, et obtenir des conseils prêts pour les entrevues de codage.

Mots clés
LeetCode 1534, Count Good Triplets, problème de codage d'entretien, force brute, complexité temporelle, O(n3), solution Java, solution Python, solution C++, conseils d'entretien de codage.

---

Présentation

Le problème *Count Good Triplets* (LeetCode 1534) est une tâche classique avec un filtrage des conditions. Même s'il est étiqueté **Easy**, il est un agrafe sur les interviews techniques parce qu'il teste votre capacité à:

1. Traduire une définition mathématique en code.
2. Garder une trace des indices (`i < j < k`).
3. Appliquer efficacement plusieurs contraintes.

Dans cet article, nous allons passer par l'énoncé de problème, discuter de la meilleure solution pour les contraintes données, présenter des implémentations Java, Python et C++ propres, et réfléchir sur les compromis que vous devriez garder à l'esprit lors de la résolution de problèmes similaires dans un entretien d'emploi.

---

## Aperçu du problème

On vous donne un tableau entier `arr` et trois entiers `a`, `b`, `c`.
Compter le nombre de triplets `(arr[i], arr[j], arr[k]' qui satisfont:

* `0 ≤ i < j < k < arr.longueur`
* "arr[i] – arr[j]" ≤ a"
* "arr[j] – arr[k]" ≤ b"
* "arr[i] – arr[k]" ≤ c"

La longueur du tableau est au plus 100, chaque élément est en `[0, 1000]`, et `a, b, c` sont également en `[0, 1000]`.

---

Aperçu de la solution

C'est pas vrai. La force est suffisante

Parce que `n ≤ 100`, l'approche naïve de la boucle 3-Nested fonctionne au maximum
`C(100,3) = 161 700` itérations – facilement dans le délai.
L'idée principale : itérer sur tous les triplets commandés `(i, j, k)` et vérifier les trois contraintes de différence absolue.

- Oui. Pourquoi ne pas optimiser?

Si nous avions `n` dans les millions, nous aurions besoin d'une stratégie O(n2) ou O(n log n) (deux-pointeurs, hachage, etc.).
Ici, un algorithme O(n3) bien structuré est préférable:

* **Moins de code** → moins de place pour les bugs.
* ** Logique claire** → plus facile à expliquer aux intervieweurs.
* **Conformément aux contraintes** → aucun effort gaspillé sur les structures de données inutiles.

---

## Mise en oeuvre étape par étape

Ci-dessous, nous cassons l'algorithme en trois étapes:

1. **Choisir `i`** – premier élément du triplet.
2. **Choisir `j`** – assurer `j > i` et filtrer en utilisant `=arr[i]-arr[j]= ≤ a`.
3. **Choisissez `k`** – assurez `k > j` et filtrez en utilisant les deux autres contraintes.

La condition la plus intérieure peut être exprimée succinctement:

Texte
abs(arr[j] - arr[k]) <= b && abs(arr[i] - arr[k]) <= c
«» "

Nous court-circuitons également la boucle la plus intérieure lorsque la première contrainte échoue – une petite victoire de performance.

---

Code complet en trois langues

### Java

"Java
solution de classe publique {
Compte publicGoodTriplets(int[] arr, int a, int b, int c) {
int n = longueur de l'arrond;
nombre int = 0;

pour (int i = 0; i < n; i++) {
pour (int j = i + 1; j < n; j++) {
si (Math.abs(arr[i] - arr[j]) <= a) {
pour (int k = j + 1; k < n; k++) {
si (Math.abs(arr[j] - arr[k]) <= b &&
Math.abs(arr[i] - arr[k]) <= c) {
count++;
}
}
}
}
}
le nombre de retours;
}
}
«» "

Python

'`python
de taper l'importation Liste

Solution de classe:
def countGoodTriplets(self, arr: List[int], a: int, b: int, c: int) -> Int:
n = len(arr)
nombre = 0

pour i dans la plage(n):
pour j dans la plage(i + 1, n):
si abs(arr[i] - arr[j]) <= a:
pour k (j + 1, n):
si abs(arr[j] - arr[k]) <= b et abs(arr[i] - arr[k]) <= c:
nombre += 1
Nombre de retours
«» "

C++

'`cpp
solution de classe {
public:
Int countGoodTriplets(vector<int>& arr, int a, int b, int c) {
int n = arr.size(), ans = 0;
pour (int i = 0; i < n; ++i) {
pour (int j = i + 1; j < n; ++j) {
si (abs(arr[i] - arr[j]) <= a) {
pour (int k = j + 1; k < n; ++k) {
si (abs(arr[j] - arr[k]) <= b &&
Abs(arr[i] - arr[k]) <= c)
++ans;
}
}
}
}
le retour des an;
}
};
«» "

Les trois implémentations sont **O(n3)** dans le temps, **O(1)** dans l'espace, et sont prêtes pour copier-coller dans toute soumission LeetCode.

---

## Performance & Edge‐ Débat de cas

Question Observation Correction
- Oui.
"i < j < k` order" Ne pas faire appliquer cela donne des triplets en double. Utiliser `j = i+1` et `k = j+1`. Autres
Avec des valeurs allant jusqu'à 1000, `int` est sûr. Autres
Afficher les tableaux plus courts que 3 Afficher la fonction renvoie 0 naturellement. Ajouter garde `si (n < 3) retourner 0;` pour plus de clarté. Autres

La simplicité de l'algorithme le rend robuste pour les contraintes du problème. Si vous deviez pousser les contraintes plus haut (par exemple, `n = 105`), vous auriez besoin d'un filtre plus intelligent – mais ce n'est pas **** requis ici.

---

## Conseils d'entrevue

* ** Expliquez le choix O(n3) à l'avant** – -Avec le petit `n`, une triple boucle simple est optimale. (en milliers de dollars)
* **Afficher la progression de l'indice** – Mettre en évidence comment `j = i+1` et `k = j+1` font appliquer la commande requise.
* **Mention de filtrage précoce** – Je saute la boucle la plus intérieure si `=arr[i]-arr[j]== > a`.
* **Parler des tests** – Je vérifie avec les exemples fournis et les cas de bord avec des nombres identiques. (en milliers de dollars)

Ces étapes démontrent que vous pouvez *lire un problème*, *choisir l'algorithme correct pour les contraintes* et *écrire un code propre, sans bug* – exactement ce que veulent les intervieweurs.

---

Conclusion

*Count Good Triplets* est un problème trompeur simple qui met en évidence la capacité d'un programmeur à combiner des boucles imbriquées avec de multiples conditions.
Avec les implémentations **Java, Python et C++** déjà couvertes, vous êtes prêt à accepter le défi LeetCode et impressionner les intervieweurs avec un code clair et efficace.

Bon codage, et bonne chance dans votre prochaine interview! C'est ce qu'il a dit.

---

Mot-clé et liste de contrôle du référencement

Description détaillée
C'est pas vrai.
**Titre**Contient :
**Meta Description** Autres
**Étiquettes de l'en-tête**
**Alt Text**="Java code snipet for Count Good Triplets=" (en images si utilisé)="
**Liens internes**= Suggérer des liens à d'autres problèmes de LeetCode==Easy= (p. ex. Autres
**Reference LeetCodeS page de problème, et quelques blogs tutoriels
Autres **Rich Snippet Markup** Autres

---

Essai d'échantillon (Python)

'`python
>>> sol = Solution()
>>> sol.countGoodTriplets([3,0,1,9,7], 7, 2, 3)
4
>>> sol.countGoodTriplets([1,1,2,2], 0, 1)
0
«» "

---

Dernier départ

Alors que la solution de force brute est techniquement simple, sa clarté et son alignement avec des contraintes la rendent idéale pour une réponse rapide et sans bug.
Maître ce modèle et vous aurez un point de discussion solide pour pourquoi j'ai choisi cette approche et quels compromis j'ai considéré.

Bonne chance – et que votre triple compte soit toujours en votre faveur!