---
titre: LeetCode 2573. Trouvez la chaîne avec LCP -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2573 – Trouvez la chaîne avec LCP
*Hard – LeetCode*

> **Objectif** – Reconstruire le mot lexicographiquement le plus petit qui satisfait un certain
> `lcp` matrice, ou retourner une chaîne vide si aucun tel mot n'existe.

Ci-dessous vous trouverez trois solutions prêtes à la production (Java, Python, C++), un passage concis de l'algorithme, une analyse des cas de bord, et un article de blog complet qui explique les parties *bon*, *mauvais* et *grosse* du problème.
Le blog est SEO-optimisé pour des titres comme ** 2573 – Trouvez la chaîne avec LCP** et ** Solution** pour que vous puissiez l'utiliser sur vos messages portfolio ou LinkedIn.

---

Code de démarrage rapide

- Oui. 1. Java (Java 17 +)

"Java
Importation de java.util.*;

solution de classe publique {
public Chaîne trouverTheString(int[]] lcp) {
int n = longueur de lcp;
groupe int[] = nouveau groupe int[n]; //
le groupe intermédiaire = 0;

// 1/ 1/ Rédiger une chaîne *potentiel* en regroupant des caractères égaux
pour (int i = 0; i < n; i++) {
si (groupe [i] != 0) poursuivre;
si (++curGroup > 26) retourne "; // > 26 caractères distincts impossibles
groupe[i] = curGroup;
pour (int j = i + 1; j < n; j++) {
si [lcp[i][j] > 0) groupe[j] = curGroup;
}
}

Vérifie que les groupes construits satisfont vraiment à "lcp"
pour (int i = 0; i < n; i++) {
pour (int j = 0; j < n; j++) {
int attendu = (groupe[i] == groupe[j]) ?
(i + 1 < n && j + 1 < n) ? lcp[i + 1] [j + 1] + 1 : 1) :
0;
si (attendu != lcp[i][j]) retourner ";
}
}

// 3=2 Convertir les identifiants de groupe en lettres (a‐z)
StringBuilder sb = nouveau StringBuilder();
pour (int g : groupe) sb.append(char) ('a' + g - 1);
retour sb.toString();
}
}
«» "

> **Complexité** – temps `O(n2)`, espace auxiliaire `O(n).
> `n ≤ 1000`, donc la solution correspond facilement aux limites.

---

- Oui. 2. Python (Python 3.10 +)

'`python
Solution de classe:
def trouver TheString(self, lcp: List[List[int]]) -> str:
n = len(lcp)
groupe = [0] * n # 1
pour = 0

# Construire une chaîne potentielle
pour i dans la plage(n):
si groupe[i]:
poursuivre
pour 1
si cur > 26:
retour ""
groupe[i] = cur
pour j dans la plage(i + 1, n):
si lcp[i][j]:
groupe[j] = cur

# Valider la lcp
pour i dans la plage(n):
pour j dans la plage(n):
Exp = 0
si groupe[i]== groupe[j]:
exp = (lcp[i + 1][j + 1] + 1) si i + 1 < n et j + 1 < n autre 1
si exp != lcp[i][j]:
retour ""

# Convertir en chaîne
retourner ''.join(chr(ord('a') + g - 1) pour g dans le groupe)
«» "

---

- Oui. 3. C++ (C++17 +)

'`cpp
solution de classe {
public:
chaîne trouver La chaîne(vecteur<vecteur<int>>&lcp) {
int n = lcp.size();
vector<int> groupe(n, 0); // 1-based group id
Int cur = 0;

// / / / / / Construisez une chaîne candidate
pour (int i = 0; i < n; ++i) {
si (groupe [i]) se poursuit;
si (++cur > 26) retourner ";
groupe[i] = cur;
pour (int j = i + 1; j < n; ++j) {
si [lcp[i][j] > 0) groupe[j] = cur;
}
}

Vérifier la matrice lcp
pour (int i = 0; i < n; ++i) {
pour (int j = 0; j < n; ++j) {
Int attendu = 0;
si (groupe [i] == groupe [j]) {
= (i + 1 < n && j + 1 < n) ? lcp[i + 1] [j + 1] + 1 : 1;
}
si (attendu != lcp[i][j]) retourner ";
}
}

// 3
la chaîne rés;
res.reserve(n);
pour (int g : groupe) res.push_back('a' + g - 1);
retour rés;
}
};
«» "

---

