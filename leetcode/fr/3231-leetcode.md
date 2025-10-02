---
titre: LeetCode 3231. Nombre minimum de séquences subséquentes croissantes à supprimer -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Résoudre le LeetCode 3231: Nombre minimum de subséquences croissantes à supprimer
C++ – O(n log n) Temps, O(n) Espace**

---

Récapitulation des problèmes

> Étant donné un tableau entier `nums`, vous pouvez à plusieurs reprises **supprimer une sous-séquence en pleine augmentation** (pas nécessairement contigu).
> **Objectif:** supprimer le tableau entier en utilisant le moins d'opérations possible.

«» "
Exemple 1
Entrée : nombres = [5,3,1,4,2]
Produit : 3
Explication :
1ère op: supprimer [1,2]
2ème op: supprimer [3,4]
3ème op: supprimer [5]
«» "

«» "
Contraintes
1 ≤ longueur nominale ≤ 105
1 ≤ nombres[i] ≤ 105
«» "

---

Le point de vue – Théorème de Dilworth

La tâche est équivalente à la partition du tableau dans le nombre ** minimum de sous-séquences en pleine augmentation**.
Par le théorème de **Dilworth, le nombre minimal de ces sous-séquences est égal à la longueur de la subséquence la plus longue non-augmentation** (LNIS) du tableau.

Le problème se réduit donc à un problème classique de tri de patience : trouvez la longueur de la plus longue séquence non croissante.

---

Deux approches pratiques

L'approche Langue Idée fondamentale Complexité
- C'est quoi ?
*TreeMap (Java) * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Heure: `O(n log n)`<br>Espace: `O(n)` Autres
**Traitement de la patience sur les valeurs annulées**= Python / C++= Conversion du problème LNIS en un LIS standard en niant chaque élément. Heure: `O(n log n)`<br>Espace: `O(n)` Autres

Les deux méthodes s'exécutent dans les mêmes limites asymptotiques, mais la version TreeMap se sent plus "Java-ish", tandis que la version LIS-on-negated-values est concise en Python et C++.

---

Détails de la mise en œuvre

- Oui. 1. Java – Version TreeMap

"Java
Importation de java.util.*;

solution de classe {
Services d'information
// Carte <ending value, count of subsequences se terminant avec cette valeur>
Carte de l'arbre<entier, entier> carte = nouvelle carte de l'arbre<>();

pour (int num : nombres) {
// Trouvez la clé la plus petite (< num)
Entier inférieur = map.lowerKey(num);
si (inférieur != nul) {
// Nous prolongeons un subséquence se terminant par 'moins '
int cnt = map.get(lower) - 1;
si (cnt == 0) map.supprimer(inférieur);
sinon map.put(lower, cnt);
}

// Maintenant démarrez / prolongez une séquence subséquente se terminant par 'num '
map.put(num, map.getOrDefault(num, 0) + 1);
}

// Total des sous-séquences gauche = réponse
= 0;
pour (int v : map.values()) total += v;
le total des retours;
}
}
«» "

**Pourquoi `la clé inférieure`?**
Si nous avons une sous-séquence se terminant à la valeur `x` (`x < num`) nous pouvons en toute sécurité y ajouter `num`. Nous choisissons la valeur plus petite *proche* de sorte que nous consommions l'une des sous-séquences qui peut être étendue.

---

- Oui. 2. Python – Patience Tri des valeurs négligées

'`python
de bisect importer bisect_left

Solution de classe:
def minOperations(self, nombres: List[int]) -> Int:
queues = [] nombre de queues de LIS sur des valeurs negées
pour x en nombres:
y = -x # convertir LNIS en LIS
idx = bisect_left(tails, y)
Si idx == len(tails):
(y)
Sinon:
queues[idx] = y
retour len(tails)
«» "

**Explication**
`tails` garde la queue la plus petite possible pour une séquence croissante de chaque longueur.
En niant, une séquence *non-augmentation* dans `nums` devient une séquence * strictement croissante* dans `-nums`.
`bisect_left` garantit que nous remplaçons la première queue qui est ≥ `y`, en maintenant des queues optimales.

