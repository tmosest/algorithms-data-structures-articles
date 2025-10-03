---
titre: LeetCode 631. Conception de la formule de somme Excel - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes (LeetCode 631 – Formule de somme Excel de conception)

On vous demande de mettre en place un petit tableur Excel qui supporte trois opérations :

Description de la méthode
C'est pas vrai.
"Excel(hauteur de l'int, largeur de l'omble)" Initialisez une grille `hauteur × largeur' (lignes 1‐hauteur, colonnes 'A'‐largeur) avec tous les zéros. Autres
"evit set(int rang, colonne char, int val)" Écrire une valeur entière dans une cellule. Cela élimine toute formule qui aurait pu être là. Autres
"int get(int range, colonne char)" Lire la valeur entière actuelle d'une cellule. Autres
`int sum(int range, colonne char, List<String> numbers)`=Définir une formule pour une cellule. La valeur de la cellule devient la somme des cellules/intervalles en « nombres ». La formule reste jusqu'à ce que la cellule soit écrasée par un « set » ou un autre « sum ». Les références ne forment jamais un cycle. Autres

**Contrôles* *

* `1 ≤ hauteur ≤ 26` (max. 26 rangs)
* `'A' ≤ largeur ≤ 'Z'' (max. 26 colonnes)
* `1 ≤ nombre d'appels ≤ 100`
* `numéros` contient 1-5 références, chacune soit `"ColRow"` ou `"ColRow1:ColRow2"` (y compris rectangle)
* `-100 ≤ valeur ≤ 100`

---

Conception de haut niveau

Le défi clé : lorsqu'une cellule change de valeur (soit par « set » soit en redéfinissant sa propre formule), chaque cellule qui en dépend doit aussi être mise à jour – *et* que la propagation peut en cascade.

La façon la plus simple de gérer ceci est:

1. **Conservez la valeur brute de chaque cellule** – un tableau 2-D (ou une carte de hachage 1-D clé par `"ColRow"`).
2. **Store a formula definition** per cell when `sum` is appeled – essentiellement une liste de toutes les cellules qu'il regarde.
3. **Maintenir un graphique de dépendance inverse**:
`dépendance[x] → { y=Y dépend de x }`.
Chaque fois qu'une formule est définie, pour chaque cellule référencée `x` nous ajoutons la cellule actuelle à `dépendant[x]`.
4. **Modifications proposées**:
*Lorsque la valeur d'une cellule change* – exécutez une première profondeur (ou largeur) sur le graphique inverse et recalculez chaque enfant. Comme le graphique est acyclique, cette promenade se terminera toujours.

La propagation est *pas* chère parce que la feuille de calcul est minuscule 26×26) et nous avons au plus 100 opérations. Pas besoin d'un type topologique complet; un simple DFS/BFS suffit.

---

Code complet

Ci-dessous sont **trois implémentations complètes et autonomes** (Java, Python, C++).
Tous les trois partagent la même idée algorithmique décrite ci-dessus.

> **Conseil pour les entrevues** – Dans une entrevue, vous pouvez expliquer que vous utilisez une *liste d'adjacence* pour les dépendances inverses, et que la propagation est faite par DFS/BFS, faisant la solution O(N) par mise à jour où N est le nombre de cellules dépendantes.

### 2.1 Java

"Java
Importation de java.util.*;

