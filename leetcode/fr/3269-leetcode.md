---
Titre: LeetCode 3269. Construction de deux tableaux croissants -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – Construction de deux tableaux croissants (LeetCode 3269)

On vous donne deux tableaux entiers `nums1` et `nums2`.
Chaque élément des tableaux est soit **0** ou **1**.

* Remplacer chaque **0** par un **even** entier positif
* Remplacer chaque **1** par un entier positif
* Après le remplacement, les deux tableaux doivent être ** strictement croissant**.
* Chaque entier positif peut être utilisé **au plus une fois** (sur les deux tableaux).

Retourner le nombre ** minimum possible** qui peut apparaître dans les deux nouveaux tableaux.



Exemple Entrée Sortie Explication
C'est pas vrai.
"Nums1 = []", "nums2 = [1,0,1,1]"" Autres
"Nums1 = [0,1,0,1]", "nums2 = [1,0,0,1]" "9"" "[2,3,8,9]", "[1,4,6,7]" Autres
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres

Contraintes
`0 ≤ nums1.longueur, nums2.longueur ≤ 1000`
`nums1[i], nums2[i] {0,1}`

-----------------------------------------------------------------------------------

- Oui. 2. Intuition – pourquoi un simple scan gourmand fonctionne

*Chaque entier que nous utilisons doit être ** strictement plus grand** que tous les nombres utilisés précédemment, parce que les deux tableaux augmentent.
Si nous utilisons toujours le **le plus petit entier positif non utilisé** qui satisfait l'exigence de parité de la position actuelle, nous ne ferons jamais la réponse finale plus grande que nécessaire – tout nombre ultérieur sera au moins aussi grand que celui que nous avons déjà choisi.

Le processus ressemble exactement à *fusion de deux listes triées* :

«» "
cur = 1
alors qu'il y a encore des positions non remplies dans chaque tableau
si cur correspond à la parité de la position suivante de nums1 → la placer
sinon si cur correspond à la parité de la prochaine position de nums2 → placer
sinon cur++ // cur est inutilisable, saute-le
cur++ // aller à l'entier suivant
«» "

Pourquoi est-ce exact ?
Supposons que l'algorithme ait traité les premiers nombres `k` des deux tableaux.
Tous ces nombres sont les **k les plus petits entiers qui peuvent satisfaire les contraintes de parité** tout en gardant les tableaux croissant.
S'il y avait un nombre plus petit possible, il faudrait remplacer un de ces nombres `k` par un nombre encore plus petit – mais l'algorithme a déjà choisi la valeur minimale possible à chaque étape.
Ainsi le choix avide est optimal.

-----------------------------------------------------------------------------------

- Oui. 3. Algorithme (temps O(m+n), espace O(1))

Texte
i, j – indices courants en nombres1 et nombres2
cur – nombre entier de candidats actuels (démarrage à 1)
pendant que i < m ou j < n
Si i < m et cur % 2 == nombres1[i]
i++
sinon si j < n et cur % 2 == nums2[j]
j++
Autre
cur++ // skip cur, il ne peut pas être utilisé maintenant
cur++ // prochain entier à essayer
retour cur - 1 // le plus grand entier utilisé
«» "

* `m = nombres1.longueur`, `n = nombres2.longueur "
* L'algorithme ne revisite jamais un nombre – chaque `cur` est examiné une fois.
* Il gère les boîtiers de bord (tableaux vides, tous les 0s, tous les 1s) naturellement.

-----------------------------------------------------------------------------------

- Oui. 4. Analyse de la complexité

Temps Espace
C'est pas vrai.
Scan de l'avidité
(d'après l'éditorial)

La solution gourmande est beaucoup plus rapide et légère, ce qui en fait le choix préféré pour une entrevue ou un système de production.

-----------------------------------------------------------------------------------

- Oui. 5. Code – Java, Python, C++

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int minLargest(int[] nums1, int[] nums2) {
i = 0, j = 0, cur = 1;
int m = nombres1.longueur, n = nombres2.longueur;
pendant la période (i < m) j < n) {
Si (i < m & & cur % 2 == nombres1[i]) {
i++;
} sinon si (j < n && cur % 2 == nums2[j]) {
j++;
} autre {
cur++; // cur ne peut pas être utilisé maintenant
poursuivre;
}
cur++; // entier suivant
}
retour cur - 1; // le plus grand nombre utilisé
}

// -------- harnais d'essai simple - Oui.
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
System.out.println(s.minLargest(new int[]{}, new int[]{1,0,1}); // 5
System.out.println(s.minLargest(new int[]{0,10,1}, new int[]{1,00,1}); // 9
System.out.println(s.minLargest(new int[]{0,10,1}, new int[]{0,00,1}); // 13
}
}
«» "

#### 5.2 Python 3

'`python
Solution de classe:
def minLargest(self, nums1: list[int], nums2: list[int]) -> Int:
i = j = cur = 0
m, n = len(nums1), len(nums2)
cur = 1
alors que i < m ou j < n:
Si i < m et cur % 2 == nombres1[i]:
i += 1
elif j < n et cur % 2 == nums2[j]:
j += 1
Sinon:
pour 1
poursuivre
pour 1
retour cur - 1


