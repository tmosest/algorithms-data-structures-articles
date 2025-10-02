---
titre: LeetCode 1166. Système de fichiers de conception -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème – 1166.

> **Numéro de code de débit**: 1166
> **Difficulté**: Moyenne
> **Tag**: Conception, tableau de bord, trie

On vous demande de mettre en place un système de fichiers miniature qui supporte deux opérations :

Méthode Signature Comportement
C'est pas vrai.
"créerPath(chemin, valeur)" "boolean" Ajouter un nouveau chemin et y attacher une valeur entière. Retourne **false** si le chemin existe déjà ou si son chemin parent n'existe pas. Autres
«get(path)» «int» Retourne la valeur associée à *path* ou **-1** si le chemin n'existe pas. Autres

*Format papier* – une chaîne non vide qui commence par `/` et ne contient que des lettres anglaises minuscules. Exemples: `/a`, `/leetcode/problèmes`. La racine `/` elle-même est **pas** un chemin valide.

**Contrôles* *

- `2 <= chemin.longueur <= 100`
- `1 <= valeur <= 109`
- ≤ 104 appels à "créerPath"/"get" au total

L'objectif est de construire une implémentation efficace et prête à l'interview qui peut être présentée en Java, Python ou C++.

---

- Oui. 2. Choix de conception de haut niveau

