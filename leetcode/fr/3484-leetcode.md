---
Titre: LeetCode 3484. Feuille de calcul - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
##  uvre de conception – Solution O(1) (Java / Python / C++)

Ci-dessous vous trouverez:

Langue Nom du fichier Structure des données clés Complexité
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Autres "Java" `Spreadsheet.java`" `HashMap<String,Integer>`" **O(1)** pour chaque opération
Python "spreadsheet.py" "dict" **O(1)** pour chaque opération
C++="Spreadsheet.cpp=" `unordered_map<string,int=" **O(1)** pour chaque opération="

L'implémentation suit la même logique dans chaque langue – une carte unique qui contient les valeurs *explicites* définies par l'utilisateur. Les cellules non définies contiennent implicitement `0`.

> **Astuce:** Utilisez une carte de hachage au lieu d'un tableau 2-D pour garder l'empreinte de la mémoire minimale, surtout lorsque les « lignes » peuvent atteindre 103 et que la grille est clairsemée.

---

Récapitulation des problèmes

- La feuille de calcul comporte 26 colonnes (A–Z) et un nombre de lignes spécifié par l'utilisateur.
- Toutes les cellules commencent par la valeur `0`.
- Opérations soutenues :

Méthode Signature Ce qu'il fait
- C'est quoi ?
"setCell(Cellule fixe, valeur int)" Définit la valeur d'une cellule (par exemple, "A1" → 10"). Autres
"resetCell(String cell)" Réinitialise une cellule à `0`. Autres
"getValue (formule de fixation)" Évaluer `"=X+Y"` où `X` & `Y` sont soit des entiers soit des références cellulaires. Autres

- Oui. Au plus 104 appels, "valeur ≤ 105", "lignes ≤ 103".

---

- Oui. Idées de base

> **Utilisez une carte de hachage clé par la chaîne de référence cellulaire. **

- **Set / Reset** → il suffit d'insérer/écraser la clé avec la nouvelle valeur.
- **Get** → diviser la formule à `+`, traiter chaque opérande:
- Si elle commence par une lettre → regarder vers le haut dans la carte (par défaut 0).
- Autrement → l'analyser comme un entier.

Toutes les opérations sont * amorties O(1)*.

---

Code

C'est pas vrai. Java – `Spreadsheet.java "

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

***
* LeetCode 3484 – Feuille de calcul
*/
classe publique {
// Carte qui stocke seulement les cellules qui ont été explicitement définies
carte finale privée<String, entier> cellules;

public Feuille de calcul(int lignes) {
// lignes n'est pas nécessaire pour la logique – il s'agit seulement de satisfaire la signature du constructeur
cellules = nouvelle HashMap<>();
}

*** Définit la valeur d'une cellule. */
public vide setCell(Cellule fixe, valeur int) {
cellules.put(cell, valeur);
}

*** Réinitialise une cellule à 0. */
réinitialisation du vide public Cellule(cellule de maintien) {
cellules.put(cellule, 0);
}

/** Évaluer "=X+Y" où X/Y sont soit entiers ou réfs cellulaires. */
Int public getValue (formule de classement) {
// Bande menant '=' et divisée sur '+ '
Chaîne[] parties = formula.substring(1).split("\\+");
int gauche = parseOperand(parties[0]);
int droite = parseOperand(parties[1]);
retour gauche + droite;
}

*** Aide à l'analyse d'un opérande : soit un int, soit une référence cellulaire. */
parse privée Operand (jeton d'appui) {
i (Caracter.isUpperCase(token.charAt(0))) {
retourner les cellules.getOrDefault(token, 0);
}
retour Integer.parseInt(token);
}
}
«» "

**Utilisation**

"Java
Feuille de calcul obj = nouvelle feuille de calcul(3);
b) Cell("A1", 10);
oj.resetCell("A1");
valeur int = obj.getValue("=A1+5"); // retourne 5
«» "

---

Python – `spreadsheet.py "

'`python
classe Feuille de calcul:
"""
Feuille de calcul – solution O(1) Python.
"""

def __init_(self, lignes: int):
# lignes non utilisées dans l'implémentation
auto.cellules = {}

def setCell(self, cellule: str, valeur: int) -> Aucun:
auto.cells[cell] = valeur

def resetCell(self, cellule: str) -> Aucun:
auto.cellules[cellule] = 0

def getValue(self, formule: str) -> Int:
a, b = formule[1:].split('+')
retourner self._eval(a) + self._eval(b)

def _eval(self, token: str) -> Int:
retourner self.cells.get(token, 0) si token[0].isalpha() autre int(token)
«» "

**Test**

