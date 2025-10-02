---
titre: LeetCode 1964. Trouvez le cours d'obstacle le plus long valide à chaque poste -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. LeetCode 1964 – *Trouver le plus long cours d'obstacle valide à chaque poste*
**Trancher**=O(n log n)=Java==Python=C++

> On vous donne un tableau `obstacles`.
> Pour chaque index `i` vous devez choisir une sous-séquence qui **inclut** `obstacles[i]`,
> est **non-diminution** et a une longueur maximale possible.
> Retourner un tableau `ans` où `ans[i]` est cette longueur maximale.

La façon classique de résoudre ceci est **Patience Tri** (le même truc qui est utilisé pour
La plus longue séquence augmente).
Nous conservons un tableau auxiliaire `dp` où `dp[len]` est la fin la plus petite possible
valeur* d'une sous-séquence non décroissante de longueur «len + 1» déjà vue.
En balayant les obstacles de gauche à droite, nous recherchons binairement la position
où l'obstacle actuel s'inscrirait dans "dp".
Cette position + 1 est la réponse pour cet indice.
Si l'obstacle prolonge la plus longue séquence jusqu'à présent, nous la poussons sur «dp»,
sinon nous remplaçons la valeur existante – le remplacement garantit que la
la valeur de fin de séquence reste aussi petite que possible, ce qui maintient le tableau optimal
pour les éléments futurs.

Ci-dessous vous trouverez une implémentation propre et prête à la production dans **Java**, **Python** et **C++**.

> **Pourquoi le référencement? * *
> Si vous visez un rôle de codage lourd, LeetCode 1964 est une interview parfaite
> exemple. En avant-plan LeetCode 1964 Solution Java, Cours d'obstacle le plus long
Dans l'article fera le rang de poste
> pour les recruteurs à la recherche d'algorithmes.

---

#### 1.1 Java ( 2024-Style )

"Java
solution de classe {
public int[] le plus longObstacleCoursAchaquePosition(int[] obstacles) {
int n = obstacles. longueur;
int[] dp = nouveau int[n]; // dp[len] – plus petite valeur finale de longueur len+ 1
int[] ans = nouvelle int[n];
int len = 0; // courant longueur la plus longue

pour (int i = 0; i < n; i++) {
// style lié supérieur: premier indice avec valeur > obstacles[i]
Int pos = Arrays.binarySearch(dp, 0, len, obstacles[i] + 1);
si (pos < 0) pos = -pos - 1; // standard

// Mettre à jour le tableau dp
dp[pos] = obstacles[i];

// si nous avons joint à la fin, augmenter la longueur globale
si (pos) len++;

ans[i] = pos + 1; // longueur de la séquence qui se termine à i
}
le retour des an;
}
}
«» "

*Pourquoi `obstacles[i] + 1`? *
Nous utilisons `upper_bound` (premier élément **plus grand** que la clé).
L'ajout de `1` à l'obstacle transforme l'exigence de "non-décroissant" en une exigence strictement
une recherche accrue.

---

#### 1.2 Python ( 3.10+ )

'`python
de bisect import bisect_right
de taper l'importation Liste

def longObstacleCoursAchaquePosition(obstacles: List[int]) -> Liste[int]:
"""
Tri de la patience + recherche binaire (O(n log n)).
"""
dp = [] # dp[len] – plus petite valeur finale pour la subséquence de longueur len+ 1
ans = []

pour x dans les obstacles:
# bisect_right retourne le premier indice avec valeur > x (en haut)
pos = bisect_right(dp, x)
si pos == len(dp):
dp.annexe(x)
Sinon:
dp[pos] = x
Annexe(pos + 1)

retour et
«» "

*Tip:* `bisect_right` est exactement le `upper_bound` dont nous avons besoin.
Si vous utilisez accidentellement `bisect_left` la réponse sera **off par un**.

---

#### 1.3 C++ (Moderne, 2024-style)

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
std::vector<int> le plus longObstacleCoursA chaque position(std::vector<int>& obstacles) {
std::vector<int> dp; // dp[len] – valeur finale minimale de longueur len+ 1
std::vecteur<int> ans;
pour (int x : obstacles) {
// cap_bound: premier élément > x
auto it = std::upper_bound(dp.begin(), dp.end(), x);
int pos = it - dp.begin();
si (it == dp.end())
dp.push_back(x); // prolonger la plus longue longueur
Autre
*it = x; // remplacer pour conserver la valeur finale minimale
ans.push_back(pos + 1); // longueur de subséquence qui se termine à cet indice
}
le retour des an;
}
};
«» "

> **Pourquoi `upper_bound` au lieu de `lower_bound`?* *
> Nous voulons une subséquence non décroissante.
> `upper_bound` garantit que nous insérons *après* tous les éléments égaux à `x`, en veillant à ce que
> subséquence reste non décroissante et le tableau dp reste optimal.

---

- Oui. 2. Les bons, les mauvais et les méchants – Un guide d'entrevue 2024

> *Un article complet, convivial pour le SEO, convivial pour la recherche d'emploi pour quiconque se prépare à
> entretien technique. *

---

2.1 Introduction – Pourquoi LeetCode 1964 compte

- **Mot-clé-rich**: LeetCode 1964.
problème, interview de codage, algorithme d'entretien d'emploi, Java/Python/C++.
- Les recruteurs cherchent des candidats qui peuvent résoudre *Hard* LeetCode questions avec
Code propre et efficace.
- LeetCode 1964 est un défi de programmation dynamique dans le monde réel**
de nombreuses banques de questions d'entrevue.

---

