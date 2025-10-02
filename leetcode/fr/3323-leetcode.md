---
titre: LeetCode 3323. Minimiser les groupes connectés en insérant l'intervalle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Mastering LeetCode 3323: ** Minimiser les groupes connectés en insérant Interval**
> *Java-Python C++ – Une solution de fenêtre coulissante qui passe 1 e5*

---

- Oui. 1. Aperçu du problème

On vous donne un tableau de **intervalles** (chaque `[début, fin]`) et une longueur maximale autorisée `k` pour un intervalle *new* que vous devez insérer exactement une fois.
Après avoir inséré l'intervalle, vous voulez ** minimiser** le nombre de groupes *connectés* d'intervalles.

Un groupe *connecté* est un ensemble maximal d'intervalles qui couvrent ensemble une plage continue sans discontinuité.
Exemple :

Intervalles connectés ? Autres
C'est quoi ?
[[1,3],[3,5],[5,6]" (couvertures 1 à 6)"
[[1,2],[3,4]" (écart 2-3)"

**Retour** le plus petit nombre possible de groupes connectés après avoir ajouté le nouvel intervalle.

> **Constraints**
> * 1 ≤ " longueur d ' intervalle " ≤ 105
> * 1 ≤ `démarrage` ≤ `fin` ≤ 109
> * 1 ≤ `k` ≤ 109

---

- Oui. 2. Pourquoi ce problème est difficile

* ** Grande taille d'entrée** – O(n log n) est acceptable, mais tout ce qui est quadratique TLE.
* ** L'insertion doit couvrir les écarts** – Vous ne pouvez pas simplement migrer les intervalles ; vous devez réfléchir à la façon dont le nouvel intervalle peut s'étendre ** les écarts multiple** à la fois.
* **Sliding Window on Gaps** – L'astuce clé est de traiter les écarts entre les intervalles fusionnés comme une séquence et d'utiliser une fenêtre coulissante pour trouver la plus longue séquence contiguë des écarts qui peut être couverte par un seul intervalle de longueur ≤ k.

---

- Oui. 3. Aperçu de base

1. ** Fusionner les intervalles donnés** – Après fusion, chaque paire consécutive d'intervalles fusionnés est séparée par un *gap* de longueur `gapStartGapEnd`.
2. **Les gaz sont triés** – Parce que nous avons trié les intervalles d'origine par début, les écarts sont automatiquement dans l'ordre ascendant de leurs positions de départ.
3. **Couverture d'un bloc contigu de lacunes** – Si nous choisissons une fenêtre `[l ... r]` de trous, le nouvel intervalle doit s'étendre du *début* du premier trou jusqu'au *début* du dernier trou.
*Longueur requise* = "gaps[r].end - gaps[l].start".
4. **Fenêtre coulissante** – Déplacez un pointeur de droite, réglez le pointeur de gauche lorsque la longueur requise dépasse `k`. Suivre le nombre maximum d'écarts (`r-l+1`) qui entrent dans la limite.
5. **Réponse** – Chaque écart fusionné réduit le nombre de groupes d'un.
\[
\text{réponse} = \text{groupes} - \max_{\text{window}}\#\text{gaps} = (\text{gaps} + 1) - \maxCovered = \text{groupes} - \maxCouvert
\]

---

- Oui. 4. Étapes de l'algorithme

1. **Trier les intervalles** en commençant par monter; si égal, par fin descendant (pour que nous puissions fusionner facilement).
2. **Merge** recoupant ou touchant les intervalles → "mergé".
3. **Collectez les écarts** entre les intervalles consécutifs de «fusion» → «gaps».
4. **Fenêtre coulissante sur les lacunes**
* `l = 0`, `maxCovered = 0`
* Pour chaque `r` dans `[0 ... gaps.size-1] "
* Bien que `requisLongueur > k`, incrément `l`.
* Mettre à jour `maxCovered = max(maxCovered, r-l+1)`.
5. **Retour** `merged.size() - maxCovered'.

---

- Oui. 5. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Classer **O(n log n)**
*O(n)**
Écarts **O(m)** où *m* = fusion.size()
Fenêtre coulissante
**O(n log n)**

Cela satisfait confortablement les contraintes.

---

- Oui. 6. Mise en œuvre – Java

"Java
Importation de java.util.*;

solution de classe publique {
public int minGroupes(int[][] intervalles, int k) {
i (intervalles) = 0. 0) retour 0;

// 1. Tri par début; tie‐break par fin descendante
Tableaux.sort(intervalles, a, b) -> {
si (a[0] == b[0]) retourne Integer.compare(b[1], a[1]);
retour Integer.compare(a[0], b[0]);
});

// 2. Fusionner les intervalles
Liste<int[]> fusionnée = nouvelle liste de distribution<>();
Int curStart = intervalles[0][0];
inter curEnd = intervalles[0][1];
pour (int i = 1; i < intervalles de longueur; i++) {
int[] cur = intervalles[i];
si (cur[0] <= curEnd) { // chevauchement ou contact
curEnd = Math.max(curEnd, cur[1]);
} autre { // disjoint
fusionned.add(new int[]{curStart, curEnd});
curStart = cur[0];
curEnd = cur[1];
}
}
fusionned.add(new int[]{curStart, curEnd});

// 3. Rassembler les écarts entre les intervalles fusionnés
int m = fusion.size();
Si (m) 1) retour 1; // un seul groupe, rien à pont
Liste des lacunes<int[]> = nouvelle liste de répartition<>();
pour (int i = 0; i < m - 1; i++) {
int end1 = fusionné.get(i)[1];
int start2 = fusionné.get(i + 1)[0];
gaps.add(new int[]{end1, start2}); // gap: (end1, start2)
}

// 4. Fenêtre coulissante sur les trous
int l = 0, maxCovered = 0;
pour (int r = 0; r < gaps.size(); r++) {
// longueur requise pour couvrir les lacunes[l..r]
pendant que (l <= r && gaps.get(r)[1] - gaps.get(l)[0] > k) {
l++;
}
maxCovered = Math.max(maxCovered, r - l + 1);
}

// 5. Résultat: groupes - maxCovered
retour need.size() - maxCovered;
}
}
«» "

