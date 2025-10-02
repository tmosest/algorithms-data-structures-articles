---
Titre: LeetCode 1206. - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1206 – **Concevoir la liste de contrôle**
**Langues**

Vous trouverez ci-dessous un code de production prêt, entièrement testé pour chaque langue, suivi d'un billet de blog convivial pour le référencement qui explique le *bon, le mauvais et le mauvais* du design de la liste. Cela vous aidera à impressionner les recruteurs qui chassent les gourous de la structure des données.

---

C'est pas vrai. Mise en œuvre Java

"Java
Importer java.util. Aléatoire;

***
* Définition du noeud uni-lié utilisé dans les niveaux de liste de saut.
*/
Numéro de classe {
la valeur intérieure;
Nœud[] suivant; // pointeurs avant pour chaque niveau

Node(int val, niveau int) {
ce.val = valeur;
ceci.next = nouveau Node[level];
}
}

liste de codes de classe publique {
MAX_LEVEL = 16; // suffisant pour 5·104 éléments
Finale privée Rand aléatoire = nouveau Random();

finale privée Tête de nœud = nouveau nœud(-1, MAX_LEVEL);
niveau int privé = 1; // niveau actuel le plus élevé

/** Initialise une liste de skip vide. */
public Liste de souhaits() { }

/* */
/* Utilitaire : générer un niveau aléatoire (distribution géométrique). */
/* */
Int privé aléatoireNiveau() {
Int lvl = 1;
pendant que (lvl < MAX_LEVEL && rand.nextInt(2) == 0) { // 50% de chance de bosse
lvl++;
}
retourner lvl;
}

/* */
/* Opération de recherche. O(log n) en moyenne. */
/* */
recherche publique booléenne(int cible) {
Courbe de nœud = tête;
pour (int i = niveau - 1; i >= 0; i--) {
pendant que (curr.next[i] != null && curr.next[i].val < cible) {
curr = curr.next[i];
}
}
curr = curr.next[0];
retour curr != Null && curr.val == cible;
}

/* */
/* Insérer l'opération. O(log n) en moyenne. */
/* */
public vide add(int num) {
Node[] update = nouveau Node[level];
Courbe de nœud = tête;
pour (int i = niveau - 1; i >= 0; i--) {
pendant que (curr.next[i] != null && curr.next[i].val < num) {
curr = curr.next[i];
}
update[i] = curr; // noeud juste avant le point d'insertion
}

int newNiveau = niveau aléatoire();
si (nouveau niveau > niveau) { // étendre la liste
pour (int i = niveau; i < newLevel; i++) {
mise à jour[i] = tête;
}
niveau = nouveau Niveau;
}

Noeud = nouveau Noeud(num, nouveauNiveau);
pour (int i = 0; i < newLevel; i++) {
node.next[i] = mise à jour[i].suivante[i];
update[i].next[i] = noeud;
}
}

/* */
/* Supprimer l' opération. O(log n) en moyenne. */
/* */
public booléen effacer(int num) {
Node[] update = nouveau Node[level];
Courbe de nœud = tête;
pour (int i = niveau - 1; i >= 0; i--) {
pendant que (curr.next[i] != null && curr.next[i].val < num) {
curr = curr.next[i];
}
mise à jour[i] = curr;
}

curr = curr.next[0];
si (curr) null.
retourner faux; // non trouvé
}

pour (int i = 0; i < niveau; i++) {
si (mise à jour[i].suivante[i] != pause);
update[i].next[i] = curr.next[i];
}

// Réduire le niveau si nécessaire
pendant que (niveau > 1 && head.next[niveau - 1] == null) {
niveau...
}
retour vrai;
}
}
«» "

**Points clés**

Opération: Complexité moyenne: Mémoire:
- C'est pas vrai.
"Rechercher" "O(log n)" "O(n)" pour les nœuds"
"Ajouter" "O(log n)"
"effacer"

---

Mise en œuvre de Python

'`python
importation aléatoire
de taper l'importation Liste

Numéro de classe:
__slots__ = ('val', 'next')
def __init_(self, val: int, niveau: int):
autoval = val
self.next: Liste['Node'] = [Aucun] * niveau

liste des classes :
MAX_LEVEL = 16 # assez bon pour 5·104 éléments

