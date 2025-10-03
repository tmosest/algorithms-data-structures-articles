---
titre: LeetCode 2229. Vérifiez si un tableau est consécutif -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Mise en œuvre des trois langues

Ci-dessous vous trouverez trois solutions *propre, prêt à la production* qui résolvent **LeetCode 2229 – Cochez si un tableau est consécutif** dans **O(n)** temps et **O(n)** espace auxiliaire.
Tous les trois utilisent la même idée :

1. Scannez le tableau une fois pour trouver les valeurs minimales et maximales et pour construire un `Set` (ou `HashSet` / `unordered_set`) de tous les éléments.
2. Si la longueur du tableau est égale à `max – min + 1` * et que la taille définie est égale à la longueur du tableau, le tableau contient *chaque* entier dans cette plage → il est consécutif.

> **Pourquoi il s'agit de l'approche "good"* *
> • Temps linéaire – vous ne touchez chaque élément qu'une fois.
> • Vérifications d'adhésion à temps constant via le hachage.
> • Pas de tri, pas de passes supplémentaires sur les données.

Les trois extraits sont commentés et prêts à tomber dans votre fichier solution.

---

### Java – O(n) Temps, O(n) Espace

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe publique {
***
* Vérifier si le tableau d'entrée est consécutif.
*
* @param nombres le tableau d'entrée (1 <= nombres.longueur <= 1e5, 0 <= nombres[i] <= 1e5)
* @retour vrai si chaque nombre dans [min(nums), min(nums)+nums.length-1] est présent
*/
le booléen public estconsécutif(int[] nums) {
// Copie défensive : si le tableau est vide, il est trivialement consécutif
si (nombres) null (longueur) num) 0) retour vrai;

Définir<entier> vu = nouveau HashSet<>(longueur du nombre);
int min = entier. MAX_VALEUR;
int max = entier.MIN_VALUE;

pour (int x : nombres) {
Voir.add(x);
si (x < min) min = x;
si (x > max) max = x;
}

Int attendu Longueur = max - min + 1;
retour nums.longueur == attenduLongueur && vu.size() == nums.longueur;
}
}
«» "

---

### Python – O(n) Temps, O(n) Espace

'`python
Solution de classe:
def isConsecutive(self, nombres: list[int]) -> C'est vrai.
"""
Retourner True iff `nums` contient chaque entier de min(nums)
à min(nums)+len(nums)-1 (inclus).
"""
si non nombres: # liste vide est considérée comme consécutive
retour Vrai

min_val = min(nums)
max_val = max(nums)
longueur attendue = max_val - min_val + 1

# Un ensemble garantit une recherche moyenne O(1) ; sa taille nous indique s'il existe des duplicatas
voir = ensemble(s)
return len(nums) == expected_longueur et len(seen) == len(nums)
«» "

---

### C++ – O(n) Temps, O(n) Espace

'`cpp
#incluez <vecteur>
#inclut <unordered_set>
#incluez <algorithme>
#incluez <limites>

