---
Titre: LeetCode 588. Conception du système de fichiers en mémoire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 588 – Concevoir un système de fichiers en mémoire
**Traitement: 588.

> Vous voulez obtenir cette entrevue d'ingénierie logicielle?
> La maîtrise de ce problème montre que vous pouvez concevoir une structure de données, travailler avec les arbres, et garder tout **lexicographiquement trié** – exactement ce que les gestionnaires d'embauche aiment.

---

- Oui. 1. Récapitulation des problèmes (friendly SEO)

> **Concevoir un système de fichiers en mémoire** – *LeetCode 588*.
> Créer une classe `FileSystem` qui supporte:
> * `ls(path)` – le contenu du répertoire de la liste ou un nom de fichier.
> * `mkdir(path)` – créer des répertoires.
> * `addContentToFile(filePath, content)` – créer ou ajouter du contenu de fichier.
> * `readContentFromFile(filePath)` – lire le contenu du fichier.

Tous les chemins sont absolus, commencent par `/`, et ne finissent pas par `/` (sauf la racine).
Les noms se composent de lettres minuscules, pas de duplicata dans le même dossier.

> **Pourquoi c'est important:**
> Les intervieweurs vous demandent de mesurer votre capacité à :
> * Construire une structure arborescente (fichiers et répertoires).
> * Manipulation de la chaîne de caractères & chemin de passage.
> * Gardez le répertoire trié (ordre lexicographique).
> * Pensez aux cas de bord et aux performances.

---

- Oui. 2. Aperçu de la conception

Couche Ce qu'il fait Pourquoi il importe
- C'est quoi ?
Autres **Noeud**= Représente un fichier ou un répertoire. Autres Conserve les données de base ensemble – contenu pour les fichiers, enfants pour les dirs. Autres
*Tree**= Root `Node` + navigation par chemin. Active les opérations O(profondeur). Autres
Utiliser une carte triée (`TreeMap` en Java, `std::map` en C++, `dict + trié()` en Python). Garantir l'ordre lexicographique sans travail supplémentaire. Autres

---

- Oui. 3. Mise en œuvre des références

Voici des implémentations propres et prêtes à la production pour **Java, Python et C++**.
Tous les trois suivent les mêmes principes de conception et passent les tests LeetCode.

#### 3.1 Java

"Java
Importation de java.util.*;

classe publique FileSystem {

*** Le nœud représente soit un répertoire, soit un fichier */
Nœud statique privé {
le booléen isFile;
StringBuilder content = nouveau StringBuilder(); // seulement pour les fichiers
TreeMap<String, Node> enfants = nouveau TreeMap<>(); // seulement pour les répertoires

Noeud() { ceci. isFile = faux; }
}

finale privée racine du nœud;

public FileSystem() {
root = new Node(); // root est toujours un répertoire
}

*** Énumérer le contenu d'un répertoire ou le nom d'un fichier */
liste publique<String> ls(String path) {
Noeud = traversée (chemin);
si (node.isFile) { // fichier: retourner son propre nom
Chaîne[] parties = path.split("/");
retour Collections.singletonListe(parties[parties.longueur - 1]);
}
retourner la nouvelle liste d'array<>(node.children.keySet());
}

/** Créer des répertoires le long du chemin donné */
vide public mkdir(chemin d'accès) {
traversée(chemin); // la méthode de traversée crée automatiquement des nœuds manquants
}

*** Ajouter du contenu à un fichier; créer un fichier s'il manque */
public vide addContentToFile(Path de fichier, contenu de chaîne) {
Noeud = traversée (filePath);
noeud. isFile = true;
node.content.append(content);
}

*** Retourner le contenu complet d'un fichier */
public Chaîne readContenu FromFile(String filePath) {
Noeud = traversée (filePath);
retour node.content.àString();
}

*** Aide : marcher le chemin, créer des nœuds au besoin */
traversée de nœud privé (chemin de fer) {
Noeud cur = racine;
si (path.equals("/")) retour cur;
Chaîne[] parties = path.split("/");
pour (int i = 1; i < parts.longueur; i++) { // sauter la chaîne vide
cur.children.putIfAbsent(parties[i], nouveau nœud());
cur = cur.children.get(parties[i]);
}
retour cur;
}
}
«» "

> **Les choix spécifiques à Java* *
> * `TreeMap` → commande lexicographique intégrée.
> * `StringBuilder` pour l'adaptation efficace des chaînes.
> * `putIfAbsent` garde le code rangé.

---

3.2 Python

