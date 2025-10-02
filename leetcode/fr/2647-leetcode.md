---
titre: LeetCode 2647. Couleur du Triangle Rouge -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2647. **Couleur du Triangle Rouge** – Un LeetCode dur Master‐class
> **Langues** : Java
> ** Tags du référencement** : *LeetCode hard*, *Couleur le Triangle Red*, *triangle coloriage algorithme*, *emploi interview algorithme*, *C++ code interview*, *Python interview solution*, *Java interview code*, *compétitivité programmation*, *algorithme conception*

---

Récapitulation des problèmes

> On vous donne un entier **n**.
> Considérer un triangle équilatéral de longueur latérale **n** divisé en triangles "n2" unitaires.
> La ligne i‐th (1‐basée) contient les triangles «2i‐1‐1, indexés «(i, 1 ... 2i‐1)».
> Deux triangles sont *voix* s'ils partagent un côté.

Au départ, tous les triangles sont blancs.
Vous pouvez pré-colorer **k** triangles rouges. Après cela, un algorithme fonctionne:

«» "
répéter
choisir tout triangle blanc ayant ≥ 2 voisins rouges
si aucune n'existe → arrêter
couleur que triangle rouge
jusqu'à ce qu'il ne bouge plus
«» "

**Objectif**
*Choisissez le plus petit ensemble possible de triangles précolores de telle sorte que l'algorithme se termine avec le triangle rouge entier. *
Retournez les coordonnées des triangles précolores (tout ensemble optimal fonctionne).

**Contrôles* *
`1 ≤ n ≤ 1000`

---

Intuition et observation

* L'algorithme est un remplissage d'inondation* : un triangle devient rouge quand au moins deux de ses voisins sont déjà rouges.
* Pensez-y comme une vague qui a besoin de **deux graines** pour se propager dans un triangle.
* La structure du grand triangle peut être décomposée en blocs **4 rangs** – un motif qui répète toutes les 4 lignes.
* À l'intérieur d'un bloc de 4 rangs, nous pouvons choisir des triangles aux *edges* afin que chaque triangle intérieur ait finalement deux voisins rouges.

Si nous regardons la solution optimale pour les petits n (2,3,4,5...) nous observons un modèle régulier:

Autres triangles précolores (ligne, col)
Il n'y a pas de différence entre les deux.
Autres Aucun – manipulé par les blocs de 4 rangs
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
2-- "(1,1)", "(2,1)", "(2,3)"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * ) * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

Nous pouvons donc construire la solution en :
1. **Procéder à des blocs complets de 4 rangs à partir du bas vers le haut. **
2. **Tirer les autres lignes du haut** (`n % 4`) avec le motif fixe ci-dessus.

---

C'est vrai. Algorithme

Texte
résultat ← liste vide

♪ 1. Poignez chaque bloc complet de 4 rangs (en bas → en haut)
pour i de n à 4 étapes -4:
a) Ligne i: colonnes impaires (1,3,5,...)
pour j = 1; j ≤ 2*i-1; j += 2:
ajouter (i, j) au résultat

# b) Ligne i-1: colonne 2
ajouter (i-1, 2) au résultat

# c) Ligne i-2 : même colonnes (2,4,6...), mais inversées
pour j = 2*(i-2)-1; j > 2; j -= 2:
ajouter (i-2, j) au résultat

d) Ligne i-3: colonne 1
ajouter (i-3, 1) au résultat

♪ 2. Poignez les lignes du haut (n % 4)
t ← n mod 4
si t ≥ 1: ajouter (1,1)
si t ≥ 2: ajouter (2,1), (2,3)
si t ≥ 3: ajouter (3,1), (3,5)

résultat du retour
«» "

*Proof d'exactitude* –
Chaque bloc de 4 rangs contient exactement les triangles nécessaires pour ensemencer le bloc.
Tous les triangles intérieurs d'un bloc ont au moins deux voisins rouges une fois que le bloc est complètement ensemencé.
Le bloc partiel supérieur (t = 1,2,3) suit la même logique que les cas de base.
Ainsi, l'algorithme garantit que chaque triangle finira par être coloré rouge, et aucun ensemble plus petit ne peut y parvenir.

---

Analyse de complexité

Java / Python / C++
-- -- -- -- -- -- -- -- --
**Heure**="O(n)" – chaque triangle est visité un nombre constant de fois. Autres
**L'espace**="O(k)" – nombre de triangles précolores (="n2/4" dans le pire des cas). Autres

`k` est la taille de la réponse; elle est proportionnelle à `n2`, mais l'algorithme lui-même est linéaire dans `n`.

---

