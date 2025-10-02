---
titre: LeetCode 668. Kth plus petit nombre dans le tableau de multiplication -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 668. Kth plus petit nombre dans le tableau de multiplication
### D'un entretien complet Plongée profonde

Langue Complexité Remarques
C'est quoi, ça ?
*Java** *O(m log (m·n)* Utiliser `long` pour la sécurité, aide à la recherche binaire standard Autres
**Python** Le "min" intégré maintient la boucle rapidement
**C++** Utilise "long long", "std::min" Autres

> **Mots-clés cibles**: *tableau de multiplication des nombres les plus petits*, *LeetCode 668*, *interview de recherche binaire*, *solution Java Python C++*, *questions d'entrevue de codage*.

---

- Oui. 1. Récapitulation des problèmes

La table de multiplication est une matrice `mat` où `mat[i][j] = i * j` (1-indexée).
Compte tenu des entiers `m`, `n` et `k`, retourner l'élément **kth le plus petit** dans la table `m × n`.

«» "
Exemple
m = 3, n = 3, k = 5 → 3
«» "

Les contraintes (`m, n ≤ 3·104`) excluent la construction de la table complète ("O(mn)" espace).
Nous avons besoin d'une méthode **time‐efficace** qui fonctionne avec de grandes entrées.

---

- Oui. 2. La recherche binaire classique sur la valeur

Le point de vue clé :
*Les valeurs du tableau sont dans la plage `[1, m·n]`. Nous pouvons effectuer des recherches binaires dans cette plage, en comptant le nombre de nombres ≤ mi. *

2.1 Compte ≤ milieu

Pour un `mid` donné, chaque ligne `i` contient `min(n, mi/i)` éléments ≤ `mid` parce que
'i * j ≤ milieu J ≤ milieu / i'.

Le résumé de toutes les lignes donne:

«» "
count(mid) = < < i=1} < < m > > min(n, mi/i)
«» "

Si `count(mid) ≥ k`, le kth le plus petit est **= milieu**; sinon il est **> mi**.

2.2 Boucle de recherche binaire

«» "
faible = 1
haute = m * n
alors que faible < élevé:
milieu = (faible + élevé) // 2
si count(mid) >= k:
haute = moyenne
Sinon:
faible = milieu + 1
retour faible
«» "

Lorsque la boucle se termine, `low` (ou `high`) est la plus petite valeur avec au moins `k` éléments ≤ il - c'est-à-dire le kth le plus petit.

2.3 Preuve d'exactitude (Sketch)

1. **Monotonicité**: `compte(x)` ne diminue pas en «x» car ajouter plus à `x` ne peut qu'augmenter le nombre de lignes qui satisfont à « i * j ≤ x ».
2. ** Fin de la recherche binaire** : Nous rétrécissons `[faible, élevé]` jusqu'à "faible".
3. **Invariant**: Après chaque itération, la réponse se trouve dans `[faible, élevée]`.
4. **Cas de base**: Lorsque `faible == élevée`, cette valeur satisfait `count(value) ≥ k` et pour toute `v < value`, `count(v) < k`. C'est donc le kth le plus petit.

---

- Oui. 3. L'échec des approches triviales

Pourquoi ça tourne mal
C'est pas vrai.
**Générer la mémoire et le temps `O(mn)` entiers; impossible pour `m, n = 30 000` (cellules 900M). Autres
**Priority Queue avec des duplicatas** Autres
**Membre de deux points**= Même coût asymptotique; nécessite la mémoire `O(mn)` pour stocker la liste triée. Autres

Ces méthodes naïves sont excellentes pour l'enseignement des structures de données mais **won=t passe LeetCode=S limites strictes**.

---

- Oui. 4. Les cas de bord et les pièges

Piège
- Oui.
**Débordement entier** (en `m * n`)= Utiliser `long` (Java) / `long long` (C++) / `int` (Python) – Les ints de Python ne sont pas liés. Autres
**La division de zéro**= Pas de souci – les lignes commencent à 1. Autres
**« au milieu / i » La division entière est intentionnelle ; elle nous assure de compter les lignes complètes. Autres
**Les limites de la recherche binaire**= `haute` doivent être `m * n`, et non `m + n`. Autres
**Délai**Éviter les appels `min` répétés en limitant la boucle: arrêter quand `mid/i== 0'. Autres

---

- Oui. 5. Mise en oeuvre des références

> **Chaque bloc de code est autonome, annoté et prêt à être collé. **

##### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int find KthNumber(int m, int n, int k) {
longue basse = 1;
long haut = (long) m * n; // 64-bit pour éviter le débordement

pendant que (faible < haut) {
long milieu = (faible + élevé) / 2;
longue cnt = nombre MoinsOrEqual(mid, m, n);

si (cnt >= k) {
haute = moyenne; // kth <= moyenne
} autre {
faible = milieu + 1; // kth > moyenne
}
}
retour (int) faible; // faible == élevé
}

Compte long privé MoinsOrEqual(long mi, int m, int n) {
nombre long = 0;
pour (int i = 1; i <= m; i++) {
nombre += Math.min(n, (int) (milieu / i));
si (compter >= Entier. MAX_VALUE) pause; // arrêt précoce si trop grand
}
le nombre de retours;
}
}
«» "

5.2 Python

'`python
Solution de classe:
def trouver KthNumber(self, m: int, n: int, k: int) -> Int:
faible, élevé = 1, m * n

