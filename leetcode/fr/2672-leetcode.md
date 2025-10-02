---
Titre: LeetCode 2672. Nombre d'éléments adjacents avec la même couleur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Aperçu de la solution**

Pour chaque requête, nous ne changeons que la couleur d'une cellule.
Après ce changement, nous avons seulement besoin de savoir si cette cellule forme maintenant une paire *
avec son voisin gauche ou son voisin droit.

Le nombre total de paires est la réponse pour cette requête.
Laissez

«» "
cnt – nombre actuel de paires de couleurs égales adjacentes
col[i] – couleur courante de la cellule i (0 = non coloré)
«» "

Pour une requête `(pos , newColour)`:

1. **Supprimer les anciennes paires fournies par «col[pos]».**
Si «col[pos]» était non-zéro et correspondait au voisin gauche → `cnt--`.
Si elle correspond au bon voisin → `cnt--`.

2. **Peindre la cellule. **
«col[pos] = nouvelle couleur».

3. **Ajouter les nouvelles paires créées par `newColour`.**
Si le voisin gauche n'est pas zéro et équivaut à "nouvelle couleur" → `cnt++`.
Si le bon voisin est non-zéro et égal à "nouvelle couleur" → `cnt++`.

Conservez `cnt` après chaque requête.
Toutes les opérations pour une requête sont O(1), de sorte que l'algorithme entier est O(m) où `m` est le nombre de requêtes.

---

Mise en œuvre de Python

'`python
de taper l'importation Liste

Solution de classe:
def couleur TheArray(self, n: int, requêtes: List[List[int]]) -> Liste[int]:
couleurs = [0] * n # couleurs courantes, 0 = non colorées
res = [] # réponses pour chaque requête
paires = 0 nombre actuel de paires de couleurs égales

pour pos, new_colour dans les requêtes :
old_colour = couleurs[pos]

# supprimer les vieilles paires impliquant des pos
if old_colour != 0:
if pos > 0 and colors[pos-1] == old_colour:
paires -= 1
if pos + 1 < n and colors[pos+1] == old_colour:
paires -= 1

# peinture pos avec la nouvelle couleur
couleurs[pos] = nouvelle couleur

# ajouter de nouvelles paires créées par la nouvelle couleur
if pos > 0 and colors[pos-1] == new_color:
paires += 1
si pos + 1 < n et couleurs[pos+1] == new_colour:
paires += 1

res.append(paires)

retour res
«» "

- Oui. Implémentation Java (15 lignes de code propre)

"Java
solution de classe {
public int[] colorTheArray(int n, int[][] requêtes) {
int[] col = nouvelle int[n];
int[] ans = nouvelle int[queries.longueur];
cnt = 0;

pour (int i = 0; i < requêtes.longueur; i++) {
int pos = requêtes[i][0];
int newCol = requêtes[i][1];

si (col[pos] != 0) {
si (pos > 0 && col[pos-1] == col[pos]) cnt--;
si (pos + 1 < n && col[pos+1] == col[pos]) cnt--;
}

col[pos] = nouveau Col.

si (pos > 0 && col[pos-1] == newCol) cnt++;
si (pos + 1 < n && col[pos+1] == newCol) cnt++;

as[i] = cnt;
}
le retour des an;
}
}
«» "

### Mise en œuvre C++ (compacte 15‐ligne)

'`cpp
solution de classe {
public:
vector<int> colorTheArray(int n, vector<vector<int>>& requêtes) {
vecteur<int> col(n, 0), ans(queries.size());
cnt = 0;
pour (int i = 0; i < requêtes.size(); ++i) {
int pos = requêtes[i][0], c = requêtes[i][1];
si (col[pos] != 0) {
si (pos > 0 && col[pos-1] == col[pos]) --cnt;
si (pos + 1 < n && col[pos+1] == col[pos]) --cnt;
}
col[pos] = c;
si (pos > 0 && col[pos-1] == c) + cnt;
si (pos + 1 < n && col[pos+1]] c) + cnt;
as[i] = cnt;
}
le retour des an;
}
};
«» "

---

Complexité

Valeur métrique
C'est pas vrai.
Heure **O(m)**, `m` = nombre de requêtes
Espace **O(n)** pour le tableau des couleurs (plus O(m) pour le résultat)

Cette solution est optimale – chaque requête est traitée en temps constant.