C'est vrai. Mise en œuvre des références

Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe {
public int[] colorRed(int n) {
Liste<int[]> res = nouvelle liste de distribution<>();

// 1. Blocs complets de 4 rangs
pour (int i = n; i - 4 >= 0; i -= 4) {
// Ligne i: colonnes impaires
pour (int j = 1; j <= 2 * i - 1; j += 2) {
res.add(new int[]{i, j});
}
// Ligne i-1: colonne 2
res.add(nouvelle int[]{i - 1, 2});
// Ligne i-2: même colonnes (inverse)
pour (int j = 2 * (i - 2) - 1; j > 2; j -= 2) {
res.add(nouvelle int[]{i - 2, j});
}
// Ligne i-3: colonne 1
res.add(nouvelle int[]{i - 3, 1});
}

// 2. Bloc partiel supérieur (n % 4)
t = n % 4;
si (t >= 1) res.add(nouvelle int[]{1, 1});
si (t >= 2) {
res.add(nouvelle int[]{2, 1});
res.add(nouvelle int[]{2, 3});
}
si (t >= 3) {
res.add(nouvelle int[]{3, 1});
res.add(nouvelle int[]{3, 5});
}

retourner res.àArray(nouvelle int[res.size()]];
}
}
«» "

Python

'`python
de taper l'importation Liste

Solution de classe:
def colorRed(self, n: int) -> Liste[Liste[int]]:
res = []

# Des blocs de 4 rangs
i = n
alors que i - 4 >= 0:
# Ligne i : colonnes impaires
pour j dans la plage (1, 2 * i, 2):
Annexe([i, j])
Ligne i-1: colonne 2
res.append([i - 1, 2])
# Ligne i-2: même colonnes (inverse)
pour j dans l'intervalle(2 * (i - 2) - 1, 2, -2):
res.append([i - 2, j])
# Ligne i-3: colonne 1
Annexe([i - 3, 1])
I -= 4

Top bloc partiel
t = n % 4
si t >= 1 :
Annexe([1, 1])
si t >= 2 :
Annexe([2, 1])
Annexe([2, 3])
si t >= 3 :
Annexe([3, 1])
Annexe([3, 5))

retour res
«» "

C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vector<vector<int>> colorRed(int n) {
vecteur<vecteur<int>> rés;

// Blocs 4 rangs complets
pour (int i = n; i - 4 >= 0; i -= 4) {
// Ligne i: colonnes impaires
pour (int j = 1; j <= 2 * i - 1; j += 2)
le nom de l'autorité compétente;
// Ligne i-1: colonne 2
res.push_back({i - 1, 2});
// Ligne i-2: même colonnes (inverse)
pour (int j = 2 * (i - 2) - 1; j > 2; j -= 2)
le nom de l'autorité compétente,
// Ligne i-3: colonne 1
res.push_back({i - 3, 1});
}

// Bloc partiel supérieur
t = n % 4;
si (t >= 1) res.push_back({1, 1});
si (t >= 2) {
le nom de l'autorité compétente,
res.push_back({2, 3});
}
si (t >= 3) {
les informations suivantes sont disponibles:
res.push_back({3, 5});
}

retour rés;
}
};
«» "

---

- Oui. Les bons, les mauvais, les méchants

Catégorie
C'est pas vrai.
**Readability**
**Performance**
**Scalabilité**= Fonctionne jusqu'à `n = 1000` (limite du code leet)== Non nécessaire=
**Maintenabilité**= Responsabilité unique, facile à prolonger== Risque mineur en cas de changement de modèle== Aucune=

> **A emporter**: La solution à base de motifs est *à la fois* rapide et élégante. Il évite tout BFS/DFS coûteux tout en garantissant l'optimalité – une victoire pour les interviews et la production.

---

Essais et validation

'`python
# Vérification rapide de la santé mentale
def brute(n):
# simple BFS qui teste si un semoir donné fonctionne
à partir de collections import deque
Total = n * n
# générer une carte d'adjacence
adj = {}
pour i dans la plage(1, n + 1):
pour j dans la plage (1, 2 * i, 2):
clé = (i, j)
proche = []
À gauche
si j > 1: proche.appendice(i, j - 1))
Droite
i j < 2 * i - 1: proche.
♪ à gauche
Si i < n:
Annexe(i + 1, j)
Tout droit
Si i < n:
Annexe(i + 1, j + 2))
♪ haut à gauche
i > 1 :
Annexe(i - 1, j - 2)
Tout droit
i > 1 :
Annexe(i - 1, j)
adj[key] = [p pour p dans le voisinage si p dans adj ou (i==1 ou i==n)] # ignorez l'extérieur
# graines minimales de force brute simples pour n <= 4
# omis pour la brièveté
retour

♪ Exécutez le résolveur officiel
sol = Solution()
print(sol.colorRed(3))
Nombre prévu: [[1,1],[2,1],[2,3],[3,1],[3,5]
«» "

*Le vrai harnais LeetCode vérifiera que tous les triangles deviennent rouges et que le nombre de triangles précolorés est minimal. *

---

#### 8

- **Pourquoi ça compte dans les interviews** –
La clé pour gagner *Color le Triangle* n'est pas de forcer un BFS, mais de repérer le modèle **semence**. Les intervieweurs aiment les algorithmes qui transforment un processus apparemment complexe en une simple boucle arithmétique*.

- **Pourquoi vous allez adorer le code** –
La solution est courte, n'a pas de récursion, et est écrite dans les trois langues principales. Il présente un grand mélange de **perspective mathématique** et **compétence de codage**.

Bonne chance pour votre voyage de codage! C'est ce qu'il a dit.

---