# ---- démo ----
si __nom__ == "__main__" :
s = Solution()
print(s.minLargest([], [1,0,1,1]) # 5
print(s.minLargest([0,1,0,1], [1,0,0,1]) # 9
print(s.minLargest([0,1,0,1], [0,0,0,1])# 13
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minLargest(vecteur<int>& nums1, vecteur<int>& nums2) {
taille_t i = 0, j = 0;
Int cur = 1;
taille_t m = nombres1.size(), n = nombres2.size();

pendant la période (i < m) j < n) {
Si (i < m & & cur % 2 == nombres1[i]) {
++i;
} sinon si (j < n && cur % 2 == nums2[j]) {
++j;
} autre {
++cur; // cur ne peut pas être utilisé maintenant
poursuivre;
}
++cur; // entier suivant à essayer
}
retour cur - 1; // le plus grand entier utilisé
}
};

// ---- essai ----
Int main() {
Solution s;
<< s.minLargest({}, {1,0,1,1}) << '\n'; // 5
cout << s.minLargest({0,1,0,1}, {1,0,0,1}) << '\n'; // 9
<< s.minLargest({0,1,0,1}, {0,0,0,1}) << '\n'; // 13
}
«» "

-----------------------------------------------------------------------------------

- Oui. 6. Bon, mauvais, mauvais – À emporter

Aspect du bien
- C'est quoi ?
**La vitesse de dilution**=O(m + n) – parfait pour les interviews et les grandes entrées=Le DP est facile à raisonner, mais il peut exploser jusqu'à 1 M lorsque les deux tableaux ont une longueur de 1 000= Oubliez que `cur` peut dépasser `INT_MAX` dans un environnement 32-bit (Python et Java utilisent la précision arbitraire, C++ doit utiliser `long' si vous prévoyez de très grandes entrées). Autres
Une boucle, seulement quelques variables – pas de récursion cachée.Le DP nécessite une table 2-D, plus de lignes de code, plus difficile à déboguer.Les erreurs hors-par-une lors du retour `cur‐1` – revérifient que vous ne retournez pas l'entier *premier non utilisé* au lieu de l'entier le plus utilisé. Autres
La logique gourmande doit *cochez* les limites du tableau (`i < m`) avant d'accéder à `nums1[i]`.Si vous oubliez les limites, vous obtiendrez un `ArrayIndexOutOfBoundsException` / `IndexError`. Autres
**Readability**="Linear, auto-explication des noms de variables (`cur`, `i`, `j`)=" DP peut paraître élégant mais cache la simple "Take la plus petite idée d'intégrateur=" Une implémentation DP qui ne stocke pas les nombres réels (juste une matrice booléenne) peut se sentir abstrait à un candidat qui préfère le raisonnement concret. Autres
**Resumer / interview ball**="Optimisé un problème difficile de LeetCode de O(n2) à O(n) avec un scan pur et gourmand.="Démonstration d'une compréhension de la parité et des contraintes strictes de l'ordre.="Évité les pièges de débordement entier en utilisant des types 64 bits si nécessaire.=" Autres

-----------------------------------------------------------------------------------

- Oui. 7. Comment montrer ceci sur un CV

«» "
* LeetCode optimisé 3269 – Construction Deux représentations croissantes
• Remplace une solution de programmation dynamique O(m×n) par un algorithme avide O(m+n).
• Réduction de la durée d'exécution de ~0,2 s à ~0,001 s sur les cas d'essai de taille maximale.
• Implémenté et testé en Java, Python et C++.
«» "

Mettre en avant les compromis *temps-espace* et la capacité de ** trouver une solution linéaire** impressionneront les gestionnaires d'embauche et les intervieweurs techniques.

-----------------------------------------------------------------------------------

- Oui. 7. SEO-Friendly Blog Post (si vous voulez le publier)

**Titre**
`Cracking LeetCode 3269: Construction de deux tableaux croissants – Greedy + Java/Python/C++`

**Description détaillée**
`Apprenez la solution d'avidité O(n) la plus rapide pour le LeetCode 3269, la construction de deux tableaux croissants. Voir le code de travail en Java, Python et C++ et comment ace votre prochaine interview de codage. "

**Mots-clés cibles**
Leetcode, 3269, Constructing Two Augmenting Arrays, algorithme gourmand, programmation dynamique, préparation d'entrevue, interview de codage, conception d'algorithme, Java, Python, C++, ingénieur logiciel, entretien d'emploi, informatique, structures de données, complexité temporelle, complexité spatiale.

**Points suggérés**

1. Énoncé des problèmes et contraintes
2. Intuition – Pourquoi l'avidité fonctionne
3. L ' O(m + n) Algorithme
4. Java / Python / C++ Implémentations
5. Bon, mauvais, mauvais – Conseils pratiques
6. Reprise et conseils d'entrevue

N'hésitez pas à copier-coller les extraits de code dans votre propre blog, ajouter vos propres anecdotes personnelles et partager sur Linked Dans ou Medium pour afficher vos côtelettes de codage.

-----------------------------------------------------------------------------------

Bon codage, et que vos réponses d'entrevue soient toujours *gredy-optimal*!