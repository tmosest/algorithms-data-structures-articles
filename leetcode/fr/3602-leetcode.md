---
Titre: LeetCode 3602. Conversion hexadécimal et hexatrigesimale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3602 – Hexadécimal et hexatrigesimal Conversion
Java, Python, C++, Blog**

> *Le bon, le mauvais, et la laid de ce problème de conversion apparemment trivial – et pourquoi la maîtriser vous atterrira cette interview de niveau suivant.

---

Aperçu du problème

Valeur du champ
C'est pas vrai.
**ID**
Difficulté facile
*Tags * Math, chaîne, base-conversion Autres
**Contrairements**
Pour un entier donné `n`, rendez la concaténation de:
  • la représentation hexadécimal de `n2`
  • la représentation hexatrigesimale (base‐36) de `n3` Autres

**Exemple**
«» "
n = 13
n2 = 169 → "A9" (hex)
n3 = 2197 → "1P1" (base‐36)
Résultat = "A91P1"
«» "

---

Pourquoi ce problème est-il un problème d'entrevue

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Les conversions de base**=Les intervieweurs aiment voir si vous pouvez manipuler des nombres à un niveau bas. Autres
**Manipulation de la chaîne de caractères** Autres
**Manipulation d'un boitier**= Petites contraintes, mais vous devez toujours vous protéger contre les nombres négatifs, zéro ou les grandes bases. Autres
**Temps/espace compromis**=Une bonne solution est le temps O(log n), l'espace O(log n) – parfait pour le buzz d'entrevue. Autres

---

Défaut de solution

1. ** Pouvoirs informatiques**
- `sq = n * n`
- `cube = n * n * n`

2. **Convertir aux bases requises**
- **Hexadecimal (base‐16)**: formatage intégré → `format(sq, 'X')` dans Python, `Integer.toHexString(sq).toUpperCase()` dans Java, `std::stringstream` ou `std::to_chars` dans C++.
- **Hexatrigesimal (base‐36)**: aussi un fichier intégré → `format(cube, '36').upper()` dans Python, `Integer.toString(cube, 36).toUpperCase()` dans Java, `std::to_chars` avec radix 36 dans C++.

3. **Concaténat* *
- Retour `hex_part + base36_part`.

4. **Cas**
- Pour `n = 1`, `sq = 1`, `cube = 1` → résultat `"11"`.
- Aucune manipulation particulière nécessaire pour `n = 0` parce que `n ≥ 1`.

---

Code – 3 langues

Python 3

'`python
Solution de classe:
def concatHex36(self, n: int) -> str:
Pouvoirs
2 = n * n
cube = n * n * n

N° 2 Conversions de base
hex_part = format(sq, 'X') # hexagonal supérieur
base36_part = format(cube, '36').upper() # base 36

N° 3 Concatenate
retour_partie + base36_partie
«» "

**Complexité* *

Valeur métrique
C'est pas vrai.
Heure O(log n)
Espace O(log n)

---

### Java

"Java
solution de classe publique {
chaîne publique concatHex36(int n) {
Pouvoirs
int sq = n * n;
cubique int = n * n * n;

//
Chaîne hexaPièce = Integer.toHexString(sq).toUpperCase();
Base de chaînes36Part = entier.toString(cube, 36).toUpperCase();

Concaténat
retour hexPart + base36 Partie;
}
}
«» "

**Complexité* *

Valeur métrique
C'est pas vrai.
Heure O(log n)
Espace O(log n)

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne concatHex36(int n) {
long sq = 1LL * n * n;
long cube = 1LL * n * n * n;

// Aide à convertir un nombre en n'importe quelle base (2‐36)
auto toBase = [](long num, base int) -> chaîne {
Const string chiffres = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
Si (nombre) 0) retourner "0";
la chaîne rés;
pendant la période 0) {
res.push_back(digits[num % base]);
num /= base;
}
inverse(res.begin(), res.end());
retour rés;
};

chaîne hexPart = toBase(sq, 16);
chaîne de caractères base36Part = toBase(cube, 36);
retour hexPart + base36 Partie;
}
};
«» "

**Complexité* *

Valeur métrique
C'est pas vrai.
Heure O(log n)
Espace O(log n)

