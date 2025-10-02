---
titre: LeetCode 2070. Plus bel article pour chaque requête -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2070 – Le plus bel article pour chaque requête
*Un guide complet (Java-Python C++) + SEO-ready blog post pour décrocher votre prochain emploi technologique*

---

Aperçu du problème

> **Numéro de dossier**: 2070
> **Difficulté**: Moyenne
> **Tags**: Tri de recherche binaire

On vous donne un éventail d'éléments, chacun représenté comme `[prix, beauté]`, et un éventail de requêtes.
Pour chaque requête `q`, vous devez répondre: *Quelle est la beauté maximale d'un article dont le prix ≤ q? *
Si aucun élément de ce type n'existe, retourner `0`.

---

Les contraintes

Paramètre Portée Remarques
- C'est quoi ?
"items.length", "creries.length" 1 ... 105" Grand, mais toujours gérable avec O(n+q) log n)
"prix", "beauté", "queries[j]" 1 ... 109" L'int signée 32 bits est suffisante en Java/Python, mais utiliser 64 bits en C++
Autres Les articles peuvent avoir des prix en double ou des beautés

---

Intuition et idée clé

1. **Trier les articles par prix** – cela met tous les articles abordables pour un budget dans un bloc contigu.
2. **Construisez une carte de la meilleure beauté** – pendant que nous balayons les articles triés, gardez la beauté maximale en cours.
3. **Répondre aux requêtes dans O(log n)** par recherche binaire au premier prix qui est ≤ la valeur de la requête.

Cela réduit l'approche naïve O(n·q) (vérifier chaque élément pour chaque requête) à O(n+q) log n).

---

Algorithme pas à pas

1. **Trier** « items » par le premier élément (« prix »).
2. **Pré-processus**:
Texte
maxBeauté = 0
pour chaque article (prix, beauté) dans les articles triés:
maxBeauté = max(maxBeauté, beauté)
si prix != dernier Prix Vu :
record (prix, maxBeauty) // garde la meilleure beauté à ce prix
«» "
Cela produit deux tableaux parallèles: `prix[]` et `beautés[]`.
3. **Réponse aux requêtes**: Pour chaque `q` dans `questions`, recherche binaire `prix[]` pour trouver le plus grand indice `i` avec `prix[i] ≤ q`.
Dans le cas contraire, répondez `0`; sinon répondez `beautés[i]`.

---

C'est vrai. Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Autres Produits de tri **O(n log n)**
Prétraitement
Autres Boucle de requête (recherche binaire)
**O((n+q) log n)**

Avec `n, q ≤ 105`, cela correspond confortablement dans les limites de temps de LeetCode.

---

#### 6.

Pourquoi ça compte ?
- Oui.
Dupliquer les prix avec des beautés différentes Dupliquer la recherche binaire peut retourner la mauvaise beauté si nous ne conservons pas la **maximum** beauté pour ce prix Dupliquer la recherche binaire peut retourner la mauvaise beauté
Autres Toutes les requêtes sont plus petites que le plus petit prix. `0`ш Retours de recherche binaires `-1`; traiter comme `0`
Grandes valeurs entières (jusqu'à 1e9) : risque de débordement dans certaines langues : utiliser des entiers 64 bits (`long` en Java, `long` en C++, int par défaut en Python) :

---

Mise en œuvre du code

> **Toutes les implémentations suivent la même logique algorithmique. **
> Utilisez la langue qui correspond à votre cible de travail; n'hésitez pas à copier-coller dans votre éditeur.

##### 7.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
public int[] maximumBeauty(int[][] items, int[] requêtes) {
Classer les articles par prix
les tableaux.sort(items, Comparator.comparingInt(a -> a[0]);

// 2=2 construire des tableaux de beauté de préfixe max
int n = éléments.longueur;
prix int[] = nouveaux prix int[n];
int[] bestBeauties = nouveau int[n];
Int maxBeauty = 0;
Int idx = 0;
pour (int[] it : items) {
prix int = it[0];
Int beauty = it[1];
maxBeauty = Math.max(maxBeauty, beauty);
prix[idx] = prix;
bestBeauties[idx] = maxBeauty;
idx++;
}

// Réponse à chaque requête par recherche binaire
int[] ans = nouvelle int[queries.longueur];
pour (int i = 0; i < requêtes.longueur; i++) {
int q = requêtes[i];
int pos = upperBound(prix, q) - 1; // dernier indice ≤ q
ans[i] = (pos >= 0) ? bestBeauties[pos] : 0;
}
le retour des an;
}

// premier indice > cible
Int privé supérieurBound(int[] arr, int cible) {
int l = 0, r = longueur d'arrondi;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= cible) l = m + 1;
autres r = m;
}
retour l;
}
}
«» "

##### 7.2 Python (Python 3)