'`python
classe FileSystem & #160;:
Numéro de classe:
__slots__ = ('is_file', 'content', 'children')
def __init__(self, is_file=False):
self.is_file = is_file
self.content = [] # liste de chaînes, concat efficace
auto.enfants = {} # clé -> Noeud

def _init_(self):
self.root = self.Node()

def ls(self, chemin: str) -> list[str]:
noeud = auto._traverse(path)
si node.is_file:
retour [path.split('/')[-1]]
retour trié(nœud.enfants)

def mkdir(self, chemin: str) -> Aucun:
self._traverse(path) # crée des nœuds à la volée

def addContentToFile(self, filePath: str, content: str) -> Aucun:
noeud = self._traverse(filePath)
node.is_file = Vrai
node.content.append(content)

def readContenu FromFile(self, filePath: str) -> str:
noeud = self._traverse(filePath)
retour ''.join(node.content)

def _traverse(self, path: str) -> 'FileSystem. Noeud':
cur = auto-root
si chemin == '/':
retour cur
pour partie dans chemin.strip('/').split('/'):
s'il n'y a pas d'enfants:
cur.children[part] = self.Node()
cur = enfants[partie]
retour cur
«» "

> **Tricks de python* *
> * `__slots__` → empreinte de mémoire plus petite.
> * `list` pour le contenu → évite la concaténation des chaînes quadratiques.
> * `trié()` à `l` assure l'ordre.

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe FileSystem {
particulier:
Numéro de structure {
bool isFile = false;
contenu de chaîne; // utilisé uniquement si isFile==true
carte <string, Node*> enfants; // ordre lexicographique par défaut
Node() = par défaut;
};
racine de nœud*;

// Helper: marche un chemin, créant des nœuds au besoin
Nœud* traversant (chaîne de caractères et chemin) {
Noeud* cur = racine;
si (chemin == "/") retour cur;
ss(path);
partie chaîne;
getline(ss, part, '/'); // sauter en tête '/ '
pendant la période (objectif(ss, partie, '/')) {
si (!cur->children.count(part))
cur->children[part] = nouveau nœud();
cur = cur->enfants[partie];
}
retour cur;
}

public:
FileSystem() : root(new Node()) {}

vector<string> ls(string path) {
Noeud* = traversée (chemin);
si (node->isFile) {
nom de chaîne = path.substr(path.rfind('/') + 1);
retourner {nom};
}
vecteur <string> rés;
pour (const auto& kv : noeud->enfants) res.push_back(kv.first);
retour rés;
}

vide mkdir(chemin de corde) { traversée(chemin); }

vide addContentToFile(string filePath, contenu de la chaîne) {
Noeud* = traversée (filePath);
noeud->isFile = vrai;
node->content += content; // la concaténation de la chaîne est très bien ici
}

chaîne readContentFromFile(string filePath) {
Noeud* = traversée (filePath);
retour du noeud->contenu;
}
};
«» "

> **Spécifications C++**
> * `map` garantit les clés triées.
> * `stringstream` → dédoublement du chemin.
> * `vector<string>` pour les résultats `l`.

---

- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
"l'"" **O(profondeur + k log k)** (`k` = nombre d'éléments dans le dir)
"mkdir" **O(profondeur)**
"addContentToFile" (en anglais seulement) **O(profondeur)**= O(1) pour le nœud, + O(len(content)) pour l'appendice (en anglais seulement)
«readContentFromFile» **O(profondeur)**

> La **profondeur** est délimitée par la longueur maximale du chemin (10^4 caractères) – en pratique très petite, donc toutes les opérations sont effectivement O(1) pour les entretiens.

---

- Oui. 5. Bonne, mauvaise et laid – Ce que les gestionnaires d'embauche recherchent

Aspect Ce que vous devez mettre en évidence Quoi faire ?
Il n'y a pas de problème.
**Bon**• Structure claire de l'arbre<br>• Tri lexicographique via `TreeMap`/`map`<br>• Un seul helper traversal. Autres
**C'est bien ici, mais cela peut coûter cher pour les arbres énormes. La suroptimisation peut nuire à la lisibilité. Autres
**Ugly** Chaîne vide après scission (leading slash)<br>• Fichier vs détection de répertoires. Autres

**Astuce:** Toujours ajouter un harnais `main()` / test qui imite l'exemple LeetCode. Il vous oblige à penser aux affaires de bord tôt.

---

- Oui. 6. Points de discussion prêts à l'entrevue

1. **Pourquoi un arbre? **
* Les systèmes de fichiers sont naturellement hiérarchiques – un arbre est l'abstraction la plus naturelle.
* Chaque carte `enfant` vous permet de sauter d'un niveau à l'autre dans *O(1)*.