---

Article de blog optimisé par le SEO

> *Titre:* **LeetCode 3602 – Maître Hexadécimal et Hexatrigesimal Conversion en Java, Python et C++* *
> *Meta Description:* Solve LeetCode 3602 en secondes. Obtenez des solutions Java, Python et C++, comprenez l'algorithme et apprenez des conseils prêts pour l'entretien.

---

C'est pas vrai. Qu'est-ce que Hexatrigesimal ?

- La base‐36 (0–9, A–Z) est souvent utilisée pour les identifiants compacts.
- Oui. Dans ce problème, vous devez convertir `n3` en base‐36.
- Oui. La même logique fonctionne pour toute base jusqu'à 36, un astuce utile pour de nombreux puzzles d'entrevue.

---

C'est vrai. Le code "bien" – propre et idiomatique

- **Built‐ins**: Utilisez les aides linguistiques (`Integer.toString(..., 36)` en Java, `format(..., '36')` en Python).
- **Passe simple**: Pas de boucles supplémentaires ou de récursion.
- **Readability**: Les noms variables (`sq`, `cube`, `hexPart`, `base36Part`) s'expliquent eux-mêmes.

---

C'est vrai. L'Événement – Que faut-il éviter

- **Loops manuelles pour base‐16**: Remise en œuvre de la conversion hexagonale lorsque la bibliothèque standard existe déjà.
- **Débordement entier**: Utilisation de `int` pour `n3` (par exemple, en C++ si vous utilisez `int` au lieu de `long long`).
- **Ignorer les cas de bord**: Oublier `n = 1` renvoie `"11"` ou mal gérer zéro.

---

C'est pas vrai. Le "Ugly" – Un piège commun

> **Mis à l'aide de la fonction de conversion de base** – p.ex., `Integer.toString(n, 36)` renvoie une chaîne **case**. Oublier d'appeler `.toUpperCase()` rend la sortie `"1p1"` au lieu de `"1P1"`.
>
> **Solution**: Toujours appliquer la majuscule dans la chaîne ou le document final que votre fonction de conversion renvoie la majuscule.

---

C'est vrai. Conseils de préparation à l'entrevue

1. **Afficher les mathématiques**
- Expliquer rapidement `n2` et `n3`.
- Mentionnez que le nombre de chiffres augmente logarithmiquement : `digets = =log_base(value)=‘.

2. **Heure et espace**
- Mettre l'accent sur le temps et l'espace O(log n) – parfait pour les grands `n`.

3. **Tricks linguistiques spécifiques* *
- Python: `format(num, 'X')` → hexagone supérieur; `format(num, '36').upper()` → base‐36.
- Java: `Integer.toHexString` + `toUpperCase`; `Integer.toString(num, 36).toUpperCase()`.
- C++: Conversion de base personnalisée ou `std::to_chars` (C++17+) avec support radix.

4. **Démonstration d'un cas d'urgence**
- Exécutez `n = 1`, `n = 36`, `n = 1000` dans votre esprit. Montrez que la solution les gère correctement.

---

- Oui. Pourquoi maîtriser ce problème vous aide à trouver un emploi

- ** Démontre la pensée algorithmique**: Vous convertissez des chiffres, pas seulement des chaînes de force brute.
- **Fait ressortir les connaissances linguistiques**: Connaître les fonctions de conversion intégrées et comment les utiliser est un signal fort pour les recruteurs.
- **S'intéresse aux détails**: Conversion des bases correctement et gestion des questions de sensibilité des cas en code réel.
- ** Facile à expliquer** : Il s'inscrit dans la case de codage de 10 minutes pour de nombreuses entrevues.

---

Enveloppe

LeetCode 3602 est un *quick win* pour la préparation de l'entrevue. Avec une solution d'un liner dans chaque Java, Python et C++, vous pouvez démontrer :

- **Fronts fondamentaux** (math, cordes, bases)
- **Capacité linguistique** (construits, manipulation des caisses)
- **Efficacité** (O(log n) temps/espace)

Maintenant, vous pouvez aborder ce problème avec confiance et le transformer en un point de discussion lors de votre prochain entretien technique. Bon codage ! C'est ce qu'il a dit.

---

**Bonne entrevue!**