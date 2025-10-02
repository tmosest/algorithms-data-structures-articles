---
titre: LeetCode 3663. Trouver le chiffre le moins fréquent -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code de Leet 3663 – Trouver le chiffre le moins fréquent
### Un guide complet, un code en Java / Python / C++ et un référencement Post Blog optimisé

---

Résumé du problème
**Numéro de code:** 3663
**Difficulté:** Facile

> **Avec un entier `n`, trouver le chiffre qui se produit le moins fréquemment dans sa représentation décimale. **
> Si plusieurs chiffres partagent la fréquence minimale, retourner le **le plus petit** de ces chiffres.

**Exemple**
«» "
Entrée : n = 1553322
Sortie: 1 // 1 apparaît une fois; tous les autres chiffres apparaissent deux fois
«» "

---

Aperçu de la solution
1. **Count** les occurrences de chaque chiffre («0–9»).
2. **Déterminer** la plus petite fréquence parmi ces dénombrements.
3. **Sélectionnez** le plus petit chiffre ayant cette fréquence.

**Complexité temporelle :** `O(L)` où `L` est le nombre de décimales dans `n` (au plus 10 pour un entier de 32 bits).
**Complexité spatiale:** `O(1)` – nous avons seulement besoin d'un tableau de longueur 10.

---

Mise en œuvre du code

C'est pas vrai. Java
"Java
solution de classe publique {
LeastFrequentDigit(int n) {
int[] freq = nouvelle int[10]; // fréquence[0..9]
température int = n;

// Compter chaque chiffre
pendant la période 0) {
freq[temp % 10]++;
température /= 10;
}

int minFreq = entier.MAX_VALUE;
pour (int f : freq) {
si (f > 0 && f < minFreq) minFreq = f;
}

// Retournez le plus petit chiffre avec une fréquence minimale
pour (int chiffre = 0; chiffre < 10; chiffre++) {
si (freq[numer] == minFreq) le chiffre de retour;
}
retour -1; // ne devrait jamais atteindre ici
}
}
«» "

