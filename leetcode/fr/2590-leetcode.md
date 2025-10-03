---
Titre: LeetCode 2590. Concevoir une liste de tâches -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 2590 – Concevoir une liste de tâches
### Une plongée profonde dans le problème, la solution et l'entrevue‐ Code prêt (Java / Python / C++)

---

### TL;DR
* **Problème** – Implémenter une classe *TodoList* qui peut ajouter, récupérer et compléter des tâches pour de nombreux utilisateurs.
* ** Opérations clés** – `addTask`, `getAllTasks`, `getTasksForTag`, `complète Tâche.
* **Constraints** – ≤ 100 appels, dates d'échéance uniques, ≤ 100 utilisateurs & tâches, étiquettes jusqu'à 100 par tâche.
* ** Objectif** – ajout O(1), O(k log k) pour la récupération (k = # tâches renvoyées).

Ci-dessous vous trouverez:

Solution complète (prête à coller dans LeetCode)
C'est ce que j'ai dit.
**Java** Cliquez pour agrandir</résumé>
"Java
Importation de java.util.*;
importer java.util.concurrent.ConcurrentHashMap;

TodoList de classe publique {
// Compteur pour les identifiants de tâches uniques au niveau mondial
taskCounter privé = 1;

// Tâche de cartographie Id → Tâche
finale privée Carte<entier, Tâche> taskMap = nouveau ConcurrentHashMap<>();

// Utilisateur des cartes Id → Liste des taskIds (en ordre d'insertion)
carte finale privée<entier, liste<entier>> userTasks = nouveau ConcurrentHashMap<>();

/** Initialisez votre structure de données ici. */
public TodoList() {
// Rien à faire – toutes les cartes sont déjà instantanées
}

*** Ajoutez une tâche et retournez son ID. */
int public addTask(int user Id, String taskDescription, int dueDate, List<String> tags) {
int id = tâche contre++;
Tâche = nouvelle tâche(id, taskDescription, dueDate, tags);
taskMap.put(id, tâche);

userTasks.computeIfAbsent(utilisateur Id, k -> nouveau tableau <>()).add(id);
id de retour;
}

*** Aide – retourner une liste de *inachevée* Objets de tâche pour un utilisateur, triés par dueDate. */
liste privée<Task> getPendingTasksSorted(int user Id) {
Liste<Tâche> en attente = nouvelle liste de distribution<>();
Liste<Integer> ids = userTasks.getOrDefault(userId, Collections.videList());
pour (int id : ids) {
Tâche t = taskMap.get(id);
si (!t.complété) en attente.add(t);
}
en attente.sort(Comparator.comparingInt(t -> t.dueDate);
le retour en attente;
}

*** Obtenez toutes les tâches non terminées pour un utilisateur, commandées à la date d'échéance. */
liste publique<String> getAllTasks(int user Id) {
Liste<String> res = nouvelle liste de distribution<>();
pour (Tâche t : getPendingTasksSorted(userId)) res.add(t.description);
retour rés;
}

*** Obtenez toutes les tâches non terminées pour un utilisateur qui contient une balise spécifique. */
liste publique<String> getTasksForTag(int user Id, étiquette à cordes) {
Liste<String> res = nouvelle liste de distribution<>();
pour (Tâche t : getPendingTasksSorted(userId)) {
si (t.tags.contient(tag)) res.add(t.description);
}
retour rés;
}

*** Marquer une tâche comme terminée seulement si elle appartient à l'utilisateur et est toujours en attente. */
vide public complet Tâche(int utilisateur Id, tâche int Id) {
si (!userTasks.contientKey(userId)) retourne;
si (!userTasks.get(userId).contient(taskId)) retourne;
Tâche t = taskMap.get(taskId);
si (t != null &&!t.completed) t.completed = true;
}

- Oui. Classe de tâches intérieure --------- */
classe statique privée Tâche {
l'identifiant final;
description finale de la chaîne;
finale due Date;
les étiquettes finales de la liste <String>;
booléen rempli = faux;

Tâche(int id, description de chaîne, date de dépôt int, balises List<String>) {
cet.id = id;
Ça. description = description;
ça. attendu Date d ' échéance Date;
ce.tags = nouveau ArrayList<>(tags); // copie défensive
}
}
}
«» "
</détails>
**Python**=Détails><résumé>Cliquez pour agrandir</résumé>
'`python
de collections importer par défautdict
de taper l'importation Liste

