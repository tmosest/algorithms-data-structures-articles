---
titre: LeetCode 2913. Subarrays Élément distinct Somme des carrés Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2913 – Subarrays Élément distinct Somme des carrés
*Facile – LeetCode*

> **Problème**
> Compte tenu d'un nombre entier indexé à 0, un *subarray* est toute tranche contiguë non vide de "nums".
> Pour un subarray `nums[i..j]`, son **compte distinct** est le nombre de valeurs uniques qu'il contient.
> Retourner la somme des carrés des comptes distincts pour **all** sous-arrays de "nums".

Exemple Entrée Sortie Explication
C'est pas vrai.
"[1,2,1] """ "15"" "Six sous-arrays → '1^2+1^2+1^2+2+2^2+2^2 = 15'
"[1,1]""" "3"" Trois sous-groupes → "1^2+1^2+1^2 = 3""

> **Constraints**
> * `1 ≤ longueur nominale ≤ 100`
> * `1 ≤ nombres[i] ≤ 100`

Comme le tableau est minuscule, une approche O(n2) brute propre est parfaitement adéquate.
Ci-dessous vous trouverez **trois solutions complètes** (Java, Python, C++), suivi d'une analyse de style **blog** qui vous aidera à débarquer cet entretien d'ingénierie logicielle.

---

C'est pas vrai. Java – Simple Brute-Force

"Java
Importation de java.util.*;

solution de classe {
(Liste <entier> nombres) {
int n = nombres.size();
= 0;

// Pour chaque indice de départ possible
pour (int i = 0; i < n; i++) {
Définir<integer> vu = nouveau HashSet<>();

// Élargir le sous-réseau un élément à la fois
pour (int j = i; j < n; j++) {
voir.add(nums.get(j));
int distinct = vu.size();
Total += distinct * distinct; // carré le nombre distinct
}
}
le total des retours;
}
}
«» "

**Pourquoi ça marche* *

* La boucle extérieure prend une limite gauche `i`.
* La boucle intérieure étend la limite droite `j`.
* Un `HashSet` garde une trace des valeurs uniques vues jusqu'à présent – insérer est O(1).
* Pour chaque subarray, nous calculons `size2` et l'ajoutons à la réponse.

**Complexité* *

Valeur métrique
C'est pas vrai.
Temps (max. 10 000 itérations lorsque `n = 100`) Autres
Espace (l'ensemble ne contient jamais plus d'éléments `n`)

---

## 2--Python – Brute basée sur la liste Forcer

'`python
de taper l'importation Liste

def sum_counts(nums: List[int]) -> Int:
n = len(nums)
Total = 0

pour i dans la plage(n):
vu = set()
pour j dans la plage(i, n):
voir.add(nums[j])
Total += len(see) ** 2

retour total
«» "

La logique est identique à la version Java. Le paramètre "set" donne des insertions O(1) amorties.

**Complexité* *

* Heure: 'O(n2) "
* Espace: `O(1)`

---

## C++ – Vecteur & `unordered_set "

'`cpp
#incluez <vecteur>
#inclut <unordered_set>
utilisant l'espace de noms std;

nombre d'entrées(vecteurs<int> nombres) {
int n = nombres.size();
long long total = 0; // utiliser long pour éviter le débordement pour les entrées plus importantes

pour (int i = 0; i < n; ++i) {
non ordonné_set<int> vu;
pour (int j = i; j < n; ++j) {
voir.insérer(nums[j]);
int distinct = vu.size();
Total += 1LL * distinct * distinct;
}
}
retourner static_cast<int>(total);
}
«» "

*Note*: La déclaration LeetCode garantit que le résultat correspond à un entier signé 32 bits, mais l'utilisation de «long long» protège contre les débordements accidentels.

**Complexité* *

* Heure: 'O(n2) "
* Espace: `O(1)`

---

Article du blog – Le bon, le mauvais et le mauvais de LeetCode 2913

> **Titre:**
> *Cracking LeetCode 2913: Subarrays Elément distinct Somme des carrés – Une plongée profonde pour les ingénieurs qui cherchent du travail

