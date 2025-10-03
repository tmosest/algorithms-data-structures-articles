---
title: LeetCode 1987. Nombre de produits uniques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code Leet 1987 – Nombre de bonnes séquences uniques
Les solutions C++ + SEO-Optimized Blog Post**

> Vous souhaitez obtenir votre prochain entretien d'ingénierie logicielle? Maîtrise **LeetCode 1987** vous donnera une victoire rapide sur la piste de programmation dynamique, et ce post vous guidera à travers la meilleure façon* de le résoudre, pourquoi il est élégant, et comment en parler dans un entretien d'emploi.

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Intuition et principale conclusion] (#intuition)
3. [Solution de programmation dynamique](#dp)
4. [Analyse de la complexité] (#complexité)
5. [Cas de cornière et pièges communs] (#cas de cornière)
6. [Code Snippets](#code)
* Java
* Python
* C++
7. [Le bon, le mauvais, et le mauvais] (#bon-mauvais)
8. [Interview-Ready Talking Points](#interview-parler)
9. [Résumé de l ' OEA] (#seo)

---

<a name="problem-statement"></a>
- Oui. 1. Exposé des problèmes

> **Nombre de bonnes séquences uniques* *
> On vous donne une chaîne binaire `binary`.
> Un **bonne sous-séquence** est une sous-séquence non vide qui ne commence **pas** avec un zéro avant, sauf si elle est exactement "0".
> Trouvez le nombre de **unique** bons sous-séquences de `binary`.
> Retourner la réponse modulo \(10^9 + 7\).

> **Exemples**
> * `binary = "001"` → réponse = 2 (`"0"`, `"1"`)
> * `binary = "11"` → réponse = 2 (`"1"`, `"11"`)
> * `binary = "101"` → réponse = 5 (`"0"`, `"1"`, `"10"`, `"11"`, `"101"`)

> **Constraints**
* \(1 \leq \text{len(binary)} \leq 10^5\)
> * `binary` ne contient que `'0'` et `'1'`.

---

<un nom></a>
- Oui. 2. Intuition et principales perspectives

La chaîne est binaire, de sorte qu'une bonne séquence ne peut se terminer que dans `'0'` ou `'1'`.
Pensez à construire des subséquences **un caractère à la fois**:

* ** "zeroEnd"** – nombre de sous-séquences uniques de bien qui se terminent par un "0"**.
* ** "OneEnd"** – nombre de sous-séquences uniques qui se terminent par un "1"**.

Lorsque nous lisons un nouveau caractère:

Effet sur `zeroEnd` Autres
Il y a un problème.
Nous pouvons ajouter ce `'0'` à chaque sous-séquence qui ** s'est terminée avec un `'1'`** → `zeroEnd += oneEnd`. Nous ne pouvons pas démarrer une nouvelle séquence non vide avec un `'0'` à moins qu'il n'y ait le caractère unique `"0"`. Autres
Aucun changement. Nous pouvons ajouter ce `'1'` à n'importe quelle sous-séquence existante (`zeroEnd + oneEnd`) **ou** lancer une nouvelle séquence de caractères uniques `"1"` → `oneEnd += zéro Fin + oneFin + 1`. Autres

Enfin, la réponse est `zéro Fin + oneFin '.
Mais si la chaîne contenait au moins une `'0'`, le seul subséquence `"0"` est **non** compté ci-dessus, donc nous ajoutons un `1` supplémentaire dans ce cas.

Le DP entier fonctionne dans **O(n)** temps et **O(1)** mémoire.

---

<un nom="dp"></a>
- Oui. 3. Solution de programmation dynamique

Texte
Initialiser :
zeroEnd = 0 // subséquences se terminant par '0'
unEnd = 0 // subséquences se terminant par '1 '
hasZero = false // avons-nous vu un '0' du tout?

Pour chaque caractère c en binaire:
si c == «0»:
zeroEnd = (zeroEnd + oneEnd) % MOD
a Zéro = vrai
Sinon: // c == «1»
UnEnd = (zéroEnd + unEnd + 1) % MOD

réponse = (zeroEnd + oneEnd + (hasZero ? 1 : 0)) % MOD
«» "

`MOD = 1_000_000_007`.

---

<un nom="complexité"></a>
- Oui. 4. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Une chaîne de balayage une fois **O(n)**
Modulo o(1) chacun

Pour `n = 10^5`, ceci est bien en dessous des limites.

---

<un nom="cas de corner"></a>
- Oui. 5. Cas de coin et pièges communs

Pourquoi ça compte ?
- Oui.
La corde a **non** Nous ne devons pas ajouter le "0" supplémentaire Track `hasZero` ou compter les zéros en premier
Autres Tous les zéros («0000») Un seul bon résultat unique: `"0"`="zeroEnd` devient 0, `hasZero` true → response = 1
* Grande entrée ( < 10^5 > ) * Risque de débordement * Utiliser 64 bits ( < long > / < long > ) pendant l'addition avant le mod
Modulo mal-placement

---

<un code de nom></a>
- Oui. 6. Extraits de code

### Java

"Java
solution de classe publique {
int final statique privé MOD = 1_000_000_007;

numéro int publicOfUniqueGoodSous-séquences(Binary String) {
longue zéro Fin = 0, oneFin = 0;
booléen hasZero = faux;

pour (int i = 0; i < binaire.longueur(); i++) {
char c = binaire. l'alinéa i);
si (c) '0') {
ZeroEnd = (zeroEnd + oneEnd) % MOD;
a Zéro = vrai;
} autres { // '1 '
UnEnd = (zéroEnd + unEnd + 1) % MOD;
}
}
retour (int)((zeroEnd + oneEnd + (hasZero ? 1 : 0)) % MOD);
}
}
«» "

Python

'`python
Solution de classe:
MOD = 10**9 + 7

def numberOfUniqueGoodSubséquences(self, binaire: str) -> Int:
0_end = un_end = 0
has_zero = Faux

pour ch en binaire:
si ch == '0':
zero_end = (zero_end + one_end) % self. MOD
has_zero = Vrai
Sinon : # '1'
un_end = (zero_end + un_end + 1) % soi-même. MOD

retour (zero_end + one_end + (1 si has_zero other 0)) % self. MOD
«» "

C++

'`cpp
solution de classe {
public:
MOD statique const = 1e9 + 7;
nombre intOfUniqueGoodSubséquences(chaîne binaire) {
longue longue zéro Fin = 0, oneFin = 0;
bool hasZero = faux;

pour (charc : binaire) {
si (c) '0') {
ZeroEnd = (zeroEnd + oneEnd) % MOD;
a Zéro = vrai;
} autre { // c == «1 '
UnEnd = (zéroEnd + unEnd + 1) % MOD;
}
}
retour static_cast<int>((zeroEnd + oneEnd + (hasZero ? 1 : 0)) % MOD);
}
};
«» "

---

<a name="good-bad-ugly"></a>
- Oui. 7. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**L'élégance algorithmique**=O(n) time, O(1) memory – a single pass DP==Le dénombrement naïf est O(2^n) – impossible pour n=105==Le fait d'oublier l'extra pour les cordes contenant des zéros conduit à un bug subtil off‐by‐one==
**Clarté de la mise en œuvre**= Deux compteurs + un drapeau – facile à lire== Les approches complexes basées sur la récursion ou le jeu de hachage peuvent masquer la logique==Le mélange de types de données (int vs long) peut causer un débordement – un feuillet d'entrevue fréquent==
**Scalabilité**= Fonctionne jusqu'à 105 caractères avec un arithmétique 64 bits.= Une solution de rétro-tracking frappera les limites de la pile==La valeur mod codée dur peut être placée par erreur avant l'ajout, donnant de mauvais résultats==
**Entrevue parlante-point**=Je traite le problème comme deux états DP.= J'ai utilisé un ensemble de force brute. Autres

---

<un nom="interview-parler"></a>
- Oui. 8. Points d'entrevue prêts à parler

1. **Exposer la définition d'un bon subséquence** – mettre en évidence la règle de 0.
2. **Déclarer les États du PDD** – « zeroEnd » et « oneEnd » – pourquoi ils sont suffisants.
3. **Venez à travers la transition** – montrez comment un caractère appending met à jour les compteurs.
4. **Afficher l'agrégation finale** – pourquoi nous ajoutons `1` si un zéro existait.
5. **Complexité** – rassurez l'intervieweur sur le temps O(n) et la mémoire O(1).
6. **Manipulation d'un boîtier** – mention d'une chaîne tout-zéro, d'un tout-one et d'un garde modulo.
7. **Extension facultative** – comment vous l'adapteriez si nous devions aussi compter les sous-séquences *non uniques*.

---

<un nom=seo></a>
- Oui. 9. Résumé du SEO

- **Titre Tags**: LeetCode 1987 – Nombre de bonnes séquences uniques (Java, Python, C++)
- **Description détaillée**: Solve LeetCode 1987 avec O(n) DP. Lisez nos solutions Java, Python et C++, des conseils d'entretien et une plongée profonde dans l'algorithme. (en milliers de dollars)
- **En-têtes**: `# LeetCode 1987`, `### Solution Java`, `## Solution Python`, `## C++ Solution "
- **Mots-clés**: *LeetCode 1987*, *Number of Unique Good Subséquences*, *dynamique programmation*, *solution de Java*, *solution de Python*, *solution de C++*, *interview d'emploi*, *ingénieur logiciel*, *analyse d'algorithme*, *subséquences de chaîne binaire*.
- ** Liens internes**: Lien vers d'autres blogs d'algorithmes (Dynamic Programming with Two States) et vers la page de problème LeetCode.

Avec cette structure, les moteurs de recherche indexeront l'article sous les termes les plus pertinents, attirant les développeurs se préparant à coder des entretiens ou s'attaquant aux défis LeetCode.

---

** Bon codage !**
N'hésitez pas à fourcher ce dépôt ou à adapter les extraits à votre langue préférée. Bonne chance pour la prochaine entrevue – votre solution DP est un point de discussion solide qui montre à la fois la pensée algorithmique et le codage propre.