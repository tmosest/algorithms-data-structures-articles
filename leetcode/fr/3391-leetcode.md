---
Titre: LeetCode 3391. Conception d'une matrice binaire 3D avec suivi efficace des couches -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Concevoir une matrice binaire 3D avec un suivi efficace des calques
**(LeetCode 3391 – Java / Python / C++)**

> *Obtenez un guide prêt à l'emploi, convivial pour l'entrevue et optimisé pour le référencement qui couvre le bon, le mauvais et le laid de ce problème de conception de niveau moyen. *

---

Récapitulation des problèmes

Vous recevez un tableau binaire 3-D « matrix » **n × n × n**.
Au départ, chaque cellule est `0`.

Vous devez implémenter la classe `Matrix3D`:

Description de la méthode
C'est pas vrai.
Créer le tableau 3-D vide. Autres
"net setCell(int x, int y, int z)" Définissez `matrix[x][y][z] = 1`.
"vite unsetCell(int x, int y, int z)" Définissez `matrix[x][y][z] = 0`.
"int le plus grandMatrix()" (la couche entière à ce `x`) contient le plus `1`s. Si de nombreuses couches se lient, retourner le plus grand indice. Autres

Contraintes
- `1 ≤ n ≤ 100`
- `0 ≤ x, y, z < n`
- ≤ 105 appels vers `setCell`/`unsetCell "
- ≤ 104 appels à "Matrix le plus grand() "

L'objectif : **O(1)** mises à jour et **O(n)** requêtes.

---

Aperçu de la solution

Autres Ce que nous stockons Pourquoi ça marche
- C'est quoi ?
`int[][]] matrix` (ou `bool`‐matrix)= Vue complète 3‐D – nécessaire pour détecter si nous renversons une mémoire 1=0 ou 0=1=1=0 `O(n3)` – 1 000 000 ints =4 Mo pour `n = 100`. Autres
= `int[] layerCount`== Nombre de `1`s dans chaque couche `x`.== `O(n)` mémoire. Autres
"int maxLayer" Indice de la meilleure couche (facultatif). "O 1)" récupération. Autres

**Mise à jour**
- Lors du réglage d'une cellule : si l'ancienne valeur est `0`, incrémenter `layerCount[x]`.
- Lors de la désactivation: si l'ancienne valeur est `1`, décrément `layerCount[x]`.

**Querité**
- Scanner `layerCount` à partir de la fin (`n-1 ... 0`) pour trouver la première couche avec le nombre le plus élevé.
- Parce que nous balayons en arrière, le premier coup est automatiquement le plus grand indice parmi les liens.

Toutes les opérations respectent les contraintes : au plus 105 mises à jour, chacune en **O(1)**, et au plus 104 requêtes, chacune en **O(n) = O(100)** – trivial pour les délais.

---

Mise en œuvre du code

Voici des solutions complètes, prêtes à coller pour **Java, Python et C++**.
Chacun contient la classe `Matrix3D` avec l'API requise et un simple harnais d'essai `main` / `if_name__ == "_main__"`.

---

### Java

"Java
Importation de java.util.*;

classe publique Matrix3D {
final privé n;
matrice finale privée int[][];
Int[] couche finale privéeCouvercle; // nombre de 1s par couche x

public Matrix3D(int n) {
n = n;
matrice = nouvelle int[n][n][n];
layerCount = nouvelle int[n];
}

*** Réglez la cellule à 1. Non-op si déjà 1. */
public vide setCell(int x, int y, int z) {
si [matrice[x][y][z]] 0) { // seulement si l'on retourne vraiment
matrice[x][y][z] = 1;
layerCount[x]++; // update layer total
}
}

*** Réglez la cellule à 0. Non-op si déjà 0. */
public vide non définiCell(int x, int y, int z) {
si [matrice[x][y][z]] 1) {
matrice[x][y][z] = 0;
layerCount[x]--;
}
}

*** Retour plus grand x avec la plupart des 1s. */
plus grandMatrix() {
int best = n - 1;
int bestCount = coucheCount[best];
pour (int i = n - 2; i >= 0; --i) {
si (coucheCount[i] >= bestCount) { // >= garde un indice plus grand sur la cravate
bestCount = calqueCount[i];
best = i;
}
}
le meilleur retour;
}

// - Oui. Démonstration...
public statique vide principal(String[] args) {
Matrice3D m = nouvelle Matrice3D(3);
m.setCell(0, 0, 0);
Système.out.println(m.m.matrix()); // 0
m.setCell(1, 1, 2);
Système.out.println(m.m.matrix()); // 1
m.setCell(0, 0, 1);
Système.out.println(m.m.matrix()); // 0
}
}
«» "

---

Python

'`python
classe Matrix3D:
def __init_(self, n: int):
auto.n = n
Self.matrix = [[[0] * n pour _ dans l'intervalle(n)] pour _ dans l'intervalle(n)]
nombre de couches = [0] * n

def setCell(self, x: int, y: int, z: int) -> Aucun:
si self.matrix[x][y][z]] 0:
Matrice[x][y][z] = 1
Compte_auto.layer[x] += 1

