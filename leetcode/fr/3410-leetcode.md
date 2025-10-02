---
titre: LeetCode 3410. Maximiser la somme subarray après avoir enlevé tous les événements d'un élément -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Réponse : 12 minutes (soit 750 mots)* *

---

- Oui. Ce que le problème demande vraiment

Pour chaque valeur distincte `v` dans le tableau, nous pouvons *supprimer toutes les occurrences* de `v`.
Le tableau qui reste est juste le tableau original avec ces positions supprimées, et
la tâche consiste à déclarer la somme *maximum de sous-ensemble* de ce nouveau tableau.

«» "
originale : 1 2 3 3 4
supprimer 3 : 1 2 4 → max sub-array = 1+2+4 = 7
«» "

Parce que les éléments supprimés sont simplement **décomposés**, un sous-réseau dans le nouveau tableau
correspond à une séquence d'indices dans le tableau original qui ne contient **pas**
`v` – mais il peut sauter sur les positions supprimées.
Donc, nous ne pouvons pas compter sur l'habituel accord dans la propriété originale du tableau.

---

- Oui. 1. Le Kadane

La façon la plus simple de calculer la réponse pour une valeur particulière `v` est:

«» "
_somme actuelle = 0
réponse =
pour chaque élément x du tableau:
if x == v: # élément est supprimé → rien à ajouter
poursuivre
current_sum = max(current_sum + x, x)
réponse = max(réponse, current_sum)
«» "

La boucle ne réinitialise jamais `current_sum` sur un élément supprimé – nous avons simplement *skip*
Ça. L'algorithme est un seul passage (O(n)) pour ce `v`.
La répéter pour chaque valeur distincte donne une solution O(n · U)
(«U» = nombre de valeurs distinctes).
C'est parfait pour les petites données mais devient trop lent lorsque le tableau
contient 100 000 numéros distincts (soit 1010 opérations).

---

- Oui. 2. Une solution O(n log n) presque optimale

L'éditorial officiel montre que nous pouvons construire un arbre **segment**
magasins, pour chaque intervalle:

* « somme » – somme totale de l'intervalle
* `pref` – meilleure somme préfixe
* `suff' – meilleure somme suffixe
* `meilleur` – meilleure somme de sous-cours à l'intérieur de l'intervalle

Combiner deux nœuds d'enfant est la formule classique

«» "
somme = gauche.somme + droite.somme
pref = max(gauche.pref, gauche.sum + droite.pref)
suff = max(droite.suff, droite.sum + gauche.suff)
best = max(gauche.best, droite.best, gauche.suff + droite.pref)
«» "

Une fois que l'arbre est construit (O(n), nous pouvons *modifier temporairement* chaque occurrence de
`v` à `0` (c`est-à-dire supprimer) par des mises à jour ponctuelles.
Après toutes les mises à jour pour cette valeur, le champ `meilleur` de root contient déjà
la somme maximale des sous-tarifs du tableau avec tous les `v` supprimés.
Nous retournons ensuite les modifications – chaque élément est mis à jour **exactement une fois**
toute la course, donc le travail total est

«» "
Bâtiment : O(n)
mises à jour : O(n log n) (chaque élément mis à jour log n fois)
requête : O(1) par valeur
«» "

Complexité globale : **O(n log n)**, qui respecte facilement les limites.

---

- Oui. 3. Mise en œuvre de Python (arborescence du segment)

'`python
importations
de collections importer par défautdict

# --------- arbre de segment --------
Numéro de classe:
__slots__ = ('sum', 'pref', 'suff', 'meilleur')
def __init_(self, val=0):
Self.sum = self.pref = self.suff = self.best = val

def fusion(a: noeud, b: noeud) -> Numéro:
res = Noeud()
Res.sum = a.sum + b.sum
res.pref = max(a.pref, a.sum + b.pref)
res.suff = max(b.suff, b.sum + a.suff)
res.best = max(a.best, b.best, a.suff + b.pref)
retour res

Def build(arr):
n = len(arr)
taille = 1
pendant la taille < n: taille <<= 1
seg = [Node() pour _ dans la gamme(2 * taille)]
♪ feuilles
pour i, v in énumérate(arr):
seg[size + i] = noeud(v)
# noeuds internes
pour i dans la plage (taille - 1, 0, -1):
seg[i] = fusion(seg[2 * i], seg[2 * i + 1])
retour seg, taille

