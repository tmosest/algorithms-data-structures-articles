---
titre: LeetCode 1840. Hauteur maximale du bâtiment -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Hauteur maximale du bâtiment – LeetCode 1840
- Oui. (Log M) – M = #restrictions)

> **Problème**
> On vous donne `n` nouveaux bâtiments dans une ligne (`1 ... n`).
> * Le bâtiment 1 doit avoir une hauteur 0.
> * Les bâtiments adjacents peuvent différer au maximum de 1.
> * Certains bâtiments ont une limite supérieure: `restrictions[i] = [id, maxHeight]`.
> Retournez la hauteur maximale du bâtiment le plus haut.

> **Constraints**
> * "2 ≤ n ≤ 109"
> * `0 ≤ restrictions. longueur ≤ min(n-1, 105) "
> * Chaque `id` est unique et 1.
> * `0 ≤ maxHauteur ≤ 109 "

> **Objectif** – écrire du code propre, prêt à la production en Java, Python et C++ et expliquer les parties *good*, *bad* et *ugly* de la solution.

---

- Oui. 1. Intuition & Greedy Insight

La seule chose qui limite la hauteur d'un bâtiment est la restriction la plus étroite* de chaque côté et la règle *différence adjacente*.

Si nous examinons deux restrictions consécutives (ou la restriction virtuelle au bâtiment 1), les hauteurs que nous pouvons attribuer aux bâtiments entre les deux doivent satisfaire

«» "
H[j] – H[j+1] ≤ 1 pour tous les J dans cet intervalle
«» "

et ne peut pas dépasser les deux hauteurs de la frontière.
Compte tenu des deux hauteurs limites `hL` (à l ' id `x`) et `hR` (à l ' id `y`), la plus haute hauteur possible à l ' intérieur de l ' intervalle est simplement

«» "
(hL, hR) + (y – x) – (hL – hR) / 2
«» "

Parce que nous pouvons monter de la limite inférieure jusqu'à ce que nous manquions de distance.
Donc le problème se réduit à

