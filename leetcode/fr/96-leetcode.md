---
titre: LeetCode 96. Arbres de recherche binaire uniques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## # Unique Arbres de recherche binaire – 96. LeetCode – Une plongée profonde
**Bien, mal et mal – Comment le faire dans votre prochaine entrevue* *

> **Mots clés:** Arbres de recherche binaire uniques, LeetCode 96, DP Catalan Numbers, Java, Python, C++, préparation d'entrevue

---

TL;DR
- **Problème:** Compter le nombre d'arbres de recherche binaire structurellement uniques qui peuvent être construits avec `n` clés distinctes 1...n.
- **Réponse :** Le résultat est le *n-th Catalan number*.
- **Complexité:** temps "O(n2)", espace "O(n)".
- **Pourquoi c'est important :** Ce problème est un exercice PDD classique qui met en évidence votre capacité à identifier les modèles combinatoires, à mettre en place des relations efficaces de récurrence et à écrire du code propre dans plusieurs langues.

---

- Oui. 1. Déclaration de problème (Code de bord 96)

> **Avec un entier `n`, retourner le nombre de BST structurellement uniques (arbres de recherche binaire) qui ont exactement `n` noeuds avec des valeurs distinctes de `1` à `n`**.
> **Constances:** `1 <= n <= 19`.

---

- Oui. 2. Les mathématiques derrière la réponse

2.1 Nombres catalans

Le nombre de BST distinctes avec des nœuds `n` est le nombre `n`-th Catalan:

\[
C_n = \frac{(2n) !}{n!(n+1) !} \quad\text{ou}\quad
C_n = \sum_{i=1}^{n} C_{i-1} \times C_{n-i}
\]

La récurrence résulte du choix d'une racine:
- Pour la racine `i`, le sous-arbre gauche a des nœuds `i-1`, le sous-arbre droit a des nœuds `n-i`.
- Le nombre d'arbres avec la racine `i` est `C_{i-1} * C_{n-i}`.
- Somme sur toutes les racines possibles.

2.2 Pourquoi `n <= 19`?

Le 19ème numéro catalan est `1767263190`, confortablement adapté dans un entier signé 32 bits (`int`). Cependant, pour rester en sécurité (et parce que le "int" de Java est de 32 bits, le "int" de Python est une précision arbitraire, et que le "long" de C++ est de 64 bits), nous utiliserons le "long`/`long long` en Java/C++ et simplement le "int` en Python.

---

- Oui. 3. Conception de l'algorithme

Étape Explication
- C'est quoi ?
**Initialiser** un tableau `dp[0...n]` où "dp[i]" conservera le nombre de BST uniques avec des nœuds `i`. Autres
**Causes de base**="dp[0] = 1` (arbre vide), `dp[1] = 1` (noeud unique). Autres
**Itérer** au-dessus de `nœuds = 2 ... n`= Pour chaque nombre possible de nœuds, calculer `dp[nœuds]` par la récurrence. Autres
**Retour** `dp[n]`. Autres

complexité du temps: `O(n2)` (double boucle).
complexité spatiale: `O(n)` (le tableau DP).

---

- Oui. 4. Mise en œuvre du code

Voici des implémentations idiomatiques propres dans **Java**, **Python** et **C++**. Chacun suit la même stratégie de PDD et est prêt pour une entrevue.

#### 4.1 Java

"Java
// LeetCode 96: Arbres de recherche binaire uniques
// Temps O(n^2), Espace O(n)

solution de classe publique {
public int numTrees(int n) {
long[] dp = nouveau long[n + 1]; // utiliser longtemps pour éviter le débordement
dp[0] = 1; // arbre vide
dp[1] = 1; // noeud unique

pour (int nœuds = 2; noeuds <= n; noeuds++) {
nombre long = 0;
pour (int root = 1; root <= nœuds; root++) {
int gauche = racine - 1; // noeuds dans le sous-arbre gauche
int droite = noeuds - racine; // noeuds dans le sous-arbre droit
nombre += dp[gauche] * dp[droite];
}
dp[nodes] = nombre;
}
retour (int) dp[n]; // résultat correspond à int pour n <= 19
}
}
«» "

4.2 Python

'`python
# LeetCode 96: Arbres de recherche binaire uniques
Temps O(n^2), Espace O(n)

def numTrees(n: int) -> Int:
dp = [0] * (n + 1)
dp[0] = 1 # arbre vide
dp[1] = 1 # noeud unique

