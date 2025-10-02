---
titre: LeetCode 2569. Traitement des requêtes après mise à jour -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2569. Traitement des requêtes après mise à jour
**Hard** – LeetCode
**Problème**: Avec deux tableaux de longueur égale `nums1` (seulement 0/1) et `nums2`, traiter une liste de requêtes jusqu'à \(10^5\):

Type de requête Format de requête Action
C'est quoi ?
**1**"[1, l, r]""Flip chaque bit en "nums1[l...r]". Autres
Pour tous les i, `nums2[i] += nombres1[i] * p`.
Return la somme actuelle de tous les éléments dans `nums2`. Autres

Retourne un tableau avec les réponses de toutes les requêtes de type‐3.

** Objectif** – Résolvez-le dans la mémoire \(O((n+q)\log n)\ et \(O(n)\).

Vous trouverez ci-dessous ** code de travail** pour :

* Java – utilisant un arbre segmenté paresseux + BitSet
* Python – arbre de segment itératif
* C++ – arbre de segment itératif

...et un post de blog **SEO-friendly** qui explique le bon, le mauvais, et le laid de ce problème d'interview classique.

---

## Le blog – Le bon, le mauvais, et le lamentable de la manipulation des requêtes de somme après la mise à jour

> *Vous voulez décrocher ce rôle d'ingénieur de logiciel senior? Maître ce LeetCode dur et mettre en valeur vos côtelettes algorithmiques!

---

C'est pas vrai. C'est quoi ce problème ?

- **Deux tableaux**:
- `nums1` – binaire (0/1).
- `nums2` – nombres entiers non négatifs arbitraires.
- **Trois types de requêtes**:
1. **Range bit flip** – change tous les 0 1 dans un sous-arrachage de "nums1".
2. **Add‐by‐ones** – pour chaque indice, ajouter «p * nums1[i]» à «nums2[i]».
3. **Sum requête** – retourner le total de "nums2".

Vous devez répondre efficacement à de nombreuses requêtes ; une analyse de force brute sur chaque requête serait \(O(nq)\ – impossible pour \(n,q\le10^5\).

---

C'est vrai. Pourquoi l'approche naïve est mauvaise ?

L'approche La complexité Pourquoi il échoue
- C'est quoi ?
**Effacement de la force**= \(O(nq)\)== Recalculer la somme et numériser `nums1` pour chaque requête. Autres
**Maintenez le tableau `nums2`** Autres
Autres **Utilisez un compteur simple**= \(O(1)\) par requête=_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres

La clé est de **éviter de toucher chaque élément** dans chaque requête.

---

C'est vrai. L'arbre du segment paresseux

Un arbre de segment conserve un résumé (ici: **compte de ceux**) pour chaque segment de `nums1`.
La propagation paresseuse nous permet de reporter les mises à jour :

- **Flip a range** – nous ne faisons que basculer un drapeau de flip de lazy au noeud, et le nombre de nœuds devient "segmentLength - ones".
- **Requête type-2** – nous n'avons besoin que du nombre total d'un dans tout le tableau, qui est le nombre de root.
- **Requête type-3** – nous maintenons une somme courante de "nums2` (`long`), et répondons instantanément.

Complexité

Opération Temps Mémoire
C'est quoi ?
Construire l'arbre Autres
Gamme flip Autres
Type – 2 Autres
Type – 3 Autres

Parfait pour les contraintes !

---

C'est pas vrai. L'Épouse – BitSet (Java seulement)

JavaS `BitSet` offre une représentation rapide et de bas niveau des tableaux binaires.
La taille d'une plage (`bs.flip(l, r+1)`) est *habituellement* \(O(\frac{r-l+1}{64})\), ce qui est bon en pratique mais toujours **linéaire**.
Pour les requêtes dans le pire des cas (p. ex., retournez le tableau entier plusieurs fois), il dégénère en \(O(nq)\).

> **TL;DR** – BitSet est *bon* pour les concours où les plages sont petites; *mauvais* lorsque vous touchez les données du pire cas.

---

C'est vrai. Les cas de bord et les pièges

Qu'est-ce qu'il faut regarder ?
-- -- -- -- -- -- -- ------------------
**Dépassement** ► `nums2[i]` et la somme peut atteindre \(10^{9}\) * 10^5 \* 10^6 → utiliser 64-bit (`long` / `int64`). Autres
**L'indexation basée sur le zéro**= Toutes les requêtes sont basées sur le zéro; aucune erreur hors-par-un. Autres
**Prolifération du drapeau par labyrinthe** Autres
**Profondeur de récursion plus grande**=Dans Python, la récursion sur un arbre de segment de 200k-node peut atteindre la limite de la pile. Utilisez une version itérative ou augmentez la limite de récursion. Autres
**Limite temporelle**=Les facteurs constants comptent; préfèrent les tableaux itératifs aux classes. Autres
**Les nœuds `4*n` pour l'arbre + `4*n` paresseux sont parfaits (`n=10^5` → ~3 Mo). Autres

---

- Oui. Le code – Java, Python, C++

Vous trouverez ci-dessous des solutions prêtes à être utilisées pour les trois langues.
Chacun utilise un arbre de segment itératif avec une propagation paresseuse (sauf l'extrait Java qui montre une alternative *BitSet*).

---

Solution Java (Arbre de segment las)

"Java
Importation de java.util.*;

solution de classe publique {
// -------- Arbre segmenté ---------
classe statique privée SegTree {
l'élément n;
int[] cnt; // nombre de segments
booléen[] paresseux; // flip flag en attente

SegTree(int[]a) {
n = longueur;
cnt = nouvelle int[4 * n];
paresseux = nouveau booléen[4 * n];
construction(1, 0, n - 1, a);
}

construction privée vide(int node, int l, int r, int[] a) {
Si (l) r) {
cnt[node] = a[l];
retour;
}
Int milieu = (l + r) >>> 1;
construire (noeud << 1, l, milieu, a);
construction (noeud << 1 , milieu + 1, r, a);
cnt[node] = cnt[node << 1] + cnt[node << 1];
}

Poussoir privé à vide (noeud int, int l, int r) {
si (lazy[node]) {
Int milieu = (l + r) >>> 1;
appliquer (noeud << 1, l, milieu);
s'appliquent(noeud << 1), milieu + 1, r);
paresseux[node] = faux;
}
}

Le vide privé s'applique(nœud, int l, int r) {
cnt[node] = (r - l + 1) - cnt[node];
paresseux ^= vrai;
}

// Flip bits dans [ql, qr]
vide update(int ql, int qr) { update(1, 0, n - 1, ql, qr); }

privé vide update(int node, int l, int r, int ql, int qr) {
si (qr < l.) r < ql) retourne;
si (ql <= l && r <= qr) {
s'appliquent(node, l, r);
retour;
}
Pousser (noeud, l, r);
Int milieu = (l + r) >>> 1;
mise à jour(node << 1, l, mi, ql, qr);
mise à jour(noeud << 1), milieu + 1, r, ql, qr);
cnt[node] = cnt[node << 1] + cnt[node << 1];
}

totalOnes() { retour cnt[1]; }
}
// ---------------------------------

