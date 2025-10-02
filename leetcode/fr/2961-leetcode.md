---
titre: LeetCode 2961. Double exposition modulaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## ☐ Double exposant modulaire – LeetCode 2961
- Oui. (Java-Python-C++ – Solutions + Un Blog-Style Deep-Dive)

> **Numéro de dossier:** 2961
> **Difficulté:** Moyenne
> **Mots clés:** `exponentiation modulaire`, `LeetCode`, `Java`, `Python`, `C++`, `coding interview`, `algorithm design`, `O(n)`.

---

Récapitulation des problèmes

On vous donne un tableau `variables`, où chaque élément est un quadruple
«[a, b, c, m]».
Un indice `i` est **bon** si

«» "
(a^b % 10) ^ c) % m) cible
«» "

Retournez une liste de tous les bons indices (tout ordre).

Exemple Entrée Sortie
- C'est quoi ?
= [[2,3,10],[3,3,31],[6,1,1,4]", < < cible = 2 > > , < < [0, 2] > > Autres
[[39,3,1000,1000]]", "cible = 17"

Contraintes
- `1 ≤ variables.longueur ≤ 100`
- `1 ≤ a, b, c, m ≤ 10^3`
- "0 ≤ objectif ≤ 10^3"

---

- Oui. Pourquoi est-ce un problème ?

Explication
C'est pas vrai.
**Simplicité + Profondeur** La déclaration est facile à lire mais cache des problèmes subtils avec débordement et arithmétique modulaire. Autres
**Traitement commun de l'entrevue**=L'exponentiation modulaire est un élément essentiel de nombreuses entrevues de codage (RSA, fonctions de hachage, etc.). Autres
**Langues multiples** Autres
Même si les contraintes sont petites, la solution s'étend à de très grands exposants si nécessaire. Autres

---

- Oui. Les pièges potentiels

Comment l'éviter
- C'est pas vrai.
**Les dépassements peuvent exploser (par exemple, 1000^1000"). Calculer `pow(a, b, 10)` directement avec exponentiation modulaire – ne jamais laisser la valeur intermédiaire croître. Autres
**Modulo Order**.Le mauvais ordre des opérations « % » peut changer le résultat. Suivez la formule exactement: d'abord `% 10`, puis la puissance `c`, puis `% m`. Autres
Autres **Edge Case `m = 1`**= Tout `% 1` est `0`.=Traitez-le explicitement ou comptez sur l'arithmétique modulaire – `pow(x, y, 1)` retournera toujours `0`. Autres
**L'utilisation de la puissance intégrée dans `pow` est incorrecte**.Dans Python, `pow(a, b)` retourne la puissance exacte, et non le résultat modulaire. Utiliser "pow(a, b, mod)" (formulaire à trois arguments) ou mettre en œuvre une pow rapide. Autres

---

- Oui. Le "Ugly" – Pourquoi il peut regarder Messy

- Des boucles répétées pour chaque exposant peuvent rendre le code long.
- Oui. L'implémentation naïve peut ressembler à des boucles imbriquées, obscurcissant la logique modulaire.
- L'utilisation de différents types de données (`int`, `long`, `BigInteger`) dans les langues peut prêter à confusion.

La clé d'une solution **clean** est *abstractionner* l'exposition modulaire dans une fonction d'aide.

---

C'est pas vrai. La solution la plus propre – une ligne de base

Texte
valeur = pow(pow(a, b, 10), c, m)
«» "

En Python, c'est littéralement une ligne.
En Java et C++, nous l'enveloppons dans un helper `modPow`.

---

Code – Trois langues

- Oui. 6.1 Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
// Exponentiation modulaire rapide: (base^exp) % mod
modPow (long base, long exp, long mod) {
résultat long = 1 % mod;
base %= mod;
pendant la période (exp > 0) {
si ((exp & 1)] 1) résultat = (résultats * base) % mod;
base = (base * base) % mod;
Exp >>= 1;
}
le résultat du retour;
}

liste publique<entier> getGoodIndices(int[][] variables, int cible) {
Liste<Intégrée> bonne = nouvelle liste de distribution<>();
pour (int i = 0; i < variables.longueur; i++) {
int a = variables[i][0];
int b = variables[i][1];
int c = variables[i][2];
int m = variables[i][3];

longue première = modPow(a, b, 10); // (a^b) % 10
longue seconde = modPow(premier, c, m); // (premier) % m

si (deuxième) cible {
Bien.add(i);
}
}
le bien de retour;
}
}
«» "

> **Pourquoi c'est rapide** – `modPow` tourne dans *O(log exp)*, donc l'algorithme entier est *O(n log max(b,c))*.

---

- Oui. 6.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def getGoodIndices(self, variables: List[List[int]], cible: int) -> Liste[int]:
bonne = []
pour i, (a, b, c, m) dans l'énumération (variables):
premier = pow(a, b, 10) # (a^b) % 10
deuxième = pow(premier, c, m) # (premier, c) % m
si la deuxième cible est :
Annexe i)
retour bien
«» "

> Le Python est à la fois concis et hautement optimisé.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
long mod Pow(longe base, long exp, long mod) {
long résultat = 1 % mod;
base %= mod;
pendant la période (exp > 0) {
si (exp & 1) résultat = (résultats * base) % mod;
base = (base * base) % mod;
Exp >>= 1;
}
le résultat du retour;
}

