---
titre: LeetCode 625. factorisation minimale - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 625 – Facturation minimale
### Les bons, les mauvais et les lugubres (et comment le faire dans une entrevue de codage)

> **Problème** – *Avec un entier positif `num`, retourner le plus petit entier positif `x` de telle sorte que le produit des chiffres `x` égale `num`.
> Si aucun tel `x` n'existe ou si le résultat ne correspond pas à un entier signé 32 bits, retourner `0`. *

> **Constraints**
> `1 ≤ num ≤ 2^31 – 1`

---

### TL;DR – Sommaire minimal

* La solution optimale est une factorisation **greedy**: essayez de diviser "num` par le plus grand chiffre possible (9 → 2) jusqu'à ce qu'il ne puisse plus être divisé.
* Conservez les chiffres choisis dans l'ordre inverse, puis inversez-les pour obtenir le plus petit entier possible.
* Cas de bord: `num < 10` → retour `num` elle-même; le produit final doit être égal à 1; le numéro final doit correspondre à un int 32 bits.

---

Le bon – Ce qui fonctionne et pourquoi il est élégant

Pourquoi il est grand
-- -- -- -- -- -- -- --
**O(log num)** time (temps) Nous ne divisons que par les chiffres 9–2, au plus 9×log10(num) itérations. Autres
**O(1) espace**= Aucune structure de données supplémentaire au-delà de quelques variables. Autres
**Déterministe et simple**= Facile à expliquer dans une interview – =Démarrer du plus grand chiffre et le prendre en compte.== Autres
**Poigne tous les boîtiers de bord**. Autres

La stratégie avide fonctionne parce que toute factorisation de "num` en chiffres 2–9 peut être réordonnée pour placer les chiffres plus grands plus tôt, qui *décroît* la valeur numérique globale lorsque les chiffres sont placés en ordre ascendant. En tirant d'abord le plus grand facteur possible, nous garantissons le plus petit résultat numérique.

---

- Oui. Les mauvaises – les pièges communs & Qu'est-ce que les scénarios

Qu'est-ce qui peut mal tourner
- C'est pas vrai.
**Le résultat dépasse la plage de 32 bits**Le produit des chiffres peut s'insérer dans une longue mais pas une int. Conservez le résultat dans `long` (ou `long long`), puis vérifiez contre `INT_MAX` avant de lancer. Autres
**Ne pas inverser les chiffres**** Si vous ajoutez des chiffres comme vous le considérez, vous obtiendrez le nombre dans l'ordre *descendant* (par exemple, 68 pour 48 → 8 puis 6). Ajouter une chaîne de caractères et inverser à la fin, ou prépendre pendant la construction du numéro. Autres
**Divisant par 0 ou 1** Traiter `num < 10` comme un cas de base: retourner `num` immédiatement. Autres
**Missundercompréhension de l'entier le plus positif de l'entier**=Certains pensent que le plus petit signifie le plus petit chiffre plutôt que le plus petit chiffre. Préciser que nous voulons le nombre entier *le plus petit* (par exemple 35 < 53). Autres

---

- Oui. Les pièges de bord et les cas d'essai cachés

1. **'num = 1'**
*La bonne réponse est 1, pas 0. *
Beaucoup de solutions naïves renvoient 0 par erreur pour ce cas.

2. **`num = 0`** – *non autorisé par les contraintes, mais parfois apparaît dans les tests personnalisés. *
Vous devez décider si elle est invalide ou retourner 10 (parce que 1×0 = 0). Tenez-vous aux contraintes.

3. **Très grande "num" (-)* *
Si la factorisation conduit à un nombre comme 999999999, l'algorithme doit encore détecter correctement le dépassement.

4. **Nombres non-factorables (p. ex. 17)**
La boucle gourmande finira par un reste > 1, indiquant aucune solution → retour 0.

---

- Oui. L'algorithme – Étape par étape

1. **Dossier de base**
Texte
si num < 10: retour num
«» "
2. **Initialiser**
Texte
res = 0 // résultat en entier
facteur = 1 // multiplicateur pour chaque nouveau chiffre
«» "
3. **Boucle grise (9 → 2)**
Pour chaque chiffre `d` de 9 à 2:
alors que `num % d] 0':
* diviser `num` par `d "
* ajouter `d` à l'avant de `res "
(c'est-à-dire "res = d * facteur + res")
* multiplier "facteur" par 10
4. **Vérifications finales**
*Si 'num != 1` → retourner 0* (le reste non-facturé).
*Si `res > INT_MAX` → retourner 0* (overflow).
Sinon, retourner `(int)res`.

---

Code – 3 langues

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

### Java

"Java
solution de classe publique {
plus petiteFactorisation(int num) {
si (num < 10) num de retour; // 0–9 sont déjà minimes
long res = 0, facteur = 1; // long pour éviter le débordement

pour (int d = 9; d >= 2; d--) {
alors que (num % d) 0) {
num /= d;
res = d * facteur + res; // chiffre prépendu
facteur *= 10;
}
}

// Si num > 1, il contient des facteurs principaux > 9 → impossible
// Si res > entier. MAX_VALUE, dépassement
retour (num == 1 && res <= Integer.MAX_VALUE) ? (int)res : 0;
}
}
«» "

