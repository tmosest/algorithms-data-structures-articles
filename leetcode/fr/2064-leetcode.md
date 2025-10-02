---
titre: LeetCode 2064. Maximum minimal de produits distribués à tout magasin -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2064 – Maximum minimal de produits distribués à tout magasin
- Oui. 1. Récapitulation des problèmes (Code Leet 2064)

Vous recevez:

Sens de l'entrée
C'est quoi ?
Nombre de magasins spécialisés de détail («1 ≤ n ≤ 105»). Autres
Quantités Types de produits «m» («1 ≤ m ≤ n»). «quantités[i]» est la quantité du type de produit *i* («1 ≤ quantités[i] ≤ 105»). Autres

**Règles**

1. Chaque magasin peut recevoir ** au plus un type de produit**.
2. Un magasin peut recevoir **tout montant** de ce type (y compris zéro).
3. Tous les produits doivent être distribués.

Laissez `x` être le plus grand nombre de produits donnés à n'importe quel magasin.
**Objectif:** minimiser `x`.

> **Retourner le minimum possible "x".**

---

- Oui. 2. Aperçu de la solution

L'observation clé :
Si nous décidons qu'aucun magasin ne peut recevoir plus d'articles "mid", nous pouvons vérifier si une distribution est possible.

- Pour chaque type de produit avec la quantité `q`, le nombre de magasins requis est
`ceil(q / mi) = q / mi` arrondi.
- Résumez ça pour tous les types.
- Si le total ≤ `n`, le `mid` choisi est possible; sinon, il est trop petit.

Les valeurs `mid` possibles forment un ensemble **monotonique**: si `mid` fonctionne, toutes les valeurs plus grandes fonctionnent aussi.
Par conséquent, nous pouvons effectuer une recherche binaire du plus petit `mid` possible dans la gamme `[1, max(quantités)]`.

---

- Oui. 3. Complexité

Opération Temps Espace
- C'est quoi ?
Contrôle de faisabilité (`ispossible`) Autres
Recherche binaire (log max) Autres

Avec `m ≤ 105` et `max ≤ 105`, cela fonctionne confortablement sous 100 ms.

---

- Oui. 4. Mise en œuvre du code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous utilisent le même modèle de recherche binaire + de vérification de faisabilité.

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
pulvérisateur privéDistribution(int n, quantités int[], limite int) {
magasins longs Nécessaire = 0; // utiliser longtemps pour éviter le débordement
pour (int q : quantités) {
// Ceil division: (q + limite - 1) / limite
magasins Nécessaire += (q + limite - 1) / limite;
si (storesNeeded > n) retourner false; // sortie anticipée
}
retour vrai;
}

l'intérêt public minimisé Maximum(int n, quantités int[]) {
Int faible = 1;
int high = Arrays.stream(quantités).max().orElse(1); // high = quantité maximale
réponse int = élevée;

alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;
si (peut distribuer(n, quantités, milieu)) {
réponse = milieu; // milieu de travail, essayer plus petit
élevé = milieu - 1;
} autre {
faible = milieu + 1; // milieu trop petit
}
}
réponse de retour;
}
}
«» "

> **Pourquoi "long"?**
> La somme intermédiaire peut atteindre `m * (q/1)`, qui pourrait déborder un int 32-bit.

---

4.2 Python

'`python
Solution de classe:
def can_distribute(self, n: int, quantities: List[int], limite: int) -> C'est vrai.
store_need = 0
pour q en quantités:
stores_besoins += (q + limite - 1) // limite # division ceil
si le _stores est nécessaire > n:
Retour Faux
retour Vrai

def minimisé Maximum(self, n: int, quantités: Liste[int]) -> Int:
faible, élevé = 1, max (quantités)
réponse = élevée

alors que faible <= élevé:
milieu = (faible + élevé) // 2
si self.can_distribute(n, quantités, milieu):
réponse = milieu
élevé = milieu - 1
Sinon:
faible = milieu + 1
réponse de retour
«» "

> **Astuce:** Utilisez `(q + limite - 1) // limite` pour la division Ceil pour éviter l'arithmétique en point flottant.

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
particulier:
bool canDistribute(int n, const vector<int>& quantities, int limit) {
longs stocks = 0; // utiliser longtemps pour la sécurité
pour (int q : quantités) {
magasins += (q + limite - 1) / limite; // ceil division
si (les magasins > n) retournent faux;
}
retour vrai;
}
public:
int minimisé Maximum(int n, vecteur<int>& quantités) {
Int faible = 1;
int high = *max_element(quantities.begin(), quantities.end());
int ans = élevé;

alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;
si (peut distribuer(n, quantités, milieu)) {
ans = milieu;
élevé = milieu - 1;
} autre {
faible = milieu + 1;
}
}
le retour des an;
}
};
«» "