classe TodoList:
def _init_(self):
_task_id = 1
soi-même. tâches = {} # id -> Tâche
self.user_tasks = defaultdict(list) # user_id -> liste des id des tâches

def addTask(self, userId: int, taskDescription: str,
dueDate: int, tags: List[str]) -> Int:
tid = auto._task_id
auto._task_id += 1
auto.tâches[tid] = {
"desc": description des tâches,
"attendu": date d'échéance,
"tags": ensemble(s),
"complété": Faux
}
self.user_tasks[userId].append(tid)
retour

def _pending_sorted(self, userId: int):
en attente = [self.tasks[tid] pour tid inself.user_tasks.get(userId, [])
s'il ne s'agit pas d'autotâches[tid]["achevées"]]
retour trié(en cours, clé=lambda t: t["due"])

def getAllTasks(self, userId: int) -> Liste[str]:
retourner [t["desc"] pour t in self._pending_sorted(userId)]

def getTasks PourTag(self, userId: int, tag: str) -> Liste[str]:
retourner [t["desc"] pour t in self._pending_sorted(userId) si tag in t["tags"]]

def complete Tâche(self, userId: int, taskId: int) -> Aucun:
si tâche Je n'étais pas en moi. tâches:
retour
si taskId n'est pas dans self.user_tasks.get(userId, []):
retour
si ce n'est pas lui-même.tâches[taskId]["complété"]:
auto.tâches[taskId]["complété"] = Vrai
«» "
</détails>
**C++** Cliquez pour agrandir</résumé>
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe TodoList {
public:
TodoList() : tâcheCounter(1) {}

int addTask(int utilisateur Id, description des tâches de chaîne,
int dueDate, vector<string> tags) {
int id = tâche contre++;
Tâche t{id, taskDescription, dueDate, tags, false};
tâches[id] = t;
userTasks[userId].push_back(id);
id de retour;
}

vector<string> getAllTasks(int user Id) {
vecteur <string> rés;
pour (auto &t : getPendingSorted(userId))
res.push_back(t.description);
retour rés;
}

vector<string> getTasksForTag(int user Id, chaîne de caractères) {
vecteur <string> rés;
pour (auto &t : getPendingSorted(userId))
si (t.tags.find(tag) != t.tags.end())
res.push_back(t.description);
retour rés;
}

vide complet Tâche(int utilisateur Id, tâche int Id) {
auto it = userTasks.find(userId);
si (it) l'utilisateurTasks.end() retourne;
si (find(it->second.begin(), it->second.end(), taskId) == it->second.end()
retour;
&t automatique = tâches[taskId];
si (!t.complété) t.complété = vrai;
}

particulier:
struct Tâche {
idem;
description de la chaîne;
Int dû;
tags non ordonnés_set<string>;
bool complété = faux;
Tâche(int i, chaîne d, int du, vector<string> tg)
: id(i), description(d), due(du), tags(tg.begin(), tg.end()) {}
};

int taskCounter; // prochain ID de tâche globale
non ordonné_map<int, Tâche> tâches; // tâche Id → Tâche
non ordonné_map<int, vector<int>> userTâches; // utilisateur Id → liste des tâches Ids

// Retour des tâches en attente triées par date d'échéance
vector<Task> getPendingSorted(utilisateur int) Id) {
vecteur<Tâche> en attente;
auto it = userTasks.find(userId);
si (it) l'utilisateurTasks.end() retourne en attente;
pour (int id : it->seconde) {
&t automatique = tâches[id];
si (!t.complété) en attente.push_back(t);
}
tri(en instance.begin(), en attente.end(),
[](const Task &a, const Task &b){ retourner a.due < b.due; });
le retour en attente;
}
};
«» "
</détails>
**C++** (style LeetCode plus court) Cliquez pour agrandir</résumé>
'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe TodoList {
public:
TodoList() : nextId(1) {}

int addTask(int utilisateur Id, description des tâches de chaîne,
int dueDate, vector<string> tags) {
int id = suivant Id++;
tâches[id] = {taskDescription, dueDate, tags, false};
userTasks[userId].push_back(id);
id de retour;
}

vector<string> getAllTasks(int user Id) {
auto v = en attenteSorted(userId);
vecteur <string> rés;
pour (auto &t : v) res.push_back(t.description);
retour rés;
}

vector<string> getTasksForTag(int user Id, chaîne de caractères) {
auto v = en attenteSorted(userId);
vecteur <string> rés;
pour (auto &t : v) si (t.tags.count(tag)) res.push_back(t.description);
retour rés;
}

vide complet Tâche(int utilisateur Id, tâche int Id) {
si (!userTasks.count(userId)) retourne;
si (!tasks.count(taskId)) retourne;
si (!userTasks[userId].count(taskId)) retourne;
si (!tasks[taskId].complété) tâches[taskId].complété = true;
}

particulier:
struct Tâche {
description de la chaîne;
Int dû;
tags non ordonnés_set<string>;
bool terminé;
Tâche(string d, int du, vector<string> tg)
: description(d), due(du), tags(tg.begin(), tg.end()), complété(faux) {}
};

int suivant Id;
non ordonné_map<int, Tâche> tâches; // tâche Id → Tâche
utilisateur non classé_map<int, non classé_set<int>> Tâches; // utilisateur Id → jeu de tâches Ids

// vecteurs de retour des tâches en attente triées par date d'échéance
vector<Task> en attenteSorted(utilisateur int) Id) {
vecteur<Tâche> v;
si (!userTasks.count(userId)) retourne v;
pour (int id : userTasks[userId]) {
Tâche &t = tâches[id];
si (!t.complété) v.push_back(t);
}
Tri(v.begin(), v.end(), [](const Task &a, const Task &b) {
retour a.due < b.due;
});
retour v;
}
};
«» "
</détails>

