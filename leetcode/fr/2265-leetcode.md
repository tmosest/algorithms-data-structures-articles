---
titre: LeetCode 2265. Nombre de nœuds égal à la moyenne du sous-arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2265 – Nombre de nœuds égaux à la moyenne du sous-arbre
**Code de la solution (Java / Python / C++)**

---

Le problème (Code de bord 2265)

> **Don** un arbre binaire, **compte** le nombre de nœuds dont la valeur est égale au *floor* de la moyenne de toutes les valeurs de nœuds dans son sous-arbre (y compris le nœud lui-même).

- `moyenne = - (somme des valeurs) / (nombre de nœuds) "
- Taille de l'arbre: `1 ... 1000`
- `0 ≤ Node.val ≤ 1000`

---

- Oui. Idée de base – DFS après la commande

Pour chaque nœud dont nous avons besoin :
1. **Sum** de son sous-arbre
2. **Count** de nœuds dans son sous-arbre

Un **post-ordre** (gauche → droite → noeud) traversal nous donne ces deux chiffres pour les enfants *avant* les calculant pour le parent.
Une fois que nous avons `(somme, nombre)` pour un noeud, nous pouvons vérifier:

Texte
si (somme / nombre == node.val) → réponse par incrément
«» "

Cela donne un temps de passage unique O(N), O(H) pile de récursion (H = hauteur de l'arbre, ≤ N).

---

- Oui. Code

Voici des solutions propres et prêtes à la production pour **Java**, **Python** et **C++**.
Tous utilisent la même stratégie DFS et sont prêts à coller dans LeetCode.

---

#### 3.1 Java

"Java
***
* Définition d'un noeud d'arbre binaire.
* classe publique TreeNode {
* Int val;
* TreeNode gauche;
* TreeNode droit;
* TreeNode() {}
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode gauche, TreeNode droite) {
* ce.val = valeur;
* ce.gauche = gauche;
* ce droit = droit;
*}
*}
*/
solution de classe {
réponse interne privée = 0;

***
* Renvoie un tableau : [somme du sous-arbre, nombre de nœuds].
*/
Int[] dfs (noeud TreeNode) {
si (node == null) retourne une nouvelle int[]{0, 0};

int[] gauche = dfs(node.gauche);
int[] droite = dfs(node.right);

somme int = gauche[0] + droite[0] + noeud.val;
nombre int = gauche[1] + droite[1] + 1;

si (somme / nombre == node.val) réponse++;

retourner une nouvelle int[]{sum, compter};
}

moyenne De sous-arbre(racine de node d'arbre) {
dfs(racine);
réponse de retour;
}
}
«» "

---

3.2 Python

'`python
# Définition d'un noeud d'arbre binaire.
# classe TreeNode:
# def __init_(self, val=0, gauche=Aucune, droite=Aucune):
# Self.val = val
Moi-même. gauche = gauche
Moi-même. droite = droite

Solution de classe:
moyenne DeSubtree(même, racine: TreeNode) -> Int:
total = 0

def dfs(node):
si ce n'est pas le nœud:
retour 0, 0 # (somme, noeuds)

gauche_sum, gauche_cnt = dfs(node.left)
right_sum, right_cnt = dfs(node.right)

total_sum = gauche_sum + droite_sum + noeud.val
total_cnt = gauche_cnt + droite_cnt + 1

Si total_sum // total_cnt == node.val:
nombre d ' individus 1

retourner total_sum, total_cnt

dfs(racine)
Revenez vous-même. Nombre
«» "

---

### 3.3 C++

'`cpp
***
* Définition d'un noeud d'arbre binaire.
* struct TreeNode {
* Int val;
* TreeNode * gauche;
* TreeNode *right;
* TreeNode(int x) : val(x), gauche(nullptr), droite(nullptr) {}
* };
*/
solution de classe {
public:
Int ans = 0;

// Paire de retour : {somme, nombre}
couple <long long, int> dfs(noeud TreeNode*) {
si (!node) retourne {0, 0};

auto [sumL, cntL] = dfs(node->gauche);
auto [sumR, cntR] = dfs(node->right);

long total long Somme = somme + somme + noeud->val;
Total Cnt = cntL + cntR + 1;

si (totalSum / totalCnt == noeud->val) ++ans;

retour {total Total Cnt};
}

moyenne int De sous-arbre(racine TreeNode*) {
dfs(racine);
le retour des an;
}
};
«» "

> **Pourquoi "long" en C++? **
> `sum` peut être jusqu'à `1000 * 1000 = 1e6`, s'inscrit toujours dans `int`, mais en utilisant `long` garde la mise en œuvre à l'épreuve du futur.