2.2 Le bon – Ce qui fait de ce problème un sujet d'entrevue formidable

Pourquoi ça aide ?
C'est quoi ?
**Exemple du monde réel**Les cours d'obstacle reflètent les problèmes de planification de la vie réelle (p. ex., planification). Autres
**Scales à O(n log n)**= Démontre les connaissances du candidat sur les structures de données avancées. Autres
**Language-agnostique**= Solvable en Java, Python, C++. Parfait pour les portfolios multilingues. Autres
**Non-trivial DP**= Affiche la capacité de transformer une solution O(n2) naïve en solution optimale. Autres

> *Résultat*: Vous allez montrer recruteurs vous pouvez passer d'une idée de force brute à une
> algorithme optimal en moins d'une minute.

---

2.3 Les mauvaises – Pièges communs

Erreur
- Oui.
Utiliser **`lower_bound`** (premier `>=`) Au lieu de **`upper_bound`** (first `>`)" Obstacles[i]` doivent être **inclus**; nous avons besoin d'un indice * strictement croissant* pour la nouvelle valeur. Autres
Autres Oublier d'ajouter **1** au résultat de recherche binaire. Autres
Autres Modifier le tableau `obstacles` d`origine. Autres
Autres L'initialisation de la taille `dp` est correcte. `dp` peut être un vecteur de longueur `n` (longueur maximale possible de subséquence). Autres
Utiliser la récursion pour la recherche binaire dans les langues avec petite pile.Utiliser la recherche binaire itérative pour rester dans les limites de la pile. Autres

---

2.4 Les cas les plus odieux – les cas de bord qui s'enfuient

1. **Tous les éléments sont égaux**
Exemple: `[5,5,5]` → répondre `[1,2,3,4]`.
*Pourquoi il rompt des solutions naïves?* Parce que chaque élément peut être annexé; `dp`
continue de grossir.

2. **Traitement décroissant**
Exemple: `[4,3,2,1]` → répondre `[1,1,1]`.
Binary-search retourne toujours `0`, donc nous ne prolongeons jamais `dp`.

3. ** Grandes valeurs d'entrée (jusqu'à 109)* *
Assurez-vous d'utiliser `long`/`long` si vous êtes tenté d'ajouter 1 à la valeur
avant de chercher. L'algorithme lui-même n'a besoin que d'une comparaison, pas d'arithmétique.

---

2.5 Rapide Code de démarrage (Java / Python / C++)

> **Copier-coller prêt** – il suffit de déposer dans votre IDE ou une fenêtre LeetCode .

"Java
// Java 17+ (format LeetCode)
solution de classe {
public int[] le plus longObstacleCoursAchaquePosition(int[] obstacles) {
int n = obstacles. longueur;
int[] dp = nouvelle int[n];
int[] ans = nouvelle int[n];
int len = 0; // longueur la plus longue vue jusqu'à présent

pour (int i = 0; i < n; ++i) {
int pos = binaireSearch(dp, 0, len, obstacles[i]); // first > obstacles[i]
dp[pos] = obstacles[i];
si (pos) len++;
ans[i] = pos + 1;
}
le retour des an;
}

private int binaireSearch(int[] dp, int gauche, int droite, int cible) {
int l = gauche, r = droite;
pendant que (l <= r) {
Int m = (l + r) >>> 1;
si (dp[m] <= cible) l = m + 1;
autres r = m - 1;
}
retour l; // indice lié supérieur
}
}
«» "

'`python
# Python 3.10+ (format LeetCode)
de bisect import bisect_right
de taper l'importation Liste

def longObstacleCoursAchaquePosition(obstacles: List[int]) -> Liste[int]:
dp = [] # valeur finale la plus faible pour chaque longueur
ans = []

pour x dans les obstacles:
pos = bisect_right(dp, x) # premier indice avec valeur > x
si pos == len(dp):
dp.annexe(x)
Sinon:
dp[pos] = x
Annexe(pos + 1)

retour et
«» "

'`cpp
// C++17 (format LeetCode)
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
std::vector<int> le plus longObstacleCoursA chaque position(std::vector<int>& obstacles) {
std::vector<int> dp; // valeur finale minimale pour chaque longueur
std::vecteur<int> ans;

pour (int x : obstacles) {
auto it = std::upper_bound(dp.begin(), dp.end(), x);
int pos = it - dp.begin();
si (it == dp.end())
dp.push_back(x);
Autre
*it = x;
as.push_back(pos + 1);
}
le retour des an;
}
};
«» "

---

- Oui. 3. Enveloppage – Prenez la prochaine étape

- **Showcase**: Ajouter des solutions LeetCode 1964 à votre portefeuille GitHub.
- **Explain**: Utilisez l'article de pointes dans votre CV:
en Java avec O(n log n) DP.
- **Pratique**: Répétez la logique de recherche binaire sur une recherche binaire similaire
problèmes (p. ex., score maximal de l'enlèvement de pierres ou plus longue augmentation
Succès).
- **Interview**: Lorsqu'on demande un problème *Hard*, mentionnez le cours des obstacles
analogie, puis décrire le Patience-Sorting DP en 30 secondes.

> **Votre prochain recruteur–Ready Move** – soumettre ces solutions, publier cet article,
> et regarder les offres d'entretien s'inscrire.

---

> ** Pensée finale**: Mastering LeetCode 1964 démontre que vous n'êtes pas seulement un
> codeur; vous êtes un ** résolveur de problèmes stratégiques** qui peut naviguer le bon,
> mauvais, et moche de conception d'algorithme – exactement ce dont n'importe quel rôle logiciel senior a besoin.