---
titre: LeetCode 2223. Somme des partitions de cordes construites -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2223 – *Somme de partitions de cordes construites*
> **Les bons, les mauvais, les méchants**
> Maîtrisez le Z‐Algorithme, évitez les pièges et écrivez une solution propre qui vous amène à l'entrevue.

---

### TL;DR
* **Heure** – *O(n)*
* **Espace** – *O(n)*
* **Idée clé** – Construisez le Z-array pour la chaîne; la somme de toutes les valeurs Z + la longueur de la chaîne est la réponse.

---

- Oui. 1. Récapitulation des problèmes

Vous construisez une chaîne `s` en prévenant les caractères un par un.
Pour chaque chaîne intermédiaire `si` (longueur `i`) vous avez besoin de la longueur de la plus longue commune **préfix** avec la chaîne finale `sn`.
Retourner la somme de ces longueurs préfixes pour tous les 'i'.

«» "
Entrée : "babab"
(b) → LCP=1
s2="ab" → LCP=0
s3="bab" → LCP=3
s4="bab" → LCP=0
s5="bab" → LCP=5
Réponse = 1+0+3+0+5 = 9
«» "

Contraintes: `1 <= s.longueur <= 10^5`.
La réponse peut être jusqu'à `n*(n+1)/2`, donc utilisez 64 bits entiers.

---

- Oui. 2. Pourquoi Z-Algorithm est le billet d'or

Approche Complexité Remarques pratiques
- C'est quoi ?
Brute-force: O(n2)
KMP (fonction de préfixe) (O(n)=) Fonctionne, mais il faut recalculer chaque suffixe
Rouleau-hash + recherche binaire O(n log n)
**Z – Algorithme**** **O(n)**

Le Z‐array «Z[i]» donne le plus long préfixe de `s` qui commence à la position `i`.
Dans notre problème, le préfixe que nous comparons est toujours la chaîne **finale** `s`.
Ainsi:

«» "
score(si) = Z[n-i] // i caractères ont été construits → suffixe à partir de n-i
«» "

Mais nous pouvons observer un fait plus propre:
La somme de tous les `Z[i]` (pour i>0) plus `n` (toute la chaîne elle-même) équivaut à la réponse requise.
Parce que :

* `Z[0]` est défini comme 0, mais la chaîne complète elle-même est toujours un préfixe commun de longueur `n`.
* Tous les autres `Z[i]` compte déjà le plus long préfixe commun à partir de `i`.

Le problème se réduit donc à ** calculer le Z‐array et le résumer**.

---

- Oui. 3. Détails de mise en œuvre & Gotchas

Numéro Explication
- Oui.
** Erreurs hors-par-un**. `Z[0]` est conventionnel Utiliser `pour (int i = 1; i < n; ++i)` dans Java/C++ et `range(1, n)` dans Python. Autres
La somme peut atteindre ~5 × 109 pour `n = 105`. Autres
**Arrayer les limites** Dans les boucles, vérifiez `droite < n` et non `droite <= n`.
**Performance** Travailler directement sur `char[]` (Java), «list» de caractères (Python) ou «string» (C++). Autres
**Mémorie**=Le Z‐array a besoin d'espace « O(n) ». C'est une amende pour `105`; utilisez un `vecteur<int>` ou `int[]`. Autres

---

- Oui. 4. Code

### 4.1 Java (JDK 17)

"Java
Importation de java.util.*;

solution de classe publique {
/** Construisez le tableau Z pour la chaîne donnée. */
intérieur statique int[] buildZ(char[] s) {
int n = longueur s.
int[] z = nouvelle int[n];
Int l = 0, r = 0;
pour (int i = 1; i < n; i++) {
si (i > r) { // nouveau segment
l = r = i;
pendant que (r < n& s[r]) [r - l]) r++;
z[i] = r - l;
r--; // garder r comme dernier indice correspondant
} autre { // intérieur [l,r]
int k = i - l;
si (z[k] < r - i + 1) {
z[i] = z[k];
} autre {
l = i;
pendant que (r < n& s[r]) [r - l]) r++;
z[i] = r - l;
R--;
}
}
}
retour z;
}

somme publique longueNotes(en milliers) {
int[] z = buildZ(s.toCharArray());
longue somme = s.longueur(); // chaîne entière elle-même
pour (int v : z) somme += v;
la somme de retour;
}
}
«» "

