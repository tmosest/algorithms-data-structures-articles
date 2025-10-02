---
titre: LeetCode 1414. Trouvez le nombre minimum de nombres de Fibonacci dont la somme est K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1414

> **Trouver le nombre minimum de numéros de Fibonacci dont la somme C'est K**
> Compte tenu d'un entier `k` (1 ≤ k ≤ 109), retourner le plus petit nombre de nombres de Fibonacci qui se résument à `k`.
> Le même nombre de Fibonacci peut être utilisé plusieurs fois.

La séquence Fibonacci commence par
`F1 = 1`, `F2 = 1`, `Fn = Fn−1 + Fn−2` pour `n > 2`.

> Exemple
> `k = 7 → 5 + 2 → 2 numéros Fibonacci "

> **Pourquoi est-ce intéressant? **
> C'est un problème classique. La stratégie optimale est de continuer à soustraire le plus grand nombre de Fibonacci qui ne dépasse pas le «k» restant.
> C'est aussi une excellente question d'entrevue parce qu'elle teste :
> * intuition numérique
> * Algorithmes gourmands
> * manutention de gros entiers (jusqu'à 109)

Ci-dessous vous trouverez des implémentations de travail dans **Java, Python, et C++** ainsi qu'un blog-style à travers les aspects de bon, mauvais et laid du problème.

---

- Oui. 2. Les trois solutions

#### 2.1 Java – 100 % rapide et efficace en mémoire

"Java
// 1414. Trouvez le nombre minimum de nombres de Fibonacci dont la somme Est K
// Java 17

Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
public int findMinFibonacciNumbers(int k) {
// Étape 1: générer tous les nombres de Fibonacci <= k
Liste <entier> fibs = nouvelle liste d'array<>();
fibs.add(1); // F1
fibs.add(1); F2
alors que (vrai) {
int sz = fibs.size();
int next = fibs.get(sz - 1) + fibs.get(sz - 2);
si (suivant > k) pause;
fibs.add(suivant);
}

// Étape 2: soustraction gourmande
nombre int = 0;
pour (int i = fibs.size() - 1; i >= 0 && k > 0; i--) {
pendant que (k >= fibs.get(i)) {
k -= fibs.get(i);
count++;
}
}
le nombre de retours;
}

// Main simple pour des tests manuels rapides
public statique vide principal(String[] args) {
System.out.println(nouvelle solution().findMinFibonacciNumbers(7)); // 2
System.out.println(nouvelle solution().findMinFibonacciNumbers(10)); // 2
System.out.println(nouvelle solution().findMinFibonacciNumbers(19)); // 3
}
}
«» "

> **Pourquoi c'est bon* *
> * « O(F) » heure où « F » est le nombre de nombres de Fibonacci ≤ k (= 44 pour k ≤ 109).
> * Mémoire `O(F)` – trivial pour les machines modernes.
> * itératif – pas de soucis de profondeur de récursion.

> **Quoi faire attention**
> * Ne **pas** utiliser la récursion; elle peut causer le débordement de la pile pour grand k.
> * Évitez de générer des nombres de Fibonacci plus grands que `k` – le garde de boucle fait cela.

---

2.2 Python – Concise et lisible

'`python
# 1414. Trouvez le nombre minimum de nombres de Fibonacci dont la somme Est K
# Python 3.11

def findMinFibonacciNumbers(k: int) -> Int:
# générer des fibs <= k
Fibs = [1, 1]
pendant que fibs[-1] + fibs[-2] <= k:
fibs.append(fibs[-1] + fibs[-2])

nombre = 0
# Cupidité du plus grand au plus petit
pour f en marche arrière (fig.):
alors que k >= f:
k -= f
nombre += 1
Nombre de retours

# tests rapides
si __nom__ == "__main__" :
print(findMinFibonacciNombres(7)) # 2
print(findMinFibonacciNumbers(10)) # 2
print(findMinFibonacciNumbers(19)) # 3
«» "

> **Pourquoi c'est bon* *
> * Boucle à deux lignes pour construire des numéros Fibonacci – pas de magie.
> * `O(1)` mémoire supplémentaire (liste de 44 int maximum).
> * Boucle intuitive gourmande avec `reversed()` – parfait pour l'interview narrative.

> **Quoi faire attention**
> * La profondeur de récursion de Python est un danger ; ne jamais récidiver pour ce problème.
> * Gardez le générateur Fibonacci à l'intérieur du garde-boucle – il s'arrête à `k`.

---

### 2.3 C++ – Rapide, moderne et compilé en 2023

'`cpp
// 1414. Trouvez le nombre minimum de nombres de Fibonacci dont la somme Est K
// C++17 (ou ultérieure)

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int findMinFibonacciNumbers(int k) {
// Construisez tous les numéros de Fibonacci <= k
vecteur<int> fib{1, 1};
alors que (vrai) {
int next = fib[fib.size() - 1] + fib[fib.size() - 2];
si (suivant > k) pause;
fib.push_back(suivant);
}

// Soustraction d'avidité
nombre int = 0;
pour (int i = (int)fib.size() - 1; i >= 0 && k > 0; --i) {
pendant que (k >= fib[i]) {
k -= fib[i];
+ nombre;
}
}
le nombre de retours;
}
};