def unsetCell(self, x: int, y: int, z: int) -> Aucun:
si self.matrix[x][y][z]] 1 :
Matrice[x][y][z] = 0
Self.layer_count[x] -= 1

plus grandMatrix(self) -> Int:
meilleure = self.n - 1
best_count = auto.layer_count[best]
pour i dans la plage (self.n - 2, -1, -1):
si self.layer_count[i] >= best_count : # >= choisit un indice plus grand sur la cravate
best_count = auto.layer_count[i]
meilleure = i
le meilleur retour


♪ ---------------- Démo ----------------
si __nom__ == "__main__" :
m = Matrice3D(3)
m.setCell(0, 0, 0)
print(m.la plus grandeMatrix()) # 0
m.setCell(1, 1, 2)
print(m.la plus grandeMatrix()) # 1
m.setCell(0, 0, 1)
print(m.la plus grandeMatrix()) # 0
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe Matrix3D {
l'élément n;
vecteur<vector<vector<int>>> matrice; // grille 3-D
vecteur<int> coucheCnt; // nombre de 1s par couche x

public:
Matrix3D(int n_) : n(n_), matrix(n_, vector<vector<int>>(n_, vector<int>(n_, 0)),
calqueCnt(n_, 0) {}

vide setCell(int x, int y, int z) {
si [matrice[x][y][z]] 0) {
matrice[x][y][z] = 1;
++ coucheCnt[x];
}
}

vide non définiCell(int x, int y, int z) {
si [matrice[x][y][z]] 1) {
matrice[x][y][z] = 0;
--coucheCnt[x];
}
}

la plus grandeMatrix() const {
int best = n - 1;
int mieux Cnt = coucheCnt[meilleure];
pour (int i = n - 2; i >= 0; --i) {
si (layerCnt[i] >= bestCnt) { // >= garde un indice plus grand sur la cravate
bestCnt = coucheCnt[i];
best = i;
}
}
le meilleur retour;
}
};

