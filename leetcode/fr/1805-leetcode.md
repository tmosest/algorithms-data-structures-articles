---
titre: LeetCode 1805. Nombre d'entiers différents dans une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1805 – Nombre d'entiers différents dans une chaîne

> **Objectif** – Compte tenu d'une chaîne mixte de lettres et de chiffres minuscules, remplacez chaque non-numérique par un espace, divisez la chaîne en jetons entiers, décalez les zéros et comptez le nombre d'entiers *unique* existant.
> **Typical interview scenario** – Une question qui teste l'utilisation de l'expression régulière, la sémantique et la manipulation des cas de bord.
> **Pourquoi ça compte pour les recruteurs** – Il vous force à penser aux compromis entre le temps et l'espace**, à la manipulation de gros nombres entiers et au style de code propre – tous les traits que les recruteurs recherchent dans un ingénieur de backend / full-stack.

Vous trouverez ci-dessous une solution entièrement commentée et prête à la production en **Java, Python et C++** (C++17).
Après le code, je vous donnerai un billet de blog qui parle des aspects *good*, *bad* et *ugly* de ce problème et pourquoi le maîtriser peut vous aider à décrocher votre prochain emploi.

---

Résumé du problème

«» "
Entrée: mot – une chaîne (1 ≤ ≤ ≤ 1 000 mots) composée de [0‐9] et [a‐z]
Sortie : Nombre d'entiers distincts après suppression de non-chiffres
et de jeter les zéros de tête.
«» "

*exemple*

«» "
mot = "a123bc34d8ef34" → jetons: 123, 34, 8, 34
Nombre entiers distincts: {123, 34, 8} → réponse = 3
«» "

*Cas d'urgence*

* =000 → entier 0
* les mêmes
* Très longs entiers qui ne s'intègrent pas dans les types 64 bits

---

Approche de haut niveau

1. **Scan la chaîne une fois** – garder un pointeur `i`.
2. Lorsque vous voyez un chiffre, accumulez tous les chiffres consécutifs dans un `StringBuilder` (ou `string`).
3. La bande en tête de zéros ("replacerFirst("^0+", "")".
4. Si la chaîne résultante est vide → l'entier est `0`.
5. Conservez la forme canonique dans un `HashSet` / `unordered_set` / `set`.
6. Retourne la taille de l'ensemble.

*Pourquoi cela fonctionne*:
* Chaque numéro est traité en O(longueur).
* Les zéros de décapage assurent la forme canonique; p.ex.
* L'utilisation d'un ensemble garantit l'unicité en O(1) amorti (basé sur le hash) ou en O(log n) (basé sur l'arbre).

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Numérisation du mot "" **O(n)** (n ="word")
Ajouter à l'ensemble **O(1)** amorti (Java/C++ non ordonné_set)
Dans l'ensemble **O(n)**

`n` ≤ 1000, de sorte que l'algorithme est facilement dans les limites.

---

Les solutions de code

> **Astuce** – Utilisez un `BigInteger` (Java), `int` (Python=s arbitraire-précision `int`), ou `_int128`/`std::string` en C++ lorsque le nombre peut être > 64-bit.
> Le code ci-dessous s'applique uniquement à la bibliothèque standard (pas de libs tiers).

- Oui. 1. Java (Java 17)

"Java
importation java.math. BigIntégre;
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe publique {
int public numDifferentIntégres (mot en bas) {
Set<String> vu = nouveau HashSet<>(); // stocker la représentation de la chaîne canonique
i = 0;
int n = mot.longueur();

pendant que (i < n) {
// sauter les non-données
si (!Caracter.isDigit(word.charAt(i))) {
i++;
poursuivre;
}

// accumuler des chiffres
début int = i;
(i < n& Character.isDigit(word.charAt(i))) i++;
Chaîne num = word.substring(start, i);

// zéros de tête de bande
Chaîne canonique = num.replaceFirst("^0+", "");
si (canonical.isEmpty()) canonique = "0"; // tous les zéros

voir.add (canonique);
}
retour vu.size();
}
}
«» "

**Pourquoi un ensemble `String`? * *
JavaS `BigInteger` est grand mais crée un objet lourd par nombre.
Stocker la chaîne *canonique* maintient la mémoire basse et évite l'analyse des frais généraux – suffisant pour `n ≤ 1000`.

---

- Oui. 2. Python 3 (Python 3.10+)

'`python
Solution de classe:
def numDifferentIntegers(self, word: str) -> Int:
vu = set()
i = 0
n = len(mot)

alors que i < n:
si ce n'est pas mot[i].isdigit():
i += 1
poursuivre

début = i
alors que i < n et word[i].isdigit():
i += 1

num = word[start:i].lstrip('0')
si num] «»:
num = '0 '
Voir.add(num)

retour len(see)
«» "

**Note pyronique** – `int` est une précision arbitraire, de sorte que vous pouvez convertir `num` en `int` si vous préférez l'unicité numérique, mais la forme canonique à cordes est plus simple.

---

C++17 (C++ 17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int numDifferentIntégres(mot chaîne) {
unordered_set<string> vu;
i = 0, n = mot.size();

pendant que (i < n) {
si (!isdigit(word[i])) { ++i; continuer; }

début int = i;
pendant que (i < n && isdigit(word[i])) ++i;
chaîne num = word.substr(start, i -start);

// zéros de tête de bande
size_t pos = num.find_first_not_of('0');
chaîne canonique = (pos == chaîne::npos) ? "0" : num.substr(pos);

voir.insérer(canonique);
}
retour vu.size();
}
};
«» "

