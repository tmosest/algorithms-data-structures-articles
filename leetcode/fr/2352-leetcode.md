---
titre: LeetCode 2352. Paires égales de lignes et de colonnes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2352 – Paires égales de lignes et de colonnes
**Cible Public:** Candidats de l'avant, de l'arrière, de la structure des données et des algorithmes
**Langues couvertes :** C++
**Objectif:** Obtenir une solution solide prête à l'entrevue, comprendre *bon*, *mauvais*, *meilleure* patrons, et écrire un article de style blog qui est convivial pour le référencement.

---

Récapitulation des problèmes

> **Grid** – une matrice entière 0-indexée *n × n* («1 ≤ n ≤ 200»).
> Comptez combien de paires `(ri, cj)` existent de telle sorte que tout le *row* `ri` correspond à l'élément *colonne* `cj` par élément.
>
> **Exemple**
> `` "
> grille = [3,1,2],
> [1,4,4,5],
> [2,4,2],
> [2,4,2]]
> Produit : 3
> `` "
>
> **Constraints**
> - `grid[i][j]` correspond à un entier de 32 bits
> - Délai: ~1 sec

---

Intuition

Une ligne et une colonne sont égales si la séquence ** des nombres** est identique.
Par conséquent, chaque ligne peut être considérée comme une *chaîne* (ou une tuple) et chaque colonne comme une autre chaîne.
Si nous pouvons **regarder** une chaîne de colonnes dans l'ensemble des chaînes de lignes, nous avons une correspondance.
La clé est de le faire en **O(n2)** temps au lieu d'un **O(n3)** naïf.

---

Aperçu de la solution

1. **Encoder les lignes** dans une représentation hashable (chaîne, tuple, vecteur).
2. Conservez chaque ligne codée dans une carte *hash* avec sa fréquence.
3. Itérer à travers chaque colonne, encoder de la même manière, et **lookup** la carte.
4. Ajouter la fréquence récupérée à la réponse.

> **Pourquoi ça marche ? * *
> - Chaque ligne est traitée une fois → `O(n2)`
> - Chaque colonne est traitée une fois → `O(n2) "
> - Les opérations cartographiques sont moyennes `O(1)` → global `O(n2)`.

---

# # # C'est des extraits de code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
N'hésitez pas à copier-coller dans votre éditeur IDE ou LeetCode.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public intérieur égalPairs(int[][] grille) {
int n = longueur de la grille;
résultat int = 0;

// 1. Conservez toutes les lignes dans un hashmap (rowString -> fréquence)
Carte<String, entier> rowMap = nouveau HashMap<>();
pour (int i = 0; i < n; i++) {
// Convertir la ligne en une chaîne séparée par des virgules pour unicité
StringBuilder sb = nouveau StringBuilder();
pour (int val : grille[i]) {
sb.append(val).append(','); // les virgules traînantes assurent une netteté
}
Clé de chaîne = sb.toString();
rowMap.put(key, rowMap.getOrDefault(key, 0) + 1);
}

// 2. Itérer sur les colonnes, construire la chaîne, et chercher
pour (int col = 0; col < n; col++) {
StringBuilder sb = nouveau StringBuilder();
pour (int ligne = 0; ligne < n; ligne++) {
sb.append(grid[row][col]).append(',');
}
Clé de chaîne = sb.toString();
résultat += rowMap.getOrDefault(key, 0);
}

le résultat du retour;
}
}
«» "

> **Pourquoi un `Builder String`?**
> *StringBuilder* est plus efficace que `Arrays.toString()` pour la concaténation répétée.

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def egalPairs(self, grille: List[List[int]]) -> Int:
n = len(grid)
1. Compter toutes les lignes comme des tuples (hashable)
nombres de lignes = {}
pour la ligne de la grille:
key = tuple(row) # tuples sont hashables
row_counts[key] = row_counts.get(key, 0) + 1

2. Construire des colonnes comme des tuples et regarder vers le haut
résultat = 0
pour le col dans la plage(n):
col_tuple = tuple(grid[row][col] pour ligne dans range(n))
résultat += row_counts.get(col_tuple, 0)

résultat du retour
«» "

> **Python tip** – les tuples sont immuables et hashables, ce qui en fait des clés de dictionnaire parfaites pour les séquences.

---

C++

'`cpp
#incluez <vecteur>
#incluez <string>
#inclut <non-ordonné_map>

