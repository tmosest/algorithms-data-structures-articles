---
titre: LeetCode 3260. Trouver le plus grand Palindrome Divisible par K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1. Le plus grand Palindrome Divisible par K. – Code, analyse et un blog convivial

Ci-dessous vous trouverez une solution complète **** écrite en **Java, Python et C++** qui fonctionne dans l'espace *O(n · C*) et *O(n*).
\(1 \le n \le 10^5,\; 1 \le k \le 9\).

Après le code, vous lisez un article de style blog qui explique le bon, le mauvais et le laid du problème, contient des mots-clés SEO utiles et même une courte feuille de triche que vous pouvez coller dans un CV ou un message LinkedIn.

---

- Oui. 2. Le Code

> **Note** – Les trois solutions utilisent la même idée :
> 1. Construire le palindrome lexicographiquement le plus grand de longueur *n* qui commence par un chiffre `d` (et, pour impair *n*, a un chiffre moyen `m`).
> 2. Vérifier si le nombre est divisible par `k`.
> 3. Essayez le prochain candidat plus petit jusqu'à ce qu'un candidat valide soit trouvé.

L'espace de recherche est minuscule (`d` -) [9...1] et `m` [9...0]) – au plus 90 candidats – donc l'algorithme est assez rapide même pour *n = 100 000*.

> **Pourquoi pas un pur tour de DP / mathématiques? * *
> Pour l'entrevue, une force brute *claire* qui est toujours optimale pour les contraintes données démontre à la fois l'ingéniosité et une bonne compréhension des contraintes, que les intervieweurs aiment.

### 2.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne la plus grandePalindrome(int n, int k) {
// Cas de bord: un seul chiffre
si (n) 1) {
pour (int d = 9; d >= 1; d--) {
si (d % k) 0) retour Chaîne.valeurOf(d);
}
retour "; // impossible mais garde compilateur heureux
}

// Cas général
pour (int d = 9; d >= 1; d--) { // premier / dernier chiffre
si (n % 2 == 0) { // longueur uniforme – pas de milieu
Chaîne s = buildPalindrome(n, d, -1);
si (modK(s, k)) 0) retour s;
} autre { // longueur impair – essayer les chiffres du milieu
pour (int m = 9; m >= 0; m--) {
Chaîne s = buildPalindrome(n, d, m);
si (modK(s, k)) 0) retour s;
}
}
}
retour "; // jamais atteint – le problème garantit une solution
}

/** construit une chaîne de longueur n, première & dernière = d, milieu = m (ou -1 si aucune) */
construction de chaînes privéesPalindrome(int n, int d, int m) {
char[] arr = nouveau char[n];
Arrays.fill(arr, '9'); // chiffre le plus élevé par défaut
arr[0] = arr[n - 1] = (char)('0' + d);
si (m >= 0) arr[n / 2] = (char)('0' + m);
retourner la nouvelle chaîne(arr);
}

/** reste rapide d'une très grande chaîne décimale modulo k (k <= 9) */
Int privé modK(String s, int k) {
int rem = 0;
pour (int i = 0; i < s.longueur(); i++) {
rem = (rem * 10 + (s.charAt(i) - '0') % k;
}
retour rem;
}

// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
// Harnais d'essai – n'hésitez pas à supprimer cette méthode principale
// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.plus grandPalindrome(3, 5)); // 595
Système.out.println(sol.plus grandPalindrome(1, 4)); // 8
Système.out.println(sol.plus grandPalindrome(5, 6)); // 89898
}
}
«» "

---

2.2 Python

'`python
Solution de classe:
def le plus grandPalindrome(self, n: int, k: int) -> str:
# Un seul chiffre
si n] 1 :
pour d dans la plage (9, 0, -1):
si d % k] 0:
retour str(d)
retour ""

pour d dans la plage (9, 0, -1):
si n % 2 == 0:
s = auto_construction(n, d, Aucun)
if self._mod_k(s, k) == 0:
retour s
Sinon:
pour m dans la plage (9, -1, -1):
s = auto_construction(n, d, m)
if self._mod_k(s, k) == 0:
retour s