**Pourquoi `unordered_set<string>`? * *
La même raison d'être que Java : la chaîne canonique sauve la mémoire et écarte le besoin de `boost::multiprecision` ou `_int128`.

---

Article du blog : Le bon, le mauvais, et le mauvais de LeetCode 1805

> *Mots-clés de référencement: LeetCode 1805, Nombre de différents entiers dans une chaîne, Solution Java, Solution Python, Solution C++, Interview de codage, Interview d'emploi, Analyse d'algorithme, Analyse de chaîne. *

---

Introduction

Lorsque les recruteurs scrutent votre CV, ils recherchent souvent des problèmes de « pattern-reconnaissance »** et de « set-theory** », deux piliers essentiels du code propre et prêt à la production.
Problème de LeetCode **1805 – Nombre de différents entiers dans une chaîne** est un tel bijou.
Cela vous oblige à :

* Convertir une chaîne en jetons significatifs
* Traiter les cas bord qui pourraient sembler triviaux à première vue
* Décider de la meilleure structure de données pour l'unicité
* Discuter des compromis de rendement

La maîtrise de 1805 montre que vous pouvez gérer l'analyse des données du monde réel avec confiance – une compétence qui résonne en backend, en data-engineering et en full-stack.

---

- Oui. Les bonnes

Pourquoi c'est une force
- C'est pas vrai.
**Scan linéaire**** Seulement **O(n)** temps; les recruteurs aiment les solutions linéaires pour les petites tailles d'entrée. Autres
**Canonical String**= Évite les débordements numériques; le stockage `"0"` vs `"0000"` est trivial. Autres
**Set Semantics**= Garantie unicité en temps constant; met en évidence la connaissance des tables de hachage. Autres
**Portabilité de la langue-Cross**Les solutions en Java, Python et C++ sont courtes, propres et faciles à expliquer sur un tableau blanc. Autres
Autres **Clear Edge‐Case Manualing** Autres

Ces qualités de « good » font de 1805 une pièce d'interview ** autonome** : un exemple parfait de « talk » à propos de votre expérience » lors de votre prochain cycle de codage.

---

C'est vrai. Les mauvais

Problème Impact Atténuation
- C'est quoi ?
**Potential Integer Overflow**.Les jetons très longs (p. ex. 100 chiffres) peuvent dépasser les limites de 64 bits. Utilisez la canonicisation des chaînes de caractères ou les bibliothèques grand entier (Java `BigInteger`, Python=s `int`, C++ `boost::multiprecision`). Autres
**Mémoire Overhead de BigInteger**= Création d'un "BigInteger" pour chaque numéro peut être lourd en Java. Conservez plutôt la chaîne *canonique*; analysez seulement si une comparaison numérique est nécessaire. Autres
**Performance de Regex**= Certaines personnes le résolvent avec un regex comme `re.findall(r'\d+', word)` puis `int(s)`.= Alors que rapide pour les petites entrées, regex peut masquer la logique et rend plus difficile d'expliquer les compromis algorithmiques. Autres

Les recruteurs apprécient les candidats qui peuvent repérer ces pièges et expliquer pourquoi une approche simple et claire est souvent préférable.

---

C'est pas vrai. L'Ugly

Ce qu'il ressemble Pourquoi il est Ugly
- Oui.
**Régex sur-compliqué** suivie d'une boucle qui délimite les zéros. Le régex cache le *O(n)* scan et rend difficile de voir que l'algorithme est linéaire. Autres
**Wrong Canonical Form**= Ajouter `"0"` directement à l'ensemble au lieu de décaper les zéros de tête → duplicata (`"01"`, `"1"`). Conduis à des réponses erronées; montre un manque d'attention au détail. Autres
**Les conversions de BigIntégrations inutiles** Ajoute des cycles CPU inutiles et une pression mémoire. Autres

Ces modèles sont des pièges communs pour les candidats qui se précipitent pour utiliser des fonctions intégrées sans comprendre la sémantique sous-jacente.

---

C'est vrai. Pourquoi la résolution de 1805 vous aide à chasser votre emploi

1. **Manipulation en réseau est partout** – De log parsers au routage URL, l'analyse des données mixtes est une tâche quotidienne.
2. **L'utilisation de l'ensemble démontre la sensibilisation à la structure des données** – Les recruteurs aiment voir que vous savez quand une table de hachage par rapport à l'arbre est appropriée.
3. **La pensée d'un cas Montres Maturity** – Manipulation de l'information par rapport à l'ensemble des données.
4. **Cross‐Language Confiance** – Être capable de produire du code idiomatique propre en Java, Python et C++ montre que vous pouvez travailler dans n'importe quelle pile.
5. **Performance – Premier mental** – Vous impressionnerez les intervieweurs en expliquant que la solution est O(n) et O(k) et pourquoi cela compte pour les systèmes de production.

---

- Oui. Dernier départ

LeetCode 1805 est *pas* un teaser du cerveau; c'est un exercice **code-craft** qui révèle votre style de codage pragmatique.
En maîtrisant le modèle **canonical-string + set** vous'll:

* Éviter les pièges de débordement
* Maintenir l'utilisation de la mémoire faible
* Fournir un code propre et testable
* Soyez prêt à discuter *pourquoi* vous avez choisi une structure de données par rapport à une autre dans une entrevue

Ajoutez les extraits Java, Python et C++ ci-dessus à votre portfolio GitHub, et laissez les recruteurs voir les parties *bon*, *mauvais* et *douce* de ce problème résolu avec élégance. Bonne chance sur votre prochain entretien de codage – vous êtes un pas plus près d'obtenir ce travail de rêve! C'est ce qu'il a dit