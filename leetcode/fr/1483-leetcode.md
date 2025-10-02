---
titre: LeetCode 1483. Ancêtre Kth d'un noeud d'arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code – Ancêtre d'arbre (Ancêtre K d'un noeud d'arbre)

Vous trouverez ci-dessous trois implémentations ** prêtes à être copiées** qui résolvent le problème LeetCode 1483. Ancêtre Kth d'un nœud d'arbre.
Les trois solutions utilisent ** lifting binaire** – la technique classique de requête de l'ancêtre O(log n) que chaque ingénieur logiciel senior devrait connaître.

Mots clés Autres
C'est pas vrai.
**Java**= Utilise un tableau 2-D `dp[n][LOG]`. Le prétraitement prend O(n log n). Heure de requête O(log n). Autres
Même idée avec une liste de listes. Un peu plus lent dans le Python pur mais toujours dans les limites de LeetCode. Autres
**C++**= Utiliser `vector<vector<int>>`. Rapide I / O et des tours de vitesse. Autres

> **Conseil pour les intervieweurs:**
> Expliquez que le levage binaire construit une table «dp[v][i] = 2^i‐e ancêtre de v».
> Lors d'une requête, nous décomposons `k` en binaire et sautons dans la table.

---

1.1 Mise en œuvre de Java

"Java
Importation de java.util.*;

classe publique ArbreAncêtre {
En ce qui concerne l'âge de la retraite, il convient de noter que l'âge de la retraite est inférieur à celui de la retraite.
int LOG; // puissance maximale de deux nécessaires

public ArbreAncêtre(int n, int[] parent) {
LOG = 20; // 2^20 > 5 * 10^4 (n <= 5e4)
up = nouvelle int[n][LOG];

// niveau de construction 0 (parent direct)
pour (int v = 0; v < n; v++) {
up[v][0] = parent[v] == -1 ? -1 : parent[v];
}

// construire des pouvoirs supérieurs
pour (int i = 1; i < LOG; i++) {
pour (int v = 0; v < n; v++) {
int milieu = haut[v][i - 1];
up[v][i] = (milieu) -1) ? -1 : vers le haut [milieu] [i - 1];
}
}
}

*** Retourner l'ancêtre kth du noeud, ou -1 si elle n'existe pas. */
Int public getKthAncestor(int node, int k) {
pour (int i = 0; i < LOG; i++) {
si ((k & (1 << i))) != 0) {
nœud = haut[node][i];
Si (noeud) -1) retour -1;
}
}
noeud de retour;
}

// ---- Exemple de test ----
public statique vide principal(String[] args) {
Int[] parent = {-1, 0, 0, 1, 1, 2, 2};
ArbreAncêtre ta = nouvel arbreAncêtre(7, parent);

Système.out.println(ta.getKthAncêtre(3, 1)); // 1
Système.out.println(ta.getKthAncêtre(5, 2)); // 0
Système.out.println(ta.getKthAncêtre(6, 3)); // -1
}
}
«» "

---

1.2 Mise en œuvre de Python

'`python
classe ArbreAncêtre:
def __init_(self, n: int, parent: list[int]) -> Aucun:
LOG = 20 # 2^20 > 5*10^4
Self.up = [[-1] * Self.LOG pour _ dans la plage(n)]

pour v dans la plage(n):
Self.up[v][0] = parent[v] si parent[v] != -1 autre

pour moi à portée(1, moi. LOG:
pour v dans la plage(n):
milieu = auto.up[v][i - 1]
Self.up[v][i] = self.up[mid][i - 1] si mi != -1 autre

def getKthAncestor(self, noeud: int, k: int) -> Int:
pour i à portée (même. LOG:
si k & (1 << i):
noeud = self.up[node][i]
en cas de nœud - 1 :
retour -1
noeud de retour


# ---- Exemple de test ----
si __nom__ == "__main__" :
parent = [-1, 0, 0, 1, 1, 2, 2]
arbre = arbreAncêtre(7, parent)
print(tree.getKthAncêtre(3, 1)) # 1
print(tree.getKthAncêtre(5, 2)) # 0
print(tree.getKthAncêtre(6, 3)) # -1
«» "

---

*## 1.3 C++ Mise en œuvre

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe ArbreAncêtre {
vector<vector<int>> up; // up[v][i] = 2^i-e ancêtre de v
int LOG; // puissance maximale de deux nécessaires

public:
ArbreAncêtre(int n, vecteur<int> parent) {
LOG = 20; // 2^20 > 5*10^4
up.assign(n, vector<int>(LOG, -1));

pour (int v = 0; v < n; ++v)
up[v][0] = (parent[v]] -1) ? -1 : parent[v];

pour (int i = 1; i < LOG; ++i)
pour (int v = 0; v < n; ++v) {
int milieu = haut[v][i-1];
up[v][i] = (milieu == -1) ? -1 : up[milieu][i-1];
}
}

int getKthAncestor(int noeud, int k) {
pour (int i = 0; i < LOG; ++i)
Si (k & (1 << i)) {
nœud = haut[node][i];
Si (noeud) -1) retour -1;
}
noeud de retour;
}
};

