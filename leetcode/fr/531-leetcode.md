---
titre: LeetCode 531. Pixel solitaire Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. Lonely Pixel I – Les bons, les mauvais et les mauvais
> **LeetCode #531="Medium="Java="Python="C++="Algorithme="Prép* *

> Quand vous êtes dans un entretien d'emploi, vous ne répondez pas seulement à une question – vous montrez comment vous résolvez les problèmes, comment vous pensez et comment vous communiquez.

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Processus envisagé et bon plan] (#processus réfléchi et bon plan)
3. [Pièges communs – Le mauvais] (#pièges communs-mauvais)
4. [Deep-Dive – L'Ugly] (#deep-Dive-ugly)
5. [solution optimale] (#solution optimale)
6. [Mise en œuvre en trois langues] (#Mise en œuvre en trois langues)
- Java
- Python
- C++
7. [Analyse de la complexité] (#analyse de la complexité)
8. [Testing & Edge Cases] (#testing-edge-cases)
9. [Attention et conseils d'entrevue] (#Attention-entretien-tips)
10. [SEO Meta & Keywords](#seo-meta-keywords)

---

## Énoncé du problème <un nom="état du problème"></a>

> On vous donne un tableau 2-D `image` de la taille `m × n`.
> Chaque cellule est soit `'B'` (noir) ou `'W'` (blanc).
> Un pixel **noir seul** est un pixel `'B'` de telle sorte que ** toute sa ligne et toute sa colonne ne contiennent aucun autre `'B'`**.
> Retourne le nombre de pixels noirs solitaires.

*Contrôles*

- `1 ≤ m, n ≤ 500`
- `photo[i][j]` est `'B'` ou `'W'`

---

## Processus de pensée – Le bon design <un nom="processus de pensée-bon design"></a>

1. **Courbe-Force**
- Pour chaque `'B'`, scannez toute la ligne et la colonne → `O(m*n*(m+n))`.
- Fonctionne pour les petites données, mais ** inacceptable** pour `500×500`.

2. **Comptage des préfixes**
- Précomptez les pixels noirs dans chaque ligne et colonne.
- Ensuite, pour chaque `'B'`, vérifiez simplement si `rowCount[i] == 1 && colCount[j] == 1`.
- **Optimal**: "O(m*n)" temps, "O(m+n)" espace.

3. **Pourquoi c'est bon**
- **Simplicité** – logique claire, facile à raisonner.
- **Performance** – temps linéaire, s'adapte dans les limites.
- **Extensibilité** – peut être adapté à la ligne de base II (même ligne et nombre de colonnes) avec des changements minimes.

---

## Pièges communs – Le « mauvais » <un nom « commun-pièges mauvais »></a>

Pourquoi ça arrive Conséquence
- C'est quoi ?
Autres Compter à l'intérieur de la boucle.
En dehors de l'indexation Mélanger les indices ligne/colonne
Utilisation de `HashMap` par ligne de données Facteurs constants et mémoire élevés
Oubliant de traiter `'W'` comme 0' Négatif compte dans les colonnes

> **Éviter ces** par:
> *Le précomptage compte une fois,*
> * Utilisant des tableaux simples, *
> *Test sur les caisses de bord (`all W`, `all B`, ` single B`). *

---

## Deep-Dive – Le nom de "Ugly"

Parfois, les intervieweurs veulent voir comment vous manipulez ** contraintes supplémentaires** ou ** cas de pointe** vous pourriez avoir négligé:

- **Input immuable** – Si vous ne pouvez pas modifier `image`.
*Solution:* Compter dans des tableaux séparés, ne pas muter `image`.

- **Espace optimisé** – espace auxiliaire « O(1) ».
*Trick:* Utilisez deux tableaux de taille `m + n` pour les nombres, qui est `O(m+n)` – toujours optimal.

- **Exécution parallélienne** – Si l'on utilise le multithreading.
*Caveat:* Assurer la sécurité des fils lors de la mise à jour compte.

- **Grande entrée** – Au-delà de 500x500 (p. ex. 105 × 105).
*Approach:* Entrée en streaming, compte à la volée, ou utilisant un jeu de hachage pour les lignes/cols qui ont un seul `'B'`.

---

## Solution optimale <un nom="solution optimale"></a>

1. Créer deux tableaux entiers: `rowCount[m]` et `colCount[n]`.
2. ** Premier laissez-passer** – comte ` 'B'' dans chaque ligne et colonne.
3. **Deuxième passe** – Pour chaque `'B'`, si `rowCount[i]==1 && colCount[j]==1` → réponse incrément.
4. Réponse de retour.

Cet algorithme utilise seulement deux passages et aucune structure de données supplémentaire au-delà des tableaux de comptage.

---

## Mise en oeuvre en trois langues <un nom="mise en oeuvre en trois langues"></a>

### Java

"Java
Importation de java.util.*;

solution de classe {
public int trouverLonelyPixel(char[]] image) {
int m = longueur d'image;
int n = image[0].longueur;

int[] rowCount = nouveau int[m];
int[] colCount = nouvelle int[n];

// 1ère passe – compter les pixels noirs
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
si (photo[i][j]] == 'B') {
ligne Nombre[i]++;
le numéro d'identification de l'utilisateur;
}
}
}

// 2ème passe – vérifier la solitude
Int solitaire = 0;
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
si [photo[i][j]] «B» &&
rowCount[i] == 1 &&
Count[j] == 1) {
solitaire++;
}
}
}
retourner seul;
}
}
«» "

Python

'`python
Solution de classe:
def trouverLonely Pixel(même, image: Liste[Liste[str]]) -> Int:
m, n = len(photo), len(photo[0])
ligne_cnt = [0] * m
_cnt = [0] * n

# Compte
pour i dans la plage (m):
pour j dans la plage(n):
si photo[i][j]] «B»:
ligne_cnt[i] += 1
_cnt[j] += 1

Contrôle
solitaire = 0
pour i dans la plage (m):
pour j dans la plage(n):
Si photo[i][j]] 'B' et row_cnt[i]== 1 et col_cnt[j] == 1 :
solitaire += 1
retour solitaire
«» "

C++

'`cpp
solution de classe {
public:
int findLonelyPixel(vecteur<vecteur<char>>&image) {
int m = image.size();
int n = image[0].size();

vecteur<int> ligneCnt(m, 0), colCnt(n, 0);

// Nombre de pixels noirs
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
si (photo[i][j]] == 'B') {
++Cnt[i];
++colCnt[j];
}

// Vérifier la solitude
Int solitaire = 0;
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
si [photo[i][j]] «B» &&
[i] == 1 &&
- C'est pas vrai. 1 )
+ seul;

retourner seul;
}
};
«» "

> **Astuce:** Dans les trois langues, vous pouvez échanger les deux passes si vous préférez un seul passe avec un *hashset* de -candidate rows/cols--qui ont exactement un `'B'`.

---

## Analyse de complexité <un nom="analyse de complexité"></a>

Heure Espace supplémentaire
C'est quoi ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
**O(m*n)****

- Pour `m, n ≤ 500`, la solution optimale fonctionne en environ 250 000 opérations – bien moins de 1 ms en Java, Python et C++.
- Utilisation de la mémoire : deux tableaux entiers de taille ≤ 1 000 → < 4 KB.

---

## Testing & Edge Cases <a name="test-edge-cases"></a>

Autres Test d'entrée prévu
- C'est quoi ?
Tous les blancs "0"
Tous les Noirs
Un seul seul "[['B','W'],['W','W']]" "1"
"['B','W','W'],['W','B','W'],['W','W','B']
Autres Large aléatoire de 500×500 avec 1000 `'B`s en positions aléatoires de O(1) – il suffit d'exécuter la solution

> **Meilleure pratique:** Exécutez l'algorithme à deux passages sur une grille aléatoire de 500×500 10× et affirmez que le résultat est cohérent.

---

## Takeaway & Interview Tips <a name="takeaway-interview-tips"></a>

- ** Expliquez votre plan** avant de coder.
- **Discuse** pourquoi le comptage par tableau est optimal.
- **Afficher** le code dans au moins une langue avec laquelle l'intervieweur est à l'aise (Java/Python/C++).
- **Mention** l'échange spatial "O(m+n)" et qu'il est toujours optimal.
- **Ask** sur les contraintes : entrée immuable, données en streaming, ou dimensions énormes.
- **Finir** en résumant la complexité et en donnant un extrait rapide du test unitaire.

> **Rappelez-vous:** Dans les interviews, la clarté bat l'intelligence. Une solution propre et linéaire que vous pouvez expliquer avec confiance vaut bien plus qu'une solution micro-optimisée mais illisible.

---

## SEO Meta & Keywords <a name="seo-meta-keywords"></a>

**Titre de la méta* *
Lonely Pixel I (LeetCode 531) – Optimal Java, Python & C++ Solutions pour les entrevues

**Description détaillée**
Solve LeetCode 531 – Pixel solitaire Je suis en Java, Python et C++. Lisez notre analyse de bonne, mauvaise et ugly, apprenez l'algorithme O(m*n) optimal et obtenez des extraits de code prêts à l'entrevue.

** Mots-clés principaux**
- Pixel solitaire Les
- LeetCode 531
- Algorithme d'entretien
- Solution Java
- Solution Python
- Solution C++
- complexité du temps
- La complexité spatiale
- Préparation d'un entretien d'embauche

** Mots-clés secondaires**
- Conseils d'entretien d'emploi
- Entretien de codage
- Structures de données
- Design d'algorithme
- Nombre de pixels noirs
- Préfixer les sommes

---

La pensée finale

> Maîtrise **Pixel solitaire I** démontre votre capacité à traduire un énoncé de problème dans un algorithme **optimal** et à le mettre en œuvre proprement dans plusieurs langues.
> C'est exactement l'ensemble de compétences que les gestionnaires d'embauche recherchent chez les ingénieurs de logiciels seniors, les data savants, et les développeurs de backend.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit