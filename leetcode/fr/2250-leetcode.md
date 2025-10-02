---
titre: LeetCode 2250. Nombre de rectangles contenant chaque point - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2250. Nombre de rectangles contenant chaque point – LeetCode Deep‐Dive
*(Java-Python C++) – Un billet de blog favorable à l'emploi

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [La solution naïve et pourquoi elle fait défaut] (#la solution naïve)
3. [Observation clé] (#observation clé)
4. [Algorithme optimal] (#algorithme optimal)
5. [Analyse de la complexité] (#analyse de la complexité)
6. [Calendrier des cas d'urgence](#Calendrier des cas d'urgence)
7. [Applications complètes] (#mises en œuvre)
* Java
* Python
* C++
8. [Test de la solution] (#test)
9. [Interview-Ready Tips](#interview-tips)
10. [Résumé du référencement](#seo-summary)

---

- Oui. Aperçu du problème <a name="problem-overview"></a>

Vous recevez:
- `rectangles`: `[[l1,h1], [l2,h2], ...]` – chaque rectangle commence par `(0,0)` et se termine à `(li, salut)`.
- `points`: `[[x1,y1], [x2,y2], ...]` – un ensemble de points de requête.

Retourner un tableau `count` où `count[j]` est le nombre de rectangles qui **contient** point `(xj, yj)`.
Les points sur le bord du rectangle sont considérés à l'intérieur.

**Contrôles* *

Valeur du paramètre
C'est quoi ?
"longueur de l ' ancre", "longueur de l ' ancre" 1 ... 5 × 104
"1 ≤ li, xj ≤ 109"
"1 ≤ hi, yj ≤ 100"
Autres Tous les rectangles / points sont uniques.

Parce que la hauteur* est plafonnée à 100, nous pouvons l'exploiter pour obtenir une solution efficace.

---

La solution naïve et pourquoi elle fait défaut <un nom></a>

Une double boucle droite:

Texte
pour chaque point (x, y):
pour chaque rectangle (l, h):
si x <= l et y <= h: count++
«» "

*Temps*: O(P · R) 2.5 × 109 opérations → **Temps-out**.
*Espace*: O(1).

Nous avons besoin d'une approche plus intelligente qui réduit le nombre de contrôles rectangle par point.

---

Remarque clé <un nom d'observation clé></a>

- **Hauteur (h) ≤ 100** – une petite portée fixe.
- Pour une hauteur fixe «h», seuls les rectangles avec cette hauteur exacte (ou plus) peuvent contenir un point avec «y ≤ h».
- Si on regroupe les longueurs rectangles (`l`) par hauteur, chaque groupe peut être trié une fois.
- Pour un point de requête `(x, y)`, nous n'avons besoin de regarder que les groupes avec la hauteur `h` où `h ≥ y`.

Ainsi, nous transformons un problème de confinement 2-D en une recherche **1-D** dans au plus 100 listes triées.

---

Algorithme optimal <un nom="algorithme optimal"></a>

1. **Coupe par hauteur* *
- Créer un tableau `buckets[101]` (`0` inutilisé).
- Pour chaque rectangle `(l, h)`, pousser `l` dans `buckets[h]`.

2. **Trier chaque seau**
- Pour chaque hauteur `h` qui a rectangles, trier la liste des longueurs ascendantes.

3. **Réponse aux questions**
Pour chaque point `(x, y)`:
Texte
Total = 0
pour h en [y, 100]:
si les seaux[h] ne sont pas vides:
// recherche binaire pour trouver la première l >= x
idx = link_bound(buckets[h], x)
Total += (lentilles[h]) - idx)
count.append(total)
«» "

La recherche binaire garantit O(log k) par seau, où *k* est le nombre de rectangles de cette hauteur.
Parce que la boucle externe itère au plus 100 fois, le travail total par requête est limité.

---

Analyse de complexité <un nom=analyse de complexité></a>

Étape Temps Espace
C'est pas vrai.
Bâtiment de seau
Tri des seaux **O(R log R)** (somme sur tous les seaux)
Autres Traitement des demandes de renseignements **O(P · H · log R)** avec H = 100 –
Total **O(R log R + P · H · log R)**

Avec `R, P ≤ 5 × 104` et `H = 100`, cela s'inscrit facilement dans les limites (~5 × 106 opérations).

---

C'est pas vrai. Liste de vérification des cas <un nom> Liste de vérification des cas de référence></a>

1. **Points avec y > 100** – aucun rectangle ne peut les contenir; le résultat est 0.
2. **Seaux vides** – sautez rapidement (pas de recherche binaire).
3. **Très grand `l` (= 109)** – s'inscrit dans l'int signée 32 bits; pas de débordement.
4. **Des rectangles multiples de même hauteur** – traités par tri.
5. **Point sur le bord** – `x <= l` et `y <= h` inclusive; la recherche binaire lower_bound les compte correctement.

---

Nombre de mises en oeuvre complètes <un nom></a>

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Les trois suivent les mêmes étapes algorithmiques et utilisent des idiomes spécifiques au langage.

- Oui. 1. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
Int[] countRectangles(int[][] rectangles, int[][] points) {
// longueurs du godet par hauteur (1..100)
Liste <entier>[] seaux = nouvelle liste d'array[101];
pour (int h = 0; h <= 100; h++) seaux[h] = nouvelle liste de distribution<>();

pour (int[] rect : rectangles) {
int l = rect[0], h = rect[1];
les seaux[h].add(l);
}

// trier chaque seau
pour (Liste<entier> seau : seau) {
si (!bucket.isEmpty()) Collections.sort(bucket);
}

int[] ans = nouvelle int[points.longueur];
pour (int i = 0; i < points. longueur; i++) {
int x = points[i][0];
int y = points[i][1];

si (y > 100) { // aucun rectangle ne peut contenir ce point
as[i] = 0;
poursuivre;
}

= 0;
pour (int h = y; h <= 100; h++) {
Liste <entier> seau = seau[h];
si [bucket.isEmpty()] continue;

// Recherche binaire : premier indice avec l >= x
int idx = inférieur Bound(bucket, x);
Total += seau.size() - idx;
}
ans[i] = total;
}
le retour des an;
}

// l'implémentation classique lower_bound
int privé lowerBound(Liste<Integer> liste, int cible) {
int lo = 0, hi = list.size(); // hi est exclusif
pendant qu ' il y a (l < bonjour) {
Int milieu = lo + (h - lo) / 2;
si (list.get(mid) < cible) {
lo = milieu + 1;
} autre {
hi = milieu;
}
}
retour lo;
}
}
«» "

---

- Oui. 2. Python 3

'`python
de bisect importer bisect_left
de collections importer par défautdict

Solution de classe:
def countRectangles (soi, rectangles, points):
# longueurs de seau par hauteur
seaux = defaultdict(list)
pour l, h en rectangles:
seaux[h].append(l)

# Trier chaque seau
pour h dans les seaux:
les seaux[h].sort()

ans = []
pour x, y en points:
si y > 100: # aucun rectangle ne peut contenir ce point
ans.append(0)
poursuivre

Total = 0
pour h dans la plage (y, 101):
Si h n'est pas dans les seaux:
poursuivre
lst = seaux[h]
idx = bisect_left(lst, x) # first l >= x
Total += len(lst) - idx
(total)

retour et
«» "

---

- Oui. 3. C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> countRectangles(vecteur<vecteur<int>>& rectangles,
vecteur<vecteur<int>&points) {
// longueurs du godet par hauteur (1..100)
vectoriel<vector<int>> seaux(101);
pour (auto &rect : rectangles) {
int l = rect[0], h = rect[1];
les seaux[h].push_back(l);
}

// trier chaque seau
pour (auto & bucket : seaux)
tri(bucket.begin(), seau.end());

vecteur <int> ans;
pour (auto &pt : points) {
int x = pt[0], y = pt[1];
si (y > 100) { // impossible
ans.push_back(0);
poursuivre;
}

= 0;
pour (int h = y; h <= 100; ++h) {
Const auto &bucket = seaux[h];
si [bucket.vide()] continue;

// lien _inférieur: premier indice avec l >= x
auto it = lower_bound(bucket.begin(), seau.end(), x);
total += seau.end() - il;
}
ans.push_back(total);
}
le retour des an;
}
};
«» "

---

> **Pourquoi ceux-ci sont prêts pour l'entrevue* *
> * Séparation claire des préoccupations (bucket → trier → requête).
> * Chaque solution utilise les opérations de structure de données les plus rapides disponibles: `Collections.sort`, `bisect_left`, `std::sort`.
> * Évite les frais généraux inutiles (par exemple, création `ArrayList` par seau seulement une fois).

---

## ☐ Tester la solution <un nom="test"></a>

'`python
# test d'échantillon en Python
sol = Solution()
rectangles = [[4,4],[5,5],[5,4]
points = [[3,3],[5,5],[5,1],[2,6]]
print(sol.countRectangles(rectangles, points))
# → [2, 1, 2, 0]
«» "

**Échantillons de cas* *

Contribution attendue
C'est pas vrai.
Récipients = `[10, 10]`, points = `[10,10]`
Rectangles = `[[1,1], [2,2]`, points = `[[5,5]]` "0"
Rectangles = `[1000000000,100]`, points = `[[1,100]]`
Rectangles = `[[3,10]]`, points = `[[4,9]]`

Exécutez les trois implémentations contre le même générateur de test aléatoire pour confirmer la parité.

---

Conseils pour la préparation de l'entrevue <un nom></a>

Conseil Pourquoi c'est important
-- -- -- -- --
**Déclarer l'observation principale** – Hauteur ≤ 100 – gagne tôt des points. Montre que vous pouvez repérer des contraintes qui simplifient le problème. Autres
Autres ** État du temps et de la complexité spatiale** avant de plonger dans le code. Les intervieweurs aiment une analyse de complexité concise. Autres
**Utilisez des helpers de recherche binaire intégrés** (`bisect_left`, `std::lower_bound`, `Collections.binarySearch`). Gagne du temps, réduit les bugs. Autres
**Check corner cas** (`y > 100`, seaux vides) *avant* effectuer des travaux lourds. Prévient les contrôles inutiles O(1). Autres
**Proof d'exactitude**: Afficher que le nombre de rectangles est moins élevé avec `l >= x` *and* `h >= y`. Autres
**Mention la limite fixe de 100 hauteur** comme arme secrète. Ça fait ressortir votre solution. Autres
Autres **Parlez de la façon dont vous avez géré des contraintes plus grandes** (par exemple, si `h` n'étaient pas plafonnés). Montre l'adaptabilité. Autres
Autres **Nettoyez le code** – évitez les micro-optimisations qui nuisent à la lisibilité. Valeur du code à conserver par les intervieweurs. Autres

---

## OBJECTIF-Résumé amical <un nom="seo-summary"></a>

- **Question d'entrevue de LeetCode** – *Nombre de Rectangles contenant chaque point*
- **Langues**: Java, Python, C++
- **Algorithme optimal** : seau par hauteur (= 100), longueurs de tri, recherche binaire par requête.
- **Complexité temporelle**: O(R log R + P · 100 · log R) – bien en dessous de 5 × 106 ops pour les limites de LeetCode.
- **Complexité spatiale**: O(R).
- **Pourquoi c'est un grand problème d'interview** : mise en évidence de la capacité d'exploiter les contraintes, d'utiliser la recherche binaire et de raisonner sur la géométrie 2-D avec des structures de données 1-D.

> **Prêt à passer votre prochaine entrevue sur la structure des données? * *
> Maîtrisez l'astuce de seau et préparez-vous à expliquer *pourquoi* une liaison de 100 hauteur est un changement de jeu.

Bon codage, et bonne chance pour ce travail ! C'est ce qu'il a dit.

---

> **Mots clés**: LeetCode, nombre de rectangles contenant chaque point, question d'entrevue, Java, Python, C++, Algorithme, recherche binaire, complexité temporelle, complexité spatiale, structures de données, conseils d'entrevue de travail.

---