// ---- Exemple de test ----
Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

vecteur<int> parent = {-1, 0, 0, 1, 1, 2, 2};
ArbreAncêtre ta(7, parent);

Cout << ta.getKthAncêtre(3, 1) << '\n'; // 1
Cout << ta.getKthAncêtre(5, 2) << '\n'; // 0
Cout << ta.getKthAncêtre(6, 3) << '\n'; // -1
}
«» "

> **Pourquoi 20 bits? **
> Avec `n <= 50 000`, la puissance la plus élevée de deux est < 2^16. 20 est un "over-kill" sûr qui maintient le code simple tout en garantissant "2^LOG > n".

---

- Oui. 2. Billet de blog – L'enlèvement de lapins en action: le bon, le mauvais, le mauvais

> **Titre:**
> *Maîtriser le problème de l'ancêtre K – Lifting binaire, LeetCode dur et succès d'entrevue*
>
> **Meta Description:**
> Apprenez à résoudre LeetCode 1483 avec levage binaire. Des solutions Java, Python et C++ détaillées, des compromis entre l'espace temporel et des explications prêtes à l'entrevue. Boostez vos compétences d'algorithme d'arbre et décrochez votre prochain rôle d'ingénierie logicielle.

---

2.1 Introduction – Pourquoi l'ancêtre K importe

Les requêtes basées sur l'arbre apparaissent dans chaque interview big-tech : de la navigation du système de fichiers** à la lignage des événements dans les graphiques sociaux**.
Le problème de l'ancêtre K-th est un problème canonique difficile sur LeetCode qui teste:

1. **Graphique traversant** (DFS/BFS).
2. ** Programmation dynamique sur les arbres**.
3. **Manipulation de bits** et ** Astuces de prétraitement**.

> **Conseil de la carrière:**
> *Chaque ingénieur logiciel senior sait que le . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . Maîtrisez-le et vous impressionnerez les gestionnaires d'embauche. *

---

### 2.2 Énoncé du problème (Code de débit 1483)

> **Input**
> * `n`: nombre de nœuds (`1 <= n <= 5 * 104`)
> * `parent[0 ... n-1]`: parent de chaque noeud (`parent[0] = -1` comme racine).
> * `queries`: jusqu'à `5 * 104` appels à `getKthAncestor(node, k)`.
> ** Sortie**
> * Retourner l'ancêtre k de `node` ou `-1` s'il n'existe pas.

> **Exemple**
> ```texte
> parent = [-1, 0, 0, 1, 1, 2, 2]
> getKthAncêtre(3, 1) -> 1
> getKthAncêtre(5, 2) -> 0
> getKthAncêtre(6, 3) -> -1
> `` "

---

### 2.3 Le bien – Pourquoi le levage binaire est un gagnant

Qu'est-ce que ça signifie ?
C'est quoi ?
**O(n log n) prétraitement** Un balayage linéaire par niveau de log – pas cher pour n ≤ 50 000. Autres
**O(log n) temps de la requête** Autres
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
**Conceptuellement simple** Autres
**Dessin réutilisable**Les travaux pour LCA, l'ancêtre, les pointeurs de saut, l'ascenseur binaire – une technique unique pour de nombreux problèmes d'arbres. Autres

---

### 2.4 L'Éclate – Pièges potentiels

Sujet Atténuation
C'est pas vrai.
Pour `n = 5·104`, `LOG = 20` suffit ('2^20 = 1 048 576`). Toujours définir `LOG = =log2 n=1+`. Autres
**Le parent est "-1". En Java et C++, nous nous préservons contre `-1` lors de l'accès `up[mid][i-1]`. Autres
**Les boucles Python pures sont plus lentes; si les limites de temps se resserrent, utilisez PyPy ou Cython. Autres
**Large k**.Le `k` peut dépasser la profondeur; notre boucle frappera un `-1` et un court-circuit. Autres

