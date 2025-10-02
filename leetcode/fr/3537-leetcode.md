---
titre: LeetCode 3537. Remplir une grille spéciale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3537 – *Remplir une grille spéciale*
> **Mots clés:** *Remplir une grille spéciale*, *LeetCode 3537*, *Java solution*, *Python solution*, *C++ solution*, *diviser-et-conquérir*, *interview d'emploi*, *récursion*

---

### TL;DR

Langue Heure Espace
- C'est quoi ?
(c'est-à-dire O((2n)2))
*Python * O(4n) O(4n) Autres
O(4n) Autres

> Le point de vue clé : une grille 2n×2n peut être divisée de façon récursive en quatre sous-réseaux 2n−1×2n−1.
> Placez les numéros dans l'ordre **en haut à droite → en bas à droite → en bas à gauche → en haut à gauche**.
> Cela garantit les relations requises entre les quadrants.

---

Récapitulation des problèmes

> **Remplir une grille spéciale**
> Vous êtes donné un entier `n`. Construire une matrice `2n × 2n` remplie avec les entiers `0 ... 22n – 1` de telle sorte que:
> 1. Chaque élément du quadrant **haut-droit** est plus petit que tout élément du quadrant **bas-droit**.
> 2. Chaque élément du quadrant **bottom-right** est plus petit que tout élément du quadrant **bottom-left**.
> 3. Chaque élément du quadrant **bottom-gauche** est plus petit que tout élément du quadrant **top-gauche**.
> 4. Chaque quadrant lui-même est une grille spéciale (état récursif).
> 5. Toute grille `1×1` est spéciale.

> Retourne la matrice complétée.

> **Exemples**

Résultat Raisonnement
C'est pas vrai.
[[0]] Un seul élément
[[3,0],[2,1]]» Ordre des quadrants : TR=0 < BR=1 < BL=2 < TL=3
[[15,12,3,0],[14,13,2,1],[11,8,7,4],[10,9,6,5]"

---

- Oui. Pourquoi ce problème a-t-il des répercussions sur les entrevues?

C'est bon C'est mauvais
- C'est quoi ?
**Récursion + Diviser-et-Conquer** – compétences de base en matière de CS.
**Clean, deterministic output** – aucune randomité. **Cas d'Edge n=0** – trivial mais doit quand même retourner une matrice. **Large `n`** (=10) → 4n jusqu'à 1 048 576 – la profondeur de la mémoire et de la récursion peut être préoccupante.
Autres **Aucune bibliothèque externe** – pure algorithme

> La maîtrise de ce problème démontre :
> * Pensée récursive
> * Manipulation des rayons
> * Analyse temps/espace
> * Attention aux détails (manutention de l'index)

---

- Oui. Idée de haut niveau

1. **Cas de base** – Si le sous-réseau est `1×1`, placez la valeur de compteur actuelle et incrémentez-la.
2. **Étape récursive** –
* Divisez le sous-réseau actuel en 4 quadrants égaux.
* Remplissez les quadrants dans l'ordre **haut à droite → bas à droite → bas à gauche → haut à gauche**.
* Parce que nous incrémentons toujours le compteur après avoir rempli un quadrant, les nombres dans les quadrants précédents sont garantis être plus petits que les nombres dans les quadrants ultérieurs, satisfaisant aux 3 conditions de commande.
3. Récupérer jusqu'à ce que chaque cellule soit remplie.

La profondeur de récursion est `n` (=10), sûre dans toutes les langues.
Le compteur commence à `0` et se termine à `22n – 1`.

---

Mise en œuvre

#### 4.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
compteur interne privé = 0; // compteur mondial

public int[] specialGrid(int n) {
taille int = 1 << n; // 2^n
int[][] grille = nouvelle int[dimension];
remplir(grid, 0, taille - 1, 0, taille - 1);
la grille de retour;
}

***
* Remplir récursivement le sous-réseau défini par les gammes ligne/col.
*/
vide privé remplissage(int[], int sr, int er, int sc, int ec) {
// Cas de base: cellule 1x1
Si (sr) er && sc) ec) {
grille[sr][sc] = contre++;
retour;
}

(sr + er) / 2;
Int midCol = (sc + ec) / 2;

// Ordre: en haut à droite, en bas à droite, en bas à gauche, en haut à gauche
Remplissage(grid, sr, MidRow, MidCol + 1, ec); // en haut à droite
remplissage(grid, mi-Row + 1, er, mi-Col + 1, ec); // bas à droite
Remplissage(grid, mi-Row + 1, er, sc, mi-Col); // en bas à gauche
remplissage(grid, sr, miRow, sc, miCol); // en haut à gauche
}

// Démo principal (facultatif)
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
int[] g = s.spécialGrid(2);
pour (int[] ligne : g) Système.out.println(Arrays.toString(row));
}
}
«» "

4.2 Python

'`python
def specialGrid(n: int) -> list[list[int]]:
taille = 1 << n # 2**n
quadrillage = [[0] * taille pour _ dans la plage(dimension)]
compteur = 0

