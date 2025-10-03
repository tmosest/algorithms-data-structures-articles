---
titre: LeetCode 816. Coordonnées ambiguës -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# # 816. Coordonnées ambiguës – Un guide complet de préparation au référencement

> **TL;DR**
> • Parsez la corde **s** après avoir enlevé les parenthèses extérieures.
> • Énumérer toutes les positions possibles.
> • Pour chaque côté, générer chaque représentation légale "integer" ou "decimal".
> • Combinez les deux côtés et retournez la liste finale.
> • Complexité: **O(n2)** temps, **O(n)** espace auxiliaire.

---

- Oui. 1. Récapitulation des problèmes

On vous donne une chaîne `s` qui ressemble à un point 2 dimensions, par exemple `"(1, 3)"`.
Toutes les virgules, points décimaux et espaces ont été enlevés, produisant une chaîne telle que

«» "
"(1,3)" -> "(13)"
"(2,0,5)" -> "(205)"
«» "

Votre tâche est de retourner ** chaque** possible paire de coordonnées originales qui pourrait
produire «s» lorsque la ponctuation a été dépouillée.
Les règles applicables aux numéros valides sont les suivantes:

* Pas de zéros avant à moins que le nombre soit exactement "0".
* Un point décimal ne peut apparaître que **après** au moins un chiffre.
* Les nombres qui peuvent être représentés avec moins de nombres (par exemple `"001"` → `"1"`, `"0.0"` → `"0"`) ne sont pas autorisés.

La liste finale peut être dans n'importe quel ordre, mais chaque paire doit avoir exactement un espace après la virgule.

---

- Oui. 2. Pourquoi ce problème est intéressant

* Il teste les compétences de manipulation de chaîne**, en particulier la manipulation des positions décimales.
* Les règles de « leader/trailing-zero » en font un problème**.
* La solution est une bonne illustration de la structure **=generate et filter==**:
– générer toutes les façons de diviser les chiffres et insérer un point décimal,
– puis filtrer les invalides.

