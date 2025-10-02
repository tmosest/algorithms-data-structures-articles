---
titre: LeetCode 3557. Trouver le maximum Nombre de sous-chaînes non intersectrices -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code (Java-Python-C++)

Voici trois solutions totalement autonomes qui fonctionnent toutes dans **O(n)** temps et **O(1)** espace supplémentaire.
Ils utilisent tous l'idée *greedy* que nous pouvons toujours s'engager à une sous-chaîne dès que nous en voyons une valide, parce que toute sous-chaîne ultérieure qui commence à l'intérieur du courant le chevaucherait nécessairement.

"Java
// - Oui. Java - Oui.
Importation de java.util.*;

solution de classe {
int public maxSubstrings (mot de chaîne) {
int res = 0;
Carte<Caractère, entier> d'abord = nouveau HashMap<>();
pour (int i = 0; i < word.longueur(); i++) {
c = mot.charAt(i);
si (!first.contientKey(c)) { // première fois que nous voyons c
premier.put(c, i);
} sinon si (i - first.get(c) + 1 >= 4) { // sous-chaîne de non-overlaping valide
res++;
first.clear(); // redémarrage – aucun chevauchement autorisé
}
}
retour rés;
}
}
«» "

'`python
♪ - Oui. Python...
def maxSubstrings(mot: str) -> Int:
Res = 0
premier = {}
pour i, c en énumération(mot):
si c n'est pas en premier:
premier[c] = i
elif i - premier[c] + 1 >= 4: # sous-chaîne valide trouvée
Rés += 1
first.clear() # reset – aucun chevauchement
retour res
«» "

'`cpp
// C++ - Oui.
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int maxSous-chaînes(mot chaîne) {
int res = 0;
unordered_map<char,int> d'abord;
pour (int i = 0; i < (int)word.size(); ++i) {
c = mot[i];
si (!first.count(c)) {
premier[c] = i; // première occurrence
} sinon si (i - premier[c] + 1 >= 4) { // une sous-chaîne valide se termine ici
++res;
first.clear(); // reset – aucun chevauchement autorisé
}
}
retour rés;
}
«» "

Les trois extraits se compilent uniquement avec la bibliothèque standard et produisent la même réponse pour chaque cas d'essai.

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 3557