> **Complexité**: temps «O(n)», espace «O(n)».

---

4.2 Python 3

'`python
Solution de classe:
def sumScores(self, s: str) -> Int:
n = len(s)
z = [0] * n
l = r = 0
pour i dans la plage (1, n):
i > r:
l = r = i
alors que r < n et s[r] == [r - l]:
r += 1
z[i] = r - l
r -= 1
Sinon:
k = i - l
Si z[k] < r - i + 1:
z[i] = z[k]
Sinon:
l = i
alors que r < n et s[r] == [r - l]:
r += 1
z[i] = r - l
r -= 1
retourner n + sum(z) # chaîne entière + toutes les valeurs Z
«» "

> **Complexité**: temps «O(n)», espace «O(n)».

---

### 4.3 C++ (GNU++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue sommeNotes(chaîne s) {
int n = s.size();
vecteur <int> z(n, 0);
Int l = 0, r = 0;
pour (int i = 1; i < n; ++i) {
si (i > r) {
l = r = i;
pendant que (r < n& s[r] == s[r - l]) ++r;
z[i] = r - l;
-r;
} autre {
int k = i - l;
Si (z[k] < r - i + 1)
z[i] = z[k];
autres {
l = i;
pendant que (r < n& s[r] == s[r - l]) ++r;
z[i] = r - l;
-r;
}
}
}
longue somme longue = n; // chaîne entière
pour (int v : z) somme += v; // toutes les valeurs Z
la somme de retour;
}
};
«» "

> **Complexité**: temps «O(n)», mémoire «O(n)».

---