'`python
de bisect import bisect_right
de taper l'importation Liste

Solution de classe:
def maximumBeauty(self, items: List[List[int]], requêtes: List[int]) -> Liste[int]:
# 1=1 trier par prix
items.sort(key=lambda x: x[0])

# 2-Construire les tableaux de préfixe max
prix, beautés = [], []
_b max = 0
pour le prix, beauté dans les articles:
max_b = max(max_b, beauté)
prix.annexe(prix)
beautés.append(max_b)

Réponse aux questions
res = []
pour q dans les requêtes :
idx = bisect_right (prix, q) - 1
res.append(beautés[idx] si idx >= 0 autre 0)
retour res
«» "

#### 7.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> maximumBeauté(vecteur<vecteur<int>>& items, vecteurs<int> et requêtes) {
Classer les articles par prix
tri(items.begin(), items.end(),
[](const auto& a, const auto& b){ retourner a[0] < b[0]; });

2/ Préfixe beauté max
int n = items.size();
vector<int> prix(n), bestBeauty(n);
ant curMax = 0;
pour (int i = 0; i < n; ++i) {
curMax = max(curMax, éléments[i][1]);
prix[i] = postes[i][0];
bestBeauty[i] = curMax;
}

Réponses aux questions
vecteur <int> ans;
as.reserve(queries.size());
pour (int q : requêtes) {
int idx = cap_bound(prices.begin(), prices.end(), q) - prices.begin() - 1;
ans.push_back(idx >= 0 ? bestBeauty[idx] : 0);
}
le retour des an;
}
};
«» "

---

- Oui. Ce que l'intervieweur veut vraiment

**Aspect**
C'est pas vrai.
*Simplicité*: tri + préfixe max + recherche binaire. La logique est claire, facile à tester, et fonctionne dans toutes les langues majeures. * Solution naïve* : O(n·q) avec deux boucles imbriquées est beaucoup trop lent pour 105. *Readability*: Évitez la suringénierie; gardez les noms variables intuitifs. Autres
**Le code Leet force parfois les limites de 1 seconde – une solution quadratique TLE. La surcomplication de l'implémentation de la recherche binaire peut causer des bogues (erreurs hors-par-un). Une mauvaise utilisation des ints 32 bits en C++ peut entraîner un débordement. Autres
**Ugly**= Mémoire de stockage de tableaux supplémentaires – mais toujours O(n). Une utilisation inutile de HashMap pour le prix→beauté au lieu de deux tableaux parallèles augmente les facteurs constants. Recalculer la beauté maximale pour chaque requête (inefficient). Autres

---

#### 9.

Comment le problème aide à le montrer
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Structures de données**Le tri + recherche binaire est un modèle classique. Dans votre explication, mentionnez «sorted‐array + prefix max». Autres
(n+q) log n) vs. O(n·q). Dans votre entrevue, indiquez les limites temps/espace et pourquoi elles sont acceptables. Autres
**Tests**=Cas de bord (duplicata, petits budgets). Écrire des tests d'unité dans votre demande ou les mentionner dans votre blog. Autres
**Communication**= Code clair et concis + commentaires.= Afficher votre code sur GitHub ou un blog; référez-le dans votre CV. Autres
**Savoir-faire en langues** Choisissez la langue la plus utilisée dans la société cible. Autres

---

Billet de blog (SEO-Ready)

> **Titre**: LeetCode 2070 – Plus bel article pour chaque requête – Java, Python & C++ Solutions
> **Meta Description**: Master LeetCode 2070 avec des solutions Java, Python et C++ efficaces. Apprenez l'algorithme, la complexité et les conseils d'entrevue pour stimuler votre préparation d'entrevue de codage.

