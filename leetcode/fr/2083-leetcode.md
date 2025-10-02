---
titre: LeetCode 2083. Sous-chaînes qui commencent et se terminent avec la même lettre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2083 – Sous-chaînes Qui commencent et finissent par la même lettre
> **Délai**: 1 s – 2 s (type LeetCode).
> **Limitation de l'espace**: 256 Mo.

---

Déclaration de problème (courte)

Avec une chaîne **s** de lettres anglaises minuscules, compter toutes les sous-chaînes contiguës non vides dont le premier et le dernier caractères sont identiques.

> **Exemples**
> `s = "abcba"` → **7** (`"a", "b", "c", "b", "a", "bcb", "abcba"`)
> `s = "abacad"` → **9** (`"a", "b", "a", "c", "a", "d", "aba", "aca", "abaca"`)
> `s = "a"` → **1**

Contraintes
`1 ≤ s. longueur ≤ 10^5`

---

Pourquoi cela compte dans les entrevues

- Montre la familiarité avec **préfixes / combinatoires**.
- Démontre l'espace auxiliaire *O(n)* traversant + *O(1)* – un modèle d'entrevue classique.
- Donne un instant rapide à un seul passage avec un tableau de fréquence résout tout.

---

## Description générale de la solution – Le bien

1. ** Compte de fréquence + combinatoire**
- Pour chaque lettre, il faut indiquer le nombre d'événements.
- Toutes les sous-chaînes qui commencent et finissent par cette lettre se présentent sous deux formes :
*sous-chaînes à caractères simples* ('cnt' d'entre elles)
* sous-chaînes de caractères multiples* formées par la sélection de deux occurrences différentes : `cnt * (cnt-1) / 2`.
- Somme sur les 26 lettres.
- **Complexité**: temps «O(n)», espace «O(1)».

2. **Single-Pass Constante-Espace**
- Traversez la corde de droite à gauche.
- Gardez un tableau `count[26]` où `count[c]` détient le nombre de fois que le caractère `c` a déjà été vu à la droite*.
- Pour chaque position «i»:
«» "
Total += nombre[ s[i] ] + 1
Nombre[ s[i] ]++
«» "
Le `+1` représente la sous-chaîne à caractère unique à `i`.
- **Complexité**: temps «O(n)», espace «O(1)», *pas de combinatoire*.

Les deux solutions produisent la même réponse et fonctionnent confortablement sous les contraintes.

---

Le mal – Que ne pas faire

Une erreur Pourquoi elle échoue
- C'est quoi ?
** Force brute** – Énumérer toutes les sous-chaînes « O(n2) » et vérifier les extrémités. Autres
**Utiliser `StringBuilder` par sous-chaîne** Utiliser uniquement les indices. Autres
**L'utilisation de `Map<Caracter, Integer>`**" 26 clés est très bien, mais l'utilisation d'un HashMap ajoute un coût de hachage inutile. Un tableau simple de taille 26 est plus rapide. Autres
**Débordement de l'int**= `cnt * (cnt-1)/2` peut dépasser `int` pour `n=105`.

---

L'Ugly – Cas de bord et pièges

1. **Dépassement**
- Pour `n = 105`, la réponse maximale possible est `n*(n+1)/2 "5·109`, ce qui *ne correspond pas à un `int' signé 32-bits.
- Utilisez `long` / `int64_t`.

2. **Validation d'entrée* *
- LeetCode garantit les lettres minuscules, mais si vous écrivez une bibliothèque, gardez-vous contre les chaînes nulles ou vides.

3. **Grandes épreuves* *
- Si la chaîne est tout le même caractère, l'algorithme fonctionne toujours dans `O(n)`, mais la formule combinatoire donne le plus grand résultat – assurez-vous que votre type de données peut le contenir.

---

Mise en œuvre du code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**. Tous suivent la méthode de l'espace constant monopass (vous pouvez l'échanger à la méthode combinatoire si vous préférez).

---

C'est pas vrai. Java

"Java
importation java.io.*;

solution de classe publique {
***
* compte toutes les sous-chaînes qui commencent et finissent avec la même lettre.
* Utilise un seul balayage de droite à gauche et un tableau de fréquences.
*
* @param s la chaîne d'entrée (case inférieure seulement)
* @retourner le nombre total de sous-chaînes valides
*/
grand nombre DeSous-chaînes {
long total = 0;
int[] count = nouveau int[26]; // fréquence de chaque lettre vue à droite
char[] arr = s.toCharArray(); // éviter les répétitions de s.charAt()

pour (int i = arr.longueur - 1; i >= 0; i--) {
int idx = arr[i] - 'a';
total += nombre[idx] + 1; // +1 pour la sous-chaîne à caractère unique
count[idx]++; // ce char est maintenant vu à droite
}
le total des retours;
}

// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
// Voici l'implémentation combinatoire classique.
// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
public long nombre OfSubstringsCombinatorial(String s) {
long[] freq = nouveau long[26];
pour [charc : s.toCharArray()) {
freq[c - 'a']++;
}

long res = 0;
pour (long f : freq) {
Res += f * (f - 1) / 2 + f; // combinaison simple + paire
}
retour rés;
}

// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
// Méthode principale d'essai manuel rapide (facultatif)
// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
Chaîne s = br.readLine();
Solution sol = nouvelle solution();
System.out.println(sol.numberOfSubstrings(s));
}
}
«» "

---

# # # # # #

'`python
Solution de classe:
def numberOfSubstrings(self, s: str) -> Int:
"""
Comptez les sous-chaînes qui commencent et finissent par la même lettre.
Passage simple droit à gauche avec un tableau de 26 éléments.
"""
count = [0] * 26 # freq de chaque lettre vue à droite
Total = 0

pour ch en sens inverse(s):
idx = ord(ch) - 97 # 'a' == 97
total += nombre[idx] + 1 # +1 pour la sous-chaîne à caractère unique
nombre[idx] += 1

retour total

♪ ----------------------------------------------------------------------------------
# Alternative: approche combinatoire
♪ ----------------------------------------------------------------------------------
def numberOfSubstrings_combinatorial(self, s: str) -> Int:
freq = [0] * 26
pour ch en s:
freq[ord(ch) - 97] += 1

Res = 0
pour f en freq:
Res += f * (f - 1) // 2 + f
retour res
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Pass unique O(n) avec espace O(1)
long nombre DeSous-chaînes(chaîne s) {
long total = 0;
int cnt[26] = {0};

pour (auto it = s.rbegin(); it != s.rend(); ++it) {
int idx = *it - 'a';
+= cnt[idx] + 1; // +1 pour la sous-chaîne monochar
++cnt[idx];
}
le total des retours;
}

// ----------------------------------------------------------------------------------
// Variante: combinatoire
// ----------------------------------------------------------------------------------
long nombre de sous-chaînesCombinatoire(chaîne s) {
long freq[26] = {0};
pour (char c : s) freq[c - 'a']++;

longue rés = 0;
pour (long long f : freq) res += f * (f - 1) / 2 + f;
retour rés;
}
};
«» "