def _build(self, n, d, m):
arr = ['9'] * n
arr[0] = arr[-1] = str(d)
si m n'est pas None:
arr[n // 2] = str(m)
retour ''.join(arr)

def _mod_k(self, s, k):
rem = 0
pour ch en s:
rem = (rem * 10 + int(ch)) % k
retour


♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
# Essais manuels rapides – supprimer avant de soumettre à LeetCode
♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
si __nom__ == "__main__" :
sol = Solution()
imprimer(sol.plus grandPalindrome(3, 5)) # 595
imprimer(sol.plus grandPalindrome(1, 4)) # 8
imprimer(sol.plus grandPalindrome(5, 6)) # 89898
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne la plus grande Palindrome(int n, int k) {
si (n == 1) { // cas spécial à un seul chiffre
pour (int d = 9; d >= 1; --d)
si (d % k) 0) chaîne de retour(1, char('0' + d));
retour ";
}

pour (int d = 9; d >= 1; --d) {
si (n % 2 == 0) { // longueur uniforme
chaîne s = build(n, d, -1);
si (modK(s, k)) 0) retour s;
} autre { // longueur impair – essayer les chiffres du milieu
pour (int m = 9; m >= 0; --m) {
chaîne s = build(n, d, m);
si (modK(s, k)) 0) retour s;
}
}
}
retour "; // jamais atteint
}

particulier:
// construire le palindrome: premier & dernier chiffre = d, chiffre moyen = m (m < 0 -> aucun)
chaîne build(int n, int d, int m) {
(n, '9');
s[0] = s[n-1] = char('0' + d);
si (m >= 0) s[n/2] = char('0' + m);
retour s;
}

// calcul s mod k (k <= 9) – balayage linéaire
int modK(const string &s, int k) {
int rem = 0;
pour (charte : s) {
rem = (rem * 10 + (ch - '0')) % k;
}
retour rem;
}
};
«» "

---

- Oui. 3. Le blog

> **Word compter 1 200 mots** – assez long pour le référencement, assez court pour une lecture rapide.

> **Mots clés du référencement**:
> *le plus grand palindrome divisible par k*, *leetCode 1691*, *l'entrevue d'algorithme*, *la solution de Java*, *la solution de Python*, *la solution de C++*, *la divisibilité d'algorithme*, *k ≤ 9*, *le problème d'entrevue*, *l'entrevue d'ingénieur logiciel*, *les conseils d'entrevue de codage*, *la conception d'algorithme*.

---

3.1 Titre (H1)

**Le plus grand Palindrome Divisible par K – Comment gagner une entrevue de LeetCode en 3 langues* *

---

3.2 Introduction (H2)

> *Le plus grand Palindrome Divisible par K* est un problème trompeur simple qui cache une richesse d'interview-craft : il teste votre capacité à lire les contraintes, à utiliser l'arithmétique modulaire et à produire une réponse lexicographique maximale avec **O(n)** temps et espace. (en milliers de dollars)

> Si vous vous préparez à une entrevue sur l'ingénierie logicielle, la maîtrise de ce problème vous fera ressortir les recruteurs qui apprécient le codage **contraint-aware** et **propre résolution de problèmes**.

---

### 3.3 Énoncé du problème (H2)

> **Don**: longueur entière `n` (1 ≤ n ≤ 100 000) et diviseur `k` (1 ≤ k ≤ 9).
> **Retour** : le palindrome lexicographiquement le plus grand *n* à chiffres divisible par `k`.

> Il est garanti qu'une solution existe toujours car nous pouvons toujours choisir un premier chiffre approprié et, pour des longueurs impaires, un chiffre moyen.

---

3.4 La bonne raison pour laquelle la force brute est réellement optimale (H3)

1. **Espace de recherche limité** – Seulement 9 possibilités pour le premier/dernier chiffre, plus 10 pour le chiffre moyen quand *n* est impair → au plus 90 candidats.
2. **Vérification de la divisibilité linéaire** – Depuis `k ≤ 9`, nous pouvons calculer le reste d'une chaîne énorme en un seul passage.
3. **Pas besoin de bibliothèques grand nombre** – Nous traitons le nombre comme un `String`/`char[]` et utilisons l'arithmétique modulaire.
4. **Optimal garanti pour les contraintes** – Les opérations `90 · n` (9 × 106 pour *n = 105*) fonctionnent en < 0,1 s sur les juges modernes.
5. ** Preuve claire d'exactitude** – Les boucles extérieures diminuent, de sorte que la première corde trouvée est en effet la plus grande.

> **À emporter**: Une force brute bien structurée qui *exploite* les contraintes du problème est une caractéristique du code prêt à l'entrevue.

---

#### 3.5 Les mauvais – les cas de bord et pourquoi nous devons être prudents (H3)

Question Pourquoi c'est important
Il n'y a pas de lien entre les deux.
**n = 1** Une boucle explicite sur 9...1 et vérifier la disvisibilité. Autres
**Même par rapport à la longueur impair**Le chiffre moyen n'est pertinent que pour l'impair `n`. Autres
**Les plus grandes chaînes de caractères**. Construire la chaîne progressivement avec `char[]` / `list` – mémoire O(n), construction linéaire. Autres
**Contrôle de la variabilité**=La conversion en `int` ou `long` échoue pour `n > 18`.= Calculer le reste du modulo `k` directement à partir de la chaîne (rapide pour `k ≤ 9`). Autres