L'Algorithme

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
**1. Indices égaux du groupe** 0` signifie `mot[i] == mot[j]`. Nous leur attribuons le même groupe. Dans une matrice LCP, une entrée non nulle force l'égalité à la position actuelle. Autres
**2. Utilisez des lettres minimales**.Le premier index est toujours « a ». Pour chaque nouvel indice, nous réutiliserons la plus petite lettre autorisée par toute égalité antérieure. Lexicographie minimisation: nous n'introduisons une nouvelle lettre que lorsque cela est absolument nécessaire. Autres
**3. Valider**. Calculer le LCP du mot construit (en retour DP: `dp[i][j] = 1 + dp[i+1][j+1]` si égal, sinon `0`) et le comparer à l'entrée. Un mot construit * doit* reproduire exactement la matrice. Le PDD garantit que nous n'avons pas fait d'erreur. 1. Autres
**4. Chaîne finale**= Carte des id de groupe aux lettres `a ... z`.= Les groupes sont une bijection aux lettres; si plus de 26 groupes étaient nécessaires, le problème est impossible. Autres

L'algorithme est essentiellement une stratégie **générative + vérificateur**.
Il fonctionne en 'O(n2)' temps – quadratique est inévitable parce que l'entrée elle-même est une matrice `n × n` – mais les facteurs constants sont minuscules.

---

Cas de bord et pièges communs

Qu'est-ce qu'il faut surveiller ?
Ce n'est pas le cas.
**Plus de 26 caractères distincts** 26` → impossible.
**L'indexation fondée sur le zéro et l'indexation fondée sur le monotype**Le LCP prévu pour le dernier indice d'un groupe devrait être «1». Poignez soigneusement `i+1 < n` et `j+1 < n`. Autres
**Dimensions inégales**= L'entrée garantit `lcp` est `n×n`, mais le codage défensif aide lors du piratage du juge. Autres Ajouter les contrôles des limites avant d'accéder à `lcp[i+1][j+1]`. Autres
Utiliser le stockage auxiliaire `O(n)` pour les groupes, pas de tableau DP 2-D. Autres
**Matrice non symétrique**=Une matrice mal formée sera capturée lors de la vérification. L'étape de vérification garantit l'exactitude. Autres

---

No # # , , , , , , et , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , ,