1. **Commander toutes les restrictions par id** (plus le point obligatoire `1,0').
2. **Clip** chaque restriction a une hauteur des deux côtés de sorte que la différence avec son voisin ne dépasse jamais la distance entre eux.
3. **Scannez chaque intervalle** et calculez la hauteur maximale possible.

C'est un coup de foudre classique.

> **Pourquoi ça marche** – Les contraintes sont toutes *locales* (différences adjacentes) et *monotonique* (aucun avantage à élever un bâtiment au-delà de la restriction la plus proche). En forçant les hauteurs à être aussi bas que nécessaire des deux côtés, nous garantissons que nous pouvons toujours satisfaire toutes les restrictions tout en maintenant la possibilité d'un pic élevé intact.

---

- Oui. 2. Caisses de bord et pièces d'exception

C'est une mauvaise idée.
- Oui.
Grand `n` (jusqu'à 1 milliard) – il est impossible d'aller sur chaque bâtiment. Autres Nécessité d'utiliser des entiers 64 bits (`long` / `long`) parce que `hauteur maximale + distance` peut déborder de 32 bits. Autres
Autres Aucune restriction du tout – le bâtiment le plus haut se trouve simplement à la position `n`. Autres
Les restrictions peuvent ne pas inclure le bâtiment 1 ou le bâtiment n. Autres
Tri O(M log M) où M ≤ 105 est bon, mais doit être mis en œuvre correctement. Autres Utiliser une paire/tuple qui mélange les types int et long peut conduire à des bugs subtils. Autres

---

- Oui. 3. L'algorithme optimal

1. **Ajouter le point obligatoire** `(1, 0)` à la liste des restrictions.
2. **Trier** la liste par numéro de bâtiment.
3. ** Passage vers l'avant** – pour chaque restriction `i` (à partir de la seconde), set
`hauteur[i] = min[i], hauteur[i-1] + (id[i] - id[i-1])"
4. **Pass arrière** – pour chaque restriction "i" (à partir de la deuxième dernière), ensemble
`hauteur[i] = min[i], hauteur[i+1] + (id[i+1] - id[i])"
5. ** Calculer la réponse**
* Initialiser `ans = 0`.
* Pour chaque paire consécutive `(i, i+1)` dans la liste, laissez `d = id[i+1] - id[i]`, `hL = hauteur[i]`, `hR = hauteur[i+1]`.
`peak = max(hL, hR) + ( d - abs(hL - hR) ) / 2`.
`ans = max(ans, pic)`.
* Traitez également le dernier segment du bâtiment `n`: `peak = height[last] + (n - id[last])`.
Mettre à jour `ans` en conséquence.

L'algorithme fonctionne dans **O(M log M)** time et **O(M)** memory – parfaitement adapté aux limites.

---

- Oui. 4. Code

Voici les implémentations entièrement commentées dans **Java**, **Python** et **C++**.
Tous les trois utilisent des entiers 64 bits pour éviter les débordements.

---

#### 4.1 Java

"Java
Importation de java.util.*;

***
* Code Leet 1840 - Hauteur maximale du bâtiment
* Solution Greedy O(M log M)
*/
solution de classe {

public int maxBuilding(int n, int[][] restrictions) {
// Liste des {id, hauteur}
Liste <long[]> list = nouvelle liste d'array<>();

// Point de départ obligatoire
liste.add(nouveaux longs[]{1L, 0L});

// Ajouter des restrictions réelles
pour (int[] r : restrictions) {
liste.add(nouveaux longs[]{r[0], r[1]});
}

// Trier par id
liste.sort(Comparator.comparingLong(a -> a[0]);

int m = list.size();

// Passer vers l'avant
pour (int i = 1; i < m; i++) {
longue dist = list.get(i)[0] - list.get(i - 1)[0];
long permis = list.get(i - 1)[1] + dist;
si (list.get(i)[1] > autorisé) {
list.get(i)[1] = autorisé;
}
}

// Passage en arrière
pour (int i = m - 2; i >= 0; i--) {
longue dist = list.get(i + 1)[0] - list.get(i)[0];
long permis = list.get(i + 1)[1] + dist;
si (list.get(i)[1] > autorisé) {
list.get(i)[1] = autorisé;
}
}

// Calculer la réponse
long ans = 0;

// Intervalles entre les restrictions
pour (int i = 0; i < m - 1; i++) {
longue idL = list.get(i)[0];
long hL = list.get(i)[1];
longue idR = list.get(i + 1)[0];
long hR = list.get(i + 1)[1];

longue distance = idR - idL;
pic long = Math.max(hL, hR) + (dist - Math.abs(hL - hR)) / 2;
si (crête > ans) ans = pic;
}

// Dernier segment à construire n (aucune restriction supérieure)
longue dernière Id = list.get(m - 1)[0];
long lastH = list.get(m - 1)[1];
long pic Fin = lastH + (n - lastId);
si (peakEnd > ans) ans = pic Fin;

// et s'adapte en 32 bits parce que les contraintes le garantissent
retour (int) ans;
}
}
«» "

---

4.2 Python

'`python
Solution de classe:
def maxBuilding(self, n: int, restrictions: List[List[int]]) -> Int:
# Liste des tuples (id, hauteur) comme ints
lst = [(1, 0)]
lst.extend(restrictions)

# Tri par id
lst.sort(key=lambda x: x[0])

# Passer vers l'avant
pour i dans la plage (1, len(lst)):
dist = lst[i][0] - lst[i-1][0]
admis = lst[i-1][1] + dist
si les conditions suivantes sont admises:
lst[i] = (lst[i][0], autorisé)

Passage en arrière
pour i dans l'intervalle (len(lst)-2, -1, -1):
dist = lst[i+1][0] - lst[i][0]
admis = lst[i+1][1] + dist
si les conditions suivantes sont admises:
lst[i] = (lst[i][0], autorisé)

# Calculer la réponse
ans = 0
pour i dans la fourchette (len(lst)-1):
idL, hL = lst[i]
idR, hR = lst[i+1]
dist = idR - idL
pic = max(hL, hR) + (dist - abs(hL - hR)) // 2
ans = max(ans, pic)

# Dernier segment à n
last_id, last_h = lst[-1]
ans = max(ans, last_h + (n - last_id))
retour et
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxBuilding(int n, vector<vector<int>>& restrictions) {
// vecteur de paires {id, hauteur} en utilisant longue
vecteur<pair<long long,long long>> v);
v.emplace_back(1LL, 0LL);
pour (auto &r : restrictions)
v.emplace_back(r[0], r[1]);

trier(v.begin(), v.end()); // trier par id

int m = v.size();

// Passer vers l'avant
pour (int i = 1; i < m; ++i) {
long long dist = v[i].premier - v[i-1].premier;
long permis = v[i-1].seconde + dist;
si (v[i].seconde > autorisée) v[i].seconde = autorisée;
}

// Passage en arrière
pour (int i = m-2; i >= 0; --i) {
long long dist = v[i+1].premier - v[i].premier;
long permis = v[i+1].seconde + dist;
si (v[i].seconde > autorisée) v[i].seconde = autorisée;
}

long an = 0;

// Intervalles entre les restrictions
pour (int i = 0; i < m-1; ++i) {
long idL = v[i].premier, hL = v[i].seconde;
long idR = v[i+1].premier, hR = v[i+1].seconde;
longue distance = idR - idL;
long pic long = max(hL, hR) + (dist - llabs(hL - hR)) / 2;
ans = max(ans, pic);
}

// Dernier segment à construire n
long last_id = v.back().first, last_h = v.back().second;
ans = max(ans, last_h + (long long)n - last_id);

retourner static_cast<int>(ans);
}
};
«» "