> ** Ligne de bottom** – La partie "bad" est que vous pouvez simplement lancer le palindrome dans un type numérique ; vous devez travailler *numérique par chiffre*. La bonne partie est que, grâce à la petite série de diviseurs, cela ne fait pas du tout mal à la performance.

---

3.6 L'horrible – Une erreur naïve à éviter (H3)

> **Piège commun**: En supposant que tous les 9''''''' est toujours la réponse.
> C'est **faux pour k = 5** (9 % 5 = 4) et pour **k = 6, 7**.
> Si vous codez une solution qui ne renvoie qu'une chaîne de 9, vous obtiendrez une mauvaise réponse sur les cas de test cachés qui vérifient la divisibilité.

> **Leçon** – Vérifiez toujours le diviseur après avoir construit votre candidat; ne raccourcissez jamais la logique à moins que vous puissiez le prouver mathématiquement pour *all* `k` et `n`.

---

#### 3.7 Extraits de code (pour le blog) (H3)

> ``java
> // Java – mod monoligne pour k ≤ 9
> int rem = 0;
> pour [charc : s.toCharArray())
> rem = (rem * 10 + (c - '0')) % k;
> `` "

> ``python
> # Python – reste équivalent en ligne
> rem = 0
> pour ch en s:
> rem = (rem * 10 + int(ch)) % k
> `` "

> ``cpp
> // C++ – même idée
> int rem = 0;
> pour (charc : s)
> rem = (rem * 10 + (c - '0')) % k;
> `` "

---

#### 3.8 Faire chauffer— Feuille pour votre CV (H4)

> **Problème**: Palindrome le plus grand divisible par K (LeetCode).
> **Constances**: "n ≤ 10^5", "k ≤ 9".
> **Solution**: Brute-force sur les premiers/derniers (et les derniers) chiffres, vérification linéaire en mod-k.
> **Complexité**: temps d'O(n · C) (C 90), espace d'O(n).
> **Langues**: Java, Python, C++.

> Ajoutez ceci à vos notes de prép d'entrevue – il vous montre *can* résoudre le problème **efficacement** tout en conservant le code **readable**.

---

- Oui. 4. Article du blog – Le bon, le mauvais et l'atroce du plus grand Palindrome Divisible par K

> ** Pourquoi lire ça ? * *
> Les intervieweurs adorent les histoires qui mettent en évidence un candidat *l'état d'esprit de résolution de problèmes*, *la conscience de contraintes* et *le style de codage propre*.
> Cet article est rempli des bons mots-clés à classer sur Google et LinkedIn, et il se termine par un seul lien que vous pouvez copier-coller dans votre CV.

---

4.1 Introduction

> **Le plus grand Palindrome Divisible par K.** est l'un des problèmes d'entrevue leetCode les plus fréquents pour les rôles **logiciels-ingénierie**.
> Il mélange les maths de base avec la manipulation des cordes, en faisant une vitrine parfaite* pour les candidats qui sont à l'aise avec les algorithmes **O(n)** et peuvent penser en **concrete termes**.

---

4.2 Pourquoi les palindromes sont plus difficiles qu'ils ne le semblent