classe Excel {

les rangées privées finales d'inte, de cols;
valeur finale privée int[]; / valeur numérique brute
carte finale privée<String, liste<String>> formule; // cellule → liste de références
liste finale privée<Set<String>> dépendants; // cellule → ensemble de cellules qui en dépendent

// Aide à transformer "B5" en "B5" (clé canonique)
clé de chaîne privée(int r, char c) { retourner "" + c + r; }

public Excel(hauteur de l'int, largeur de l'omble) {
ceci.rows = hauteur;
ce.cols = largeur - 'A' + 1;
ceci.value = nouveau int[rows][cols];
ce.formula = nouveau HashMap<>();
ceci.dépendents = nouveau ArrayList<>(lignes * cols);
pour (int i = 0; i < lignes * cols; ++i) dépendants.add(new HashSet<>());
}

ensemble public vide(ligne int, colonne char, int val) {
Cellule chaîne = clé (ligne, colonne);
// Supprimer toute ancienne formule
formule.supprimer(cellule);
// Mettre à jour les bords inversés
desdépenses claires(cellules);
valeur[ligne-1][colonne-'A'] = valeur;
// Propager le changement
propagation(cellule);
}

int public get(int rang, colonne de caractères) {
valeur de retour[ligne-1][colonne-'A'];
}

public int sum(int rang, colonne d'omble, liste des numéros <String>) {
Cellule chaîne = clé (ligne, colonne);
// Supprimer la formule précédente et ses bords
formule.supprimer(cellule);
desdépenses claires(cellules);

// Construire la liste de référence (avec des duplicatas comptés)
Liste<String> refs = buildRefs(nombres);

// Calculez la valeur maintenant
= 0;
pour (String ref : refs) {
somme += getCellValue(ref);
}
valeur[ligne-1][colonne-'A'] = somme;
formule.put(cellule, réfs);

// Enregistrer les dépendances inverses
pour (String ref : refs) {
dépendants.get(cellToIndex(ref))add(cell);
}

// Propager la nouvelle valeur
propagation(cellule);
la somme de retour;
}

// ---- Aides -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

// Retourner la valeur numérique d'une chaîne de référence (manipulation d'une cellule simple ou d'une plage)
Int privé getCellValue(String ref) {
int r1 = ref.charAt(1) - '0';
si [ref.longueur()] 3) {// cellule simple, par exemple, "B5"
valeur de retour[r1-1][ref.charAt(0)-'A'];
} autre { // plage "B1:D3"
les parties de chaînes = ref.split(":");
int rStart = Integer.parseInt(parties[0].substring(1));
int rEnd = Integer.parseInt(parties[1].substring(1));
Char cStart = pièces[0].charAt(0);
Char cEnd = parties[1].charAt(0);
= 0;
pour (int r = rStart; r <= rEnd; ++r) {
pour (char c = cDémarrage; c <= cFin; ++c) {
somme += valeur[r-1][c-'A'];
}
}
la somme de retour;
}
}

