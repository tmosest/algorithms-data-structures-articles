---
titre: LeetCode 3036. Nombre de subarrays qui correspondent à un modèle II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code – Trois langues

Vous trouverez ci-dessous une mise en œuvre **prête à copier** de la solution optimale pour LeetCode 3036
`Nombre de subarrays qui correspondent à un modèle II`.
La solution fonctionne en **O(n + m)** temps et **O(m)** espace auxiliaire, en utilisant le KMP
(=Knuth–Morris–Pratt=) idée d'appariement sur un tableau *comparaison*.

> *Pourquoi KMP? *
> Après avoir converti le tableau numérique en un tableau de `-1, 0, 1` qui
> représente <, =, > , le problème devient
> un problème d'appariement de motifs exact sur une chaîne entière – exactement quoi
> KMP est destiné à.

---

### 1.1 Java – `Solution.java "

"Java
Importation de java.util.*;

solution de classe publique {

- Oui. Construire le tableau lps (prétraitement KMP) --------- */
construction de vide statique privéLps(int[] pat, int[] lps) {
int m = longueur de la tige;
int len = 0; // longueur du suffixe de préfixe précédent le plus long
lps[0] = 0; // lps[0] est toujours 0

pour (int i = 1; i < m; ) {
si (pat[i] == pat[len]) {
len++;
lps[i] = len;
i++;
} autre {
Si (len != 0) {
len = lps[len - 1];
} autre {
lps[i] = 0;
i++;
}
}
}
}

/* ----------- API principale ---------- */
nombre d'entrées publiquesMatchingSubarrays(int[] nums, int[] pattern) {
int n = longueur nums;
int m = profil.longueur;
Si (m) 0) retour 0;

/* Construire le tableau de comparaison pour les nombres (taille n‐1) */
int[] cmp = nouvelle int[n - 1];
pour (int i = 0; i < n - 1; i++) {
si (nums[i] < nums[i + 1]) cmp[i] = 1; //
Sinon, si (nums[i] > nombres[i + 1]) cmp[i] = -1; //
autres cmp[i] = 0; // -=- → 0
}

/* KMP nécessite le modèle lui-même, donc nous le conservons tel quel. */
int[] lps = nouvelle int[m];
boundLps(modèle, lps);

- Oui. Recherche KMP sur cmp
i = 0; // indice pour cmp[]
int j = 0; // indice pour motif[]
réponse int = 0;

pendant que (i < cmp.longueur) {
Si (cmp[i] == modèle[j]) {
i++; j++;
}

si (j == m) { // une correspondance complète trouvée
réponse++;
j = lps[j - 1]; // continuer à rechercher le prochain chevauchement
} sinon si (i < cmp.longueur && cmp[i] != motif[j]) {
Si (j != 0) j = lps[j - 1];
autres i++;
}
}
réponse de retour;
}
}
«» "

> **Compilation et exécution* *
> ```bash
> Javac Solution. java
> java -jar leetcode. jar # le harnais LeetCode appellera countMatchingSubarrays
> `` "

---

### 1.2 Python – `solution.py "

'`python
Solution de classe:
C'est... Prétraitement KMP ---------
def _build_lps(self, pat):
m = len(pat)
lps = [0] * m
longueur = 0
i = 1
alors que i < m:
Si pat[i] == Pat[longueur]:
longueur += 1
lps[i] = longueur
i += 1
Sinon:
si longueur != 0:
longueur = lps[longueur - 1]
Sinon:
lps[i] = 0
i += 1
retourner lps

C'est... API principale...
def countMatchingSubarrays(self, nombres: List[int], pattern: List[int]) -> Int:
n, m = len(nums), len(pattern)
Si m == 0:
retour 0

# Construire le tableau de comparaison pour les nombres (taille n-1)
cmp = [0] * (n - 1)
pour i dans la plage (n - 1):
si des nombres [i] < nombres[i + 1]:
CMP[i] = 1 #
nombres d'élif[i] > nombres[i + 1]:
[i] = -1 #
Sinon:
CMP[i] = 0 #

# Construire une table d'échec KMP
lps = auto._build_lps(pattern)

# Recherche KMP
i = j = 0
réponse = 0
alors que i < len(cmp):
Si cmp[i] == motif[j]:
i += 1
j += 1
Si j == m: # correspondance complète
réponse += 1
j = lps[j - 1]
elif i < len(cmp) et cmp[i] != modèle[j]:
Si j != 0:
j = lps[j - 1]
Sinon:
i += 1
réponse de retour
«» "