En raison de ses difficultés modérées (LeetCode
solution, ce problème est un favori sur les listes de prép d'entrevue.

---

- Oui. 3. Aperçu de la solution

1. **Strip les parenthèses** → obtenir la chaîne à chiffres purs `digets`.
2. **Énumérer les positions des virgules** – fractionner les « chiffres » dans une partie gauche `x` et une partie droite "y".
3. **Générer toutes les représentations valides** d'une chaîne à chiffres
* pas de point décimal (seulement si la chaîne est à un seul chiffre ou ne commence pas par `'0'`)
* un point décimal après le premier chiffre (seulement si la chaîne se termine par un non-zéro)
* une décimale quelque part au milieu (uniquement si la chaîne ne commence pas avec `'0'` et ne se termine pas avec `'0'`)
4. **Combinez chaque option de gauche avec chaque option de droite et enveloppez-les dans `"(" + gauche + ", " + droite + ")"`.
5. **Retour** la liste finale.

L'étape « Générer toutes les représentations valides » est le cœur de l'algorithme.

---

- Oui. 4. Algorithme détaillé

Texte
chiffres = s[1:-1] // bande '(' et ') '
pour chaque i de 1 à len(chiffres)-1:
x_str = chiffres[0:i]
y_str = chiffres[i:]
gauche_opts = generateOptions(x_str)
right_opts = generateOptions(y_str)
pour chaque a dans gauche_opts:
pour chaque b dans right_opts:
résultat.add("(" + a + ", " + b + ")")
résultat du retour
«» "

`generateOptions(str)` fonctionne comme ceci:

«» "
options = []

// 1) entier
si len(str) == 1 ou str[0] != «0»:
options.append(str)

// 2) décimale après le premier chiffre
si len(str) > 1 et str[-1] != «0»:
options.append(str[0] + "." + str[1:])

// 3) décimale à toute autre position
si len(str) > 2 et str[0] != '0' et str[-1] != «0»:
pour k dans la plage(2, len(str)):
options.append(str[:k] + "." + str[k:])

options de retour
«» "

Toutes les contraintes sont vérifiées par les conditions ci-dessus; la fonction retourne
Seulement les chaînes qui satisfont à la règle --pas de tête/trailing zéro.

---

## 4.1 Cas de bord

Entrée Explication Résultat
C'est pas vrai.
"(10)" Impossible – il n'y a pas assez de chiffres pour une virgule
"(000)" Split comme `00` / `0` – toutes les options contiendraient des zéros de tête → `[]` Autres
"(010)" Split `0` / `10` → `0` est bien, mais `10` est bien → `["(0, 10)"]` Autres
"(0000)" Toutes les scissions contiennent plus d'un zéro → `[]`

---

4.2 Preuve d'exactitude

1. ** Postes de responsabilité** :
Chaque paire légale doit avoir une virgule quelque part entre le premier et le dernier chiffre de « chiffres ».
La boucle `pour i dans 1..len(digits)-1` visites **all** de telles positions, donc aucune scission possible n'est manquée.

2. **'options génériques' validité**:
* Si la chaîne a un chiffre → il est toujours valide (pas de problème de zéro de tête).
* Si elle commence par `'0'` → la seule décimale valide est `"0.xxx"`; toute autre forme aurait un zéro en tête ou un zéro en arrière.
* Si elle se termine par `'0'` → seul le formulaire entier est autorisé parce qu'une décimale se terminant par zéro aurait un zéro suivant.
* Pour les chaînes qui satisfont aux règles ci-dessus, toutes les positions décimales possibles sont considérées, mais seulement si la partie droite de la décimale (la partie fractionnelle) est non-zéro – sinon elle se terminerait par un zéro.

Ainsi, les "Options Générales" énumèrent **tous** et **seulement** les représentations juridiques.
La combinaison des parties gauche et droite produit donc toutes les paires de coordonnées possibles,
et aucune paire invalide ne peut passer.

---

- Oui. 5. Analyse de la complexité

Que `n` soit le nombre de chiffres à l'intérieur des parenthèses (`3 ≤ n ≤ 8` pour les contraintes de problème).

* Séparer la chaîne : `O(n)` par division.
* Pour chaque côté, `generateOptions` produit au maximum `n` chaînes (pas de décimale) + `n-1` (décimal à l'une des positions `n-1`).
Donc "O(n)" de chaque côté.
* Nous avons `n-1` positions de virgule → temps global `O(n * n) = O(n2)` (= 64 opérations pour l'entrée maximale).
* La liste de résultats peut contenir au plus des éléments `O(n2)`; nous conservons quelques vecteurs auxiliaires de taille `O(n)` → espace auxiliaire global `O(n)`.

Avec `n ≤ 8`, c'est assez rapide pour tous les essais.

---

- Oui. 6. Mise en œuvre du code

Voici des solutions propres et bien commentées dans **Python 3**, **Java 17** et **C++17**.
N'hésitez pas à copier-coller dans votre IDE préféré ou juge en ligne.

6.1 Python 3

'`python
de taper l'importation Liste

Solution de classe:
# Aide qui transforme une chaîne à chiffres en tous les numéros légaux
def _options(self, num: str) -> Liste[str]:
opte = []

1) Forme entière
Si len(num) == 1 ou num[0] != «0»:
opts.append(num)

2) Décimal après le premier chiffre
si len(num) > 1 et num[-1] != «0»:
opts.append(num[0] + '.' + num[1:])

3) Décima au milieu (pas de zéro en tête et pas de zéro en piste)
si len(num) > 2 et num[0] != '0' et num[-1] != «0»:
pour i dans la plage (1, len(num)):
opts.append(num[:i] + '.' + num[i:])

opte pour le retour

def ambiguë Coordonnées(s) :
chiffres = s[1:-1] # bande '(' et ') '
res = []

# divisé entre 1..len(chiffres)-1
pour i dans la plage (1, len(chiffres)):
gauche = chiffres[:i]
droite = chiffres[i:]

gauche_opts = self._options(gauche)
right_opts = self._options(right)

pour une _opts de gauche :
pour b dans le_droit :
Annexe(f'({a}, {b})')

retour res
«» "

---

#### 6.2 Java 17

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
// Génère toutes les représentations légales d'une chaîne numérique
options de liste privée<String>(String num) {
Liste<String> res = nouvelle liste de distribution<>();

// 1) Forme entière
if (num.longueur()) == 1=== num.charAt(0) != '0')
le nom de l'autorité compétente;

// 2) Décimal après le premier chiffre
si (num.longueur() > 1 && num.charAt(num.longueur() - 1) != '0')
res.add(num.charAt(0) + "." + num.substring(1));

