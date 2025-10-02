---
titre: LeetCode 1622. Séquence de fantaisie - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Séquence de fantaisie (LeetCode 1622) – Solution complète dans **Java, Python, C++**
### TL;DR
* **Heure** – "O(1)" par opération
* **Espace** – `O(n)` pour stocker les valeurs brutes
* **Idea** – conserver deux multiplicateurs et adders cumulatifs de la valeur globale, stocker chaque valeur ajoutée sous une forme *normalisée* et reconstruire la valeur réelle sur requête.

---

- Oui. 2. Pourquoi ce problème est une médaille d'or pour les entrevues

C'est pas vrai.
C'est le cas.
**Hard** – 1622 est coté -Hard sur LeetCode, mais il est *solvable en O(1)* par opération. **Profondeur conceptuelle** – vous montre comprendre l'arithmétique modulaire, les produits de préfixe, les mises à jour paresseuses et comment éviter TLE. **Pitfall** – la solution naïve sera TLE («O(n)» par addAll/multAll). Autres
**Language‐agnostic** – fonctionne en Java, Python, C++ et même JavaScript. **Tricky corner case** – vous devez utiliser l'inverse modulaire lors de l'adaptation après multiplication. Autres
**L'évolutivité** – 105 opérations, 105 éléments → doivent être à temps constant. Autres

---

- Oui. 3. Récapitulation des problèmes

Exemple d'opération (mod = 109+7)
C'est le cas.
"Append(val)" Ajouter `val` à la fin de la séquence.
Ajouter `inc` à chaque élément**.
"multAll(m)" Multiplier **chaque élément** par `m`. Autres
Retourner la valeur courante à `idx` modulo 109+7.

Si `idx` ≥ longueur → retourner `-1`.

---

- Oui. 4. Idées fondamentales

Laissez

* `globalMul` – produit de tous les `multes Toutes les opérations jusqu'ici.
* `globalAdd` – somme de tous `ajouter Toutes les opérations, *mais éparpillées par le " GlobalMul " actuel.

Lorsqu'une nouvelle valeur `v` est annexée, nous devons la stocker d'une manière qui puisse être plus tard.
La valeur réelle d'un élément à tout moment est:

«» "
realVal = (stockéVal * globalMul + globalAdd) % MOD
«» "

Pour stocker `v` afin que la formule fonctionne, nous avons besoin:

«» "
stockéVal = ((v - globalAdd) * inv(globalMul)) % MOD
«» "

Ici `inv(globalMul)` est l'inverse modulaire de `globalMul` sous MOD (puisque MOD est le premier, nous pouvons utiliser Fermat='s Little Theorem).

Les quatre opérations deviennent "O(1)".

---

- Oui. 5. Mise en œuvre – Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

classe publique Fantaisie {
int final statique privé MOD = 1_000_000_007;
liste finale privée <Long> brute; // valeurs normalisées
global privé longMul = 1; // produit de tous les muls Tous
private long globalAdd = 0; // somme de tous addAll (déjà graduée)

publique () {
brut = nouvelle station <>();
}

annexe publique vide(int val) {
// Normalise val: supprimer le courant global Ajouter, puis supprimer l'effet de - Oui.
long corrigé = ((val - globalAdd) % MOD + MOD) % MOD; // assurer un résultat positif
corrigé = (ajusté * modInverse(globalMul)) % MOD;
brut.add(ajusté);
}

public vide addAll(int inc) {
GlobalAdd = (globalAdd + inc) % MOD;
}

vide public multAll(int m) {
globalMul = (globalMul * m) % MOD;
mondial Ajouter = (globalAjouter * m) % MOD;
}

Int public getIndex(int idx) {
si (idx >= rough.size()) retourne -1;
long res = (raw.get(idx) * globalMul + globalAdd) % MOD;
retour (int) rés;
}

- Oui. Fonctions de l'assistant
privé long modInverse(long a) {
Puissance de retour (a, MOD - 2); // Fermat
}

puissance privée longue (long base, long exp) {
résultat long = 1;
base %= MOD;
pendant la période (exp > 0) {
si ((exp & 1)] 1) résultat = (résultats * base) % MOD;
base = (base * base) % MOD;
Exp >>= 1;
}
le résultat du retour;
}
}
«» "

**Explication**

