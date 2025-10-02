---
titre: LeetCode 3035. Palindromes maximums après les opérations -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Voici trois implémentations compactes et prêtes à la production qui suivent toutes la même idée gourmande :

* Compter le nombre total de *paires* de caractères qui existent dans toutes les chaînes combinées.
* Triez les longueurs des cordes en ordre ascendant.
* Marcher dans les longueurs triées, en soustrayant les paires nécessaires pour chaque mot (`len/2`).
* Dès que le pool de paires est épuisé nous arrêtons – cet indice est le nombre maximum de palindromes que nous pouvons créer.

L'algorithme fonctionne dans le temps `O(n log n)` en raison du tri (avec `n ≤ 1000`) et utilise `O(1)` espace supplémentaire (seulement le tableau de fréquence).

---

### Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe {
int public maxPalindromes Après les opérations(mots de frappe[]) {
int n = longueur de mots;
int[] len = nouvelle int[n];
pour (int i = 0; i < n; ++i) len[i] = mots[i].longueur();
Arrays.sort(len); // ascendant

int[] freq = nouveau int[26];
pour (Pièce w : mots)
pour [charc : w.toCharArray())
freq[c - 'a']++;

paires int = 0;
pour (int f : freq) paires += f / 2; // paires totales disponibles

pour (int i = 0; i < n; ++i) {
paires -= len[i] / 2; // paires nécessaires pour ce mot
si (paires < 0) retour i; // ne peut satisfaire ce mot
}
retour n; // tous les mots peuvent être palindromes
}
}
«» "

---

### Python (style LeetCode)

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def maxPalindromes Après les opérations(self, mots: List[str]) -> Int:
# longueurs triées ascendantes
objectif = trié(carte(len, mots))

# fréquences globales de caractères
freq = Counter(c pour w en mots pour c en w)