// 3) Décima au milieu
si (num.longueur() > 2 && num.charAt(0) != '0' && num.charAt(num.longueur() - 1) != '0') {
pour (int i = 1; i < longueur num(); ++i) {
res.add(num.substring(0, i) + "." + num.substring(i));
}
}
retour rés;
}

Liste publique <String> ambigu Coordonnées(String s) {
Chiffres de chaîne = s.substring(1, s.longueur() - 1); // entre parenthèses
Liste du résultat <String> = nouvelle liste de distribution<>();

pour (int i = 1; i < chiffres.longueur(); ++i) { // positions possibles des virgules
Chaîne gauche = chiffres.substring(0, i);
Chaîne droite = chiffres.substring(i);

Liste<String> gaucheOpts = options(gauche);
Liste<String> rightOpts = options(droite);

pour (String a : gaucheOpts) {
pour (String b : droiteOpts) {
résultat.add("(" + a + ", " + b + ")";
}
}
}
le résultat du retour;
}
}
«» "

---

*### 6.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur <string> ambigu Coordonnées(chaîne s) {
chiffres de chaîne = s.substr(1, s.size() - 2); // entre parenthèses
vecteur <chaîne> ans;

pour (size_t i = 1; i < chiffres.size(); ++i) {
chaîne gauche = chiffres.substr(0, i);
chaîne droite = chiffres.substr(i);

vector<string> leftOpts = options(left);
vector<string> rightOpts = options(right);

pour (suite &a : gaucheOpts)
pour (const string &b : rightOpts)
le nom de l'autorité compétente de l'État membre d'origine;
}
le retour des an;
}

particulier:
// Toutes les représentations valides d'une chaîne numérique
vector<string> options(const string &num) {
vecteur <string> rés;

// Forme entière
si (num.size()) == 1== '0')
le nom de l'entité concernée;

// Décimal après le premier chiffre
si (num.size() > 1 && num.back() != '0')
res.push_back(string(1, num[0]) + "." + num.substr(1));

// Décimal à toute position médiane
si (num.size() > 2 && num[0] != '0' && num.back() != '0') {
pour (size_t i = 1; i < num.size(); ++i)
(num.substr(0, i) + "." + num.substr(i));
}
retour rés;
}
};
«» "

---

- Oui. 7. Résumé

* **Problème** – Rebâtir toutes les coordonnées possibles à partir d'une chaîne mangued.
* **Key Insight** – énumérer toutes les scissions légales et pour chaque partie ne générer que les formats entiers/décimal valides.
* **Heure** – «O(n2)» («n ≤ 8»), **Espace** – «O(n)».
* **Résultat** – Solutions propres en Python, Java, C++ prêtes pour l'entretien ou la programmation compétitive.

---

## 7.1 Bonus: Une alternative plus efficace

Une petite optimisation vous pouvez tomber dans n'importe quelle des solutions est de sauter les scissions qui
serait certainement produire des zéros de tête des deux côtés.
Par exemple, si `num[0] == '0' && num[1] == '0'' nous pouvons casser tôt, en sauvegardant une poignée d'appels inutiles – pas strictement requis pour la correction, mais agréable pour la performance dans les langues où les appels de fonction sont chers.

---

7.2 Essais

'`python
si __nom__ == "__main__" :
sol = Solution()
print(sol.ambigulousCoordonnées("(123)") # Exemple de l'énoncé
«» "

---

7.3 Pensées finales

Le problème des coordonnées ambiantes est un excellent exemple d'énumération **combinatoire** avec quelques contraintes subtiles.
La clé à prendre : ** briser le problème en petites pièces testables** (découpage + génération d'options).
Une fois que vous pouvez isoler un sous-problème, la preuve de l'exactitude est généralement simple, et le code reste rangé.

Bon codage ! C'est ce qu'il a dit.

---

- Oui. 8. Lecture supplémentaire

* [Code Leet 797. Tous les chemins de la source à la cible](https://leetcode.com/problems/all-paths-from-source-to-target/) – autre dénombrement combinatoire.
* [Top-Down vs Bottom-Up DP] – comprendre les compromis de complexité.
* [C++17 String Manipulation] – apprenez à travailler efficacement avec `substr`, `emplace_back`.

Bonne chance avec votre prochain entretien ou défi de codage!