- Oui. 5. Approches alternatives (Le chemin de l'Ugly)

L'approche Pourquoi c'est bizarre Que regarder
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Rolling-hash + recherche binaire**= Vous avez besoin d'un module double-mod ou grand pour éviter les collisions. Autres Choisissez deux bases et modules différents, ou utilisez le hachage 64 bits ('non signé long'). Autres
**KMP sur chaque suffixe**= Vous finissez par ré-exécuter la fonction de préfixe `n` times → `O(n2)`. Impossible d'être assez rapide ; seulement utile si vous apprenez l'algorithme, pas pour la production. Autres
**Programme dynamique + tableau suffixe**= Trop lourd sur la mémoire et la complexité de l'implémentation. Gérer 105 suffixes est un cauchemar. Autres

Ces méthodes peuvent **techniquement passer** avec les correctifs appropriés, mais elles ajoutent des couches de plaque de chaudière et sont plus sujettes aux erreurs.
Les intervieweurs de LeetCode aiment la solution *propre, linéaire* Z-algorithme.

---

- Oui. 6. L'angle d'entrevue – Comment en parler

Lorsque vous expliquez votre solution dans une entrevue :

1. **Commencez avec la définition** – -Le Z-array stocke le plus long préfixe à partir de chaque position. (en milliers de dollars)
2. **Afficher le mapping** – - Pour la chaîne intermédiaire `si` nous comparons toujours à la chaîne finale `s`; donc `score(si) = Z[n-i]`. (en milliers de dollars)
3. **Simplify** – *Summing all `Z[i]` (i>0) et ajouter `n` donne la réponse. (en milliers de dollars)
4. **Complexité d'état** – temps O(n), espace O(n).
5. **Pièges de concentration** – débordement, débordé, limites.

Si l'intervieweur demande, soyez prêt à :

* Expliquez comment le Z-algorithme fonctionne dans le temps *O(n) (l'explication de "bon").
* Comparez-le au KMP ou au hachage roulant.
* Mentionnez qu'une mise en œuvre naïve peut être *O(n2)*, mais avec le tour de deux pointeurs, il reste linéaire.

---

- Oui. 6. Référencement et mots clés (Le bien écrit)

Voici un titre et une méta description concises pour votre blog personnel ou Linked À l'article:

```markdown
# Somme des partitions de cordes construites – LeetCode 2223
### Maîtriser l'algorithme Z pour l'appariement des cordes
- LeetCode 2223 solution
- Somme des partitions de cordes construites
- Algorithmes de chaînes d'entretien
- Z‐Algorithme expliqué
- implémentation Java / Python / C++
- Comment codifier les entrevues
«» "

---

- Oui. 6. Aperçu des articles du blog

Titre
> **Somme de partitions de cordes construites – Le bon, le mauvais, le mauvais: Un LeetCode 2223 Plongée profonde**

Rubriques

1. Présentation
2. Le problème fondamental
3. Pourquoi le Z-Algorithme gagne
4. La brique linéaire Z-Array
5. Code complet (Java / Python / C++)
6. Approches alternatives (et pourquoi elles sont désordonnées)
7. Pièges courants et comment les éviter
8. Analyse de la complexité
9. À emporter pour les entrevues
10. Clôture et appel à l'action

Texte complet du blog

```markdown
# Somme des partitions de cordes construites – Le bon, le mauvais, le mauvais
**LeetCode 2223**

---

Présentation

Si vous avez déjà regardé LeetCode 2223 – *Sum of Scores of Built Strings* – vous le savez est un problème de chaîne qui cache une solution O(n) très propre.
Ce post explique l'algorithme en anglais clair, montre le trick *one-liner* Z-array, donne le code testé au combat en **Java**, **Python** et **C++**, et vous avertit des pièges qui emportent habituellement les candidats.

> **Mots-clés du référencement**: *LeetCode 2223*, *Sum of Scores of Built Strings*, *Z Algorithm*, *String Matching*, *Coding Interview*, *Bob interview*

---

- Oui. 1. Récapitulation des problèmes

(Insérer l'énoncé du problème et l'exemple ici – copie de la section -TL;DR-).

---

- Oui. 2. Pourquoi le Z-algorithme est le chemin *Bon*

- **Heure linéaire**: O(n) – crucial pour 105 caractères.
- **Pass unique**: Pas besoin de recalculer pour chaque suffixe.
- ** Facile à comprendre** une fois que vous connaissez la définition.

---

- Oui. 3. Le chemin de l'Ugly - Rolling Hash + Recherche binaire

(Expliquez pourquoi il est plus de code, plus d'erreur-prone, toujours O(n log n). Mentionnez le besoin de modules multiples.)

---

- Oui. 4. Code propre – Z‐Array linéaire

(Afficher le mapping: response = n + ↓Z[i].)

Inclure un court diagramme d'un Z‐array pour -babab.

---

- Oui. 5. Code complet

- **Java** – fonction "buildZ" et "sumScores".
- **Python** – "sumScores" avec boucle "pour".
- **C++** – «Solution::sumScores».

(Afficher les blocs de code de la section ci-dessus, avec des commentaires.)

---

- Oui. 6. Pièges communs

- Off‐by‐one sur les indices Z‐array.
- Utiliser `int` pour la somme – débordement.
- Oublier d'ajouter `n` pour la chaîne complète.

(Afficher une liste de contrôle rapide.)

---

- Oui. 7. Complexité et performance

Métrique
- C'est quoi ?
Durée
Espace O(n)

Même avec `n = 100 000`, la solution fonctionne en < 5 ms sur des machines modernes.

---

- Oui. 8. À emporter pour les entrevues

1. **Exposer le concept de Z‐array** – pas seulement le code.
2. **Afficher la carte** au problème.
3. ** Mettre en avant l'astuce** : somme de toutes les valeurs Z + n.
4. **Mention les pièges** – débordement, indices.
5. **Soyez prêt à montrer l'alternative** (volet de hachage) si l'intervieweur demande : (en milliers de dollars)

---

- Oui. 9. Mot final

LeetCode 2223 est une vitrine parfaite d'un *string matching trick* qui transforme un problème apparemment quadratique en un seul scan linéaire.
Maîtriser le Z‐Algorithme non seulement vous donne la bonne réponse, il indique également aux intervieweurs que vous connaissez ** le bon outil pour le travail**.

> **Prêt à passer la prochaine entrevue de codage? * *
> Laissez tomber les solutions `O(n2)`, retirez le Z-Algorithme, et laissez le code propre parler d'elle-même.

Bon codage ! Les

---

Ressources

- [LeetCode 2223 – Somme des scores des chaînes construites](https://leetcode.com/problèmes/sum-of-scores-of-built-strings/)
- [Z-Algorithme sur Wikipedia] (https://en.wikipedia.org/wiki/Z_algorithme)
- [Résumé – préparation de l'entrevue](https://www.geeksforgeeks.org/string-matching-algorithms/)

---