* `append` normalise la valeur de sorte que les multiplications/additions ultérieures sont "transparentes".
* `addAll` vient de mettre à jour l'ajout global.
* `multAll` balance à la fois le multiplicateur global et l'additif.
* `getIndex` reconstruit la valeur réelle.

Toutes les opérations sont "O(1)"; l'espace est "O(n)".

---

- Oui. 6. Mise en œuvre – Python

'`python
MOD = 1 000 000 007

Catégorie:
def _init_(self):
Self.raw = [] # valeurs normalisées
Self.mul = 1 # produit de toutes les mues Tous
auto.add = 0 # cumulé addAll (échelle)

def append(self, val: int) -> Aucun:
# Normaliser
val = (val - auto.add) % MOD
val = (val * pow(self.mul, MOD - 2, MOD)) % MOD
Annexe(val)

def addAll(self, inc: int) -> Aucun:
auto.add = (auto.add + inc) % MOD

def multAll(self, m: int) -> Aucun:
Self.mul = (Self.mul * m) % MOD
Self.add = (Self.add * m) % MOD

def getIndex(self, idx: int) -> Int:
si idx >= len(self.raw):
retour -1
retour (self.raw[idx] * self.mul + self.add) % MOD
«» "

Les Python's intégrés dans `pow(a, b, mod)` implémentent automatiquement une exponentiation rapide et inversement modulaire.

---

- Oui. 7. Mise en œuvre – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

catégorie Fancy {
static const int MOD = 1'000'000'007;
vectorielle <long long> brute; // valeurs normalisées
long long mul = 1; // produit de tous les muls Tous
longue addition = 0; // addition cumulée Tous (échelle)

long long modpow(long long a, long e) {
longue rés = 1;
a %= MOD;
pendant que e) {
si (e & 1) res = res * a % MOD;
a = a * a % MOD;
e >>= 1;
}
retour rés;
}

long long modinv(long long a) { retour modpow(a, MOD - 2); }

public:
Fancy() = par défaut;

vide appendice(int val) {
long v = ( ( long)val - ajouter ) % MOD + MOD ) % MOD;
v = v * modinv(mul) % MOD;
rough.push_back(v);
}

vide addAll(int inc) { add = (add + inc) % MOD; }

vide multAll(int m) {
mul = mul * m % MOD;
ajouter = ajouter * m % MOD;
}

Int getIndex(int idx) {
si (idx >= (int)raw.size()) retourne -1;
retour (int )( (raw[idx] * mul + add) % MOD );
}
};
«» "

Toutes les opérations restent `O(1)`; la seule étape coûteuse est `modinv(mul)` sur `append`, qui est `O(log MOD)` (~30 itérations) – temps toujours constant.

---

- Oui. 8. Performance et complexité

Opération de Java Python C++
C'est pas vrai.
"Append" "O(1)" (rapidement modulaire inverse par pow) ( propres pow rapide)
"AddAll" "O(1)" "O(1)" Autres
"MultAll" "O(1)" "O(1)" Autres
"getIndex" "O(1)" "O(1)" Autres

Utilisation de la mémoire: valeurs brutes `O(n)`, plus deux entiers 64 bits.

**Le temps d'exécution de 105 opérations est nettement inférieur à 1 ms en pratique.

---

- Oui. 8. Le bon, le mauvais, le mauvais

Aspect du bien
C'est pas vrai.
**L'élégance algorithmique**=Le tour du temps constant – montre la profondeur==La suringénierie est possible si vous oubliez l'inverse modulaire=== Mauvaise application de l'inverse → mauvais résultats==
**Pièges spécifiques à la langue**=Java `long` → attention avec le débordement=== Python `pow` poignées mod‐inverse automatiquement===C++ doit mod‐normaliser pour éviter les négatifs===
**Cas d'Edge**=1 pour les indices hors gamme=0=S'assurer que `(val - ajouter) % MOD` reste positif=
**Maintenance**= Interface O(1) propre== Tout état caché dans la classe== Si vous oubliez d'utiliser `add` sur `multAll`, chaque requête casse===

---

- Oui. 8. Article sur le blog des amis du SEO (Job-Ready)

> **Mots-clés**: LeetCode, Fancy Sequence, Question d'entrevue, Java, Python, C++, Mises à jour paresseuses, Inverse Modulaire, Algorithme O(1), Interview de codage, Structures de données, Algorithme, Interview de travail, Interview technique

---

