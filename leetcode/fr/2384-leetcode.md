---
titre: LeetCode 2384. Le plus grand nombre palindromique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2384 – Le plus grand numéro palindromique
**Type de problème:** Chaîne / Hash-Table / Greedy
**Difficulté:** Moyenne

---

Récapitulation des problèmes

Étant donné une chaîne `num` qui se compose uniquement de chiffres décimaux, vous pouvez :

* **recommander** les chiffres arbitrairement,
* **omit** tout sous-ensemble de chiffres (mais gardez au moins un).

Retourne l'entier palindromique (en tant que chaîne) qui peut être formé.
Le résultat doit **non** contenir des zéros de tête.

> *Exemples*
> `num = "444947137"` → `"7449447"`
> `num = "00009"` → `"9"`

---

2. Aperçu de l'algorithme

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
**1. Compter les fréquences** Autres
**2. Construisez la moitié gauche. Pour chaque chiffre `d`:<br>• Si `cnt[d] ≥ 2` appendice `d` exactement `cnt[d] / 2` fois à un `StringBuilder` `gauche`. Autres
**3. Choisissez le chiffre moyen**. Autres Une seule position peut être au centre; le plus grand chiffre impair donne le milieu maximum. Autres
**3. Monter le palindrome**.Concaténate: `gauche + milieu(facultatif) + inverse(gauche)`. La propriété Palindrome est préservée. Autres
**4. Edge‐cases**. <ul><li>Tous les zéros → réponse `"0"`</li><li>Laisser zéro après la construction de la moitié gauche → retourner le chiffre médian (le cas échéant) ou `"0"`</li></ul> Il gère l'exigence de zéros de tête. Autres

> **Une preuve du mariage**
> La valeur du palindrome est déterminée par l'ordre* de son côté gauche ; le côté droit est une image miroir.
> Tout écart par rapport à l'ordre décroissant remplacerait un chiffre de tête plus grand par un chiffre plus petit, diminuant la valeur.
> La seule liberté est le chiffre central – nous choisissons le *plus grand* chiffre impair-compte parce qu'il donne la contribution moyenne maximale tout en gardant le côté gauche optimisé.

---

- Oui. Complexité

* **Heure:** `O(n)` – un passage pour compter, un passage (soit 10 itérations) pour construire la réponse.
* **Espace:** `O(1)` pour le tableau de fréquences + `O(n)` pour la chaîne de sortie (implicite dans le constructeur).

---

3. Mise en œuvre – Java, Python, C++

> *Les trois versions partagent la même logique. N'hésitez pas à copier-coller l'extrait qui correspond à votre langue préférée. *

---

#### Java 17

"Java
Importation de java.util.*;

solution de classe publique {
publique Chaîne la plus grandePalindromique(String num) {
Nombre de fréquences
int[] cnt = nouvelle int[10];
pour (char ch : num.toCharArray() cnt[ch - '0']++;

// / / / Construisez le côté gauche avec cupidité
StringBuilder gauche = nouveau StringBuilder();
int milieu = -1; // plus grand chiffre impair

pour (int d = 9; d >= 0; d--) {
c = cnt[d];
si (c) 0) poursuivre;

// Sauter les zéros avant
si (longueur gauche) == 0 && d == 0) poursuivre;

// Ajouter des paires à la moitié gauche
paires int = c / 2;
pour (int i = 0; i < paires; i++) gauche.append((char) ('0' + d));

// Si ce chiffre se produit bizarrement, il rivalise pour le milieu
i (c % 2 == 1) milieu = Math.max (moyen, d);
}

Assembler la chaîne finale
StringBuilder ans = nouveau StringBuilder();
si (longueur gauche) == 0 & & milieu == -1) retourner «0»; // tous les zéros

(à gauche);
Si (moyen != -1) ans.append(char) ('0' + milieu));
et/ miroir de la moitié gauche

// 4
si (ans.charAt(0) == '0') retourner String.valueOf(char) ('0' + milieu));

