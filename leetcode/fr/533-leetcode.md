---
titre: LeetCode 533. Unité Pixel II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
533. Lonely Pixel II – Solutions multilingues

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous les trois suivent la même stratégie spatiale O(m·n).

Texte
Entrée: image = [ [ "W", "B", "W", "B", "B", "W"],
"W", "B", "W", "B", "B", "W"],
"W", "B", "W", "B", "B", "W"],
"W", "W", "B", "W", "B", "W"]
cible = 3
Produit : 6
«» "

---

### Java

"Java
Importation de java.util.*;

classe publique LonelyPixelII {
public int trouver BlackPixel[[]] image, int cible) {
int m = image.longueur, n = image[0].longueur;
int[] rowCnt = nouvelle int[m];
int[] colCnt = nouvelle int[n];
Carte<String, entier> rowMap = nouveau HashMap<>();

// 1. Compte B dans chaque ligne, colonne et rang de magasin
pour (int i = 0; i < m; i++) {
StringBuilder sb = nouveau StringBuilder();
pour (int j = 0; j < n; j++) {
char ch = image[i][j];
sb.annexe(ch);
si (ch == 'B') {
ligne Cnt[i]++;
Le présent règlement est obligatoire dans tous ses éléments et directement applicable dans tout État membre.
}
}
Chaîne ligneStr = sb.toString();
si (rowCnt[i] == cible) { // seulement lignes avec la matière cible exacte
rowMap.put(rowStr, rowMap.getOrDefault(rowStr, 0) + 1);
}
}

// 2. Pour chaque colonne, si elle contient la cible B ET toutes les lignes avec B
// dans cette colonne ont le même motif, ajouter la cible pour répondre
Int ans = 0;
pour (int j = 0; j < n; j++) {
si (colCnt[j] != cible) continue; // colonne doit également avoir cible B

// collecte toutes les lignes qui ont un B dans la colonne j
Chaîne firstRow = null;
booléen même = vrai;
pour (int i = 0; i < m; i++) {
si (photo[i][j]] == 'B') {
Chaîne de lignesStr = nouvelle chaîne(image[i]); // ligne comme chaîne
si (premier rang) Ligne = ligne Échelle;
sinon si (!rowStr.equals(firstRow)) { même = faux; casse; }
}
}
si (même & & & firstRow != null) {
// toutes les lignes avec B dans cette colonne sont identiques
ans += cible; // chacun de ces B est un pixel solitaire
}
}
le retour des an;
}
}
«» "

> **Note**: `nouvelle chaîne(image[i])` fonctionne parce que `image[i]` est une «char».
> Pour les très grandes matrices, vous pourriez vouloir garder le «rowStr» de la première boucle au lieu de le reconstruire.

---

Python

'`python
Solution de classe:
def findBlackPixel(self, image: List[List[str]]], cible: int) -> Int:
m, n = len(photo), len(photo[0])
ligne_cnt = [0] * m
_cnt = [0] * n
ligne_map = {}

1. Comptez B et construisez des chaînes
pour i dans la plage (m):
ligne_str = "".join(photo[i])
cnt = ligne_str.count('B')
ligne_cnt[i] = cnt
si cnt == cible:
row_map[row_str] = row_map.get(row_str, 0) + 1

pour j, ch en énumération(photo[i]):
si ch == 'B':
_cnt[j] += 1

2. Colonnes de balayage
ans = 0
pour j dans la plage(n):
si col_cnt[j] != cible:
poursuivre

