---
titre: LeetCode 1191. K-Concaténation Somme maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# K-Concaténation Somme maximale – Solution complète en **Java, Python et C++**
> **LeetCode 1470** – *Somme maximale d'un tableau après K Reversals* (en fait K-concaténation)

---

TL;DR

Langage Durée Complexité Espace Complexité Code final Autres
-- -- -- -- -- -- -- -- -- -- -- -- -- --
*Java*** O(n)* O(1)* <details><sommaire> Afficher le code Java</résumé>...</détails> Autres
**Python**=O(n)=O(1)= <details><sommaire> Afficher le code Python</résumé>...</détails> Autres
**C++**= O(n)= O(1)= <details><sommaire> Afficher le code C++</résumé>...</détails> Autres

> **Réponse** – `maxSubarraySum(duplicatedArray)` quand `k==1`.
> Lorsque la somme totale de `arr` est négative, la réponse vient des deux premières concaténations.
> Lorsque la somme totale est positive, nous ajoutons `(k-2) * sum(arr)` à cette valeur.
> Enfin, appliquer `max(0, réponse) % 1_000_000_007`.

---

- Oui. Pourquoi cela importe

Pour toute entrevue de codage ou tout défi de programmation concurrentielle, obtenir l'algorithme *right* qui fonctionne dans le temps linéaire tout en gardant le code lisible est le bon endroit.
Ci-dessous vous trouverez:

1. Une solution ** propre, prête à la production** pour chaque langue.
2. A **blog post** qui plonge dans les aspects *good*, *bad* et *ugly* des solutions typiques.
3. Titres, en-têtes et utilisation des mots clés conviviaux pour que l'article se classe sur les moteurs de recherche pour la somme maximale de la concaténation et les requêtes connexes.

---

- Oui. 1. Le problème (Code Leet 1470)

> **K-Concaténation Somme maximale**
> Avec un tableau entier 1-D `arr` et un entier `k`, former un tableau en concatérant `arr` à lui-même `k` temps.
> Retournez la somme de sous-tarifs maximale possible dans ce nouveau tableau.
> La réponse doit être prise modulo `109 + 7`. Si la somme maximale est négative, retourner `0`.

Les contraintes sont grandes (l'arr) ≤ 105, k ≤ 105) – nous avons besoin d'un algorithme O(n), pas O(k·n).

---

- Oui. 2. L ' idée fondamentale (bonne)

- **L'algorithme de Kadanes** donne la somme sub-array maximale de n'importe quel tableau dans O(n).
- Lorsque nous concaténons deux copies de `arr` (`k==2`), le sous-array maximum peut franchir la frontière; nous avons besoin de Kadane sur un tableau de longueur‐`2·n`.
- Let `total = somme(arr)`.
* Si `total ≤ 0`, la meilleure somme ne peut pas être améliorée en ajoutant plus de copies, donc la réponse est juste le Kadane sur les deux premières copies.
* Si `total > 0`, la meilleure somme utilise une partie qui commence dans la *première* copie et se termine dans la *dernière* copie. Toutes les copies au milieu contribuent à la totalité du "total".
Par conséquent, pour `k>2` et `total>0`:

Texte
réponse = Kadane(arr dupliqué deux fois) + (k-2) * total
«» "

- Enfin, prendre `max(0, réponse) % MOD`.

C'est la solution O(n) **canonique** qui fonctionne dans un espace supplémentaire constant.

---

- Oui. 3. Code complet

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

kConcaténationMaxSum(int[] arr, int k) {
int n = longueur de l'arrond;
long total = 0;
pour (int v : arr) total += v;

// Kadane pour un seul exemplaire
long bestSingle = kadane(arr);

si (k) 1) retour (int)Math.max(meilleureSingle, 0);

// Kadane sur deux exemplaires (taille 2*n)
longue meilleure Deux = kadaneTwoCopies(arr);

si (total <= 0) {
retour (int)Math.max(meilleur Deux, 0) % (int)MOD;
}

long ans = meilleur Deux + (k - 2) * total;
as %= MOD;
retour (int)Math.max(ans, 0);
}

// Kadane standard, fonctionne sur n'importe quelle longueur de tableau
privé long kadane(int[]a) {
longue courbure = a[0], meilleure = a[0];
pour (int i = 1; i < a.longueur; i++) {
cur = Math.max(a[i], cur + [i]);
best = Math.max (best, cur);
}
le meilleur retour;
}

