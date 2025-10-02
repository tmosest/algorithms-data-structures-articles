---
titre: LeetCode 1490. Clone Arbre N-ary -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Clone N‐ary Tree – 1490 (Code Leet)
**Bien, mal et mal – une plongée profonde prête au travail**
* Publié 2025 – SEO-optimisé pour la préparation des entrevues et les gestionnaires d'embauche*

---

- Oui. 1. Aperçu du problème

LeetCode 1490 – **Clon N‐ary Tree**
- **Difficulté:** Moyenne
- **Objectif:** Retourner une copie profonde d'un arbre N‐ary.
- **Format d'entrée:** Sérialisation par ordre de niveau avec "null" comme séparateur d'enfant.
- **Constraints:**
- Profondeur ≤ 1000
- Nœuds totaux ≤ 104

> La tâche est essentiellement la même que *Clone Graph* (LC 133) mais avec une structure arborescente.
> Vous pouvez le résoudre avec DFS (récursif ou itératif) ou BFS – tout l'espace auxiliaire O(N) et O(N).

---

- Oui. 2. Pourquoi ce problème est important

Pourquoi les intervieweurs s'occupent-ils?
C'est la première fois que l'on parle d'un problème.
**Récursif vs itératif**= Montre la maîtrise de la gestion de la pile/de la file d'attente et de la manipulation de la base de caisse. Autres
**HashMap / Dictionary** Autres
**Graph vs. Tree** Autres
Autres **L'espace-temps des compromis** Autres

> Résoudre ceci en *toutes les trois langues principales* (Java, Python, C++) indique que vous êtes un codeur complet prêt pour n'importe quelle pile technique.

---

- Oui. 3. L'Élégant DFS récursif –

"Java
/* Java – DFS récursif (propre et idiomatique) */
Numéro de classe {
Int val public;
Liste publique <Node> enfants = nouvelle liste de distribution<>();
Nœud public {}
Nœud public (int _val) { val = _val; }
Noeud public(int _val, Liste <Noe> _enfants) { val = _val; enfants = _enfants; }
}

solution de classe {
publique Clone de nœud Tree(Node root) { retourner dfs(root); }

privé Nœud dfs(nœud cur) {
si (cur == null) retourner null;
clone de nœud = nouveau Node(cur.val);
pour (nœud enfant : cur.enfants) {
clone.children.add(dfs(child));
}
retour du clone;
}
}
«» "

