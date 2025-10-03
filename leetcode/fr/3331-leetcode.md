---
titre: LeetCode 3331. Trouver des tailles de sous-arbres après les changements -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* 3331. Trouver les dimensions du sous-arbre après les changements – Code complet (Java / Python / C++) + SEO-Optimized Blog Post

---

### TL;DR
- **Problème** – Reparent chaque nœud à l'ancêtre le plus proche ayant le même caractère et retourne la taille de chaque sous-arbre dans le nouvel arbre.
- **Solution** – Deux traversées en profondeur.
1. **DFS1** – En marchant sur l'arbre original, conservez l'indice *dernier vu* pour chaque personnage. Si un index précédent existe, ce nœud devient le nouveau parent.
2. **DFS2** – Créer une nouvelle liste d'adjacence avec les parents mis à jour et compter les tailles de sous-arbres dans un autre DFS post-commande.
- **Complexité** – **O(n)** temps, **O(n)** espace.
- **Langues** – Java, Python, C++ – prêtes à copier-coller dans votre IDE ou LeetCode.

---

- Oui. 1. Le Code

> C'est vrai. Profondeur de récursion** – L'entrée peut contenir jusqu'à \(10^5\) nœuds.
> En Java / C++, la pile par défaut gère habituellement cela, mais en Python, vous devez bloquer la limite de récursion (ou utiliser un DFS itératif).

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe {
public int[] findSubtreeSizes(int[] parent, Chaîne s) {
int n = longueur parent;
Liste <entier>[] enfants = nouvelle liste de répartition;
pour (int i = 0; i < n; i++) les enfants[i] = nouvelle liste de distribution<>();

// Construire la liste d'adjacence originale
pour les enfants [parent[i]].add(i);

int[] newParent = parent.clone(); // tiendra les parents mis à jour
int[] lastSeen = nouveau int[26];
Arrays.fill(dernière vue, -1);

// DFS1 – trouver de nouveaux parents
dfsParent(0, s.toCharArray(), enfants, lastSeen, newParent);

// Construire une nouvelle liste d'adjacence à partir du nouveauParent
Liste <entier>[] nouveauxEnfants = nouvelle liste de répartition[n];
pour (int i = 0; i < n; i++) nouveauxenfants[i] = nouvelle liste de distribution<>();
pour (int i = 1; i < n; i++) nouveauxenfants[newParent[i]].add(i);

réponse int[] = nouvelle réponse int[n];
dfsSize(0, nouveaux enfants, réponse);
réponse de retour;
}

vide privé dfsParent(int node, char[] chars, liste<entier>[] enfants,
int[] lastSeen, int[] newParent) {
int idx = chars[node] - 'a';
int prev = lastSeen[idx];
si (prév != -1) newParent[node] = prev; // nouveau parent trouvé

lastSeen[idx] = noeud; // courant de poussée
pour (int enfant : enfants[node]) {
dfsParent(enfant, chars, enfants, lastSeen, nouveauParent);
}
lastSeen[idx] = prev; // pop / restorer
}

int privé dfsSize(int node, Liste<integer>[] enfants, int[] ans {
int sz = 1;
pour (int enfant : enfants[node]) {
sz += dfsSize(enfant, enfants, ans);
}
ans[node] = sz;
retour sz;
}
}
«» "

---

#### 1.2 Python

'`python
importations
sys.setrecursionlimite(200000) # requis pour les arbres profonds

Solution de classe:
def findSubtreeSizes(self, parent: list[int], s: str) -> list[int]:
n = len(parent)
enfants = [[] pour _ dans l'intervalle(n)]
pour i dans la plage (1, n):
enfants[parent[i]].appendice(i)

new_parent = parent[:] # copie des parents originaux
last_seen = [-1] * 26

def dfs_parent(u: int):
idx = ord(s[u]) - ord('a')
prev = last_seen[idx]
si prev != - 1 :
nouveau_parent[u] = prev
last_seen[idx] = u
pour v chez les enfants[u]:
dfs_parent(v)
last_seen[idx] = prev

Dfs_parent(0)

# Construire une nouvelle dépendance
new_children = [[] pour _ in range(n)]
pour i dans la plage (1, n):
nouveaux_enfants[nouveau_parent[i]].annexe(i)

réponse = [0] * n

def dfs_size(u: int) -> Int:
sz = 1
pour v in new_children[u]:
sz += dfs_size(v)
réponse[u] = sz
retour sz

dfs_size(0)
réponse de retour
«» "

---

*## 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findSubtreeSizes(vector<int>& parent, chaîne s) {
int n = parent.size();
vecteur<vecteur<int>> enfants(n);
pour les enfants [parent[i]].push_back(i);

vecteur<int> nouveau parent = parent; // copie
vecteur<int> lastSeen(26, -1);

fonction<vit(int)> dfsParent = [&](int u) {
int idx = s[u] - 'a';
int prev = lastSeen[idx];
si (prév != -1) nouveauParent[u] = prev;
lastSeen[idx] = u;
pour (int v: children[u]) dfsParent(v);
lastSeen[idx] = prev; // restaurer
};
dfsParent(0);

// Construire une nouvelle liste d'adjacence
vector<vector<int>> newChildren(n);
pour (int i = 1; i < n; ++i) nouveauxenfants[newParent[i]].push_back(i);

vecteur<int> réponse(n);

fonction<int(int)> dfsSize = [&](int u) -> Int {
int sz = 1;
pour (int v: newChildren[u]) sz += dfsSize(v);
réponse[u] = sz;
retour sz;
};
dfsSize(0);
réponse de retour;
}
};
«» "