> **Méta-Description (SEO):* *
> Découvrez comment résoudre LeetCode 2913 en Java, Python et C++. Comprendre les compromis algorithmiques, lire un tutoriel étape par étape et découvrir des idées prêtes à l'entrevue pour stimuler vos perspectives d'emploi.

---

Introduction

Dans une entrevue d'ingénierie logicielle, le but du recruteur n'est pas seulement de tester votre code – ils évaluent également votre état d'esprit de résolution de problèmes, style de codage et capacité de communiquer.
LeetCode 2913 est un problème classique d'array-and-hash-set, qui est **facile** en termes de difficulté mais **puissant** dans l'enseignement de concepts importants:

1. ** Force brute contre optimisation** – quand une solution naïve est-elle acceptable?
2. **Le choix de la structure des données** – pourquoi un jeu de hachage est parfait pour compter des éléments distincts.
3. ** Analyse de complexité** – pourquoi O(n2) est bon pour n ≤ 100 mais se briserait autrement.
4. ** nuances spécifiques à la langue** – Java="List<integer>` vs. Python="s `list`, C++="s `unordered_set`.

Nous décrivons ci-dessous les aspects *good*, *bad* et *ugly* des solutions typiques et comment les transformer en code gagnant en entrevue.

---

C'est vrai. Les bonnes

Qu'est-ce que les intervieweurs aiment ?
-- -- -- -- -- -- -- -- -- -- -- -- --
**Simplicité**= Une seule boucle imbriquée et un ensemble maintiennent le code court et lisible. Réduit la charge cognitive pour l'intervieweur de suivre votre logique. Autres
**Correctness**Utilisez directement la définition de "compte distinct" – pas de trucs cachés. Démontre une cartographie claire de l'énoncé de problème au code. Autres
**Le rendement pour les contraintes est ≤ 10 000 opérations. Montre que vous comprenez les limites du problème et que vous pouvez faire le bon compromis. Autres
**Language-Amis**Soit en Java, Python, C++ sans plaque de chaudière complexe. Vous donne de la flexibilité pour coder dans la langue avec laquelle vous êtes le plus à l'aise. Autres

> *Astuce:* Dans votre entrevue, commencez par l'approche de la force brute, puis demandez à l'intervieweur si vous êtes autorisé à optimiser – cela montre de l'humilité et de la volonté à itérer.

---

C'est vrai. Les mauvais

Question Conséquences Correction
- Oui.
** Mémoire excessive** – Utiliser un tableau de taille `n2` pour stocker tous les résultats subarray. Déchets RAM, inutile. Autres
**Integer Overflow** – La mise en quarantaine de comptes distincts pourrait déborder de 32 bits dans des langues avec des limites plus strictes. Utiliser 64 bits entiers ("long long" en C++, `long` en Java, `int` en Python est débordé). Autres
**Inefficient Set Reset** – La réallocation de l'ensemble dans chaque boucle externe peut être coûteuse en microbenchmarks. Un léger ralentissement. Réutiliser le même ensemble si vous le videz, mais avec n ≤ 100 l'avantage est négligeable. Autres
**Ignorer les contraintes de type** – Passer un `int[]` brut lorsque l'API s'attend à `List<Integer>` conduit à des erreurs de compilation. Le code ne compile pas. Correspond exactement à la signature (`Liste<Integer>`). Autres

> *Key takeaway:* Même les problèmes "easy" cachent de petits pièges; les attraper montre l'attention au détail.

---

C'est vrai. L'Ugly

Un problème Pourquoi il s'agit d'une meilleure pratique
- C'est quoi ?
**Numéros magiques codés par la main** – Utilisation de `n < 100` comme hypothèse cachée. Le code devient fragile si les contraintes changent. Dérivé `n` de `nums.size()`; éviter les nombres magiques. Autres
**Lack de documentation** – Pas de commentaires ou d'explications. Autres Ajouter de brefs commentaires ou une description de méthode. Autres
**Code non idiomatique** – Utiliser `pour (int i = 0; i < nums.size(); i++)` au lieu d'une foreach. Les fonctionnalités de langue manquantes, peuvent être plus lentes. Utiliser amélioré pour les boucles le cas échéant, mais pour les index vous aurez encore besoin d'eux. Autres
**Ignoring Edge Cases** – Pas de test pour "nums" étant vide (bien que les contraintes disent ≥ 1). Il montre des tests insouciants. Autres