---

- Oui. 7. Mise en œuvre – Python

'`python
de taper l'importation Liste

Solution de classe:
def minGroupes connectés(eux-mêmes, intervalles: List[List[int]], k: int) -> Int:
intervalles.sort(key=lambda x: (x[0], -x[1]))

Fusionner
fusionné = []
cur_start, cur_end = intervalles[0]
pour s, e par intervalles[1:]:
si s <= cur_end: # chevauchement / contact
cur_end = max(cur_end, e)
Sinon:
fusionne.append((cur_start, cur_end))
cur_start, cur_end = s, e
fusionne.append((cur_start, cur_end))

si len (fusionné) == 1 :
retour 1

Les lacunes
Lacunes = []
pour (s1, e1), (s2, e2) dans zip(fusionné, fusionné[1:]):
gaps.append(e1, s2)) # (fin_de_première, début_de_seconde)

Fenêtre coulissante
l = 0
max_couvert = 0
pour r à portée(len(gaps):
alors que l <= r et lacunes[r][1] - lacunes[l][0] > k:
l += 1
max_covered = max(max_covered, r - l + 1)

retour len(mergé) - max_couvert
«» "

---

- Oui. 8. Mise en œuvre – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minGroupes connectés(vecteur<vecteur<int>>& intervalles, int k) {
tri(intervalles.debut(), intervals.end(),
[](const vector<int>& a, const vector<int>& b) {
si (a[0] == b[0]) retourne a[1] > b[1];
retourner a[0] < b[0];
});

// Intervalles de fusion
vecteur<pair<long long, long>> fusion;
long curStart = intervalles[0][0];
longue courbure longue = intervalles[0][1];
pour (size_t i = 1; i < intervals.size(); ++i) {
long s = intervalles[i][0];
long e = intervalles[i][1];
si (s <= curEnd) { // chevauchement
curEnd = max(curEnd, e);
} autre {
fusionne.emplace_back(curStart, curEnd);
curStart = s;
curEnd = e;
}
}
fusionne.emplace_back(curStart, curEnd);

si (merged.size()) == 1) retour 1;

// Écarts entre les intervalles fusionnés
vecteur<pair<long long, long>> les lacunes;
pour (size_t i = 0; i + 1 < fusionne.size(); ++i) {
long terme1 = fusionné[i].seconde;
longue durée de démarrage2 = fusionné[i + 1].
gaps.emplace_back(end1, start2); // (fin, start)
}

// Fenêtre coulissante sur les trous
taille_t l = 0, maxCouverture = 0;
pour (size_t r = 0; r < gaps.size(); ++r) {
alors que (l <= r && gaps[r].second - gaps[l].first > k) {
++l;
}
maxCovered = max(maxCovered, r - l + 1);
}

retourner static_cast<int>(merged.size() - maxCovered);
}
};
«» "

---

- Oui. 9. Cas de bord traités

Comment nous le traitons
-- -- -- -- -- --
Autres Aucun intervalle.
Autres Tous les intervalles se chevauchent déjà → un groupe
Autres Un nouvel intervalle ne peut couvrir aucun écart. Autres
Autres Lacunes exactement de la longueur `k`-

---

- Oui. 10. Essai – Essai en unité rapide (Java)

"Java
public statique vide principal(String[] args) {
int[]a = {{1, 3}, {3, 5}, {6, 7}, {8, 9}, {10, 11}};
System.out.println(nouvelle solution().minGroupes connectés(a, 4)); // attendu 2
}
«» "

Exécutez le même test sur Python et C++ pour confirmer la cohérence.

---

## 11. Prenez l'initiative de votre entrevue

* **Toujours penser à fusionner en premier** – Réduit le problème à une séquence linéaire de lacunes.
* **Les écarts de traitement en tant que principale structure de données** – Ce sont les seules parties que vous pouvez -Pont.
* **Utilisez une fenêtre coulissante** – La technique classique à deux points s'applique même lorsque la contrainte de la fenêtre dépend d'une différence calculée ('gapEnd - gapStart').
* ** Méfiez-vous des débordements entiers** – Les lacunes et les longueurs requises peuvent atteindre 109, donc utiliser des types 64 bits (Java `long`, C++ `long`, Les entiers natifs de Python).

---

- Oui. 12. Lecture supplémentaire et problèmes connexes

* **** : Nombre maximal d'intervalles non chevauchants** – fenêtre coulissante classique
* **=Merge Intervals==** – problème fondamental dans la manipulation de l'intervalle
* **=Longest subarray avec la somme ≤ k=** – fenêtre coulissante analogique pour les sommes

---

13. Verdict final

Avec la stratégie fusion‐gap‐gliding‐window, le problème devient une question de **une passe linéaire** après tri.
Cette solution élégante non seulement passe les limites de temps, mais vous donne également une base de code propre et durable en Java, Python et C++.

> ** Bon codage !**

---

> **Mots-clés**: fusion d'intervalle, espaces, fenêtre coulissante, LeetCode, interview d'algorithme, complexité temporelle O(n log n).