---

- Oui. 5. Le bon, le mauvais et le mauvais

Qu'est-ce qui fonctionne Qu'est-ce qui peut aller mal
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Binary Search Bounds** Oublier que `n` peut être plus grand que `m` → vous pouvez mettre bas trop haut. Toujours régler bas = 1; haut = max. Autres
Autres **La division de conseil**= `(q + limite - 1) / limite` est entière, rapide et correcte. L'utilisation de `ceil(q / limit)` avec un point flottant peut donner des erreurs de précision. Collez à la formule entière. Autres
**Excédent**= Utilisation de 64 bits (longs/longs) pour les sommes intermédiaires. Summing 105 * 105 peut déborder int. 32-bit. Autres
Autres **Découvrez la boucle lorsque les magasins > n économisent du temps. Ajouter `if (stores_need > n) retourner false;` dans la boucle. Autres
Autres Tous les produits = 1 → réponse = 1. La vérification de faisabilité gère tout. Autres
**Tests**= Tests randomisés couvrant `n == m`, `n >> m` et de grandes valeurs `q`. Une couverture de test inadéquate → bugs cachés. Écrire des tests d'unité qui exercent chaque cas d'angle. Autres

> **Ligne de bottom:** Gardez l'invariant de recherche binaire ('faible <= haut') et gardez contre le débordement. Le code ci-dessus suit ces lignes directrices.

---

- Oui. 6. Pourquoi cela compte pour votre entrevue

1. **Reconnaissance des brevets** – La recherche binaire sur la limite réalisable est un tour d'interview canonique.
2. **Efficacité de l'espace** – Toutes les solutions sont exécutées sous la rubrique «O(1)» mémoire supplémentaire, un plus pour le code de production.
3. ** Flexibilité linguistique** – Démontrez que vous pouvez résoudre le même problème en Java, Python et C++.
4. **Classification des problèmes** – Il s'agit d'un problème classique *array + recherche binaire* ; étant couramment en elle montre que vous pouvez gérer des énigmes -array ou -min-max.

Autres *Ajouter cette solution à votre liste de LeetCode et être prêt à expliquer le raisonnement dans un entretien technique. *

---

- Oui. 6. SEO-Optimized Blog Post

Ci-dessous est un article complet qui est prêt à coller dans un CMS ou un éditeur de balisage.
Il contient les mots-clés de la cible, la méta description, la structure du cap et les liens internes aux extraits de code.

---

** Maximum minimal de produits distribués dans n'importe quel magasin (Code Leet 2064)**

Description de la méta
Solve LeetCode 2064 – Maximum minimal de produits distribués à tout magasin – avec des solutions Java, Python et C++ efficaces. Apprenez l'astuce de recherche binaire, l'analyse de complexité et les idées prêtes à l'entrevue.

---

C'est vrai. Mots clés
- LeetCode 2064
- Maximum minimal de produits distribués à tout magasin
- algorithme de recherche binaire
- problème de partage du tableau
- problème de codage des entretiens
- entretien de génie logiciel
- Recherche binaire Python
- Problèmes de tableau Java
- Entretien algorithmique C++

---

Table des matières

1. Aperçu du problème
2. Aperçu de la solution
3. Analyse de la complexité
4. Échantillons de codes
- Java
- Python
- C++
5. Les bons, les mauvais et les méchants
6. Conseils d'entrevue
7. Lire plus

---

- Oui. 1. Aperçu du problème

* Fournir l'énoncé concis du problème avec des exemples et des contraintes. *

> **Exemple 1**
> `n = 4, quantités = [2, 3, 4]` → réponse = **3**.

> **Exemple 2**
> `n = 6, quantités = [10, 12, 15]` → réponse = **5**.

---

- Oui. 2. Aperçu de la solution

1. ** Vérification de faisabilité** – Décider d'une limite « mi ».
Calculer les magasins requis: `ceil(q / mi)` pour chaque type.
2. **Monotonicité** – Si `mid` fonctionne, toute limite plus grande fonctionne aussi.
3. **Binary Search** – Trouvez le plus petit "mid".

> *Pourquoi la recherche binaire? *
> L'ensemble de limites réalisables est un intervalle contigu. La recherche binaire donne des réductions `O(log max)`.

---

- Oui. 3. Analyse de la complexité

- **Heure**: "O(m log max(quantités)) "
- **Espace**: "O(1)"

