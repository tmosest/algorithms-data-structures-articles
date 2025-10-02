---
titre: LeetCode 428. Serialize et Desérialize N-ary Tree -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 428. Serialize and Desérialize N‐ary Tree
> **LeetCode Hard-Interview Prêt**

---

- Oui. 1. Aperçu du problème

Dans un arbre N-ary enraciné chaque noeud peut avoir un nombre arbitraire d'enfants (jusqu'à **N**).
La tâche consiste à ** convertir l'arbre entier en une chaîne** (`serialize`) et ensuite ** re-construire le même arbre exactement de cette chaîne** (`desérialize`).

- **Input**: `root` – pointeur/référence à la racine d'un arbre N-ary (peut être `null`).
- ** Sortie**:
* `serialize(root)` → `String` qui représente uniquement l'arbre.
* `désérialize(data)` → `Node` qui est bit-for-bit identique à l'arbre original.

**Principales contraintes**

Valeur
- Oui.
*Nœuds* Autres
* Gamme de valeur* Autres
*Pas d'état global/statique * Chaque appel doit être **absolue**. Autres
*Temps*=Linéaire dans le nombre de nœuds. Autres
*Space*=O(nombre de nœuds) pour la chaîne de sortie. Autres

---

- Oui. 2. Pourquoi ce problème importe

* **Agrafe d'entrevue** – De nombreux intervieweurs de niveau supérieur demandent un truc pour les arbres, les listes liées, les graphiques, etc.
* **LeetCode 428** fait partie des collections de l'Arbre Binaire et du Design, et il apparaît dans l'ensemble emploi-prép de l'arbre.
* La maîtrise de ce problème démontre une bonne compréhension de la récursion, des techniques de traversée et de la manipulation soigneuse des cordes – toutes les compétences de base pour les rôles centrés sur l'algorithme (ingénieur logiciel, ingénieur de backend, ingénieur de données, etc.).

---

Stratégies de solution

Voici les trois modèles les plus courants** que vous verrez dans les solutions d'entretien de production:

Motif Ce qu'il fait
C'est pas vrai.
**Depth‐First Search (DFS) avec le nombre d'enfants**= `val childCount <children‐DFS>=== *Simple, pas de symboles sentinelles supplémentaires.*= Nécessite une manipulation attentive de l'index lors de l'analyse. Autres
**Breadth‐First Search (BFS) avec sentinelle nulls**="val childCnt child1 child2 ... null ...="=" *Itérative, facile à comprendre. Il faut se rappeler où se termine chaque liste d'enfants. Autres
**Format personnalisé avec délimiteurs** *Très compact, pas d'espaces nécessaires. Autres

Ci-dessous, nous implémentons le modèle **DFS + child-count** dans **Java, Python et C++** – la manière la plus propre, la plus rapide et la plus sûre de répondre aux contraintes du problème.

---

## 3-Mise en œuvre des langues

