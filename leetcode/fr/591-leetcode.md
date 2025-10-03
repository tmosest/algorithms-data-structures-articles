---
titre: LeetCode 591. Validateur d'étiquette - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° 591. Validateur d'étiquette – Solutions complètes + Blog optimisé SEO

Ci-dessous vous trouverez trois solutions complètes et prêtes à la production pour LeetCode **591 – Validateur d'étiquette** écrit en **Java**, **Python** et **C++**.
Après le code, vous trouverez un long-forme, l'article SEO-friendly qui explique le problème, l'algorithme, et le bon, mauvais et moche, les pièges que vous voulez mentionner dans une interview.

> **TL;DR – Algorithme**
> • Scannez la chaîne de gauche à droite.
> • Utilisez une pile pour garder les noms d'étiquettes ouverts.
> • `<` démarre une balise ou CDATA.
> • CDATA («<![CDATA[ ... ]]>») est traité comme un texte simple.
> • Chaque `</TAG>` doit correspondre au sommet de la pile.
> • Le code doit être enveloppé dans une étiquette de haut niveau.
> • Tous les noms d'étiquettes doivent être de 1 à 9 lettres majuscules.
> • Complexité: **O(n)** temps, **O(n)** empiler l'espace.

---

C'est pas vrai. Java 17 Solution

"Java
Importation de java.util.*;

solution de classe publique {
booléen public est Valid(code de la chaîne) {
// Un extrait de code doit commencer par une balise d'ouverture
si (code.isEmpty()== code.charAt(0) != '<') retourner faux;

Deque<String> pile = nouvelle ArrayDeque<>();
i = 0;
int n = code.longueur();

pendant que (i < n) {
// Si nous voyons un '< '
si (code.charAt(i) == '<') {
// 1. Section CDATA
si (i + 9 < n && code.startsWith("<![CDATA[", i)) {
i + 9);
si (fin == -1) retourner faux; // pas de fermeture ]]
i = fin + 3; // saut CDATA
poursuivre;
}

// 2. Étiquette de fermeture
si (i + 1 < n && code.charAt(i + 1) == '/') {
int j = i + 2;
inter close = code.indexOf('>', j);
i (fermer) -1) retourner faux; // pas de fermeture >
Tag chaîne = code.substring(j, fermer);
si (!isValidTagName(tag)) retourne false;
si (stack.isEmpty()- !stack.peek().equals(tag)) retourne faux;
pile.pop();
i = proche + 1;
poursuivre;
}

// 3. Étiquette d'ouverture
i + 1;
inter close = code.indexOf('>', j);
i (fermer) -1) retourner faux; // pas de fermeture >
Tag chaîne = code.substring(j, fermer);
si (!isValidTagName(tag)) retourne false;
pile.push(étiquette);
i = proche + 1;
poursuivre;
}

// Tout autre caractère est autorisé dans le contenu
i++;
}

// L'ensemble du code doit être enveloppé dans une étiquette de haut niveau
retour pile.isEmpty();
}

// Règles relatives au nom d'étiquette : 1–9 lettres majuscules
booléen privé estValidTagName(String s) {
si (longueur() < 1=1 s.longueur() > 9) retourner faux;
pour (int k = 0; k < s.longueur(); k++) {
c = s.charAt(k);
si (c < " A " " c > " Z " ) retourner faux;
}
retour vrai;
}
}
«» "

**Pourquoi ça marche* *

* Nous **n'utilisons jamais regex pour la validation – l'énoncé du problème met en garde contre les régexes fragiles.
* La pile garantit une nidification correcte et chaque étiquette d'ouverture a une étiquette de fermeture correspondante.
* Les sections CDATA sont dérobées atomiquement – nous n'inspectons jamais leur contenu intérieur.
* La dernière vérification `stack.isEmpty()` garantit que l'extrait entier est enveloppé dans une seule étiquette.

---

Solution Python 3

'`python
Solution de classe:
def isValid(self, code: str) -> C'est vrai.
si non code ou code[0] != '<':
Retour Faux

pile = []
i, n = 0, len(code)

alors que i < n:
si code[i] == '<':
# Section CDATA
i + 9 < n et code.commence avec("<![CDATA[", i):
fin = code.find("]>", i + 9)
Si fin == -1:
Retour Faux
i = fin + 3
poursuivre

# Étiquette de fermeture
si i + 1 < n et code[i + 1] == '/':
j = i + 2
fermer = code.find('>', j)
si elle est proche - 1 :
Retour Faux
tag = code[j:close]
si ce n'est pas soi-même._is_valid_tag(tag):
Retour Faux
sinon pile ou pile[-1] != étiquette :
Retour Faux
Pile.pop()
i = proche + 1
poursuivre

