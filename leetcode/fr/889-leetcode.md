---
Titre: LeetCode 889. Construire l'arbre binaire de la précommande et de la postcommande Traversal -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
889. Construire l'arbre binaire à partir de la précommande et de la postcommande Traversal
**Langues:** C++
**Difficulté:** Moyenne
**Entretien prêt:**

---

C'est pas vrai. Mise en œuvre Java

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
public TreeNode constructionFromPrePost(int[] préorder, int[] postorder) {
// Nous maintenons un pointeur mutable à l'index courant en précommande
int[] idx = nouvelle int[]{0};
retour build(précommande, postcommande, idx, 0, postcommande.longueur - 1);
}

build(int[] pre, int[] post, int[] idx,
Int postDémarrage, int postEnd) {
si (idx[0] >= avant.longueur.

// Racine du sous-arbre actuel
racine TreeNode = nouveau TreeNode(pre[idx[0]++]);

// Si ce noeud est une feuille, aucun enfant à attacher
si (postStart == postEnd) retourne root;

// Trouvez l'index de l'enfant de gauche en postcommande
int leftVal = pre[idx[0]];
Int gauche Idx = postStart;
pendant que (post[leftIdx] != gauche Val) gauche Idx++;

Int gauche Taille = gauche Idx - postStart + 1;

// Construire récursivement les sous-arbres gauche et droit
root.left = build(pre, post, idx, postStart, leftIdx);
root.right = build(pre, post, idx, leftIdx + 1, post Fin 1);

retour de racine;
}
}
«» "

---

Mise en œuvre de Python