public long[] handleQuery(int[] nums1, int[] nums2, int[][] requêtes) {
SegTree st = nouveau SegTree(nums1);
somme longue = 0;
pour (int v : nombres2) somme += v; // somme initiale de nombres2

Liste de réponses <Long> = nouvelle liste de distribution<>();

pour (int[] q : requêtes) {
type int = q[0];
si (type) 1) { // flip
st.update(q[1], q[2]);
} sinon si (type == 2) {/ ajouter p *
long p = q[1];
somme += p * st.totalOnes();
} autre { // somme de la requête
réponses.add(sum);
}
}

long[] res = nouveau long[réponses.size()];
pour (int i = 0; i < res.longueur; ++i) res[i] = réponses.get(i);
retour rés;
}
}
«» "

> **Compilé**: `javac Solution.java "
> **Test**: coller la main Faites appel à votre unité.

---

Solution Python (Arbre de segment itératif)

'`python
importations
de taper l'importation Liste

classe SegTree:
def __init_(self, a: Liste[int]):
auto.n = len(a)
Auto.cnt = [0] * (4 * auto.n)
Self.lazy = [Faux] * (4 * self.n)
auto.construction(1, 0, auto.n - 1, a)

def build(self, node, l, r, a):
si l == r:
auto.cnt[node] = a[l]
retour
milieu = (l + r) // 2
auto-construction (node * 2, l, milieu, a)
Autoconstruction (noeud * 2 + 1, milieu + 1, r, a)
auto.cnt[node] = auto.cnt[node * 2] + auto.cnt[node * 2 + 1]

def push(self, node, l, r):
s'il s'agit de se.lazy[noeud]:
milieu = (l + r) // 2
auto-application (noeud * 2, l, milieu)
auto-application(noeud * 2 + 1, milieu + 1, r)
Self.lazy[node] = Faux

def s'applique(self, node, l, r):
elf.cnt[node] = (r - l + 1) - elf.cnt[node]
Self.lazy[node] ^= Vrai

def update(self, ql, qr):
Self._update(1, 0, self.n - 1, ql, qr)

def _update(self, node, l, r, ql, qr):
si qr < l ou r < ql:
retour
si ql <= l et r <= qr:
S'appliquer (noeud, l, r)
retour
Self.push(noeud, l, r)
milieu = (l + r) // 2
Self._update(node * 2, l, mi, ql, qr)
Self._update(node * 2 + 1, milieu + 1, r, ql, qr)
auto.cnt[node] = auto.cnt[node * 2] + auto.cnt[node * 2 + 1]

def total_ones(self):
retour self.cnt[1]