// Démo rapide
Int main() {
Solution s;
<< s.findMinFibonacciNumbers(7) << enl; // 2
<< s.findMinFibonacciNumbers(10) << enl; // 2
Cout << s.findMinFibonacciNumbers(19) << enl; // 3
}
«» "

> **Pourquoi c'est bon* *
> * Utilise `vector<int>` – pas de gestion manuelle de la mémoire.
> * `O(F)` temps et espace, identique à Java & Python.
> * Compilation rapide; pas de récursion.

> **Quoi faire attention**
> * Méfiez-vous du débordement entier: `int` est bien parce que les nombres de Fibonacci ≤ 109 s'inscrivent dans 32-bit.
> * Gardez toujours la boucle avec `k > 0` – empêche une boucle infinie si quelque chose tourne mal.

---

- Oui. 3. Les bons, les mauvais et les méchants

3.1 Les bons – Pourquoi Ce problème est une victoire

Pourquoi ça compte ?
- Oui.
Le problème est un exemple de manuel d'un algorithme *greedy* qui peut être prouvé optimal via le théorème de Zeckendorf. Autres
Autres **Petits espaces de recherche**Les nombres de Fibonacci ≤ 109 ne sont que 44 en nombre, ce qui rend la force brute ou DP inutile. Autres
**Appel à l'entrevue** *générer → gourmand → compter*. Autres
**Language-agnostic**Les trois implémentations partagent la même logique. Autres

3.2 Les mauvaises – Pièges communs

Qu'est-ce qui arrive?
- C'est quoi ?
**Solution récursive**= Débordement de la pile sur le grand `k`.= Utiliser l'itération ou la récursion de la queue (pas nécessaire). Autres
**Générer tous les nombres de Fibonacci**. Autres
**Ignorer les cas d'Edge** `0`. Autres
Autres **Complexité du temps Mauvaise conception** Le coût réel est < < O(F * count) > > , mais < < F > ≤ 44 et < < count > > ≤ 5 (par Zeckendorf). Autres

3.3 Les pièges logiques subtils

Pourquoi c'est bizarre Comment éviter
- C'est quoi ?
**Utilisation "long`/`long` Une mémoire supplémentaire et des opérations plus lentes. Utiliser `int` (32-bit) – tous les numéros Fibonacci correspondent. Autres
**Utiliser `temps (k >= fib)` à l'intérieur de la boucle extérieure** dans le pire des cas, si "fib = 1". Puisque la boucle externe est déjà de grande à petite, une seule soustraction par `k` suffit. Autres
**Off‐by‐one dans la génération de Fibonacci**= La séquence peut commencer par `[1]` seulement, sans la seconde `1`. Commencez toujours par `[1, 1]`. Autres
**En supposant que l'avidité fonctionne pour toutes les sommes entières** Gardez Zeckendorf à l'esprit le théorème. Autres

---

- Oui. 4. SEO-Optimized Blog Titre & Meta Description

**Titre**
> LeetCode 1414: Master the Minimum Fibonacci Sum – Solutions Java, Python & C++

**Description détaillée**
> C'est avec LeetCode 1414 ? Apprenez la stratégie gourmande pour trouver les nombres minimums de Fibonacci qui s'élèvent à K. Full Java, Python, et C++ solutions plus interview-friendly. Augmentez votre performance d'entrevue de codage aujourd'hui. (en milliers de dollars)

---

- Oui. 5. Takeaway – Comment faire tourner l'entrevue

1. ** Expliquez le Greedy Insight** – mentionnez le théorème de Zeckendorf et pourquoi la plus grande approche est optimale.
2. **Afficher le code** – choisissez la langue avec laquelle vous êtes le plus à l'aise ; la logique est identique à travers Java, Python et C++.
3. **Discuss Complexity** – soulignez qu'il fonctionne en temps constant ('O(1)' en pratique, puisque seulement ~44 nombres de Fibonacci).
4. **Mention Edge Cases** – montrez que vous avez pensé à `k = 1` et de grandes valeurs.
5. **Soyez prêt à comparer** – discutez pourquoi la récursion est mauvaise et pourquoi la cupidité itérative bat DP.

---

- Oui. 6. Pensées finales

LeetCode 1414 est plus qu'un exercice de codage ; c'est une vitrine de l'élégance algorithmique. En maîtrisant la stratégie gourmande, vous impressionnerez les intervieweurs avec:

* * Conciseness* – petites boucles claires.
* *Speed* – comportement O(1) pour les limites pratiques.
* *Robustness* – gère toutes les entrées valides sans risque de dépassement ou de récursion.

Déposez les trois extraits de code dans votre repo GitHub, ajoutez le billet de blog à votre portfolio, et vous aurez un point de discussion poli pour toute entrevue d'ingénierie logicielle. Bonne chance ! C'est ce qu'il a dit