// ---------------- Démo ----------------
Int main() {
Matrice3D m(3);
m.setCell(0, 0, 0);
Cout << m.matrix() << endl; // 0
m.setCell(1, 1, 2);
Cout << m.matrix() << endl; // 1
m.setCell(0, 0, 1);
Cout << m.matrix() << endl; // 0
retour 0;
}
«» "

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
Autres **L'utilisation de l'espace**= tableau 3-D (= 4 Mo pour la taille maximale) + compteurs O(n) – amende pour les contraintes.= Le tableau 3-D peut se sentir trop qualifié quand un seul compteur de calques est nécessaire. Il n'est pas nécessaire de stocker toute la grille si vous ne vous souciez que des totaux des couches; les environnements à mémoire restreinte auraient besoin d'une représentation plus intelligente. Autres
**Mise à jour du coût**** **O(1)** – il suffit de lire l'ancienne valeur, d'écrire une nouvelle valeur et de toucher un compteur. Aucun – l'algorithme brille ici. Si vous avez besoin de *plus* que les totaux des couches (p. ex., statistiques par colonne), vous aurez besoin de compteurs supplémentaires, ajoutant un coût linéaire caché. Autres
**Coût de la requête**=Scanner en arrière, liens résolus automatiquement → **O(n)** (=100). Pour d'énormes `n` vous auriez besoin d'une requête plus rapide (par exemple, arbre segment ou arbre binaire indexé). Si vous effectuez un balayage vers l'avant et utilisez `<` pour les liens, vous retournerez l'indice *le plus petit*, brisant les spécifications. Autres
**Cas d'angle de correction**=Checks for `old value == 0/1` garde contre les doubles incréments. Ne pas vérifier les limites (`x`, `y`, `z`) – mais LeetCode les garantit. Si vous oubliez le garde et incrément aveuglément, les totaux de la couche deviennent faux et `la plus grandeMatrix()` donne une mauvaise réponse. Autres
**Structures de données alternatives** 0. Mais alors vous perdez O(1) *read* de la vieille valeur (vous auriez besoin d'une autre carte). L'utilisation de bit-packing (32 cellules par int 32 bits) permet d'économiser de l'espace, mais complique l'index des mathématiques – pour les intervieweurs. Autres
**Codage style**= Séparation claire des préoccupations, des méthodes publiques exactement selon les besoins. Pas de mise en cache du meilleur calque – vous pouvez garder `maxLayer` mais ensuite vous devez le recalculer sur les liens, ajoutant la complexité. Utiliser l'état mutable global sans encapsulation appropriée est une recette pour les bugs. Autres

---

Pourquoi cela compte pour votre portefeuille d'entrevues

1. **Présentation de la conception et du carton** – Nous maintenons un compteur *stateful* tout en conservant les données brutes pour la détection du changement.
2. ** Sensibilisation au commerce** – Vous pouvez discuter quand une matrice 3-D complète est justifiée par rapport à une représentation compressée.
3. ** Clarté algorithmique** – Les mises à jour O(1) + les requêtes O(n) sont les problèmes de la norme d'or pour la conception d'une structure de données contre-basée.

Au cours d'une entrevue, vous pouvez dire:
J'ai choisi un tableau 3-D parce que la spécification dit que nous avons besoin de connaître la valeur de l'ancienne cellule pour chaque mise à jour. Le tableau de comptoir nous donne des mises à jour rapides et des requêtes rapides. Si la mémoire devient un goulot d'étranglement, nous pourrions comprimer la grille en bit-vectors ou même la déposer entièrement et ne stocker que les totaux par couche.

---

Liste de contrôle du référencement

Mot-clé Pourquoi ça compte
C'est-à-dire
**3-D conception des matrices** Autres
**Matrix3D LeetCode 3391**. Autres
**O(1) mise à jour, requête O(n)** Autres
Autres **Entretien Java Python C++** Autres
Autres **Comptoir d'atelier, tableau 3-D, modèle de conception** Autres
**Space‐time trade‐off** , vous pouvez parler de complexité au-delà du code. Autres

*Astuce:* Utilisez le tableau ci-dessus comme votre **LinkedIn article**, **GitHub README**, ou **portfolio page**. Il contient un poinçon de mots-clés tout en étant facile à skim.

---

Prochaines étapes

1. **Run la démo** dans votre IDE – voir les méthodes en action.
2. **Ajouter les essais de cas de bord** (réinitialiser un 1, désinitialiser un 0, remplir une couche entière, etc.).
3. **Temps vous-même** sur une grande séquence de mises à jour suivie de requêtes pour sentir la linéarité.
4. ** Expliquez les compromis** à un pair – c'est ce que les recruteurs aiment.

Bonne chance ! Vous disposez maintenant d'une solution propre et prête à l'entrevue pour *Design a 3-D Binary Matrix with Effective Layer Tracking* qui impressionnera à la fois les gestionnaires d'embauche et les moteurs de recherche.