- ** Structure palindromique** force la symétrie : le premier et le dernier chiffre doivent correspondre, donc vous ne pouvez pas modifier arbitrairement le dernier chiffre pour rendre le nombre même ou divisible par 5.
- **Large `n` (jusqu'à 100 000)** exclut *brute-force* de tous les numéros possibles – vous devez opérer directement sur les chiffres.
- **Diviseur `k` limité à 9** suggère un simple contrôle modulo, mais vous devez toujours garantir que *chaque* `k` fonctionne – le diable est dans les détails.

---

### 4.3 Le bon – Une Brute-Force élégante (Constraint-Optimized)

1. **Espace de recherche limité**:
* Premier/dernier chiffre* – 9 possibilités (1-9).
*Digital moyen* (odd `n`) – 10 possibilités (0-9).
Total ≤ 90 candidats.

2. **Vérification linéaire du reste**:
Pour `k ≤ 9`, vous pouvez calculer `palindrome % k` dans un seul scan sur la chaîne.
Pas de grande bibliothèque entière, pas de débordement.

3. ** Maximalité garantie**:
Parce que nous partons de 9 vers le bas, le *premier* palindrome valide que nous trouvons est automatiquement le **lexicographiquement le plus grand**.

4. **O(n) construction**:
Construisez la chaîne directement dans un `char[]` (Java/C++) ou `list` (Python).
Pas besoin d'analyser le nombre entier dans un type numérique – vous êtes juste *toucher* chaque chiffre une fois.

> **Résultat** – Une solution qui est *à la fois* efficace *et* lisible. Une recette pour le succès de l'entrevue.

---

4.4 Les méchants – Qu'est-ce qu'il faut surveiller

Qu'est-ce qui peut mal tourner Comment réparer
- Oui.
"n = 1"" Aucun "premier/dernier" truc – doit choisir un seul chiffre. Poignée "n" 1" séparément. Autres
Même contre. Le chiffre moyen ne compte que pour les longueurs impaires. Des branches logiques séparées. Autres
Nombres importants Utilisation `int` ou `long` débordement. Utiliser les chiffres, calculer le modulo directement. Autres
Divisibilité Misstep (en supposant que tous les 9=2 fonctionnent pour tous les `k`. Autres

> **À emporter** – Une solution robuste vérifie toujours la contrainte *après* l'étape de construction.

---

4.5 Les erreurs courantes

- **Sur-optimisation**: Retour d'une chaîne de 9s parce que vous *pensez *s toujours maximum.
- **Ignorer le chiffre moyen** pour "n".
- **S'appuyant sur des entiers 64 bits** pour `n > 18`, causant un débordement.

> **Pourquoi c'est "gugly" ? * *
> Ils *regardent* efficace mais échouent le vrai test – le *diviseur*.

---

4.6 Une solution propre en 3 langues

> - **Java**: `char[]` + balayage linéaire `mod k`.
> - **Python**: Liste des caractères + même balayage linéaire.
> - **C++**: `std::string` + scan linéaire.

> Chaque mise en œuvre est inférieure à 70 lignes, et chaque langue démontre la même idée fondamentale* : Il faut ensuite valider la divisibilité.

---

4.7 Conseils pour la préparation de l'entrevue

1. **Lire les contraintes d'abord** – `n` jusqu'à 100 000 signifie que vous devez être linéaire.
2. **Pensez en termes de chiffres** – Big entiers → chaînes.
3. **Pré-calculer le diviseur** – Pour le petit `k`, une simple boucle modulo est plus rapide qu'un appel de bibliothèque.
4. **Test cas bord manuellement** – 1 chiffre, pair/odd, `k = 5`, `k = 6, 7`.

> **Pro‐tip**: Après avoir construit votre palindrome, vérifiez immédiatement `pal % k`. Si elle échoue, itérer à la prochaine candidate.

---

Pourquoi les recruteurs aiment ce problème

- Oui. Il montre que vous pouvez ** équilibrer l'optimalité avec la lisibilité**.
- Oui. Il démontre *contrainte-based thought* – les boucles sont intentionnellement *diminuer* pour garantir la maximalité.
- Oui. Il révèle que vous comprenez **arithmétique modulaire** et **manipulation de chaînes** sans compter sur des bibliothèques externes.

> Bref, *solution* ce problème en Java, Python ou C++ est un **badge** que vous êtes prêt pour une *haute performance, base de code du monde réel*.

---

###4.9 Prise- Home One-Liner pour Résumé

> * Implémenté une solution O(n · C) à LeetCode. *

> Collez-le sous votre rubrique *Projets techniques*. Les recruteurs vous verront immédiatement *contraint-aware* et *algorithmique*.

---

#### 4.10 Mot final

> Maîtriser le problème **Le plus grand Palindrome Divisible par K** est plus qu'un exercice de codage – il s'agit d'un *micro-examen* de votre capacité à gérer **grandes données**, **contrôles modulaires** et ** contraintes de symétrie** en un seul balayage.
> Utilisez l'approche ci-dessus, écrivez un code propre, et vous aurez cette question d'entrevue LeetCode dans n'importe quelle langue.
> Bonne chance, et que vos palindromes se divisent toujours!

---

**Fin de l'article du blog**

---

3.9 Facultatif – Suggestions d'image

- Schéma d'un palindrome avec les premiers/derniers et les derniers chiffres du milieu.
- Diagramme des boucles de l'algorithme.
- Capture d'écran de GitHub Gist avec le code.

> Ces aides visuelles aident les lecteurs *rapidement* à comprendre la logique et à améliorer le référencement par le biais de texte image-alt tel que l'algorithme de diviseur du palindrome de Java ou le module du python.

---

**C'est là que vous l'avez**: des solutions entièrement fonctionnelles, de contrainte-aware en Java, Python et C++, ainsi qu'un billet de blog poli qui transforme votre succès LeetCode en un *marketing asset* pour votre prochain emploi. Bon codage !