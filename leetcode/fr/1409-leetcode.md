---
titre: LeetCode 1409. Des questions sur une permutation avec la clé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 1409 – Demande sur une permutation avec la clé
> **Cible auprès du public:** Développeurs front‐end / back‐end, passionnés de datastructure, passionnés de préparation d'entrevue
> **Objectif:** Livrez un code propre et bien commenté en **Java, Python et C++** + un article de blog **SEO-friendly** qui met en valeur votre solution de problèmes et vous aide à décrocher votre prochain rôle d'ingénierie logicielle.

---

Table des matières
Ce que vous apprendrez
C'est-à-dire
Description du problème Comprendre les exigences exactes
Pourquoi la solution est importante
Approach Brute-Force : Intuitif mais toujours efficace pour LeetCode
Solution O(n log m) optimale pour les interviews Autres
Java, Python, C++ – prêt à copier et coller
Le bon, le mauvais et l'hommage – un article de référence
Ce que les recruteurs veulent voir

---

Récapitulation des problèmes

Étant donné:

* Un tableau `queries` – chaque élément [1, m].
* Une permutation initiale `P = [1, 2, ..., m]`.

Pour chaque requête `q = requêtes[i]`:

1. Trouvez l'index 0 de `q` dans `P`.
2. Déplacer `q` vers l ' avant de `P`.
3. Enregistrez l'index avant le déménagement.

Retourner la gamme d'indices enregistrés.

> **Constraints**
> 1 ≤ m ≤ 103 '
> • `1 ≤ requêtes.longueur ≤ m "
> • `1 ≤ requêtes[i] ≤ m "

---

- Oui. Pourquoi ce problème est un «Gold‐Mine» pour les entrevues

Autres Ce que les recruteurs se soucient de ce problème
-- -- -- -- -- -- -- ------------------------------------------------------------------
**Savoirs sur la structure des données**Vous utilisez les permutations, l'indexation et les arbres Fenwick en option. Autres
Vous identifiez une solution O(n2) naïve contre une solution O(n log n). Autres
Autres **Codage style et commentaires**= Code propre et lisible avec manipulation de la caisse. Autres
**Recours dans l'espace-temps**Vous discutez quand une approche simple est acceptable. Autres
**Résoudre des problèmes sous contraintes**= m ≤ 1000 → force brute OK; mais vous affichez toujours une méthode évolutive. Autres

---

## 3-- Solution Brute-Force (intuitive)

Complexité
* **Temps:** O(n × m) (meilleure caisse 1 000 × 1 000 = 106 opérations – parfaitement bonne pour LeetCode).
* **Espace:** O(1) extra (supprimé).

Mise en œuvre Java

"Java
solution de classe publique {
public int[] processQueries(int[] requêtes, int m) {
int[] perm = nouvelle int[m];
pour (int i = 0; i < m; i++) perm[i] = i + 1; //

int[] result = nouvelle int[queries.longueur];

pour (int idx = 0; idx < requêtes.longueur; idx++) {
int q = requêtes[idx];
= 0;
// trouver l'index
pour (int i = 0; i < m; i++) {
si (perm[i] == q) {
pos = i;
pause;
}
}
résultat[idx] = pos;

// passer à l ' avant (éléments de déplacement à droite)
température int = perm[pos];
pour (int i = pos; i > 0; i--) perm[i] = perm[i - 1];
perm[0] = température;
}
le résultat du retour;
}
}
«» "

Mise en œuvre de Python

'`python
Solution de classe:
def processus Questions(self, requêtes: List[int], m: int) -> Liste[int]:
perm = liste(intervalle(1, m + 1))
res = []

pour q dans les requêtes :
pos = perm.index(q) # O(m) recherche
res.append(pos)
perm.pop(pos) # O(m) poste
perm.insert(0, q) # O(m) poste
retour res
«» "

Mise en œuvre du C++

'`cpp
solution de classe {
public:
vector<int> processQueries(vector<int>& requêtes, int m) {
vecteur <int> perm(m);
iota(perm.begin(), perm.end(), 1); // valeurs basées sur 1

vecteur<int> rés;
pour (int q : requêtes) {
int pos = find(perm.begin(), perm.end(), q) - perm.begin();
res.push_back(pos);
Int val = perm[pos];
perm.erase(perm.begin() + pos); // quart gauche
perm.insert(perm.begin(), val); // poste droit
}
retour rés;
}
};
«» "