L'approche La force La faiblesse Le cas d'utilisation
- C'est quoi ?
**Arbre basé sur Hash-Map**= Simple, rapide O(longueur) par opération== Utilise plus de mémoire qu'un hash-table plat===
**Flat Hash‐Table** (chemin → valeur) , O(1) moyenne recherche , nécessite une logique supplémentaire pour vérifier l'existence du parent , utile pour un très grand nombre de chemins indépendants ,
**Trie**= Efficacité de la mémoire pour les préfixes communs== Code légèrement plus complexe== Bon lorsque de nombreux chemins partagent des préfixes (par exemple `/a/b/c`, "/a/b/d"

La solution la plus conviviale pour les interviews est un arbre *hash-map (parfois appelé structure **Trie-like**). Il conserve un nœud racine et une cartographie des noms d'enfants → nœuds d'enfants. Chaque opération ne descend que les composants du chemin, donnant `O(L)` temps où `L` est le nombre de composants (= 100). L'utilisation de la mémoire est `O(N)` où `N` est le nombre total de nœuds créés.

---

- Oui. 3. Mise en œuvre des références

On trouvera ci-dessous des solutions complètes et prêtes à être collées dans **Java**, **Python** et **C++**. Chacun suit le même modèle d'arbre.

### 3.1 Java – Interview-Ready

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

classe publique FileSystem {

- Oui. Définition du nœud
Nœud statique privé {
Nom de chaîne; // nom du composant
valeur int; // valeur stockée sur ce nœud
Carte <String, Node> enfants; // enfants par nom de composant

Noeud(nom de la chaîne) {
Ça. nom = nom;
Cette valeur = 0; // 0 ne signifie pas encore de valeur
ce.enfants = nouveau HashMap<>();
}
}

- Oui. API du système de fichiers --------- */
finale privée racine du nœud;

public FileSystem() {
root = nouveau nœud(""); // root représente "/"
}

public booléen createPath(String path, int value) {
si (chemin) null.isEmpty()=1 chemin.equals("/") retourne faux;

Chaîne[] parties = path.split("/"); // fractionnement sur '/', première partie vide
Noeud cur = racine;

/* marcher jusqu'au parent du nouveau chemin */
pour (int i = 1; i < parties.longueur - 1; i++) {
Partie de chaîne = parties[i];
cur = cur.children.get(part);
si (cur == null) retourner false; // parent n'existe pas
}

Chaîne dernière = parties[parties.longueur - 1];
si (cur.children.contientKey(dernier)) retourner faux; // existe déjà

Node newNode = nouveau Node(dernier);
newNode.value = valeur;
cur.children.put(dernier, nouveauNode);
retour vrai;
}

public int get(String path) {
if (path == null="path.isEmpty()="path.equals("/") retourne -1;

Chaîne[] parties = path.split("/");
Noeud cur = racine;

pour (int i = 1; i < parties.longueur; i++) {
Partie de chaîne = parties[i];
cur = cur.children.get(part);
si (cur == null) retourner -1;
}
valeur de retour;
}
}
«» "

> **Pourquoi cela est-il convivial? * *
> * Séparation claire des préoccupations* : classe `Node` légère, ligne directe `createPath` et `get`. La logique est facile à tracer dans une entrevue de codage en direct.

---

3.2 Python – Concise et lisible

'`python
classe FileSystem & #160;:
_Node de la classe :
__slots__ = ("nom", "valeur", "enfants")

def __init_(self, nom: str):
nom propre = nom
Self.value = 0 # 0 signifie "pas encore de valeur"
Les enfants = {}

def _init_(self):
self.root = self._Node("") # root représente "/"

def createPath(self, chemin: str, valeur: int) -> C'est vrai.
si ce n'est pas le chemin ou le chemin == "/":
Retour Faux

parties = path.split("/")[1:] # ignorent la partie vide principale
cur = auto-root

pour partie dans les parties[:-1]: # marcher jusqu'au parent
s'il n'y a pas d'enfants:
Retour Faux
cur = enfants[partie]

dernière = parties[-1]
si la dernière en cur.children: # existe déjà
Retour Faux

cur.children[dernier] = soi-même._Node(dernier)
cur.enfants[dernier]. Valeur
retour Vrai

def get(self, chemin: str) -> Int:
si ce n'est pas le chemin ou le chemin == "/":
retour -1

parties = path.split("/")[1:]
cur = auto-root

pour partie:
cur = cur.children.get(part)
si cur est None:
retour -1
retour cur.value
«» "

> ** Touches pyroniques* *
> *'__slots__'* maintient les objets de nœuds maigres.
> *Splitter sur `/`* donne un moyen facile d' itérer les composants.

---

### 3.3 C++ – Rapide et moderne

'`cpp
#inclut <non-ordonné_map>
#incluez <string>
#incluez <vecteur>

classe FileSystem {
particulier:
Numéro de structure {
valeur int{0}; // 0 => pas encore de valeur
std::unordered_map<std::string, Noeud*> les enfants;
};

Noeud* root = nouveau Noeud(); // root représente "/"

// Utilitaire : diviser un chemin en composants, sauter ceux vides
std statique::vector<std::string> split(const std::string&path) {
md::vecteur<std::chaîne> parties;
size_t start = 1; // saut en tête '/ '
pour (size_t i = 1; i <= path.size(); ++i) {
if (i == chemin.size()="path[i]="/") {
i (i > start) parts.emplace_back(path.substr(start, i - start));
début = i + 1;
}
}
les pièces retournées;
}

public:
FileSystem() = par défaut;
~FileSystem() { limpide(root); }

bool createPath(const std::string& path, valeur int) {
si (path.vide()="path == "/") retourner false;

parties automatiques = split(path);
Noeud* cur = racine;

pour (size_t i = 0; i + 1 < parts.size(); ++i) { // aller à parent
Const auto & comp = pièces[i];
auto it = cur->children.find(comp);
si (it) cur->children.end() retourne faussement;
cur = it->seconde;
}

const std::string& last = parts.back();
si (cur->children.count(dernier)) retourne faux;

Noeud* enfant = nouveau Noeud();
enfant->valeur = valeur;
cur->enfants[dernier] = enfant;
retour vrai;
}

int get(const std::string&path) const {
si (path.vide()="path == "/") retourne -1;

parties automatiques = split(path);
Noeud* cur = racine;

pour (const auto & comp : pièces) {
auto it = cur->children.find(comp);
si (it) cur->children.end() retourne -1;
cur = it->seconde;
}
valeur de retour cur->;
}

particulier:
vide (noeud) {
pour (auto& [_, enfant] : noeud->enfants)
clair(enfant);
supprimer le nœud;
}
};
«» "

> **Pourquoi C++?**
> *La gestion explicite de la mémoire* (avec "claire") montre une prise de conscience de la propriété.
> *`unordered_map`* donne la recherche attendue `O(1)`.

---

- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
« createPath» – où «L» est le nombre de composants dans le chemin.
Aucun (lit uniquement les nœuds existants)

- `L` ≤ 100 (compte tenu des contraintes).
- Mémoire totale `O(N)` où `N` = nœuds totaux jamais créés (= nombre d'appels réussis `createPath`).

Les implémentations Java/Python et C++ satisfont les contraintes LeetCode facilement.

---

- Oui. 5. Entrevue‐Commerce spécifique‐ Hors taxes

Sujet Ce que les intervieweurs recherchent Pièges à éviter
-- -- -- -- -- -- -- -- -- -- -- -- --
**Cas d'Edge**, chaîne vide, composant dupliqué.
**L'existence du parent**La transversale doit atteindre le nœud *parent* en premier.
**Valeur 0 vs. Aucune valeur**=0 est une valeur stockée valide?= Dans les valeurs spec sont ≥ 1, donc 0 peut signifier en toute sécurité aucune valeur pour l'instant. Autres
Chaque noeud contient une carte des enfants.
**Garbage Collection**=Java/Python: automatique; C++: manuel== Ne pas supprimer les nœuds entraîne des fuites==

---

- Oui. 5. Pièges courants et comment réparer Eux

1. **Splitting `/` incorrectement* *
*Fix* : ignorez les chaînes vides ou sautez la ligne de tête `/`.
2. **En supposant que le parent existe automatiquement**
*Fix*: descendez le chemin *jusqu'au parent* et retournez `faux` si un composant manque.
3. **Renvoi de la mauvaise valeur pour l'instant* *
*Fix* : stocker les valeurs uniquement sur les nœuds qui sont explicitement créés, laisser d'autres nœuds à une sentinelle (par exemple, 0 ou `Aucune`).
4. ** Racine manuelle `/`**
*Fix*: l'instruction de problème dit que root n'est pas un chemin valide – traitez-le spécialement ou rejetez-le franchement.

---

- Oui. 5. Et si les variations

- **Table de Hash-Flat *
'`cpp
unordered_map<string,int> val;
non ordonné_map<string,string> parent; // parent[path] = "/a/b"
«» "
- `createPath` doit vérifier que `parent[path]` existe.
- `get` est la moyenne `O(1)`.

- **Segment Tree** (overkill pour ce problème) – bon pour les requêtes par lots sur des plages numériques.

---

- Oui. 5. Sommaire – Messages à emporter pour votre prochaine entrevue

1. **La carte du hachage à base d'arbres (comme les soies) est la norme de l'or** : propre, rapide et facile à expliquer.
2. **Validez toujours le parent** avant d'insérer.
3. **Keep node stockage light** – utilisez une seule carte par noeud, un champ de valeur, et éventuellement une sentinelle pour une valeur de zéro. (en milliers de dollars)
4. **La complexité temporelle** est linéaire dans le nombre de composants de chemin (=100), qui est bien en dessous de la limite de LeetCode.
5. **L'utilisation de l'espace** est linéaire dans le nombre de nœuds – fin pour ≤ 104 nœuds.

> **Conseil d'intervieweur**: Pouvez-vous décrire comment vous stockeriez la structure des données ? (en milliers de dollars)
> Réponse : Un nœud racine, chaque noeud tient un dictionnaire `children` clé par le prochain composant de chemin. (en milliers de dollars)
> Puis écrivez les deux méthodes – le reste suit naturellement.

---

- Oui. 6. Prise finale Away – Système de fichiers de conception en 3 langues

- **Java**: Utilisez `HashMap<String, Node>` à l'intérieur de chaque noeud; divisez les chemins avec `split("/")`.
- **Python**: Même idée, mais utilisez `__slots__` pour garder les noeuds maigres.
- **C++**: `unordered_map` + manuel `new`/`delete` vous donne à la fois rapidité et clarté de propriété.

Les trois solutions satisfont aux contraintes du LeetCode et peuvent être démontrées lors de toute entrevue de codage ou évaluation technique. Choisissez la langue avec laquelle vous êtes le plus à l'aise, ou présentez les trois pour montrer l'étendue des connaissances.

> **Rappelez-vous** – la vraie valeur de l'entrevue n'est pas seulement le code final, mais la possibilité de discuter *pourquoi* vous avez choisi cette conception, quels compromis vous considériez, et comment vous avez testé les cas de bord. Bonne chance !