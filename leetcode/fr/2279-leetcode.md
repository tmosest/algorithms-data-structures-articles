---
titre: LeetCode 2279. Sacs maximum avec pleine capacité de roches -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2279. ** Sacs maximaux avec pleine capacité de roches** – Un guide complet
C++*

> **SEO Mots-clés:** LeetCode 2279, Sacs Maximaux avec pleine capacité de roches, Algorithme Greedy, solution Java, solution Python, solution C++, préparation d'entrevue, interview d'algorithme, entretien d'emploi

---

Table des matières

1. [Énoncé du problème] (#Énoncé du problème)
2. [Intuition & Idée de la race] (#Intuition---Idée de la race)
3. [Régimes et pièges] (#cases--règles)
4. [Analyse de la complexité] (#analyse de la complexité)
5. [Mise en œuvre](#Mise en œuvre)
- Java
- Python
- C++
6. [Bon, mauvais et affreux]
7. [Pourquoi ce problème est-il à l'origine de votre demande d'entrevue] (#pourquoi ce problème-rocks-votre demande d'entrevue)
8. [Conclusion] (#conclusion)

---

## Déclaration du problème

Vous avez **n** sacs indexés de **0** à **n‐1**.
- `capacité[i]` – le nombre maximal de roches que le sac *i*-th peut contenir.
- `rocks[i]` - le nombre actuel de roches dans le sac *i*-th (`0 ≤rocks[i] ≤contenance[i]`).

Vous avez également un entier `en plus' – le nombre total de roches supplémentaires que vous pouvez distribuer entre les sacs (vous pouvez laisser certains inutilisés).

**Retourner le nombre maximum de sacs qui peuvent atteindre la pleine capacité après avoir distribué les roches supplémentaires de façon optimale. **

> **Constraints**
Capacité. longueur == rochers.longueur "
> * `1 ≤ n ≤ 5·104`
> * `1 ≤ capacité[i] ≤ 109 "
> * `0 ≤ roches[i] ≤ capacité[i] "
> * `1 ≤ autresRocks ≤ 109 "

---

## Intuition — Idée d'avidité

La quantité de roches nécessaires pour remplir le sac *i* est "besoin[i] = capacité[i] – roches[i]".
Si nous voulons maximiser le nombre de sacs *full*, nous devrions d'abord remplir les sacs qui ont besoin des roches **fewest**.
Pourquoi ? Parce que chaque sac que nous remplissons consomme une certaine quantité de "rocks supplémentaires".
Choisir les plus petites valeurs `need[i]` nous donne d'abord le plus grand nombre de sacs qui peuvent être complétés.

Ainsi:

1. Calculer les besoins pour tous les sacs.
2. Triez le tableau des besoins.
3. Traverser la liste triée, en soustrayant chaque «besoins» des «Rocks supplémentaires» alors qu'elle reste non négative.
4. Le nombre de fois que nous pourrions soustraire avant de courir est la réponse.

C'est une stratégie classique **greedy** : des choix locaux optimaux (remplir le sac le plus facile d'abord) mènent à une solution mondiale optimale.

---

## Cas de bord et pièges

Pourquoi ça compte ? Comment gérer ?
- C'est quoi ?
**Grand nombre** – capacités et roches jusqu'à `109`. Utiliser 64 bits (`long`/`long long`) pour des sommes intermédiaires, mais la réponse finale correspond à `int`. Autres
Autres ** Besoins de Zero** – certains sacs peuvent déjà être pleins. Ils devraient être comptés immédiatement sans consommer de roches. Rechercher les besoins. 0` ou les traiter comme des éléments à coût nul qui ne réduisent jamais les "Rocks supplémentaires". Autres
Autres * Distribution inutile** – vous n'avez peut-être pas besoin d'utiliser toutes les roches. L'algorithme s'arrête lorsque `supplémentalRocks < nextNeed`. L'état de la boucle s'en occupe naturellement. Autres
Autres Le tri doit être efficace. Le tri O(n log n) est acceptable. Utiliser un tri de bibliothèque efficace (TimSort / introsort). Autres
**Différences linguistiques** – p.ex., l'int par défaut de Python est débordé, l'int de Java est 32 bits. Assurez-vous d'utiliser le bon type. Autres

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Calculer le tableau des besoins **O(n)**
Classer **O(n log n)** (Java & C++ trie des copies; Python utilise Timsort en place)
Balayage de la graisse

**Total** :
- **Heure**: "O(n log n) "
- **Espace**: `O(n)` (peut être réduit à `O(1)` si vous triez une copie du tableau original).

---

Mise en œuvre

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
Chacun suit le même algorithme gourmand décrit ci-dessus.

- Oui. 1. Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
Int maximum Sachets(int[] capacité, roches int[], roches int supplémentaires) {
int n = capacité. longueur;
besoin long[] = nouveau besoin long[n];
int full = 0; // sacs déjà pleins

pour (int i = 0; i < n; i++) {
si (rocks[i] == capacité[i]) {
Full++; // pas de roches nécessaires
} autre {
besoin[i] = (long)capacité[i] - les roches;
}
}

// Trier seulement les éléments nécessaires; les fentes inutilisées sont zéro
Tableau 3.

longues roches À gauche = roues supplémentaires;
Int ajouté = 0;

pour (int i = 0; i < n; i++) {
longue req = besoin[i];
Si (requ) 0) continuer; // déjà plein
si (rocksLeft >= req) {
roches À gauche -= req;
ajouté++;
} autre {
pause;
}
}
retour complet + ajouté;
}
}
«» "

> ** Points clefs**
> * Utilisez `long` pour le tableau `need` pour éviter le débordement.
> * Sautez les besoins zéro après le tri; ils correspondent à des sacs déjà pleins.

- Oui. 2. Python

'`python
Solution de classe:
def maximum Sacs(auto, capacité: List[int], rochers: List[int],
Rocks supplémentaires: int) -> Int:
# Calculer combien de pierres de plus chaque sac a besoin
besoin = [c - r pour c, r en zip(capacité, roches) si c - r > 0]
besoin.sort()

nombre = 0
pour les besoins:
si additionalRocks >= req:
supplémentaires Rocks -= req
nombre += 1
Sinon:
pause
Tous les sacs sont déjà pleins
nombre += len(capacité) - len(besoins) - nombre
Nombre de retours
«» "

> **Pourquoi filtrer `> 0'**
> Garde la liste petite et saute déjà des sacs pleins dans la boucle.

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximum Sacs(vecteur<int>& capacité, vecteur<int>& roches, int additionalRocks) {
int n = capacité.size();
vectorielle <long> besoin;
Int déjàFull = 0;

pour (int i = 0; i < n; ++i) {
si (rocks[i] == capacité[i])
++déjàFull; // aucune roche nécessaire
Autre
need.push_back(static_cast<long long>(capacité[i]) - roches[i]);
}

tri(need.begin(), need.end());

longues longues roches À gauche = roues supplémentaires;
Int ajouté = 0;
pour (long terme : besoin) {
si (rocksLeft >= req) {
roches À gauche -= req;
+ additionné;
} autre pause;
}
retour déjà Total + ajouté;
}
};
«» "

> **Notes**
> * Nous ne stockons que les *positifs* nécessaires pour réduire la mémoire.
> * "long long" protège contre le débordement.

---

Bien, mal et moche

Aspect du bien
- C'est quoi ?
**Correctivité de la graisse**= Intuitivement clair: remplir les sacs les plus faciles d'abord. Nécessite la preuve que l'optimalité locale donne un optimum global. Certains pourraient penser par erreur que nous pouvons remplir n'importe quel sac; ignorer l'ordre peut conduire à des comptes sous-optimaux. Autres
**Complexité du temps**= `O(n log n)` – rapide pour n ≤ 5·104.= Le tri peut être coûteux si vous avez également besoin de structures de données supplémentaires. L'utilisation d'une file d'attente prioritaire avec des suppressions répétées ajoute des frais généraux inutiles. Autres
Autres **L'utilisation de l'espace**. Stockage de tableaux supplémentaires pour les besoins augmente l'empreinte mémoire. La suringénierie (p. ex., la construction d'un arbre segmentaire) est une surcompétence. Autres
**Risque de dépassement** Oublier d'utiliser des types 64 bits en Java/C++ conduit à des bugs subtils. Le mélange des types signés/non signés en C++ peut donner de mauvais résultats. Autres
**Readability** Le code verbeux ou les commentaires excessifs peuvent masquer la logique. Il est difficile de maintenir un code miné ou fortement macroéconomique. Autres

---

Pourquoi ce problème est-il à l'origine de votre interview ?

1. **Classic Greedy Pattern** – Beaucoup d'intervieweurs aiment les problèmes où tri + gourmand donne la réponse. La maîtrise de ce modèle vous donne confiance pour des questions similaires de distribution optimale.

2. ** Grandes contraintes d'entrée** – Démontre que vous pouvez penser au temps et à l'espace. Le tri `O(n log n)` pour 5 × 104 est acceptable, mais vous devez reconnaître la limite.

3. **Types de données et overflow** – Une erreur subtile avec des entiers 32 bits peut causer de mauvaises réponses sur les cas de bord. L'affichage des limites numériques impressionne les intervieweurs.

4. **Code évolutif** – Les solutions fournies sont concises mais prêtes à être produites. Vous pouvez les adapter aux tests unitaires, au profilage des performances ou aux contextes de révision de code.

5. **Le support linguistique Versatile** – Avoir la solution en Java, Python et C++ montre la polyvalence – valorisable pour les équipes travaillant dans des environnements polyglottes.

---

## Référencement optimisé à emporter

Si vous êtes en train de vous préparer à une interview **de l'ingénieur logiciel** et que vous voulez **impresser les recruteurs**, attaquez LeetCode 2279—**Sacs maximum avec pleine capacité de roches**. La stratégie gourmande est à la fois élégante et efficace.
Affichez votre code en **Java**, **Python** et **C++**; soulignez l'importance d'utiliser l'arithmétique 64 bits. Discutez des aspects bons, mauvais et laids** – cette profondeur démontre une pensée critique.

> ** Titre riche en mots clés :** Code de Leet 2279: Java/Python/C++ Solution pour l'avidité – Le bon, le mauvais et le mauvais*
> **Description détaillée:** *Découvrez comment résoudre LeetCode 2279 en Java, Python et C++ en utilisant un algorithme gourmand. Comprendre les cas de bord, éviter les débordements, et stimuler vos perspectives d'entrevue.

---

Conclusion

- Oui. Le problème se résume à *sacs de remplissage qui ont besoin des plus petits rochers d'abord*.
- Greedy + tri donne une solution optimale dans le temps "O(n log n).
- La prise en compte des grands nombres et des cas de bord assure la justesse.
- Présenter la solution dans plusieurs langues met en évidence l'adaptabilité – un trait attrayant pour les recruteurs.

Bon codage, et bonne chance d'atterrir ce travail de rêve!