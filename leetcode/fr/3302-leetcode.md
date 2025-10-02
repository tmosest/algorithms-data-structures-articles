---
titre: LeetCode 3302. Trouver la séquence la plus lexicographiquement la plus petite valide -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3302. Trouver la séquence la plus lexicographiquement la plus petite valide
**Java / C++ / Python – Une solution d'avidité qui fonctionne en O(n+m)* *

---

TL;DR

Langue Heure Espace
- C'est quoi ?
*Java * O(n+m)
*C++**= O(n+m)= O(m)=
*Python * O(n+m)

*`n = mot1.longueur`, `m = mot2.longueur` (m < n ≤ 3·105)*

L'idée clé :
1. **Précalculer l'index le plus droit dans `word1` qui peut correspondre à chaque suffixe de `word2`. **
2. **Scan `word1` de gauche à droite, cueillir avec cupidité des indices qui correspondent ou sont sûrs de sauter le caractère `word2` actuel** (une seule fois).
3. La première fois que nous pouvons sauter un personnage, nous devons le faire immédiatement – ce qui garantit la minimalité lexicographique.

---

Réévaluation des problèmes

On vous donne deux chaînes minuscules, `word1` et `word2`.

- Une chaîne `x` est **presque égale** à `y` si vous pouvez changer **au plus un** caractère de `x` de sorte qu'il devient identique à `y`.
- Une séquence d ' indices " seq " est **valable** si:
1. `seq` est trié en montée.
2. Concaténation du mot1[seq[i]» dans l'ordre donne une chaîne qui est presque égale à `word2`.

Retournez la séquence valide *lexicographiquement la plus petite* (pour les indices).
Si aucune séquence valide n'existe, retournez un tableau vide.

> **Note** : Le tableau le plus petit de manière lexicographique signifie que nous comparons les séquences élément par élément, et non la chaîne résultante.

---

Les contraintes

Paramètre Gamme
C'est quoi ?
"1 ≤ word2.longueur < word1.longueur ≤ 3·105"
Personnages

---

Le point de vue sur l'avidité

Imaginez que nous balayons `word1` de gauche à droite et voulons construire la séquence.

1. **Si le caractère actuel est égal à `word2[j]`, nous *must* le prendre** – choisir un match ultérieur ne ferait que déplacer les indices à droite et ne produirait jamais un tableau plus petit.
2. **S'il ne correspond pas** nous pouvons *skip* le `word2[j]` **une fois** (changement de caractère).
Mais nous ne pouvons le sauter que si nous pouvons encore terminer le reste de `word2` en utilisant le suffixe de `word1` qui suit la position actuelle.

Nous avons donc besoin, pour chaque position `i` dans `word1`, de la position *earliest* dans `word2` qui peut être jumelée avec le suffixe `word1[i...]`.
C'est l'astuce qui nous permet de décider en O(1) si sauter est sûr.

---

Comment fonctionne l'algorithme

1. **Pass en arrière – build `last[j]`**
«dernier[j]» stocke l'index *rightmost* dans `word1` qui peut correspondre à `word2[j]`.
Scanner `word1` de droite à gauche; chaque fois que nous voyons `word1[i] == word2[j]`, définir `last[j] = i` et déplacer `j` à gauche.

2. **Passer vers l'avant – construire avide* *
Marcher `word1` à nouveau (à gauche → à droite).
Gardez deux variables :
* `j` – position actuelle dans `word2`.
* `skip` – que nous ayons déjà utilisé l'inadéquation autorisée (0 ou 1).

Pour chaque «i»:
- **Case 1 – Correspondance directe**: `word1[i] == word2[j]` → prendre `i`, "j++".
- **Case 2 – Saut autorisé** (`skip == 0`) et il est *safe* de sauter `word2[j]`:
*Sûre* signifie que le caractère suivant de `word2` (`word2[j+1]`) peut encore être assorti d'un indice ultérieur.
Cela équivaut à `i < last[j+1]` (ou si `j` est le dernier index, nous sommes libres de sauter).
Si la condition se maintient, prenez `i`, définissez `skip = 1`, `j++`.

3. **Termination**
Si nous avons réussi à correspondre à tous les caractères `m` (`j == m`), retournez les indices collectés.
Sinon, retournez un tableau vide.

---

Modèle de preuve d'exactitude

1. **Feasibility** – L'algorithme n'ajoute un index que s'il correspond au caractère `word2` actuel ou s'il s'agit d'un saut sûr.
*Safe skip* garantit que le reste de `word2` peut encore être assorti, de sorte que la chaîne finale sera presque égale à `word2`.

2. ** minimalité lexicographique** –
* Tout index choisi plus tôt qu'un match plus tard sera plus petit, donc nous ne reportons jamais un match qui est possible.
* La seule fois que nous reportons est de sauter un personnage.
Nous sautons *seulement quand il est sûr* et *immédiatement* (la première fois qu'un saut est possible).
Passer plus tard augmenterait le premier indice différent dans la séquence résultante, violant ainsi la minimalité lexicographique.

3. **Unicité de la séquence** –
Les choix avides sont forcés: une fois qu'un match direct existe, nous devons le prendre; si nous sautons, le nombre de sauts devient 1 et nous ne pourrons plus jamais sauter.
Par conséquent, l'algorithme produit une séquence unique qui est lexicographiquement minimale parmi toutes les séquences valides.

---

Analyse de complexité

Autres Phase du temps Espace
C'est pas vrai.
C'est la dernière fois que l'on s'arrête. Autres
O(m) (tableau de résultats)
**O(n + m)**

"n" peut être jusqu'à 300 000, ce qui est bien dans les limites des CPU modernes.

---

Pièges communs

Une erreur Pourquoi elle échoue Comment éviter
C'est pas vrai.
**Utiliser le premier match pendant le scan vers l'avant**=Il pourrait être mal si un personnage plus tard peut être sauté en toute sécurité plus tôt. Pré-calculer le dernier et l'utiliser pour vérifier la sécurité avant de sauter. Autres
**Passer chaque fois que vous voyez une erreur** Utiliser le tableau `dernier` pour garantir que le suffixe contient toujours une correspondance pour le suffixe restant de `word2`. Autres
**Les erreurs de calcul sont incorrectes**. Autres Traitez le dernier index spécialement : vous pouvez le sauter à tout moment parce qu'il n'y a rien après. Autres
**Utiliser trop de mémoire** Enregistrez seulement `dernier` de la taille `m` (longueur suffixe), et non un tableau de la taille `n`. Autres

---

Mise en œuvre du code

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe {
public int[] validSéquence(String word1, String word2) {
int n = word1.length(), m = word2.length();
int[] last = new int[m]; // last[j] = index le plus droit dans word1 qui correspond à word2[j]
les tableaux.fill(dernier, -1);

// Passage en arrière
j = m - 1;
pour (int i = n - 1; i >= 0 && j >= 0; i--) {
si (word1.charAt(i) == word2.charAt(j)) {
last[j] = i;
J--;
}
}

// Passer vers l'avant
j = 0;
Int skip = 0;
int[] res = nouvelle int[m];
int pos = 0; // position dans res

pour (int i = 0; i < n && j < m; i++) {
si (word1.charAt(i) == word2.charAt(j)) { // correspond directement
res[pos++] = i;
j++;
} sinon si (skip) 0) { // envisager de sauter
le booléen sans danger = (j == m - 1)
si (sûre) {
res[pos++] = i;
skip = 1;
j++;
}
}
}

retour (j == m) ? res : nouveau int[0];
}
}
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> validSequence(string word1, string word2) {
int n = word1.size(), m = word2.size();
vector<int> last(m, -1); // positions les plus droites

// Passage en arrière
j = m - 1;
pour (int i = n - 1; i >= 0 && j >= 0; --i) {
si (mot1[i] == mot2[j]) {
last[j] = i;
--j;
}
}

// Passer vers l'avant
vecteur<int> rés;
res.reserve(m);
j = 0;
Int skip = 0;
pour (int i = 0; i < n && j < m; ++i) {
si (mot1[i] == mot2[j]) {
res.push_back(i);
++j;
Sinon si (!skip) {
bool safe = (j == m - 1).
si (sûre) {
res.push_back(i);
skip = 1;
++j;
}
}
}

retour (j == m) ? res : vector<int>();
}
};
«» "

C'est vrai. Python

'`python
Solution de classe:
def validSequence(self, word1: str, word2: str) -> Liste[int]:
n, m = len(mot1), len(mot2)
dernier = [-1] * m

# Pass en arrière : calculer les indices les plus proches
j = m - 1
pour i dans la fourchette(n - 1, -1, -1):
si j >= 0 et word1[i] == word2[j]:
last[j] = i
J = 1

# Pass avant : construction gourmande
res = []
j = 0 # indice courant dans word2
skip = 0 # 0 → aucune inadéquation utilisée

pour i, ch en énumération(mot1):
si j >= m:
pause
si ch == word2[j]:
res.append(i)
j += 1
elif skip == 0:
# Sûr pour sauter si nous pouvons encore égaler le suffixe restant
sécurité = (j == m - 1) ou (i < last[j + 1])
en cas de sécurité:
res.append(i)
skip = 1
j += 1

retour res si j == m autre []
«» "

Les trois solutions utilisent la logique *même* ; les seules différences sont des détails syntaxiques spécifiques au langage.

---

## --Qu'est-ce que ce problème apprend

Aspect du bien
- C'est quoi ?
**Difficulté**= Question d'entrevue de 2 heures= Nécessite un raisonnement prudent de l'O(n)= 300 000-char entrées voyage naïf DP ou récursion=
Un seul skip n'est possible que si le reste de `word2` correspond encore. Autres
**Les erreurs communes**=Le fait de prendre l'index *premier* correspondant est faux; vous devez reporter seulement pour *safe* skips===Supprimer arbitrairement donne un mauvais résultat lexicographique==Ne pas gérer le dernier caractère de `word2` (skip autorisé une seule fois)===
Autres **Ce que les intervieweurs aiment** , temps linéaire, mémoire O(m), raisonnement clair et gourmand. Démontrer vous pouvez gérer d'énormes entrées sans récursion

---

Comment cela aide votre travail de chasse

*Pourquoi maîtrise-t-on ce genre de problème avide d'une tactique de career-boost? *

1. **Entrevue–Amis** – De nombreux entretiens techniques demandent des solutions *O(n)* sur les problèmes linéaires.
Démontrer que vous pouvez penser en termes de *deux passes* et *sécurité précalculée* vous montre que vous êtes à l'aise avec des algorithmes à temps optimal.

2. **L'échelle mentale** –
Des entreprises comme Google, Facebook et Amazon mettent l'accent sur la taille des données dans les millions.
Affichage vous pouvez traiter 3·105 caractères en dessous d'une seconde (10 ms) signaux que vous allez écrire un code prêt à la production.

3. **Expliquer et Démo** –
Lorsque vous traversez la solution au cours d'une entrevue, narrez la *perspective de confiance*, la *vérification de sécurité* et la *garantie lexicographique*.
Cela démontre la clarté de la pensée – une compétence soft-skill précieuse dans les comités d'embauche.

---

Référence rapide – Extraits de code de préparation à la pâte

### Java

"Java
public int[] validSéquence(String word1, String word2) {
int n = word1.length(), m = word2.length();
int[] last = nouvelle int[m];
les tableaux.fill(dernier, -1);

// Passage en arrière
j = m - 1;
pour (int i = n - 1; i >= 0 && j >= 0; i--) {
si (word1.charAt(i) == word2.charAt(j)) {
last[j] = i;
J--;
}
}

// Passer vers l'avant
int[] res = nouvelle int[m];
int idx = 0, saut = 0, j2 = 0;
pour (int i = 0; i < n && j2 < m; i++) {
si (word1.charAt(i) == word2.charAt(j2)) {
res[idx++] = i;
j2++;
} sinon si (skip) 0) {
booléen sans danger = (j2 == m - 1)
si (sûre) {
res[idx++] = i;
skip = 1;
j2++;
}
}
}
retour (j2 == m) ? res : nouveau int[0];
}
«» "