retourner les ans.àString();
}
}
«» "

---

Python 3

'`python
Solution de classe:
def le plus grandPalindromic(self, num: str) -> str:
N° 1 Nombre de fréquences
cnt = [0] * 10
pour ch en nombre:
cnt[int(ch)] += 1

N° 2 Construire la moitié gauche
gauche = []
milieu = -1
pour d dans la plage (9, -1, -1):
c = cnt[d]
si c == 0: continuer
si len (à gauche) == 0 et d) 0: continuer # éviter les zéros

# ajouter des paires
Left.extend([str(d)] * (c/ 2))
# événement étrange -> candidat au milieu
Si c % 2 == 1:
milieu = max (milieu, d)

si ce n'est pas à gauche et au milieu == - 1 :
retourner "0" # tous les chiffres étaient zéro

N° 3 Assembler le palindrome
res = ''.join(gauche)
Si au milieu != - 1 :
res += str(moyen)
res += ''.join(reversed(gauche))
retour res
«» "

---

### C++ (GNU‐C++17)

'`cpp
solution de classe {
public:
chaîne la plus grandePalindromic(chaîne num) {
Nombre de fréquences
vecteur<int> cnt(10, 0);
pour (char ch : num) cnt[ch - '0']++;

Construisez la moitié gauche
chaîne gauche;
int milieu = -1;
pour (int d = 9; d >= 0; --d) {
c = cnt[d];
si (c) 0) poursuivre;
si (left.vide() && d == 0) continuer; // pas de zéro de début

// Ajouter des paires
gauche.annexe(c / 2, char('0' + d));
si (c % 2] 1) milieu = max (milieu, d);
}

// Edge : tous les zéros
si (left.vide() && milieu) == -1) retourner "0";

Assembler la chaîne finale
string res = gauche;
Si (moyen != -1) res.push_back(char('0' + milieu));
inverse(gauche.degin(), gauche.end());
res += gauche;
retour rés;
}
};
«» "

Les trois extraits fonctionnent dans **O(n)** temps et **O(1)** espace auxiliaire (le tableau de fréquences de 10 dimensions). Ils sont compilés dans les normes linguistiques les plus récentes (`Java 17`, `Python 3.8+`, `C++17`).

---

3. Maîtrise de l'arrière-plan (bon, mauvais et mauvais)

Catégorie Que regarder pour: Conseils
C'est pas vrai.
**Bien** - La construction de Greedy garantit l'optimalité. <br> - Logique simple O(n) facile à expliquer. Autres
**Bad** - Manipulation **Le palindrome qui commence par `0` est invalide. <br> - Vous pouvez sauter tous les zéros seulement si la moitié gauche est vide. *Toujours sauter `0` quand le côté gauche est toujours vide.* Autres
**Décider le nombre moyen**: si plusieurs chiffres apparaissent un nombre impair de fois, vous devez choisir le **plus grand** parmi eux. <br> - Lorsque l'entrée est `"0"` ou tous les zéros, la réponse correcte est `"0"` (pas une chaîne vide). * Méfiez-vous de renvoyer `""` – ce n'est pas une chaîne entière valide.* Autres

** Pièges communs* *

Pourquoi il échoue
C'est quoi ?
En utilisant `StringBuilder.reverse()` sur toute la chaîne **après** en ajoutant le chiffre moyen. Autres
Ne pas manipuler `"0000"` → retourne `""`"Les intervieweurs vous attraperont; vous devez retourner `"0"`. Autres
Ne pas sauter en tête `0` lorsque la moitié gauche est vide. Autres

---

4. Code de préparation à l'entrevue

Ci-dessous vous trouverez des implémentations propres et concises pour **Java**, **Python** et **C++** – prêtes à coller dans une soumission LeetCode ou dans votre portefeuille de codage personnel.

- Oui. Java (Java 17)

"Java
solution de classe publique {
publique Chaîne la plus grandePalindromique(String num) {
int[] cnt = nouvelle int[10];
pour (char ch : num.toCharArray() cnt[ch - '0']++;

StringBuilder gauche = nouveau StringBuilder();
int milieu = -1;

pour (int d = 9; d >= 0; d--) {
c = cnt[d];
si (c) 0) poursuivre;
si (longueur gauche) == 0 && d == 0) continuer; // éviter de diriger zéro

// Ajouter des paires
gauche.append(String.valueOf(char) ('0' + d))repeat(c/2);

// Candidat enregistré pour le milieu
i (c % 2 == 1) milieu = Math.max (moyen, d);
}

// Edge‐case: tous les chiffres sont zéro
si (longueur gauche) == 0 & & milieu == -1) retourner "0";

StringBuilder res = nouveau StringBuilder(gauche);
Si (moyen != -1) res.append(char) ('0' + milieu)
res.append(nouveau StringBuilder(gauche).reverse());
retour res.toString();
}
}
«» "

### Python 3 (Python 3.8+)

'`python
Solution de classe:
def le plus grandPalindromic(self, num: str) -> str:
cnt = [0] * 10
pour ch en nombre:
cnt[ord(ch) - 48] += 1

gauche = []
milieu = -1
pour d dans la plage (9, -1, -1):
c = cnt[d]
si c == 0:
poursuivre
si ce n'est pas à gauche et d == 0:
continuer # éviter de diriger zéro

Left.extend([str(d)] * (c/ 2))
Si c % 2 == 1:
milieu = max (milieu, d)

si ce n'est pas à gauche et au milieu == - 1 :
retourner "0" # tous les zéros

res = ''.join(gauche)
Si au milieu != - 1 :
res += str(moyen)
res += ''.join(reversed(gauche))
retour res
«» "

### C++ (GNU C++17)

'`cpp
solution de classe {
public:
chaîne la plus grandePalindromic(chaîne num) {
vecteur<int> cnt(10, 0);
pour (char ch : num) cnt[ch - '0']++;

chaîne gauche;
int milieu = -1;
pour (int d = 9; d >= 0; --d) {
c = cnt[d];
si (c) 0) poursuivre;
si (left.vide() && d == 0) continuer; // éviter de diriger zéro

gauche.annexe(c / 2, char('0' + d));
si (c % 2] 1) milieu = max (milieu, d);
}

si (left.vide() && milieu) == -1) retourner "0";

string res = gauche;
Si (moyen != -1) res.push_back(char('0' + milieu));
inverse(gauche.degin(), gauche.end());
res += gauche;
retour rés;
}
};
«» "

---

Pourquoi ça compte ?

* **Échelle :** `O(n)` résout le problème des limites maximales de LeetCode (`n ≤ 10^4`).
* ** Maintenabilité :** Une table de fréquence est un *design pattern* qui peut être réutilisé pour des problèmes tels que la chaîne de réarrangement ou le palindrome le plus long.
* ** Communication :** L'algorithme est l'une des rares solutions optimales que vous pouvez expliquer en moins de 5 minutes – une grande victoire dans une interview technique.

---

4. Suivis proposés

1. **Analyse de la complexité Q&A** – être prêt à discuter du tableau de fréquences « O(1) » par rapport au hachage dynamique.
2. **Variants** – p.ex. Si vous avez besoin du plus petit palindrome, inversez l'ordre de sélection des chiffres.
3. **Inputs Memory-heavy** – montrez comment vous pouvez diffuser la chaîne (pas de pré-allocation) tout en utilisant la table de fréquence.

---

5. A emporter

*Votre solution est élégante, efficace et passe tous les cas de test. *
N'oubliez pas de souligner la raison d'être gourmande, de traiter les cas avec soin et d'expliquer votre prise de décision lors de la présentation aux intervieweurs. Bonne chance ! C'est ce qu'il a dit.

---

**Tags:** `Java`, `Python`, `C++`, `String`, `Greedy`, `HashMap`, `FrequecyTable`, `Palindrome`, `Algorithme`, `LeetCode`.

---