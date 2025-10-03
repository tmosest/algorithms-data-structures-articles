---
titre: LeetCode 1906. Demande de renseignements sur la différence absolue minimale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1906. Demandes de renseignements sur la différence absolue minimale
### D'un codeur prêt à l'interview

---

TL;DR
- **Problème** – Pour chaque requête `[l, r]` retourner la plus petite différence absolue entre deux *différents* nombres dans le sous-array `nums[l...r]`. Si tous les numéros sont identiques, retourner `-1`.
- **Key Insight** – "nums[i]" est limité par **1...100**. Ce petit domaine nous permet de construire une table de compte **préfixe** de taille `n × 100`.
- **Complexité** – temps "O(n + q) · 100", espace "O(n · 100). Fonctionne confortablement pour `n ≤ 1e5`, `q ≤ 2·104`.
- **Pourquoi c'est important** – Démontre la maîtrise de **préfixe des sommes**, **questions hors ligne** et **dénombrement de gamme**—tous les sujets doivent connaître pour les entrevues sur la structure des données.

---

- Oui. 1. Récapitulation des problèmes

> Avec `nums` (size `n`) et `queries` (`q` paires `[l, r]`), pour chaque recherche
> `` "
> min.nums[i] – nombres[j] avec l ≤ i < j ≤ r et nombres[i] Nombres [j]
> `` "
> Retourner `-1` si chaque élément de `[l, r]` est égal.

`n` peut être jusqu`à `105`, `q` jusqu`à `2·104`.
`nums[i]` vit dans `[1, 100]`.

---

- Oui. 2. Approches naïves

L'approche Temps Espace Verdict
C'est pas vrai.
Brute-force double boucle par requête. Autres
Autres Trier le sous-réseau par requête, puis numériser les voisins. Encore trop lent. Autres
Autres Utiliser une BST ou un multiset équilibré par requête. Une complexité inutile. Autres
**Prefix count + scan 1‐100**="O((n+q)·100)"="O(n·100)"=" **Pas assez** pour les contraintes. Autres

Parce que le domaine *value* est minuscule, nous pouvons éviter le tri ou les BST entièrement.

---

- Oui. 3. La solution optimale – Table de comptage des préfixes

3.1 Idées fondamentales

- Construire un tableau 2-D `pref[i][v]` = nombre d'occurrences de valeur `v` (0-basé sur l'index, `v [0,99]`) dans le préfixe `nums[0...i-1]`.
- Pour une requête `[l, r]` le nombre de valeur `v` dans la plage est
Texte
count_v = pref[r+1][v] - pref[l][v]
«» "
- Traverser tous les `v` de `0` à `99` et collecter les valeurs qui apparaissent au moins une fois dans la plage.
- Comme la liste est déjà triée par «v», la différence absolue minimale est simplement l'écart minimal entre les valeurs actuelles consécutives.
- Oui. Si une seule valeur est présente → répondre `-1`.

3.2 Pourquoi cela fonctionne

- **Nombre d'intervalles de temps constants**: La table de préfixe indique `O(1)` par valeur.
- **Nombre de valeurs fixes**: Nous envoyons toujours plus de 100 numéros – indépendamment de `n` ou `q`.
- **Pas de tri nécessaire**: Les valeurs sont traitées en ordre ascendant.

3.3 Complexité

- **Heure**: `O(n·100 + q·100)` = `O(n+q·100)` → environ 1,2 × 107 opérations pour le pire cas.
- **Espace**: 'O(n·100)' entiers (~ 40 Mo) – acceptables dans des environnements d'interview typiques.

---

- Oui. 4. Faits saillants de la mise en œuvre

#### 4.1 Java

"Java
solution de classe {
public int[] minDifférence(int[] nombres, int[][] requêtes) {
int n = longueur nums;
int[][] pref = nouvelle int[n + 1][100]; // nombre de préfixes

// préfixe de construction
pour (int i = 0; i < n; i++) {
Système.arraycopy(pref[i], 0, pref[i + 1], 0, 100);
[i + 1][nums[i] - 1]++; // passage à 0
}

int q = requêtes. longueur;
int[] ans = nouveau int[q];

pour (int qi = 0; qi < q; qi++) {
int l = requêtes[qi][0];
int r = requêtes[qi][1] + 1; // exclusive

int prev = -1, minDiff = entier.MAX_VALUE, distinct = 0;

pour (int v = 0; v < 100; v++) {
int cnt = pref[r][v] - pref[l][v];
si (cnt > 0) {
distinct++;
si (prév != -1) {
minDiff = Math.min(minDiff, v - prev);
}
prev = v;
}
}

ans[qi] = (distinct <= 1) ? -1 : minDiff;
}
le retour des an;
}
}
«» "

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def minDifférence(self, nombres: List[int], requêtes: List[List[int]]) -> Liste[int]:
n = len(nums)
pref = [[0] * 100 pour _ dans la plage (n + 1)]

pour i, val dans l'énumération(nombres, 1):
pref[i] = pref[i - 1] # copier la ligne précédente
[i] [val - 1] += 1