Le problème de séquence fantastique sur LeetCode – 1622
**Pourquoi cela compte pour votre prochaine entrevue sur l'ingénierie logicielle* *

C'est vrai. 1. Présentation
LeetCodeS **Fancy Sequence (1622)** est un problème de type "Hard" qui peut être résolu avec un algorithme O(1) simple. Il teste votre maîtrise des concepts modulaires d'arithmétique et de mise à jour paresseuse, compétences que les intervieweurs désirent.

C'est vrai. 2. Le défi
Vous devez supporter 4 opérations sur un tableau dynamique :

- `annexe(val) "
- "AddAll(inc)"
- "MultAll(m)"
- "getIndex(idx)"

Tous les résultats sont modulo 1 000 000 007. La taille d'entrée peut atteindre 105, de sorte qu'une mise à jour `O(n)` naïve par `addAll`/`multAll` sera TLE.

C'est vrai. 3. Pourquoi c'est génial pour les entrevues
- **Astuce cachée**: Le temps constant par opération montre une compréhension profonde des mathématiques et des structures de données.
- **Language-agnostique**: Les solutions en Java, Python, C++ sont toutes attendues.
- **Évoluable**: 105 opérations → O(1) est la seule approche viable.

C'est vrai. 4. Idée fondamentale – Constante Mise à jour paresseuse
Maintenez deux variables :

- `globalMul` – produit cumulatif de tous les `multes Tous.
- `globalAdd` – somme cumulative de `addAll`, déjà multipliée par `globalMul`.

Conservez chaque valeur ci-jointe `v` sous une forme *normalisée*:

«» "
% MOD
«» "

Reconstruire sur requête :

«» "
valeur = (rawVal * globalMul + globalAdd) % MOD
«» "

Toutes les opérations deviennent "O(1)".

C'est vrai. 5. Mise en œuvre du code

###### 5.1 Java
* (voir bloc de code ci-dessus)*

5.2 Python
* (voir bloc de code ci-dessus)*

*##### 5.3 C++
* (voir bloc de code ci-dessus)*

C'est vrai. 6. Analyse de la complexité

Opération Temps Espace
C'est le cas.
Annexe par élément
"AddAll"
"Mult" Tous "O(1)" – "
« getIndex »
Total pour les opérations "n"

C'est vrai. 7. Les bons, les mauvais, les méchants

**Beau**
C'est le cas.
Solution constante → passe toutes les 105 opérations. Vous devez gérer correctement l'inverse modulaire ; beaucoup le manquent. Oublier la normalisation des valeurs ajoutées conduit à des bogues subtils qui n'apparaissent qu'après de nombreux appels `multAll`. Autres
Autres Séparation claire de l'état global → facile à raisonner. Il faut connaître le Petit Théorème de Fermat ; tout le monde ne le mémorise pas. Les erreurs hors-par-un (0-based indexing) peuvent faire monter des novices. Autres
Le code est propre et facile à porter entre Java/Python/C++. Certains candidats sur-optimisation (arbre de segment) au lieu d'utiliser le simple tour. Si `MOD` n'étaient pas prime, vous auriez besoin d'une stratégie inverse différente. Autres

C'est vrai. 8. A emporter pour votre prochaine entrevue

1. ** Expliquez l'astuce d'abord** – montrez-vous pourquoi une solution à temps constant est possible.
2. **Montrer vos connaissances arithmétiques modulaires** – parler des inverses, Fermat, etc.
3. **Ecrire un code propre et lisible** – même une solution courte `O(1)` doit être sans bug.
4. **Complexité du comportement** – les intervieweurs adorent vous voir articuler "O(1)` vs "O(n)".

La maîtrise de ce problème démontre que vous pouvez repérer et appliquer des raccourcis mathématiques élégants – exactement les recruteurs de l'ensemble des compétences recherchent chez un ingénieur logiciel junior/mi-niveau.

---

Pensée de clôture

> *Le problème de la séquence Fancy est un exemple éclatant de la façon dont une question d'entrevue apparemment difficile peut s'effondrer dans une solution soignée et constante avec la bonne idée. Que ce soit en Java, Python ou C++, la clé réside dans le traitement de toutes les mises à jour paresseusement et le stockage des données sous une forme normalisée. *

Bonne chance pour votre prochaine interview – résoudre ceci, maîtriser l'astuce, et apporter cette confiance dans la pièce!