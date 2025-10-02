---
titre: LeetCode 400. Nième chiffre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème (le code 400 – **Nième chiffre**)

Avec un entier **n**, retourner le nième chiffre de la séquence entière infinie

«» "
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, ...
«» "

> *exemple*
> `n = 11` → **0** (le onzième chiffre est le deuxième chiffre du chiffre 10)

> **Constraints**
> `1 ≤ n ≤ 231 – 1`

Le but est de le faire en **O(log n)** temps sans générer la séquence entière.



-----------------------------------------------------------------------------------

- Oui. 2. Idées fondamentales

Les chiffres sont groupés par leur nombre.

Nombres Nombres totaux
C'est quoi, ça ?
D'après les résultats de l'enquête
100 × 2 = 180
100 à 999 900 × 3 = 2700
- Oui.

1. **Trouver le bloc** qui contient le nième chiffre.
Soustraire les tailles de blocs de *n* jusqu'à *n* s'insère dans le bloc courant.

2. **Locez le nombre exact** dans ce bloc.
`nombre = début + (n‐1) / chiffreLongueur "

3. **Extrait le chiffre** de ce numéro.
Convertir en chaîne ou utiliser division/modulo.

-----------------------------------------------------------------------------------

- Oui. 3. Mise en œuvre des références

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Tous les trois utilisent la même approche basée sur les mathématiques.

---

#### 3.1 Java

"Java
solution de classe publique {
NthDigit(int n) {
// Numéros à 1 chiffre (1-9)
nombres int = 1;
nombre long = 9; // combien de nombres dans ce bloc
base longue = 1; // premier nombre dans ce bloc

pendant que (n > chiffres * nombre) {
n -= chiffres * nombre; // sauter le bloc entier
chiffres++; // prochain bloc
nombre *= 10; // 10× nombres supplémentaires
base *= 10; // le premier nombre est 10^ chiffres
}

// le nombre qui contient le nième chiffre
nombre long = base + (n - 1) / chiffres;
int digitIndex = (int) (n - 1) % digits);

// retourner le chiffre requis
Chaîne s = Long.toString(nombre);
retourner s.charAt(digitIndex) - '0';
}
}
«» "

**Points clés* *

* `long` est utilisé pour éviter le débordement lorsque `n` est proche de `231 – 1`.
* L'algorithme est `O(log10 n)` parce que la boucle itère au plus 10 fois.



---

3.2 Python

'`python
Solution de classe:
def findNthDigit(self, n: int) -> Int:
chiffres = 1 # longueur du chiffre courant du bloc
nombre = 9 nombres # dans ce bloc
start = 1 # premier numéro dans ce bloc

# Étape 1 – trouver le bloc
alors que n > chiffres * comptent:
n -= chiffres * nombre
chiffres += 1
Nombre *= 10
début *= 10

# Étape 2 – localiser le numéro
nombre = début + (n - 1) // chiffres
# Étape 3 – chiffre à l'intérieur du nombre
nombre_index = (n - 1) % chiffres
retourner int(str(number)[numer_index])
«» "

**Pourquoi ça marche* *

* La boucle de temps est ≤ 10 fois (pour les entiers 32 bits).
* L'arithmétique entière est sûre en Python – aucun problème de débordement.



---

### 3.3 C++

'`cpp
solution de classe {
public:
int findNthDigit(int n) {
longs chiffres longs = 1; // longueur du bloc courant
long compte long = 9; // nombres dans le bloc courant
long départ = 1; // premier nombre dans le bloc actuel

// 1) Trouvez le bloc qui contient le nième chiffre
pendant que (n > chiffres * nombre) {
n -= chiffres * nombre;
chiffres++;
nombre *= 10;
début *= 10;
}

// 2) Localiser le nombre exact
nombre long = début + (n - 1) / chiffres;
int digitIndex = (int)(n - 1) digits);

// 3) Extraire le chiffre requis
chaîne s = to_string(nombre);
retourner s[digitIndex] - '0';
}
};
«» "