_première ligne = Aucune
même = Vrai
pour i dans la plage (m):
si photo[i][j]] «B»:
r = "".join(photo[i])
si le _premierrow n'est pas :
_première ligne = r
élif r != _première ligne :
Même = Faux
pause
if meme et first_row:
ans += cible
retour et
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
dans trouverBlackPixel(vecteur<vecteur<char>>& image, cible int) {
int m = picture.size(), n = picture[0].size();
vecteur<int> ligneCnt(m, 0), colCnt(n, 0);
unordered_map<string, int> rowMap;

// 1. Compte B en lignes et colonnes, rappelez-vous les chaînes de lignes
pour (int i = 0; i < m; ++i) {
ligne de chaîne Échelle;
la réserve (n);
pour (int j = 0; j < n; ++j) {
char ch = image[i][j];
rowStr.push_back(ch);
si (ch == 'B') {
++Cnt[i];
++colCnt[j];
}
}
si (cible derowCnt[i] ==)
++rowMap[rowStr];
}

// 2. Inspecter chaque colonne
Int ans = 0;
pour (int j = 0; j < n; ++j) {
si (colCnt[j] != cible) continue;

chaîne d'abord Ligne = ";
bool meme = true;
pour (int i = 0; i < m; ++i) {
si (photo[i][j]] == 'B') {
chaîne de caractères curRow(image[i].debut(), image[i].end());
si (firstRow.vide())
premier Ligne = curRow;
sinon si (curRow != firstRow) {
même = faux;
pause;
}
}
}
si (même & & & !firstRow.vide())
ans += cible; // chaque correspondance B est seul
}
le retour des an;
}
};
«» "

---

- Oui. 2. Article du blog
Code 533 – Lonely Pixel II : Les bons, les mauvais et les méchants*

> **Mots clés**: LeetCode, 533, Lonely Pixel II, codage d'entretien, Java, Python, C++, algorithme, ingénierie logicielle, entretien d'emploi, structures de données, complexité temporelle, complexité spatiale.

---

- Oui. 1. Aperçu du problème

LeetCode 533 *Lonely Pixel II* vous demande de compter ** pixels noirs solitaires** dans une image binaire.
Un pixel `'B'` à la position `(r, c)` est solitaire si:

1. La ligne `r` contient exactement **`cible`** pixels noirs.
2. La colonne `c` contient exactement **`cible`** pixels noirs.
3. Chaque ligne qui a un pixel noir dans la colonne `c` est **identique** à la ligne `r`.

L'image est une grille `m × n` (`1 ≤ m, n ≤ 200`).
La tâche est de retourner le nombre de pixels si solitaires.

---

- Oui. 2. Pourquoi c'est une grande question d'entrevue

- **Profondeur conceptuelle**: Teste la compréhension de la traversée du tableau 2-D, des cartes de hachage et de la manipulation des chaînes.
- **Réconciliations entre l'espace et le temps**: Il faut compter soigneusement pour rester dans le temps O(m·n) et dans l'espace O(m + n).
- ** Polyvalence linguistique** : Solvable en Java, Python, C++, ou toute langue qui supporte les cartes de hash et la gestion des chaînes.

---

- Oui. 3. La stratégie optimale

3.1 Idées de haut niveau

1. **Couvercle de pixels noirs par ligne et par colonne**.
*Les lignes* sont stockées sous forme de chaînes; si une ligne a exactement des pixels noirs `target`, nous conservons sa chaîne dans une carte de hachage.

2. ** Colonnes de valeur**:
Pour chaque colonne qui contient exactement des pixels noirs `target`, vérifiez que les lignes **all** ayant un `'B'` dans cette colonne sont **identiques**.
S'ils le sont, chaque `'B'` dans cette colonne est un pixel solitaire.

3. **Résultat**:
Chaque colonne valide apporte des pixels solitaires `cible` (un par ligne qui a un `'B'` dans cette colonne).

3.2 Pourquoi ça marche

- **État de rotation**: La carte garantit que seules les lignes avec des pixels noirs `cible` sont considérées.
- ** État de la colonne**: La boucle de colonnes garantit que les colonnes ont également des pixels noirs `target`.
- **État de l'identité faible** : En comparant les chaînes de lignes, nous confirmons que toutes les lignes partageant la colonne sont identiques.

L'algorithme fonctionne dans `O(m·n)` parce que nous traversons la matrice un nombre constant de fois, et les opérations de la carte sont `O(1)` en moyenne.