C++

'`cpp
vector<int> validSequence(string word1, string word2) {
int n = word1.size(), m = word2.size();
vecteur<int> dernier(m, -1);

// Passage en arrière
j = m - 1;
pour (int i = n - 1; i >= 0 && j >= 0; --i) {
si (mot1[i] == mot2[j]) {
last[j] = i;
--j;
}
}

// Passer vers l'avant
vecteur<int> rés;
res.reserve(m);
j = 0;
Int skip = 0;
pour (int i = 0; i < n && j < m; ++i) {
si (mot1[i] == mot2[j]) {
res.push_back(i);
++j;
Sinon si (!skip) {
bool safe = (j == m - 1).
si (sûre) {
res.push_back(i);
skip = 1;
++j;
}
}
}

retour (j == m) ? res : vector<int>();
}
«» "

Python

'`python
def validSequence(self, word1: str, word2: str) -> Liste[int]:
n, m = len(mot1), len(mot2)
dernier = [-1] * m

Passage en arrière
j = m - 1
pour i dans la fourchette(n - 1, -1, -1):
si j >= 0 et word1[i] == word2[j]:
last[j] = i
J = 1

# Passer vers l'avant
res, j, skip = [], 0, 0
pour i, ch en énumération(mot1):
si j >= m:
pause
si ch == word2[j]:
res.append(i)
j += 1
elif skip == 0:
sécurité = (j == m - 1) ou (i < last[j + 1])
en cas de sécurité:
res.append(i)
skip = 1
j += 1

retour res si j == m autre []
«» "

---

TL;DR

- **Problème:** Trouvez un tableau d'index lexicographique le plus petit, permettant au plus une inadéquation.
- **Solution :** Deux passes linéaires, pré-calculer les positions les plus sûres ("dernier") et faire appliquer le contrôle de sécurité avant un seul saut.
- **Complexité:** "O(n)" temps, "O(m)" mémoire.
- **À emporter :** La maîtrise de ces modèles gourmands stimule la performance des interviews et démontre l'évolutivité de la pensée, essentielle à tout rôle technologique de premier ordre.

---

Mots clés (pour les lecteurs de blog)

`#Algorithmes #Greedy #Interview #LinearTime #TwoPassAlgorithm #ScalableCode #Java #C++ #Python #TechInterviewTips #BigData #InterviewPréparation "

Bon codage et bonne chance pour votre prochaine interview! C'est ce qu'il a dit