---

Article de blog (optimisé par le référencement)

> **Titre:**
> * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
> *Une plongée profonde dans la SDD, les causes de bord et les astuces d'entrevues

> **Désignation de la méta (=160 caractères):**
> Résoudre le LeetCode 2265 en Java, Python & C++ avec un seul passage DFS. Comprendre l'algorithme, la complexité, les pièges et la façon de répondre à cette question d'entrevue binaire.

---

4.1 Introduction

Lors des entrevues de codage, les problèmes d'arbre binaire dominent le paysage.
LeetCode 2265 – *Count Nodes Equal to Medium of Subtree* – est une étoile moyenne qui mélange les techniques de traversée avec le raisonnement arithmétique.

> **Pourquoi c'est important:**
> • Démontre la maîtrise de la première recherche en profondeur (DFS).
> • Affiche la capacité de travailler avec les données agrégées (somme & nombre).
> • Teste l'attention à la division entière et l'arrondi.

Laissez-vous casser le problème, marcher à travers une solution optimale, explorer les pièges, et terminer par le code complet en **Java, Python, C++**.

---

4.2 Récapitulation des problèmes (points clés)

Point de détail
- C'est quoi ?
**Objectif**=Compte des nœuds où `node.val=="sum(subtree)/count(subtree)=". Autres
**Constances**
**Taille de l'arbre** Autres

---

#### 4.3 – Pourquoi le DFS après l'ordre Gagner

1. **Agrégation du bas vers le haut**
- La post-commande garantit que nous connaissons les sommes des enfants avant de calculer les parents.
- Pas besoin de structures de données auxiliaires (comme les files d'attente).

2. **Complexité temporelle et spatiale**
- **O(N)** temps – chaque noeud traité une fois.
- **O(H)** cheminée de récursion – H est la hauteur (= N, mais dans les arbres équilibrés = log N).

3. **Simplicité**
- Une fonction récursive renvoie un tuple `(somme, nombre)`.
- Immédiatement utilisable pour mettre à jour la réponse globale.

> **Ligne de bottom:** *Un seul laissez-passer DFS vous donne toutes les informations dont vous avez besoin. *

---

### 4.3 Étape par étape (Code Pseudo)

«» "
DFS(nœud):
si le nœud est nul:
retour (somme = 0, nombre = 0)

gauche Somme, gaucheCnt = DFS(node.gauche)
rightSum, rightCnt = DFS(node.right)

Total général Somme = gaucheSum + droite Somme + noeud.val
Total général Nombre = gauche Cnt + droite Cnt + 1

Si totalSum // total Compte == noeud.val:
réponse += 1

retour (totalSum, totalCount)
«» "

**Avis:** `/` (ou `/` dans des langues entières) exécute exactement la division minimale*, ce que le problème exige.

---

#### 4.4 – Pièges communs et comment les éviter

Pourquoi c'est mauvais
- C'est quoi ?
**L'utilisation de pré-commande**= Vous devez connaître les sommes d'enfants → doubles passes ou stockage temporaire. Utiliser le SSD après la commande. Autres
**Intégrement du débit**Summing 1000 nœuds de valeur 1000 → 1.000.000 (s'adapte en 32-bit), mais dans les entrées plus grandes ou d'autres problèmes cela peut déborder. Utiliser 64-bit (`long long` en C++ / `long` en Java) pour la sécurité. Autres
**Somme / compte" par rapport à `somme // compte`. Autres
Autres **Manipulation des nœuds nulls**.Returning `null` sans fond → `NullPointerException`. Autres
Autres **Profondeur de la pile**= Arbre profondément déséquilibré (par exemple, liste liée) → profondeur de récursion ~ N.= soit utiliser la pile itérative ou augmenter la limite de récursion dans Python. Autres

---

#### 4.5 - Scénarios de bord et de coin

1. **Tree avec toutes les valeurs égales* *
- La moyenne de chaque noeud est égale à la valeur du noeud → réponse = N.
2. **Arbre asymétrique (liste liée)* *
- Hauteur = N → profondeur de récursion = N. Dans Python, vous pouvez avoir besoin de `sys.setrecursionlimit(2000)`; dans Java/C++ récursion fonctionne bien pour N = 1000.
3. **Valeur du nœud 0**
- La moyenne peut également être 0 – aucune manipulation spéciale nécessaire, mais assurez-vous que la division par zéro ne se produit jamais.
4. ** Grandes valeurs* *
- Même si `val ≤ 1000`, le cumul de 1000 nœuds s'adapte toujours en 32 bits, mais dans les tests personnalisés avec des contraintes plus grandes, vous devriez promouvoir à 64 bits.