---

Post de blog draft – -Le bon, le mauvais, l'Ugly (SEO optimisé)

> **Titre**
> *Le compte de sous-chaîne en Java, Python & C++ – Le bon, le mauvais et le mauvais de LeetCode 2083*

> **Description détaillée**
> Apprenez à résoudre le LeetCode 2083 – sous-chaînes qui commencent et se terminent avec la même lettre – en Java, Python et C++ avec un temps O(n) optimal et un espace O(1). Découvrez la meilleure approche, les pièges communs et les extraits de code qui impressionnent les intervieweurs.

---

Introduction

Lorsque vous appuyez sur *LeetCode 2083*, vous êtes confronté à un problème de comptage trompeur qui, s'il est résolu efficacement, peut instantanément augmenter votre score – et votre confiance. Dans ce post, nous allons passer par **pourquoi** ce problème est important, **comment** pour le résoudre en **trois** langues populaires, et ce qui vous écueillera à éviter.

- Oui. Le problème en coque

Avec une chaîne de lettres minuscules, compter toutes les sous-chaînes contiguës non vides qui commencent et se terminent par la même lettre.

*Exemple:*
`s = "abcba"` → 7 sous-chaînes (`"a", "b", "c", "b", "a", "bcb", "abcba"`)

Pourquoi les intervieweurs aiment ce problème

- ** Démontre la pensée algorithmique**: Un scan classique de droite à gauche + tableau de fréquence.
- **Afficher l'efficacité de l'espace**: O(1) espace auxiliaire (seulement 26 entiers) par rapport aux solutions "O(n2)" naïves.
- **Ouvre la porte aux combinatoires**: Beaucoup de candidats sont surpris d'apprendre qu'une formule simple suffit.

### La bonne – La solution monopasse constante-espace

1. **Maintenir un tableau de fréquence de droite à gauche. **
2. Pour chaque caractère à la position `i`:
Total += nombre[char] + 1`
Nombre [char]++
3. Le `+1` compte la sous-chaîne à caractère unique à `i`.

Ce scan nécessite une seule passe sur la chaîne, ce qui la rend **O(n)** dans le temps et **O(1)** dans l'espace. C'est aussi **langue-agnostique** : la même idée fonctionne en Java, Python et C++.

"Java
int idx = s.charAt(i) - 'a';
total += droitCount[idx] + 1;
droite Nombre[idx]++;
«» "

- Oui. Les mauvaises – pièges communs

Question: Ce qui ne va pas
C'est ce que j'ai dit.
Utiliser un tableau de comptage. Autres
Utilisation d'un `HashMap`. Tableau simple de 26 int. Autres
Débordement de 32 bits Le terme `cnt*(cnt-1)/2` peut dépasser `int`. Autres

### L'Ugly – Cas de bord et écoulement excessif

Pour "n = 100 000", la réponse peut atteindre 5 milliards. Utilisez toujours un entier 64 bits.
- ** Chaîne de caractères tout-même**: Ce cas pousse l'algorithme à sa réponse maximale ; assurez-vous que votre langue de type numérique peut le stocker.

Extraits de code (Java / Python / C++)

> * Ci-dessous, vous trouverez des solutions propres et prêtes à copier pour la méthode à un passage et une alternative combinatoire classique. *

[Insérer les blocs de code Java, Python, C++ à partir de la section "Applications de code".]

Quelle approche devrais-je montrer dans une entrevue?

- **Si vous êtes sur une plateforme de codage chronométrée**: La méthode **simple-pass** est la plus rapide (= 0,05 s pour 100 k caractères sur LeetCode).
- **Si vous voulez impressionner avec les mathématiques**: La version **combinatoire** est élégante et montre que vous connaissez les formules binomiales de base.

Dernier départ

LeetCode 2083 est une vitrine parfaite de la finesse algorithmique. En adoptant un scan *de droite à gauche avec un tableau de 26 éléments*, vous obtenez :

- **O(n)** temps – linéaire dans la longueur de la chaîne.
- **O(1)** espace – pas de structures dynamiques, juste quelques entiers.
- **Robustness** – pas de débordement avec `long` / `int64_t`.

Utilisez les extraits de code ci-dessus comme référence, modifiez-les pour votre style, et vous serez prêt à répondre à cette question *sans accrochage* dans une entrevue ou un juge en ligne.

---

Clôture

Maintenant que vous avez la solution *=good=*, les erreurs *=bad=* à éviter, et les idées *=ugly=* edge–case, allez de l'avant et soumettez ces solutions propres, O(n) en Java, Python ou C++. Bonne chance, et que vos intervieweurs aiment l'élégance de votre réponse autant qu'ils aiment le tour algorithmique! C'est ce qu'il a dit.

---

**Tags**: #LeetCode #AlgorithmDesign #Java #Python #C++ #Manipulation de la chaîne #InterviewPréparation #CodingInterview #AlgorithmiqueThinking

---

*Sentir libre d'adapter la mise en page du post, d'ajouter des captures d'écran, ou de l'intégrer dans une série sur le thème "Counting Problems" sur votre blog personnel ou Medium. La clé est de garder le code croustillant, l'explication claire, et les balises de référencement se sont concentrées sur le LeetCode 2083, le comptage des sous-chaînes et l'algorithme d'entretien. *