solution de classe {
public:
int egalPairs(std::vector<std::vector<int>& grille) {
int n = quadrillage.size();
résultat int = 0;

// Aide à convertir une ligne/colonne en une clé de chaîne
auto toKey = [n](const std::vector<int>& v) -> std::string {
md:: touche de chaîne;
cle.reserve(n * 12); // réserve brute
pour (int x : v) {
key += std::to_string(x);
touche += ','; // délimiteur
}
la clé de retour;
};

// 1. Stocker les lignes
std::unordered_map<std::string, int> rowMap;
pour (const auto & ligne : grille) {
md:: touche chaîne = toKey(row);
++rowMap[key];
}

// 2. Vérifier les colonnes
pour (int col = 0; col < n; ++col) {
à:vecteur<int> colVec(n);
pour (int ligne = 0; ligne < n; + ligne)
colVec[row] = grille[row][col];
std:: touche chaîne = toKey(colVec);
auto it = rowMap.find(key);
si (it != rowMap.end())
résultat += it->seconde;
}

le résultat du retour;
}
};
«» "

> **Pourquoi la conversion des chaînes en C++? * *
> Le `std::vector` lui-même n'est pas hachage par défaut; la conversion à une chaîne maintient le code simple et assez rapide pour `n ≤ 200`.

---

Analyse de complexité

Formule métrique Résultat
C'est quoi, ça ?
(processus n lignes + colonnes)
**L'espace**="O(n2)" pour la carte (le pire cas chaque ligne est unique)=" ≤ 40 000 paires de clés/valeurs"

---

Bon, mauvais et affreux

Catégorie Que faire Que faire Que faire pour éviter
- C'est quoi ?
**Bien** Utilisez une carte de hachage (ou dictionnaire) pour stocker les lignes. <br>• Convertir les lignes/colonnes en une touche *unique* (chaîne/tuple). <br>• Tirer parti des tables de hachage natif pour la recherche moyenne O(1).
**Bad** <br>• Recréer un tableau de colonnes entier pour chaque comparaison sans cache.
**Ugly**. • Fonctions de hachage personnalisées trop compliquées pour les vecteurs. <br>• Concaténation manuelle de la chaîne avec les boucles internes `%s`/`+` menant à la construction de chaînes quadratiques. <br>• Éviter les délimiteurs causant des collisions avec le hachage (par exemple, `[1,23]` vs `[12,3]`).

---

Conseils d'entrevue

1. ** Expliquez votre idée d'abord** – parlez à travers le tour de la carte de hachage; les intervieweurs aiment vous voir briser le problème.
2. **Cas de bord de Mention** – `n = 1`, lignes/colonnes dupliquées, tous les nombres les mêmes, tous distincts.
3. **Discuse les compromis temps/espace** – C'est O(n2) ce qui est optimal; O(n3) serait timeout pour n=200. (en milliers de dollars)
4. **Optimisation facultative** – Stocker les colonnes d'abord, puis itérer les lignes (symétrique).
5. **Lisibilité du code** – Utilisez des noms de variables significatifs (`rowMap`, `colKey`, etc.).

---

Autre lecture

La langue de la ressource Autres
C'est pas vrai.
Solution LeetCode Discutez de solutions optimales approuvées par la communauté
Cracking the Coding Interview (en anglais seulement) – Hash Tables (en anglais seulement)
Algorithmes, 4ème édition – Section sur les tableaux deash

---

Structure du blog amicale

```markdown
# LeetCode 2352 – Paires égales de lignes et de colonnes
## Java, Python, C++ Solutions et guide d'entrevue

Description de la méta
« Apprenez la solution O(n2) la plus rapide pour LeetCode 2352 – Equal Row and Column Pairs. Trouvez le code Java, Python et C++, plus les stratégies d'entrevue."

Mots clés
LeetCode 2352, Equal Row and Column Pairs, interview par algorithme, solution de hash map, interview de codage Java, interview de Python, interview de codage C++

Aperçu
1. Récapitulation du problème
2. Aperçu de l'intuition et de la solution
3. Code (Java / Python / C++)
4. Analyse de la complexité
5. Bonnes/Bad/Ugly Patterns
6. Conseils d'entrevue
7. Lecture supplémentaire
«» "

> L'article ci-dessus est prêt à être publié sur Medium, Dev.to, ou votre blog personnel.
> Il suffit de copier le Markdown, ajuster la méta description, et vous êtes prêt à partir!

---

Enveloppe

- ** Solution optimale :** `O(n2)` avec une carte de hachage.
- **Les trois langues** montrent la même idée ; choisissez celle avec laquelle vous êtes le plus à l'aise.
- **Explication prête à l'entrevue** + code propre = votre billet au tour suivant.

Bon codage, et bonne chance pour votre prochain entretien technique! C'est ce qu'il a dit