Ouverture de la balise
j = i + 1
fermer = code.find('>', j)
si elle est proche - 1 :
Retour Faux
tag = code[j:close]
si ce n'est pas soi-même._is_valid_tag(tag):
Retour Faux
pile.append(étiquette)
i = proche + 1
poursuivre

Caractère ordinaire
i += 1

retour non pile

@staticmethod
def _is_valid_tag(nom: str) -> C'est vrai.
retourner 1 <= len(name) <= 9 et name.isupper() et name.isalpha()
«» "

**Notes de python**

* `str.find()` est utilisé au lieu de regex - le maintient rapide et simple.
* `stack` est une liste; `append`/`pop` donnent des opérations amorties **O(1)**.
* L'assistant `_is_valid_tag` garde la règle isolée.

---

Solution C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool isValid(code chaîne) {
si (code.vide()== code[0] != '<') retourne false;

vecteur <string> m;
i = 0, n = code.size();

pendant que (i < n) {
si (code[i] == '<') {
// Section CDATA
si (i + 9 < n && code.compare(i, 9, "<![CDATA[")] 0) {
i + 9);
si (fin == chaîne::npos) retourner false;
i = fin + 3;
poursuivre;
}

// Étiquette de fermeture
si (i + 1 < n && code[i + 1] == '/') {
int j = i + 2;
int close = code.find('>', j);
si (fermer == chaîne::npos) retourner false;
tag chaîne = code.substr(j, fermer - j);
si (!isValidTag(tag)) retourne faux;
si (st.vide()=) st.back()= tag) retourner false;
le _retour_st.pop();
i = proche + 1;
poursuivre;
}

// Ouverture de la balise
i + 1;
int close = code.find('>', j);
si (fermer == chaîne::npos) retourner false;
tag chaîne = code.substr(j, fermer - j);
si (!isValidTag(tag)) retourne faux;
st.push_back(tag);
i = proche + 1;
poursuivre;
}

++i; // caractère normal
}

retour st.vide();
}

particulier:
bool isValidTag(chaîne de caractères Const) {
si (s.vide())S.size() 9) retourner faux;
pour (charc : s)
si (c < " A " " c > " Z " ) retourner faux;
retour vrai;
}
};
«» "

**Tricks C++* *

* `string::compare` donne une vérification constante du préfixe CDATA.
* `vector<string>` est utilisé comme pile; il est assez rapide pour la limite de 10 000 caractères.
* Toutes les boucles s'exécutent dans **O(n)** – pas de récursion, pas de régex.

---

Article du blog – Validateur de Tag Leetcode 591

> **Mots clés**: *Tag Validator, LeetCode 591, entretien d'analyse XML, algorithme de pile, codage d'entrevue d'emploi, entretien d'ingénieur logiciel, questions d'entrevue de codage, modèles d'entrevue de programmation*

### Validateur d'étiquette – LeetCode 591 expliqué

Imaginez que vous soyez un ingénieur **récepteur** travaillant sur un petit moteur de balisage XML.
LeetCodes **591 – Tag Validator** vous demande de décider si une chaîne donnée est un extrait de code valide suivant *strict* règles de style XML:

Règle Description Autres
- C'est quoi ?
Autres **Il faut commencer par une étiquette d'ouverture**.L'extrait entier est enveloppé dans une seule étiquette de haut niveau. Autres
Autres **Dénomination de l'étiquette**=1–9 caractères alphabétiques majuscules seulement. Autres
**Les étiquettes doivent être correctement imbriquées; chaque `</TAG>` doit fermer la dernière étiquette ouverte. Autres
**Aucune variance `<` ou `>`**. Tous les supports d'angle appartiennent à des étiquettes ou CDATA. Autres
**CDATA**. `<![CDATA[ ... ]]>` est traité comme du texte brut; son contenu est ignoré. Autres

On vous donne un seul `code d'attache` (10 000 caractères) et vous devez retourner `true` s'il suit toutes les règles, sinon `faux`.

### La partie "Bien" – Pourquoi une pile est le bon outil

* ** Représentation naturelle des structures imbriquées** – chaque étiquette ouverte pousse son nom sur la pile; une étiquette étroite doit correspondre au sommet de la pile.
* **Temps linéaire** – vous ne scannez qu'une fois, chaque personnage a examiné un nombre constant de fois.
* ** Mémoire limitée par la profondeur de la nidification** – pire cas « O(n) » mais généralement beaucoup moins.
* ** Comportement prévisible** – pas de surprises dues au moteur régex ou au recul.

- Oui. La partie "Pièges communs"

