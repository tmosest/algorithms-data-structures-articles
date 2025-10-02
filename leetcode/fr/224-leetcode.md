---
titre: LeetCode 224. Calculatrice de base - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 224. Calculatrice de base – Hard – Java / Python / C++ Solutions + SEO-Optimized Blog Post

Ci-dessous vous trouverez **trois implémentations complètes** de LeetCode 224 – *Basic Calculator* – un en Java, Python et C++.
Après le code, vous trouverez un article de blog SEO détaillé qui couvre le bien, le mauvais, et la laid de ce problème d'interview classique.

---

- Oui. 1. Java – basé sur la pile (itérative)

"Java
Importer java.util. Pioche;

solution de classe publique {
calcul de l'int public(en milliers) {
Pile <integer> = nouvelle pile<>();
résultat int = 0; //
int num = 0; // nombre actuel en cours de construction
signe int = 1; // +1 ou -1

pour (int i = 0; i < s.longueur(); i++) {
c = s.charAt(i);

si [Caracter.isDigit(c)] {
// Construisez le numéro actuel (maintenez plusieurs chiffres)
num = num * 10 + (c - '0');
} sinon si (c == '+') {
résultat += signe * num;
num = 0;
signal = 1;
} sinon si (c) {
résultat += signe * num;
num = 0;
signal = -1;
} sinon si (c) '(') {
// Poussez l'état du courant sur la pile
pile.push(résultat);
empil.push(signal);
// Réinitialiser pour la sous-expression
résultat = 0;
signal = 1;
} sinon si (c) {
résultat += signe * num; // terminer le numéro intérieur
num = 0;
int prevSign = pile.pop(); // signe avant '('
int prevResult = pile.pop(); // result avant '('
résultat = prevRésultat + prevSign * résultat;
} sinon si (c) ') {
// Sauter l'espace blanc
poursuivre;
}
}

// Ajouter tout nombre restant
si (num != 0) {
résultat += signe * num;
}
le résultat du retour;
}
}
«» "

> **Pourquoi cela fonctionne:**
> La pile stocke le *context* avant chaque parenthèse d'ouverture : le résultat cumulatif jusqu'à ce point et le signe qui s'applique à toute la sous-expression à l'intérieur des parenthèses. Lorsque nous touchons une parenthèse de clôture, nous popons ces deux valeurs et les combinons avec le résultat de la sous-expression.

---

- Oui. 2. Python – base Stack (itérative)

'`python
Solution de classe:
def calcul(self, s: str) -> Int:
pile = []
résultat = 0
num = 0
signe = 1 # +1 ou -1

pour ch en s:
si ch.isdigit():
num = num * 10 + int(ch)
* '+':
résultat += signe * num
num = 0
signal = 1
élif ch == '-':
résultat += signe * num
num = 0
signe = -1
élif ch == '(':
pile.append(résultat)
pile.append(sign)
résultat = 0
signal = 1
élif ch == ')':
résultat += signe * num
num = 0
prev_sign = pile.pop()
prev_result = pile.pop()
résultat = prev_result + prev_sign * résultat
# ignorer les espaces

si num:
résultat += signe * num
résultat du retour
«» "

---

- Oui. 3. C++ – Base de la pile (itérative)

'`cpp
#incluez <string>
#incluez <stack>
utilisant l'espace de noms std;

solution de classe {
public:
(chaîne s) {
pile<int> st; // stocke le résultat précédent et signe
résultat int = 0; //
int num = 0; // nombre actuel
signe int = 1; // +1 ou -1

pour (charc : s) {
si [risque(c)] {
num = num * 10 + (c - '0');
} sinon si (c == '+') {
résultat += signe * num;
num = 0;
signal = 1;
} sinon si (c) {
résultat += signe * num;
num = 0;
signal = -1;
} sinon si (c) '(') {
s.push(résultat);
s.push(signe);
résultat = 0;
signal = 1;
} sinon si (c) {
résultat += signe * num;
num = 0;
Int prevSign = st.top(); st.pop();
int prevRésultat = st.top(); st.pop();
résultat = prevRésultat + prevSign * résultat;
}
// ignorer les espaces
}

si (num != 0) résultat += signe * num;
le résultat du retour;
}
};
«» "

---

Le bon, le mauvais et le mauvais de LeetCode 224: Calculatrice de base

- Oui. 1. Présentation

> **LeetCode 224 – Calculatrice de base (Hard)**
> Le problème vous demande d'évaluer une expression arithmétique simple qui contient des entiers non négatifs, `+`, `-`, entre parenthèses et espaces.
> **Pourquoi c'est important:**
> • C'est une question classique d'entrevue *stack* qui teste votre capacité à gérer la préséance de l'opérateur et les structures imbriquées.
> • De nombreuses entreprises technologiques (Google, Amazon, Microsoft, Meta, etc.) utilisent des variantes de ce problème pour évaluer les candidats.
> • L'écriture d'une solution propre et efficace démontre la maîtrise de la logique itérative, de la récursion et de la manipulation des erreurs – qualités très appréciées sur votre CV.

- Oui. 2. Énoncé du problème (mots clés du référencement)

- ** Calculatrice de base** – LeetCode 224
- **Hard** – défi d'entrevue de codage
- ** Solution à base de piles**
- **Java, Python, C++** – code spécifique à la langue
- **Évaluation de l'expression arithmétique** – pas d'aval() "

> Entrée: `s = "1 + 1"` → Sortie: `2`
> Entrée: `s = "(1+(4+5+2)-3)+(6+8)"` → Sortie : `23`

