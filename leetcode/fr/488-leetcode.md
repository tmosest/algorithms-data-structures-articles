---
titre: LeetCode 488. Zuma Jeu -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Jeu Zuma – 488 sur LeetCode
> **Hard** – Tableau de 5 couleurs, main de 5 boules, trouver les insertions minimales pour effacer le tableau

---

TL;DR
Langue Heure Espace idée clé Autres
- C'est quoi ?
**Java**= O(= *état* × *branche*== O(= *état*=== DFS + mémo + compression de planche===
**Python**= O(= *état* × *branche*== O(= *état*== Récursion + lru_cache + planche à tuple===
**C++**= O(= *état* × *branche*== O(= *état*=== DFS + non classé_map + chaîne de caractères===

> **Résultat** – Insertion minimale (ou `-1` si impossible).

---

Rétablissement des problèmes

Nous avons une planche 1-D de boules colorées (`R Y B G W`) et une main de boules.
Un tour consiste en

1. **Insérer** n'importe quelle boule entre deux boules existantes (ou à une fin).
2. **Collision**: tout groupe contigu de 3+ boules de même couleur disparaît; de nouveaux groupes peuvent se former et s'effondrer récursivement.
3. **Répéter** jusqu'à ce que le tableau soit vide (gagnant) ou que la main soit épuisée (perdue).

Retourner le nombre minimal d'insertions nécessaires pour nettoyer le panneau, ou `-1` si impossible.

**Contrôles* *

- `1 ≤ longueur de la planche ≤ 16`
- "1 ≤ longueur de la main ≤ 5'
- Oui. Aucun groupe initial de 3+ n'existe sur le tableau.

---

- Oui. Pourquoi c'est dur

Facteur Pourquoi ça compte
-- -- -- -- -- --
**Espace de recherche exponentielle**= Chaque insertion peut se produire à *any* gap → facteur de branchement jusqu'à 17, profondeur ≤ 5 → 175 . Autres
**Explosion de l'État**Les configurations des conseils d'administration peuvent être énormes; la DFS naïve revisite les mêmes états. Autres
**Règles de taille**= Il faut identifier quand un mouvement est inutile (par exemple, insérer une couleur qui n'aide jamais). Autres
**Mémoization Overlap**= Deux séquences différentes peuvent produire le même état `(board, hand)`. Autres
**Language Variants**= Java: besoin de hachage personnalisé; Python: limites de récursion; C++: vitesse vs mémoire. Autres

---

- Oui. Idée de base – DFS + Mémo + Compression de la carte

1. ** Représentation de l ' État* *
- **Board** – compressé comme une chaîne.
- **Poignée** – un tableau de la taille 5 (« R Y B G W ») qui suit les autres comptes.
- Encoder l'état comme `board#handString` (par exemple `"WWRBB#21200"`).
2. **DSE récursif**
- Pour chaque *gap* sur la planche, essayez d'insérer une boule de la même couleur que l'une des boules voisines (sinon aucun effondrement possible).
- Après insertion, **collapse** la planche: supprimer à plusieurs reprises toutes les stries 3+ de même couleur.
- Récursez le nouveau tableau et mettez à jour la main.
- Gardez une trace des étapes minimales.
3. **Mémoisation**
- Utilisez une carte de hachage (`Map<String,Integer> memo`) pour mettre en cache la meilleure réponse pour un état donné.
- Si un état a déjà été résolu, retournez la valeur mise en cache.
4. **Ébauche**
- Si aucune balle à main ne correspond à une couleur de tableau, sautez.
- Si une couleur a besoin `k` boules pour s'effondrer mais la main a moins, sauter.
- Sortie anticipée si la planche devient vide.

La clé est que la carte est *courte* (=16) et la main est minuscule (=5), donc nous pouvons nous permettre un DFS compact.

---

Mise en œuvre du code

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// 0:R 1:Y 2:B 3:G 4:W
omble final statique privé[] COULEURS = {'R', 'Y', 'B', 'G', 'W'};
carte privée<String, entier> mémo = nouveau HashMap<>();

public int findMinStep(Plaque à cordes, main à cordes) {
int[] handCnt = nouveau int[5];
pour (charc : main.àCharArray())
handCnt[charIdx(c)]++;

retour dfs(board, handCnt);
}

Int privé dfs(Plage, int[] handCnt) {
si (board.isEmpty()) retourne 0;
Clé de chaîne = carte + "#" + handCntToStr(handCnt);
si (memo.contientKey(key)) retourne memo.get(key);

int ans = entier. MAX_VALEUR;
// Pour chaque position d'écart
pour (int i = 0; i <= longueur de la planche(); i++) {
char gauche = (i) 0) ? 'X' : tableau.charAt(i - 1);
Char droit = (i == longueur du tableau() ? 'X' : tableau.charAt(i);
// Insérez seulement une balle qui correspond à au moins un voisin
pour (int color = 0; color < 5; color++) {
si (handCnt[couleur]) 0) poursuivre;
c = COULEURS[couleur];
si (c != gauche && c!= droite) continuer;

handCnt[color]--;
Chaîne après = effondrement(board.substring(0, i) + c + board.substring(i));
int res = dfs(après, handCnt);
Si (res != -1) ans = Math.min(ans, res + 1);
handCnt[color]++; // backtrack
}
}

mémo.put(key, ans). MAX_VALUE ? -1 : ans);
retourner mémo.get(key);
}

effondrement des chaînes privées (String s) {
StringBuilder sb = nouveau(s) StringBuilder;
booléen modifié = vrai;
pendant que (changement) {
changement = faux;
int n = longueur sb();
i = 0;
pendant que (i < n) {
i + 1;
pendant que (j < n& sb.charAt(j) == sb.charAt(i)) j++;
Si (j - i >= 3) { // supprimer les stries
sb.delete(i, j);
changement = vrai;
n = longueur sb();
i = Math.max(0, i - 1); // revérifier la position précédente
} autre {
i = j;
}
}
}
retour sb.toString();
}

Int. privée {
interrupteur c) {
cas «R»: retour 0;
case «Y»: retour 1;
cas «B»: retour 2;
cas «G»: retour 3;
case «W»: retour 4;
par défaut: lancer un nouvel argument illégalException();
}
}

chaîne privée mainCntToStr(int[] cnt) {
retour Chaîne.format("%d%d%d%d%d", cnt[0], cnt[1], cnt[2], cnt[3], cnt[4]);
}
}
«» "

C'est vrai. Pourquoi ça marche

- **Mémoization** garantit que chaque paire unique `(board, main)` est traitée une fois.
- **Filtration de gaz** (appariement d'un voisin) coupe les branches inutiles.
- **Collaps** est effectué de façon itérative jusqu'à ce que stable, s'assurant que le tableau est toujours canonique pour la clé de mémo.

---

4.2 Python

'`python
à partir de functools importer lru_cache
Importations provenant des collections Compteur

Solution de classe:
COULEURS = 'RYBGW'

def trouver MinStep (self, board: str, main: str) -> Int:
hand_cnt = [hand.count(c) pour c en soi. COULEURS]

@lru_cache(maxsize=Aucune)
def dfs(b: str, h: str) -> Int:
si non b:
retour 0
hand_cnt = [int(h[i]) pour i dans l'intervalle(5)]
meilleure = flotteur('inf')

# Scanner chaque point d'insertion
pour i dans la plage (len(b) + 1):
gauche = b[i-1] si i autre 'X '
droite = b[i] si i < len(b) autre 'X'

pour c en soi. COULEURS:
si cnt_main[se] [se]. COULEURS.index(c)] == 0:
poursuivre
Si c != gauche et c != à droite :
poursuivre

# Insérer
nouveau_plan = b[:i] + c + b[i:]
nouveau_plan = effondrement(nouveau_plan)

_self. COULEURS.index(c)] -= 1
res = dfs(new_board, ''.join(map(str, hand_cnt)))
_self. COULEURS.index(c)] += 1

si res != - 1 :
best = min(best, res + 1)

retour -1 si meilleur == flotter('inf') sinon meilleur

retour dfs(board, ''.join(map(str, hand_cnt)))

def effondrement(s): str -> str:
"""Supprimer à nouveau les stries de 3+ de même couleur."""
pile = []
i = 0
n = len(s)
alors que i < n:
j = i + 1
alors que j < n et s[j] == s[i]:
j += 1
si j - i >= 3 :
i = j # sauter ce bloc
Sinon:
Annexe(s[i:j])
i = j
new_s = ''.join(stack)
retour effondrement(new_s) si new_s != s autres nouvelles _s
«» "

> **Astuce:** La profondeur de récursion du Python n'est pas un problème ici parce que la profondeur ≤ 5 (taille de la main). La fonction `collapse` est récursive; elle est sûre et rapide.

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
Const string COLORS = "RYBGW";
unordered_map<string, int> mémo;

// Tableau d'effondrement après insertion
chaîne s'effondrer(const string &s) {
la chaîne cur = s;
bool change = true;
pendant que (changement) {
changement = faux;
int n = taille cur.();
chaîne suivante;
pour (int i = 0; i < n; ) {
i + 1;
pendant que (j < n& cur[j] == cur[i]) j++;
Si (j - i >= 3) {
change = true; // supprimer ce bloc
} autre {
suivant += cur.substr(i, j - i);
}
i = j;
}
cur.swap(suivant);
}
retour cur;
}

int dfs(carte à cordes, vecteur<int> &hand) {
si (board.vide()) retourne 0;
touche chaîne = tableau + "#" + toKey(main);
si (memo.count(key)) retourne mémo[key];

int best = INT_MAX;
int len = board.size();

pour (int i = 0; i <= len; ++i) {
char gauche = (i) 0) ? «? » : tableau [i-1];
char right = (i == len) ? '?' : planche[i];

pour (int c = 0; c < 5; ++c) {
si (!hand[c]) continue;
couleur du char = COULEURS[c];
si (couleur != gauche && couleur != droite) continuez;

[c];
string next = collaps(board.substr(0, i) + color + board.substr(i));
int res = dfs(suivant, main);
hand[c]++;

Si (res != -1) meilleur = min(meilleure, res + 1);
}
}

mémo[key] = (meilleur] INT_MAX ? -1 : meilleur;
retourner mémo[key];
}