Aspect du bien
- C'est quoi ?
**Énoncé du problème**=Définir la spécification d'entrée/sortie, les contraintes et la matrice d'exemple. La matrice est dense : chaque entrée doit être vérifiée. La définition de `lcp` est *pas* standard LCP; c'est la table *full* suffixe-matching, qui confond avec les nouveaux arrivants. Autres
**L'élégance algorithmique**=Un simple passage pour construire une corde candidate, puis un seul passage pour valider. Aucun – vous avez seulement besoin de comprendre lcp[i][j] > 0` ↓ le même caractère et le même PD pour LCP. Les gens essaient souvent DP à partir de zéro (O(n3)) ou sur-moteur de la construction; le groupement gourmand est l'endroit doux. Autres
**Difficulté de mise en œuvre** Requiert une manipulation soigneuse des conditions limites (dernier index). Lorsque la matrice `lcp` est mal formée (par exemple zéros incohérents), vous devez déboguer l'inadéquation entre le DP construit et l'entrée. Autres
**Tests**= Utiliser les deux exemples fournis, ainsi que des matrices aléatoires qui satisfont aux contraintes. Autres Assurez-vous de tester les cas `n = 1` et `n = 1000`. Une entrée corrompue aléatoirement pour vérifier que le code retourne """. Autres

---

Pourquoi ce problème est-il une excellente preuve d'entrevue

* **Groupement semblable à un graphique** – la matrice LCP définit implicitement un graphique non dirigé où les bords existent si `lcp > 0`.
* **Greedy + DP** – démontre une approche en deux phases que de nombreux candidats sautent.
* **Limits** – s'inscrit parfaitement dans le paradigme *O(n2)*, ce qui en fait une référence propre pour les intervieweurs.
* **Extension** – vous pouvez modifier le code pour travailler avec plus de 26 lettres, ou pour produire tous les mots possibles, ce qui est excellent pour les projets parallèles.

---

Article de blog optimisé du SEO

Ci-dessous est l'article de blog complet que vous pouvez coller à un blog personnel, Medium, ou LinkedIn.
Il comprend le titre riche en mots clés, une méta description, des en-têtes et des points de puce pour la lisibilité.

---

Code Leet 2573 – Trouver la chaîne avec LCP
**Java / Python / C++ Solutions

Description de la méta
Résolvez le LeetCode 2573 en utilisant un algorithme `O(n2)` optimal. Apprenez l'astuce derrière les indices de regroupement, la vérification LCP, et la manipulation des cas de bord. Parfait pour coder la préparation d'entrevue.

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Comprendre la matrice LCP] (#comprendre-la-lcp-matrice)
3. [La stratégie Greedy‐Plus‐DP] (#la stratégie Greedy-plus-dp)
4. [Mise en œuvre en Java, Python, C++](#mise en œuvre-en-java-python-c)
5. [Testing & Edge‐Case Checklist](#testing-edge-case-checklist)
6. [Complexité temps-espace] (#complexité temps-espace)
7. [Pièges communs (les mauvais)] (#pièges communs-les mauvais)
8. [variations avancées (les plus moles)] (#variations avancées-le-gros)
9. [Attention et conseils d'entrevue] (#Attention-entretien-tips)
10. [Lis supplémentaires] (#autres lectures)

---

- Oui. 1. Aperçu du problème <un nom="problème-overview"></a>

> **LeetCode 2573** – *Trouver la chaîne avec LCP*
> On vous donne une matrice `n × n` `lcp` où `lcp[i][j]` est la longueur du plus long préfixe commun des suffixes commençant aux positions `i` et `j`.
> Votre tâche : **reconstruire le mot lexicographiquement le plus petit** qui satisfait cette matrice, ou retourner une chaîne vide si aucun tel mot n'existe.

Pourquoi est-ce intéressant ?
- Oui. Il mélange *string matching* avec *matrix de raisonnement*.
- La matrice LCP est une table 2-D complète, pas un simple vecteur de valeurs.
- Oui. L'exigence lexicographique impose une construction minutieuse du mot candidat.

---

- Oui. 2. Comprendre la matrice LCP <a name="comprendre-le-lcp-matrix"></a>

- **Les entrées de Zero** signifient que les deux suffixes diffèrent à droite au premier caractère: `word[i] != word[j]`.
- **Inscriptions positives** garantie `word[i] == word[j]`.
En fait, la chaîne entière est partitionnée en **classes d'équivalence** d'indices qui partagent la même lettre.

Exemple (pour la chaîne `"abbc"`):

C'est ce qu'il faut faire.
-- -- -- -- -- -- -- -- -- -- --
(En milliers de dollars des États-Unis)
**b**
D'après les résultats de l'enquête sur les forces de travail, l'écart entre les taux de chômage et les taux de chômage a été plus faible que prévu.
*C**

Vous pouvez voir comment chaque cellule avec une valeur non nulle indique la même lettre aux deux positions.

---

- Oui. 3. La stratégie Greedy‐Plus‐DP <un nom></a>

1. **Construire une chaîne *potentielle* *
*Démarrer avec le groupe id `1` pour l'index 0 (lettre `a`).
Pour chaque nouvel indice «i»:
- S'il existe un `j < i` avec `lcp[i][j] > 0`, réutiliser `word[j]`.
- Sinon, choisissez la lettre *suivante inutilisée* (max(`mot[0...i‐1]') + 1).
- Si nous manquons de lettres (`> z`), retourner immédiatement `""". *

2. **Validité**
Calculer le LCP du mot construit (inverse DP: `dp[i][j] = 1 + dp[i+1][j+1]` si les chars sont égaux, sinon `0`).
Si la table calculée diffère de l'entrée, le candidat est invalide → retourner `""".

3. **Retour** le mot construit.