// Construire une liste de références; les duplicatas sont conservés (ils additionnent deux fois)
liste privée<String> buildRefs(liste<String> nombres) {
Liste<String> refs = nouvelle liste de distribution<>();
pour (String s : nombres) {
si (!s.contient(":") {
réfs.add(s);
} autre {
Parties de chaînes = s.split(":");
int r1 = Integer.parseInt(parties[0].substring(1));
int r2 = Integer.parseInt(parties[1].substring(1));
Char c1 = parties[0].charAt(0);
Char c2 = parties[1].charAt(0);
pour (int r = r1; r <= r2; ++r) {
pour (charc = c1; c <= c2; ++c) {
refs.add(" + c + r);
}
}
}
}
retour refs;
}

// Enlever tous les bords inversés qui sortent de cette cellule
vide privé défrichéDépendants(cellule de fixation) {
int idx = celluleToIndex(cell);
pour (Set<String> set : dependents) set.remove(cell);
}

// Changement de valeur de la propriété pour toutes les personnes à charge
le vide privé se propage (cellule fixe) {
Deque<String> q = nouveau ArrayDeque<>();
q.add(cellule);
Set<String> visité = nouveau HashSet<>();
visité.add(cell);

alors que (!q.isEmpty()) {
Chaîne cur = q.poll();
pour (Enfant en attente : personnes à charge.get(cellToIndex(cur))) {
// Recalculer la valeur de l'enfant
Liste <String> refs = formula.get(child);
Int nouveau Val = 0;
pour (String ref : refs) newVal += getCellValue(ref);
valeur[child.charAt(1)-'1'[child.charAt(0)-'A'] = newVal;
si (visited.add(child)) q.add(child);
}
}
}

// Convertir la chaîne de cellules "B5" en un index dans la liste des personnes à charge
cellule interne privéeToIndex(cellule de maintien) {
retour (cell.charAt(1) - '1') * cols + (cell.charAt(0) - 'A');
}
}
«» "

---

2.2 Python

'`python
classe Excel & #160;:
def __init__(self, hauteur: int, largeur: str):
Self.rows, self.cols = hauteur, ord(largeur) - 64 # 'A' -> 1
Self.val = [[0] * Self.cols pour _ dans la plage (hauteur)]
auto.formula = {} # cellule -> liste des références
indépendants = {} # cellule -> ensemble de cellules qui en dépendent

def _cell_key(self, r: int, c: str) -> str:
retourner f"{c}{r}"

def set(self, ligne: int, colonne: str, val: int) -> Aucun:
key = self._cell_key(row, colonne)
Self.val[row-1][ord(colonne)-65] = valeur
Self.formula.pop(clé, Aucun)
_propagate(clé)

def get(self, ligne: int, colonne: str) -> Int:
retour self.val[row-1][ord(colonne)-65]

def sum(self, ligne: int, colonne: str, nombres: list[str]) -> Int:
key = self._cell_key(row, colonne)
refs = []
pour réf en nombre:
si ':' pas dans ref:
Annexe(ref)
Sinon:
a, b = ref.split(':')
c1, r1 = a[0], int(a[1:])
c2, r2 = b[0], int(b[1:])
pour r dans la plage(r1, r2+1):
pour c dans la plage(ord(c1), ord(c2)+1):
Annexe(f"{chr(c)}{r}")
auto.formula[key] = refs
auto._calc(clé, réfs)
_propagate(clé)
retour self.val[row-1][ord(colonne)-65]

def _calc(self, clé: str, refs: list[str]) -> Aucun:
Total = 0
pour r à réfs:
si ':' pas en r:
cellule = r
Total += autoval[int(cell[1:])-1][ord(cell[0])-65]
Sinon:
# ce bloc n'est jamais touché parce que nous élargissons les plages avant
passer
autoval[int(key[1:])-1][ord(key[0])-65] = total

def _propagate(self, clé: str) -> Aucun:
# construire le graphique de dépendance inverse paresseuse
si la clé n'est pas en soi. personnes à charge:
autonome[clé] = set()
pour dép, refs en autoformula.items():
si la clé dans refs:
self.dependents.setdefault(dep, set()).add(key)

# BFS/DFS
pile = [clé]
vu = {clé}
pendant la pile:
cur = empil.pop()
cur_val = auto.val[int(cur[1:])-1][ord(cur[0])-65]
pour parent, réfs en autoformula.items():
si cur en refs:
auto._calc(parent, réfs)
si parent non vu:
voir.add(parent)
pile.append(parent)
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe Excel {
public:
Excel(hauteur de l'int, largeur du char) {
R = hauteur;
C = largeur - 'A' + 1;
val.assign(R, vecteur<int>(C, 0));
depend.assign(R*C, unordered_set<string>());
}

jeu de vide(int r, char c, int v) {
string key = string(1, c) + to_string(r);
val[r-1][c-'A'] = v;
formule.erase(clé);
propagation(clé);
}

Int get(int r, char c) {
retour val[r-1][c-'A'];
}

int sum(int r, char c, vecteur const <string>& nums) {
string key = string(1, c) + to_string(r);
formule.erase(clé);
clear_dependents(key);

vecteur <string> refs;
pour (auto &s : nombres) {
si (s.find(':') == chaîne::npos) refs.push_back(s);
autres {
parties automatiques = fraction(s), ':');
char c1 = parties[0][0], c2 = parties[1][0];
int r1 = stoi(parties[0].substr(1));
int r2 = stoi(parties[1].substr(1));
pour (int rr = r1; rr <= r2; ++rr)
pour (char cc = c1; cc <= c2; ++cc)
refs.push_back(string(1, cc) + to_string(rr));
}
}

formule[clé] = réfs;
recalc(clé, réfs);
pour (auto &ref : refs) dépend[idx(ref)].insert(key);
propagation(clé);
retour val[r-1][c-'A'];
}

particulier:
la position R, C;
vecteur<vecteur<int>> valeur;
non ordonné_map<string, vector<string>> formule;
vector<unordered_set<string>> dépend;

key(int r, char c) { return string(1,c) + to_string(r); }
int idx(const string& s){ retour (s[1]-'1')*C + (s[0]-'A'); }

vide recalc(cont string& key, const vector<string>& refs){
= 0;
pour (auto &ref : refs) {
si (ref.find(':') == chaîne::npos)
total += val[ref[1]-'1'][ref[0]-'A'];
}
val[key[1]-'1'[key[0]-'A'] = total;
}

le vide se propage (clé de chaîne) {
file d'attente <string> q;
q.push(clé);
_set non ordonné<string> visité {clé};

pendant que [!q.vide()]{
chaîne cur = q.front(); q.pop();
pour (auto &child : dépend[idx(cur)]) {
// Récalculer l ' enfant
auto refs = formule[enfant];
la valeur de l'élément est égale à 0;
pour (auto &r : refs)
si (r.find(':') == chaîne::npos)
tt += val[r[1]-'1'][r[0]-'A'];
val[child[1]-'1'[child[0]-'A'] = tot;
si (visited.insert(child).second) q.push(child);
}
}
}

vector<string> split(chaîne &s de const, char delim) {
vecteur <string> rés;
chaîne de caractères cur;
pour(char ch : s){
if(ch==delim){ res.push_back(cur); cur.clear(); }
autres cur.push_back(ch);
}
res.push_back(cur);
retour rés;
}
};
«» "

---

2.4 C++ (moderne)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe Excel {
particulier:
la position R, C;
vecteur<vecteur<int>> valeur;
non ordonné_map<string, vector<string>> formule;
vector<unordered_set<string>> rev; // bords inversés

string key(int r, char c) { return string(1, c) + to_string(r); }

int toIdx(const string &s) {
retour (s[1]-'1') * C + (s[0]-'A');
}

vide cleanEdges(const string &k) {
pour (auto &s : rev) s.erase(k);
}

le vide se propage(const string &k) {
file d'attente <string> q;
non ordonné_set<string> vis;
q.push(k); vis.insert(k);

pendant que (!q.vide()) {
chaîne cur = q.front(); q.pop();
pour (enfant auto : rev[toIdx(cur)]) {
// Recalculer la valeur de l'enfant
auto refs = formule[enfant];
= 0;
pour (auto &ref : refs) {
si (ref.find(':') == chaîne::npos) {
total += val[ref[1]-'1'][ref[0]-'A'];
}
}
val[enfant[1]-'1'[enfant[0]-'A'] = total;
si (vis.insert(child).second) q.push(child);
}
}
}

public:
Excel(int h, char w) : R(h), C(w - 'A' + 1), val(h, vector<int>(C, 0),
(R*C) {}

jeu de vide(int r, char c, int v) {
chaîne k = clé(r, c);
val[r-1][c-'A'] = v;
formule.erase(k);
clearEdges(k);
se propagent(k);
}

Int get(int r, char c) {
retour val[r-1][c-'A'];
}

int sum(int r, char c, const vector<string> &nums) {
chaîne k = clé(r, c);
formule.erase(k);
clearEdges(k);

vecteur <string> refs;
pour (auto &s : nombres) {
si (s.find(':') == chaîne::npos) refs.push_back(s);
autres {
auto p = fraction(s), ':';
int r1 = stoi(p[0].substr(1));
int r2 = stoi(p[1].substr(1));
char c1 = p[0][0];
char c2 = p[1][0];
pour (int rr=r1; rr<=r2; ++rr)
pour (char cc=c1; cc<=c2; ++cc)
refs.push_back(string(1, cc) + to_string(rr));
}
}

formule[k] = réfs;
la valeur de l'élément est égale à 0;
pour (auto &ref : refs) tot += val[ref[1]-'1'][ref[0]-'A'];
val[r-1][c-'A'] = tot;
// Mettre à jour le graphique inverse
pour (auto &ref : refs) rev[toIdx(ref)].insert(k);

se propagent(k);
retour à domicile;
}

particulier:
vector<string> split(chaîne &s de const, char delim) {
vecteur <string> rés;
chaîne de caractères cur;
pour (charte : s) {
if (ch == delim) { res.push_back(cur); cur.clear(); }
autres cur.push_back(ch);
}
res.push_back(cur);
retour rés;
}
};
«» "

---

---

C'est pas vrai. Pourquoi ça marche

- **Liste d'Adjacence** – Les "dépendants" stockent les bords *réversifs*, afin que nous puissions marcher d'une cellule changée vers l'extérieur sans problèmes de profondeur de récursion.
- **Acyclique** – Parce que seul `sum` peut ajouter des bords, et nous n'ajoutons jamais un bord qui crée un cycle (la spécification garantit une référence acyclique). DFS/BFS est sûr.
- **Complexité** – Chaque mise à jour visite chaque enfant une fois, de sorte que le coût est proportionnel au nombre de cellules touchées, bien en dessous de la taille de la grille.

---

## -- 5-- Interview Points de discussion

1. **Exposer les structures de données** – tableau 2-D pour les valeurs, hash-map pour les formules, liste d'adjacence de dépendance inverse.
2. **Afficher l'algorithme de propagation** – DFS/BFS qui recalcule les enfants.
3. **Discussion des cas de bordure** – Dupliquer les références (comptes deux fois), l'expansion de la portée avant l'évaluation.
4. **Complexité** – O(N) par mise à jour, N = nombre de cellules affectées; pour ≤ 26×26, c'est trivial.

Bonne chance dans votre interview ! C'est ce qu'il a dit.

---

Note finale

Les solutions ci-dessus sont compactes et facilement testables.
Si vous souhaitez prolonger le tableur plus tard (plus de lignes/cols, plus de données), il suffit de passer des tableaux aux dictionnaires – la logique de propagation reste la même.
Bon codage !