---

Qu'est-ce que la création d'une liste de todo ?
À première vue, il ressemble à un simple problème de structure de données de style CRUD.
Mais dans une interview vous êtes en fait testé sur:

1. **Conception orientée objet** – comment vous modélisez *tâches*, *utilisateurs* et la liste elle-même.
2. **Scalabilité et complexité** – même si LeetCode limite les appels à 100, vous devriez toujours viser **O(1) add** et **log-linearity fetches**.
3. **Manipulation des cas** – balises, identifiants d'utilisateur en double, identifiants de tâches inexistants, etc.
4. **Lisibilité du code** – les intervieweurs recherchent un code propre et commenté.

### Bonne, mauvaise et laid: une liste de contrôle rapide
C'est bien, c'est mal.
C'est pas vrai.
Une séparation claire des responsabilités (TodoList vs. Task). Le tri sur chaque fetch peut être gaspillé si vous avez beaucoup de tâches. Autres
- Oui. Utilisation de copies défensives (étiquettes, chaînes de caractères). Les structures mutables (`list` des taskIds) peuvent masquer les bogues lorsque les tâches sont supprimées. Autres
O(1) `addTask` grâce à des cartes de hachage. La tâche ' doit vérifier l'adhésion de l'utilisateur - une analyse linéaire si vous gardez un vecteur. Autres
"GetAllTasks" / "getTasksForTag" partagent un helper commun – pas de duplication de code." "GetAllTasks" / "getTasksForTag" partage un helper commun – pas de duplication de code. Autres

---

Aperçu de la conception

- Oui. 1. Modèle de données

