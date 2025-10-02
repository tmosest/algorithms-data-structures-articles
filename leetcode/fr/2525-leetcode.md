---
titre: LeetCode 2525. Categorize Box selon les critères - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2525 – Catégorie boîte selon les critères
**Une solution rapide et complète en Java, Python & C++ (heure O(1), espace O(1))* *

---

Aperçu du problème

- **Input**: 4 entiers – "longueur", "largeur", "hauteur", "masse" "
** Sortie**: "String" représentant la catégorie:
- "Bulky" – toute dimension ≥ 10 000 **ou** volume ≥ 1 000 000 000
- "Lourd" – masse ≥ 100
- "Les deux" - satisfait aux deux conditions
- "Ni " – ne satisfait à aucun
- **Constraints**
- "1 ≤ longueur, largeur, hauteur ≤ 105 "
"1 ≤ masse ≤ 103"
- Le volume peut être aussi grand que 1015 → 64-bit entier requis

> **Objectif** : Retourne la bonne catégorie en temps et mémoire constants.

---

- Oui. Idées de base

Tous les contrôles sont des comparaisons simples – pas de boucles, pas de récursion.
La seule subtilité est d'éviter le débordement entier lors du calcul du volume.
Nous jetons à `long` (Java), `long long` (C++), ou utilisons des entiers non liés.

Texte
encombrant = (dim ≥ 10_000) OU (volume ≥ 1_000_000_000)
masse > 100
«» "

Retourner le résultat en fonction des quatre combinaisons possibles de booléens.

---

C'est vrai. Mise en œuvre

Voici des solutions idiomatiques propres pour **Java**, **Python** et **C++**.

---

#### 3.1 Java

"Java
***
* Code Leet 2525 – Catégoriser Encadré selon les critères
* Java 17
*/
solution de classe publique {
public Chaîne catégoriserBox(longueur int, largeur int, hauteur int, masse int) {
// Utiliser longtemps pour éviter le débordement de longueur*largeur*hauteur
volume long = 1L * longueur * largeur * hauteur;

booléen encombrant = longueur >= 10_000=1 largeur >= 10_000=1 hauteur >= 10_000
Volume >= 1 000_000_000L;
booléen lourd = masse >= 100;

si (bombardement et lourd) retournent les deux;
si (bulky) retourne "bulky";
si (lourd) retourne "lourd";
retourner "ni l'un ni l'autre";
}
}
«» "

*Complexité*: temps `O(1)`, espace supplémentaire `O(1)`.

---

3.2 Python

'`python
Code Leet 2525 – Catégoriser Encadré selon les critères
# Python 3

def categorisBox(longueur: int, largeur: int, hauteur: int, masse: int) -> str:
volume = longueur * largeur * hauteur # Les ints Python sont non liés

encombrant = longueur >= 10_000 ou largeur >= 10_000 ou hauteur >= 10_000 \
ou volume >= 1_000_000_000
masse >= 100

si volumineux et lourd:
retour "Les deux"
si volumineux:
retour "Bulky"
si lourd:
retour "Lourd"
retourner "ni l'un ni l'autre"
«» "

*Complexité*: temps "O(1)", espace "O(1)".

---

#### 3.3 C++

'`cpp
// LeetCode 2525 – Catégoriser Encadré selon les critères
// C++17

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
catégorisation des chaînes Boîte (longueur de l'int, largeur de l'int, hauteur de l'int, masse de l'int) {
// Multiplication 64 bits pour éviter les débordements
long volume = 1LL * longueur * largeur * hauteur;

bool encombrant = longueur >= 10000,1 largeur >= 10000,1 hauteur >= 10000
Volume >= 1000000000LL;
bool heavy = masse >= 100;

si (bombardement et lourd) retournent les deux;
si (bulky) retourne "bulky";
si (lourd) retourne "lourd";
retourner "ni l'un ni l'autre";
}
};
«» "

*Complexité*: temps «O(1)», espace auxiliaire «O(1)».

---

C'est pas vrai. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
Une passe, pas de boucle. La logique est banale mais facile à lire. Les solutions originales utilisaient parfois plusieurs chaînes temporaires (`box`, `box1`), rendant le flux plus difficile à suivre. Autres
**Sécurité**= Utilise l'arithmétique 64 bits pour éviter les débordements. Aucun. Autres
**Readability**. Nécessite un modèle mental de quatre combos booléens. Les chaînes "if" nichées ou les noms de variables trop verbeux peuvent masquer l'intention. Autres
**Performance** Aucun.
**Extensibilité** Aucune.La suringénierie (p. ex. créer une structure pour chaque condition) gonflerait le code. Autres

> ** Ligne de bottom** – Gardez-le court, utilisez des drapeaux `bool` et jetez-les sur `long`/`long` pour vous protéger contre les débordements. C'est tout ce dont vous avez besoin pour une réponse d'entrevue prête à la production.

---

C'est vrai. Pourquoi cela compte pour votre travail de chasse

- **LeetCode Mastery** – Démontre le raisonnement rapide et l'utilisation correcte des types de données.
- **Préparation à l'entrevue** – Montre que vous pouvez produire des solutions O(1) propres.
- **Cross‐Language Proficiency** – Résolue en Java, Python et C++ → idéal pour les piles technologiques qui utilisent n'importe lequel de ces.
- **Explication** – Le billet de blog lui-même est un grand point de discussion dans les interviews comportementales: Voici un problème que j'ai résolu, et je vais marcher à travers le bon, le mauvais, et le laid. (en milliers de dollars)

---

Liste de contrôle finale (avant votre prochaine entrevue)

- Confirmer les contraintes pour décider de la taille entière.
- Utilisez des drapeaux booléens au lieu de plusieurs cordes.
- Écrire un seul bloc de retour (ou une chaîne claire de `if`/`else`).
- Ajouter des commentaires pour plus de clarté (en particulier pour la manipulation des caisses).
- * Essai avec valeurs limites:
- `longueur = 10_000, largeur = 1, hauteur = 1, masse = 99` → `"Bulky"`
- `volume = 1_000_000_000, masse = 100` → `"Les deux"`
- `masse = 99, toutes dimensions < 10_000` → `"ni l'un ni l'autre"`

---

Prêt à faire ce travail ?

Partagez cette solution sur votre GitHub, écrivez un billet de blog (comme celui ci-dessus), et présentez le code propre et efficace dans votre prochaine interview de codage.
Bon codage et bonne chance dans votre parcours professionnel!