---

- Oui. 5. Pourquoi cette solution est prête à la production

Critère Ce que nous avons fait
C'est pas vrai.
**Complicité du temps** Autres
**L'espace-complexité** Autres
**Sécurité de l'écoulement**= Toutes les valeurs intermédiaires utilisent 64 bits (long'/long'). Autres
**Readability**= Les noms variables comme `idL`, `hL`, `peak` rendent l'intention évidente. Autres
**Test**Le code gère zéro, une et de nombreuses restrictions sans boîtier spécial dans la boucle principale. Autres
**Sécurité du boîtier**Le clippage avant et arrière garantit que chaque paire de points consécutifs satisfait à la règle de distance, éliminant ainsi la nécessité d'une vérification de faisabilité complexe plus tard. Autres

---

- Oui. 6. Résumé

Aspect
C'est pas vrai.
**Bon**Simple balayage gourmand, scans linéaires, formule claire pour le pic d'intervalle. Autres
**Le temps et la mémoire sont optimaux. Autres
**Ugly**= Utilisation soigneuse des types 64 bits et des points virtuels pour `n`. Autres

Ce schéma de **triage + coupe à deux côtés + analyse de l'intervalle** apparaît dans de nombreux problèmes (p. ex., "Construisez la Fence", "Maximum Subarray avec Contraintes"), et le même raisonnement s'applique : imposer les contraintes localement, puis calculer l'optimum global à partir des frontières clippées.

---

- Oui. 7. Comment appliquer cette connaissance

* **Interview** – décrire le balayage gourmand et la formule de pic d'intervalle en moins de 5 minutes.
* **Code de production** – ajouter des vérifications défensives (par exemple, vérifier `n > 0`, `restrictions` non-null).
* **Tests** – créer des tests unitaires couvrant:
* Aucune restriction.
* Une seule restriction loin des deux extrémités.
* Restrictions multiples qui se chevauchent.
* Grand `n` avec peu de restrictions.
* Les cas qui forcent la coupure vers l'avant ou vers l'arrière à prendre effet.

Avec cette fondation, vous pouvez aborder avec confiance les variations des problèmes de construction et de hauteur qui apparaissent dans le codage des entrevues, des concours et des logiciels de planification architecturale du monde réel. Bon codage !

---

**Mots-clés**: * Hauteur maximale du bâtiment*, *Code de bord 1840*, *Plongée de grêle*, *O(M log M*), *différence adjacente*, *découpage de restriction*, *Java*, *Python*, *C++*, *cas de bordure*.