* "long long" protège contre les débordements.
* La solution suit la même stratégie mathématique.



-----------------------------------------------------------------------------------

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais de Leetcode 400

> ** Mots clés du référencement**:
> *Nth Digit Leetcode*, *Java solution*, *Python solution*, *C++ solution*, *codage interview*, *algorithme interview*, *entretien d'emploi*, *O(log n) algorithme*, *difficulté d'extraction des chiffres*

---

4.1 Introduction

Le problème **Nth Digit** (Leetcode 400) est un puzzle d'entrevue classique qui teste la capacité d'un candidat à raisonner sur les positions numériques, les séquences arithmétiques et la manipulation soigneuse de grands nombres. Bien que la déclaration semble simple, les pièges cachés peuvent monter même les programmeurs chevronnés. Dans ce post, nous disséquons le problème dans ses aspects *bon* (meilleures pratiques), *mauvais* (erreurs courantes) et *ugly* (céphalées de fond), et nous fournissons des solutions propres dans **Java, Python et C++**.

> *Pourquoi maîtriser ce problème vous aide - t - il à trouver un emploi? *
> Parce qu'il présente :
> 1. **Aperçu mathématique** – transformer un problème apparemment brutal en formule log-time.
> 2. ** Attention au débordement** – critique pour les entrevues sur les limites 32 bits/64 bits.
> 3. **Portabilité en langage brut** – vous pouvez expliquer le même algorithme dans n'importe quelle pile.

---

4.2 Récapitulation des problèmes

> **Objectif:** Retourner le `n`-ième chiffre de la séquence concaténée `123456789101112...`.
> **Constances:** < < 1 ≤ n ≤ 231 − 1 > > (2 milliards de dollars).
> **Pièges typiques:**
> * Générer des nombres ou des chaînes jusqu'à `n` – O(n) temps et mémoire.
> * Oublier que `n` est basé sur 1 tandis que les indices de tableau sont basés sur 0.
> * Dépassement lors du calcul de `10^chiffres` ou `chiffres * count`.

---

### 4.3 Le *bon* – Élégant O(log n) Solution

4.3.1 Mathématiques au travail

1. ** Tailles de la serrure**
* Nombres à 1 chiffre: 9 × 1 = 9 chiffres
* Nombres à 2 chiffres : 90 × 2 = 180 chiffres
* Nombres à 3 chiffres : 900 × 3 = 2700 chiffres

2. **Trouver le bloc** – soustraire la taille du bloc jusqu'à ce que le reste `n` corresponde.
Comme chaque bloc augmente d'un facteur de 10, nous avons besoin au maximum de **10 itérations** pour un entier de 32 bits.

3. **Nombre exact** – une fois que nous connaissons le bloc, le nombre cible est
`nombre = début + (n‐1) / chiffres`.

4. **Digital cible** – l'index à l'intérieur de ce nombre est
«indice numérique = (n‐1) % chiffres».
Nous pouvons soit convertir en chaîne, soit utiliser la division/multiplication entière pour isoler le chiffre.

Pourquoi c'est rapide

L'algorithme est **O(log n)**: la boucle tourne ~10 fois, et le reste est arithmétique à temps constant.
L'utilisation de l'espace est **O(1)**.
Cette efficacité est ce que les intervieweurs veulent voir.

---

4.4 Les erreurs communes

Pourquoi il échoue
- C'est quoi ?
**Bâtiment de chaîne de force brute** (`pour i en 1..n: résultat += i`)
**Utiliser l'int au lieu de long/long**
**Les erreurs hors-par-un**. `n` sont basées sur 1; de nombreuses personnes utilisent par erreur des indices 0. jusqu'à l'étape finale
**Ignorer les nombres à 0 chiffres**
**En supposant que le premier chiffre est toujours non-zéro**.Les nombres comme 100 contiennent 0; oublier de convertir en chaîne peut manquer les zéros de tête.

---