> **Les trois codes sont apatrides, O(1) espace auxiliaire (à l'exception de la pile de récursion), et garantis pour reconstruire exactement le même arbre. **

### 3.1 Solution Java

"Java
Importation de java.util.*;

// LeetCode Définition du nœud
Numéro de classe {
Int val public;
liste publique <Node> des enfants;

Nœud public() {ceci.enfants = nouvelle liste de distribution<>(); }

Nœud public (int val) {
ce.val = valeur;
Ça. enfants = nouvelle liste de répartition<>();
}

Nœud public(int val, Liste < Nœud> enfants) {
ce.val = valeur;
Ça. enfants = enfants;
}
}

Codec {

/** Encode un arbre N‐ary à une seule chaîne. */
chaîne publique serialize(Node root) {
if (root == null) retourner "; // null arbore → chaîne vide
StringBuilder sb = nouveau StringBuilder();
dfsEncode(root, sb);
retour sb.toString();
}

vide privé dfsEncode(Node node, StringBuilder sb) {
sb.append(node.val).append('); // valeur du noeud
sb.append(node.children.size())append('); // nombre d'enfants
pour (nœud enfant : nœud enfants) {
dfsEncode(enfant, sb); // encoder récursivement chaque enfant
}
}

*** Décodes vos données encodées à l'arborescence. */
public Node désérialize(Données de positionnement) {
si (data.isEmpty()) retourne null; // chaîne vide → arborescence null
Chaîne[] jetons = data.split("\\s+");
indice int[] = {0}; // porte-indice mutable
retourner dfsDecode(tokens, index);
}

privé Node dfsDecode(String[] jetons, index int[]) {
int val = Integer.parseInt(tokens[index[0]++]); // lire la valeur du nœud
enfant Nombre = Integer.parseInt(tokens[index[0]++]); // lire nombre d'enfants
noeud = nouveau noeud (val);
node.children = nouvelle station <>();
pour (int i = 0; i < childCount; ++i) {
node.children.add(dfsDecode(tokens, index));
}
noeud de retour;
}
}
«» "

> **Complexité**
> *Temps*: `O(N)` – chaque noeud est visité une fois pendant la sérialisation et la désérialisation.
> *Espace*: `O(N)` – longueur de chaîne de sortie plus pile de récursion.

---

3.2 Solution Python

'`python
♪ Définition du nœud (format LeetCode)
Numéro de classe:
def __init_(self, val=None, children=None):
autoval = val
enfants = enfants ou []

classe Codec:
"""Encode un arbre N‐ary à une chaîne et le décode en arrière."""

def serialize(self, root: 'Node') -> str:
si ce n'est pas la racine:
retour '
parties = []
def dfs(node):
parties.appendice(str(node.val))
Parties et pièces détachées
pour enfant en nœud. enfants:
dfs(enfant)
dfs(racine)
retour ''.join(parties)

def desérialize(self, data: str) -> 'Noeud':
si ce n'est pas des données:
retour Aucune
jetons = data.split()
idx = 0
def dfs():
idx non local
val = int(tokens[idx]); idx += 1
child_cnt = int(tokens[idx]); idx += 1
noeud = noeud(val)
node.children = [dfs() pour _ in range(child_cnt)]
noeud de retour
retour dfs()
«» "

> **Complexité** – identique à la solution Java.

---

### 3.3 C++ Solution

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// LeetCode Définition du nœud
Numéro de structure {
la valeur intérieure;
vecteur <Node*> les enfants;
Node(int _val) : val(_val) {}
Node(int _val, vecteur const <Node*>& _children) : val(_val), children(_children) {}
};

Codec {
public:
// Sérialiser l'arbre N‐ary à une corde
chaîne serialize(Node* root) {
si (!root) retourne ";
les chaînes de caractères;
dfsEncode(root, ss);
retour ss.str(); // contient de l'espace de fuite – inoffensif
}

// Désérialiser la corde de retour à un arbre N‐ary
Node* désérialise(chaîne de caractères et données Const) {
si (data.vide()) retourne nullptr;
stringstream ss(données);
retourner dfsDecode(s);
}

particulier:
vide dfsEncode(Node* noeud, chaîne de caractères &ss) {
ss << noeud->val << ' << noeud->children.size() << ' ';
pour (nœud* enfant : nœud->enfants)
dfsEncode(enfant, ss);
}

Node* dfsDécode(stringstream &ss) {
Int val, enfantCnt;
ss >> val >> enfantCnt;
Noeud* = nouveau Noeud(val);
noeud->enfants.resize(enfantCnt);
pour (int i = 0; i < childCnt; ++i)
noeud->enfants[i] = dfsDécode(s);
noeud de retour;
}
};
«» "

> **Complexité** – mêmes caractéristiques du temps et de l'espace `O(N)`.

---

Article du blog – Serialize & Deserialize N‐ary Tree: Le guide complet

---

### **Titre (SEO-optimisé)* *
> **LeetCode 428 – Serialize & Desérialize N‐ary Tree Solution et entrevue étape par étape Conseils* *

---

- Oui. **Description détaillée**
> Vous voulez ace LeetCodeS difficile problème #428? Apprenez à sérialiser et à désérialiser un arbre N-ary, à comprendre les tendances de la SFD et de la SFB, et à obtenir des idées d'entrevue prêtes à travailler. (en milliers de dollars)

---

- Oui. **Table des matières**

1. [Problème de snapshot] (#problème de snapshot)
2. [Pourquoi cela importe] (# pourquoi-il-matières)
3. [Contraintes clés et cas de bord](#contraintes clés)
4. [Aperçu de la solution] (#solution-overview)
5. [FDS + Compte d'enfant – Le modèle classique] (#dfs-compte d'enfant)
6. [BFS + Null Sentinel – une alternative] (#bfs-sentinel)
7. [Code Walk-Trough (Java / Python / C++)](#code-trough)
8. [Complexité et pièges](#complexité-pièges)
9. [Interview-Ready Tips](#interview-tips)
10. [Pensées finales et prochaines étapes] (#pensées finales)

---

### **1="Problem Snapshot** <a name="problem-snapshot"></a>

> **LeetCode #428 – Serialize and Desérialize N‐ary Tree**
> Difficulté : **Hard**
> Délai: Limite de mémoire: 512 Mo

> *Avec une référence à la racine d'un arbre N-ary, écrivez deux fonctions : *

Fonction
-- -- -- -- -- --
"sérialize(root)" Transformez l'arbre entier en une chaîne. Autres
Recréer l'arbre original de cette chaîne. Autres

> *La sortie de `désérialize(serialize(root))` doit être **bit‐for‐bit identique** à l'arbre original. *

---

C'est pas vrai. Pourquoi ça compte** <un nom=why-it-matières></a>

- **Core Data‐Structure Skill** – Les arbres sont omniprésents (systèmes de fichiers, analyse JSON, organigrammes).
- **Interview Gold‐mine** – De nombreuses interviews seniors demandent à « serialize/desérialize » de tester la récursion, la traversée et la gestion de l'État.
- **Real‐World Pertinence** – Les bases de données graphiques et les systèmes distribués nécessitent une sérialisation efficace pour le transport ou la persistance des réseaux.

---

- Oui. C'est ce que j'ai dit. Contraintes clés et causes de bord** <un nom="contraintes clés"></a>

Qu'est-ce qu'il faut regarder
-- -- -- -- -- --
Arbre vide ("root == null") Retourne une chaîne vide. Autres
Autres Arbre de nœud unique -Sérialisation comme valeur 0 ` (0 enfants). Autres
Autres Arbre profond (profondeur = 104) : profondeur de la récursion → considérer la récursion de la queue ou le BFS itératif si les limites du langage sont préoccupantes. Autres
Autres Grandes valeurs de nœuds («» 109») Éviter les délimiteurs à caractère unique qui pourraient s'opposer aux chiffres. Utilisez des espaces ou un séparateur non numérique. Autres

> *Rappel : Aucune variable globale/statique – chaque appel doit être autonome. *

---

Description de la solution** <un nom="solution-overview"></a>

> **Deux modèles propres** – DFS (récursif) et BFS (intérimaire).

> **FDS + Nombre d'enfants**
> - Encoder comme: `node Val childCnt child1 ... childK` récursivement.
> - Très facile à analyser en utilisant un pointeur d'index.

> **BFS + Null Sentinel**
> - Encoder niveau par niveau, en insérant une sentinelle (`null`) pour marquer la fin d'une liste d'enfants.
> - Itératif, pas de pointeur d'index nécessaire, mais vous devez savoir quand chaque sous-liste se termine.

> Les deux modèles atteignent le temps linéaire et l'espace.

---

Description de la solution** <a name="solution-overview"></a>

> ** Le nombre d'enfants est le plus fréquent** et recommandé pour les raisons suivantes :

1. ** Formatage minimal** – pas de délimiteur spécial, juste des espaces.
2. **Parlage déterministe** – vous lisez toujours une valeur, puis le nombre d'enfants.
3. **Compact** – la longueur de la chaîne est approximativement `2 * number_of_nodes + sum_of_child_counts`.

---

* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

Algorithme

1. **Sérialisation (DFS)* *
- Nœud de visite.
- Ajouter `node.val` et `node.children.size()` séparés par un espace.
- Récursez chaque enfant.
2. **Désérialiser (DFS)* *
- Diviser la chaîne par espaces → tableau `tokens`.
- Maintenir un index mutable (`int[] idx` ou une liste Python).
- Lire `tokens[idx++]` → `val`.
- Lire le jeton suivant → `childCount`.
- Créer un noeud avec `val`.
- Récupérer les temps d ' enfance pour construire des enfants.
- Un nœud de retour.

> **Pourquoi ça marche** – Le format est *prefix* (noeud d'abord) et chaque noeud déclare explicitement combien d'enfants suivent, de sorte que l'analyseur n'a jamais mal identifié les limites.

---

### **6=" BFS + Null Sentinel – Une alternative** <un nom"bfs-sentinel"></a>

Si vous préférez une solution **itative**, vous pouvez coder niveau par niveau, en insérant une sentinelle `null` après chaque liste d'enfants.

Texte
[ rootVal, rootChildCnt, enfant1, enfant2, ..., null, ... ]
«» "

> - Chaque `null` indique au désérialisateur que la liste enfant actuelle est terminée.
> - Temps toujours linéaire, mais vous devez garder une file d'attente et suivre les positions sentinelles.
> - Un peu plus de verbe que DFS + child‐count.

---

- Oui. **7.

Nous avons fourni **trois implémentations complètes** plus tôt (Java, Python, C++).
Points clés à souligner lors d'une présentation :

* Utiliser **espaces** comme délimiteurs – ils survivent à l'analyse "split"/"istringstream".
* Toujours gérer ** arbres vides** tôt (retourner ou analyser une chaîne vide).
* La profondeur de la récursion est naturellement limitée par la hauteur des arbres; pour les arbres très profonds, considérer une version récursive de la queue ou BFS.

---

- Oui. La complexité et les pièges

Opération Temps Espace Erreurs communes
C'est pas vrai.
"serialize" "O(N)"" "O(N)" chaîne "O(N)"" Oublier un espace après le nombre d'enfants → analyser mal aligné. Autres
"désérialize" "O(N)" "O(N)" pile de récursion "O(N)" utilisant des variables globales (violates apatridies). Autres
Manipulation de gros "val" , "O(1)" par noeud , "O(1)" Dépassement si vous stockez comme `char`. Utilisez la corde pour éviter. Autres

> **Pitfall 1** – **Index Out‐of‐Bounds** – Vérifiez toujours que le tableau de jetons contient suffisamment d'éléments avant d'accéder.
> **Pitfall 2** – **Espaces de formation** – Certaines langues les traitent comme des jetons vides ; soyez cohérents.
> **Pitfall 3** – **Dépassement de la pile récursive** – Pour les arbres extrêmement déformés (profondeur = 104), vous pouvez atteindre les limites de la pile en Java/Python; envisager d'augmenter la taille de la pile ou utiliser BFS.

---

### **9=" Conseils d'entrevue** <un nom="interview-tips"></a>

1. ** Expliquez votre format à l'avant** – Je vais utiliser DFS avec le nombre d'enfants parce que...
2. **Afficher les cas de bord** – Arbre vide, noeud unique, grandes valeurs.
3. **Discuss Complexité** – Temps linéaire et espace; justifier la récursion pile.
4. **Mention No Global State** – Chaque appel n'utilise que des variables locales / pile de récursion. (en milliers de dollars)
5. **Optionnel: Ajouter des essais unitaires** – Tester rapidement la sérialisation/désérialisation aller-retour.

---

### **10:00 Pensées finales et prochaines étapes** <un nom="pensées finales"></a>

* Mastering LeetCode #428 vous équipe d'une technique de traversée de l'arbre **versatile** et met en valeur votre capacité à **encoder l'état** dans une chaîne compacte.
* Pratiquer en étendant la solution aux formats **N‐ary** ou **custom serialization**.
* Ajoutez des tests unitaires dans votre langue préférée pour simuler des scénarios du monde réel.
* Continuez à explorer les problèmes de LeetCodes *Design* (par exemple `Serialize/Desérialize Binary Search Tree`, `Design Twitter`, etc.) – les mêmes modèles s'appliquent.

---

> **Happy Coding** et **Good Luck** sur votre prochaine interview d'algorithme! C'est ce qu'il a dit.

---

- Oui. **Appel à l'action**

*Si vous avez aimé ce post, appuyez sur le bouton **S'abonner**, commentez ci-dessous avec vos propres solutions ou questions, et partagez sur LinkedIn ou Twitter avec le hashtag `#LeetCode428`. *

---

Ressources de la prochaine étape

1. Jeu de problèmes LeetCode: Arbre binaire – Sérialisation
2. L'arbre récursif vs itératif Traversal – Coursera / Udacity.
3. Série de graphiques – défis G4G et Hackerrank.

---

> **Fin de l'article**

---

C'est pas vrai. Enveloppe finale En haut

Vous avez maintenant :

1. ** Code entièrement fonctionnel et apatride** en trois langues.
2. Une explication ** concise, prête à l'entrevue** des raisons du problème.
3. Un billet de blog **complet** que vous pouvez publier sur Medium, dev.to, ou votre site de portfolio personnel pour démontrer la maîtrise.

Bonne chance pour écraser LeetCode 428 et impressionner les gestionnaires d'embauche! C'est ce qu'il a dit