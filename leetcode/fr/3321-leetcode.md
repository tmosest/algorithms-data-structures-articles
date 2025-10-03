---
titre: LeetCode 3321. Trouver X-Sum of All K-Long Subarrays II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Code de Leet 3321 – Trouver X-Sum of All K‐Long Subarrays II
*Solution en **Java**, **Python** et **C++** + un billet de blog qui explique le bon, le mauvais et le laid. *

---

Récapitulation du problème

> Avec un tableau «nums» (longueur *n*) et deux entiers «k» et «x».
> Pour chaque subarray contigu de longueur `k`
> 1. Compter la fréquence de chaque élément.
> 2. Conservez les éléments les plus fréquents du "x" *
> *Si deux éléments se connectent en fréquence, la plus grande valeur gagne. *
> 3. Résumez les éléments conservés (ou l ' ensemble du sous-réseau s ' il a moins de valeurs " x " distinctes).
> Retournez un tableau de ces X‐Sums pour toutes les fenêtres coulissantes.

---

- Oui. 1. L'idée de base – deux multisets + fenêtre coulissante

C'est bon C'est mauvais
- C'est quoi ?
*Requiert un comparateur personnalisé* – difficile dans certaines langues. *La suppression lente pour les tas* – peut masquer les bugs.
*L'utilisation de l'espace* – deux multisets + carte de hachage (dans le pire des cas)
*Déterministe tie-breaking* – plus grande valeur gagne lorsque les fréquences tie=* *Harder à raison* – surtout quand `k == x` (la fenêtre entière est toujours résumée)

- Oui. Comment ça marche

Étape
- C'est quoi ?
**1. Conserver les fréquences** – `freq[value]` dans une carte de hachage. Autres
**2. Deux ensembles multiples** –
"large" – contient au plus des éléments "x", le courant "top x".
`petit` – tous les éléments restants. Autres
**3. Ordre** – multiset est trié **ascendant** par `(fréquence, valeur)`.
*Le premier* (« le plus petit ») dans le « grand » est le candidat le plus faible à démoter.
*Le dernier* ("le plus grand") dans "petit" est le candidat le plus puissant à promouvoir. Autres
**4. Maintenir la somme de tous les éléments de la «grande». Autres
**5. Sur chaque changement de fenêtre** – ajouter un nouvel élément, supprimer l'ancien élément, puis rééquilibrer `large` & `small` pour satisfaire l'invariant `=large===x` (ou toutes les valeurs distinctes si moins nombreuses). Autres

Puisque chaque élément est inséré et supprimé exactement une fois par diapositive de fenêtre, l'algorithme entier est `O(n log n)` (le `log n` vient des opérations multiset).

---

- Oui. 2. Mise en œuvre des références

Vous trouverez ci-dessous un code propre et prêt à la production pour **Java**, **Python** et **C++** que vous pouvez coller dans votre éditeur ou utiliser comme référence pour vos propres solutions.

> **Astuce:** Toutes les solutions utilisent l'arithmétique 64 bits (`long` / `long`) parce que la somme peut dépasser `int32`.

---

2.1 Java (TreeSet + HashMap)

"Java
Importation de java.util.*;

***
* LeetCode 3321 – Trouver X-Sum de tous les K‐Long Subarrays II
*/
solution de classe publique {
classe statique privée Paire Comparable <Pair> {
valeur finale int; // valeur de l'élément
int freq; // fréquence de courant

Pair(int value, int freq) {
Ça. valeur = valeur;
ce.freq = freq;
}

@Override
comparaison publique Pour (Paire o) {
si (this.freq != o.freq) retourne Integer.compare(this.freq, o.freq);
retourner Integer.compare(cette valeur, o.value);
}

@Override
booléen public est égal(Object o) {
o exemple de Pair p &&
p.value == this.value && p.freq == this.freq;
}

@Override
code hash() public
retourner Objects.hash(valeur, freq);
}
}

finale privée Carte<integer, integer> freq = nouveau HashMap<>();
final privé TreeSet<Pair> grand = nouveau TreeSet<>();
final privé TreeSet<Pair> petit = nouveau TreeSet<>();
somme privée longueLarge = 0; // somme des éléments en 'large '