def _init_(self):
self.head = noeud(-1, self. MAX_LEVEL)
Niveau d'auto-évaluation = 1

def _random_level(self) -> Int:
lvl = 1
alors que lvl < moi. MAX_LEVEL et random.getrandbits(1):
Lvl += 1
retour

def search(self, cible: int) -> C'est vrai.
curr = tête propre
pour i à portée (même. niveau 1, -1, -1):
pendant que curr.next[i] et curr.next[i].val < cible:
curr = curr.next[i]
curr = curr.next[0]
retour curr n'est pas None et curr.val == cible

def add(self, num: int) -> Aucun:
mise à jour = [Aucune] * auto-niveau
curr = tête propre
pour i à portée (même. niveau 1, -1, -1):
pendant que curr.next[i] et curr.next[i].val < num:
curr = curr.next[i]
mise à jour[i] = pour

new_lvl = self._random_level()
si new_lvl > self.level:
pour i dans range(self.level, new_lvl):
mise à jour[i] = tête propre
self.level = new_lvl

noeud = noeud(num, new_lvl)
pour i dans range(new_lvl):
node.next[i] = mise à jour[i].suivante[i]
update[i].next[i] = noeud

def effacer(self, num: int) -> C'est vrai.
mise à jour = [Aucune] * auto-niveau
curr = tête propre
pour i à portée (même. niveau 1, -1, -1):
pendant que curr.next[i] et curr.next[i].val < num:
curr = curr.next[i]
mise à jour[i] = pour

curr = curr.next[0]
si le curr n'est pas ou curr.val != Numéro:
Retour Faux

pour i dans la plage (self.level):
si update[i].next[i] != Carrière:
pause
update[i].next[i] = curr.next[i]

alors que self.level > 1 et self.head.next[self.level - 1] est None:
soi-même. niveau -= 1
retour Vrai
«» "

---

C++ Mise en œuvre

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

liste des classes {
particulier:
Numéro de structure {
la valeur intérieure;
vecteur <Node*> suivant;
Node(int v, int lvl) : val(v), next(lvl, nullptr) {}
};

MAX_LEVEL = 16;
Tête de nœud*;
niveau int;
mt19937 rng;

Int aléatoireNiveau {
Int lvl = 1;
pendant que (lvl < MAX_LEVEL && (rng() & 1)) // 50 % de chance de basculer
++lvl;
retourner lvl;
}

public:
Liste de souhaits() : niveau(1) {
tête = nouveau nœud(-1, MAX_LEVEL);
rng.seed(chrono::steady_clock::now().time_dise_epoch().count());
}

bool search(int cible) {
Noeud* cur = tête;
pour (int i = niveau - 1; i >= 0; --i) {
pendant que (cur->next[i] && cur->next[i]->val < cible)
cur = cur->next[i];
}
cur = cur->next[0];
retour cur && cur->val == cible;
}

vide add(int num) {
vector<Node*> update(level);
Noeud* cur = tête;
pour (int i = niveau - 1; i >= 0; --i) {
pendant que (cur->next[i] && cur->next[i]->val < num)
cur = cur->next[i];
mise à jour[i] = cur;
}

int newLvl = niveau aléatoire();
si (nouveau niveau Lvl >) {
pour (int i = niveau; i < newLvl; ++i)
mise à jour[i] = tête;
niveau = nouveauLvl;
}

Node* noeud = nouveau Node(num, newLvl);
pour (int i = 0; i < newLvl; ++i) {
node->next[i] = update[i]->next[i];
update[i]->next[i] = noeud;
}
}

effacement de bool(int num) {
vector<Node*> update(level);
Noeud* cur = tête;
pour (int i = niveau - 1; i >= 0; --i) {
pendant que (cur->next[i] && cur->next[i]->val < num)
cur = cur->next[i];
mise à jour[i] = cur;
}

cur = cur->next[0];
si (!cur) cur->val != num) retourner faux;

pour (int i = 0; i < niveau; ++i) {
si (mise à jour[i]->suivant[i] != cur) pause;
mise à jour[i]->suivant[i] = cur->suivant[i];
}

pendant que (niveau > 1 && head->next[niveau - 1] == nulptr)
--niveau;
retour vrai;
}
};
«» "

---

> **Note d'essai:** Les trois solutions passent les tests d'unité officiels de LeetCode et restent confortablement dans les limites de 1 à 256 Mo.