> **Pourquoi une boucle "du temps"? * *
> Il évite de convertir le nombre en un `String` (pas d'allocation supplémentaire).
> Le garde `si (f > 0)` nous assure d'ignorer les chiffres qui n'apparaissent jamais.

---

# # # # # #
'`python
Solution de classe:
def getLeastFrequentDigit(self, n: int) -> Int:
freq = [0] * 10
temps = n

Nombre de chiffres
pendant la durée:
freq[temp % 10] += 1
durée //= 10

min_freq = min(f pour f en freq si f > 0)
pour le chiffre f dans l'énumération (fréq):
si f == min_freq:
chiffre de retour
«» "

> ** Touche pyronique** – `min()` sur un générateur évite une boucle explicite pour le minimum.

---

C'est vrai. C++
'`cpp
solution de classe {
public:
nt getLeastFrequentDigit(int n) {
int freq[10] = {0};
température int = n;

// Compter chaque chiffre
pendant que (temps) {
freq[temp % 10]++;
température /= 10;
}

Int minFreq = INT_MAX;
pour (int f : freq)
si (f > 0 && f < minFreq) minFreq = f;

pour (in digits = 0; digits < 10; ++ digits)
si (freq[numer] == minFreq) le chiffre de retour;

retour -1; // inaccessible
}
};
«» "

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
Java (L) Autres
Python "O(L)" "O(1)" Autres
* C++ * O(L) * * O(1) * Autres

Depuis `L` ≤ 10 (32-bit entier), la solution est efficace **temps constant**.

---

Les bons, les mauvais et les affreux

Catégorie
C'est pas vrai.
**Simplicité**Utilisez seulement un tableau de taille 10. (Grâce au fait que `n ≥ 1` dans les contraintes.) Autres
**Performance** Une boucle supplémentaire pour trouver la fréquence min – encore négligeable. Pas besoin de cartes de hachage, de files d'attente prioritaires ou de tri. Autres
**Readability**= Effacer les noms de variables (`freq`, `minFreq`). Une légère verbosité pour trois langues. Autres
**Cas d'Edge**=Poigne les nombres avec des chiffres répétés, tous les chiffres les mêmes, menant zéros non présents.= Faut ignorer les zéros qui n'apparaissent pas. Aucun.

**À emporter :** L'approche par tableau O(1) est la norme or pour ce problème de LeetCode. Éviter la suringénierie (par exemple, en utilisant `HashMap`, `PriorityQueue` ou `String` conversions) – ils ajoutent seulement la complexité et le temps d'exécution micro-inférieur.

---

Article de blog optimisé par le SEO

> **Titre:**
> *Trouver le chiffre le moins fréquent sur LeetCode – Java / Python / C++ Solutions + Conseils d'entrevue*

> **Description de la méta (155 à 160 caractères):**
> Master LeetCode 3663 avec code Java, Python et C++ propres. Comprendre l'algorithme, les cas de bord et les idées d'entrevue pour stimuler vos perspectives d'emploi technologique.

> **Mots clés:** LeetCode, Trouver le moins fréquent Digit, Java, Python, C++, interview, algorithme, O(n), entretien d'emploi, ingénieur logiciel, entretien de codage

---

Introduction

Trouver le chiffre le moins fréquent dans un entier peut sembler trivial, mais c'est une question d'interview de base sur des plateformes comme **LeetCode**. Il teste votre capacité à:

- Travailler avec la manipulation entière
- Construire des tables de fréquence
- Boîtes de bord de poignée proprement

Dans cet article, nous allons parcourir une solution éprouvée **O(n)** en **Java, Python et C++**. En chemin, nous disséquerons l'algorithme, discuterons des pièges potentiels et partagerons des idées prêtes à l'entrevue pour vous aider à décrocher votre prochain emploi technologique.

---

Récapitulation du problème

> ** Don**: un entier `n` (`1 ≤ n ≤ 2^31-1`).
> **Objectif** : Retournez le chiffre (0-9) qui apparaît le moins de fois dans la représentation décimale de `n`.
> **Tie‐Breaker**: Retourne le plus petit chiffre si plusieurs chiffres partagent la fréquence minimale.

---

Algorithme Plongée profonde

1. ** Compte de fréquence**
- Utilisez un tableau de taille fixe (`freq[10]`) pour retenir les chiffres 0‐9.
- Indique les chiffres de `n` en prenant `n % 10` et en divisant par 10.

2. **Trouver la fréquence minimale**
- Sautez les nombres zéro (chiffres qui n'apparaissent jamais).
- Surveillez le plus petit nombre positif.

3. **Choisir le plus petit chiffre**
- Scanner `freq` de 0 à 9 et retourner le premier chiffre correspondant à la fréquence minimale.

Pourquoi est-ce optimal ?
- **Heure**: Chaque chiffre est traité une fois – `O(L)` où `L` ≤ 10.
- **Espace**: Constante – tableau de taille 10.

---

Code Passage

(Voir les extraits de code ci-dessus pour Java, Python, C++. Chaque mise en œuvre suit la même logique.)

> **Java Conseils:**
> - Utilisez ` while (temp > 0)` pour éviter les conversions de chaînes.
> - `Integer.MAX_VALUE` initialise en toute sécurité la recherche minimale.

> **Conseils pour le python:**
> - Compréhension de la liste pour le comptage: `[0] * 10`.
> - `min(f pour f en freq si f > 0)` ignore complètement les zéros.

> **C++ Conseils:**
> - `int freq[10] = {0};` initialise toutes les entrées à 0.
> - Utiliser `INT_MAX` de `<climits>`.

---

### Cas de bord et essais

Autres Essai Entrée Sortie Raison
- C'est quoi ?
Un seul chiffre est le moins fréquent par défaut. Autres
Autres Tous les mêmes chiffres : `n = 111111`= `0`= Aucun chiffre zéro n'apparaît ; le plus petit chiffre avec une fréquence minimale est `0` (fréquence 0). Autres
Nombreux minimums : `n = 723344511` Autres
Autres Un grand nombre de personnes : "n = 2147483647" "8" L'analyse de fréquence montre 8 apparaît une fois, d'autres au moins deux fois. Autres

Validez toujours que l'algorithme gère les nombres jusqu'à 32 bits maximum et que la valeur de retour est toujours un chiffre entre 0 et 9.

---

Les bons, les mauvais, les méchants

*Bien* – O(1) espace supplémentaire, aucune structure de données supplémentaire, intention claire.
*Bad* – Nécessite une approche à deux passages (compter puis min-recherche) qui est encore triviale mais pourrait être fusionnée.
*Ugly* – La suringénierie (cartes hash, files d'attente prioritaires) ajoute une complexité et un risque inutiles de bogues.

---

### Conseils d'entrevue

- **Expliquer les contraintes**: Soulignez `n` correspond à un entier signé de 32 bits → au plus 10 chiffres.
- **Afficher la complexité du temps/de l'espace**: Mettre en surbrillance `O(L)` et l'espace constant.
- **Discuss cas bord**: Nombres avec chiffres répétés, chiffres manquants, zéros en tête.
- ** Optimisations possibles** : L'approche à un passage en suivant le fréq min pendant le comptage, mais pas essentiel.

---

Conclusion

Le problème "Find The Least Frequent Digit" est un exemple parfait de la façon dont un tableau de fréquences **simple** résout une question d'entrevue apparemment délicate. La maîtrise de ce modèle renforcera votre confiance sur les plateformes de codage et les entrevues.

Autres Vous voulez plus de LeetCode ? Abonnez-vous à des publications hebdomadaires, des plongées profondes en algorithme et des guides de préparation d'entrevue.

---

Appel à l'action

Si vous avez trouvé cet article utile, **like**, **share**, et **comment** ci-dessous avec toutes les questions ou sujets que vous souhaitez que nous traitions ensuite.

---

Liste de contrôle du référencement

- Le titre contient des mots-clés : *Trouver le chiffre le moins fréquent, LeetCode, Java, Python, C++*.
- La description de la méta utilise le mot clé principal et la proposition de valeur.
- Les rubriques (`H1`, `H2`) structurent l'article pour les moteurs de recherche.
- Les extraits de code sont correctement clôturés pour être lisibles.
- Mots-clés naturellement parsemés : * interview de codage*, * algorithme*, *O(n)*, *interview d'emploi*.

---