#### 4.5 Les *Ugly* – Quirques de cas de bord

1. **La plus grande «n»**
* `n = 231 – 1 - 2,1 milliards "
* Le bloc à 10 chiffres ('100 000 0000'''9 999 999') commence au chiffre `9 999 999`
* Notre algorithme s'en occupe gracieusement parce que "compte" devient "9 000 000" (toujours dans "long").

2. ** Chiffre zéro à l'intérieur des numéros* *
* Le premier zéro apparaît à la position 10 (le chiffre 10).
* Notre extraction numérique (`(n-1)%digets`) fonctionne parce qu'il indexe dans la représentation de la chaîne, pas la valeur numérique.

3. **Bases non décimales**
* L'algorithme suppose base‐10. Pour les entrevues, clarifier la base, sinon les changements mathématiques.

---

4.6 Extraits de code complets

> **Java**

"Java
solution de classe publique {
NthDigit(int n) {
nombres int = 1;
nombre long = 9;
base longue = 1;
pendant que (n > chiffres * nombre) {
n -= chiffres * nombre;
chiffres++;
nombre *= 10;
base *= 10;
}
nombre long = base + (n - 1) / chiffres;
l'indice int = (int) (n - 1) % de chiffres);
retour Chaîne.valeurDe(nombre).charAt(digitIndex) - '0';
}
}
«» "

> **Python**

'`python
Solution de classe:
def findNthDigit(self, n: int) -> Int:
chiffres, nombre, début = 1, 9, 1
alors que n > chiffres * comptent:
n -= chiffres * nombre
chiffres += 1
Nombre *= 10
début *= 10
nombre = début + (n - 1) // chiffres
retourner int(str(numéro)[(n - 1) % chiffres])
«» "

> **C++**

'`cpp
solution de classe {
public:
int findNthDigit(int n) {
longs chiffres longs = 1, nombre = 9, début = 1;
pendant que (n > chiffres * nombre) {
n -= chiffres * nombre;
chiffres++;
nombre *= 10;
début *= 10;
}
nombre long = début + (n - 1) / chiffres;
int digitIndex = (int)(n - 1) digits);
retourner à_string(number)[digitIndex] - '0';
}
};
«» "

---

4.7 Tester votre mise en œuvre

Valeur prévue Raison
C'est quoi, ça ?
Les 3 premiers chiffres sont 1,2,3
10 contient 0
Le 100e chiffre est le premier '1' du numéro 10
Dernier chiffre du bloc des numéros à 2 chiffres
1900 $1 $ Premier chiffre du bloc des numéros à 3 chiffres $
2147483647: 7: Coffret bord, le plus grand int. 32 bits

Utilisez des tests unitaires ou des scripts rapides pour valider chaque cas.

---

### 4.8 Prise- Points pour votre recherche d'emploi

1. **Afficher la pensée mathématique** – les intervieweurs aiment les algorithmes qui sautent la route O(n) naïve.
2. **Cas de bord à la main avec confiance** – démontrer la conscience du débordement et 1-based vs 0-based thought.
3. **Livrer un code propre et cross-language** – être prêt à expliquer votre solution en Java, Python ou C++ selon la pile d'entretien.
4. **Exposer le temps et la complexité de l'espace** – *O(log n)* le temps, *O(1)* l'espace.
5. **Revenir aux modèles d'entrevue** – ce problème est une variante des questions de DP et de position de séquence qui apparaissent sur de nombreuses pistes d'entrevue.

---

4.9 Pensées finales

Le problème Nth Digit est trompeurment simple mais rempli de concepts pertinents pour l'entrevue : séquences arithmétiques, recherche logarithmique, gestion des débordements et code propre. La maîtrise ne vous rapporte pas seulement 6 mois sur Leetcode, mais montre aussi aux recruteurs que vous pouvez transformer un défi apparemment brutal en une solution élégante O(log n).

Bon codage, et que votre prochaine entrevue soit *n*th-to-the-meilleur!