---

2.5 Le "Ugly" – Quand les choses tournent mal

1. ** Erreurs hors-par-un** – oubliant que `node` pourrait devenir `-1` après un saut.
*Solution:* Ajouter `si (noeud) == -1) retour -1; ' après chaque saut.

2. **L'utilisation `int LOG = 17` pour n=5e4** – échoue pour les arbres plus grands.
*Solution:* Calculer dynamiquement `LOG`:
'`cpp
LOG = 1; pendant ((1 << LOG) <= n) ++ LOG;
«» "

3. **La fragmentation de la mémoire en Java** – «new int[n][LOG]» peut déclencher de grands blocs contigus.
*Solution:* Utiliser `ArrayList<int[]>` ou `int[][]` mais surveiller l'utilisation de tas sur des serveurs réels.

4. **Inefficient E/S** – surtout en C++ lorsqu'il est utilisé dans une compétition de codage.
*Solution:* `ios::sync_with_stdio(false); cin.tie(nullptr);`

---

2.6 Récapitulation de la complexité

Étape Temps Espace
C'est pas vrai.
Pré-traitement **O(n log n)**
Demande de renseignements **O(log n)**
Total (le pire cas)

Pour les contraintes de LeetCode (`n, q ≤ 5 000`), les trois implémentations fonctionnent confortablement dans les délais.

---

- Oui. 3. The Blog Post – L'élévation de la viande : le bon, le mauvais et le mauvais de l'ancêtre K-th

> **Cible Public:**
> • Les candidats à l'entrevue en ingénierie logicielle
> • Ingénieurs seniors cherchant à rafraîchir la connaissance de l'algorithme des arbres
> • Les recruteurs et les gestionnaires d'embauche veulent un rafraîchissement technique rapide

---

3.1 Titre et métadonnées Données

```markdown
# Maîtriser le problème de l'ancêtre K avec le levage binaire – LeetCode 1483, Conseils d'entrevue et Code en Java, Python, C++
Description de la méta: Un guide complet pour résoudre le LeetCode Ancêtre de Kth d'un noeud d'arbre en utilisant le levage binaire. Comprend le code Java, Python et C++, l'analyse de complexité et des explications conviviales.
Mots clés : Ancêtre Kth, levage binaire, ArbreAncêtre, LeetCode Hard, algorithmes d'arbre, entretien d'ingénieur logiciel, ingénieur logiciel senior, entretien technique
«» "

---

### 3.2 Introduction – Le puzzle arbre-ancêtre

> Dans un arbre enraciné, on vous donne un noeud et vous devez trouver son ancêtre **k-th** (l'ancêtre qui se trouve au-dessus des bords de `k`).
> Sur le LeetCode il est **Hard** (1483) parce que l'arbre peut contenir jusqu'à **50 000** noeuds et vous pouvez avoir jusqu'à **50 000** requêtes.
> L'approche naïve de la marche vers les "k" parents est O(k) – beaucoup trop lente.

---

### 3.3 Le bien – Pourquoi le levage binaire gagne

* **Bâtiment de table de passe simple** – Après un DFS/BFS vous pouvez répondre à n'importe quelle requête d'ancêtre dans le temps logarithmique.
* **Déterministe O(log n) runtime** – garantit des performances cohérentes, un must-know pour les systèmes évolutives.
* ** Mémoire compacte** – `n * log n` entiers est une fraction d`un mégaoctet pour les contraintes LeetCode.
* **Modèle réutilisable** – La même table fonctionne pour:
* Ancêtre commun le plus bas
* Les requêtes Jump-pointer dans le jeu AI
* Arbres d'héritage dans les applications d'entreprise

> ** À emporter pour les recruteurs :** Si un candidat peut expliquer le levage binaire, il a maîtrisé un arbre fondamental- Technique de PDD qui s'applique à de nombreux problèmes réels.

---

### 3.4 L'Énorme – Gotchas communs et comment les éviter

