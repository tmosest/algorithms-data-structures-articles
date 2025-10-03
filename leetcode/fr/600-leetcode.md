---
titre: LeetCode 600. Les nombres entiers non négatifs sans les nombres consécutifs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 600 – *Titres non negatifs sans éléments consécutifs*
**Langues:** C++
**Tags:** `Programmation dynamique`, `Manipulation de bits`, `Récursion`, `Question d'entrevue "

---

Résumé du problème

> **Don** un entier positif «n» (1 ≤ n ≤ 109).
> **Retour** le nombre d'entiers dans la gamme inclusive `[0, n]` dont la représentation binaire **ne contient pas** deux `1`s consécutifs.

**Exemples**

Réponse
C'est pas vrai.
5. Le chiffre < < 0,110 100 101 > > – seul le chiffre < < 11 > > (3) est invalide
1-
,10'

---

Pourquoi cette question se pose pour les entrevues

* Tests *programmation dynamique* connaissance – la récurrence de type Fibonacci est cachée derrière les contraintes binaires.
* Forcez-vous à penser aux opérations de niveau **bit** et à la représentation de l'État.
* Peut être résolu en **O(log n)** time – une vitrine parfaite de l'efficacité algorithmique.

Si vous pouvez attraper ce problème (et l'expliquer proprement), vous vous démarquerez des gestionnaires d'embauche à **FAANG, Bloomberg, Google, Microsoft, etc.* *

---

Idée de solution – Digit DP + Fibonacci Cache

C'est pas vrai. Observer la structure

* Let `dp[i]` est le nombre de chaînes binaires valides de longueur `i` (i` bits) qui ** ne contiennent pas** de `1`s consécutifs.
* La récurrence est simplement la séquence Fibonacci:

«» "
dp[0] = 1 // chaîne vide
dp[1] = 2 // "0" et "1"
dp[i] = dp[i-1] + dp[i-2] (i ≥ 2)
«» "

Raison:
- Oui. Si le premier bit est `0`, les bits `i‐1` restants peuvent être n'importe quelle chaîne valide de longueur `i‐1`.
- Oui. Si le premier bits est `1`, le second bits doit être `0`, laissant `i‐2` des bits libres.

Numéros de compte ≤ n

Marchez à travers les bits de `n` du bit le plus significatif (MSB) au bit le moins significatif (LSB).
Maintenir :

- `prev` – si le bit précédent était `1`.
- `ans` – nombre cumulé de nombres valides découverts jusqu'à présent.

À chaque position de bit `i`:

«» "
Si n a un 1 à la fois i:
// Si nous définissons ce bit à 0, les bits inférieurs restants peuvent être n'importe quelle chaîne de longueur valide i
ans += dp[i]
// Si nous définissons ce bit à 1, nous devons vérifier que prev==0 (pas de 1s consécutifs)
si prev == 1: // consécutifs apparaissent
break // aucun autre nombre n'est valide
Prév = 1
Sinon:
prev = 0
«» "

Après avoir terminé la boucle, inclure `n` lui-même (si elle n'a pas de consécutifs) en ajoutant 1.

C'est vrai. Complexité

* **Heure:** `O(log n)` – nous balayons au plus 31 bits (`n ≤ 109`).
* **Espace:** `O(1)` – seulement quelques variables entières et un petit tableau DP de taille ~32.

---

Mise en œuvre du code

- Oui. 1. Java

"Java
solution de classe publique {
// Précalculé dp[0,31] pour une séquence similaire à Fibonacci
int[] dp = nouveau int[32];

solution publique() {
dp[0] = 1;
dp[1] = 2;
pour (int i = 2; i < dp.longueur; i++) {
dp[i] = dp[i - 1] + dp[i - 2];
}
}

Recherche publique Integers(int n) {
Int ans = 0;
int prev = 0; // bit précédent traité
pour (int i = 30; i >= 0; i--) { // 31 bits suffisent pour n <= 1e9
si ((n >> i) et 1) == 1) { // bit i est 1
ans += dp[i]; // mettre 0 ici
si (prév) 1) {/ créerait 11
retour et // arrêt, le repos est invalide
}
prev = 1; // définissez ce bit à 1
} autre {
prev = 0; // bit est 0
}
}
retourner les ans + 1; // inclure n lui-même
}
}
«» "