alors que faible < élevé:
milieu = (faible + élevé) // 2
si self._count_le(mid, m, n) >= k:
haute = moyenne
Sinon:
faible = milieu + 1
retour faible

@staticmethod
def _count_le(mid: int, m: int, n: int) -> Int:
somme de retour (min(n, mi/ i) pour i dans la plage (1, m + 1))
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int trouver KthNumber(int m, int n, int k) {
long long bas = 1, élevé = 1LL * m * n;

pendant que (faible < haut) {
long moyen = (faible + élevé) / 2;
si (compteLE(mid, m, n) >= k)
haute = moyenne;
Autre
faible = milieu + 1;
}
retourner static_cast<int>(faible);
}

particulier:
long long countLE(long moyen, int m, int n) {
long cnt = 0;
pour (int i = 1; i <= m; ++i)
cnt += min<long long>(n, milieu/i);
retour cnt;
}
};
«» "

---

- Oui. 6. Résumé de l'entrevue

Questions clés Autres
C'est pas vrai.
*Pourquoi la recherche binaire sur la valeur? Les valeurs du tableau sont triées dans un sens conceptuel 1-D. Autres
*Quelle est la complexité du temps? *= `O(m log (m·n))` – le `log` vient de la recherche binaire sur la plage de valeurs; la boucle `m` compte. Autres
*Pouvons-nous nous améliorer à `O(log m + log n)`? Non, parce que chaque nombre nécessite l' itération sur les lignes `m` (ou les colonnes `n`). Autres
*Comment gérer les grands entiers `m, n`?*= Utiliser des entiers 64 bits pour les calculs. Autres
*Pourquoi ne pas utiliser un tas? *= Le tas aurait besoin de "O(mn)" pousses/pops → beaucoup trop lent. Autres

**À emporter** : La stratégie binaire de recherche sur la valeur est élégante, rapide et à l'échelle. C'est le modèle *exacte* que de nombreux gestionnaires d'embauche recherchent lors de la recherche de votre intuition algorithmique.

---

- Oui. 7. SEO-Optimized Blog Post Structure

«» "
<title>Kth plus petit nombre dans la table de multiplication – LeetCode 668 Solution (Java, Python, C++)</title>
<meta name="description" content="Apprenez la solution de recherche binaire optimale pour LeetCode 668 – Kth plus petit nombre dans le tableau de multiplication. Extraits de code en Java, Python, C++. Conseils d'entrevue.">
«» "

C'est vrai. H1: LeetCode 668 – Kth plus petit nombre dans le tableau de multiplication

#### H2: Aperçu du problème et contraintes
C'est vrai. H2: Pourquoi les approches naïves échouent – La mauvaise
C'est vrai. H2: Solution de recherche binaire optimale – Le bon
- H3 : comptage ≤ milieu
- H3: Boucle de recherche binaire
- Oui. H3: Correctivité et complexité

#### H2: Pièges communs – Les Extrêmes
C'est vrai. H2: Code de référence en Java, Python, C++
C'est vrai. H2: Conseils d'entrevue et comment expliquer votre processus de pensée
C'est vrai. H2: Vers le haut et plus loin Lecture

Utilisez les listes **bullet**, **code clôtures** et **mots-clés gras** pour améliorer la lisibilité et le référencement. Inclure des liens internes (p. ex., D'autres problèmes de LeetCode similaires à 668) et des liens externes aux messages de discussion LeetCode que vous avez référencés.

---

- Oui. 8. Pensée de clôture

Mastering *Le numéro le plus petit de la table de multiplication* montre votre capacité à :

1. Reconnaître **ordre implicite** dans une structure 2-D.
2. Appliquer **recherche binaire** sur une plage de valeurs, pas des indices.
3. Poignez de grandes entrées avec **arithmétique entier prudent**.

Ces compétences sont exactement ce que les intervieweurs de Google, Amazon et Stripe demandent. Laissez tomber cet article sur votre portfolio ou LinkedIn et laissez les offres d'emploi rouler!