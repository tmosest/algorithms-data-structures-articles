---
titre: LeetCode 1558. Nombre minimum d'appels de fonction pour effectuer la répartition des cibles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1558 – Nombres minimums d'appels de fonction pour effectuer la répartition des cibles
C++)**

---

Récapitulation des problèmes

On vous donne un tableau entier **`nums`**.
Vous commencez par un tableau **`arr`** de la même longueur, tous les zéros.
Vous pouvez appeler l'une des deux opérations n'importe quel nombre de fois:

Opération Effet
-- -- -- -- -- --
"incrément i)" Augmenter de 1.
"double()" Multipliez **chaque** élément dans `arr` par 2.

Votre objectif est de transformer `arr` en `nums` avec les opérations totales **fewest**.
Retournez le nombre minimum d'opérations.

> **Constraints**
> * 1 ≤ "longueur en nombre" ≤ 105
> * 0 ≤ `nums[i]` ≤ 109
> * La réponse correspond toujours à un entier signé 32 bits.

---

- Oui. Points de vue clés – Pensez à l'inverse

Si nous *construisons* un nombre de 0 à sa valeur finale, chaque `1` bit nous force à utiliser un `incrément`.
Chaque fois que nous décalons une représentation binaire gauche (c.-à-d., multiplier par 2), nous utilisons un "double".

**Vue inverse* *
Commencez par les numéros finals et les épluchez à zéro:

1. Alors qu'un nombre est étrange → nous devons avoir effectué un `increment`.
(Supprimer ce `1` en soustrayant 1 → équivalent à `num & (num‐1)` en bits.)
2. Chaque fois que le nombre est même → un `double` a été appliqué plus tôt.
(Divide par 2 → quart à droite.)

Donc :

* **Nombre d'accroissements** = nombre pop-count total de tous les nombres.
* **Nombre de doubles** = *nombre maximum* de postes de droite nécessaires pour tout élément
= `(longueur maximale du bit) – 1`.

L'option «double» apparaît parce que le tableau commence à 0; le tout premier «double» est inutile si tous les nombres sont nuls.

---

Algorithme final (Greedy & Bit-Level)

Texte
étape_inc = 0
max_shift = 0

pour chaque x en nombres:
Nombre 1 bits (incréments)
steps_inc += popcount(x)

# Suivre le nombre de quarts (doubles) requis
si x > 0:
équipes = plancher(log2(x)) # ou bit_longueur - 1
max_shift = max(max_shift,shift)

return steps_inc + max_shift
«» "

*Complexité temporelle* – **O(n log M)**, où `M` est l'élément maximum.
*Complexité spatiale* – **O(1)**.

Parce que `nums[i] ≤ 109`, `log2(M)` ≤ 30, donc l'algorithme est effectivement linéaire dans la pratique.

---

- Oui. Référence Mise en œuvre

#### 4.1 Java

"Java
solution de classe publique {
Services d'information
Int addOps = 0;
int maxShift = 0;

pour (int x : nombres) {
// Compte 1 bits
addOps += Integer.bitCount(x);

// Nombre de doubles nécessaires pour cet élément
si (x > 0) {
shift int = 31 - entier.numberOfLeadingZeros(x); // floor(log2(x))
maxShift = Math.max(maxShift, poste);
}
}
retour addOps + maxShift;
}
}
«» "

> **Pourquoi `31 - numéro OfLeadingZeros`?**
> Le Javas `Integer.bitCount` donne pop-count.
> `Integer.numberOfLeadingZeros' renvoie le nombre de bits zéro en tête d'un int 32 bits;
> soustrayant de 31 donne l'indice du bit le plus élevé.

---

4.2 Python

'`python
def min_operations(nums):
add_ops = 0
max_shift = 0

pour x en nombres:
add_ops += bin(x).count('1') # popcount
si x:
déplacement = x.bit_longueur() - 1 # plancher(log2(x))
max_shift = max(max_shift, shift)

retour add_ops + max_shift
«» "

*Note:* `int.bit_length()` retourne le nombre de bits nécessaires pour représenter le nombre en binaire, c'est-à-dire `floor(log2(x)) + 1`.

---

### 4.3 C++

'`cpp
solution de classe {
public:
les opérations (vecteurs<int> et nombres) {
longue longue addOps = 0; // utiliser longtemps pour éviter les débordements pendant le comptage
int maxShift = 0;

pour (int x : nombres) {
addOps += __constructin_popcount(x); // popcount

si x) {
shift int = 31 - __constructin_clz(x); // plancher(log2(x))
maxShift = max(maxShift, quart);
}
}
retourner static_cast<int>(addOps + maxShift);
}
};
«» "

`_builtin_clz` compte des zéros en tête; `31 - clz(x)` est l'indice bit le plus élevé.