Python

'`python
Solution de classe:
def la plus petiteFactorisation (self, num: int) -> Int:
si num < 10:
retour num

Res = 0
facteur = 1

pour d dans la plage (9, 1, -1):
alors que num % d == 0:
num //= d
res = d * facteur + res # chiffre prépendu
facteur *= 10

si num != 1 ou rés > 2**31 - 1:
retour 0
retour res
«» "

C++

'`cpp
solution de classe {
public:
la plus petiteFactorisation(int num) {
si (num < 10) retour num;

longue rés = 0;
facteur long = 1;

pour (int d = 9; d >= 2; --d) {
alors que (num % d) 0) {
num /= d;
res = d * facteur + res; // chiffre prépendu
facteur *= 10;
}
}

si (num != 1=1 res > INT_MAX) retourne 0;
retourner static_cast<int>(res);
}
};
«» "

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Autres Boucle d'avidité **O(log num)** (faible case, 9 × log10(num) divisions)
Contrôles définitifs

---

Autres approches

Description de la méthode
- C'est quoi ?
**Depth‐First Search**=Essayez récursivement tous les chiffres 2–9, prune quand le produit dépasse `num`.=Poigne les modèles de factorisation arbitraires. Dans le pire des cas, ce problème n'est pas nécessaire. Autres
**Programmation dynamique**=Construisez le plus petit nombre pour chaque produit possible. Donne un aperçu de la structure des sous-problèmes. Utilisation de la mémoire élevée; inutile pour ce problème limité. Autres
**Fabrication de prime**= Conversion de `num` en premiers 2,35,7, puis combinaison en chiffres. Nécessite une manipulation soigneuse des combinaisons ; essentiellement la même logique gourmande. Autres

La solution gourmande est la plus conviviale pour les interviews et fonctionne dans un espace constant.

---

## 8- Points de discussion prêts

1. ** Expliquez la raison d'être de l'amertume** – Nous calculons d'abord le plus grand chiffre; toute factorisation valide peut être réordonnée pour produire un nombre plus petit si les plus grands chiffres sont placés plus tard. (en milliers de dollars)
2. **Montrer la manipulation de cas de bord** – parler à travers `num < 10`, débordement, et factorisations impossibles.
3. ** Discussion sur la complexité** – mettre en évidence le temps O(log num) et l'espace O(1).
4. **Garde de débordement Mention** – en utilisant une variable 64 bits avant de vérifier `INT_MAX`.
5. **Facultatif** – mentionner que la même logique fonctionne dans n'importe quelle langue avec un type entier 64 bits.

---

## 9=" SEO-Optimized Blog Post Outline

Titre
**LeetCode 625 – Factorisation Minimum.

Description de la méta
"Master LeetCode 625 : Facturation minimale. Lisez les solutions complètes Java, Python et C++, découvrez l'algorithme gourmand, les cas de bord, la complexité et les points d'entretien. »

Rubriques et mots-clés
1. **Qu'est-ce que LeetCode 625 – Facturation minimale?** (Code 625, factorisation minimale)
2. **Pourquoi Greedy fonctionne pour les problèmes de factorisation** (algorithme de concordance, codage d'entrevue)
3. **Java, Python & C++ – Code de travail complet** (solution Java, solution Python, solution C++)
4. **Cas d'écoulement et dépassement de la factorisation** (traitement des dépassements, cas bords)
5. **Découpe de complexité temporelle et spatiale** (complexité temporelle, complexité spatiale)
6. **Conseils d'entrevue : Comment expliquer votre solution** (entrevue de codage, entrevue de LeetCode)
7. ** Approches alternatives (SDF, PDD) – Quand les utiliser** (recherche approfondie, programmation dynamique)
8. **Pièges communs à éviter** (bogues communs, mauvaise réponse, débordement)
9. **Problèmes pratiques similaires à la factorisation minimale** (problèmes de LeetCode pratique, pratique de l'algorithme)

### Appel à l'action
> "Prêt pour votre prochaine entrevue de codage? Plongez dans notre guide de solution complète, expérimentez le code et ajoutez ** Factorisation Minimum** à votre répertoire de résolution de problèmes ! »

---

À emporter

- **La factorisation gourmande est optimale**: retirez 9→2 jusqu'à ce que plus de divisions.
- **Les cas d'urgence sont importants** : manipulez `num < 10`, les nombres de débordement et les nombres non-factorables.
- **Gardez-le simple** : un algorithme O(log num) qui convient à l'espace O(1).
- **Afficher la confiance**: expliquer pourquoi l'avidité fonctionne et couvrir tous les cas de bord.

En maîtrisant ce problème, vous démontrez une forte compréhension de la théorie des nombres, des stratégies cupides et des meilleures pratiques d'entrevue – exactement ce que les recruteurs recherchent. Bonne chance, et le codage heureux! C'est ce qu'il a dit