chaîne toKey(const vector<int> &hand) {
chaîne k;
pour (int v : main) k += char('0' + v);
retour k;
}

public:
int trouver MinStep(planche à cordes, main à cordes) {
vecteur<int> cnt(5, 0);
pour (charc : main) cnt[COLORS.find(c)]++;
retour dfs(board, cnt);
}
};
«» "

---

C'est pas vrai. Qu'est-ce qui s'est passé ? (Les bons)

Explication
C'est pas vrai.
**Compact State** Autres
**Mémoisation**Évite les explosions exponentielles – chaque état visité une fois. Autres
**Filtration par gap**.Seulement insérer des couleurs qui peuvent déclencher un effondrement → moins de branches. Autres
**Claquement itératif**Le tableau devient canonique; la même configuration a toujours la même clé. Autres
**Language‐Specific Optimizations**=Java: custom hash key; Python: `lru_cache`; C++: `unordered_map` avec la clé chaîne. Autres

---

C'est pas vrai. Où ça pourrait être plus intelligent ? (Les méchants)

Numéro
C'est quoi ?
**Re-computation de la clé inutile**=Construire une nouvelle clé de chaîne chaque appel de récursion peut être lourd. Pré-calculer la chaîne de clés pour une fois, la réutiliser. Autres
**Complexité d'effondrement** Utilisez l'approche de la pile à deux points pour O(N). Autres
Autres **La taille actuelle suppose une taille manuelle ≤ 5. Si la main pousse, l'algorithme peut nécessiter une taille plus poussée (p. ex. compter les billes nécessaires pour chaque couleur). Autres
La carte de mémo n'est pas sécuritaire. Dans les concours, un seul fil est parfait. Autres