---

C'est pas vrai. Article du blog: Le bon, le mauvais et le mauvais de LeetCode 1558

Titre optimisé du SEO
Code de sortie 1558 – Nombres minimums d'appels de fonction pour faire la répartition des cibles: une solution de graisse de niveau bit (Java, Python, C++)* *

Mots clés
* Code Leet 1558
* Nombre minimum d'appels de fonction
* Un peu de manipulation gourmande
* Solution Java
* Solution Python
* Solution C++
* Problème d'entrevue de codage
* Entretien sur l'ingénierie logicielle

---

Article

5.1 Introduction
Lors de la préparation d'une entrevue sur l'ingénierie logicielle, le problème des nombres minimums d'appels de fonction pour rendre la répartition des cibles apparaît souvent. Il teste votre capacité à penser *revers* et de levier **bit manipulation** pour atteindre une complexité de temps optimale. Ci-dessous, nous disséquons le problème, nous traversons une solution avide élégante, et nous le comparons à des alternatives moins efficaces.

5.2 Réévaluation des problèmes
Nous commençons par un tableau de zéros et deux opérations: `increment(i)` (ajouter 1 à un seul élément) et `double()` (multipliez chaque élément par 2). Notre tâche est de transformer le zéro-array en «nums» cible avec les opérations totales **fewest**.

5.3 L'approche « Bonne » – Greedy Bit-Level
- **Simplicité**: Il suffit de deux compteurs – un pour les incréments (somme «popcount») et un pour les doubles ('max bit‐longueur – 1').
- **Efficacité du temps**: O(n log M) où M ≤ 109, qui est essentiellement linéaire.
- **Efficacité spatiale**: O(1).
- ** Logique intuitive** : Chaque bit `1` demande un accroissement ; chaque changement de gauche exige un double.
- **Language-agnostique**: La même logique fonctionne en Java, Python et C++ avec des différences de syntaxe minimes.

##### 5.4 L'erreur – Simulation de la force brute
Une simulation naïve :

1. Itérer à travers chaque élément, effectuer des incréments et doubler sur le tableau lui-même jusqu'à ce qu'il corresponde à "nums".
2. Chaque opération modifierait le tableau entier, ce qui entraînerait un temps O(n × #operations).
3. Cela explose rapidement pour `nums.longueur = 105` et de grands nombres (jusqu'à 109).
4. De plus, il utilise l'espace supplémentaire O(n) pour stocker des tableaux intermédiaires.

**Pourquoi c'est une mauvaise idée**: Il n'exploite pas la structure mathématique du problème et conduit à des timeouts sur de vraies plateformes d'interview.

##### 5.5 Le "Ugly" – Maths sur-optimisés avec des journaux
Certaines solutions tentent de précalculer le nombre maximum de doubles en divisant le nombre maximum à plusieurs reprises par 2 :

"Java
int maxShift = 0;
Int x = *max(nums);
pendant que (x > 0) { maxShift++; x /= 2; }
«» "

Bien que correcte, cette approche :

- Utilise la division entière dans une boucle – toujours O(log M) mais moins lisible.
- Nécessite un passe supplémentaire pour trouver le maximum.
- Il manque le calcul le plus concis de la longueur du bit (`Integer.numberOfLeadingZeros`).

Le code résultant peut être moins durable et plus difficile à comprendre en un coup d'oeil.

5.6 Réflexions finales et conseils d'entrevue
- **Exposer la perspective inverse**: Nous pelons les chiffres binaires. (en milliers de dollars)
- **Mention popcount**: Beaucoup d'intervieweurs aiment que vous utilisiez des tours de bits intégrés (`_builtin_popcount`, `Integer.bitCount`).
- ** État du temps et de la complexité spatiale**.
- **Soyez prêt à discuter de cas de bord** : Tous les zéros, un seul élément, de grands nombres.
- **Afficher le code dans la langue choisie** – Java, Python ou C++ – et souligner que la logique reste la même.

##### 5.7 Enveloppe
Le problème LeetCode 1558 illustre comment un ensemble d'opérations apparemment complexe s'effondre dans une solution linéaire propre lorsqu'on le voit à travers la lentille de représentation binaire. Maîtrisez cette approche, et vous aurez un fort point de discussion pour toute interview d'algorithme.

---

Conclusion

- **Java** – Utiliser `Integer.bitCount` et `Integer.numberOfLeadingZeros`.
- **Python** – Utilisez `bin(x.count('1')` et `x.bit_length()`.
- **C++** – Utiliser `_builtin_popcount` et `_builtin_clz`.

Les trois solutions fonctionnent en temps linéaire et en espace constant, parfaitement adaptés aux contraintes de LeetCode 1558. Bonne chance dans votre prochain entretien !