Pourquoi ça marche ?
- **Correctness** :
*Groupement par `lcp > 0' garantie que toutes les égalités sont satisfaites.
L'étape du PDD garantit l'absence de contradictions cachées. *
- ** minimalité lexicographique**:
Nous réutiliserons toujours la plus petite lettre possible. Ce n'est qu'en cas de besoin que nous passerons à la lettre suivante. Ainsi, la corde finale est la plus petite possible.

---

- Oui. 4. Mise en œuvre en Java, Python, C++ <a name=" implementation-in-java-python-c"></a>

*(Voir les blocs de code ci-dessus – un par langue.) *

Les trois implémentations partagent la même logique :
- Une seule passe pour assigner *IDs de groupe*.
- Une double boucle pour valider toute la matrice.
- Dernière conversion en lettres.
La complexité temporelle est `O(n2)` et l'espace auxiliaire `O(n)`.

---

- Oui. 5. Essais et bords Liste de vérification des cas <un nom d'une liste de vérification des cas sur la base d'essais"></a>

Autres Essai
C'est quoi ?
** Taille minimale** `n = 1''' Doit renvoyer `"a"` indépendamment de la seule entrée. Autres
**Tous les zéros à l'exception de la diagonale**=Les chaînes comme les groupes `"abc"` → doivent être `a`, `b`, `c`. Autres
Autres **Tous positifs** (complètes) (toutes les mêmes lettres). Autres
**Plus de 26 lettres nécessaires**=Construisez une matrice avec 27 classes d'équivalence → vérifiez l'échec immédiat. Autres
**Matrice malformée** (par exemple, `lcp[0][1] = 1` mais `lcp[1][0] = 0`))= La validation devrait attraper l'inadéquation → retourner `"`. Autres
**Random matrices valides**.Utilisez un générateur qui construit une chaîne aléatoire et calcule son LCP; donnez cette matrice au solveur. Autres
**Large `n`** `= 1000`. Autres
**Boundaire à l'index final****S'assurer que le PDD utilise `dp[n-1][n-1] = 1` correctement. Autres

---

- Oui. 6. Complexité temporelle et spatiale <un nom="complexité temporelle-espace"></a>

- **Time**: `O(n2)` – requis parce que nous avons une entrée `n × n`.
- **Espace**: `O(n)` – seulement le tableau de groupe; pas de tableau DP 2-D supplémentaire.

Ces chiffres sont idéaux pour les intervieweurs: la solution s'inscrit dans les budgets de temps d'entrevue communs et est facile à raisonner.

---

- Oui. 6. Pièges communs (les mauvais) <un nom (les mauvais)</a>

Comment ça se montre
C'est-à-dire
**Confuser `lcp > 0` avec DP**.Les débutants pourraient penser que si `lcp[i][j]` est 1, les deux premiers caractères sont identiques, mais peut-être plus tard les caractères diffèrent. La clé est que *toute* valeur non nulle force l'égalité à la position *current*. Autres
L'accès à `lcp[i+1][j+1]` sans vérifier les limites conduit à `ArrayIndexOutOfBounds`. Protégez toujours contre `i+1 < n`.
**Passer le vérificateur**= Certaines solutions s'arrêtent après avoir construit la chaîne candidate, mais échouent ensuite sur des contradictions cachées. L'étape du PDD est essentielle. Autres

---

- Oui. 7. Variations avancées (L'Ugly)

> Dans le cas d'un problème de style de recherche, on pourrait vous demander :
> - *Support des alphabets supérieurs à 26* (Unicode).
> - *Produire tous les mots possibles* qui satisfont la matrice (exponentielle).
> - *Recouvrez la chaîne lorsque plusieurs solutions valides existent* et classez-les lexicographiquement.

Ces variations nécessitent une logique supplémentaire :
- Une structure disjointe (Union-Find) pour le regroupement.
- BFS/DFS pour explorer toutes les affectations de lettres.
- Élagage soigneux pour éviter une explosion combinatoire.

---

- Oui. 8. Takeaway & Interview Tips <a name="takeaway-interview-tips"></a>

- **Exposer l'idée de classe d'équivalence**: Un modèle mental rapide pour le raisonnement sur `lcp`.
- **Afficher les deux phases**: génération + vérification.
- **Parler de la complexité**: Quadratic est le meilleur que vous pouvez espérer étant donné la taille d'entrée.
- **Manipulation des frontières**: dernier cas spécial d'index → `1`.

En expliquant, soulignez que la partie gourmande assure la minimalité lexicographique, tandis que DP garantit la justesse.

---

- Oui. 9. Lecture supplémentaire <un nom>

- *Suffix Trees and LCP arrays* – Texte standard sur LCP basé sur suffixe.
- *Set Union (Union-Find)* – Utile pour la phase de regroupement.
- *InterviewBit LCP Problèmes* – Défis similaires d'appariement de matrice.
- * Programmation concurrente 4 – Correspondance de chaînes* – Plongez profondément dans les calculs LCP.

---

Les pensées finales

LeetCode 2573 peut sembler intimidant car il implique une matrice dense `n × n`, mais le principe sous-jacent est simple: ** propagation de l'égalité + validation DP**.

Mise en œuvre en Java, Python ou C++ :
- Capacité de penser graphiquement aux cordes.
- Compétence dans la construction avide avec des garanties correctes.
- Manipulation soigneuse des cas de bord et des contraintes.

** Bonne chance pour votre prochaine interview!**

---


---

N'hésitez pas à adapter l'article ou les extraits de code à votre style, ou à ajouter des captures d'écran de votre harnais de test.

Bon codage !