solution de classe {
public:
Bool isConsecutive(std::vector<int>& nums) {
si (nums.vide()) retourne true; // cas bord: tableau vide

Int minval = INT_MAX, max_val = INT_MIN;
std::unordered_set<int> vu;

pour (int x : nombres) {
voir.insérer(x);
si (x < min_val) min_val = x;
si (x > max_val) max_val = x;
}

int expectated_len = max_val - min_val + 1;
return nums.size() == expected_len && see.size() == nums.size();
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de vérifier si un tableau est consécutif

> **Description détaillée**
> Maîtrisez le LeetCode, vérifiez si un problème d'array est consécutif. Apprenez la solution *bonne* linéaire-temps, pourquoi l'approche *mauvaise* de tri échoue, et comment éviter les pièges *meilleures*. Préparez-vous aux interviews en Java, Python ou C++.

Introduction

*Vérifier si un tableau est consécutif** (LeetCode #2229) semble trompeurment simple, mais c'est un agrafe d'interview classique qui teste votre capacité à raisonner sur les plages, les duplications et l'efficacité algorithmique. Beaucoup de candidats parviennent à un tri ou à un balayage à deux points, mais ces approches peuvent être plus lentes et plus difficiles à justifier lors d'une entrevue chronométrée.

Dans cet article, nous disséquons le problème en trois parties:

Autres Phase Ce que vous découvrirez Pourquoi ça compte
Il y a un problème.
**Le bon**=Le temps linéaire, une solution à base d'ensemble= Rapide, clair et facile à expliquer==
**Le mauvais**
**Les cas de bord et la manipulation des duplicatas

---

- Oui. Le problème en bref

> **Grâce à un nombre entier.
> **Retour** `true` si `nums` contient **chaque** entier dans l'intervalle `[min(nums), min(nums)+len(nums)-1]`.
> **Autres** retour `faux`.

**Contrôles* *
- `1 <= longueur nums. <= 10^5`
- `0 <= nombres[i] <= 10^5`

---

## La bonne – Solution linéaire

- Oui. Pourquoi c'est la meilleure approche

1. **O(n) time** – un passage pour trouver `min`, `max`, et recueillir des éléments dans un ensemble.
2. **O(n) espace** – l'ensemble contient chaque valeur distincte.
3. **Pas de tri** – évite le facteur supplémentaire `n log n`.
4. **Poignées dupliquées naturellement** – la taille de jeu égale la longueur du tableau si il n'y a pas de duplicata.

Étape par étape

1. **Trouver les valeurs minimales (`min`) et maximales (`max`). **
2. **Construisez un ensemble de hachage de tous les éléments. **
3. ** Calculer la longueur prévue** : `attendu = max - min + 1`.
4. **Retour** "nums.longueur" == attendu && set.size() == nums.longueur".

Code Pseudo

«» "
fonction isConsecutive(nums):
si nombres vides : retourner true
minVal = +
maxVal = -
jeu = jeu de hachage vide

pour chaque x en nombres:
Ensemble.add(x)
minVal = min(minVal, x)
maxVal = max(maxVal, x)

Len = maxVal - minVal + 1
retour len(nums) == prévuLen et len(set) == len(nums)
«» "

- Oui. Java / Python / C++ Extraits

*(Voir la section 1 ci-dessus pour le code entièrement commenté dans chaque langue.) *

### Conseil d'entrevue

Expliquez que l'ensemble ne garantit aucun duplicata. Si la taille de l'ensemble diffère de la longueur du tableau, vous savez qu'il y a un duplicata et que le tableau ne peut pas être consécutif.

---

- Oui. Le mauvais – tri ou double numérisation

Piège commun

Beaucoup de candidats trieront d'abord le tableau :

"Java
Tableaux.sort(nums);
int min = nombres[0];
pour (int i = 1; i < nombres de longueur; i++) {
si (nums[i] != min + i) retourner false; // détecter l'écart ou le duplicata
}
«» "

- Oui. Pourquoi il est suboptimal

- **O(n log n)** temps dû au tri, ce qui est inutile étant donné que la solution linéaire existe.
- Tri détruit l'ordre original, qui pourrait être une exigence dans d'autres contextes.
- Nécessite un passe supplémentaire pour valider les lacunes et les duplicatas, en ajoutant des facteurs cachés constants.

Quand cela pourrait être acceptable

Si vous êtes certain que l'intervieweur ne se soucie que de *correctitude* et non d'optimalité, ou si `n` est extrêmement petit, une approche de tri peut être bonne. Mais pour un tableau de 10^5, les frais généraux sont mesurables.

---

## L'Ugly – Cas de bord et manipulation du duplicata

Nombres dupliqués

L'instruction de problème permet des duplications (par exemple, `[1,1,2,3]`), mais un tableau consécutif valide doit contenir *chaque* entier exactement une fois.
**Code de bord**:
'`python
si len(set(nums)) == len(nums) et max(nums) - min(nums) + 1 == len(nums):
retour Vrai
«» "
Ce code fonctionne, mais si vous oubliez la vérification de la taille définie, vous retournerez incorrectement `True` pour `[1,2,2,3]`.

Tableau vide

Les contraintes garantissent au moins un élément, mais une mise en œuvre défensive devrait traiter `[]`.
** Bonne pratique**: `si nums.vide() retourne true;` (ou `faux` si vous préférez).

Nombres importants et dépassements

Avec des valeurs `int` allant jusqu'à `10^5`, l'expression `max - min + 1` ne débordera pas en entiers 32 bits.
Cependant, si les contraintes étaient plus grandes, utilisez un entier 64 bits (`long` en Java, `long` en C++).

Essais de performance

Si vous n'êtes pas sûr de la linéarité, lancez un micro-benchmark :

"Java
int[] big = nouveau int[100_000];
pour (int i = 0; i < 100_000; i++) big[i] = i;
nouvelle solution().isConsecutive(big); // devrait être vrai
«» "

---

- Oui. Prise- Liste de contrôle pour l ' éloignement

Objet
- Oui.
Utiliser un jeu de hachage pour garantir la recherche O(1) et la détection du double. Autres
Calculer `min` et `max` dans la même passe que l'insertion. Autres
Valider "nums.length" (max - min + 1)" et "set.size()"). Autres
Éviter de trier à moins que vous ayez une bonne raison. Autres
N'oubliez pas de manipuler les duplicatas. Autres
Ne présumez pas que le tableau n'est pas vide à moins que les contraintes le garantissent. Autres

---

## Pensées de clôture

Le problème « Vérifier si un tableau est consécutif » est un micro-traitement de la logique *range* et de l'unicité *set-based. En maîtrisant la solution linéaire vous non seulement marquer des points sur LeetCode, mais aussi démontrer aux intervieweurs que vous:

- **Connaître la complexité** – peut choisir O(n) sur O(n log n) le cas échéant.
- **Comprendre les structures de données** – jeux de hachage pour les vérifications d'adhésion.
- **Ecrire un code propre et vérifiable** – chaque partie de l'algorithme est isolée et facile à raisonner.

Bonne chance pour écraser vos entretiens de codage, et continuer à pratiquer – chaque cas de bord que vous manipulez maintenant paiera des dividendes plus tard!

---

**Mots clés:** LeetCode 2229, Vérifier si un tableau est consécutif, question d'entrevue, algorithme, Java, Python, C++, O(n), set de hachage, tri des pièges, conseils d'entrevue de codage, entretien d'emploi, ingénierie logicielle, structures de données, complexité temporelle.