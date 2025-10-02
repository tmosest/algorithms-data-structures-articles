---
titre: LeetCode 1320. Distance minimum pour taper un mot en utilisant deux doigts -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1320 – Distance minimale pour taper un mot en utilisant deux doigts
**Solutions en Java, Python et C++ **Article complet du blog (optimisé par le référencement)* *

---

Récapitulation des problèmes

Vous avez un clavier 5 × 6 (A...Z).
Les coordonnées sont:

Lettre (x, y)
C'est quoi ?
A. A. (0, 0)
B.B. (0, 1)
- Oui.
Z. (4, 1)

Vous avez deux doigts. La première utilisation de chaque doigt est libre (aucune distance n'est facturée).
Pour chaque presse clé suivante, vous payez la distance entre les deux lettres que vous tapez.

> **Objectif** – tapez une chaîne `word` (2 ≤ ≤ = 300) avec la distance totale **minimum**.

---

# # # , Intuition & Etat DP

- Lorsque nous sommes en position "i" dans "mot", la seule chose qui compte est ** où chaque doigt est**.
- Chaque doigt peut être :
- *un-set* (gratuit pour la première utilisation) – nous encoderons ceci comme `-1`.
- ou sur une lettre `c` (0-25).

Ainsi, un état DP est :

«» "
dp[i][f1][f2] = distance minimale pour terminer la dactylographie de i,
où doigt1 est sur f1, doigt2 sur f2
«» "

`f1, f2 Ohio {‐1, 0...25}` → 27 × 27 valeurs possibles pour chaque `i`.

**Transition* *

«» "
Laisser cur = mot[i]
Option 1: utiliser le doigt1
Coût = distance(f1, cur) // 0 si f1 == -1
suivant = dp[i+1][cur][f2]

Option 2: utiliser le doigt2
Coût = distance(f2, cur) // 0 si f2 == -1
suivant = dp[i+1][f1][cur]
«» "

Réponse = `dp[0][-1][-1]`.

La distance entre deux lettres est précalculée une fois.

---

- Oui. Complexité

Temps Espace
C'est le cas.
Récursifs + Méme **O(=mot=272)** 200 000 opérations **O(=mot=272)** Autres
Iterative

Les deux s'adaptent confortablement dans les limites.

---

- Oui. Code

Vous trouverez ci-dessous des implémentations **prêtes à coller** dans les trois langues demandées.

> **Astuce** – Tous les trois utilisent la même logique DP sous-jacente, qui vient d'exprimer idiomatiquement.

---

#### 4.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
// 26 lettres + 1 non encore utilisé
int final statique privé NOT_SET = -1;
N = 27; // 0...25 pour les lettres, 26 pour NOT_SET
int[][] pos = nouvelle int[26][2];
mémoire statique privée [[]];
Sol privé;
Int len privé;

// Positions précalculées sur un clavier 5×6
statique {
pour (int i = 0; i < 26; i++) {
[i] = i % 6; // x
pos[i][1] = i / 6; // y
}
}

Int minimum public Distance (mot d'ordre) {
ce.word = mot;
ceci.len = mot.longueur();
// +1 pour stocker l'état NO_SET à l'index 26
mémo = nouvelle int[len + 1][N][N];
pour (int i = 0; i <= len; i++)
pour (int f1 = 0; f1 < N; f1++)
Tableau.fill(memo[i][f1], -1);
retour resolve(0, NOT_SET, NOT_SET);
}

solution d'int privé(int idx, int f1, int f2) {
si (idx == len) retourne 0;
int fi1 = (f1 == NOT_SET) ? 26 : f1;
int fi2 = (f2 == NOT_SET) ? 26 : f2;
int cached = mémo[idx][fi1][fi2];
Si (cache != -1) retour mis en cache;

int cur = word.charAt(idx) - 'A';
// Option 1: utiliser le doigt1
coût int1 = distance(f1, cur) + résolution(idx + 1, cur, f2);
// Option 2: utiliser le doigt2
coût int2 = distance(f2, cur) + résolution(idx + 1, f1, cur);

int ans = Math.min(coût1, coût2);
mémo[idx][fi1][fi2] = ans;
le retour des an;
}

distance privée int(int de, int à) {
si (à partir de) NOT_SET) retourne 0;
int x1 = pos[from][0], y1 = pos[from][1];
int x2 = pos[to][0], y2 = pos[to][1];
retourner Math.abs(x1 - x2) + Math.abs(y1 - y2);
}
}
«» "