res = []
pour l, r dans les requêtes:
r += 1
prev = Aucune
distinct = 0
min_diff = 101
pour v dans la plage(100):
si pref[r][v] - pref[l][v]:
distinct += 1
si prev n'est pas None:
min_diff = min(min_diff, v - prev)
prev = v
res.append(-1 si distinct <= 1 autre min_diff)
retour res
«» "

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> minDifférence(vecteur<int>& nombres, vectorielle<vecteur<int>>& requêtes) {
int n = nombres.size();
vecteur<array<int, 100>> pref(n + 1);
pour (int i = 1; i <= n; ++i) {
pref[i] = pref[i - 1]; // copie
pref[i][nums[i - 1] - 1]++; // passage à 0
}

vecteur <int> ans;
as.reserve(queries.size());

pour (auto &q : requêtes) {
int l = q[0], r = q[1] + 1; // rendre r exclusif
Int prev = -1, minDiff = 101, distinct = 0;

pour (int v = 0; v < 100; ++v) {
si (préf[r][v] - pref[l][v]) {
+ différent;
si (prév != -1) minDiff = min(minDiff, v - prev);
prev = v;
}
}
ans.push_back(distinct <= 1 ? -1 : minDiff);
}
le retour des an;
}
};
«» "

---

- Oui. 5. Cas de bord et pièges

Pourquoi ça fait mal ?
- C'est quoi ?
Autres Oubliant de faire `r` exclusive lors de l'utilisation du préfixe sums. Autres
Utiliser `int[]]` en Java sans copier des lignes. Des
Autres Supposons que le domaine peut changer.Si `nums[i]` > 100, l'algorithme se brise. Autres
Impossible de traiter le cas `-1`. Autres
Utiliser `int[]]` pour le préfixe dans Python=Les listes de listes sont mutables; copier par ligne nécessaire= Utiliser `pref[i]= pref[i-1]=" dans la boucle. Autres

---

- Oui. 6. Variations du problème

Variante Solution suggérée
C'est-à-dire
** Nombres sans limite** (par exemple, 1...106) Compresser les valeurs, puis construire une table de préfixe 2-D ou utiliser un **BIT / Fenwick** sur les indices compressés. Autres
Autres **Grand nombre de requêtes** (`q φ 1e6`)= Le `100`-itération fonctionne toujours, mais vous pouvez frapper les limites de mémoire== Utilisez un **bitset** (`std::bitset<101>`) par préfixe pour couper l'espace. Autres
**Requêtes en ligne**= Besoin d'une structure de données qui prend en charge l'insertion/suppression à la volée==BST équilibrée (`TreeMap`) par préfixe, ou de maintenir un multiset pour la fenêtre coulissante. Autres
**Les mises à jour dynamiques de `nums`**.La table de préfixe devient stale. Autres

---

- Oui. 6. Pourquoi cette solution semble bonne dans les entrevues

1. **Shows Problem-Solving Skills** – Vous avez repéré le lien sur `nums[i]` et l'avez utilisé.
2. **Utilise Classic Data-Structures** – Les sommes de préfixe sont un agrafe; vous les transformez en table de comptage 2-D.
3. **Poignées Grandes Entrées Avec grâce** – Le temps et la mémoire restent linéaires dans `n` et `q`.
4. ** État de préparation linguistique** – Nous avons fourni un code idiomatique propre en Java, Python et C++.
5. **Extensible** – Le même motif (table de préfixe + scan de domaine fixe) fonctionne pour de nombreux problèmes de style de gamme-min-diff.

---

- Oui. 6. Liste de contrôle à emporter pour les intervieweurs

- [ ] Construisez correctement une table `pref` (lignes de copie, valeurs de décalage).
- [ ] Convertir la requête `[l, r]` en `[l, r+1)` avant de soustraire les préfixes.
- [ ] Scan `v` de `0` à `99` - pas de tri supplémentaire nécessaire.
- [ ] Retourner `-1` quand `distinct <= 1`.
Vérifier avec les cas d'angle :
- Des requêtes d'éléments uniques.
- Toutes valeurs égales.
- Demande de tableau complet.

---

- Oui. 6. Pensées finales

La gamme de valeurs **tiny** transforme un problème de recherche de gamme apparemment lourd en un algorithme simple et linéaire.
La maîtrise de ce modèle démontre :

- **Utilisation créative des contraintes** – transformer un problème qui semble avoir besoin d'un arbre de segment en un problème de comptage "O(1)".
- **Traitement hors ligne efficace** – construction de structures de données une fois et réutilisation pour de nombreuses requêtes.
- **Clear, maintenable code** – pas besoin de hacks obscurs, juste une table de préfixe propre et un seul passage sur 100 valeurs.

> *Si vous pouvez expliquer cette solution dans une interview et écrire le code Java/Python/C++ sur place, vous passerez la question de la structure des données avec des couleurs volantes. *

---

## SEO & Tags sociaux

- **Description détaillée**: Code Solve Leet 1906 – Demande de renseignements sur la différence absolue minimale dans O(n+q)·100. Table de comptage préfixe, solutions Java/Python/C++, conseils d'entretien, cas de bord. (en milliers de dollars)
- **Mots-clés**: `questions de différence absolue minimale`, `préfix sums`, `standing`, `LeetCode 1906`, `data structure interview`, `segment tree`, `Mo's algorithme`, `C++ solution`, `Java solution`, `Python solution`, `questions hors ligne`.

Bon codage, et bonne chance pour votre prochaine interview!