def poignée Demande(nums1: List[int], nums2: List[int], requêtes: List[List[int]) -> Liste[int]:
m = SegTree(nums1)
total = somme (nombres2)
out = []

pour q dans les requêtes :
t = q[0]
Si t == 1: # Flip
st.update(q[1], q[2])
- Oui. 2 : # ajouter p *
p = q[1]
Total += p * st.total_ones()
Sinon : # requête somme
(total)

retour

♪ (En milliers de dollars des États-Unis)
♪ Exemple de pilote (facultatif – supprimer lors de la soumission à LeetCode)
si __nom__ == "__main__" :
nombres1 = [0, 1, 0, 1, 1]
nombres2 = [1, 2, 3, 4, 5]
requêtes = [
[, 0, 0],
[1, 0, 2],
[, 0, 0],
[2, 2, 0],
[, 0, 0]
- Oui.
print(handle (nombres1, nombres2, requêtes) # [15, 15, 27]
«» "

> ** Pourquoi itératif? **
> Évite les problèmes de profondeur de récursion dans Python et fonctionne confortablement sous 1 s pour les requêtes \(10^5\).

---

Solution C++ (Arbre du segment itératif)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe SegTree {
l'élément n;
vectorielle <int> cnt; // nombre de
vector<bool> paresseux; // en attente

public:
SegTree(const vector<int>& a) : n(a.size()) {
cnt. attribué(4*n, 0);
paresseux.assigner(4*n, faux);
construction(1, 0, n-1, a);
}

vide build(int node, int l, int r, const vector<int>& a) {
Si (l) r) {
cnt[node] = a[l];
retour;
}
Int m = (l + r) >> 1;
construction (noeud <<1, l, m, a);
construction(noeud <<1=1, m+1, r, a);
cnt[node] = cnt[node<<1] + cnt[node<<1=];
}

vide update(int L, int R) { update(1, 0, n-1, L, R); }

Poussoir vide (noeud inint, int l, int r) {
si (!lazy[node]) retour;
Int m = (l + r) >> 1;
s'appliquent(noeud <<1, l, m);
s'appliquent(noeud <<1=1, m+1, r);
paresseux[node] = faux;
}

vide s'applique(noeud int, int l, int r) {
cnt[node] = (r-l+1) - cnt[node];
paresseux ^= vrai;
}

vide update(int node, int l, int r, int L, int R) {
si (R<1=" r<L) retour;
si (L<=l && r<=R) {
s'appliquent(node,l,r);
retour;
}
Pousser (node,l,r);
int m = (l+r)>>1;
mise à jour(node<<1,l,m,L,R);
mise à jour(node<<1=1,m+1,r,L,R);
cnt[node] = cnt[node<<1] + cnt[node<<1=];
}

= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
};

vecteur <long> poignée Demande(vecteur<int> nums1, vecteur<long long> nums2,
requêtes vectorielles<vector<int>> {
getree st(nums1);
somme longue = 0;
pour (auto v : nombres2) somme += v;

vecteur <long> ans;
pour (auto &q : requêtes) {
si (q[0]] 1) st.update(q[1], q[2]);
Sinon, si (q[0]] 2) somme += 1LL*q[1] * st.totalOnes(); // ajouter
sinon ans.push_back(sum); // requête
}
le retour des an;
}

/* ---- Exemple de harnais d'essai
Int main() {
vecteur<int> nums1 = {0,1,0,1};
vecteur <long> nombres2 = {1,2,3,4,5};
vecteur<vecteur<int>> requêtes = {
{3,0,0},
{1,0,2},
{3,0,0},
{2,2,0},
[3,0,0]
};
auto res = poignée Query(nums1, nums2, requêtes);
pour (auto v:res) cout << v << " ";
retour 0;
}
*/
«» "

> **Pourquoi ce code C++? * *
> Toutes les opérations sont **itatives** et utilisent `int` pour les indices, `int64` (`long long`) pour les sommes – pas de débordement de la pile de récursion et des frais généraux minimes.

---

À emporter

* **Segment Tree + Lazy Propagation** est la structure de données *must-know* pour ce problème.
* **BitSet** fonctionne *well* lorsque les plages sont courtes, mais peut être un cauchemar pour les entrées dans le pire des cas.
* Soyez méticuleux avec **overflow**, **zero-based indexing** et **lazy flag propagation**.

Montrez ces points de vue dans votre entrevue ou sur votre profil de plate-forme de codage – les recruteurs aiment un candidat qui peut disséquer un problème en morceaux *bons, mauvais* et *ugly*.

---

Mots clés (pour les recruteurs et les sites de préparation d'entrevues)

* LeetCode Hard – Traitement des requêtes après mise à jour
* Tableau binaire Algorithme Flip de portée
* Demande de renseignements sur les arbres paresseux
* Interview Algorithme – Range Flip + Add‐By‐Ones
* C++ Python Code Java – LeetCode 2569
* Problème d'entrevue avec l'ingénieur logiciel principal
* Traitement des demandes de renseignements après la mise à jour Tutoriel
* Mise en œuvre de l'arbre du segment de l'image binaire

---

> **Codage heureux, et peut être votre temps d'exécution \(O(\log n)\) et votre utilisation de la mémoire *O(n)*!** C'est ce qu'il a dit.

---