> *Leçon :* Le code propre, bien commenté et « cas de bord » sépare un bon candidat d'un bon.

---

Comment parler de ce problème dans une entrevue

1. **Retrait le problème dans tes propres mots. **
Nous devons considérer chaque tranche contiguë du tableau, compter les nombres uniques à l'intérieur, carré qui comptent, et les ajouter tous ensemble.

2. ** Expliquez votre algorithme choisi. **
*=Nous allons parcourir chaque index de départ `i`, garder un ensemble de nombres vus en cours d'exécution pendant que nous élargissons l'index de fin `j`. Ajouter `set.size()2` à la réponse pour chaque extension.

3. ** Analyser la complexité. **
Avec `n ≤ 100`, la double boucle tourne ≤ 10 000 fois – parfaitement bien. Chaque insert est O(1), donc globalement O(n2). L'utilisation de la mémoire est O(1) en plus de l'ensemble.

4. **Discuse les optimisations potentielles (facultatif). **
Si `n` étaient plus grands, nous pourrions utiliser une fenêtre coulissante ou un tableau de fréquence de préfixe pour éviter de recalculer le jeu à partir de zéro.

5. **Cas de bord de Mention & débordement. **
Nous utilisons un entier 64 bits pour être en sécurité, et le jeu gère automatiquement les valeurs dupliquées.

---

Les pensées finales

- **Pratiquer le modèle.**
Compter des éléments distincts dans une fenêtre coulissante est une trompe d'interview récurrente – l'appliquer à des problèmes comme le plus long Substring avec At Most K Personnages Distincts () ou le subarray Distinct Count ().

- **Connais tes limites linguistiques. **
Le "HashSet" de Java est un wrapper autour d'une table de hachage, le "set" de Python est une table de hachage et le "unordered_set" de C++ est la même idée. Tous donnent O(1) amortisé insert/lookup.

- Gardez-le lisible. **
Les intervieweurs lisent le code plus vite qu'ils le déboguent. Utilisez des noms de variables significatifs (`i`, `j`, `seen`, `distinct`, `total`) et évitez toute abstraction inutile.

- **Préparer quelques cas d'essai** (bord, typique, grand).
*`[1]`, `[1,2,3,4]`, `[1,1,1]`, `[100,99,100]`* - démontrer que vous comprenez comment les comptes distincts changent.

- **Show curiosité.**
Demandez si l'intervieweur veut une solution plus efficace ou si vous voulez discuter comment vous avez géré un `n` de 105. Même si c'est impossible avec l'approche naïve, expliquer le goulot d'étranglement montre que vous pensez à l'évolutivité.

---

Prêt à décrocher ce job ?

1. **Copier le code** dans votre IDE favori et exécuter les tests LeetCode.
2. **Ajouter un court bloc de commentaires** expliquant l'approche – cela sera superbe dans votre GitHub README.
3. **Blog it up** (comme la section ci-dessus) – utiliser des mots-clés: *=LeetCode 2913 solution==,==l'élément distinct===,==l'algorithme de jeu de hash===,==l'entretien d'un emploi==.
4. **Partager** le poste dans les communautés technologiques, LinkedIn, ou votre portefeuille. Les recruteurs regardent souvent vos échantillons d'écriture.

Avec une implémentation propre en **Java, Python et C++**, une interview solide à travers, et un billet de blog poli, vous vous démarquez en tant que candidat qui non seulement résout le problème mais aussi le communique clairement. Bonne chance ! C'est ce qu'il a dit.

---


*© 2024 Engineering Interview Insights* – Tous droits réservés.

---

*Sentez libre d'adapter l'article pour votre propre voix ou développez sur les optimisations si vous voulez présenter des compétences algorithmiques plus profondes. *