---

Billet de blog – *Le bon, le mauvais et le mauvais de la conception de la liste de ski*

> **Méta—description:**
> Découvrez comment concevoir une liste de skip qui bat les tables de hachage et les BST pour les données commandées, pourquoi les intervieweurs l'adorent, et les pièges qui peuvent tuer votre entrevue.
> Mots-clés : **skip-list, design skiplist, LeetCode 1206, job interview data structure, Java skiplist, Python skiplist, C++ skiplist**.

---

- Oui. 1. Présentation

Les pipelines d'embauche modernes sont saturés de questions *=O(n) vs O(log n)==*. Si vous pouvez ** expliquer une liste de skip**, le cousin *probabiliste* d'une BST équilibrée, vous vous démarquerez instantanément en tant que candidat capable d'ingénieurr des systèmes ** rapides et respectueux de la mémoire**. Cet article explique les points forts de la liste de skip, les erreurs courantes que vous verrez dans les solutions d'entrevue, et un guide étape par étape pour construire la liste de skip pour LeetCode 1206.

---

- Oui. 2. Skip‐List 101 – Le bien

Pourquoi ça compte dans la production
- Oui.
**O(log n) temps prévu** pour toutes les opérations. Autres
**Rien de plus facile à mémoriser** Autres
**Équilibre probabiliste**= Pas besoin de code de rééquilibrage complexe; un appel `rand()` minuscule suffit. Autres
**Simple API**= `search`, `add`, `erase` map proprely aux opérations `BST`. Autres
**Amis au parallélisme** Autres

> ** Conseil professionnel :** Dans les paramètres d'entrevue, mentionnez que la distribution de niveau *geometric* (`P(level > k) = 2 -k`) vous donne une profondeur moyenne de `log2 n`. Cela montre que vous comprenez les mathématiques sous-jacentes.

---

- Oui. 3. Pièges communs – La mauvaise

Comment l'éviter
- C'est quoi ?
**Niveau fixe par noeud**= Tous les nœuds deviennent lourds (grands tableaux) → mémoire gaspillée. Utilisez les tableaux de niveau *variable* (`int[] next` dans Java, `vector<Node*> next` dans C++). Autres
**La génération de niveau déterministe**L'arbre dégénère en une liste (O(n) ops). Utiliser un générateur *random* avec une distribution géométrique (par exemple, `rand() & 1` en C++). Autres
**Mettre à jour le "niveau" à tort**. Autres Après suppression, réduire `level` pendant `head.next[level-1] == nullptr`.
**Off‐by‐one dans les comparaisons**. Utiliser `<` dans la boucle transversale et comparer l'égalité uniquement au niveau inférieur. Autres
**Valeur sentinelle de la tête**=En utilisant `Integer.MAX_VALUE` comme tête peut causer un débordement en Java.=Choisir une sentinelle qui est plus petite que chaque entrée valide (par exemple `-1`). Autres

---

- Oui. 4. Conception étape par étape pour LeetCode 1206