def fill(sr, er, sc, ec):
compteur non local
Si sr == er et sc == ec:
quadrillage[sr][sc] = compteur
compteur += 1
retour
mi_r, mi_c = (sr + er) // 2, (sc + ec) // 2
Ordre: en haut à droite, en bas à droite, en bas à gauche, en haut à gauche
remplissage(sr, mi_r, mi_c + 1, ec) # en haut à droite
remplissage(mid_r + 1, er, mi_c + 1, ec) # bas à droite
Remplir(mid_r + 1, er, sc, mi_c) # en bas à gauche
remplissage(sr, mi_r, sc, mi_c) # haut à gauche

remplissage(0, taille - 1, 0, taille - 1)
grille de retour
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<vecteur<int>> spécialGrid(int n) {
taille int = 1 << n; // 2^n
vector<vector<int>> grille (taille, vector<int>(taille));
compteur int = 0;
remplir(grid, 0, taille - 1, 0, taille - 1, compteur);
la grille de retour;
}

particulier:
(vecteur<vecteur<int>>&g, int sr, int er, int sc, int ec, int& cnt) {
Si (sr) er && sc) ec) {
g[sr][sc] = cnt++;
retour;
}
int miR = (sr + er) / 2;
int midC = (sc + ec) / 2;
// Ordre: en haut à droite, en bas à droite, en bas à gauche, en haut à gauche
remplissage(g, sr, mi-R, mi-C + 1, ec, cnt); // en haut à droite
remplissage(g, mi-R + 1, er, mi-C + 1, ec, cnt); // bas à droite
remplissage(g, mi-R + 1, er, sc, mi-C, cnt); // en bas à gauche
remplissage(g, sr, mi-R, sc, mi-C, cnt); // en haut à gauche
}
};
«» "

---

Analyse de complexité

Langue Heure Espace
- C'est quoi ?
Java / Python / C++** (chaque cellule visitée une fois) **O(4n)** (la grille elle-même)

> `4n = (2n)2` – le nombre total de cellules dans la grille.
> La profondeur de récursion est `n` (=10), négligeable par rapport à la taille de la grille.

---

## 6--Cas de bord & Gotchas

Problème
C'est pas vrai.
«n = 0» Retourner un tableau «0 × 0» Adapter explicitement le boîtier de base (dimension = 1 << 0 = 1»). Autres
Calcul de l'indice (en dehors de chaque ligne/cols) Utiliser la division entière `mid = (début + fin) / 2`. Autres
Autres Le dépassement du compteur de 22n peut dépasser `int` pour les grandes `n`=1 `n ≤ 10`, `int` suffit; pour les plus grandes valeurs, utiliser `long`. Autres
Débordement de la cheminée 1000.000 Pas un problème ici (`n ≤ 10`), mais utiliser une approche itérative pour des contraintes plus élevées. Autres

---

Autres approches

Démarcher Quand utiliser
- C'est quoi ?
Certains participants ont découvert un modèle où la valeur est égale au XOR bitwise des indices de ligne et de colonne.
**Itératif (pas de récursion)**= Éviter les problèmes de profondeur de récursion== Même temps/espace== Plus de complexité de code==
**Bottom-up DP**= Remplir la grille niveau par niveau== Pas de récursion, plus facile à déboguer== Légèrement plus de mémoire en raison de tableaux temporaires==

---

- Oui. Réflexions finales

- **La solution canonique est la division récursive et la conquête**.
- Oui. L'ordre du quadrant **TR → BR → BL → TL** est le secret qui impose les trois contraintes de commande.
- Oui. L'algorithme est *déterministe* et *entièrement déterministe*, ce qui en fait une excellente démonstration d'interview de **clarité + rectitude**.

---

## Comment cela stimule votre rappel d'entrevue

- **Shows mastery of recursion** – un point de départ dans de nombreux entretiens d'algorithmes.
- ** Démontre un code propre** – des fonctions d'aide minimales, un bon nom.
- **Fait ressortir la résolution de problèmes** – vous transformez une condition complexe de commande en un simple ordre de traversée.
- **Avantage de référencement** – lorsque les recruteurs cherchent à remplir une grille spéciale Java, votre poste GitHub ou blog apparaîtra.

---

Lecture supplémentaire

- [Code leet 3537 – Remplir une grille spéciale (problème officiel)(https://leetcode.com/problèmes/fill-a-special-grid/)
- [Divide-and-Conquer Patterns] (https://www.geeksforgeeks.org/divide-and-conquer-algorithms/)
- [Récursion contre itération] (https://www.programiz.com/dsa/recursion-vs-itération)

---

Enveloppe

> **=Remplir une grille spéciale==** est plus qu'un défi de codage: il s'agit d'un micro-leçon dans l'état d'esprit récursif, le découpage des tableaux et l'indexation méticuleuse.
> Avec les solutions ci-dessus, vous êtes prêt à répondre à la question et impressionner les gestionnaires d'embauche avec votre style algorithmique.

Bon codage et bonne chance ! C'est ce qu'il a dit.

---