---
titre: LeetCode 259. 3Sum plus petit -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3Sum plus petit – Le bon, le mauvais, et le mauvais
*(Leetcode 259 – Interview-Ready, Java/Python/C++ Solution + SEO – Friendly Blog*

> ** Keyword Focus**: `3Sum Smaller`, `Leetcode 259`, `deux pointeurs`, `O(n2)` algorithme, `Java`, `Python`, `C++`, `interview d'emploi`, `algorithme design`.

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Constraints & Edge Cases](#contraintes--edge-cases)
3. [Stratégie de résolution] (#solution-stratégie)
- 3.1 Technique à deux points
- 3.2 Pourquoi trier les aides
4. [Mise en œuvre de Java] (#Mise en œuvre de Java)
5. [Python implementation] (#python implementation)
6. [Mise en œuvre C++](#c++-mise en œuvre)
7. [Complexité temporelle et spatiale] (#temps--complexité spatiale)
8. [Le bon, le mauvais, le mauvais] (#le bon, le mauvais)
9. [Conclusion et prochaines étapes] (#conclusion - prochaines étapes)

---

## Aperçu du problème <a name="problem-overview"></a>

**Codage de sortie 259 – 3Sum Smaller* *

> Avec un tableau entier `nums` et un entier `cible`, retournez le nombre de triplets `(i, j, k)` avec `0 ≤ i < j < k < n` de sorte que `nums[i] + nums[j] + nums[k] < cible`.

Exemple Entrée Sortie Explication
C'est pas vrai.
[2,0,3], cible Triplettes: `[2,0,1]`, `[2,0,3]`
"[]", cible Pas de triplets
"[0]", cible Pas de triplets

---

## Contraintes et cas de bord <un nom="contraintes-cas de bord"></a>

Paramètre Gamme
C'est quoi ?
"nums.longueur" "0 ... 3500" Autres
"Nums[i]" "-100 ... 100" Autres
Cible 100 Autres

**Décisions de la Cour* *

- Vider un tableau ou un tableau avec moins de 3 éléments → retourner `0`.
- Tous les numéros sont les mêmes.
- Nombres négatifs et positifs entrelacés.

---

## Stratégie de solution <a name="solution-strategy"></a>

L'approche classique consiste à trier le tableau d'abord, puis à utiliser un balayage à deux points pour chaque premier élément fixe.

3.1 Technique à deux points

Pour chaque indice `i` (le premier élément du triplet), nous devons compter les paires `(gauche, droite)` de telle sorte que
`nums[i] + nums[left] + nums[right] < cible` avec `left = i + 1`, `right = n - 1`.

Parce que le tableau est trié :

- Si `nums[i] + nums[left] + nums[right] < cible`, *chaque élément entre `left` et `right` comblera également l'inégalité pour cette `i` et `left` parce que les nombres n'augmentent que lorsque nous déplaçons `à droite` vers la gauche.
Par conséquent, nous pouvons ajouter `à droite - à gauche` à la réponse et incrément `à gauche`.
- Si la somme est `≥ cible`, nous avons besoin d'une somme plus petite → decrement `right`.

Cela donne un algorithme `O(n2)` avec un espace supplémentaire `O(1)`.

3.2 Pourquoi trier les aides

Le tri transforme le problème de *recherche de toutes les paires de qualifications* en *analyse linéaire* par `i`.
Sans trier, il faudrait vérifier explicitement toutes les paires `O(n2)`, ce qui mène au temps `O(n3)`.

---

- Oui. Mise en œuvre Java <a name="java-implémentation"></a>

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public int troisSumSmaller(int[] nums, int cible) {
si (nombres) null (longueur < 3) retourner 0;

Tableaux.sort(nums);
int n = longueur nominale, nombre = 0;

pour (int i = 0; i < n - 2; i++) {
int gauche = i + 1, droite = n - 1;
pendant que (à gauche < à droite) {
somme int = nombres[i] + nombres[gauche] + nombres[droite];
si (somme < cible) {
// Tous les éléments entre travail de gauche et travail de droite
nombre += droite - gauche;
gauche++;
} autre {
droit...
}
}
}
le nombre de retours;
}
}
«» "

**Explication**

- `Arrays.sort(nums)` – `O(n log n) "
- Boucle extérieure – "O(n)"
- Balayage intérieur à deux points – 'O(n)` par itération → total 'O(n2)`

---

## Python Implementation <a name="python-implementation"></a>

'`python
Solution de classe:
Trois SumSmaller(self, nombres: list[int], cible: int) -> Int:
s'il n'y a pas de nombres ou de nombres < 3:
retour 0

nombres.sort()
n, nombre = len(nums), 0

pour i dans la plage (n - 2):
gauche, droite = i + 1, n - 1
à gauche < à droite:
curr_sum = nombres[i] + nombres[gauche] + nombres[droite]
si curr_sum < cible:
count += droite - gauche # tous les indices entre travail gauche et travail droit
gauche += 1
Sinon:
droite -= 1
Nombre de retours
«» "

Python"s `sort()` est `O(n log n)`. La logique reflète exactement la version Java.

---

## C++ Mise en œuvre <a name="c++-implémentation"></a>

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int troisSumSmaller(std::vector<int>& nums, int cible) {
si (nums.size() < 3) retourner 0;
à:sort(nums.begin(), nums.end();
int n = nombres.size(), nombre = 0;

pour (int i = 0; i < n - 2; ++i) {
int gauche = i + 1, droite = n - 1;
pendant que (à gauche < à droite) {
somme int = nombres[i] + nombres[gauche] + nombres[droite];
si (somme < cible) {
nombre += droite - gauche;
+ + gauche;
} autre {
--droite;
}
}
}
le nombre de retours;
}
};
«» "

C++ suit le même modèle ; `std::sort` gère l'étape de tri.

---

## Complexité temporelle et spatiale <a name="time--space-complexity"></a>

Complexité
C'est pas vrai.
**Heure**="O(n log n)` (triage) + `O(n2)` ( boucle à deux points) → global `O(n2)` Autres
**Space**= `O(1)` auxiliaire (le tri en place pour Java/C++; la liste de Python est en place)==

Pour la taille maximale d'entrée (`n = 3500`), `O(n2)` 12 millions d'itérations – facilement gérables dans les environnements modernes.

---

## Le bon, le mauvais, l'horrible <un nom, le bon, le mauvais, le mauvais"></a>

Aspect du bien
- C'est quoi ?
**Concept**= Utilisation élégante du tri + deux pointeurs. Il faut trier → étape supplémentaire. Le tri pourrait être exagéré pour de très petits tableaux; encore très bien. Autres
**Mise en œuvre**= Clean, O(1) mémoire supplémentaire.= Doit gérer le débordement `int` dans des langues comme C++ si les entrées étaient plus grandes. Aucun—`int` est sûr avec des contraintes données. Autres
**Solution rapide « O(n2) », acceptée dans 99 % des tests LeetCode. Pour d'énormes `n`, `O(n2)` devient lourd (pas le cas ici). Aucune, mais si les contraintes étaient plus strictes (`n ≤ 105`), cette approche échoue. Autres
**Readability**. Certains pourraient mal interpréter la logique " droite - gauche " ; ajouter des commentaires. Autres
Autres **Manipulation d'un cas** → retourne Aucun.

---

## Conclusion et prochaines étapes <a name="conclusion--next-steps"></a>

*3Sum Smaller* est un problème d'entrevue classique qui teste votre capacité à combiner tri avec un balayage à deux points. La solution `O(n2)` est simple mais puissante et vous marquera des points dans toute entrevue de codage.

**Quoi d'entrainer ensuite? **

1. **Problèmes liés au code leet* *
- 16. 3Sum
5. Subchaîne palindromique la plus longue (approche à deux points)
- 15. 3Sum le plus proche

2. **Des motifs algorithmiques**
- Deux points sur les tableaux triés
- Fenêtre coulissante
- Variantes de recherche binaire

3. ** Entrevues de codage**
- Entretiens sur des plateformes comme Pramp, InterviewBit ou LeetCode Discut.
- Passez en revue le cadre « Good, Bad, Ugly » pour expliquer vos solutions.

**SEO Bonus** – Utilisez ce billet de blog comme une pièce de portefeuille. Il démontre non seulement votre compétence en codage, mais aussi votre capacité à expliquer clairement les idées complexes, un trait critique pour les ingénieurs en logiciels.

Bonne chance ! C'est ce qu'il a dit.

---

**Références**

- LeetCode 259: https://leetcode.com/problèmes/3sum-smaller/
- Technique à deux points: https://leetcode.com/discuss/102391/trois-sum-smaller-o-n2-solution-in-java
- Notions de base : https://en.wikipedia.org/wiki/Sorting_algorithm

---

*Sentez libre de déposer un commentaire ci-dessous si vous souhaitez discuter d'autres optimisations ou des stratégies de prép d'entrevue! *