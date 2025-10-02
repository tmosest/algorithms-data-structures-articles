---
titre: LeetCode 2055. Plaques entre les bougies -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Idée de la solution – O(n + q)**

Pour chaque requête `(l , r)` nous avons besoin

* le premier `' à ou après `l` – appelez-le **L**
* le dernier `" à ou avant `r` – appelez-le **R**
* le nombre de `*` entre **L** et **R**.

Si une telle paire de tuyaux n'existe pas (il n'y a pas de `=" à gauche de `r` ou pas de `="` à droite de `l`), la réponse est `0`.

Toutes les informations dont nous avons besoin peuvent être obtenues en un seul scan de la chaîne:

Description de la variable
- C'est quoi ?
"nextPipe[i]"" distance de `i` au **nearest `" sur la droite** (y compris lui-même). `-1` si aucune. Scanner de droite à gauche. Autres
"prevPipe[i]"" distance entre `i` et le **nearest `" sur la gauche** (y compris lui-même). `-1` si aucune. Scanner de gauche à droite. Autres
"starPref[i]" Nombre de `*` ** strictement avant** position `i` (c'est-à-dire dans `[0 , i)`). Valeur préfixe standard. Autres

Avec ces trois tableaux, chaque requête est répondue en O(1).

---

Prétraitement (O(n))

'`cpp
int n = s.size();
vecteur<int> étoilePref(n + 1, 0); // étoilePref[0] = 0
vector<int> nextPipe(n, -1); // distance jusqu'à la suivante '
vector<int> prevPipe(n, -1); // distance jusqu'à la précédente '

int lastPipe = -1; // distance jusqu'à la plus proche '=' sur la gauche
pour (int i = 0; i < n; ++i) {
Si (s[i] == '*')
étoilePref[i + 1] = étoilePref[i] + 1;
Autre
starPref[i + 1] = starPref[i];

if (s[i] == '=) lastPipe = 0; // la position du courant est un tuyau
Sinon si (lastPipe != -1) ++lastPipe;
prevPipe[i] = lastPipe; // distance jusqu'à la plus proche '' sur la gauche
}
«» "

'`cpp
Int nextPipeDist = -1;
pour (int i = n - 1; i >= 0; --i) {
si (s[i] == '=) suivantPipeDist = 0;
Sinon si (suivantPipeDist != -1) ++suivantPipeDist;
nextPipe[i] = nextPipeDist; // distance jusqu'à la plus proche '=" à droite
}
«» "

Tout de suite

* index du premier tuyau après la position `l` → `l + nextPipe[l]` (si la suivante est Pipe[l]) -1` → pas de tuyau)
* index du dernier tuyau avant la position `r` → `r - prevPipe[r]` (si 'prevPipe[r]]] -1` → pas de tuyau)

---

C'est vrai. Réponse à une requête (O(1))

'`cpp
int left = requêtes[i][0];
int right = requêtes[i][1];

int afterL = (suivantPipe[left]] -1) ? -1 : gauche + suivantePipe[gauche];
int beforeR = (prevPipe[right]). -1) ? -1 : à droite - prevPipe[à droite];

si (après L == -1=1 avant R == -1=1 après L > droite=1 avant R < gauche) {
ans[i] = 0; // aucune paire de tuyaux valide
} autre {
ans[i] = étoilePref[avantR] - étoilePref[aprèsL];
}
«» "

Le tableau `starPref` est défini de sorte que `starPref[x]` est égal au nombre de `*` ** strictement avant** la position `x`.
D'où "starPref[avant R] - starPref[après L]" compte exactement le `*` entre les deux tuyaux.

---

Complexité

*Time* : `O(n + q)` – un passage linéaire pour le prétraitement et un pour les requêtes.
*Espace*: `O(n)` – trois tableaux entiers de longueur `n`.

---

#### Mise en œuvre complète du C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> plaques EntreCandles(chaîne s, vecteur<vector<int>>&questions) {
n = (int)s.size();

- Oui. Prétraitement
vecteur<int> étoilePref(n + 1, 0); // étoilePref[i] = nombre de '*' dans [0, i)
vector<int> nextPipe(n, -1); // distance jusqu'à la suivante '
vector<int> prevPipe(n, -1); // distance jusqu'à la précédente '

int dist = -1; // distance jusqu'à la plus proche '=" sur la gauche
pour (int i = 0; i < n; ++i) {
Si (s[i] == '*')
étoilePref[i + 1] = étoilePref[i] + 1;
Autre
starPref[i + 1] = starPref[i];

si (s[i]] == «») dist = 0;
Sinon si (dist != -1) ++dist;
prevPipe[i] = dist; // distance jusqu'au tuyau le plus proche à gauche
}

dist = -1; // maintenant de droite à gauche
pour (int i = n - 1; i >= 0; --i) {
si (s[i]] == «») dist = 0;
Sinon si (dist != -1) ++dist;
nextPipe[i] = dist; // distance jusqu'au tuyau le plus proche à droite
}

Réponses aux questions
vectorielle <int> ans(queries.size(), 0);
pour (int i = 0; i < (int)queries.size(); ++i) {
int l = requêtes[i][0];
int r = requêtes[i][1];

int afterL = (suivantPipe[l]) -1) ? -1 : l + nextPipe[l];
int beforeR = (prevPipe[r]) -1) ? -1 : r - prevPipe[r];

si (après L == -1=1 avant R == -1=1 après L > r=1 avant R < l)
as[i] = 0;
Autre
ans[i] = étoilePref[avantR] - étoilePref[aprèsL];
}
le retour des an;
}
};
«» "

Le code suit l'algorithme décrit ci-dessus et fonctionne dans l'espace requis « O(n + q) » et « O(n) ».