- Oui. 3. Contraintes

Contestation Raison
C'est pas vrai.
`1 <= s.longueur <= 3 * 10^5`= Poignées de grandes expressions
`s` ne contient que des chiffres, `+`, `-`, `(`, `)` et espace.
Autres Pas unaire `+`-Clarifie que `+1` est invalide
Unaire `-` permis=Poigne des expressions comme `-1` ou `-(2+3)` Autres
Autres Pas d'opérateurs consécutifs.
32-bit signed integer fits

- Oui. 4. Le bon – ce qui rend ce problème élégant

- ** Grammaire déterministe :** Aucun opérateur ambigu n'a préséance au-delà des parenthèses et du binaire `+`/`-`.
- **Qualité de la pile :** Chaque paire de parenthèses se met naturellement en correspondance avec un push/pop, conservant l'algorithme O(n).
- ** Pass unique :** Nous pouvons résoudre le problème dans un scan linéaire, qui est une grande victoire pour les intervieweurs.
**Échelle:** Fonctionne pour des entrées énormes ('3*10^5' chars) sans problèmes de profondeur de récursion.
- **Langue Agnostique :** La logique de la pile est identique en Java, Python, C++.

- Oui. 5. Les mauvaises – pièges et erreurs communs

Comment éviter
C'est quoi ?
**Obligation d'ajouter le dernier numéro**= Après la boucle, ajouter `sign * num` si `num` est non-zéro. Autres
*Push *result* d'abord, puis *sign*. Lorsque vous sautez, retournez l'ordre. Autres
**En supposant des nombres à un chiffre**. Autres
**Utiliser la récursion pour `()`**.La profondeur de récursion peut frapper le débordement de la pile pour les parenthèses profondément imbriquées. Autres
**Traiter les espaces de manière incorrecte** Autres

- Oui. 6. Les cas d'indulgence – bord qui voyagent candidats

1. **Unaire moins au début**: `"-1+2"`
- L'algorithme doit traiter le `-` comme un signe pour le premier numéro.
2. **Négatives entre parenthèses**: "- (1+2)"
- L'espace après `-` est inoffensif, mais l'algorithme doit toujours pousser le bon signe sur la pile.
3. **Parenthèses imbriquées multiples**: `"((1+2)+(3+4)"`
- Veiller à ce que la pile ne soit jamais en aval; chaque `(` doit avoir une `) correspondante`.
4. **Grands chiffres**: ""123456789+987654321"
- Utilisez `int` (32-bit) mais faites attention à ce que les sommes intermédiaires restent dans les limites (ils le font, selon les contraintes).

- Oui. 7. Balade de l'algorithme (basée sur les piles)

1. **Initialiser**: `résultat = 0`, `num = 0`, `sign = 1`, pile vide.
2. **Choisir chaque personnage**:
- **Digit** → construire `num`.
- **`+` / ``** → appliquer `sign * num` à `result`, réinitialiser `num`, définir un nouveau `sign`.
- **`(`** → appuyez sur `résultats` et `sign`, réinitialisez-les (`résultats = 0`, `sign = 1`).
- **`)`** → terminer le nombre intérieur, multiplier par le signe surgissant de la pile, puis ajouter au résultat extérieur.
3. **Après la boucle**: Ajouter tout nombre restant à "résultats".

Cet algorithme fonctionne dans **O(n)** temps et utilise **O(n)** empiler de l'espace dans le pire des cas (entre parenthèses entièrement imbriquées). Le facteur constant est très petit — seulement une poignée de variables entières et les opérations de la pile.

- Oui. 8. Échantillons de codes

*Le code source complet pour Java, Python et C++ est fourni ci-dessus. *
Tous les trois partagent la même logique ; juste la syntaxe change.

- Oui. 9. Analyse de la complexité

Langue Heure Espace
- C'est quoi ?
Java Autres
Python "O(n)" Autres
"O(n)" Autres

> **Pourquoi est-ce acceptable? * *
> Les intervieweurs recherchent des algorithmes linéaires pour les problèmes difficiles. La récursion aurait ajouté des frais généraux supplémentaires et un trop-plein de cheminée risqué.

10 ans. Comment briller sur votre CV

- **Ajoutez un badge "Coding Interview"** à côté du problème de calculatrice de base sur votre blog GitHub ou personnel.
- **Afficher la solution de empilement de l'O(n) dans les messages README ou LinkedIn de votre projet.
- **Mention implémentations multi-langues** (Java, Python, C++) pour montrer la capacité d'adaptation.
- **Fournir un extrait de mesure du temps** pour montrer que votre solution fonctionne sous 1 ms pour les caractères `3*10^5` sur le matériel typique.

10 ans. Dernier départ

> Le problème de calculatrice de base est un exemple *beau* de la façon dont un problème d'analyse complexe peut être distillé dans des opérations de pile simples.
> En maîtrisant l'approche basée sur la pile et en anticipant les cas de bord, vous avez non seulement saisi cette question LeetCode, mais aussi démontré une profondeur de compréhension que les recruteurs recherchent chez les ingénieurs logiciels seniors.

** Bonne chance pour votre prochaine interview!**

---

**Note moyenne**: Le contenu du blog ci-dessus peut être utilisé in extenso sur des blogs personnels, Medium, dev.to, ou même dans des messages LinkedIn. Il est rempli de titres SEO-friendly, de paragraphes riches en mots clés et d'extraits de code pratiques.