// aide à mettre à jour la fréquence d'une valeur
changement de vide privéFreq(int val, int delta) {
int oldF = freq.getOrDefault(val, 0);
int newF = ancien F + delta;
si (nouveauF < 0) lance une nouvelle exception d'État illégal();

Paire oldPair = nouvelle paire (val, oldF);
Paire neuve = nouvelle paire (val, nouvelle F);

// supprimer l'ancienne paire de l'ensemble auquel elle appartient
si (grand.contient(vieuxPair)) {
grand.supprimer(vieillePair);
sumGrand -= (long) vieuxF * val;
si (nouveauF > 0) {
grand.add(nouveauPair);
sumLarge += (long) newF * val;
} autre {
// freq devient 0 -> chute complètement
freq.remove(val);
retour;
}
} sinon si (petit.contient(vieuxPair)) {
petit.supprimer(vieillePair);
si (nouveauF > 0) petit.add(nouveauPair);
sinon freq.remove(val);
} autre { // élément n'était pas présent avant
si (nouveauF > 0) {
petit.add(nouveauPair);
} autre {
retour; // rien à faire
}
}

si (newF > 0) freq.put(val, newF);
}

// rééquilibrer grand/petit pour maintenir la taille x
rééquilibre du vide privé(int x) {
// passer de petit à grand si nécessaire
alors que (large.size() < x & & ! small.isEmpty()) {
Pair toMove = small.last(); // plus fort chez les petits
small.supprimer;
grand.add (à déplacer);
sumLarge += (long) toMove.freq * toMove.value;
}

// Démoter le plus faible
alors que (!small.isEmpty() && large.size() > x) {
Pair toMove = grand.first(); // le plus faible en grand
grand.supprimer(déplacer);
sumGrand -= (long) toMove.freq * toMove.value;
petit.add (à déplacer);
}

// swap si un élément plus fort est assis en petit
si (!large.isEmpty() &&!small.isEmpty() {
Paire le plus faibleLarge = large.first(); // le plus faible dans le top‐x
Paire la plus forte Petit = petit.dernier(); // le plus fort parmi les autres

i (plus fortSmall.freq > faibleLarge.freq
(le plus fortSmall.freq) == le plus faibleLarge.freq &&
plus fortPetit.valeur > plus faibleGrand.valeur)) {

// Démoter le plus faible Grandes
grand.supprimer(faibleLarge);
sumGrand -= (long) faibleLarge.freq * faibleLarge.valeur;
petit.add(faibleLarge);

// promouvoir le plus fort Petite
petit.supprimer(le plus fortPetit);
grand.add(plus fortPetit);
sumGrand += (long) plus fortSmall.freq * plus fortSmall.value;
}
}
}

Int[] getXSum(int[] nombres, int k, int x) {
int n = longueur nums;
int[] ans = nouvelle int[n - k + 1];

pour (int i = 0; i < k; i++) changementFrek(nums[i], 1);
rééquilibre(x);
ans[0] = (int) sumLarge;

pour (int i = 1; i <= n - k; i++) {
changement Freq(nums[i - 1], -1); // supprimer le plus à gauche
changeFrek(nums[i + k - 1], 1); // ajouter le plus à droite
rééquilibre(x);
as[i] = (int) sumGrand;
}

le retour des an;
}
}
«» "

**Pourquoi il s'agit de l'implémentation Java d'Igali* *

- `TreeSet` garantit *log‐n* insertion / suppression dans **O(1)** temps par opération.
- `Pair` tient la fréquence *current*, afin que nous puissions recalculer la somme à la volée.
- L'invariant `=large===x` est restauré avec une petite boucle, en gardant la logique lisible.

---

2.2 Python (deux tas + suppression paresseuse)

'`python
importation heapq
de collections importer par défautdict
de taper l'importation Liste

♪ -------------------------------------------------------
Code Leet 3321 – Python (pap + suppression paresseuse)
♪ -------------------------------------------------------
Solution de classe:
def xSum(self, nombres: List[int], k: int, x: int) -> Liste[int]:
n = len(nums)
ans = []

freq = defaultdict(int) # element -> fréquence

# Min-heap pour 'large' (haut-x)
grand = [] # (freq, valeur)
# Max-heap pour 'petit' (tout le reste)
petite = [] # (-freq, -valeur)
sum_large = 0
taille_large = 0

def clean:
""""Inscriptions creuses dont la fréquence ne correspond plus."""
pendant que le tas:
f, v = masse[0]
real_f = freq.get(v, 0)
si real_f == 0 ou real_f != f:
n° de rejet
Sinon:
pause

def rebalance():
non local sum_large, size_large
# passer de petit à grand si nous avons de l'espace
alors que size_large < x et petite:
f, v = heapq.nlargeur(1, petite)[0]
heapq.heappop(petit)
heapq.heappush(large, (f, v))
sum_large += f * v
taille_large += 1

# Démotez le plus faible si nous en avons trop
tandis que size_large > x et grand:
f, v = heapq.nsmallest(1, grande)[0]
heapq.heappop(large)
sum_large -= f * v
heapq.heappush (petit, (-f, -v))
taille_large -= 1

# promouvoir plus petit si elle bat plus faible
tandis que petits et grands:
# le plus fort chez les petits : le plus grand (-f, -v)
sf, sv = -petit[-1][0], -petit[-1][1]
lf, lv = grande[0] # le plus faible
si sf > lf ou (sf == lf et sv > lv):
# Démoter le plus faible
heapq.heappop(large)
sum_large -= lf * lv
heapq.heappush (petit, (-lf, -lv))
# promouvoir la plus forte petite
heapq.heappop(petit)
heapq.heappush(large, (sf, sv))
sum_large += sf * sv
Sinon:
pause

C'est... Fenêtre coulissante principale...
pour i dans la plage(k):
v = nombres[i]
freq[v] += 1
heapq.heappush(large si len(large) < x autre petite,
(freq[v], v))

# Après la première fenêtre, construire des tas correctement
pour v, f dans freq.items():
Si f > 0:
heapq.heappush(large si len(large) < x autre petite,
f, v))
rééquilibre()
as.append(int(sum_large))

pour i dans la plage (k, n):
# fenêtre de déplacement
old = nombres[i - k]
nouveau = nombres[i]
freq[old] -= 1
freq[nouveau] += 1

# Poussez de nouvelles entrées (la suppression paresseuse gérera les entrées statiques)
si freq[old]] 0:
del freq[old]
heapq.heappush(large si len(large) < x autre petite,
(freq.get(vieux, 0), vieux)
heapq.heappush(large si len(large) < x autre petite,
[nouveau])

rééquilibre()
as.append(int(sum_large))

retour et
«» "

> **Attention :** La version Python ci-dessus est **conceptuelle** – la suppression paresseuse (`heapq` + carte de fréquence) fonctionne mais peut être un peu lente pour grand `n`. Dans la pratique, vous pouvez remplacer les deux tas par `bisect.insort` dans une liste triée (bibliothèque `conteneurs triés`) pour une implémentation plus propre.

---

### 2.3 C++ (multiset + non ordonné_map)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

/*
* LeetCode 3321 – Trouver X-Sum de tous les K‐Long Subarrays II
*/
solution de classe {
public:
struct Pair {
valeur int val; // élément
int freq; // fréquence de courant

Paire(int v, int f) : val(v), freq(f) {}
// ascendant par (freq, val)
opérateur de bool<(pair de const& o) const {
si (freq != o.freq) retourner freq < o.freq;
valeur de retour < o.val;
}
};

vecteur<int> xSum(vecteur<int>& nums, int k, int x) {
unordered_map<int, int> freq;
multiset<Pair> grand, petit;
longue sommeLarge = 0;
int n = nombres.size();
vecteur <int> ans(n - k + 1);

mise à jour automatique = [&](int val, int delta) {
int oldF = freq.count(val) ? freq[val] : 0;
int newF = ancien F + delta;
si (newF < 0) lancer logique_error("fréquence négative");

Paire oldPair(val, oldF), newPair(val, newF);

si (large.count(oldPair)) {
grande.erase(large.find(oldPair));
sumGrand -= 1LL * oldF * val;
si (nouveauF > 0) {
grand.insert(newPair);
Montant Grand += 1LL * nouveauF * val;
}
} sinon si (petit.compte(vieillePaire)) {
petite.erase(petit.find(vieillePair);
si (newF > 0) petit.insert(newPair);
} autre { // première apparition
si (newF > 0) petit.insert(newPair);
}

si (newF > 0) freq[val] = newF;
autres freq.erase(val);
};

rééquilibre automatique = [&](int x) {
// remplir grand si possible
alors que (large.size() < (size_t)x && ! small.vide() {
auto it = prev(small.end()); // plus fort dans les petits
sumGrande += 1LL * it->freq * it->val;
grand.insérer(*it);
petite (il);
}
// démote le plus faible si nous en avons trop
pendant que (!small.vide() && large.size() > (size_t)x) {
auto it = small.end(); // plus petit (pas nécessaire ici)
// En fait, nous ne démobilisons que lorsque grand > x
auto itLow = large.begin(); // le plus faible
sumGrand -= 1LL * itLow->freq * itLow->val;
petit.insert(*itLow);
large.erase(itLow);
}
// promouvoir si un petit plus fort bat un grand plus faible
pendant que (!small.vide() && !large.vide() {
faible automatiqueLarge = large.degin();
auto forte Petite = prev(small.end());
si (fortSmall->freq > faible
(fortSmall->freq) faible
fortePetit->val > faibleGrand->val) {
sumGrand -= 1LL * faibleGrand->freq * faibleGrand->val;
large.erase(faible);
Montant Grand += 1LL * fortPetit->freq * fort Petite vallée;
grand.insert(*fortSmall);
small.erase (smithSmall);
} autre pause;
}
};

// fenêtre initiale
pour (int i = 0; i < k; ++i) mise à jour(nums[i], 1);
rééquilibre(x);
ans[0] = static_cast<int>(sumLarge);

pour (int i = 1; i <= n - k; ++i) {
update(nums[i - 1], -1); // supprimer le plus à gauche
update(nums[i + k - 1], 1); // ajouter le plus à droite
rééquilibre(x);
ANS[i] = statique_cast<int>(sumLarge);
}
le retour des an;
}
};
«» "

> La version C++ reflète la logique Java, mais bénéficie des itérateurs `multiset`.S *bidirectionnel*, ce qui rend la logique swap/promouvoir succincte.

---

- Oui. 3. Principales options pour une production Solution prête

Langue de travail Structure des données Complexité Force
- C'est quoi ?
**Java**="TreeSet<Pair>="O(n log k)=" Maintenance invariante simple, commande intégrée. Autres
**Python**= `heapq` + `defaultdict` (effacement paresseux)= O(n log k)= Fonctionne mais peut être lent; utilisez la liste triée si la vitesse compte. Autres
**C++**="multiset<Pair>="O(n log k)="Contrôle total des itérateurs. Autres

**Qu'est-ce qui fait la solution de "good"* *
- **Opérations prédictibles de log-n** par arbre ou tas équilibrés.
- **Entretien de somme explicite** – évitez de recalculer à partir de zéro pour chaque fenêtre.
- **Restaurant invariant clair** – garder `==large===== x` avec des boucles minimales.
- **Éviter les objets temporaires excessifs** – mettre à jour les structures de données en place.

---

### TL;DR

- **Utilisez un arbre équilibré (`TreeSet` / `multiset`)** en Java, C++ ou C++ pour suivre les éléments `k` et maintenir le sous-ensemble top-x.
- **Mettre à jour les fréquences sur chaque diapositive**, en ajustant la somme à la volée.
- **Rebalance** lorsque le nombre d'éléments dans le réglage top‐x change ou lorsqu'un élément plus fort apparaît dans le reste.

Cela donne une solution élégante, rapide et durable pour le problème **=X-sum d'une fenêtre coulissante.