> **Pourquoi est-ce rapide? * *
> Avec `m, max ≤ 105`, la boucle intérieure tourne au plus 105 fois et la recherche binaire externe est ≤ 17 itérations → < 2 ms.

---

- Oui. 4. Échantillons de codes

#### 4.1 Java

"Java
solution de classe publique {
pulvérisateur privéDistribution(int n, quantités int[], limite int) {
magasins longs = 0;
pour (int q : quantités) {
magasins += (q + limite - 1) / limite; // ceil division
si (les magasins > n) retournent faux;
}
retour vrai;
}

l'intérêt public minimisé Maximum(int n, quantités int[]) {
int low = 1, high = Arrays.stream(quantities).max().orElse(1), ans = high;
alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;
si (peut distribuer(n, quantités, milieu)) {
ans = milieu;
élevé = milieu - 1;
} autre {
faible = milieu + 1;
}
}
le retour des an;
}
}
«» "

4.2 Python

'`python
Solution de classe:
def can_distribute(self, n: int, quantities: List[int], limite: int) -> C'est vrai.
magasins = 0
pour q en quantités:
magasins += (q + limite - 1) // limite
si les magasins > n:
Retour Faux
retour Vrai

def minimisé Maximum(self, n: int, quantités: Liste[int]) -> Int:
faible, élevé = 1, max (quantités)
ans = élevé
alors que faible <= élevé:
milieu = (faible + élevé) // 2
si self.can_distribute(n, quantités, milieu):
ans = milieu
élevé = milieu - 1
Sinon:
faible = milieu + 1
retour et
«» "

### 4.3 C++

'`cpp
solution de classe {
particulier:
bool canDistribute(int n, vecteur const<int>& q, limite int) {
longs magasins longs = 0;
pour (int val : q) {
magasins += (val + limite - 1) / limite;
si (les magasins > n) retournent faux;
}
retour vrai;
}
public:
int minimisé Maximum(int n, vecteur<int>& quantités) {
int low = 1, high = *max_element(quantités.begin(), quantities.end(), ans = high;
alors que (faible <= haut) {
int milieu = faible + (élevé - faible) / 2;
si (peut distribuer(n, quantités, milieu)) {
ans = milieu;
élevé = milieu - 1;
} autre {
faible = milieu + 1;
}
}
le retour des an;
}
};
«» "

---

5. Les bons, les mauvais et les méchants

Ce qui est bon
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Choisir les limites**= `1 ... max(quantités)` couvre toujours la réponse. Erreurs hors-par-un (par exemple, en commençant par «faible» à 0). Conserver `faible = 1`. Autres
**La division de conseil est rapide et exacte. L'utilisation de `math.ceil()` ou de mathématiques flottantes peut ralentir les choses. Stick à l'arithmétique entier. Autres
**L'excès d'eau est une protection du nombre de magasins. Utilisez des entiers de 64 bits. Autres
**Démarrer rapidement**=Casser la boucle dès que les magasins dépassent `n`.=Le manque de sortie anticipée peut perdre du temps. Ajouter `si (stores > n) retourner false;`. Autres
**Tests**= Les tests randomisés couvrent tous les cas d'angle.= Pas de test pour `n` >> `m`.= Inclure les cas de bord dans le harnais d'essai. Autres

---

- Oui. 6. Conseils de préparation à l'entrevue

1. ** Expliquez la monotonicité** tôt – les intervieweurs adorent vous voir repérer la propriété de recherche binaire.
2. **Afficher vos maths** : dérivez la formule de la division Ceil.
3. **Débordement de Mention** – expliquez pourquoi vous avez utilisé des compteurs 64 bits.
4. **Cas d'Edge** – mettre en évidence `n` > `m`, tous `q` = 1, seul grand type.
5. **Heure et espace** – état `O(m log max)` et justifier.

---

- Oui. 7. Lire plus

Sujet Lien
- Oui.
LeetCode 2064 Discussion: https://leetcode.com/problèmes/minimisé-maximum-de-produits-distribué-à-tout-magasin/ Autres
Modèle de recherche binaire https://leetcode.com/tag/binary-search/ Autres
La division Ceil en entier arithmétique https://stackoverflow.com/a/1115627 Autres
Des problèmes d'array de style d'entrevue Autres

---

- Oui. 8. TL;DR

*Binary recherche la plus petite limite par magasin. Pour une limite choisie, compter les magasins requis avec `ceil(q / limite)`. Si ≤ `n`, la limite fonctionne; sinon, augmentez-la. Implémenté proprement en Java, Python et C++ ci-dessus. *

Bonne chance pour tuer l'interview ! C'est ce qu'il a dit