2. **Tenir des listes triées**
* `TreeMap` / `std::map` garde les clés triées automatiquement – pas de `sort()` supplémentaire Appelez.
* Dans Python, `sorted()` sur les clés fonctionne bien parce que les dictionnaires ne sont pas triés.

3. **Path Parsing**
* `split('/')` fonctionne mais laisse une chaîne vide à l'index 0 pour les chemins absolus.
* `putIfAbsent` / `children.emplace` créent des répertoires manquants sans vérification d'existence séparée.

4. ** Empreinte mémoire* *
* Chaque noeud de répertoire stocke un `TreeMap` ou `unordered_map`.
* Les fichiers stockent seulement un `StringBuilder` / `list`.
* L'entrée type LeetCode est petite; l'utilisation réelle nécessiterait une persistance ou une compression.

5. **Manipulation d'erreurs**
* Le problème officiel garantit des chemins valides – mais dans la vie réelle, vous devez ajouter validation & lancer des exceptions descriptives.

---

- Oui. 7. Comment cela vous aide à obtenir un emploi

Exemple du système de fichiers Comment les recruteurs le voient
-- -- -- -- -- -- -- -- -- -- -- -- --
**Conception de la structure des données**= Arbre des objets `Node`= Affiche que vous pouvez modéliser les systèmes du monde réel. Autres
**La pensée algorithmique**= O(profondeur) traversale== Indique la résolution efficace des problèmes. Autres
**Maîtrise de la langue** Autres
**Testing & debugging**.Écrire des tests unitaires pour chaque méthode. Autres

Lorsque vous énumérez ce problème sur votre CV ou que vous en parlez dans une entrevue, utilisez **mots clés** que les recruteurs recherchent:

* **Système de fichiers en mémoire* *
* **Code de bord 588**
* **Design In-Memory File System**
* ** Entretien sur les structures de données**
* ** Entretien avec un emploi**
* **Entretien de codage**

Mentionnez les langues avec lesquelles vous êtes à l'aise et soulignez que vous pouvez adapter la logique de base à travers **Java, Python, C++** – un signal clair de l'expertise *cross-platform*.

---

- Oui. 8. Aperçu de l'article du blogue (optimisé par le SEO)

Titre
LeetCode 588 – Concevoir un système de fichiers in-Memory (Java, Python, C++)

Description de la méta
> Master LeetCode 588 et impressionner les gestionnaires d'embauche. Lisez la solution complète en Java, Python et C++ en plus d'une plongée profonde dans les décisions de conception et les conseils d'entrevue.

Rubriques (H1–H4)

Mots clés Autres
C'est quoi ?
**H1:** LeetCode 588 – Concevoir un système de fichiers In-Memory, Code du véhicule
**H2:** Résumé des problèmes et contraintes Autres
**H2:** Conception de la structure des données
**H3:** Mise en œuvre Java `Java`, `TreeMap`, `StringBuilder` Autres
**H3:** Mise en œuvre de Python Autres
**H3:** Mise en œuvre C++
**H2:** Performance et compromis Autres
**H2:** Pièges communs et causes de bord Autres
**H2:** Comment ce problème vous prépare pour les entrevues

- Oui. Extrait de blog

> Dans ce post, nous décrivons LeetCode est le plus difficile problème de système de fichiers, vous montrons comment le coder en Java, Python et C++, et expliquer les choix de conception qui impressionneront vos intervieweurs. De la structure de l'arbre qui maintient les répertoires triés aux subtils parsages de chemin, nous couvrons tout ce que vous devez savoir pour as l'interview et terre ce travail de rêve.

---

- Oui. 9. Scénario d'essai rapide (facultatif)

'`python
si __nom__ == "__main__" :
fs = SystèmeFichier()
L'objectif est de réduire les émissions de gaz à effet de serre.
fs.addContentToFile("/a/b/c/d", "bonjour")
print(fs.ls("/")) # ['a']
print(fs.ls("/a/b/c")) # ['d']
print(fs.readContentFromFile("/a/b/c/d")) # Bonjour
«» "

N'hésitez pas à les coller dans votre IDE préféré ou compilateur en ligne pour tester davantage.

---

## 10. Dernier départ

* ** Abstraction nette** (Node + Arbre) + ** récipient trié** = solution propre et durable.
* La même logique de base fonctionne à travers **Java, Python, C++** – un excellent point de preuve d'entrevue.
* Comprendre ce problème renforce vos connaissances *structure des données*, une compétence incontournable pour toute entrevue sur l'ingénierie des logiciels**.

Essayez cela, ajoutez-le à votre portfolio, et regardez ces offres d'emploi rouler! C'est ce qu'il a dit