> **Running**
> ```bash
> solution python -m unittest. py # harnais d'essai facultatif
> `` "

---

### 1.3 C++ – `solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
- Oui. Prétraitement KMP: construire un tableau lps --------- */
vide buildLps(vector const<int>& pat, vector<int>& lps) {
int m = taille de rotule();
lps.assign(m, 0);
int len = 0; // précédent plus long suffixe de préfixe
pour (int i = 1; i < m; ) {
si (pat[i] == pat[len]) {
len++;
lps[i] = len;
i++;
} autre {
Si (len != 0)
len = lps[len - 1];
Autre
lps[i] = 0, i++;
}
}
}

- Oui. API principale --------- */
nombre intMatchingSubarrays(vecteur<int>& nums, vecteur<int>& patron) {
int n = nombres.size(), m = motif.size();
Si (m) 0) retour 0;

/* Construire le tableau de comparaison pour les nombres (taille n-1) */
vecteur <int> cmp(n - 1);
pour (int i = 0; i < n - 1; ++i) {
si (nums[i] < nums[i + 1]) cmp[i] = 1; //
autres si (nums[i] > nombres[i + 1]) cmp[i] = -1; //
autres cmp[i] = 0; //
}

/* Prétraitement KMP sur le modèle */
vecteur <int> lps;
boundLps(modèle, lps);

/* Recherche KMP */
i = 0, j = 0, réponse = 0;
pendant que (i < cmp.size()) {
Si (cmp[i] == modèle[j]) {
++i; ++j;
}

si j == m) { // correspondance complète
++réponse;
j = lps[j - 1];
} sinon si (i < cmp.size() && cmp[i] != motif[j]) {
Si (j != 0)
j = lps[j - 1];
Autre
++i;
}
}
réponse de retour;
}
};
«» "

> **Compilation**
> ```bash
> g++ -std=c++17 -O2 -pipe -statique -s solution.cpp -o solution
> `` "

---

- Oui. 2. Un regard rapide sur l'approche optimale

L'approche Temps Espace Remarques
C'est pas vrai.
**O(n · m)**=O(1)=Simple à écrire mais TLE sur les tests de 105 dimensions. Autres
**Sliding-Window + Hash******* O(n)**= O(n)= Utilise un hachage roulant; risque de collision (rare mais possible). Autres
**KMP on Compare Array***** **O(n + m)**. **O(m)**. Autres

2.1 À quoi ressemble le tableau comparatif

Pour les «nums = [1, 3, 2, 4]»:

«» "
1 < 3 → 1
3 > 2 → -1
2 < 4 → 1
«» "

Ainsi, le tableau de comparaison est `[1, -1, 1]`.
Le motif reste `[1, -1, 1]` (exactement les mêmes valeurs).
Maintenant la tâche est : *= Combien de fois la chaîne entière `pattern` apparaît dans
cette chaîne de comparaison?- Une question classique de KMP.

---

- Oui. 3. Article de blog – Cracking LeetCode 3036 avec KMP (Java, Python, C++)

> **Mots-clés** : *Code d'accès 3036*, *Nombre de sous-barrages qui correspondent à un modèle II*, *KMP*, *Java*, *Python*, *C++*, *codage interview*, *algorithme design*, *emploi interview prep*.

---

3.1 Introduction

> **LeetCode 3036 – Nombre de subarrays qui correspondent à un modèle II**
> est un problème faussement simple mais hautement noté qui teste un candidat
> capacité de reconnaître les modèles, de transformer les données et d'appliquer un classique
> algorithme d'appariement de chaînes (KMP).
> Pour quiconque se prépare à coder des interviews dans les entreprises de haute technologie, maîtriser
> ce problème est un "must-know" parce qu'il démontre:

- Compréhension approfondie de la manipulation **array** et de la programmation **dynamique**.
- Capacité d'identifier un problème comme une tâche cachée **chaîne-appariement**.
- Compétence en **Java, Python et C++** – les trois langues les plus souvent
demandé dans les entrevues.

---

### 3.2 Énoncé du problème (court et doux)

> Avec deux tableaux entiers "nums" (taille *n*) et "pattern" (taille *m*),
> compter combien de sous-tribus contigus de "nums" ont le **exacte même
> modèle directionnel** en tant que modèle.
> Le modèle directionnel est défini par des comparaisons:
> * `= 1` → l'élément sub-array à la position *i* est **plus grand* *
> * `============================================================================================================================================================================================================================================================= *
> * `i] = 0` → l'élément sub-array à la position *i* est **égal* *

