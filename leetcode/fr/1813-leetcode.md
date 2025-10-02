---
titre: LeetCode 1813. Condamnation Similarité III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code – LeetCode 1813

Ci-dessous vous trouverez **trois implémentations propres, prêtes à la production** – une en Java, une en Python et une en C++.
Chaque mise en œuvre suit la même stratégie de deux points O(n) décrite dans l'éditorial:

1. Séparez les deux phrases en listes de mots.
2. Marcher à gauche pendant que les mots correspondent.
3. Marcher à droite pendant que les mots correspondent.
4. Si le nombre de mots appariés (`gauche + droite`) est au moins la taille de la phrase plus courte, les deux phrases sont similaires.

---

### 1.1 Java (format LeetCode)

"Java
Importation de java.util.*;

solution de classe publique {
booléen public sont les peines Similar(String phrase1, String phrase2) {
// Séparer en mots
Chaîne[] words1 = phrase1.split(");
Chaîne[] words2 = phrase2.split(");

// S'assurer que words1 est la phrase plus longue
si (mots1.longueur < mots2.longueur) {
Chaîne[] tmp = mots1; mots1 = mots2; mots2 = tmp;
}

i = 0, j = 0; // indices de démarrage
int n1 = mots1.longueur, n2 = mots2.longueur;

// Un match depuis le début
(i < n2 && words1[i].equals(words2[i]) i++;

// 2=2 match de la fin
(j < n2 && words1[n1 - j - 1].equals(words2[n2 - j - 1]) j++;

Tous les mots de la phrase plus courte sont couverts
retour i + j >= n2;
}
}
«» "

> **Pourquoi cela fonctionne** –
> Le seul endroit où une nouvelle phrase peut être insérée est entre le préfixe assorti et le suffixe.
> Si la partie médiane non assortie de la phrase plus longue s'inscrit pleinement dans cette phrase, les deux phrases peuvent être identiques.

---

### 1.2 Python 3 (format LeetCode)

'`python
Solution de classe:
les peines Similar(self, phrase1: str, phrase2: str) -> C'est vrai.
# Séparer en listes de mots
w1 = phrase1.split()
w2 = phrase2.split()

# Faites w1 la liste la plus longue
si len(w1) < len(w2):
w1, w2 = w2, w1

i = 0 # pointeur de départ
j = 0 # pointeur d'extrémité
n1, n2 = len(w1), len(w2)

Correspondance
alors que i < n2 et w1[i] == w2[i]:
i += 1

# Nombre suffisant
alors que j < n2 et w1[n1 - j - 1] == w2[n2 - j - 1]:
j += 1

# Tous les mots de la phrase plus courte sont couverts
retour i + j >= n2
«» "

---

### 1.3 C++ (format LeetCode)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Bool sont les peines Similar(string phrase1, string phrase2) {
// Aide : diviser une phrase en mots
fractionnement automatique = [](cont string& s) {
vecteur <string> rés;
chaîne de caractères cur;
pour (charc : s) {
si c) ' ) {
si (!cur.vide()) { res.push_back(cur); cur.clear(); }
} autre {
pour += c;
}
}
si (!cur.vide()) res.push_back(cur);
retour rés;
};

vectorielle<string> w1 = split(sentence1);
vecteur <string> w2 = split(sentence2);

// S'assurer que w1 est le vecteur le plus long
si (w1.size() < w2.size()) swap(w1, w2);

taille_t i = 0, j = 0;
size_t n1 = w1.size(), n2 = w2.size();

// Correspondance de l'avant
pendant que (i < n2 && w1[i] == w2[i]) ++i;

// Correspondance de l'arrière
pendant que (j < n2 && w1[n1 - j - 1] == w2[n2 - j - 1]) ++j;

// Tous les mots de la phrase plus courte sont pris en compte
retour i + j >= n2;
}
};
«» "

---

- Oui. 2. Billet de blog – Le bon, le mauvais, et le mauvais de LeetCode 1813

> **Mots-clés cibles:** *LeetCode, Sentence Similitude III, interview par algorithme, entretien d'emploi, défi de codage, préparation d'entrevue, Java, Python, C++ *

2.1 Introduction

Quand vous trébuchez **LeetCode 1813 – La peine Similitude III** dans votre prép d'entrevue, la première chose qui vous frappe est qu'il est un problème de moyen. Pourtant sa solution est *remarquablement simple* une fois que vous voyez le bon angle.
Dans ce post, nous allons marcher à travers l'algorithme, disséquer ce qui le rend grand, exposer les pièges cachés, et vous montrer les cas de bord de l'algorithme qui pourraient vous faire monter. Nous vous offrons également une implémentation **ready‐to-colle** en Java, Python et C++ afin que vous puissiez vous vanter de vos compétences lors de votre prochaine interview.

> **Pourquoi cela compte pour votre chasse au travail** –
> Les intervieweurs aiment les problèmes qui vous forcent à penser en termes de *préfixe/suffixe* et de *deux-pointeurs*. Démontrer la maîtrise de ce modèle montre que vous pouvez traduire un énoncé de problème en une solution efficace et durable. De plus, connaître les pièges vous empêche de ce moment où un test échoue de façon inattendue.

---

2.2 Récapitulation du problème

> **Objectif** : Déterminer si deux phrases peuvent devenir identiques en insérant *toute* phrase contiguë (éventuellement vide) dans l'une d'entre elles.

- Les peines sont des mots séparés de l'espace.
- Pas d'espaces de guidage.
- Les mots ne contiennent que des lettres (en haut/en bas).

**Exemples**

Condamnation 1 Condamnation Résultat
C'est pas vrai.
Autres Mon nom est Haley
Beaucoup de mots
Je mange tout de suite

