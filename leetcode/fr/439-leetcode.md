---
titre: LeetCode 439. Analyseur d'expression terne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 439

Nom de l'entreprise Code du leet ID de l'entreprise Difficulté Tags
- C'est quoi ?
Parser d'expression terne 439 $ Medium $ String, Stack, Récursion Autres

**Input** – Une chaîne `expression` qui ne contient que des chiffres `0–9`, les lettres `T` (true) et `F` (faux), et les délimiteurs ternaires `?` et `:`.
**Garantie** – « expression » est syntaxiquement correcte et chaque chiffre est un numéro de caractère unique.
**Output** – La valeur de l'expression: un caractère unique qui est soit un chiffre, `T` ou `F`.

Les groupes d'opérateurs ternaires **de droite à gauche**:

«» "
T?2:3 → (T?2:3) → 2
F?1:T?4:5 → (F?1:(T?4:5)) → 4
T?T?F:5:3 → (T?(T?F:5):3) → F
«» "

La façon classique de l'évaluer est de traiter l'expression à partir de la fin **d'extrêmement** et de garder une pile des résultats des sous-expressions.

---

- Oui. 2. Aperçu de l'algorithme

1. **Démarrer au caractère le plus droit** – il est garanti qu'il s'agit d'une valeur (`0‐9`, `T` ou `F`).
2. **Scan à gauche**.
* Chaque fois que nous voyons une `?`, le caractère à sa ** droite** est la branche *true* et le caractère deux positions à droite (après avoir sauté la `:`) est la branche *faux*.
* Choisissez la branche en fonction du caractère qui ** précède immédiatement** le `?`.
3. **Répéter** jusqu'à ce que nous ayons traité toute la chaîne – le dernier caractère restant est la réponse finale.