**Pour**
- **Simplicité** – une ligne par étape, facile à raisonner.
- **Espace** – O(H) pile de récursion (H = hauteur de l'arbre).
- **Readability** – parfait pour coder les entrevues.

**Cons**
- La profondeur de récursion peut atteindre la limite de la pile de Javas si l'arbre est très profond (=1000 → sûr, mais toujours un risque dans les langues avec des limites plus strictes).

---

- Oui. 4. L'utilisation inefficace de la carte

"Java
/* Java – Utilisation d'une carte qui recrée des nœuds à chaque fois (O(N2)) */
classe BadSolution {
clone de nœud public Arbre(racine de nœud) {
si (root) null retourne null;
Carte <Node, Node> carte = nouvelle HashMap<>();
clone(racine, carte);
retour map.get(root);
}

clone privé vide(Node cur, Carte <Node, Node> carte) {
si (cur] null) retour;
clone de nœud = map.computeIfAbsent(cur, n -> new Node(n.val));
pour (nœud enfant : cur.enfants) {
clone.children.add(clone(enfant, carte);
}
}
}
«» "

> Le truc "computeIfAbsent" est bien, mais le code force toujours une recherche de carte pour **chaque enfant**, causant un facteur constant O(N2) caché dans le pire des cas.
> **Éviter** dans la production; utiliser la version récursive simple ci-dessus.

---

- Oui. 5. La gestion manuelle des piles en Java

"Java
/* Java – pile manuelle mais toujours O(N) */
classe UglySolution {
clone de nœud public Arbre(racine de nœud) {
si (root) null retourne null;
Carte <Node, Node> carte = nouvelle HashMap<>();
Deque<Node> pile = nouvelle ArrayDeque<>();
pile.push(racine);
map.put(root, nouveau Node(root.val));

pendant que (!stack.isEmpty()) {
Cur du nœud = pile.pop();
pour (nœud enfant : cur.enfants) {
si (!map.contientKey(child)) {
map.put(enfant, nouveau nœud(enfant.val));
pile.push(enfant);
}
mapp.get(cur).children.add(map.get(child));
}
}
retour map.get(root);
}
}
«» "

> Fonctionne bien mais encombre la solution. Dans les entrevues, on préfère généralement une méthode récursive *simple*.
> N'utilisez des versions itératives que lorsque l'intervieweur le demande explicitement.

---

- Oui. 6. BFS – Clone niveau par niveau (Python et C++)

Python

'`python
# Python 3 – Solution BFS (queue)
à partir de collections import deque
de taper l'importation Liste

Numéro de classe:
def __init_(self, val=0, children=None):
autoval = val
enfants = enfants ou []

Solution de classe:
def clone Arbre(même, racine: 'Node') -> 'Noeud':
si ce n'est pas la racine:
retour Aucune

cartographie = {root: Node(root.val)}
q = deque([root])

alors que q:
cur = q.popleft()
pour enfant en cur. enfants:
si l'enfant ne figure pas dans la cartographie:
mapping[child] = Noeud(child.val)
q. annexe(enfant)
mapping[cur].children.append(mapping[child])

retour map[root]
«» "

C++

'`cpp
// C++17 – Solution BFS (queue)
#incluez <vecteur>
#incluez <queue>
#inclut <non-ordonné_map>

utilisant l'espace de noms std;

Numéro de structure {
la valeur intérieure;
vecteur <Node*> les enfants;
Noeud(int _val = 0) : val(_val) {}
};

solution de classe {
public:
Clone de nœud*Race de nœud* {
si (!root) retourne nullptr;
unordered_map<Node*, Node*> mp;
mp[root] = nouveau nœud(root->val);
file d'attente <Node*> q;
q.push(root);

pendant que (!q.vide()) {
Noeud* cur = q.front(); q.pop();
pour (nœud* enfant : cur->enfants) {
si (!mp.count(child)) {
mp[child] = nouveau nœud (enfant->val);
q.push(enfant);
}
[cur]->children.push_back(mp[child]);
}
}
retour mp[root];
}
};
«» "

**Traitements clés**

La langue préférée
- C'est quoi ?
DFS récursif (par défaut)
Python (queue) est plus clair (O(N) temps, O(N) file d'attente)
BFS ou DFS, les deux temps OK (N), mémoire O(N)

---

- Oui. 7. Suivi: des arbres aux graphiques

Si l'entrée était un graphe **dirigé** au lieu d'un arbre, le même motif fonctionne:

- **Maintenir une `carte<originale, clone>`** pour éviter de revisiter les nœuds.
- Traverser avec le DFS/BFS comme d'habitude.
- Oui. La seule différence est que nous **doit** vérifier la carte avant de récurser/copier pour gérer les cycles.

> **Interview Trick:**
> *=Il suffit de copier la logique de l'arbre mais ajouter un ensemble visité. Ça marche aussi pour les graphiques.
> Afficher l'intervieweur que vous comprenez *identité vs valeur*.

---

- Oui. 8. Récapitulation de la complexité du temps et de l'espace

L'approche Temps Espace
- C'est quoi ?
DFS Récursif **O(N)**
Déplacement itératif de la pile DFS
(BFS) **O(N)**

> Pour un arbre équilibré, log N → utilisation de la pile presque linéaire.
> Pour un arbre dégénéré (liste linkée), le H N → est toujours acceptable pour les contraintes données.

---

- Oui. 9. SEO–Friendly Closing: Pourquoi ce blog aide à votre recherche d'emploi

1. **Mot-clé Rich** – Coule N‐ary Tree, Code de leet 1490, Code de leet 1490, Code FDS, Code BFS, Code Java C++.
2. **Interview–Ready** – Couvre *tous* styles de traversée, utilisation de la carte et extension du graphique.
3. **Job-Specific** – Démontre que vous pouvez résoudre un problème d'entrevue canonique *entre les langues*.
4. **Problème–Solving Insight** – Explique pourquoi certaines approches sont « good » ou « bad », un recruteur de compétences qui aime.

> **À emporter :** La maîtrise de ce problème prouve que vous pouvez *deep-clone*, *traverse* et *réutiliser* la logique à travers les structures de données – une caractéristique d'un ingénieur principal de backend.

---

10. Extraits de code complet

> Utilisez les extraits suivants comme référence rapide ou pour copier-coller dans votre IDE.

### Java (DFS récursif)

"Java
Noeud de classe { ... } // comme dans la section 3
classe Solution { ... } // code DFS récursif
«» "

### Java (DFS itératif)

"Java
Solution de classe { ... } // code DFS itératif (section 4)
«» "

### Java (BFS)

"Java
Solution de classe { ... } // Code BFS (section 4)
«» "

### Python (BFS)

'`python
Numéro de classe: ...
Solution: ...
«» "

### C++ (BFS)

'`cpp
Numéro de la structure { ...};
la solution de classe { ... };
«» "

---

## 11. Liste de vérification pour le démarrage rapide

Objet
- Oui.
Rédigez la définition `Node` dans votre langue.
Choisir *DFS* pour des entretiens rapides (Java/Python) ou *BFS* pour plus de clarté (Python/C++).
Utilisez un seul `map/Dictionary` pour stocker le clone original →.
Démontrer l'extension du graphique si demandé.
Test avec des arbres dégénérés (profondeur = 1000) pour confirmer la sécurité de la cheminée.

---

**Codage heureux – et bonne chance pour votre prochaine interview! * *
*(Sentez libre de marquer cette page ou de la partager avec vos collègues candidats.) *