- Oui. 2. Python

'`python
Solution de classe:
def _init_(self):
auto.dp = [0] * 32
auto.dp[0], auto.dp[1] = 1, 2
pour i dans la plage(2, 32):
- C'est pas vrai. = auto.dp[i - 1] + self.dp[i - 2]

def trouver Integers(self, n: int) -> Int:
ans = 0
prev = 0
pour i dans la plage(30, -1, -1): # 31 bits
si (n >> i) & 1:
ans += self.dp[i] # définissez ce bit à 0
si prev == 1: # consécutif 1 apparaîtrait
retour et
Prév = 1
Sinon:
prev = 0
retourner les ans + 1 # inclure n lui-même
«» "

- Oui. 3. C++

'`cpp
solution de classe {
public:
Solution {
dp[0] = 1;
dp[1] = 2;
pour (int i = 2; i < 32; ++i)
dp[i] = dp[i - 1] + dp[i - 2];
}

int trouver Totals(int n) {
Int ans = 0;
int prev = 0;
pour (int i = 30; i >= 0; --i) {
si ((n >> i) et 1) {
la valeur de l'élément de référence est égale à la valeur de référence de l'élément de référence.
si (prév) 1) retourner les ans; // consécutif 1 trouvé
Prév = 1;
} autre {
prev = 0;
}
}
retourner les ans + 1; // inclure n lui-même
}
particulier:
dp[32];
};
«» "

---

Article sur le blog – Le bon, le mauvais et le mauvais de LeetCode 600

Titre
> **Les intégrateurs non négatifs sans éléments consécutifs – les bons, les mauvais et les mauvais (un guide d'entrevue gagnant)* *

### Description de la méta (SEO)
> Master LeetCode 600 en Java, Python et C++. Apprenez la programmation dynamique, les bit tricks, les pièges, et comment aser ce difficile problème d'entrevue. Parfait pour les chercheurs d'emploi en génie logiciel.

---

Introduction

Dans le monde du codage des interviews, une question se pose toujours en haut des listes de "hard" : **LeetCode 600 – *Négatifs entiers sans consécutifs***.
Pourquoi ? Parce que cela vous force à mélanger **bitwise perspicacité** avec **dynamique programmation**. Si vous pouvez le résoudre proprement et expliquer le raisonnement, vous impressionnerez les gestionnaires d'embauche à Google, Amazon, Microsoft, et au-delà.

Cet article plonge dans:

* La **good** – élégante solution DP qui fonctionne en O(log n).
* Les **mauvais** – pièges communs, idées fausses, et pourquoi la récursion naïve échoue.
* Le **ugly** – des tentatives trop optimisées ou piratées qui brisent la lisibilité.

Et oui – nous allons vous montrer le code de travail en **Java**, **Python** et **C++** afin que vous puissiez choisir la langue avec laquelle vous êtes le plus à l'aise.

---

C'est pas vrai. Le problème en anglais clair

> **Donné** d'un entier `n` (1 ≤ n ≤ 109), compter tous les nombres `x` dans la plage `[0, n]` de sorte que la représentation binaire de `x` ne contient *pas* deux `1`s adjacents.

**Pourquoi est-ce difficile? **
Parce que vous ne pouvez pas juste brut-force `0...n`. Même à 109, c'est un milliard de chèques. Le défi est de compter *implicitement* en utilisant les mathématiques.

---

C'est vrai. Le bon – Un DP propre + Digit‐DP Approche

1. **Construire une table de type Fibonacci* *
* `dp[i]` = nombre de chaînes binaires valides de longueur `i`.
* Récurrence: `dp[i] = dp[i-1] + dp[i-2]` (fibonacci classique).
* Complexité : pré-computation constante (32 entrées).

2. **Procéder aux bits de `n`**
* Marchez de la partie la plus significative jusqu'à 0.
* Lorsque le bit actuel de `n` est `1`, nous avons deux choix:
- Réglez-le sur "0" : tous les bits inférieurs peuvent être n'importe quelle chaîne valide de cette longueur (`dp[i]`).
- Réglez-le sur `1`: seulement si le bit précédent n'était pas `1`.
* Arrêtez tôt si deux "1" consécutifs apparaissent.

3. **Ajouter le numéro final**
* Après la boucle, nous avons compté tous les nombres *plus petits* que `n`.
* Inclure `n` s'il n'a pas de `1`s consécutif.

**Résultat** – temps O(log n), espace O(1).

---

C'est vrai. Les mauvais – ce qui va mal

Une mauvaise pratique
C'est quoi ?
Autres **Récursion temporaire** (annexe 0/1 et nombre) Pour `n = 1e9`, la profondeur de récursion et le nombre d'appels explosent au-delà de toute pile possible. Autres
**Programmation dynamique sans mémoisation** Autres
**Ignorer la longueur du bit** Autres
Alors que `int` suffit pour 109, utiliser l'arithmétique 64 bits partout ralentit marginalement la solution et peut induire en erreur sur la vraie complexité. Autres

> **Ligne de bottom:** Visez la solution O(log n) digit‐DP. Il est concis, rapide et à l'échelle maximale.

---

C'est pas vrai. Le mauvais – trop optimisé / difficile à– Lire le code

Parfois, les candidats essaient de presser chaque milliseconde de:

* Écrire une seule ligne de magie bit-wise qui est cryptique (`ans += (1 << i) & ~(1 << (i+1)) - 1)`).
* Déroulement des boucles ou simulation manuelle de la pile au lieu de récursion.
* Surmener chaque opération triviale, encombrer la logique.

> ** Conseil professionnel :** *Readability = score d'entrevue. *
> Une solution propre et bien structurée est généralement meilleure qu'un liner unique que personne d'autre ne peut comprendre.

---

C'est vrai. Code Java / Python / C++ (Voir ci-dessus)

> Copiez l'extrait qui correspond à votre langue d'entrevue. N'oubliez pas de tester avec les exemples de cas !

---

- Oui. Comment utiliser cette connaissance pour trouver un emploi

1. ** Mettre en avant le concept**
* Dans votre curriculum vitae et LinkedIn : LeetCode 600 dans O(log n) en utilisant la manipulation DP + bit. (en milliers de dollars)
* Dans les interviews : J'ai utilisé une table DP de type Fibonacci pour compter les chaînes binaires valides, puis j'ai effectué un chiffre PDD traversée de `n`.

2. **Expliquer les compromis**
* Une récursion naïve frapperait un temps exponentiel; ma solution s'échelonnerait jusqu'à la limite de 32 bits. (en milliers de dollars)
* J'ai évité l'utilisation de la mémoire lourde; la table DP s'intègre dans un tableau fixe. (en milliers de dollars)

3. **Afficher le code dans la langue de l'entreprise* *
* Beaucoup de géants de la technologie ont Java ou C++ dans leur pile de technologie; Python est souvent utilisé pour le script.
* Les trois versions montrent une polyvalence.

4. **Questions de suivi pratiques* *
Et si `n` étaient 64-bits? – Réponse : Augmentez le tableau DP à 64 entrées.
* * Pourriez-vous généraliser pour k consécutif `1`s? - Réponse: Étendre la récurrence DP en conséquence.

---

Conclusion

LeetCode 600 est plus qu'un puzzle de comptage numérique. C'est un **microcosme des défis d'entrevue** – combiner la perspicacité mathématique, l'efficacité algorithmique et une communication claire.

En maîtrisant le **bon**, en évitant le **mauvais**, et en s'éloignant du **ugly**, vous allez entrer dans une interview avec confiance.

Bon codage – et bonne chance d'atterrir ce rôle d'ingénierie logicielle de rêve!

---

Auteur Bio
> *Alex Chen* – Ingénieur en stack complet, 5 ans et plus chez Cloud Services, mentor sur *LeetCode Solutions* et *Coding Interview Prep*. Suivez-moi sur Twitter @AlexCoding pour plus d'interviews hacks.

---

Références
* LeetCode Problem 600 – [https://leetcode.com/problems/non-negative-integers-out-consecutive-ones/](https://leetcode.com/problems/non-negative-integers-out-consecutive-ones/)
* Classic Fibonacci DP – Wikipedia.

---

* Fin du blog *

---

Ce post complet devrait vous aider à maîtriser LeetCode 600, éviter les pièges communs, et impressionner les intervieweurs, que vous soyez code dans **Java**, **Python** ou **C++**. Joyeux entretien !