```markdown
# Code de Leet 2070 – Plus beau article pour chaque requête

---

Déclaration du problème

Vous êtes donné un tableau `items` où chaque élément est `[prix, beauté]`, et un tableau `demandes`.
Pour chaque requête `q`, retourner la beauté maximale d'un article avec `prix <= q`.
Si aucun élément ne peut être fourni, retourner `0`.

---

Les contraintes

- `1 ≤ items.longueur, requêtes.longueur ≤ 105 "
- `1 ≤ prix, beauté, questions[i] ≤ 109 "
- Les articles peuvent partager le même prix ou la même beauté.

---

Intuition

Trier les articles par prix nous permet de les balayer une fois et de garder une beauté maximale.
Avec une table préfixe-maximum, nous pouvons répondre à chaque requête avec une recherche binaire dans `O(log n)`.

---

Algorithme

1. **Trésor** « items » par prix.
2. **Passer** le tableau trié, construire deux tableaux:
- `prix[]` – prix uniques, en hausse.
- "Meilleures Beautés" – beauté maximale vue à ce prix.
3. Pour chaque requête `q`, recherche binaire `prices[]` pour le plus grand `price ≤ q` et affiche la beauté correspondante.
Si aucune, sortie `0`.

---

Complexité

- **Heure**: 'O(n + q) log n) "
- **Espace**: "O(n)"

---

Cas de bord

Pourquoi réparer
C'est pas vrai.
Dupliquer les prix doivent garder le *maximum* beauté.
Demande < plus petit prix "0" Taux de recherche binaire `-1` → traiter comme `0`
Utiliser 64 bits (long'/long') Autres

---

Code (Java / Python / C++)

### Java

"Java
// coller dans votre éditeur LeetCode
solution de classe publique {
public int[] maximumBeauty(int[][] items, int[] requêtes) {
les tableaux.sort(items, Comparator.comparingInt(a -> a[0]);
int n = éléments.longueur;
prix int[] = nouveaux prix int[n];
int[] bestBeauties = nouveau int[n];
Int maxBeauty = 0;
pour (int i = 0; i < n; i++) {
maxBeauty = Math.max(maxBeauty, items[i][1]);
prix[i] = postes[i][0];
bestBeauties[i] = maxBeauty;
}
int[] ans = nouvelle int[queries.longueur];
pour (int i = 0; i < requêtes.longueur; i++) {
int q = requêtes[i];
int idx = upperBound(prix, q) - 1;
ans[i] = (idx >= 0) ? bestBeauties[idx] : 0;
}
le retour des an;
}
Int privé supérieurBound(int[] arr, int cible) {
int l = 0, r = longueur d'arrondi;
pendant que (l < r) {
Int m = (l + r) >>> 1;
si (arr[m] <= cible) l = m + 1;
autres r = m;
}
retour l;
}
}
«» "

Python

'`python
de bisect import bisect_right
de taper l'importation Liste

Solution de classe:
def maximumBeauty(self, items: List[List[int]], requêtes: List[int]) -> Liste[int]:
items.sort(key=lambda x: x[0])
prix, meilleur = [], []
_max = 0
pour p, b dans les rubriques:
cur_max = max(cur_max, b)
prix.annexe(p)
best.append(cur_max)
retourner [best[bisect_right(prices, q)-1] si bisect_right(prices, q) sinon 0 pour q dans les requêtes]
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> maximumBeauté(vecteur<vecteur<int>>& items, vecteurs<int> et requêtes) {
tri(items.degin(),items.end());
le meilleur des prix;
ant curMax = 0;
pour (auto& it : items) {
curMax = max(curMax, it[1]);
prix.push_back(it[0]);
best.push_back(curMax);
}
vecteur <int> ans;
as.reserve(queries.size());
pour (int q : requêtes) {
Int pos = upper_bound(prices.begin(), prices.end(), q) - prices.begin() - 1;
ans.push_back(pos >= 0 ? best[pos] : 0);
}
le retour des an;
}
};
«» "

---

Liste de vérification de l'entrevue

Actions
- Oui.
Master *sorting + préfixe max* pattern. Autres
Pratiquer la recherche binaire sur les tableaux Éviter les bugs hors-par-un. Autres
Valider les cas de bord sur LeetCode. Autres
Documentez votre solution sur un blog Les recruteurs aiment voir un code propre et lisible + explications. Autres
Partager sur LinkedIn/GitHub Accroître la visibilité. Autres

---

Prochaines étapes

- Clone cette repo: <https://github.com/votre-utilisateur/leetcode-2070>
- Suivez la liste de vérification de l'entrevue.
- Ajoutez d'autres harnais dans vos tests unitaires.

Bonne chance pour écraser **LeetCode 2070** et poser votre rôle de logiciel de rêve!

«» "

---

Clôture

Vous avez maintenant :

1. **Trois solutions polies** (Java, Python, C++) prêtes pour toute interview.
2. Un post **blog** qui met en évidence votre compréhension de l'algorithme, de la complexité et de la manipulation des cas de bord.
3. **Conseils d'entrevue** pour encadrer ce problème comme une vitrine de vos compétences en structure de données, en algorithme et en communication.

Bon codage et bonne chance avec votre prochaine interview – vous avez obtenu cela! Les

---

*Sentez-vous libre d'adapter les extraits de code et les explications à votre style personnel ou aux normes de codage de l'entreprise. *

---

*Tout le contenu ci-dessus est à des fins éducatives et peut être librement utilisé sur GitHub, blogs personnels, ou le matériel de préparation d'entrevue. *

---

**Fin du guide**
---
«» "

---

N'hésitez pas à copier le Markdown ci-dessus dans votre éditeur de blog (par exemple, Jekyll, Hugo, Medium) et à ajuster les méta tags en fonction de votre stratégie de référencement. Votre message devrait inclure des images du flux d'algorithme ou des diagrammes de cas de test pour stimuler davantage l'engagement. Bonne chance !