def point_update(seg, taille, pos, val):
i = taille + pos
seg[i] = noeud(val)
* = 1
alors que i:
seg[i] = fusion(seg[2 * i], seg[2 * i + 1])
* = 1
L'extrémité de l'arbre

def resouver() -> Aucun:
il = iter(sys.stdin.read().strip().split())
n = int(next(it))
a = [int(next(it)) pour _ dans la plage(n)]

# cas trivial – tous les nombres négatifs
Si tous(x < 0 pour x dans a):
imprimer(max(a))
retour

# positions de chaque valeur
pos = defaultdict(list)
pour i, v dans l'énumérationa:
[v].Append(i)

seg, taille = build(a)
réponse = max(a) # nous pouvons toujours prendre un seul élément

pour val, idx en pos.items():
# 1. supprimer temporairement cette valeur
pour i en idx:
point_update(seg, taille, i, 0)

réponse = max(réponse, seg[1].meilleur)

# 2. restaurer les valeurs originales
pour i en idx:
point_update(seg, taille, i, a[i])

print(réponse)

si __nom__ == "__main__" :
résoudre()
«» "

**Explication des éléments clés**

Autres Partie Pourquoi c'est nécessaire
-- -- -- -- -- -- -- -- -- --
`Node`=" Stocke les quatre paramètres; `_slots__` maintient l'utilisation de la mémoire faible. Autres
"merge" combine deux enfants; identique à la formule de l'éditorial. Autres
Construire l'arbre en temps linéaire. Autres
"point_update" Utilisé deux fois par élément – une fois pour le définir à `0`, une fois pour le restaurer. Autres
`pos`= Dictionary `value → liste des indices` – itération sur ce dictionnaire
garantit que chaque élément est mis à jour exactement une fois pour l'algorithme entier. Autres

---

- Oui. 4. Mise en œuvre C++ (arborescence du segment)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

Numéro de structure {
longue somme, préf, suffisance, meilleure;
Noeud(long long v = 0) : sum(v), pref(v), suff(v), best(v) {}
};

Node fusion (const Node &l, const Node &r) {
Numéro de référence:
res.sum = l.sum + r.sum;
res.pref = max(l.pref, l.sum + r.pref);
res.suff = max(r.suff, r.sum + l.suff);
res.best = max({l.best, r.best, l.suff + r.pref});
retour rés;
}

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);
l'élément n;
si (!(cin >> n)) retourner 0;
vecteur <long> a(n);
pour (auto &x : a) cin >> x;

si (*max_element(a.begin(), a.end()) < 0) {
cout << *max_element(a.begin(), a.end()) << '\n';
retour 0;
}

non ordonné_map<long long, vector<int>> Pos;
pour (int i = 0; i < n; ++i) pos[a[i]].push_back(i);

int sz = 1;
pendant que (sz < n) sz <<= 1;
vecteur <Node> seg(2 * sz, Node());

pour (int i = 0; i < n; ++i) seg[sz + i] = noeud(a[i]);
pour (int i = sz - 1; i > 0; --i) seg[i] = fusion(seg[2 * i], seg[2 * i + 1]);

automatique point_update = [&](int p, long val) {
p += sz;
seg[p] = noeud(val);
pour (p >>= 1; p; p >>= 1 )
seg[p] = fusion(seg[2 * p], seg[2 * p + 1]);
};

longue réponse longue = *max_element(a.begin(), a.end());
pour (auto &[val, idx] : pos) {
pour (int idx : idxs) point_update(idx, 0);
réponse = max(réponse, seg[1].meilleur);
pour (int idx : idxs) point_update(idx, a[idx]);
}

cout << réponse << '\n';
retour 0;
}
«» "

Le code C++ suit la même logique que la version Python – un bottom-up
arbre segmenté et dictionnaire de positions. Toutes les mises à jour sont effectuées dans
temps `O(log n)`, et chaque élément de tableau est mis à jour exactement deux fois sur le
exécution complète.

---

- Oui. 5. Mise en œuvre Java (arborescence du segment)

"Java
importation java.io.*;
Importation de java.util.*;