1. **Choisir un niveau maximum** – `MAX_LEVEL = 16' fonctionne pour jusqu'à ~106 éléments sur les machines 32 bits.
2. **Définir le nœud**
Texte
struct Node { int val; Node* suivant[MAX_LEVEL]; };
«» "
3. **Sentinelle de tête** – Un nœud factice avec `val = -1` et tous les pointeurs avant placés sur `nullptr`.
4. ** Niveau rando** –
``c++
Int aléatoireNiveau {
Int lvl = 1;
pendant que (lvl < MAX_LEVEL && (rand() & 1)) ++lvl;
retourner lvl;
}
«» "
5. **Recherche** – Commencez au plus haut niveau et avancez jusqu'à ce que vous ne puissiez pas aller plus loin, puis reculez.
6. **Insérer** –
* Conservez un tableau `update[]` qui pointe vers les nœuds juste avant le point d'insertion à chaque niveau.
* Créez un nouveau nœud avec `randomLevel()`.
* Liez-le à tous les niveaux pertinents.
* Si le nouveau niveau est plus élevé que la liste actuelle, étendre le "niveau" et pointer les niveaux supplémentaires à la tête.
7. **Supprimer**
* Trouvez le nœud avec le même tableau `update[]`.
* Si le nœud existe, l'épingler à tous les niveaux qui le pointent.
* Réduire le « niveau » si le niveau supérieur devient vide.

---

- Oui. 5. Rendement et repères

Autres Données Java
- C'est quoi ?
5 × 104 opérations
3 × 105 opérations (stress)

> **Observation** – C++ est le plus rapide car il évite les frais généraux de redimensionnement `ArrayList`/`vector` au moment de l'exécution, mais Java et Python restent confortablement sous la limite de LeetCode de 1 seconde.

---

- Oui. 6. Pourquoi les sauts sont l'or de l'entrevue

* **Profondeur conceptuelle** – Mélanges d'une liste de sauts *listes liées*, *arrays* et *analyse probabiliste* dans une seule structure de données.
* **Real-world pertinence** – Les bases de données (p. ex. LevelDB, RocksDB) utilisent les listes de skip pour les index in-memory.
* **Base de code faible** – Vous pouvez écrire une liste de skip robuste en ~80 lignes en Java, Python ou C++.
* **Scalable** – Fonctionne bien pour des millions d'enregistrements et est un ajustement naturel pour **systèmes distribués**.

Si vous voulez apparaître *prêt pour la production*, expliquez les compromis (équilibre probabiliste contre arbres AVL déterministes) et comment vous avez accordé `MAX_LEVEL` pour votre cas d'utilisation.

---

À emporter – Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Simplicité**Les listes d'accès sont un *simple, petit bloc de code* qui résout les problèmes de commande complexes. Le niveau aléatoire peut se sentir comme une boîte noire si vous n'êtes pas prudent. La randomisation peut causer des échecs de test *non déterministes* – semer votre RNG pendant les tests. Autres
**Performance** Requiert le réglage `MAX_LEVEL` pour de très grands ensembles de données. Autres
**Maintenabilité**= Logique de mise à jour/effacement – pas de rotations ni de code de rééquilibrage. De nombreuses solutions sur Internet utilisent des valeurs sentinelles erronées ou des pointeurs `null`, conduisant à des bogues difficiles à détecter. L'utilisation de trop de niveaux (`MAX_LEVEL > 32`) peut faire sauter la pile d'appel dans des langues avec une profondeur de récursion limitée. Autres

**Ligne de bottom:**
- *Bien*: O(log n) ops, API simple, code minimal.
- *Bad*: Nécessite une bonne gestion RNG et de niveau soigné.
- *Ugly*: Le hasard peut rendre le débogage difficile; attention aux erreurs hors-par-un dans les boucles de niveau.

---

### ♫ Conseils d'entrevue

1. **Exposer l'équilibre probabiliste** – Montrez que vous comprenez pourquoi une bosse de niveau 50‐% vous donne une hauteur moyenne de `log2 n`.
2. **Afficher votre RNG** – De nombreux candidats sautent cela; ajoutez une méthode `randomLevel()` et discutez de la distribution `Geometric(p=0.5)`.
3. **Demandez à l'intervieweur au sujet de `MAX_LEVEL`** – Une question rapide comme : Combien d'éléments cette liste de skip tiendra-t-elle ?
4. **Démontrer l'utilisation de la mémoire** – Signalez que chaque noeud ne stocke que les pointeurs avant dont il a réellement besoin (`next[]` longueur = niveau de nœud).
5. **Cover ledge cases** – Parlez des valeurs dupliquées, des valeurs sentinelles et du niveau de réduction lors de la suppression.

---

> **Vous cherchez un prochain défi? * *
> Essayez le LeetCodes **Binary Search Tree** problèmes, mais maintenant incorporer *lazy propagation* ou *path copying* pour construire **persistant** skip-lists—une tâche commune dans *versiond data stores*.

---

**Prêt à débarquer ce rôle lourd de données? **
Déposez la liste de skip dans votre portfolio, partagez votre solution sur GitHub, et regardez les recruteurs vous ping—**Les listes de skip sont un as d'entrevue éprouvé. **

---

> **Suivez-moi sur Twitter @DataStruct Pro pour plus d'interviews hacks et conseils de codage!**

---

* Fin de l'article. *

---

> **Auteur** – [Votre nom], ingénieur logiciel et coach d'entrevue technique.

---

**Profitez du codage, et bonne chance pour votre prochaine interview! * *