---

- Oui. 2. Le billet de blog – *Faire exploser votre score d'entrevue! *

> *Ce billet est écrit pour les candidats qui veulent maîtriser les problèmes d'arbre LeetCode, clouer leur prochaine interview, et obtenir un emploi dans une entreprise de haute technologie. *
> Utilisez l'en-tête « Trouver les tailles du sous-arbre après les changements » et le mot clé « LeetCode 3331 » dans votre moteur de recherche pour une visibilité instantanée.

---

Titre
> LeetCode 3331 – Trouver des tailles de sous-arbres après les changements : maîtriser le problème de l'arbre DFS *

### 2.2 Méta-Description (SEO)
> * Apprenez à résoudre le LeetCode 3331 – Trouver les dimensions du sous-arbre après les changements – avec les solutions Java, Python et C++, plus une explication approfondie du DFS, de la recomposition des arbres et du calcul de la taille. *

2.3 Article complet

> **Mots clés**: LeetCode 3331, trouver les tailles de sous-arbres après les changements, les problèmes d'arbre, DFS, tableau parent, Java, Python, C++, entretien de codage, conception d'algorithmes, structures de données, entretien d'emploi, entretien d'ingénierie logicielle, questions d'entrevue, défi de codage.

---

3331 – Quel est le problème en fait?

Vous êtes donné un arbre enraciné comme un tableau **parent** `parent[i]` (la racine a `-1`) et une chaîne `s` où `s[i]` est le caractère du noeud `i`.
Pour chaque nœud `x` (sauf la racine) vous devez **re-parent** le à l'ancêtre le plus proche** qui détient le même caractère.
Après que tous les nœuds se sont déplacés, vous retournez un tableau `ans` où `ans[i]` égale le nombre de nœuds dans le sous-arbre enraciné au nœud `i` ** dans le nouvel arbre**.

---

Principales observations

1. **La structure de l'arbre est connue par un tableau parent. **
Convertir cela en une liste d'adjacence ("children") est trivial: pour chaque `i > 0`, ajouter `i` à `children[parent[i]]`.