'`python
# Définition d'un noeud d'arbre binaire.
classe TreeNode:
def __init__(self, val=0, gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
def construction FromPrePost(self, preorder: list[int], postorder: list[int]) -> Numéro d'arbre:
# utilisez une liste comme pointeur mutable dans le précommande
auto.idx = [0]
return self._build(précommande, postcommande, 0, len(postcommande) - 1)

def _build(self, pre, post, post_start, post_end):
si self.idx[0] >= len(pre) ou post_start > post_end :
retour Aucune

racine = TreeNode(pre[self.idx[0]])
[0] += 1

# noeud de feuille – pas d'enfants
si post_start == post_end :
retour de racine

gauche_val = pre[self.idx[0]]
gauche_idx = post_démarrage
pendant que post[left_idx] != _val gauche :
gauche_idx += 1

gauche_size = gauche_idx - post_démarrage + 1

root.left = self._build(pre, post, post_start, left_idx)
root.right = self._build(pre, post, left_idx + 1, post_end - 1)

retour de racine
«» "

---

C++ Mise en œuvre

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
TreeNode* builtFromPrePost(vector<int>& preorder, vector<int>& postorder) {
// Indice de précommande mutable
Int idx = 0;
retour build(précommande, postcommande, idx, 0, postorder.size() - 1);
}

particulier:
TreeNode* build(vector<int>& pre, vector<int>& post, int& idx,
Int postDémarrage, int postEnd) {
if (idx >= pre.size()="postStart > postEnd) retourne nullptr;

TreeNode* racine = nouveau TreeNode(pre[idx++]);

// Noeud des feuilles
si (postStart == postEnd) retourne root;

Int gauche Val = pré[idx];
Int gauche Idx = postStart;
pendant que (post[leftIdx] != gauche Val) + + gaucheIdx;

Int gauche Taille = gauche Idx - postStart + 1;

root->left = build(pre, post, idx, postStart, leftIdx);
root->right = build(pre, post, idx, leftIdx + 1, post Fin 1);

retour de racine;
}
};
«» "

---

Article du blog : Les bons, les mauvais et les méchants
- Oui. **Construire l'arbre binaire en précommande et postcommande – un guide complet pour les entrevues**

---

Table des matières
1. [Introduction et contexte](#introduction)
2. [Présentation du problème](#problème-aperçu)
3. [Pourquoi ce problème compte dans les entrevues](#interview-matières)
4. [Le bon: Pourquoi la solution est belle] (#le bon)
5. [Les mauvaises: pièges communs et l'affaire Gotchas] (#the-bad)
6. [Les cas complexes et comment les démêler] (#the-ugly)
7. [Algorithme et complexité] (#complexité)
8. [Stratégie d'essai et essais unitaires d'échantillons](#test)
9. [A emporter et Conseils de carrière] (#A emporter)
10. [Conclusion] (#conclusion)

---

Introduction et contexte
> **LeetCode 889** – *Construire Binary Tree from Preorder and Postorder Traversal* – est une base d'entretiens techniques, notamment dans les grandes entreprises de technologie et les startups fintech.
> La maîtrise de ce problème démontre que vous pouvez **raisonner avec récursion**, comprendre **propriétés traversales**, et produire des solutions propres, **O(N)** en plusieurs langues.

**Mots clés:** *Code de débit 889*, *Construire l'arbre binaire de la précommande et de la postcommande*, *Reconstruction de l'arbre binaire*, *Entretien de codage*, *Préparation de l'entrevue d'embauche*.

---

### #2-

- **Input:** Deux tableaux entiers: `preorder` (root → gauche → droite) et `postorder` (gauche → droite → racine).
- **Output:** Noeud racine de l'arbre binaire qui correspond aux deux traversées.
- **Constraints:**
- Toutes les valeurs des nœuds sont **unique**.
- Le nombre de nœuds `n` satisfait `1 <= n <= 30` (mais les échelles de solution à plus grande `n`).

> **Pourquoi est-ce dur? * *
> Contrairement à inorder & preorder ou inorder & postorder, vous ne pouvez pas directement mapper les indices des nœuds ; l'arborescence est **pas uniquement définie**. Un arbre valide est toujours garanti car l'entrée est cohérente.

---

C'est vrai. Pourquoi ce problème compte dans les entrevues

Pourquoi il est demandé
- Oui.
De nombreuses personnes interrogées ont du mal à construire des arbres récursifs. Autres
**Cartographie de l'indice** Autres
Autres **Optimisation de l'espace** Autres
**Multi-language Mastery**Les employeurs s'attendent à ce que vous traduisiez des algorithmes entre Java, Python, C++, etc. Autres

> **SEO Boost** – Inclure des phrases comme *=LeetCode 889 solution==* *=question d'entretien d'arbre binaire=* *=interview de codage Java Python C++=* pour obtenir un classement plus élevé dans les résultats de recherche des recruteurs à la recherche de solutions éprouvées.

---

C'est pas vrai. Le bien – ce qui fait Ce problème est grand

Pourquoi il est positif
- Oui.
**Modèle de récursion claire**= Root → divisé en gauche/droite en fonction de la valeur de précommande suivante. Autres
**No Extra Hash Map Needed**= Une simple recherche linéaire en postorder maintient le code lisible. Autres
**Linear Time Complexity** **O(N)**. Autres
**Structure de l'arbre déterministe**= Toute paire de précommande/postorder valide produit *a* l'arbre correct (pas nécessairement unique). Autres
La même logique s'applique en Java, Python, C++, Allez, etc. Autres

**À emporter :** Concentrez-vous sur l'aide *récursive* qui utilise un index de précommande mutable et des limites postcommande. C'est le motif qui rend la solution élégante.

---

C'est vrai. Les mauvaises – Erreurs communes et bords Quirks de cas

Erreurs d'impact
C'est quoi ?
**L'utilisation d'un HashMap pour la valeur → index postcommande**= Ajoute de l'espace supplémentaire à O(N); toujours bon mais inutile pour de petites contraintes. Effectuer un balayage linéaire (`alors que post[i] != pre[idx]`) – fonctionne parce que chaque élément est examiné au plus deux fois. Autres
**Les limites de post-commande incorrectes**Les erreurs hors-par-un produisent des nœuds `NullPointerException` / `Aucun` dans de mauvais endroits. Rappelez-vous que le dernier élément du segment postcommande est la racine courante (`postEnd`). Autres
**En supposant que l'arbre est plein**= Certaines solutions pensent à tort que chaque noeud interne doit avoir deux enfants; cela échoue pour les arbres à inclinaison droite. Vérifier `postStart=postEnd` pour identifier les feuilles. Autres
**Ne pas mettre à jour l'index de précommande après récursion** Utilisez un wrapper mutable (`int[] idx` en Java, `idx[0]` en Python) qui est incrémenté une fois par noeud. Autres
**Éviter de soustraire 1 de postEnd pour le sous-arbre droit**. Utiliser `postEnd - 1` lors de la construction du sous-arbre droit. Autres

> **Conseil de débogage:** Visualisez avec un petit exemple:
> ```texte
> précommande : [1, 2, 4, 5, 3, 6]
> postcommande: [4, 5, 2, 6, 3, 1]
> `` "
> Passez la récursion manuellement pour voir où les indices changent.

---

- Oui. Les cas des arbres et des bords non uniques

Scénario Pourquoi c'est la stratégie de manipulation Ugly
- C'est pas vrai.
Un noeud peut n'avoir qu'un enfant gauche (ou seulement un enfant droit). Dans de tels cas, la taille du sous-arbre gauche est encore déterminée correctement parce que l'enfant gauche est l'élément suivant en précommande. La récursion la gère automatiquement; aucun drapeau spécial n'est nécessaire. Autres
**Tree with All Nodes in One Line (Skewed)**= La précommande et la postcommande sont identiques (par exemple, `[1,2,3]` & `[3,2,1]`). L'algorithme doit encore créer un arbre à droite valide. L'état de la feuille `postStart=postEnd` arrête la récursion, en préservant la forme asymétrique. Autres
**Empty Input** Ajouter un garde si (prélongueur) 0) retour nul;». Autres
Autres **Grande entrée (n > 30)**= Les données réelles d'entrevues peuvent être plus grandes; l'utilisation de `tout en trouvant l'indice dans l'ordre peut devenir \(O(N^2)\) si elle est mise en œuvre naïvement. Construire un hashmap `value -> index` une fois pour la recherche O(1), atteindre vrai O(N). Pour les contraintes moyennes (-30), le balayage linéaire est parfaitement fin. Autres

---

#### 7-

Langue Heure Espace
- C'est quoi ?
**O(N)** – Chaque noeud est traité une fois; un balayage linéaire de la postcommande se produit O(1) par niveau de récursion. Autres
Python **O(N)**** **O(N)** – Profondeur de récursion et indice mutable. Autres
C++. **O(N)**. **O(N)** – Profondeur de la pile ; chaque création de nœud est un temps constant. Autres

> **Proof d'optimalité:**
> - L'accroissement de l'indice de précommande est constant par noeud.
> - Les scans postcommande s'arrêtent à l'enfant gauche, ce qui est unique.
> - Pour les arbres biaisés, profondeur de récursion = `N`; pour les arbres équilibrés = `O(log N)`.

---

### 8--Stratégie d'essai et essais unitaires

'`python
def inorder(root):
si non racine: retourner []
retour inorder(root.left) + [root.val] + inorder(root.right)

def test_pre_post(pre, post):
racine = Solution()._build(pre, post, 0, len(post)-1)
indorder(root) == trié(pre) # pas utile, juste vérification de la santé
# Construire l'arbre attendu manuellement pour le petit cas:
# 1
Numéro / \
# 2 3
Numéro / \
# 4 5
# ...
«» "

> **Idée de test automatisée:**
> - Générer des valeurs uniques aléatoires.
> - Construire un arbre binaire aléatoire.
> - Calculez sa précommande & postcommande.
> - Alimentation pour solveur; puis vérifier `preorder(root)` et `postorder(root)` correspondent aux originaux.

> **Pourquoi ça aide les recruteurs :** Démontre la capacité de *valider* des solutions programmatiques, une compétence cruciale dans les revues de code de production.

---

#####=" À emporter et carrière– Conseils pour booster

1. **Entre les langues:** Afficher les recruteurs vous pouvez implémenter la même logique en Java, Python et C++ en une seule interview.
2. ** Expliquer votre récursion :** Toujours verbaliser la logique *index de précommande* et * segment de postcommande*.
3. **Efficacité de l'espace :** Mention que vous pouvez ajouter un hashmap pour la recherche d'index O(1), mais que vous avez opté pour une solution plus simple compte tenu des contraintes.
4. **Afficher le code de l'échantillon dans le curriculum vitae:** Ajouter une balle : *LeetCode 889 en Java, Python et C++ avec une complexité O(N). *
5. **Cas de bord des pratiques:** Des nœuds à droite, à gauche, à un seul enfant et des arbres de taille minimale.

> **Resume Hook:** L'algorithme de reconstruction binaire efficace du LeetCode 889 en Java, Python et C++ permet d'atteindre la complexité linéaire du temps et de l'espace. (en milliers de dollars)

---

Conclusion

Maîtrise **LeetCode 889** vous équipe d'une boîte à outils **récursion + cartographie d'index** qui est hautement transférable dans les entrevues de codage.

- **Le Bon** – Récursion propre, temps linéaire, langage-agnostique.
- **Le mauvais** – Attention aux limites et aux mises à jour d'index manquantes.
- **The Ugly** – Poignez avec grâce des arbres non uniques.

> En pratiquant le modèle ci-dessus, vous non seulement résoudre le problème, mais aussi signaler aux recruteurs que vous êtes à l'aise ** abstraction des concepts dans les langues**, **optimisation de l'espace**, et **debugging recursion complexe**.

**Votre prochaine étape:** Construisez un petit outil en ligne de commande qui accepte deux tableaux et imprime l'arborescence dans l'ordre de niveau; incluez-le dans votre site Web de portefeuille ou GitHub readme pour présenter votre solution en direct aux gestionnaires d'embauche.

---

**Codage heureux!**

> * Prêt pour votre prochain entretien ? Plongez dans les solutions, lancez-les sur votre IDE préféré, puis poussez votre repo à GitHub avec des messages de commit clairs. Les recruteurs aiment les solutions de problèmes visibles et bien documentées. *

---



---

> **Disclaimer:** Les extraits de code ci-dessus sont entièrement compilables dans leurs environnements respectifs (Java 17+, Python 3.10+, C++17). Vérifiez toujours le problème LeetCode pour toutes les contraintes cachées avant de soumettre.

---