Erreurs dans les résultats
- C'est quoi ?
Autres Oublier que le parent racine est "-1" , Erreurs index-out-of-range , définissez "dp[root] [0] = -1` et gardez contre "-1` lors de l'accès à "dp[mid] [i-1]". Autres
Autres Utilisation d'un LOG statique qui est trop petit. Autres
Décomposition de `k` incorrectement. Autres
Autres En Python : compréhensions de liste naïve. Autres

---

### 3.5 Le "Ugly" – Quand votre solution rompt

* ** Grande consommation de cheminée dans DFS** – La profondeur de récursion peut frapper `n`.
*Itérative DFS* ou `sys.setrecursionlimit(1 << 25)' dans Python le résout.

* ** Limites de mémoire sur les serveurs** – Même 1 Mo peut être important si d'autres services fonctionnent simultanément.
*Pack le tableau DP comme `short` si possible ou utiliser un bit-set **compressé** si les profondeurs sont peu profondes. *

* ** Gestion des requêtes parallèles** – Dans un système réel, vous pouvez traiter les requêtes simultanément.
*Solution :* Faites la table DP en lecture seule et cachez le résultat de chaque requête ; aucune condition de course.

---

3.6 Extraits de code (Java, Python, C++)

> Inclure les trois implémentations décrites ci-dessus.

"Java
int[][] up = nouvelle int[n][LOG]; // Java
«» "

'`python
dp = [[-1]*LOG pour _ dans la plage(n)] # Python
«» "

'`cpp
vector<vector<int>> up(n, vector<int>(LOG, -1)); // C++
«» "

> **Pourquoi inclure plusieurs langues? * *
> Les recruteurs posent souvent la question suivante : « Montrez-moi l'algorithme dans votre langue préférée. Démontrer les trois montre une adaptabilité.

---

3.7 Complexité rapide Référence

```markdown
- Prétraitement: O(n log n) temps, O(n log n) espace
- Chaque requête : O(log n) time
- Total: O(n + q) log n) temps
«» "

> **Plot ceci sur un graphique** – vous verrez une ligne quasi verticale de requêtes, ce qui signifie que la performance ne se dégrade pas avec plus de requêtes.

---

#### 3.8 Analogies du monde réel

* ** Hiérarchie des entreprises** – Trouver un gestionnaire « k » au-dessus d'un employé.
* ** Résolution du chemin du système de fichiers** – Localisation des étapes du répertoire `k` au-dessus d'un fichier.
* **Ancêtre de la famille** – Détermination du grand-grand-parent dans les logiciels généalogiques.

> **Pourquoi cela importe aux gestionnaires d'embauche :** De nombreux systèmes de production maintiennent des données hiérarchiques (contrôle d'accès, enregistrement, analyse). Les requêtes d'ancêtres efficaces sont une réalité quotidienne.

---

###3.9 Conclusion – Prochaines étapes pour la réussite des entrevues

1. **Run le code** sur votre machine locale.
2. **Exposer le tableau PDD** : Nous stockons `dp[v][i]` = 2^i-e ancêtre de `v`.
3. **Afficher la décomposition du bit**: Pour grimper les bords de k, nous regardons la représentation binaire de k.
4. **Préparer les variations**: LCA, les requêtes de chemin, ou même trouver le gestionnaire commun le plus bas de l'organigramme d'une entreprise.

> **Débarquer votre rôle :**
> En maîtrisant ce modèle, vous aurez des questions liées aux as, vous vous démarquerez parmi les pairs et vous démontrerez la valeur des recruteurs algorithmiques.

---

#### 3.10 Appel à l'action

> Vous êtes prêt à attaquer LeetCode 1483 ? Essayez les extraits de code ci-dessus, soumettez-les et partagez votre expérience dans les commentaires. Vous voulez plonger plus profondément dans l'arbre DP? Consultez notre série complète sur *Algorithmes Tree pour les ingénieurs logiciels*.

---

- Oui. 4. Liste de contrôle finale

Point terminé
- Oui.
Fournir des implémentations Java, Python, C++ propres
Explication des compromis dans l'espace temporel
Mettre en évidence les idées prêtes à l'entrevue
Inclure les métadonnées pour le référencement
Discutez des pièges et des conseils de débogage

> **Prochain mouvement:** Intégrez ces extraits dans votre repo GitHub. Ajoutez le billet de blog à votre portfolio technique, et vous aurez un point de discussion exceptionnel dans votre prochaine interview.

---