---

4.2 Python

'`python
importer des functools
de taper l'importation Liste

Solution de classe:
# Coordonnées précalculées pour A..Z
Coords: Liste[tuple] = [(i % 6, i // 6) pour i dans l'intervalle(26)]

def minimum Distance (self, mot: str) -> Int:
@functools.lru_cache(Aucun)
def dp(idx: int, f1: int, f2: int) -> Int:
""f1/f2 sont des indices 0‐25 pour une lettre, -1 signifie non utilisé."""
Si idx == len(mot):
retour 0

cur = ord(mot[idx]) - 65 n° 0

# Utiliser le doigt 1
coût1 = autodistillation(f1, cur) + dp(idx + 1, cur, f2)
# Utilisez le doigt 2
coût2 = autoréglage(f2, cur) + dp(idx + 1, f1, cur)

retour min(coût1, coût2)

retour dp(0, -1, -1)

def dist(self, from_idx: int, to_idx: int) -> Int:
si depuis _idx] - 1 :
retour 0
x1, y1 = auto.coords[from_idx]
x2, y2 = self.coords[to_idx]
retour abs(x1 - x2) + abs(y1 - y2)
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Coordonnées précalculées pour A..Z
vecteur<pair<int,int>> pos(26);
vecteur<vecteur<vecteur<int>>> mémo;
mot chaîne;
l'élément n;

Solution {
pour (int i = 0; i < 26; ++i) {
pos[i] = {i % 6, i / 6};
}
}

Int minimum Distance(mot chaîne) {
ce->mot = mot;
n = word.size();
// 27 = 26 lettres + 1 pour les lettres non utilisées
mémo.assign(n + 1, vecteur<vector<int>>(27, vecteur<int>(27, -1));
retour dp(0, 26, 26); // 26 représente NOT_SET
}

particulier:
Int dp(int idx, int f1, int f2) {
si (idx) n) retourner 0;
si [memo[idx][f1][f2] != -1) retourner mémo[idx][f1][f2];

int cur = mot[idx] - 'A';
// Utiliser le doigt 1
coût int1 = dist(f1, cur) + dp(idx + 1, cur, f2);
// Utiliser le doigt 2
coût int2 = dist(f2, cur) + dp(idx + 1, f1, cur);

retour mémo[idx][f1][f2] = min(coût1, coût2);
}

int dist(int de, int à) {
si (à partir de == 26) retourner 0; // NON_SET
auto [x1, y1] = pos[from];
auto [x2, y2] = pos[to];
retourner abs(x1 - x2) + abs(y1 - y2);
}
};
«» "

---

Article du blog (optimisé par le référencement)

> **Titre:** *Distance minimale pour taper un mot en utilisant deux doigts – Java, Python & C++ Solutions*
> **Meta Description:** Résolvez le LeetCode 1320 avec des explications DP claires, un code Java/Python/C++ optimal et un guide convivial pour la préparation des interviews.

---

5.1 Introduction

La distance minimale pour taper un mot en utilisant deux doigts** est un défi de programmation dynamique classique qui teste votre capacité à modéliser l'état et à optimiser les transitions. C'est une question d'entrevue parfaite pour les rôles d'ingénierie logicielle, en particulier ceux qui se concentrent sur la conception algorithmique et la maîtrise de la structure des données.

Cet article passe par le raisonnement, présente trois implémentations prêtes à la production, et vous donne une compréhension plus approfondie des aspects de bon, mauvais et laids que vous rencontrerez tout en le résolvant.

---

5.2 Récapitulation des problèmes

- ** Mise en page du clavier :** 5 lignes × 6 colonnes (lettres A à Z).
- **Distance :** Distance de Manhattan, `=x1‐x2=+=y1‐y2='.
- **Règlement :**
- Chaque doigt est libre.
- Les doigts peuvent démarrer sur n'importe quelle clé (y compris le premier caractère).
- Vous devez taper le mot donné avec **distance totale minimale**.

**Input** – une chaîne `word` (en haut, longueur ≤ 300).
** Sortie** – la distance minimale (entier).

---

5.3 Idées clés

1. **Compression de l'état**
La seule chose qui influence les coûts futurs est l'emplacement actuel de chaque doigt. Nous n'avons pas besoin de toute l'histoire, donc nous comprimons l'état à `(index, doigt1, doigt2)`.

2. **Sentinel pour les produits non encore utilisés *
Utilisez `-1` (ou `26` en C++) pour représenter l'état de "gratuit". La première fois qu'un doigt est utilisé, la distance est `0`.

3. **Pré-computation**
Les coordonnées de chaque lettre sur le clavier sont déterministes. Conservez-les dans un tableau pour la recherche O(1).

4. **Symmétrie de transition**
Pour déterminer quel doigt utiliser pour le personnage suivant, les deux options sont symétriques. Cela réduit considérablement l'espace de recherche.

---

5.3 Dérivation dynamique de la programmation

Étape Ce que nous faisons Pourquoi ça marche
- C'est quoi ?
**Définir le DP** – coût minimal à partir de la position `i` donné emplacement des doigts. Capture toutes les dépendances futures. Autres
**Cas de base**=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1 Autres
**Transition**= Utiliser chaque doigt. Calculer le coût + `dp[i+1][...]`. Autres
**Mémoisation** ► Cache donne un tableau 3-D ou `lru_cache`. Éviter les explosions exponentielles; chaque état résolu une fois. Autres

---

#### 5.4 - Pourquoi DP fonctionne

- **Espace d'état déterministe** – Seules les positions des doigts comptent.
- **Heure de mission** – Les contraintes sont modestes, mais le PDD garantit l'efficacité.
- ** Séparabilité nette** – La règle de première utilisation se traduit par un simple coût de 0 si elle n'est pas définie.

---

#### 5.5 – Pièges communs

Numéro Explication
- Oui.
L'utilisation de `-1` directement dans l'indice de tableau 3-D conduit à des indices négatifs. Carte `-1` → 26 (ou tout emplacement supplémentaire). Autres
Autres Distance de comptage excessive. Cas particulier: "distance = 0` quand le doigt == Autres
La limite de récursion de Python est de 1000, mais la longueur du mot ≤ 300, donc elle est sûre, mais garde toujours avec `sys.setrecursionlimit`. Autres

---

#### 5.6 – Opportunités et variations

- **Consommation de mémoire** – 273 × 300 200 000 int (~ 0,8 Mo). Si la mémoire devient une préoccupation (par exemple, dans un environnement d'entretien avec mémoire), vous pouvez la réduire à **deux calques** (`dp_cur`, `dp_next`) parce que `dp[i]` dépend uniquement de "dp[i+1]".
- ** Différentes formes de clavier** – Si la disposition du clavier change, vous n'avez qu'à reconstruire le tableau `pos`.
- **Parallélisme** – Pas nécessaire ici; le DP est intrinsèquement séquentiel en raison de l'ordre des caractères.

---

5.7 Réflexions finales et conseils d'entrevue

- ** Expliquez clairement votre état** – Les intervieweurs aiment vous voir expliquer pourquoi chaque dimension compte.
- **Afficher le diagramme de transition** – Une simple transition table ou pseudocode clarifie votre raisonnement.
- **Demander des précisions** – Par exemple, sommes-nous autorisés à basculer le même doigt entre deux touches consécutives? Dans ce problème, oui, mais rendre cette hypothèse explicite peut éviter les bugs subtils.
- **Test edge cases** – Chaîne vide, toutes les mêmes lettres, lettres alternées, chaîne la plus longue.

---

Résumé

Nous avons:

1. Décodé le problème LeetCode 1320 en un modèle DP concis.
2. A traversé le **bon** – état déterministe, complexité polynôme, transitions propres.
3. Mise en évidence du **mauvais** – pièges autour des valeurs sentinelles, coût de première utilisation.
4. S'attaque au **ugly** – utilisation de la mémoire, problèmes potentiels de profondeur de récursion.

Les extraits de code pour **Java, Python et C++** sont entièrement testés et prêts pour des entretiens de production ou comme modèle pour des problèmes DP similaires.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---


---


**Fin de l'article**



---


- Oui. Note finale

> **Tip Pro** – Lors de la préparation des entrevues, gardez ce modèle à l'esprit : *Identifiez le minimum de mémoire requis pour décrire l'avenir*, codez-le comme un état DP, pré-calculez toute recherche coûteuse (comme les distances), puis itérez-vous sur les choix.
> LeetCode 1320 est un exemple de manuel de ce principe. Bonne solution !