---

- Oui. 3. C++ – Idée de tri de la même patience

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
les opérations (vecteurs<int> et nombres) {
vectorielle<int> queues; // queues de LIS sur des valeurs negées
pour (int x : nombres) {
int y = -x; // convertir LNIS en LIS
auto it = lower_bound(tails.begin(), tails.end(), y);
si (it == queues.end())
falls.push_back(y);
Autre
*it = y;
}
retour (int)tails.size();
}
};
«» "

---

Pourquoi ça marche ? (Proof Sketch)

1. **Le Théorème de Dilworth** nous dit que le nombre minimal de subséquences croissantes qui divisent une séquence est égal à la taille de son plus grand antichaîne (ici, une subséquence non croissante la plus longue).
2. Notre algorithme *TreeMap* construit essentiellement la plus longue subséquence non croissante: chaque fois que nous trouvons un nombre plus petit, nous extendons la subséquence actuelle; sinon nous en commençons une nouvelle.
3. Dans l'approche du tri de patience, nous calculons littéralement la longueur de la plus longue subséquence non croissante en la transformant en problème LIS.

---

Décomposition

Langue Heure Espace
- C'est quoi ?
Java (TreeMap) Autres
Python / C++ (Patience) Autres

- Oui. Le facteur log vient des opérations `TreeMap` ou de la recherche binaire (`bisect_left` / `lower_bound`).
- L'espace auxiliaire `O(n)` est dû au tableau `tails` / TreeMap.

---

Pièges communs

Piège
- Oui.
L'utilisation de `floorKey` au lieu de `lowerKey` en Java' `floorKey(num-1)` est inutile; `lowerKey(num)` est plus clair. Autres
La confusion de `bisect_left` par rapport à `bisect_right` dans Python. Autres
Autres Oublier de nier la valeur dans l'approche LIS.Sans négation, vous calculez LIS du tableau original, ce qui donne la mauvaise réponse pour le cas non croissant. Autres
Erreurs hors-par-un dans C++ `lower_bound`. Toujours vérifier `if (it == tails.end()) tails.push_back(y);` Autres

---

À emporter – Le bon, le mauvais, le mauvais

Aspect du bien
- C'est quoi ?
Le théorème de Dilworth donne une base mathématique propre. Nécessite la connaissance des posets, qui peuvent se sentir lourds pour les intervieweurs. Autres Penser en termes de cartes d'arbres peut être intimidant si vous n'êtes pas à l'aise avec `TreeMap`. Autres
La version TreeMap est très lisible pour Java ; la version LIS est concise pour Python/C++. TreeMap utilise beaucoup de mémoire (hash au-dessus). La négation des valeurs pour transformer le NISL en NIS peut ne pas être intuitive pour les nouveaux arrivants. Autres
Performance (O) `(n log n)` fonctionne confortablement jusqu'à 105.= La recherche binaire sur un tableau est plus rapide en pratique que `TreeMap`.= Aucune – les deux implémentations sont efficaces. Autres

---

Résumé optimisé du SEO

Si vous êtes à la recherche de solutions **LeetCode 3231**, cet article livre:

- **Les implémentations Java, Python et C++** qui fonctionnent dans le temps `O(n log n)`.
- Une plongée profonde dans le théorème de Dilworth** et la façon de transformer le problème en une tâche classique.
- Extraits de code pratiques avec **TreeMap** et **Traitement de la patience**.
- Conseils pour éviter les pièges communs et l'analyse **temps/espace**.

Que vous soyez en train de vous préparer à une entrevue de niveau dur ou tout simplement d'affiner votre boîte à outils algorithmique, ce guide vous donne le code propre et prêt à la production dont vous avez besoin. Bon codage !

---

**Mots-clés:** LeetCode 3231, Nombre minimum de subséquences croissantes à supprimer, solution Java, solution Python, solution C++, Théorème de Dilworth, subséquence non croissante la plus longue, LIS sur les valeurs negées, préparation d'entrevues, analyse d'algorithme.