L'algorithme fonctionne dans le temps **O(n)** et dans l'espace auxiliaire **O(1)** (aucune pile réelle n'est nécessaire – nous ne conservons que la position actuelle).

Ci-dessous vous trouverez des implémentations propres et idiomatiques dans **Java**, **Python** et **C++**.

---

- Oui. 3. Solutions de code

> **Conseil pour les entrevues** – expliquer la propriété de droite à gauche avant de plonger dans le code; cela montre que vous comprenez la sémantique de l'opérateur ternaire.

---

3.1 Java – itératif, droit à Gauche

"Java
solution de classe publique {
public parseTernaire(Expression de la chaîne) {
int i = expression.longueur() - 1; // commencer au dernier char
résultat char = expression.charAt(i); // résultat courant
i--; // déplacer à gauche vers le char précédent

pendant que (i >= 0) {
Si (expression.charAt(i) == '?') {
// La valeur avant '?' décide quelle branche conserver
si (expression. (i - 1) == 'T') {
// garder la vraie branche: caractère après '? '
résultat = expression.charAt(i + 1);
} autre {
// conserver la fausse branche : sauter sur ':' et la valeur après elle
résultat = expression.charAt(i + 3);
}
i -= 2; // sauter sur le '?' et la branche choisie
} autre {
i--; // sauter les caractères ordinaires
}
}
retour Chaîne.valeurDe(résultats);
}
}
«» "

**Pourquoi ça marche** – En marchant de la droite, nous connaissons toujours la *valeur* qui suit un `?`. Le caractère *avant* que `?` nous dit de quel côté prendre. Parce que nous traitons d'abord les expressions intérieures, les opérateurs ternaires externes sont évalués correctement.

---

3.2 Python – Récursion (espace élégant mais O(n))

'`python
Solution de classe:
def parseTernary(self, expression: str) -> str:
Def helper(i: int) -> (str, int):
# Retourne la valeur à la position i et l'index du jeton suivant
si expression[i].isdigit() ou expression[i] dans 'TF':
retour [i], i

L'expression ? '
true_val, next_i = helper(i + 1)
false_val, _ = helper(next_i + 2) # skip over ': '
retourner true_val si expression[i - 1] == 'T' sinon false_val, next_i

val, _ = aide(len(expression) - 1)
retour val
«» "

> **Traitement** – la récursion est lisible mais utilise **O(n)** empiler l'espace. Pour `n ≤ 10^4` c'est bien dans Python, mais dans les interviews vous pouvez vouloir la version itérative.

---

### 3.3 C++ – itératif, sans pile

'`cpp
solution de classe {
public:
chaîne parseTernary(expression de chaîne) {
i = expression.size() - 1; // indice de la valeur actuelle
résultat char = expression[i]; // résultat courant
i--; // déplacer à gauche vers le char précédent

pendant que (i >= 0) {
si (expression [i] == '?') {
i (expression [i - 1] == 'T')
résultat = expression[i + 1]; // vraie branche
Autre
résultat = expression[i + 3]; // fausse branche
i -= 2; // sauter les pièces traitées
} autre {
i--; / / skip non-operator char
}
}
retour de la chaîne(1, résultat);
}
};
«» "

> **Pourquoi C++?** La logique est identique à Java; il suffit de garder un œil sur l'indexation basée sur 0 et la construction de chaînes.

---

- Oui. 4. Le bon, le mauvais et le mauvais

Aspect du bien
- C'est quoi ?
Il faut se rappeler que le ternaire est droit à gauche, ce qui est contre-intuitif. Autres L'oubli de la règle de droite à gauche conduit à une mauvaise sélection des branches. Autres
**Mise en oeuvre**= O(n) temps, espace O(1).= Nécessite un arithmétique de l'indice prudent; les erreurs hors-par-un sont fréquentes. Version récursive peut souffler la pile pour la nidification profonde (`n = 10^4`). Autres
La solution itérative est concise. La solution basée sur les piles (poussées/pop) peut être verbeuse. Le mélange de la récursion et de la chaîne de caractères en Python peut masquer la logique. Autres
**Performance** Pas grand- Aucun – la solution sans pile est optimale. Autres
**Cas d'Edge** Il faut bien sauter `:` quand on prend une fausse branche. Le traitement accidentel du `:` comme faisant partie de la valeur peut produire une mauvaise sortie. Autres

---

- Oui. 5. Article de blog optimisé par le SEO

> **Titre** – *=Mastering LeetCode 439: Analyseur d'expression terne en Java, Python & C++ – Un guide de préparation à l'emploi*
> **Meta Description** – *= Apprenez à résoudre LeetCode 439 – Ternary Expression Parser. Obtenez des solutions Java, Python et C++, comprenez l'algorithme et asez vos entretiens de codage.

---

5.1 Introduction

Si vous êtes à la recherche d'une position **ingénieur logiciel**, vous avez probablement vu LeetCodes parser (ID 439). C'est un problème étonnamment subtil qui teste votre compréhension de *l'évaluation de droite à gauche* et votre capacité à écrire un code propre et efficace en **Java, Python ou C++**.

Cet article vous fait découvrir :

1. **La déclaration de problème** – ce que nous résolvons et pourquoi elle compte.
2. **L'algorithme de base** – pourquoi un scan de droite à gauche est le tour de magie.
3. **Trois solutions linguistiques** – code prêt à coller que vous pouvez utiliser lors des entrevues.
4. **Pièges communs** – le bon, le mauvais et le laid.
5. **Comment en parler sur votre CV et dans les entrevues** – transformer un exercice de codage en avantage de carrière.

---

5.2 Récapitulation des problèmes

> *Avec une chaîne qui représente une expression ternaire avec des chiffres, `T` (true), `F` (faux), `?` et `:` – évaluer l'expression et retourner le résultat final. *

Principales contraintes :

- Longueur de l'expression : 5 à 10 000 caractères.
- Chaque chiffre est un caractère (« 0–9 »).
- Oui. L'expression est **valide** et **de droite à gauche** groupée.

---

5.3 Pourquoi le balayage de droite à gauche fonctionne

Lorsque vous lisez une expression ternaire du caractère le plus droit, vous connaissez déjà la *valeur* qui appartient à la branche *true* ou *faux* de la `?` la plus proche. Le personnage juste avant ça ? vous dit de quel côté prendre. En détachant à plusieurs reprises l'expression la plus intérieure, vous effondrez toute l'expression à une seule valeur.

Cette observation supprime le besoin d'une pile ou récursion explicite (bien que ce soient de grandes façons de penser au problème). Elle garantit également **O(n)** temps et **O(1)** espace auxiliaire.

---

#### 5.4 Mises en œuvre spécifiques aux langues

> **Tip** – Dans les interviews, commencez par la solution *iterative* (Java/C++) et mentionnez que vous pouvez facilement la convertir en Python. Mettre en évidence la justification de droite à gauche.

##### 5.4.1 Java – itératif, sans pile

"Java
solution de classe publique {
public parseTernaire(Expression de la chaîne) {
i = expression.longueur() - 1; // indice le plus droit
char result = expression.charAt(i); // valeur actuelle
i--;

pendant que (i >= 0) {
Si (expression.charAt(i) == '?') {
// 'T' ou 'F' est juste avant '? '
si (expression. charAt(i - 1) == 'T')
résultat = expression.charAt(i + 1); // vrai branche
Autre
résultat = expression.charAt(i + 3); // fausse branche
i -= 2; // sauter la partie traitée
} autre {
i--; / sauter non-exploitant
}
}
retour Chaîne.valeurDe(résultats);
}
}
«» "

5.4.2 Python récursif (légant)

'`python
Solution de classe:
def parseTernary(self, expression: str) -> str:
Def helper(i: int) -> (str, int):
# Si le char courant est une valeur, retournez-le
si expression[i].isdigit() ou expression[i] dans 'TF':
retour [i], i

L'expression ? '
true_val, next_i = helper(i + 1)
false_val, _ = helper(next_i + 2) # skip over ': '
retourner true_val si expression[i - 1] == 'T' sinon false_val, next_i

val, _ = aide(len(expression) - 1)
retour val
«» "

#### 5.4.3 C++ – itératif, sans pile

'`cpp
solution de classe {
public:
chaîne parseTernary(expression de chaîne) {
i = expression.size() - 1; // le plus droit
char result = expression[i];
i--;

pendant que (i >= 0) {
si (expression [i] == '?') {
i (expression [i - 1] == 'T')
résultat = expression[i + 1];
Autre
résultat = expression[i + 3];
i -= 2;
} autre {
i--;
}
}
retour de la chaîne(1, résultat);
}
};
«» "

> **Note de rendement** – Tous les trois fonctionnent en un seul passage et sont prêts pour de grandes entrées.

---

#### 5.5 Pièges communs et interviews

Piège Comment éviter Interview Talking Point
- C'est quoi ?
Autres Mauvaise lecture de l'ordre de l'opérateur. **Ternaire est droit-à-gauche**. Autres
Utiliser `i - 1` et `i + 3` soigneusement. Autres
Utiliser la version itérative ou ajouter l'optimisation de l'appel arrière. Je peux passer à une solution itérative pour rester O(1) dans l'espace. Autres
Autres Oubliant de sauter `:` dans une fausse branche. Autres

---

5.6 Mettre le problème en évidence

- **Resume blue**: "Implemented a right-to-left parser for LeetCode 439 (Ternary Expression Parser) amenant O(n) time et O(1) space à travers Java, Python et C++. (en milliers de dollars)
- **Cadre d'entrevue**: Ce problème met en évidence ma capacité à raisonner sur la sémantique d'expression et à les traduire en algorithmes linéaires. Je l'ai résolu avec une approche itérative qui fonctionnerait dans n'importe quelle langue, et je peux également discuter des alternatives récursives et basées sur les piles si nécessaire. (en milliers de dollars)

---

5.7 Pensées finales

LeetCode 439 est plus qu'un problème de "trick". Cela vous force à penser **en dehors de la lecture habituelle de gauche à droite** et au code de métier qui est *fast* et *memory efficient*. La maîtrise démontre :

- ** intuition algorithmique** – vous pouvez identifier le travail minimum nécessaire.
- **Capacité de la langue** – vous pouvez adapter une idée centrale à Java, Python ou C++ à la volée.
- **Confiance d'entrevue** – vous pouvez exprimer à la fois le *pourquoi* et le *comment*.

Déposer les extraits de code dans votre GitHub, inclure une section sur votre CV, et être prêt à expliquer la nuance de droite à gauche dans votre prochaine entrevue de codage. Bonne chance : votre prochain rôle d'ingénierie logicielle n'est qu'une expression ternaire !

---

- Oui. 6. Mot final

Résoudre *LeetCode 439 – Ternary Expression Parser* est une petite victoire mais puissante pour votre boîte à outils d'entrevue. Par:

- En gravant la sémantique de droite à gauche,
- Écrire un scan propre, O(n) dans la langue de votre choix,
- Oui. Et étant prêt à discuter d'écueils,

vous transformez un défi apparemment de niche en un ** showcase de maîtrise algorithmique**. Bonne chance, et le codage heureux!