1. ** Utilisation du régex**
Beaucoup de solutions naïves essaient un grand régex pour valider les balises, mais la spécification avertit que de tels modèles sont *fragile* et difficile à maintenir.
*Pourquoi régex échoue* : Il ne peut pas imposer la nidification sensible au contexte (par exemple, s'assurer que `</A>` correspond à la bonne `<A>).

2. **Manipulation de CDATA *
Le fait de traiter le CDATA comme un texte ordinaire conduit à de faux négatifs (par exemple, un `>` errant à l'intérieur du CDATA).
*Solution*: Passez le bloc CDATA entier une fois que vous détectez son marqueur d'ouverture.

3. **Vérification d'emballage de niveau supérieur**
Oublier d'exiger que l'extrait complet soit enveloppé dans une seule étiquette provoque des bugs subtils.
*Fix* : Après le scan, la pile doit être vide – toute étiquette restante signifie que l'extrait n'était pas complètement fermé.

### La partie "Ugly" – Les cas de bord qui voyagent

Pourquoi c'est bizarre Comment manipuler
- C'est quoi ?
`<A></A>` – un extrait de code minimal valide. Gardez la pile à vérifier `stack.vide()` après la boucle. Autres
Autres Nom de l'étiquette longueur 10 ou boîtier mixte. Encapsuler la règle dans un assistant ('isValidTagName'). Autres
Autres Pas de fermeture `>` ou `]]>` Les calculs de l'indice deviennent négatifs, conduisant à "StringIndexOutOfBounds". Toujours vérifier que l'index est trouvé avant de trancher. Autres
"<" au milieu du contenu Si elle n'est pas suivie d'une étiquette valide ou d'un CDATA, elle est un caractère illégal. Traiter tout autre `<` comme invalide et retourner `faux`. Autres
Il y a des gens qui oublient ce pré-vérification rapide et laissent l'algorithme s'exécuter jusqu'à la fin, renvoyant incorrectement `true`. Autres

### Étape par étape Algorithme Marche à travers

1. **Pré-vérification** – L'extrait doit commencer par `<`.
2. **Initialiser une pile vide** – conservera les noms des balises ouvertes.
3. **Scan gauche → droite* *
* Lorsque vous frappez un `<`:
* **CDATA** (`<![CDATA[`) – Trouvez le suivant `]> et sautez dessus.
* **Tag de fermeture** (`</TAG>`) – Extraire le nom de la balise, le valider et pop la pile. Retourner `false` si elle ne correspond pas au haut.
* **Ouvrir la balise** (`<TAG>`) – Extraire le nom de la balise, la valider et la pousser sur la pile.
* Tout autre caractère est autorisé dans le contenu – il suffit de passer à autre chose.
4. **Vérification finale** – La pile doit être vide, ce qui signifie que chaque étiquette ouverte a été fermée et que le code entier est enveloppé dans une étiquette de haut niveau.

Analyse de complexité

Calcul métrique
C'est pas vrai.
Chaque caractère est inspecté un nombre constant de fois → **O(n)** Autres
**L'espace**La pile stocke au plus des noms d'étiquettes `n/2` → **O(n)** dans le pire des cas (nicher profondément). Autres

### Conseils d'entrevue

* ** Expliquez votre invariant de pile** – Le haut de la pile représente toujours la balise la plus récente qui n'a pas encore été fermée.
* **Montrer que vous comprenez CDATA** – Il n'est pas analysé; il est simplement un bloc de texte brut.
* **Mention la règle du nom de la balise** – 1–9 caractères alphabétiques majuscules.
* **Éviter le régex** – La plupart des intervieweurs s'attendent à ce que vous artisanalisiez l'analyseur.
* ** Cas d'erreur manuelle précoce** – Si vous trouvez une étiquette manquante `>` ou incorrecte, sortez immédiatement.

Les pensées finales

- **Bien** – L'approche de la pile est propre, O(n) et facile à raisonner.
- **Bad** – Un régex complexe est tentant mais fragile ; évitez-le.
- **Ugly** – Souvenez-vous des conditions de limites subtiles : le tout premier `<` doit être une balise d'ouverture, le tout dernier doit être sa balise de fermeture correspondante, et les sections CDATA doivent être sautées atomiquement.

Si vous pouvez expliquer cet algorithme, parcourir quelques cas de test, et montrer l'une des trois solutions ci-dessus, vous aurez une réponse solide pour **LeetCode 591 – Tag Validator** qui impressionne à la fois les classificateurs automatisés et les intervieweurs.

Bonne chance pour votre entretien de codage et votre prochain rôle d'ingénierie logicielle! C'est ce qu'il a dit.

---

Copie rapide pour les entrevues d'embauche

"Java
// Java 17 – Validateur d'étiquette
solution de classe publique { ... } // voir le code ci-dessus
«» "

'`python
# Python 3 – Validateur d'étiquettes
classe Solution: ... # voir code ci-dessus
«» "

'`cpp
// C++17 – Validateur d'étiquette
classe Solution { ... } // voir le code ci-dessus
«» "

Bon codage !