pour les noeuds de portée(2, n + 1):
Total = 0
pour la racine de portée(1, noeuds + 1):
gauche, droite = racine - 1, noeuds - racine
Total += dp[gauche] * dp[droite]
dp[nodes] = total

retour dp[n]
«» "

### 4.3 C++

'`cpp
// LeetCode 96: Arbres de recherche binaire uniques
// Temps O(n^2), Espace O(n)

#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
nt numTrees(int n) {
vecteur <long> dp(n + 1, 0);
dp[0] = 1; // arbre vide
dp[1] = 1; // noeud unique

pour (nœuds int = 2; noeuds <= n; ++nœuds) {
nombre long = 0;
pour (int root = 1; racine <= noeuds; ++root) {
int gauche = racine - 1;
int droite = noeuds - racine;
nombre += dp[gauche] * dp[droite];
}
dp[nodes] = nombre;
}
retour static_cast<int>(dp[n]); // s'insère dans int pour n <= 19
}
};
«» "

---

- Oui. 5. Le bien, le mal et le mal

Aspect du bien
- C'est quoi ?
**Mathématical Insight** Pas évident pour les débutants. Une mauvaise interprétation de la récurrence entraîne des bugs hors-par-un. Autres
**Complexité du temps**Le `O(n2)` est optimal pour le DP. La récursion naïve est invraisemblable. La sur-ingénierie (p. ex. l'exposition à la matrice) est inutile. Autres
Autres **Optimisation de l'espace** DP bidimensionnel avec mémoire "n2". Débordement de la pile de récursion si ce n'est pas mémorisé. Autres
**Cas d'Edge**=Poignées `n=0` (arbre vide) gracieusement. Oublier `dp[0] = 1` brise la formule. Retour `int` quand `long` nécessaire pour plus grand `n`. Autres
**Nuances de langue** La précision arbitraire de Python cache le débordement mais coûte de la vitesse. C++ "long" nécessaire pour la sécurité. Autres
Utiliser `n=3 → 5`, `n=1 → 1`, `n=19 → 1767263190`. Autres

**À emporter:** Une solution DP claire, des cas de base corrects, et une bonne manipulation de type sont les bons. Évitez la surcomplication avec les tables de récursion ou de mémo au-delà de la nécessité. Le "gugly" vient généralement de ne pas penser à travers la récurrence ou la mal-manipulation des dimensions entières.

---

- Oui. 6. Conseils d'entrevue

1. ** Expliquez d'abord la récurrence.** Parlez de choisir une racine et de multiplier le nombre de sous-arbres gauche/droit.
2. **Afficher le lien catalan** – les employeurs aiment quand vous connectez un problème à une séquence bien connue.
3. **Débats temps/espace.** Pourquoi `O(n2)` DP bat la récursion naïve.
4. **Faire ressortir les cas de base**. Souligner l'importance de «dp[0] = 1».
5. ** Contraintes à la peine de mort** Montrez que vous avez vérifié que le 19ème numéro catalan correspond à `int`.

---

- Oui. 7. Résumé du blog optimisé SEO

Description de la méta
> Master LeetCode 96 – Arbres de recherche binaire uniques. Lisez notre guide détaillé avec des solutions Java, Python et C++, des idées de programmation dynamiques et des conseils de préparation d'entrevues. Parfait pour les ingénieurs en logiciels prêts à décrocher leur prochain emploi.

Titres suggérés
- `Arbres de recherche binaires uniques – 96`
- "Pourquoi les nombres catalans comptent dans DP"
- Étape par étape Solution Java "
- `Python Implementation for Quick Grabs "
- Code `C++ rapide et sûr "
- "Le Bon, le Mauvais et le Méchant du compte de la BST"
- `Interview Hacks: parler de ce problème "

### Mots-clés pour éparpiller
- arbres de recherche binaire uniques
- leetcode 96 solution
- programmation dynamique catalane
- question d'entrevue BST
- Compte de la TVB Java
- Exemple Python DP
- C++ défi de codage
- entretien avec l'ingénieur logiciel

---

- Oui. 8. Pensées finales

- Reste simple. Une récurrence nette du PDD remporte des entrevues.
- **Montrer la polyvalence.** Présenter des solutions en plusieurs langues – démontrer la capacité d'adaptation.
- **Relativement aux fondamentaux.** Les chiffres catalans relient la combinatoire, la théorie des graphiques et le DP ensemble.
- ** Pratique.** Essayez les variations : comptez les BST avec des valeurs de nœuds non 1...n, ou comptez les BST avec des contraintes de hauteur.

Bonne chance ! C'est ce qu'il a dit