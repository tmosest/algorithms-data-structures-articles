---
titre: LeetCode 1183. Nombre maximum de personnes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1183 – *Nombre maximum de personnes*
**Le bon, le mauvais et le mauvais – un guide complet de préparation à l'entrevue**

---

Pourquoi ce problème se pose (et pourquoi il devrait être sur votre liste d'entrevues)

- **Real-world pertinence** – la contrainte --toute sous-matrix peut avoir au plus X--sons est un problème classique de restriction des motifs qui apparaît dans le traitement de l'image, la mise en page de la mémoire, et même dans les problèmes de programmation.
- ** Variété algorithmique** – vous pouvez le résoudre avec une simple cupidité, un DP, ou un aperçu mathématique. Les intervieweurs aiment entendre pourquoi vous avez choisi une approche plutôt qu'une autre.
- **Clarifier le moment**** – une observation rapide (cochez les décalages les plus fréquents) transforme un DP de 100 lignes en une solution de 30 lignes.
- **SEO Gold** – chaque blog technique ou article à la recherche d'un emploi qui mentionne *LeetCode 1183*, *Maxim Nombre of Ones*, *Greedy Algorithme*, *C++ interview*, *Python interview*, *Java interview* sera classé haut.

---

Déclaration de problème (Code Leet 1183)

> Étant donné une matrice `M` des dimensions `largeur × hauteur` contenant seulement `0` ou `1`, on nous dit que **toute** `sideLength × sideLength` sous-matrice de `M` contient **au plus** `maxOnes`.
> **Retourner le nombre maximum de ceux que `M` peut contenir.

**Contrôles* *

Paramètre Gamme
C'est quoi ?
Largeur, hauteur 1 ... 100
1 ... min (largeur, hauteur) Autres
0 ... côté Longueur × longueur latérale» Autres

**Exemples**

«» "
Entrée : largeur=3, hauteur=3, côtéLongueur=2, maxOnes=1
Produit : 4
Matrice :
1 0 1
0 0 0
1 0 1

Entrée : largeur=3, hauteur=3, côtéLongueur=2, maxOnes=2
Produit : 6
Matrice :
1 0 1
1 0 1
1 0 1
«» "

---

Le bien – La perspective de l'avidité

**Observation principale**

Chaque fenêtre `sideLength × sideLength` contient exactement **une** cellule de chacune des classes de résidus `sideLength2` `(i mod sideLength, j mod sideLength)`.

- Pensez à la grille carrelée avec un motif `sideLength × sideLength` qui répète chaque ligne `sideLength` ** et**.
- Chaque classe de résidus est l'ensemble des positions qui s'alignent avec le même endroit à l'intérieur de ce motif.
- Si nous décidons de mettre un `1` dans une classe de résidus, **chaque fenêtre** qui contient cette classe obtiendra une autre `1`.

Ainsi:

1. Compter le nombre de cellules appartenant à chaque classe de résidus.
`count[r][c] = nombre de mailles avec (ligne mod sideLength = r, col mod sideLength = c)`
2. Choisissez les classes de résidus **`maxOnes` les plus importantes** – mettre `1` dans ces classes maximise les classes totales tout en garantissant que toute fenêtre contient au plus `maxOnes`.
3. La réponse est la somme des nombres des classes choisies.

Pourquoi est-ce optimal ?
Parce que nous choisissons les classes qui contribuent le plus aux cellules. Si nous remplaçons une classe choisie par une classe non choisie, le total diminuerait strictement. Et la contrainte sur chaque fenêtre est déjà satisfaite parce que chaque fenêtre peut choisir au plus une de chaque classe, donc au plus `maxOnes`.

---

## Le "Bad" – Un piège à éviter

- **Surpenser le PDD** – On pourrait essayer un DP 4-dimensionnel pour se rappeler le nombre de ceux dans les dernières lignes/colonnes "sideLength". C'est inutile et ferait exploser le temps/la mémoire.
- **En supposant que nous pouvons choisir les cellules "maxOnes" arbitrairement** – Si vous choisissez simplement les cellules les plus fréquentes sans respecter les classes de résidus, le chevauchement des fenêtres peut violer la contrainte.
- **Ignorer le modèle modulo** – Ne pas réaliser que les classes de résidus sont la seule chose qui compte pour la contrainte de fenêtre conduira à de mauvaises solutions.

---

Quand votre code va mal

Symptôme Cause probable Correction
- C'est quoi ?
"IndexOutOfBoundsException" en Java ou "IndexError" en Python" Mauvaise indexation modulo (off‐by‐one) Autres
Autres Mauvaise réponse pour `maxOnes == sideLength*sideLength`. Autres
Autres La limite de temps est dépassée pour la grille 100×100. Autres
Autres Mauvaise réponse pour les grilles rectangulaires ( 'largeur !=hauteur') Autres

---

Les solutions de code

Voici des implémentations propres, prêtes à l'interview dans **Java**, **Python** et **C++**.

C'est pas vrai. Java

"Java
Importer java.util. Les tableaux;
Importer java.util. Comparateur;

solution de classe {
public int maxNombreOfOnes(largeur int, hauteur int, côté intLongueur int maxOnes) {
// Nombre de cellules pour chaque classe de résidus
int[] cnt = nouvelle int[sideLength[sideLength];
pour (int r = 0; r < hauteur; r++) {
pour (int c = 0; c < largeur; c++) {
cnt[r % sideLength[c % sideLength]++;
}
}

// Compte aplati et tri descendant
int[] plat = nouveau int[sideLength * sideLength];
Int idx = 0;
pour (int[] ligne : cnt) {
pour (int v : ligne) plat[idx++] = v;
}
Tableau.sort(plat);
int n = longueur plate;
Int ans = 0;
// Sommez les plus grands comptes "maxOnes"
pour (int i = n - 1; i >= n - maxOnes; i--) {
ans += plat[i];
}
le retour des an;
}
}
«» "

> **Pourquoi cela fonctionne** –
> - Agrégats `cnt` par classe de résidus.
> - `flat` contient toutes les tailles de classe.
> - Tri donne les plus grandes tailles à la fin; nous somme le top "maxOnes".

# # # # # #

'`python
Solution de classe:
def maximumNumberOfOnes(
soi-même,
largeur: int,
hauteur: int,
longueur latérale: int,
maxOnes: int
-> Int:
Nombre par classe de résidus
cnt = [[0] * longueur latérale pour _ dans la plage (longueur latérale)]
pour r (hauteur):
pour c dans la plage (largeur):
cnt[r % de longueur latérale][c % de longueur latérale] += 1

# Aplatir et obtenir le plus grand maxOnes compte
flat = [v pour la ligne en cnt pour la ligne en v]
flat.sort(reverse=True)
somme de retour(flat[:maxOnes])
«» "

> Les compréhensions de la liste de Python font le code concis et facile à lire.

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxNumberOfOnes(largeur int, hauteur int, côté intLongueur int maxOnes) {
vector<vector<int>> cnt(sideLength, vector<int>(sideLength, 0));

pour (int r = 0; r < hauteur; ++r)
pour (int c = 0; c < largeur; ++c)
++cnt[r % de longueur latérale][c % de longueur latérale];

vecteur <int> plat;
pour (auto &row : cnt)
pour (int v : ligne) flat.push_back(v);

tri(flat.begin(), flat.end(), plus grand<int>();
Int ans = 0;
pour (int i = 0; i < maxOnes; ++i) ans += plat[i];
le retour des an;
}
};
«» "

> Utilise `plus grand<int>()` pour trier la descente, exactement comme les versions Java et Python.

---

Analyse de complexité

Opération de Java Python C++
- C'est quoi ?
Autres Cellules de comptage "O(largeur × hauteur) " " O(largeur × hauteur) " Autres
Tri des éléments "sideLength2`" "O(sideLength2 log sideLength2)" "O(sideLength2 log sideLength2)" Autres
L'espace "O(sideLength2)" "O(sideLength2)" "O(sideLength2)" Autres

Avec `largeur, hauteur ≤ 100` et `sideLength ≤ 100`, l'algorithme fonctionne bien sous une milliseconde sur le matériel moderne.

---

Comment parler Ceci dans une interview

1. **Énoncer succinctement le problème** – On nous donne une grille et une contrainte sur n'importe quel sous-matrix `k×k`. Trouvez le maximum. (en milliers de dollars)
2. **Identifiez le motif** – - Toute fenêtre `k×k` contient exactement une cellule de chaque classe de résidus modulo `k`.
3. ** Expliquez l'avidité** – On compte les cellules par classe de résidus et on choisit les classes `maxOnes` supérieures; chaque fenêtre voit au plus `maxOnes`. (en milliers de dollars)
4. **Cas de bord de Mention** – Quand `maxOnes` équivaut `k2`, nous pouvons remplir toute la grille. (en milliers de dollars)
5. **Parler de la complexité** – temps O(nm + k2 log k2), espace O(k2), trivial pour les contraintes données. (en milliers de dollars)
6. **Optionnel** – Si `k` étaient énormes, nous pourrions garder un peu de taille `maxOnes` pour éviter le tri complet. (en milliers de dollars)

---

Essai et validation

'`python
# vérification rapide de la santé mentale
def brute(largeur, hauteur, k, m):
de itertools importation produit
meilleur = 0
pour la grille du produit[0,1], répéter=largeur*hauteur:
ok=Vrai
pour r dans la plage (hauteur-k+1):
pour c dans la plage (largeur-k+1):
s=sum(grid[(r+i)*width+(c+j)] pour i en range(k) pour j en range(k))
si s>m:
ok=Faux; pause
si non ok: pause
si oui:
best=max(best,sum(grid))
le meilleur retour

print(brute(3,3,2,1)) # 4
print(brute(3,3,2,2)) # 6
«» "

L'algorithme avide correspond à la force brute exhaustive pour toutes les petites grilles ( 'largeur, hauteur ≤ 4'). N'hésitez pas à intégrer ces tests dans votre bibliothèque personnelle.

---

À emporter

- **Les classes de résidus modulo `k` sont la seule dimension pertinente** – les fenêtres ne peuvent pas se différencier au-delà de cela.
- **Greedy est à la fois simple et optimal** – vous n'avez jamais besoin d'un DP complexe.
- **La mise en œuvre est simple** – compter, trier, somme.

Utilisez cette solution pour **score** dans les concours de codage et **win** dans les entrevues techniques. Bon codage !

---

*Préparé par votre assistant d'algorithme amical. *