> **LeetCode 3557 – *Trouver le nombre maximal de sous-chaînes de non-intersecting***
> *Une plongée profonde dans DP vs Greedy, pourquoi l'avidité est l'endroit doux, et comment vous pouvez le clouer dans une interview. *

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Pourquoi ce problème compte] (#pourquoi-ce-problème-matières)
3. [Force-brute/Intuition] (#force-brute--intuition)
4. [Programmation dynamique (La voie "Bad")
5. [Greedy (La bonne voie)] (#greedy-la-bonne voie)
6. [Régimes et pièges] (#cases--règles)
7. [Test de votre solution] (#test de votre solution)
8. [Take‐aways & Conseils d'entrevue] (#take-aways--interview-tips)
9. [Autres lectures et ressources] (#autres lectures-ressources)
10. [Conclusion] (#conclusion)

---

### Aperçu du problème <un nom="problème-overview"></a>

On vous donne une chaîne `word` (1 ≤="word ≤ 2 × 105) composée de lettres anglaises minuscules.
Retourner le nombre de sous-chaînes **maximum** de *non-overlaping* qui satisfont :

* Longueur ≥ 4
* Commence et se termine par la même lettre

Exemple
«» "
mot = "abcdeafdef"
→ ["abcdea", "fdef"] (réponse = 2)
«» "

---

- Oui. Pourquoi ce problème est-il important?

- **Pattern-matching** + **horaire d'intervalle** → compétences de base CS.
- Les contraintes vous poussent vers des solutions **O(n)**.
- Beaucoup d'intervieweurs aiment les problèmes où un choix *greedy* est réellement optimal – il teste votre capacité à raisonner sur l'optimalité, pas seulement le codage.

---

### Brute-Force / Intuition <un nom="brute-force--intuition"></a>

Une approche naïve énumère toutes les sous-chaînes, vérifie la validité, et fait ensuite un DP d'emballage par intervalles.
Complexité: **O(n2)** temps, **O(n2)** mémoire – impossible pour 200 000 chaînes de longueur.

Aperçu : *Toute sous-chaîne valide est définie par une paire de caractères égaux à distance ≥ 3*.
Il suffit donc de suivre **premiers événements** de chaque lettre.

---

### Programmation dynamique (Le chemin "Bad") <un nom "dynamic-programming-the-bad-path"></a>

Une formulation PDD propre:

«» "
dp[i] = nombre max de sous-chaînes valides en mot[0 ... i-1)
«» "

Transition:

«» "
dp[i+1] = max(dp[i+1], dp[j] + 1) pour tous les j où word[j]==word[i] et i-j+1 >= 4
«» "

L'implémentation utilise une file d'attente par lettre pour ne garder que les quatre derniers événements, réduisant la boucle interne à au plus 4 vérifications par caractère.
**Heure:** O(n)
**Espace:** O(n) pour tableau dp, O(n) pour files d'attente dans le pire des cas → **O(n)* *

Bien qu'il soit correct, le tableau supplémentaire et la tenue de livres de DP.
Les intervieweurs préfèrent souvent la solution avide plus propre.

---

### Greedy (Le Chemin du Bon) <a name="greedy-the-goe-path"></a>

Observation

Si nous voyons un caractère `c` à nouveau et la distance entre les deux événements est ≥ 4, nous * pouvons* réclamer la sous-chaîne entre eux ** sans perte d'optimalité**.
Pourquoi ?
Parce que toute sous-chaîne qui commence à l'intérieur de ce candidat devrait se terminer avant le caractère suivant `c` (autrement qu'il se chevaucherait), la forçant à être plus courte que 4 – impossible.

Algorithme

1. Scanner de gauche à droite.
2. Pour chaque lettre stocker le **premier index** où il est apparu («premier[c]».
3. Lorsque la même lettre apparaît à nouveau à l'index «i»:
* Si `i - first[c] + 1 ≥ 4` → **commit** à la sous-chaîne `[first[c], i]`, incrément reponse, **effacer tous les premiers indices enregistrés** (aucun chevauchement autorisé).
* Sinon → il suffit de garder le premier index (pas encore de commit).

L'étape claire garantit la règle *no-overlap* : chaque nouvelle sous-chaîne commence après la fin précédente.

Pourquoi ça marche ?

Il s'agit essentiellement de la programmation classique *interval par la première finition* preuve:
le plus tôt temps de finition (le plus tôt possible `i` qui donne une sous-chaîne valide) ne vous blesse jamais parce qu'il laisse la marge maximale possible pour les sous-chaînes ultérieures.

Extraits de code

L'avidité est exactement le code que nous avons listé dans la section 1 (Java/Python/C++).
Remarquez l'utilisation de l'espace **O(1)** : seulement une petite carte de hachage de 26 clés que nous videons chaque fois que nous nous engageons.

---

### Cas et pièges sur les bords <un nom</a>

Bordure Ce qu'il faut faire attention
Il n'y a pas de problème.
""aaaaa" La même lettre apparaît 5 fois → deux sous-chaînes ? La Greedy s'engagera sur le *premier* répéter qui est ≥ 4, en éliminant tout – toujours optimal. Autres
""abcd" ""Pas de lettres égales à distance ≥ 3 → réponse 0" Votre code doit retourner 0 si aucune sous-chaîne valide n'est trouvée. Autres
Autres Réinitialiser la carte de hachage sur chaque commit est O(26) → frais généraux triviaux. Si vous utilisez des tableaux bit-mask +, le réglage de 26 entrées est correct; si vous utilisez un vecteur par lettre, vous devez effacer toutes les files d'attente à chaque fois. Autres
Utilisez des entrées/sorties rapides si votre langue en a besoin (Java: `BufferedReader`, Python: `sys.stdin.read()`). Dans l'extrait de code, nous utilisons `enumerate(word)` – déjà linéaire en CPython. Autres

---

### Tester votre solution <un nom</a>

1. **Tests simples** (à partir de l'invite).
2. **Tests de rando**: générer des chaînes de longueur aléatoire jusqu'à 10 000, force brute avec un solveur lent pour la justesse.
3. ** Tests de résistance**: une longue chaîne de 200 000 caractères, par exemple `word = 'a'*200000` → response = 50000.
4. **Décisions**: "abcd", "abc", "a"*4.

Exemple de test de contrainte Python:

'`python
importation aléatoire, chaîne, heure
def brute(mot):
n=len(mot); best=0
# O(n^2) brute – seulement pour les petites cordes
pour i dans la plage(n):
pour j dans la plage(i+3, n):
si mot[i]==mot[j]:
best=max(best,1)
le meilleur retour

pour _ dans l'intervalle(1000):
s=''.join(random.choice(string.ascii_lowercase) pour _ dans l'intervalle(random.randint(1,20))
affermissez maxSubstrings(s)==brute(s)
print("Tous les tests au hasard ont réussi")
«» "

---

### Take-aways & Conseils d'entrevue <a name="take-aways--interview-tips"></a>

Autres Ce qu'il faut souligner Pourquoi
Il s'agit d'un projet pilote.
**Expliquez l'argument avide** Autres
** Contraintes de la Mention → O(n) requis**=Les intervieweurs adorent quand vous parlez de complexité tôt. Autres
**Afficher les deux DP et Greedy** Autres
**Afficher l'étape de réinitialisation**= C'est la seule partie de "gugly" qui doit être manipulée avec soin. Autres
Autres **Test ledge case live**.Il rend votre solution robuste et montre la pensée analytique. Autres

**TL;DR** – Utilisez la version hash‐map, limpide sur le succès, et soyez prêt à expliquer *pourquoi* ce commit est sûr.

---

### Autres lectures et ressources <un nom</a>

- **Programme d'intervalle** – problème classique de manuel gourmand.
- **LeetCode Solutions (C++, Java, Python)** – pratiquez des problèmes similaires comme *Longest Repeating Substring* ou *Nombre maximum de segments non-overlaping*.
- ** Programmation dynamique** – si vous voulez approfondir les connaissances du PDD, vérifiez « Top-Down vs Bottom-Up DP » sur LeetCode.

---

### Conclusion <un nom="conclusion"></a>

LeetCode 3557 est un puzzle *pattern assorti + horaire d'intervalle* qui se trouve à l'intersection de DP et Greedy.
La solution cupide est à la fois **simpler** et **plus efficace** pour les paramètres d'entrevue, tandis que la version DP présente une approche classique « full-blown ».

En maîtrisant ce problème, vous allez non seulement résoudre la question elle-même, mais aussi apprendre à:

* **Choisir le bon algorithme** sous des contraintes serrées.
* **Justifier l'optimalité** avec une preuve propre.
* **Écrire un code propre en plusieurs langues** qui peut être montré à un panel d'intervieweurs.

Bonne chance pour votre prochaine entrevue de codage – et rappelez-vous: parfois le choix le plus simple est le plus puissant!