---
titre: LeetCode 2152. Nombre minimum de lignes vers les points de couverture -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre minimum de lignes pour couvrir les points – LeetCode 2152
Aperçu du problème
Point de détail
- C'est quoi ?
Numéro de code
**Difficulté**
Titre Nombre minimum de lignes vers les points de couverture
Autres **Idée de base**= Trouvez le plus petit ensemble de lignes droites qui couvrent tous les points donnés sur un plan XY. Autres
**Constraints**=1 ≤ points de longueur ≤ 10=, `points[i] = [xi, yi]`, tous points uniques, `-100 ≤ xi, yi ≤ 100`. Autres

> **Objectif**: Retourner le nombre minimum de lignes droites nécessaires pour couvrir chaque point.

---

Pourquoi tu devrais maîtriser ce problème

* **Agrafe d'entretien** – De nombreuses entreprises technologiques demandent à ce que l'on teste l'optimisation combinatoire, la récursion, le bit-masking et les compétences DP.
* ** Polyvalence linguistique** – Les solutions existent dans **Java, Python et C++**. La démonstration de la compétence linguistique fait preuve de souplesse auprès des gestionnaires qui embauchent.
* **Profondeur algorithmique** – Vous apprendrez comment échanger contre la force brute contre la mémoisation, et comment gérer l'état avec des masques de bits.

---

Stratégies de haut niveau

L'approche La complexité Quand utiliser
C'est pas vrai.
**Récursifs + Forte-Force**
**FDS + Bitmask DP** Un échange équilibré pour "n" ≤ 10
**Mémoized Recursion**

> **Best Choice**: Pour `n ≤ 10`, le DFS + bitmask DP est efficace et facile à mettre en œuvre.
> **Worst-Case**: 10 points → 1024 états → parfaitement.

---

Mise en œuvre du code

Vous trouverez ci-dessous des solutions entièrement commentées dans **Java, Python et C++**.
Chaque extrait de code comprend :

* Un petit harnais d'essai (méthode `main` facultative / `si __name__ == "_main__":`).
* Effacer les signatures de fonction correspondant au style LeetCode.
* Commentaires en ligne expliquant chaque étape.

---

C'est pas vrai. Java (Bitmask + DFS)

"Java
Importation de java.util.*;

solution de classe {
// Masque cible : tous les points couverts
cible privée Masque;
// Carte de mémorisation : clé -> lignes minimales
Carte privée<entier,entier> mémo;

public int minimumLines(int[][] points) {
int n = points. longueur;
cible Masque = (1 << n) - 1;
mémo = nouveau HashMap<>();
retour dfs(0, points);
}

// DFS sur l'état bitmask
Int privé dfs(int masque, int[][] points) {
si (masque == cibleMasque) retourne 0; // tous les points couverts
si (memo.contientKey(mask)) retourne memo.get(mask);

// Trouver le premier point découvert
int premier = 0;
alors que [(masque & (1 << premier)] != 0) premier++;

int best = entier.MAX_VALUE;

// Essayez de tracer une ligne qui passe par 'premier' et un autre point
pour (int i = 0; i < points. longueur; i++) {
if (i == premier) (masque & (1 << i)) != 0) poursuivre;
int newMask = masque (= 1 << premier) (= 1 << i);

double pente = pente(points[premier], points[i]);

// Inclure tous les points sur cette ligne
pour (int j = 0; j < points.longueur; j++) {
i) continuer;
si ((masque & (1 << j))) != 0) poursuivre;
si (Double.compare(pente, pente(points[premier], points[j])) == 0)
newMask= (1 << j);
}
best = Math.min(best, 1 + dfs(newMask, points));
}

// Cas de bord: tous les points restants sont collinéaires avec 'premier '
Si (meilleur) entier. MAX_VALUE) = 1;

mémo.put(masque, meilleur);
le meilleur retour;
}

double pente privée(int[] a, int[] b) {
// Éviter la division par zéro : ligne verticale -> Infinité
si (a[0] == b[0]) retourner Double. L'INFINITÉ POSITIVE;
déclaration (double)(b[1] - a[1]) / (b[0] - a[0]);
}

// - Oui. Harnais d'essai...
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
[][] points1 = {{0,1},{2,3},{4,5},{4,3}};
[][] points2 = {{0,2},{-2,-2},{1,4}};
System.out.println("Exemple 1: " + sol.minimumLines(points1)); // 2
System.out.println("Exemple 2: " + sol.minimumLines(points2)); // 1
}
}
«» "

---

Python (Bitmask + DFS)

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def minimum Lignes (self, points: List[List[int]]) -> Int:
n = len(points)
cible = (1 << n) - 1

def pente(a, b):
si a[0] == b[0]:
retour flotteur('inf') # ligne verticale
retour (b[1] - a[1]) / (b[0] - a[0])

@lru_cache(Aucun)
def dfs(masque: int) -> Int:
si masque == cible:
retour 0
# Trouver le premier point découvert
premier = 0
alors que masque & (1 << premier):
premier += 1

meilleure = flotteur('inf')
pour i dans la plage(n):
i == premier ou masque & (1 << i):
poursuivre
nouveau_masque = masque
sl = pente(points[premier], points[i])

pour j dans la plage(n):
si j en (premier, i) ou masque & (1 << j):
poursuivre
si abs(sl - pente(points[premier], points[j]) < 1e-9:
nouveau_masque= (1 << j)

best = min(meilleur, 1 + dfs(nouvelle_masque))

retourner 1 s'il y a lieu.

retour dfs(0)

♪ - Oui. Harnais d'essai...
si __nom__ == "__main__" :
sol = Solution()
print(sol.minimumLines([[0,1],[2,3],[4,5],[4,3])) # 2
print(sol.minimumLignes([[0,2],[-2,-2],[1,4]) # 1
«» "

---

C++ (Bitmask + DFS)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minimumLignes(vecteur<vecteur<int>>& points) {
int n = points.size();
cible int = (1 << n) - 1;
vecteur<int> mémo(1 << n, -1);
retourner dfs(0, points, cible, mémo);
}

particulier:
double pente(vecteur Const<int>& a, vecteur Const<int>& b) {
si (a[0] == b[0]) retourne les limites numériques<double>::infini(); // verticale
retourner static_cast<double>(b[1] - a[1]) / (b[0] - a[0]);
}

int dfs(int mask, const vector<vector<int>>& pts, int cible, vector<int>& memory) {
si (masque == cible) retourne 0;
si (memo[masque] != -1) retourner le mémo[masque];

// Trouver le premier point découvert
int premier = 0;
pendant que (masque & (1 << premier)) ++premier;

int best = INT_MAX;
pour (int i = 0; i < pts.size(); ++i) {
si (i) le premier (masque et (1 < < i)) continue;
int newMask = masque (= 1 << premier) (= 1 << i);
double sl = pente(pts[first], pts[i]);

pour (int j = 0; j < pts.size(); ++j) {
si (j) le premier (J) le (J) le (Mask & (1 < < j)) continue;
si (abs(sl - pente(pts[first], pts[j])) < 1e-9)
newMask= (1 << j);
}
best = min(meilleur, 1 + dfs(newMask, pts, cible, mémo));
}

si (meilleur) INT_MAX = 1; // Tous les points restants collinéaires avec le premier
mémo[masque] = meilleur;
le meilleur retour;
}
};

// - Oui. Harnais d'essai...
Int main() {
Solution s;
vecteur<vecteur<int>> pts1 = {{0,1},{2,3},{4,5},{4,3}};
vecteur<vecteur<int>> pts2 = {{0,2},{-2,-2},{1,4}};
Cout << s.minimumLines(pts1) << endl; // 2
Cout << s.minimumLines(pts2) << endl; // 1
retour 0;
}
«» "

---

Décomposition

Étape Temps Espace
C'est pas vrai.
Autres ** Calcul de la pente**
**Les transitions de l'état DFS**
**Nombre d'États**
Total des opérations, < 1 ms en pratique

> **Pourquoi `n^3`?**
> 1. Choisissez le premier point découvert (`n`).
> 2. Combinez-le avec tout autre point découvert (`n`).
> 3. Scanner le reste pour recueillir des points collinéaires (`n`).

> **Espace** – Table de mémo de la taille "2^n" (1024 entiers).

---

Alternative : Force brute pure (récursive)

Si vous préférez une solution **=no-memo==** pour une lisibilité maximale, le squelette Python suivant fonctionne pour `n ≤ 10`.

'`python
def brute_force(points):
n = len(points)
meilleure = n # limite supérieure

def helper(non couvert):
non local meilleur
si non découvert: # tous les points couverts
retour 0
si len(non couvert) >= meilleure: # taille
le meilleur retour

premier = découvert[0]
pour la seconde dans découvert[1:]:
line_points = [p pour p dans découvert si on_same_line(first, second, p)]
new_uncovered = [p pour p dans découvert si p n'est pas dans line_points]
best = min(best, 1 + helper(new_uncovered))
le meilleur retour

aide(s) au retour
«» "

> **Drawback** – Pas de mémoisation, mais toujours < `10!` permutations.

---

Liste de contrôle sur l'approche à suivre (entrevue)

1. ** Représentation des États* *
* Utilisez un masque (`int mask`) – chaque bit représente si un point est déjà couvert.
2. **DSE récursif**
* Choisissez le premier point découvert, jumelez-le avec un autre point, construisez une ligne, et récursez sur le nouveau masque.
3. **Mémoisation / DP**
* Résultats de cache pour chaque masque (`lru_cache` dans Python, `unordered_map` ou vecteur dans Java/C++).
4. ** Manipulation en pente**
* Poignez les lignes verticales avec `Infinity` ou `numeric_limits<double>:Infinity()`.
* Utiliser une tolérance («1e‐9») pour comparer les pentes en point flottant.

5. **Juge**
* Tous les points restants collinéaires avec le premier point découvert → utiliser une ligne.

---

## Résumé Big-O (FDS + Bitmask)

Valeur métrique
C'est pas vrai.
**Heure** Autres
**Space**="O(2^n)" pour la mémorisation + pile de récursion (niveaux "=10"). Autres
Pour `n = 10` → 1024 états, 5 × 105 opérations – fonctionne en < 1 ms.

---

- Oui. Que montrer sur votre CV

Compétence Autres
-- -- -- -- -- ------------------ -- -- --
**Conception de l'algorithme**==LeetCode 2152 avec DFS avec bit-mask DP pour minimiser les lignes couvrant jusqu'à 10 points.== Autres
**Analyse de la complexité** Autres
**Multilolinguistique**==Les solutions mises en œuvre dans **Java, Python et C++**, qui montrent la fluidité des langues.== Autres
**Le succès de l'entrevue**=Ce problème a servi à établir un rôle chez XYZ Tech – la rétroaction de l'entrevue a loué ma stratégie claire d'encodage de l'État. Autres

> **Astuce**: Lorsque vous répondez aux questions de l'entrevue, commencez par la **transformation du problème** (bitmask, DP, récursion), puis expliquez les **état** et **transitions**. Montrez votre analyse de complexité pour prouver que vous avez compris les compromis.

---

Bonus – Début rapide du terrain de jeu

Si vous souhaitez expérimenter localement, copiez simplement l'extrait de langue choisi dans un fichier et exécutez-le. La section `main`/`if __name__ == "_main__:` imprimera les sorties attendues:

"""
$ solution de javac. java & & java Solution
Exemple 1: 2
Exemple 2: 1

$ solution python3. py
2
1

$ ./a.out
2
1
«» "

---

## -Take final- Loin

* Pour LeetCode 2152, **DFS + Bitmask DP** est le spot sucré : élégant, rapide et linguistique-agnostique.
* Maîtrisez les modèles **encodage de l'état** (masques de bits) et **mémousation** – ils sont utiles pour une grande variété de problèmes d'entrevue (p. ex., Couverture de l'état, subséquence maximale de l'état, etc.).
* Pratique expliquant l'algorithme, la complexité et les cas de bord – la communication claire est la moitié de la victoire d'entrevue!

Bonne chance, et le codage heureux! (en milliers de dollars)

---

> **Description de la Meta** – Code Solve Leet 2152 : Nombre minimum de lignes vers les points de couverture. Obtenez les solutions optimales Java, Python et C++, l'analyse algorithmique et les conseils d'entrevue pour aser votre prochain entretien d'emploi. (en milliers de dollars)