2. **Trouver l'ancêtre du même personnage est un trick classique du DFS. **
En explorant l'arbre que vous conservez, pour chaque personnage, le dernier nœud que vous avez visité ('lastSeen').
Lorsque vous arrivez à un nœud `u`, si `lastSeen[char] != -1' cela signifie qu'il y a un ancêtre *précédent* avec le même char, et *parce que nous faisons une première marche en profondeur*, que l'index précédent est automatiquement le plus proche.

3. **Après avoir mis à jour tous les parents, vous pouvez traiter le nouvel arbre comme n'importe quel autre arbre. **
Construisez une nouvelle liste d'adjacence (`newChildren`) à partir du tableau `newParent` mis à jour et effectuez un DFS post-commande pour compter les tailles de sous-arbres.

---

L'algorithme des deux FDS

Étape Ce qu'il fait Pourquoi il fonctionne
- C'est quoi ?
**DFS1**"dfsParent(node)` <br> *Maintient* `lastSeen[26]` (index du nœud le plus récent pour chaque caractère). <br> *Si* un index précédent existe, set `newParent[node] = lastSeen[char]`. Autres
**Pour chaque enfant `i > 0`, insérer `i` dans `enfants[newParent[i]]`. Autres
**DFS2**DfsSize(node)» – DFS post-commande qui retourne la taille du sous-arbre. Trick post-commande classique : taille du nœud = 1 + somme des tailles de ses enfants. Autres

---

Pourquoi C'est efficace

Résultats
C'est quoi ?
**Temps**= Chaque noeud est visité deux fois – une fois en DFS1 et une fois en DFS2. \(O(n)\). Autres
**Liste d'adjacence, tableaux parent, `lastSeen` et `ans` – tous \(O(n)\). Autres
L'algorithme n'a besoin que d'un entier par caractère ('lastSeen[26]'). Pas de structures de données lourdes. Autres

---

- Oui. 3. Comment utiliser ceci dans une entrevue

Question: Comment la réponse aide
- C'est quoi ?
Expliquez votre solution en 2-min. Autres
Quelle est la période la plus défavorable? Autres
Autres Pourriez-vous écrire ceci dans Python ? Fournir le code Python ci-dessus et mentionner la limite de récursion. Autres
Qu'en est-il du DFS itératif ?Vous pouvez remplacer la récursion par une pile explicite si vous préférez. Autres

---

- Oui. 4. Liste de contrôle pour le démarrage rapide

1. **Copier** le bloc linguistique qui correspond à votre environnement.
2. **Paste** dans l'éditeur de LeetCodes ou votre IDE local.
3. **Run** sur les tests d'échantillonnage.
4. **Ajouter** vos propres boîtiers personnalisés (chaînes profondes, arbres équilibrés, mêmes caractères, caractères différents).
5. **Soumettre** – vous serez accepté dans le premier aller!

---

- Oui. 5. SEO-Optimized Blog Wrap‐ En haut

> **Titre:** *LeetCode 3331 – Trouver des tailles de sous-arbres après les changements: DFS Reparantage des arbres en Java, Python et C++ *
> **Méta—Description:** *Master LeetCode 3331 (Trouver les tailles du sous-arbre après les changements) avec des solutions complètes Java, Python et C++, une explication étape par étape DFS, et des idées prêtes à l'entrevue. *

Pourquoi lire ça vous aide à trouver un emploi

- **Deep DFS Mastery** – La plupart des entretiens testent la traversée de l'arbre. Ce problème démontre comment maintenir l'état ("lastSeen") en marchant sur un arbre.
- **Parent‐Array à l'adjacence** – La conversion entre représentations est un tour d'interview commun.
- **Analyse de complexité claire** – Démontrer \(O(n)\) espace/temps montre que vous pouvez raisonner sur les asymptomes à la volée.
- ** Flexibilité linguistique** – Connaître le même algorithme en trois langues indique aux intervieweurs que vous comprenez *concept* sur *syntax*.

---

À emporter

Si vous avez déjà regardé le tableau parent, senti comment traverser l'arbre, ou inquiet des limites de récursion, le code et l'explication ci-dessus vous donnent un plan à l'épreuve des bulles**.

Utilisez-le, testez-le et expliquez-le dans votre prochain entretien. Vous allez démontrer :

- **La pensée algorithmique** – deux passes, un minimum de mémoire supplémentaire.
- **Discipline de codage** – séparation nette des préoccupations (mise à jour parentale par rapport au calcul de la taille).
- **Les versions Java, Python et C++ sont adaptables.

Bon codage, et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit