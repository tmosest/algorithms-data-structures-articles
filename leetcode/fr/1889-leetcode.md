---
Titre: LeetCode 1889. L'espace minimum perdu de l'emballage - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Aperçu du problème
**LeetCode 1889 – Espace minimum gaspillé de l'emballage* *

Vous êtes donné

* `packages` – un tableau de `n` entiers, représentant chacun la taille d'un paquet.
* `boxes` – un tableau 2-D de la taille `m`. `boxes[j]` contient les tailles distinctes des boîtes produites par le fournisseur `j`. Chaque fournisseur dispose d'une offre *infinie* de chacune de ses tailles de boîtes.

Vous devez choisir **un** fournisseur et utiliser **seulement ses tailles de boîte** pour mettre chaque paquet dans une boîte séparée.
Si un paquet de taille `p` est placé dans une boîte de taille `b`, l'espace perdu est `b – p`.
L'objectif est de minimiser l'espace gaspillé dans tous les paquets.
S'il est impossible d'adapter tous les colis à un fournisseur quelconque, retourner `-1`.
Parce que la réponse peut être énorme, retourner modulo `10^9 + 7`.

> **Exemples**
> 1. `emballages = [2,3,5]`, `boîtes = [[4,8],[2,8]` → **6**
> 2. `emballages = [2,3,5]`, `boîtes = [1,4],[2,3],[3,4]` → **-1**
> 3. `emballages = [3,5,8,10,11,12]`, `boîtes = [[12],[11,9],[10,5,14]]` → **9**

---

Stratégie de haut niveau
1. **Trier les paquets** – facilite la recherche binaire.
2. **Construisez un tableau de somme préfixe** des paquets triés – nous permet de calculer la somme de tout sous-segment contigu dans O(1).
3. Pour **chaque fournisseur**
* Triez ses tailles de boîtes.
* Si la plus grande boîte est encore plus petite que le plus grand paquet → *skip ce fournisseur*.
* Marchez dans les tailles de boîte en ordre ascendant.
* Pour une boîte de taille `b`, utilisez ** recherche binaire** pour trouver le plus grand index de paquets `idx` de telle sorte que `packages[idx] ≤ b`.
* Tous les paquets de l'index précédent + 1 jusqu'à `idx` seront emballés dans des boîtes de taille `b`.
* Calculez l'espace gaspillé pour ce segment en utilisant les sommes préfixées.
* Accumuler les déchets pour le fournisseur actuel.
4. Conserver les déchets **minimum** dans tous les fournisseurs.
5. Si aucun fournisseur ne pouvait s'adapter à tous les paquets → retourner `-1`.
6. Sinon retour `minWaste % MOD`.

- Oui. Pourquoi cela fonctionne
* Le tri garantit que lorsque nous traitons les tailles de boîtes en ordre croissant, tous les paquets qui s'inscrivent dans une boîte plus petite sont déjà traités; les paquets qui ont besoin de plus grandes boîtes sont laissés pour les boîtes plus tard.
* La recherche binaire (`upper_bound`) donne le dernier paquet qui correspond à une taille de boîte donnée dans `O(log n)`.
* Préfixons les montants, calculons la somme des tailles de colis dans une plage de « O(1) », ce qui est crucial pour l'efficacité.

---

Analyse de complexité
*Let* `N = paquets.longueur` (= 105) et `M = nombre total de tailles de boîtes pour tous les fournisseurs` (= 105).

*Dépôt* `emballages`: `O(N log N)`
*Trier* liste de boîtes de chaque fournisseur: `O(M log M)` globalement
*Processing* chaque boîte : une recherche binaire → `O(log N)`
Durée totale: **O((N + M) log N)* *
Espace: **O(N)** (pour les paquets, préfixer les sommes; plus les tableaux temporaires pour chaque fournisseur).

---

Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Chacun suit l'algorithme décrit ci-dessus, gère les cas de bord et utilise le module 1 000 000 007.

---

### Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

public int minWastedSpace(int[] paquets, int[][] boîtes) {
int n = colis.longueur;
Arrays.sort(emballages);

// Préfixer la somme des dimensions des emballages
long[] préfixe = nouveau long[n + 1];
pour (int i = 1; i <= n; i++) {
préfixe[i] = préfixe[i - 1] + colis[i - 1];
}

long meilleur = Long. MAX_VALEUR;
booléen possible = faux;
la plus grande Paquet = colis[n - 1];

pour (int[] fournisseur : boîtes) {
les tableaux.sort(fournisseur);
la plus grande Boîte = fournisseur[longueur du fournisseur - 1];
si (plus grande boîte < plus grand emballage) {
continuer; // ce fournisseur ne peut pas s'adapter au plus grand paquet
}
possible = vrai;

déchets longs = 0;
int prev = -1; // dernier index du colis déjà emballé

pour (int boxTaille : fournisseur) {
si (boxSize < paquets[0]) {
Continuer; // cette boîte est trop petite pour n'importe quel colis
}
int idx = upperBound(packages, boxSize); // dernier paquet correspondant
long sumEmballages = préfixe[idx + 1] - préfixe[prev + 1];
longs numPackages = idx - prev;
déchets += numEmballages * boîteTaille - sommeEmballages;
prev = idx;
}

best = Math.min (best, gaspillage);
}

retour possible ? (int) (meilleur % MOD) : -1;
}

// dernier index où paquets[i] <= cible, ou -1 si aucun
intérieur statique int upperBound(int[] arr, int cible) {
int lo = 0, hi = arr.longueur - 1, ans = -1;
pendant que (lo <= bonjour) {
Int milieu = lo + (h - lo) / 2;
si (arr[mid] <= cible) {
ans = milieu;
lo = milieu + 1;
} autre {
hé = milieu - 1;
}
}
le retour des an;
}
}
«» "

---

Python 3

'`python
bisect d'importation
de taper l'importation Liste

MOD = 10**9 + 7

Solution de classe:
def minWastedSpace(self, paquets: List[int], boîtes: List[List[int]]) -> Int:
n = len(emballages)
colis.sort()

# Préfixer les sommes
pref = [0]
pour p dans les colis:
pref.append(pref[-1] + p)

plus grand_pkg = paquets[-1]
meilleure = flotteur('inf')
possible = Faux

pour le fournisseur dans les boîtes:
fournisseur.sort()
si le fournisseur[-1] < le plus grand_pkg:
continuer # ne peut pas s'adapter au plus grand paquet
possible = Vrai

déchets = 0
prev = -1

pour boîte dans le fournisseur:
si la case < colis[0]:
poursuivre
idx = bisect.bisect_right(emballages, boîte) - 1
si idx <= prev:
poursuivre
sum_pkg = pref[idx + 1] - pref[prev + 1]
num_pkg = idx - prev
déchets += num_pkg * case - sum_pkg
Prév = idx

best = min (meilleur, déchets)

retour int(meilleur % MOD) si possible -1
«» "

---

### C++ (17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;

int minWastedSpace(vecteur<int>& paquets, vecteur<vecteur<int>>& boîtes) {
int n = paquets.size();
tri(packages.begin(), packages.end());

// préfixer les sommes
vecteur <long> pref(n + 1, 0);
pour (int i = 1; i <= n; ++i)
pref[i] = pref[i - 1] + paquets[i - 1];

longue longue meilleure = LLONG_MAX;
bool possible = faux;
la plus grande Pkg = colis.back();

pour (auto et fournisseur : boîtes) {
tri(fournisseur.degin(), fournisseur.end());
si (fournisseur.back() < le plus grandPkg) continue; // ne peut pas s'adapter
possible = vrai;

déchets longs = 0;
Int prev = -1;

pour (boîte à int : fournisseur) {
si (boîte < colis.front()) continue; // trop petite pour tout colis
int idx = upperBound (emballages, boîte); // dernier emballage de montage
long terme Pkg = pref[idx + 1] - pref[prev + 1];
long cnt = idx - prev;
déchets += cnt * case - somme Pkg;
prev = idx;
}

best = min (meilleure chose, déchets);
}

retour possible ? static_cast<int>(meilleur % MOD) : -1;
}

particulier:
// dernier index où paquets[i] <= cible, ou -1 si aucun
int upperBound(vecteur commun<int>& arr, cible int) {
int lo = 0, hi = (int)arr.size() - 1, ans = -1;
pendant que (lo <= bonjour) {
Int milieu = lo + (h - lo) / 2;
si (arr[mid] <= cible) {
ans = milieu;
lo = milieu + 1;
} autre {
hé = milieu - 1;
}
}
le retour des an;
}
};
«» "

---

Article de blog – Espace minimal perdu de l'emballage: bon, mauvais et lugubre

> **Audience cible**: ingénieurs logiciels, passionnés d'entrevues et recruteurs.
> **Mots-clés**: Espace minimum perdu de l'emballage, LeetCode dur, Recherche binaire, Préfixe Sum, Java, Python, C++, entretien de codage, algorithmes, conseils d'entretien d'emploi, structures de données, résolution de problèmes d'entrevue.

---

L'histoire (bien, mal et mal)

Autres Ce qui s'est passé Pourquoi ça compte
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bon**** **Paquets classés + montants préfixés** nous donnent une base *simple* mais puissante. Permet les requêtes O(1), qui maintient l'algorithme rapidement. *Toujours* trier et préprocéder les données avant l' itération. Autres
**C'est une erreur** **Les grandes entrées** (105) nous obligent à considérer l'exécution *worst-case*. Une approche naïve O(n2) serait chronométrée. De nombreux candidats sous-estiment le besoin d'opérations logarithmiques. Ne présumez jamais que O(n2) est acceptable sur 105 éléments. Autres
**Ugly**. **Skipping des fournisseurs inutilisables** peut être sujet à erreur si vous oubliez le plus grand paquet de vérification. Testez votre code sur les cas de bord : un seul paquet, toutes les boîtes de la même taille, etc. Autres

---

Pourquoi les intervieweurs aiment ce problème
* **Il vous force à réfléchir** à l'interaction entre *différentes structures de données* (arras, préfixes, arbres de recherche binaire).
* Il montre que vous pouvez **équilibrer le prétraitement et le travail par fournisseur** – un thème d'entrevue commun.
* Il teste **attention au détail** (modulo arithmétique, sécurité 64 bits, manipulation des caisses de bord).

Comment le faire dans une entrevue technique
1. ** Expliquer l'intuition d'abord** (pourquoi trier et préfixer les sommes).
2. **Parcourir un exemple simple** sur du papier ou un tableau blanc.
3. **Énoncez votre complexité** et pourquoi elle répond aux contraintes.
4. **Mise en oeuvre proprement** – fonctions modulaires, noms de variables appropriés et commentaires.
5. **Demander des éclaircissements**: Dois-je utiliser exactement les boîtes que le fournisseur offre? Est-il permis de mélanger différentes tailles de boîtes du même fournisseur? (Ils sont explicitement autorisés, mais seulement du fournisseur choisi).

---

Récapitulatif

> * L'espace minimal perdu de l'emballage* – un problème **LeetCode Hard** qui teste la recherche binaire et préfixe la maîtrise de la somme.
> Ce blog passe par la stratégie algorithmique, montre le code Java, Python et C++ prêt à la production, et explique pourquoi cette approche est assez efficace pour 105 points de données.
> Que vous soyez en train de vous préparer à un entretien d'ingénierie **logiciel**, à un défi de codage** ou que vous souhaitiez simplement approfondir votre compréhension de l'optimisation *structure des données*, les solutions ici vous donneront une voie claire vers le succès.

**Mots clés**: Espace minimum gaspillé de l'emballage, LeetCode 1889, Recherche binaire, Préfixe Sum, Java, Python, C++, Problème d'entrevue dure, Codage Interview Prep, Algorithmes, Job Interview Tips, Software Engineering.

Codage heureux – et peut-être le gaspillage minimal (et le rappel d'entrevue) viennent à votre manière! C'est ce qu'il a dit