---

2.3 Le bon – 2-Pointeur de puissance

Aspect Pourquoi il est grand
-- -- -- -- -- --
**O(n) Temps**= Nous scannons chaque mot au plus deux fois (une fois depuis le début, une fois depuis la fin). Pas de boucles imbriquées. Autres
**O(n) Espace**=Seulement stocker des listes de mots; aucune structure de données auxiliaire lourde. Autres
**Intuitive**=La correspondance des préfixes et des suffixes est un motif qui apparaît dans de nombreux problèmes de cordes (palindromes, préfixe commun le plus long, etc.). Autres
**Language-agnostic** ► Fonctionne de la même façon en Java, Python, C++ – il suffit de diviser les chaînes et de comparer les indices. Autres
**Facile à lire**La logique de 2 points est souvent plus courte et plus claire que la récursion ou la programmation dynamique pour ce problème. Autres

> **À emporter** – Une approche concise à deux points démontre que vous pouvez extraire l'essence d'un problème et le résoudre en temps linéaire.

---

2.4 Les mauvais – Coûts cachés

Sujet Impact
C'est quoi ?
Dans un environnement d'entretien serré, on s'attend à ce que le code reste maigre. `split("")` (Java), `split()` (Python) ou tokenization manuelle (C++) all all all all assignen new strings. Pour les entrées énormes, cela peut devenir un frais généraux mesurables. Autres
**Scission sensible à l'espace **= Certaines langues traitent les espaces comme un espace blanc dépendant de l'espace local. Toujours scindé sur le caractère d'espace littéral (`"""), pas le régex par défaut, pour éviter les surprises. Autres
**Grande taille d'entrée**= Bien que l'algorithme soit O(n), vous pouvez activer les performances de Java="String.split` O(n2) si vous utilisez un regex qui compile à chaque fois. Préférez `StringTokenizer` ou analyse manuelle en Java pour le code de production. Autres
**Cas d'Edge Description phrase vide** L'instruction de problème permet d'insérer une phrase *vide*. Votre code doit gérer correctement les phrases de longueur zéro. Autres
**Les mots sont sensibles aux cas. Assurez-vous d'utiliser `egals` (Java) ou `==` après `split()` (Python) – pas `==' en Java qui compare les références d'objets. Autres

---

#### 2.5 Les horribles cas de bord

Cas de bord Pourquoi il voyage des gens Comment garder
- C'est pas vrai.
Autres **La phrase plus courte est déjà un suffixe de la phrase plus longue**. `left + right` ne peut être égal à `n2` que si le suffixe assorti est **non-overlaping** avec le préfixe. Veiller à ce que les boucles `tandis` utilisent `< n2` *not* `< n1`. Autres
**Les deux phrases sont identiques. La condition finale `gauche + droite >= n2` est le contrôle définitif. Autres
**Tous les mots correspondent, mais l'ordre diffère**= Exemple: =Hello World===HelloWorld===Hello===La méthode des deux points retournera faux parce que ni le préfixe ni le suffixe correspondent entièrement. Autres
**Insertion d'empty**=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello=Hello La vérification `>=` gère l'affaire du milieu vide. Autres
Autres **Secteur moyen très long**==a b c ...=z vs=a ...=z=a Vos tableaux divisés doivent gérer de longues listes. Utilisez une analyse efficace en Java (par exemple, `StringTokenizer`) si vous êtes préoccupé par les performances. Autres

> **Conseil de débogage** – Après les boucles à deux points, imprimer `i`, `j`, `n2` et veiller à ce que `i + j` ne dépasse jamais `n2`. Si c'est le cas, vous avez couvert toute la phrase plus courte.

---

2.6 Pseudocode

Texte
fractionner la phrase1 en mots1
fractionner la phrase2 en mots2
si len(words1) < len(words2) les échange // words1 est toujours plus long

gauche = 0
droite = 0
n1 = len(mots1), n2 = len(mots2)

tout en restant < n2 et words1[left] == words2[left]:
gauche += 1

alors que droite < n2 et mots1[n1 - droite - 1] == mots2[n2 - droite - 1]:
droite += 1

retour à gauche + à droite >= n2
«» "

---

2.7 Résumé de la complexité

Complexité
C'est pas vrai.
**Heure**="O(n)" – chaque mot est examiné au plus deux fois. Autres
**L'espace**="O(n)" – les deux vecteurs de mots. Autres
**Meilleur/Meurtre** Autres
**Scalabilité**= Fonctionne confortablement jusqu'à des millions de caractères (les cas de test LeetCode sont beaucoup plus petits). Autres

---

### 2.8 Liste de contrôle des entrevues dans le monde réel

Objet
- Oui.
Utiliser une simple boucle à deux points – pas de récursion ou de DP. Autres
Toujours échanger donc la première liste est la plus longue. Autres
Comparer les mots avec `egals` (Java), `==` après `split()` (Python), ou `==` sur les objets `string` (C++). Autres
Testez votre code sur les cas de bord suivants :
1.
2.
3.
4. (la phrase vide est **non** autorisée par la déclaration, mais bonne à vérifier). Autres

---

2.9 Dernier départ

- **Afficher le motif** – La comparaison préfixe/suffixe est une technique à feu rapide qui impressionne les intervieweurs.
- **Éviter les gotchas** – Attention au fractionnement des cordes et aux limites des pointeurs.
- **Prêt à passer** – Utilisez les extraits de code ci-dessus dans la langue de votre choix.

**Maintenant, vous pouvez entrer dans n'importe quel entretien de codage armé d'une solution propre et efficace à la Sentence Simility III et un blog qui vous montre comprendre le problème au niveau *chaque*. Bonne chance pour ce prochain travail ! **

---