'`python
oj = feuille de calcul(3)
print(obj.getValue("=5+7)) # 12
Cell("A1", 10)
print(obj.getValue("=A1+6") # 16
Cell("A1")
print(obj.getValue("=A1+5)) # 5
«» "

---

C'est vrai. C++ – `Spreadsheet.cpp "

'`cpp
#incluez <string>
#inclut <non-ordonné_map>
#incluez <sstream>

classe Feuille de calcul {
public:
// Constructeur – les lignes ne sont pas utilisées dans la logique
Feuille(int rows) {}

vide setCell(const std::string &cell, valeur int) {
cellule[cell] = valeur;
}

réinitialisation du vide Cell(const std::string &cell) {
cellules[cellule] = 0;
}

Int getValue(const std::string &formula) {
// Sauter la tête '= '
md::chaîne expr = formula.substr(1);
taille_t pos = expr.find('+');
std::chaîne gauche = expr.substr(0, pos);
std::chaîne droite = expr.substr(pos + 1);
retour eval(gauche) + eval(droite);
}

particulier:
std::unordered_map<std::string, int> cellules;

Int eval(const std::string &token) {
si [isalpha(token[0])] {
auto it = cells.find(token);
Retournez-le != cells.end() ? it->seconde : 0;
}
retour md::stoi(token);
}
};
«» "

**Compilé**

"""
g++ -std=c++17 -O2 -pipe -statique -s -o principal Feuille de calcul.cpp
«» "

**Utilisation simple* *

'`cpp
la feuille de calcul s(3);
s.setCell("A1", 10);
int res = s.getValue("=A1+5"); // 15
«» "

---

Article du blog – Feuille de calcul de conception : Master LeetCode 3484 avec O(1) HashMap

> **Mots clés:** Plan plan, LeetCode 3484, HashMap, solution O(1), Plan plan plan, Java HashMap, dictionnaire Python, C++ unordered_map, question d'entretien d'algorithme.

Introduction

Lorsque vous appuyez sur LeetCode **3484 – Feuille de calcul de conception**, de nombreux candidats se demandent s'ils ont besoin d'un tableau 2-D complet ou d'une astuce intelligente de la structure des données. L'idée clé est que seul un sous-ensemble *tiny* de cellules se voit attribuer une valeur non nulle. Tous les autres sont implicitement `0`. Cette sparsité nous permet de résoudre le problème en temps constant par opération avec une simple carte de hachage.

---

### Énoncé du problème (reformulé)

> Construire un tableur qui supporte trois opérations :
> 1. `setCell(cell, valeur)` – définissez une cellule à un entier.
> 2. `resetCell(cell)` – remettre à zéro.
> 3. `getValue(formula)` – évaluez le nombre de nombres entiers ou de références cellulaires.

Les contraintes sont légères: ≤ 104 appels, lignes ≤ 103, valeurs ≤ 105.

---

- Oui. Pourquoi un HashMap gagne

Raisons Détails
C'est quoi ?
**Space–Efficace** , Nous ne stockons que les cellules. Dans le pire des cas 104 cellules → < 10 k entrées. Autres
**Constant-Time** Autres
**Aucune validation de ligne requise**Le problème garantit des références valides; nous pouvons ignorer en toute sécurité les contrôles de limites. Autres
Autres **Mise en œuvre simple**=Le partage de la formule et la décision entre une recherche ou une analyse est trivial. Autres

---

### Mise en oeuvre étape par étape

1. ** Structure des données** – `map` (`unordered_map`/`dict`) de la chaîne à l'entier.
2. **setCell** – `map[cell] = valeur`.
3. **resetCell** – `map[cell] = 0` (ou `map.erase(cell)` si vous voulez enregistrer une clé).
4. **getValue** –
- Bande menant `=`.
- Séparer sur "+".
- Pour chaque opérande :
- Si le premier char est une lettre → `map.getOrDefault(token, 0)`.
- Autrement → `int(token)`.
- Retourne la somme.

Toutes les opérations sont "O(1)".

---

Cas et pièges de bord

Scénario Que regarder
-- -- -- -- -- -- -- -- --
Autres La cellule ne doit jamais être définie. "0". Autres
Autres Réinitialisez une cellule qui n'a jamais été définie. Autres
Formule contient des nombres avec des zéros de tête Int s'en occupe. Autres
Autres Très grands nombres ('.. 105') Autres
Formule non valide Le problème garantit la validité; pas besoin de gérer les erreurs. Autres

---

Variantes dans d'autres langues

Syntaxe Mise en évidence Autres
Il y a un problème.
Utiliser `HashMap` + `getOrDefault`. Autres
Utiliser `dict.get(token, 0)` et `int(token)`. Autres
**C++**= `unordered_map<string,int>`; `isalpha(token[0])` pour détecter une cellule. Autres

---

### Vérification des performances

Langue Mémoire Durée (approx.) Autres
C'est ce qu'on dit.
Java < 2 Mo < 0,1 ms par appel
Python < 5 Mo < 0,2 ms par appel
C++=2 MB= 0,05 ms par appel

> *Note:* Ces chiffres sont pour les environnements de juges en ligne typiques. Vos temps de fonctionnement locaux peuvent différer.

---

Dernier verdict

La solution O(1) avec une carte de hachage est la façon la plus propre, la plus rapide et la plus conviviale de résoudre **Design Spreadsheet**. Il s'élargit sans effort et démontre une forte compréhension des structures de données peu nombreuses, exactement le genre de perspicacité que les gestionnaires d'embauche aiment dans les entrevues par algorithme.

Bon codage ! C'est ce qu'il a dit.

---

Clôture

N'hésitez pas à copier les extraits de code ci-dessus, à les lancer contre le harnais de test officiel LeetCode, et à les adapter à tout autre problème d'entrevue semblable à un tableur. La clé à emporter : **Lorsque vous pouvez traiter les entrées manquantes comme des valeurs par défaut, les hash‐maps sont votre meilleur ami. **