public:
vector<int> getGoodIndices(vecteur<vector<int>>& variables, cible int) {
vecteur<int> bonne;
pour (int i = 0; i < variables.size(); ++i) {
long a = variables[i][0];
long b = variables[i][1];
long c = variables[i][2];
long m = variables[i][3];

longue longue première = modPow(a, b, 10); // (a^b) % 10
longue seconde longue = modPow(premier, c, m); // (premier) % m

if (second == cible) good.push_back(i);
}
le bien de retour;
}
};
«» "

> Utilise le même helper `modPow` pour la clarté et la vitesse.

---

Analyse de complexité

Aspect Java Python C++
- C'est quoi ?
**Heure**="O(n · (log b + log c))="O(n · (log b + log c))="O(n · (log b + log c))=" Autres
**Space**= `O(1)` auxiliaire (liste des résultats)= `O(1)` auxiliaire== `O(1)` auxiliaire==
Même chose

Même pour la taille maximale d'entrée (100 lignes), cela fonctionne en millisecondes.

---

Article de blog optimisé par le SEO

---

# Double exposant modulaire – LeetCode 2961
### Votre guide complet: Java, Python, C++ Solutions & Interview‐ Perspectives prêtes

> **Vous préparez une entrevue de codage? * *
> Cet article explique comment cracker LeetCodes *Double problème d'Exposentiation Modulaire* (2961) dans **Java**, **Python** et **C++**. Nous allons parcourir l'algorithme, mettre en évidence les pièges communs et vous donner un code prêt à la production que vous pouvez déposer dans votre portfolio ou votre prochaine interview.

---

- Oui. Pourquoi ce problème est important

- **L'exposé modulaire** est l'une des questions les plus fréquemment posées* dans les entretiens techniques.
- LeetCode 2961 teste votre capacité à combiner **arithmétique modulaire** avec **opérations de puissance**—compétences essentielles pour des rôles impliquant la cryptographie, la sécurité ou la science des données.
- Résoudre en plusieurs langues montre *la pensée linguistique-agnostique*, un trait d'intervieweur recherché.

---

- Oui. L'énoncé du problème en anglais clair

Compte tenu d'un éventail de quadruples `[a, b, c, m]`, trouver tous les indices où

«» "
(a^b % 10) ^ c) % m) cible
«» "

c'est vrai.

---

- Oui. Pourquoi c'est un problème d'entrevue de bonne qualité

Prestation
- Oui.
**Spécification claire**= Facile à lire mais assez subtil pour nécessiter une réflexion attentive. Autres
**Démontre les connaissances de base en CS**. Autres
**La solution en plusieurs langues** **Python**, **C++** (et plus). Autres
**Scales**Le même algorithme fonctionne pour les exposants astronomiquement grands si vous remplacez la "pow" intégrée par une routine d'exposation modulaire efficace. Autres

---

Erreurs courantes (Le "Bad")

- *Overflow*: `a^b` peut exploser; jamais calculer la pleine puissance.
- *Ordre Modulo* : Faire `% m` en premier ou échanger `% 10` peut changer la réponse.
*Cadre d'Edge `m = 1`*: `% 1` est toujours `0`.
- *Python mauvais usage*: `pow(a, b)` retourne la pleine puissance, pas le résultat modulaire.

> Évitez ceux-ci en utilisant *fast modulaire exponentiation* (`pow(a, b, mod)` dans Python, un assistant dans Java/C++).

---

## Garder le code propre (La transition vers la bonne)

Le calcul de base est

Texte
valeur = pow(pow(a, b, 10), c, m)
«» "

Encapsuler cela dans un helper (`modPow`) et le reste du code devient un "for-loop" concis.
Pas de boucles imbriquées, pas de boucles manuelles pour chaque exposant.

---

## Solution en Java

"Java
modPow (long base, long exp, long mod) { ... }
liste publique<entier> getGoodIndices(int[][]variables, int cible) { ... }
«» "

---

Solution dans Python

'`python
def getGoodIndices(self, variables: List[List[int]], cible: int) -> Liste[int]:
bonne = []
pour i, (a, b, c, m) dans l'énumération (variables):
d'abord = pow(a, b, 10)
seconde = pow(premier, c, m)
si la deuxième cible est :
Annexe i)
retour bien
«» "

---

## Solution en C++

'`cpp
long long modPow(long long base, long exp, long long mod) { ... }
vector<int> getGoodIndices(vector<vector<int>>& variables, int cible) { ... }
«» "

---

Complexité

- **Time**: `O(n · (log b + log c))` – négligeable pour les contraintes données.
- **Espace**: «O(1)» auxiliaire.

---

À emporter

- L'exposé modulaire est un sujet à retenir pour les entrevues.
- Implémenter un petit helper (`modPow`) pour garder le code lisible à travers Java, Python et C++.
- Oui. Cas de bord d'essai (`m == 1`, `cible == 0`, grands exposants).

Avec les extraits de code ci-dessus, vous êtes prêt à soumettre votre solution ou impressionner les gestionnaires d'embauche qui demandent: Comment résoudriez-vous la double exponentiation modulaire? *

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

Mots clés et méta-tags

- Double exposition modulaire
- LeetCode 2961
- Codage Interview Algorithmes
- Exposition modulaire Java
- Python 'pow' avec Mod
- C++ Modulaire rapide Puissance
- Préparation de l'entrevue
- Questions d'entretien technique
- Codage sécurisé
- Succès de l'entrevue d'embauche

---

**Bon codage et que votre prochaine interview soit un bon!* *