---

- Oui. 4. Les pièges communs

"Piège" Ce qui ne va pas
C'est-à-dire
**Using `photo[i].toString()`**= Retourne la référence du tableau, et non le contenu de la ligne. Convertir la ligne en une chaîne: `new String(photo[i])` ou `"".join(row)` dans Python. Autres
**Ignorer les lignes dupliquées**=Le fait de compter chaque ligne identique séparément mène au double comptage. Conservez une carte de fréquence des chaînes de lignes et multipliez seulement une fois par ligne. Autres
**Non valider le nombre de colonnes**. Passer les colonnes où `colCnt[j] != la cible. Autres
Utiliser l'identité de l'objet (`==`) dans Java/Python au lieu de l'égalité de contenu. Autres
**Les plus grandes chaînes intermédiaires**. Construire une fois pendant le premier passage; réutiliser dans la vérification de colonne. Autres

---

- Oui. 5. Les cas de bord et de gotchas

- **Toute photo blanche**: Aucune ligne ou colonne ne satisfait à la condition `target` → retourner 0.
- **Une seule ligne/colonne**: `m == 1` ou `n == 1` fonctionne encore; l'algorithme dégénère en un balayage 1-D.
- **Cible égale 1**: Seuls les "B" isolés peuvent être isolés; les colonnes avec plus d'un "B" doivent être jetées.
- ** Contraintes de mémoire** : Pour la matrice maximale de 200×200, la carte des chaînes est minuscule (< 4 kB), donc aucun problème.

---

- Oui. 6. Mise en œuvre dans trois langues

Voici des extraits propres et prêts à la production (Java, Python, C++).
Tous les trois suivent la stratégie optimale décrite ci-dessus.

- **Java**: Utilise `HashMap<String, Integer>` pour stocker le nombre de rangées.
- **Python**: Utilise `dict` et la concaténation des cordes.
- **C++**: Utilise `unordered_map<string, int>` et `std::string` conversions.

> **Astuce**: Lorsque vous soumettez sur LeetCode, assurez-vous que la signature de la fonction correspond à l'exigence de plate-forme (`findBlackPixel` en Java, `Solution.findBlackPixel` en Python, etc.).

---

- Oui. 7. Conseils de préparation à l'entrevue

1. **Déclarez votre plan**: Décrivez les deux passes et pourquoi chaque condition compte.
2. **Exposer la complexité**: temps «O(m·n)», espace auxiliaire «O(m + n).
3. **Vérification de l'état de santé de l'enfant**: Montrez que vous considérez des lignes simples, des colonnes, des matrices tout blanc.
4. **Trade-off**: Si la mémoire était plus serrée, vous pourriez éviter de stocker des chaînes de lignes en hachant les lignes.
5. **Testing**: Afficher quelques cas de test rapide, y compris les exemples de l'invite.

> **Pourquoi cela compte pour un emploi**: Les intervieweurs se soucient non seulement de la bonne réponse, mais de la façon dont vous *pensez*. Démontrer une solution claire et optimisée indique de solides compétences en résolution de problèmes qui se traduisent par l'ingénierie réelle.

---

- Oui. 8. A emporter

- **Lonely Pixel II** est un problème *medium* LeetCode qui regroupe plusieurs concepts clés CS: Tableau 2-D traversant, cartes de hachage, égalité des chaînes et comptage prudent.
- Oui. La solution optimale est simple une fois que vous séparez les vérifications de ligne, de colonne et d'identité.
- Être capable de l'implémenter proprement en Java, Python ou C++ met en valeur la polyvalence – un trait attrayant pour les rôles d'ingénierie logicielle.

---

La pensée finale

Si vous pouvez transformer une déclaration de problème confuse en un algorithme élégant et efficace, vous venez de gagner un billet d'or pour votre prochaine entrevue de codage. Bon codage, et bonne chance pour votre chasse au travail!