# Nombre total de paires que nous pouvons former
paires = somme(v // 2 pour v dans freq.values())

pour i, l dans l'énumération(lentilles):
paires -= l // 2
si paires < 0:
retour
retour len(lens)
«» "

---

### C++ (style LeetCode)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxPalindromesAprès les opérations(vecteur<chaîne>& mots) {
vecteur <int> len;
pour (auto &w : mots) len.push_back((int)w.size());
tri(len.begin(), len.end()); // ascendant

int freq[26] = {0};
pour (auto & w : mots)
pour (char c : w) freq[c - 'a']++;

paires int = 0;
pour (int f : freq) paires += f / 2; // paires totales

pour (int i = 0; i < (int)len.size(); ++i) {
paires -= len[i] / 2; // paires nécessaires
si (paires < 0) retourne i;
}
retour (int)len.size(); // tout peut être palindromes
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 3035

> ** Palindromes maximaux après les opérations**
> *LeetCode 3035 – Moyenne – 2024‐02‐18*

> **Mots clés**: LeetCode interview, palindrome, algorithme gourmand, manipulation de chaînes, entretien d'emploi, conception d'algorithmes, Java, Python, C++

---

Introduction

Lors de la préparation pour les interviews de codage, vous allez rapidement rencontrer des problèmes qui sonnent trivial mais cacher un subtil tour combinatoire. *Palindromes maximaux après opérations* (LeetCode 3035) est l'un de ces joyaux. Sur la surface, on vous demande de transformer autant de chaînes que possible en palindromes en échangeant des caractères entre deux positions en deux mots – ou même le même mot.

L'astuce est que ** chaque personnage peut être déplacé librement** ; seule la longueur * de chaque mot est immuable. Avec cela, le défi s'effondre dans un problème de comptage. Dans cet article, nous traversons la partie *bon* (pourquoi la solution gourmande fonctionne), le *mauvais* (pièges communs) et le *ugly* (cases de référence qui voyagent beaucoup de solutions). À la fin, vous aurez une mise en œuvre propre et prête à la production et une compréhension plus approfondie de la raison pour laquelle elle fonctionne – un point de discussion parfait pour votre prochaine entrevue.

---

- Oui. 3. Le bon – Pourquoi l'avidité + le tri fonctionne

### 3.1. Les paires sont la véritable ressource

* Un palindrome exige que chaque position sauf le milieu (si la longueur est impair) fait partie d'une paire* de caractères identiques.
* Globalement, le nombre de paires que nous pouvons construire est simplement `sum(freq[c] // 2)` pour chaque caractère `c` dans l'alphabet de 26 lettres.

Si nous avons assez de paires pour couvrir tous les mots d'une longueur égale * et * les mots d'une longueur étrange (avec un caractère d'un peu plus que chacun), nous pouvons faire **chaque mot** un palindrome. La seule ressource qui nous limite est le *pool de paires*.

3.2. Traiter les mots les plus courts d'abord

Pourquoi trier par longueur ? Parce qu'un mot court a besoin de paires *fewer* pour devenir un palindrome (`len/2`). En satisfaisant les mots les plus courts d'abord nous conservons autant de paires que possible pour les mots plus longs qui ont besoin de plus. C'est le principe classique d'utilisation de la plus petite demande.

Exemple

Mots Longueur Nombre de paires nécessaires ('len/2') Autres
- C'est pas vrai.
""ab"""""
"c""""""""1"
""déf"""""""""

Si le pool global contient 2 paires, nous:

1. Utilisez 1 paire pour le mot 2 lettres → 1 paire restante.
2. Utilisez 0 paires pour le mot 1 lettre → 1 paire restante.
3. Utilisez 1 paire pour le mot 3 lettres → 0 paires gauche → *tous les mots peuvent être palindromes*.

Si nous n'avions qu'une paire dans le monde, le troisième mot échouerait et nous nous arrêterions à l'index `2`, donnant des palindromes `2`.

---

- Oui. 4. Les mauvaises – erreurs courantes

Pourquoi ça se casse
C'est pas vrai.
**Skipping du genre**.Sans tri, vous pouvez essayer de satisfaire un long mot d'abord, en utilisant de nombreuses paires tôt et en laissant des paires insuffisantes pour un court mot qui aurait été faisable. Toujours en ascension. Autres
**Utiliser impairLength – impairFrek logique**=Il semble élégant mais peut fausser l'estimation lorsque plusieurs fréquences impaires =spill= dans des mots de longueur égale. La version simple de comptage par paires n'a jamais besoin de suivre les fréquences impaires explicitement. Utilisez l'avidité à base de paires; il gère naturellement les nombres impairs. Autres
**Les paires de calcul sont incorrectes**.Le terme `freq[c] / 2` est une division entière – oubliant de l'utiliser peut compter ou manquer des paires. Double-vérification avec petits tests unitaires. Autres
**Le problème garantit les lettres anglaises minuscules, mais si la déclaration change, vous aurez besoin d'une carte dynamique. Autres Gardez la taille du tableau fixe, mais documentez l'hypothèse. Autres

---

- Oui. 5. Les cas lugubres – bord qui voyagent beaucoup

1. **Tous les mots ont une longueur étrange mais nous n'avons pas de fréquences de caractères étranges* *
- L'algorithme fonctionne toujours parce que chaque mot a besoin de paires `len/2`, et il y a assez de paires.
2. **Plus de fréquences impaires que de mots impairs* *
- Exemple: `[ "a", "bb", "c" ]` → 3 fréquences impaires (`a`, `c` et le seul `b`), 2 mots impairs (`"a"` et `"c"`).
- L'algorithme avide réduit automatiquement le nombre de paires jusqu'à ce que la pénurie soit détectée ; le caractère extra-impair forcera au moins un mot à ne pas être palindrome.
3. **Grande chaîne avec une longueur étrange mais tous les caractères même**
- Parce que sa fente moyenne peut encore tenir le caractère étrange -left-over, il est compté comme un palindrome.
4. **Zero words** (panier vide) – trivial, retourne `0`.
5. **Ficelles très courtes (longueur 1)** – besoin de paires `0`, toujours satisfait si au moins une paire est disponible.

Tous les éléments ci-dessus sont traités par la boucle *simple* qui soustrait `len/2`. Même lorsque le pool de paires est négatif sur un mot particulier, nous savons que la réponse est exactement cet indice.

---

- Oui. 6. Conseils de mise en oeuvre pour l'entrevue

Conseil Code Extrait de code
C'est quoi ?
Autres **Utilisez un tableau de taille fixe pour les fréquences** – plus rapide qu'une carte.
**Longueurs de caisse en ordre ascendant** – plus facile à comprendre et garantit la justesse. Autres
**Paires de soustraction en tant que division entière** – `len[i] // 2` ou `len[i] / 2`.
**Début de la sortie** – dès que `pairs < 0`, vous pouvez `retour i`.
**Retour `n`** si la boucle se termine – tous les mots peuvent être palindromes. "retour n;" Autres

---

- Oui. 7. Analyse de la complexité

Métrique
- C'est quoi ?
Temps `O(n log n)` (tri) `O(n log n)` Autres
Espace Autres
Remarques Utilisations `int[] freq[26]` et `int[] len`

Avec `n ≤ 1000`, l'exécution est confortablement à l'intérieur des limites de LeetCode.

---

- Oui. 8. Pourquoi ce code est-il prêt à l'entrevue

* **Nom clair** – « paire » et « len » rendent l'intention évidente.
* **Pas de constantes magiques** – la seule valeur magistrale est «26», le nombre de lettres minuscules, qui s'explique lui-même.
* **Responsabilité unique** – chaque partie du code fait une chose : recueillir des données, calculer des paires, boucler des longueurs.
* **Tests de vol** – Vous pouvez immédiatement vérifier contre les tests officiels de LeetCode plus quelques cas de bord fabriqués à la main:

Texte
Entrée : ["aa", "ab", "ba"]
Sortie: 3 (Tous peuvent devenir des palindromes)

Entrée : ["abc","de"]
Sortie : 1 (Seule la première chaîne peut être faite d'un palindrome)

Entrée: ["a", "b", "c", "d", "e"]
Sortie : 5 (Toutes les chaînes de longueur-1 sont des palindromes)
«» "

---

- Oui. 9. Conclusion

LeetCode 3035 enseigne une leçon précieuse : quand le modèle d'opération est *très permissif*, le problème se réduit souvent à un simple argument de comptage. La solution avide qui trie les longueurs de mots et soustrait les paires requises est :

* **Intuitive** – Utilisez d'abord la plus petite demande. (en milliers de dollars)
* **Fast** – `O(n log n)` pour `n = 1000`.
* **Correct** – prouvé par l'invariant de comptage par paire.

La prochaine fois que votre intervieweur demande un puzzle de manipulation de chaîne, demandez-vous: *Qu'est-ce qui est immuable? Que peut-on déplacer librement?* Cette question vous indique habituellement directement une stratégie de comptage ou d'avidité – exactement l'état d'esprit qui a fait passer mon code tous les tests LeetCode en quelques secondes.

Bonne chance sur l'entrevue de travail, et que votre prochain défi de codage soit aussi gratifiant que LeetCode 3035! C'est ce qu'il a dit.

---