Élément Représentation Justification
- C'est quoi ?
**Tâche**. Objet avec champs: `id`, `description`, `dueDate`, `tags` (`Set<String>`), `complété` (bool). Conserve tous les attributs de tâches ensemble et prend en charge les mises à jour O(1). Autres
**User → Tâches**= `Map<userId, List<taskId>>` (ou `unordered_map<int, vector<int>>` dans C++). Recherche simple et rapide d'une liste de tâches utilisateur. Autres
**Identification mondiale** Id' (C++). Garantir des ID de tâches uniques au niveau mondial. Autres

> **Pourquoi pas un TreeSet par utilisateur? * *
> Avec des dates d'échéance uniques, nous pourrions garder un `TreeMap<dueDate, taskId>` par utilisateur. Cela donnerait *O(log k)* aller chercher sans trier.
> Cependant, le problème garantit des appels** de 100 et de petites tailles de données, de sorte qu'un simple balayage linéaire + "sort" est *plus que suffisant* et beaucoup plus facile à mettre en œuvre.

- Oui. 2. Ventilation des opérations

Méthode Complexe Raison
C'est pas vrai.
"addTask" **O(1)** Autres
"getAllTasks" **O(k log k)** Autres
"getTasksForTag" **O(k log k)**= Même chose qu'un filtre `tag`. Autres
"completeTask" (en anglais seulement) **O(1)** Autres

- Oui. 3. Fil‐sécurité (bonus facultatif)
La solution Java fournie utilise `ConcurrentHashMap` et conserve le `taskCounter` comme un `int` simple.
Si l'on vous a demandé une implémentation *thread‐safe*, vous devez :

* Enveloppez l'accroissement du compteur dans un bloc "synchronisé" ou utilisez `AtomicInteger`.
* Gardez `tâches utilisateur` comme `concurrent HashMap<entier, CopierSurWriteArrayList<entier>>`.
* Marquez `complété` en utilisant `AtomicBoolean`.

Pour LeetCode c'est trop de compétences, mais montrer la connaissance de la réciprocité peut impressionner les gestionnaires d'embauche.

---

L'échantillon est lancé

««« texte clair
Entrée :
["TodoList", "addTask", "getAllTasks", "getTasksForTag", "completTask", "getAllTasks"]
[[],[1,"acheter du lait",3,["épiceries"],[1],[1,"épiceries"],[1,1],[1]]

Produit :
[null,1,["acheter du lait"],["acheter du lait"],null,[]]
«» "

1. Créez une nouvelle liste.
2. Ajouter une seule tâche → ID `1`.
3. `getAllTasks` renvoie `["acheter du lait"]`.
4. `getTasksForTag` (tag = `"grociers"`) retourne la même chose.
5. `completeTask(1,1)` marque qu'elle a été faite.
6. Final `getAllTasks` donne une liste vide.

Toutes les langues fournies s'en occupent exactement comme prévu.

---

Que faire pour pratiquer

Une idée pratique Autres
- Oui.
**Tricks Hash-map**= Implémenter un cache qui invalide après *n* hits. Autres
**Set vs. List**.Construisez un petit cache LRU pour décider entre la suppression O(1) et la suppression. O(log n) recherche. Autres
**Concurrence**= Écrire un `Singleton` avec un compteur `volatile` et tester avec plusieurs fils. Autres
**Tests**=Créer des tests unitaires qui couvrent : l'utilisateur inexistant, les étiquettes dupliquées, le marquage déjà complété. Autres

---

Dernier verdict
Vous venez de résoudre un problème de LeetCode qui *est juste sur les algorithmes*, mais sur le design.
La clé à retenir : ** modélisez bien le problème**, nettoyez votre code et soyez prêt à discuter *pourquoi* vous avez choisi une structure de données particulière.

C'est là, chers amis, la marque d'un ingénieur de niveau supérieur, tant pour les entrevues que pour les projets du monde réel. C'est ce qu'il a dit.

---


**Mots clés pour les recruteurs**: conception orientée objet, carte de hachage, opérations O(1), copie défensive, concurrence, code propre, LeetCode, compétences d'entrevue.