> *Retournez le nombre total. *

---

Pourquoi Brute- Défis de force (bonnes raisons)

L'algorithme simple O(*n* · *m*) vérifie chaque sous-réseau possible
et le compare au modèle.
Avec des contraintes allant jusqu'à 100 000 éléments, cela devient peu pratique :

'`python
pour le démarrage dans la plage (n - m + 1):
match = Vrai
pour k dans la plage(m):
si compare(nums[start + k], nombres[start + k + 1]) != modèle[k]:
match = Faux; rupture
«» "

complexité temporelle: `O(105 · 105)` → ** dépasse la limite de 1 seconde** sur LeetCode.

---

### 3.4 Le point de vue clé – Convertir en tableau comparatif

1. **Construire un tableau de direction** pour les "nums" de longueur `n-1`:
- `>` → `1`
- `<` → `- 1'
- `=` → `0`

2. **Le motif lui-même est déjà une séquence de `1, -1, 0`**.
Par conséquent, nous recherchons simplement `pattern` dans le tableau de comparaison.

3. **Pas de mémoire supplémentaire pour le hachage**; juste une transformation linéaire du
tableau original.

---

3.5 Pourquoi KMP est le bon outil

- **Déterministe**: Contrairement aux méthodes basées sur le hachage, le KMP n'échoue jamais en raison de collisions.
- **Efficace**: Le prétraitement prend du temps "O(m)"; la recherche prend "O(n)".
- **Simple**: La table de défaillance ('lps') garantit la progression linéaire même
après un match.

---

3.6 Faits saillants de la mise en œuvre

Langage Technique de base Autres
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Java**
**Python**= Compréhension de la liste + aide KMP=1 `cmp[i] = 1 si nombres[i] < nombres[i+1] autres -1'
*C++**="vector<int> cmp(n-1);"="cmp[i] = (nums[i] < nums[i+1]) ? 1 : -1;»

> **Astuce**: Dans le harnais Java de LeetCode, assurez-vous que la signature de la méthode correspond
> `public int countMatchingSubarrays(int[] nums, int[] pattern)`.

---

3.7 Analyse de complexité (ce que les intervieweurs aiment)

Métrique Brute-Force
- C'est quoi ?
Heure
Espace Autres

> La complexité temporelle linéaire garantit que même les essais les plus graves
> *n* = 105 et *m* = 105 exécuter en moins de quelques millisecondes.

---

### 3.8 Pièges communs et bonnes pratiques mauvaises

Piège
- Oui.
Autres Oubliant que le tableau de comparaison a la longueur *n‐1*.Utilisez `if (i < cmp.size())` garde. Autres
Autres Complication excessive en utilisant `int[]]` pour les tranches 2-D. Autres
À l'aide d'un hachage roulant sans manipulation de collisions. Autres
En mélangeant les valeurs de la sémantique dans le tableau de comparaison, vérifier la cartographie des signes. Autres

---

####3.9 À emporter dans le monde réel

> **LeetCode 3036** est un excellent exemple de la transformation de la structure des données**.
> De nombreux problèmes d'entrevue cachent un noyau de couplage de motifs; tournant le problème
> dans une forme algorithmique familière (ici, KMP) est une compétence puissante.
> Implémentez-le dans **Java, Python, C++**, et vous aurez un polyvalent, prouvé
> solution qui impressionne les intervieweurs à Google, Amazon, Microsoft, et plus encore.

---

#### 3.10 Appel à l'action

> Pratiquer les variations suivantes:

1. ** Ajouter une nouvelle direction** ('2' signifiant -différence > seuil) et
adapter le tableau de comparaison en conséquence.
2. **Modifier l'exigence** à au moins *k* se chevauchant.
3. **La solution dans Go** (pour votre prochaine interview).

> Rappelez-vous : **Le bon code est élégant, correct et rapide**.
> La solution KMP ci-dessus coche toutes ces boîtes.

---

- Oui. 4. Conclusion

Nous avons:

- Des implémentations prêtes à la production en Java, Python et C++.
- Montré la transformation d'un problème de tableau à une recherche KMP.
- Fourni un billet de blog prêt à publier qui souligne pourquoi maîtriser LeetCode 3036
est essentiel au succès des entrevues.

Bon codage, et bonne chance pour votre prochaine interview!