classe publique {
Nœud statique privé {
longue somme, pref, suffisance, meilleure;
Node(long v) { sum = pref = suff = best = v; }
}

statique privé Fusion de nœud(Node l, Node r) {
Node res = nouveau Node(0);
res.sum = l.sum + r.sum;
res.pref = Math.max(l.pref, l.sum + r.pref);
res.suff = Math.max(r.suff, r.sum + l.suff);
res.best = Math.max(Math.max(l.best, r.best), l.suff + r.pref);
retour rés;
}

public statique vide main(String[] args) lance Exception {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
StringTokenizer st = nouveau StringTokenizer(br.readLine());
long[]a = nouveau long[n];
pour (int i = 0; i < n; i++) a[i] = Long.parseLong(st.nextToken());

si (Arrays.stream(a).allMatch(x -> x < 0)) {
Système.out.println(Arrays.stream(a).max().getAsLong());
retour;
}

Carte <Long, liste<entier>> pos = nouveau HashMap<>();
pour (int i = 0; i < n; i++) {
pos.computeIfAbsent(a[i], k -> nouvelle liste de distribution<>()).add(i);
}

taille int = 1;
pendant la taille (taille < n) <<= 1;
Noeud[] seg = nouveau Noeud[2 * taille];
pour (int i = 0; i < 2 * taille; i++) seg[i] = nouveau Node(0);

pour (int i = 0; i < n; i++) seg[size + i] = nouveau nœud(a[i]);
pour (int i = taille - 1; i > 0; --i) seg[i] = fusion(seg[2 * i], seg[2 * i + 1]);

réponse longue = Arrays.stream(a).max().getAsLong();

pour (Map.Entry<Long, List<Integer>> e : pos.entrySet() {
Liste des indices <entier> = e.getValue();
pour (int idx : indices) pointMise à jour(seg, taille, idx, 0);
réponse = Math.max(réponse, seg[1].meilleur);
pour (int idx : indices) pointMise à jour(seg, taille, idx, a[idx]);
}

Système.out.printn(réponse);
}

point de vide statique privéUpdate(Node[] seg, taille int, int pos, long val) {
int p = taille + pos;
seg[p] = nouveau nœud(val);
pour (p >>= 1; p > 0; p >>= 1 )
seg[p] = fusion(seg[p << 1], seg[p << 1=1]);
}
}
«» "

Le code Java est essentiellement la même idée que le C++, mais utilise un
classe `Node` et un tableau de `Node`s pour l'arbre de segment.

---

- Oui. 6. Comment décider quelle mise en œuvre utiliser

Situation Algorithme Complexité Commentaires
- C'est quoi ?
Autres Très petits tableaux (.. 2000). Naïve Kadane pour chaque '....(...)
De grands tableaux (≥ 104) (O(n log n)) (Traduit par le journal) (Traduit par le journal) (Traduit par le journal)
Besoin d'une solution **Python**
Besoin d'une solution **C++** ou **Java**

---

- Oui. 7. Pièges communs

1. ** Utilisant des int. 32 bits en C++/Java** – les sommes peuvent atteindre 104 · 109, donc
utiliser "long long" / "long".
2. **Mettre à jour le mauvais noeud** – rappelez-vous que dans un arbre ascendant,
feuille est à l'index `size + pos`, pas `pos`.
3. **L'initialisation erronée pour l'arbre vide** – les feuilles pour les indices inutilisés devraient
être `-ш` si vous cherchez un maximum de subarray sur l'ensemble du tableau; ici nous
simplement garder à `0` parce qu'ils ne sont jamais atteints (indices au-delà
"n" ne sont jamais interrogés).
4. **Débordement entier** – en C++ et Java utilisent `long` / `long`.
5. **Lisez l'entrée rapidement** – en particulier dans C++/Java, utilisez des E/S tamponnés; dans
Python, lisez tout le fichier immédiatement.

---

- Oui. 7. Remarque finale

Le problème se réduit à : pour chaque valeur distincte, calculer le maximum de subarray
somme après avoir enlevé toutes ses occurrences. Le point de vue crucial est que nous
peut effectuer la suppression en réglant temporairement les positions correspondantes
à `0` dans un arbre de segment, demander la réponse, puis restaurer l'original
valeurs. Comme chaque indice appartient à une valeur exacte, chaque élément est
mise à jour seulement deux fois, garantissant la limite de temps `O(n log n)`. Le code
exemples ci-dessus mettent en œuvre cette stratégie dans trois langues populaires.