---

### 4.6 Entretien– Conseils prêts

Pourquoi ça aide ?
C'est quoi ?
**Exposer l'idée post-commande** avant de plonger dans le code. Montre que vous comprenez pourquoi les enfants sont traités en premier. Autres
**Contestation** précoce. Autres
Autres **Parler de la division entière**: "la division plancher est la par défaut dans les langues entières". Faits saillants des connaissances linguistiques. Autres
**Profondeur de la cheminée de Mention** : « pire cas O(N), mais les arbres équilibrés sont O(log N) ». Autres
**Fournir des cas de test** (par exemple, un seul noeud, toutes les mêmes valeurs, arbre biaisé). Démontre la rigueur. Autres

---

### 4.7 Code de référence complet (Java / Python / C++)

> *Les extraits de code ci-dessous sont entièrement commentés et prêts à être copiés dans LeetCode. *

C'est vrai. Java

"Java
solution de classe {
réponse interne privée = 0;
Int[] dfs (noeud TreeNode) {
si (node == null) retourne une nouvelle int[]{0, 0};
int[] gauche = dfs(node.gauche);
int[] droite = dfs(node.right);
somme int = gauche[0] + droite[0] + noeud.val;
nombre int = gauche[1] + droite[1] + 1;
si (somme / nombre == node.val) réponse++;
retourner une nouvelle int[]{sum, compter};
}
moyenne De sous-arbre(racine de node d'arbre) {
dfs(racine);
réponse de retour;
}
}
«» "

Python

'`python
Solution de classe:
moyenne DeSubtree(même, racine: TreeNode) -> Int:
total = 0
def dfs(node):
si non noeud: retour 0, 0
gauche_sum, gauche_cnt = dfs(node.left)
right_sum, right_cnt = dfs(node.right)
total_sum = gauche_sum + droite_sum + noeud.val
total_cnt = gauche_cnt + droite_cnt + 1
Si total_sum // total_cnt == node.val:
nombre d ' individus 1
retourner total_sum, total_cnt
dfs(racine)
Revenez vous-même. Nombre
«» "

C++

'`cpp
solution de classe {
public:
Int ans = 0;
couple <long long,int> dfs(nœud TreeNode*){
if(!node) retourne {0,0};
auto [sumL, cntL] = dfs(node->gauche);
auto [sumR, cntR] = dfs(node->right);
long total long Somme = somme + somme + noeud->val;
Total Cnt = cntL + cntR + 1;
if(totalSum/total Cnt == noeud->val) +ans;
retour {total Total Cnt};
}
moyenne int De sous-arbre(racine TreeNode*){
dfs(racine);
le retour des an;
}
};
«» "

---

4.8 Essais et validation

Autres Test de l'arbre Réponse attendue
- Oui.
**Nœud unique**
**Tous égaux**= Arbre équilibré de tous les `1`s=" `N` (tous les nœuds correspondent)=
**Écrochés**
**Mélangé**

L'exécution du code contre ces tests confirme l'exactitude et ne révèle aucun bug caché.

---

4.9 Pensées finales

- **Bonne** – Un SSD à un liner qui capture deux agrégats par noeud; solution O(N) propre.
- **Bad** – La suringénierie avec des structures de données supplémentaires ou des passes doubles gaspille le temps et la mémoire.
- **Ugly** – Oublier la division entière (par exemple, utiliser `double` au lieu de `int`) donnera WA sur les tests cachés.

Souvenez-vous : **Les problèmes d'entrevues binaires sont tout au sujet des modèles de traversée**. La maîtrise du DFS et de l'agrégation post-commande vous donne un outil puissant qui s'applique à d'innombrables problèmes de LeetCode (p. ex.

---

C'est vrai. Clôture

> Avec les solutions ci-dessus, vous pouvez soumettre avec confiance LeetCode 2265 en **Java, Python ou C++**, et vos intervieweurs vous verront:

- Code écrit propre et à jour
- Boîtes de bord manipulées et arrondis entiers correctement
- Optimisé pour le temps et l'espace

Maintenant, préparez-vous pour votre prochaine interview de codage – hit -Solve-sur LeetCode 2265, obtenez ce badge **-- et laissez les intervieweurs être impressionnés!

---

Ressources utiles

Lien
C'est quoi, ça ?
LeetCode 2265 – Problème Autres
Tutoriel de la DFS (Java) Autres
Les bases de l'arbre binaire https://www.tutorialspoint.com/data_structures_algorithms/binary_tree.htm Autres
Préparation de l'entrevue Autres

---

* Codage heureux! *