// Kadane sur arr concaténé deux fois (longueur 2*n)
Kadane privé long DeuxCopies(int[] arr) {
int n = longueur de l'arrond;
longue cour = arr[0], meilleure = arr[0];
pour (int i = 1; i < 2 * n; i++) {
valeur int = arr[i % n];
cur = Math.max (val, cur + val);
best = Math.max (best, cur);
}
le meilleur retour;
}
}
«» "

---

3.2 Python

'`python
MOD = 1 000 000 007

Solution de classe:
def kConcaténation MaxSum(self, arr, k: int) -> Int:
n = len(arr)
total = somme (arr)

def kadane(a):
cur = meilleur = a[0]
pour x dans a[1:]:
cur = max(x, cur + x)
best = max (meilleur, cur)
le meilleur retour

Si k == 1:
ans = kadane(arr)
retour max(ans, 0) % MOD

Kadane sur deux exemplaires
double = arr * 2
best_two = kadane(double)

si total <= 0:
retour max(meilleur_deux, 0) % MOD

ans = (meilleur_deux + (k - 2) * total) % MOD
retour max(ans, 0)
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;

int kConcaténationMaxSum(vecteur<int>& arr, int k) {
int n = arr.size();
long total = 0;
pour (int v : arr) total += v;

si (k == 1) retourner static_cast<int>(max(0LL, kadane(arr)) % MOD;

longue longue meilleure Deux = kadaneTwoCopies(arr);
si (total <= 0) retourner static_cast<int>(max(0LL, bestDeux)) % MOD;

long an = (meilleur deux + (k - 2) * total) % MOD;
retourner static_cast<int>(max(0LL, ans));
}

particulier:
long long kadane(vecteur const<int>& a) {
longue courbure longue = a[0], meilleure = a[0];
pour (size_t i = 1; i < a.size(); ++i) {
cur = max((long)a[i], cur + [i];
best = max (meilleur, cur);
}
le meilleur retour;
}

long long kadane TwoCopies(vecteur commun<int>& arr) {
vecteur <int> doubleArr(arr);
le nom de l'autorité compétente;
retour kadane(doubleArr);
}
};
«» "

---

- Oui. 4. Le blog

> **Titre**: *K-Concaténation Maximum Sum – Une plongée profonde dans des solutions bonnes, mauvaises et laides*
> **Description de Meta**: Découvrez comment résoudre LeetCode 1470 en Java, Python et C++. Comprendre l'algorithme de Kadane, gérer grand k, et éviter les pièges communs. Lisez le guide complet maintenant! (en milliers de dollars)

4.1 Introduction

Quand vous vous asseyez pour résoudre **LeetCode 1470 – K‐Concaténation Maximum Sum**, une vague d'erreurs courantes se lave souvent sur votre tête :

- Concaténer des copies "k" et faire fonctionner Kadane. (en milliers de dollars)
- Utiliser la programmation dynamique sur les états `k`. (en milliers de dollars)
- N'oubliez pas le modulo 1 000 000 007. (en milliers de dollars)

Chacune de ces approches peut conduire à des bogues *TLE*, *MLE*, ou même à des bogues entiers subtils. Dans cet article, nous disséquerons les *bonnes*, *mauvaises* et *meilleures* façons de résoudre le problème, fournirons un code prêt à la copie pour trois langues populaires et vous montrerons pourquoi la solution linéaire gagne à chaque fois.

---

4.2 Ce que le problème pose vraiment

> **K‐Concaténation** – créer un nouveau tableau en ajoutant `arr` à lui-même `k` times.
> **Objectif** – la somme maximale d'une sous-entente contiguë dans ce nouveau tableau, modulo `109 + 7`.
> **Edge cas** – si la somme maximale est négative, retourner `0`.

Les contraintes sont énormes (longueur arrière jusqu'à 105, k jusqu'à 105). Une solution O(k · n) naïve ne passera jamais.

---

### 4.3 Bon : la stratégie optimale basée sur Kadane

Étape Ce qu'il fait Pourquoi il fonctionne
- C'est quoi ?
**Kadane sur un seul exemplaire**= Donne la meilleure sous-tribu qui reste à l'intérieur d'un exemplaire. Classique linéaire-temps max-sub-array. Autres
**Kadane sur deux copies** Le seul endroit où une sous-tribu peut couvrir plus d'une copie est à la jonction. Autres
**Utilisez la somme totale**. Si `sum(arr) > 0`, chaque copie du milieu contribue à la totalité de sa somme à toute sous-entente transfrontalière. Autres Toutes les copies intérieures ajoutent `total` chacune; les deux autres copies traitent la partie traversée. Autres
**Formule** Deux + (k-2) * total` (lorsque `k>2` et `total>0`). Linéaire, espace constant. Autres
Autres **Modulo & clip final**="max(0, reply) % MOD`.=" Gère les réponses négatives et garde le résultat dans les limites. Autres

*La clé est de réaliser qu'après les deux premières copies, nous n'avons jamais besoin de matérialiser l'ensemble du tableau de longueur `k`. *

---

### 4.4 Mauvais: L'approche du duplicata

Une solution tentante mais *mauvaise* est:

'`python
double_arr = arr * 2
_arr = arr * k # O(k·n) mémoire!
ans = max_subarray(full_arr)
«» "

Problèmes:

1. ** Explosion de mémoire** – `k` peut être 105, ainsi `arr * k` peut être 1010 éléments.
2. **Bondage du temps** – Kadane exécuterait O(k·n).
3. **Overflow** – Les ints de Python sont bons, mais C++/Java peut déborder les ints 32 bits avant le modulo.

Pour ces raisons, cette approche échoue les tests de la plate-forme « Time Limit dépassé » ou « Memory Limit dépassé ».

---

### 4.5 Ugly: Mélange de préfixes/surfixes avec Kadane, mauvais modulo, manipulation négative

Le modèle **ugly** ressemble à :

"Java
long ans = kadaneTwoCopies(arr) + (k-2) * total;
ans = ans % MOD; // Faux! Doit faire modulo *après* clipping négatif
résultat int = (int)Math.max(0, ans);
«» "

Pourquoi c'est moche :

- **Ordre Modulo** – L'instruction LeetCode exige que vous appliquiez `max(0, réponse)` *avant* modulo. La formulation d'un nombre négatif maintient le signe négatif, qui viole la règle de retour 0 si négatif.
- **Overflow** – `total` peut être aussi grand que `105 * 109` → nécessite 64 bits entiers.
- **Readability** – Mélanger 3 variantes distinctes de Kadane dans le même fichier rend la logique difficile à vérifier.

---

4.6 Conseils de préparation à la production

Conseil Pourquoi
- Oui.
Autres Utiliser **long/64-bit** pour les sommes intermédiaires. Prévient le débordement avant d'appliquer le modulo. Autres
**Reuse Kadane** – écrivez un seul assistant qui peut accepter n'importe quel tableau. Conserve le code DRY et facile à tester. Autres
**Modulo seulement une fois** – après le calcul complet. Évite les appels inutiles `%` qui perdent du temps. Autres
**Appliquez à zéro tôt** – `max(0, réponse)` avant le modulo final. Simplifie la logique des cas négatifs. Autres
Rédigez des commentaires clairs qui expliquent les copies médianes à la fin de la période. Le code est à l'épreuve de l'avenir et rend l'examen par les pairs plus rapide. Autres

---

- Oui. 5. Pourquoi cet article vous aide à vous classer

- ** Densité des mots-clés**: somme maximale de la concaténation de K, algorithme de Kadane, solution de LeetCode 1470, solution de LeetCode, solution de LeetCode.
- **Traitements structurés (H2, H3)** pour les rampeurs SEO.
- **Meta tags** avec une description concise et un titre riche en mots clés.
- **Extraits de code** enveloppés dans `<details>` tags pour satisfaire les humains et les robots.

Avec ces optimisations, l'article apparaîtra près du haut de Google Résultats de recherche pour tout candidat à la recherche d'une solution propre LeetCode ou des conseils de préparation d'entrevue.

---

- Oui. 5. Résumé

1. La façon **optimale** de résoudre K‐Concaténation Maximum Sum est une seule passe Kadane plus une manipulation soigneuse des copies centrales lorsque la somme totale est positive.
2. Les trois implémentations linguistiques ci-dessus fonctionnent dans **O(n)** temps et **O(1)** espace supplémentaire.
3. Éviter les pièges **ugly**: ne jamais matérialiser toutes les copies `k`, toujours gérer modulo après couper des réponses négatives, et utiliser 64-bit entiers pour garder les sommes en sécurité.

Bon codage, et que vos sommes sub-array restent toujours du haut! Les