> **Pourquoi est-ce acceptable? * *
> Les contraintes sont minuscules (`m ≤ 1000`). Même avec une boucle emboîtée, l'exécution reste bien en dessous de 100 ms sur LeetCode.

---

## 4=2 Solution optimale – Arbre de Fenwick (arbre indexé de la baie)

Quand `m` grandit (par exemple 105 ou 106), la solution naïve devient trop lente.
A **Fenwick Tree** nous permet de maintenir les positions actuelles de permutation et de les mettre à jour dans **O(log m)** time.

- Oui. Comment ça marche

1. **Capping**
* Placez chaque nombre à une position "m + i" (pour que les indices ne deviennent jamais négatifs).
* Maintenir un arbre Fenwick sur la taille `2m` pour suivre le nombre d'éléments actuellement devant chaque index.

2. **Querité**
* L'indice actuel d'un nombre `x` est la somme du préfixe jusqu'à sa position actuelle – c'est-à-dire le nombre d'éléments avant lui.

3. **Déplacer vers l'avant**
* Définissez la valeur de l'arborescence à la position actuelle à `0`.
* Placez l'élément à la prochaine fente libre de -front (à partir de `m`) et définissez sa valeur arborescente à `1`.
* Mettre à jour `pos[x]` vers la nouvelle fente.

Complexité
* **Heure:** O(n + m) log m)
* **Espace:** O(m)

Mise en œuvre Java (Fenwick)

"Java
classe Fenwick {
bit[];
l'élément n;
Fenwick(int n) { this.n = n; bit = new int[n + 2]; }

vide add(int idx, int val) {
pour (int i = idx; i <= n; i += i & -i) bit[i] += val;
}
Int sum(int idx) {
int s = 0;
pour (int i = idx; i > 0; i -= i & -i) s += bit[i];
retour s;
}
}

solution de classe {
public int[] processQueries(int[] requêtes, int m) {
int[] res = nouvelle int[queries.longueur];
int[] pos = nouvelle int[m + 1]; // position actuelle de chaque valeur
taille int = 2 * m; // pour éviter les indices négatifs
Fenwick ft = nouveau Fenwick (taille + 2);

// initialiser: tous les éléments de la moitié droite [m+1 .. 2m]
pour (int i = 1; i <= m; i++) {
Pos[i] = m + i;
ft.add(pos[i], 1);
}

int front = m; // prochaine fente avant libre
pour (int i = 0; i < requêtes.longueur; i++) {
int x = requêtes[i];
int curPos = pos[x];
int idx = ft.sum(curPos - 1); // éléments avant x
res[i] = idx;

// passer à l'avant
ft.add(curPos, -1); // supprimer de l'ancienne fente
ft.add(front, 1); // ajouter à la nouvelle fente avant
pos[x] = avant;
front--; // la prochaine requête ira encore plus tôt
}
retour rés;
}
}
«» "

Mise en œuvre du Python (Fenwick)

'`python
Catégorie Fenwick:
def __init_(self, n):
auto.n = n
Autobit = [0]*(n+2)
def add(self, i, delta):
alors que i <= self.n:
Soi.bit[i] += delta
i += et -i
def sum(self, i):
s = 0
alors que i:
s += self.bit[i]
I -= et -i
retour s

Solution de classe:
def processus Questions(self, requêtes: List[int], m: int) -> Liste[int]:
n = lentilles
taille = 2*m
pos = [0]*(m+1)
ft = Fenwick(taille+2)

pour i dans la plage (1, m+1):
Pos[i] = m + i
ft.add(pos[i], 1)

avant = m
res = []
pour x dans les requêtes :
cur = pos[x]
idx = ft.sum(cur-1)
res.append(idx)
ft.add(cur, -1)
ft.add (avant, 1)
pos[x] = avant
avant -= 1
retour res
«» "

Mise en œuvre C++ (Fenwick)

'`cpp
struct Fenwick {
vecteur <int> bit;
l'élément n;
Fenwick(int n=0){init(n);}
vide init(int n){this->n=n; bit.assign(n+2,0);}
vide add(int idx,int val){
pour(; idx<=n; idx+=idx&-idx) bit[idx]+=val;
}
Int sum(int idx){
int s=0;
pour(; idx>0; idx-=idx&-idx) s+=bit[idx];
retour s;
}
};

solution de classe {
public:
vector<int> processQueries(vector<int>& requêtes, int m) {
int sz = 2*m;
Fenwick ft(sz+2);
vecteur <int> pos(m+1), res;
pour(int i=1;i<=m;i++){
Pos[i] = m + i;
ft.add(pos[i],1);
}
int front = m;
pour(int x: requêtes) {
int cur = pos[x];
int idx = ft.sum(cur-1);
res.push_back(idx);
ft.add(cur,-1);
ft.add(front,1);
pos[x] = avant;
avant...
}
retour rés;
}
};
«» "

> ** Quand devrais-tu choisir ça ? * *
> • `m` > 105
> • Vous voulez un O(log m) garanti par requête (par exemple, pour les systèmes de streaming).
> • Démontre une connaissance approfondie du BIT.

---

C'est pas vrai. L'échange de bonnes pratiques

Scénario Solution préférée Raison
- C'est quoi ?
"m ≤ 103" " Brute-force" Code plus simple, moins de lignes, plus facile à expliquer. Autres
`m` grandit ou vous voulez montrer l'évolutivité. Autres
Autres Vous interviewez pour un rôle *codage-lourd*. Autres
Autres Vous êtes dans un *systems* interview. Autres

> **Conseil:**
> Commencez par la force brute, expliquez sa complexité, puis demandez à l'intervieweur si une méthode plus efficace est nécessaire. Cela montre l'humilité et l'adaptabilité.

---

C'est pas vrai. Cas & robustesse Contrôles

Ce que nous traitons dans le code
C'est pas vrai.
Des questions dupliquées Aucun problème – nous déplaçons simplement le même nombre à nouveau. Autres
Autres En interrogeant l'élément frontal, index = 0, les opérations arborescentes suppriment et réinsèrent la même fente – toujours O(log m). Autres
Le plus petit `m` (1)=" perm.index(1)` retourne 0; le déplacer vers le front ne fait rien – fonctionne toujours. Autres

---

Les dernières pensées et à emporter

* **Afficher une solution simple** – cela prouve que vous pouvez traduire un énoncé de problème en code immédiatement.
* **Puis, "Lève la barre"** – présentez une alternative O(n log n) en discutant quand elle compte.
* ** Expliquez clairement les compromis** : pourquoi les contraintes permettent une force brute, mais une méthode évolutive montre un aperçu plus profond.
* **Conservez votre code propre** – utilisez des noms de variables significatifs, commentez la logique de Fenwick et formatez de façon uniforme.

> **Conseil pro pour votre entrevue**:
> *Demandez à l'intervieweur si `m` avaient 105 ans, voulez-vous toujours la même approche?
> Cela lance une conversation sur la complexité du temps et met en évidence votre capacité à penser à l'échelle.

---

Prêt à écrire la prochaine solution gagnante ?

N'hésitez pas à copier/coller les extraits de code ci-dessus dans LeetCode.
Si vous souhaitez pratiquer plus, essayez de modifier le problème:
* ** Variante** – au lieu de passer à l'avant, passer au milieu.
* **Suivi** – calculer la permutation après toutes les requêtes.

Bon codage ! C'est ce qu'il a dit.

---

*Préparé par **[Votre nom]** – Enthousiaste de la structure des données, programmeur compétitif et coach d'entrevue. *
---
<blockquote>
Votre meilleur entretien de code n'est pas sur la réponse, mais sur le processus de pensée. *
</blockquote>

---

Lire plus

1. Arbre Fenwick – <https://cp-algorithms.com/data_structures/fenwick.html>
2. Binary indexé Arbre sur permutations – <https://codeforces.com/blog/entry/79354>
3. Utilisation de `iota` en C++ – <https://en.cppreference.com/w/cpp/algorithm/iota>

Bon apprentissage ! (en milliers de dollars)
---

** Fin de la solution**.