---

## 6--Pièges communs et causes de bord

Pourquoi ça arrive ?
- Oui.
**Empty Hand**= Si la main a zéro carte pour toutes les couleurs qui apparaissent dans le tableau, DFS retourne `-1` immédiatement. Autres Vérifiez tôt et retournez `-1`. Autres
**Circular Collapse**.Le retrait d'un bloc peut créer un autre de la même couleur à la limite. Une boucle d'effondrement itérative (drapeau modifié) assure que toutes les cascades sont manipulées. Autres
**Dupliquer les touches**La différence mineure dans l'ordre des mains peut produire le même état. La touche main est une chaîne à 5 chiffres; l'ordre est fixé par COLORS. Autres
**Python Récursion Profondeur**=La profondeur est limitée par la taille de la main (=5), si sûr. Si la taille de la main a augmenté, considérez la DFS itérative ou augmenter la limite de récursion. Autres

---

## 6-

- **En zonant sur les opérations clés** (insérer à l'écart + effondrement) réduit le problème à un petit DFS.
- **La représentation canonique** (tableau effondré) permet une mémoisation efficace.
- **Complexité du temps**: \(O(3^{H} \times 5^{H})\) \(O(10^3)\) pour le pire cas, grâce au mémo.
- **Complexité spatiale** : dominée par la carte mémo – au plus quelques milliers d'entrées.

---

Les pensées finales

Que ce soit dans **Java**, **Python** ou **C++**, l'idée centrale reste la même : traiter le jeu comme un problème de recherche d'état et utiliser la mémoisation pour pruner. Le jeu Zuma dans LeetCode 488 est un excellent exercice en compression *état*, en programmation dynamique* et en rétrotraçage récursif*.

Bon codage ! C'est ce qu'il a dit.

---

**Mots clés:** Zuma game, LeetCode 488, findMinStep, DFS, mémoisation, effondrement du plateau, compte de mains, Cache Java LRU, Python lru_cache, C++ non ordonné_map, conception d'algorithmes.