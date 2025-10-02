---
titre: LeetCode 3645. Total maximal de l'ordonnance d'activation optimale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Problème : Total maximal de l'ordre d'activation optimal
**Code de cap 3645** – *Moyenne*
`public long maxTotal(int[] valeur, int[] limite)`

> **Objectif:** Activer les éléments dans un ordre qui maximise la somme des valeurs des éléments activés, en respectant la règle d'activation et la règle -autodestruction qui désactive les éléments lorsque le nombre actif atteint leur limite.

---

Rétablissement du problème

Autres Objet Qu'est-ce que c'est ?
- C'est quoi ?
La valeur obtenue par l'élément d'activation « i » = 1 ≤ valeur [i] ≤ 105
Le nombre d'éléments actuellement actifs ** strictement inférieur** à la « limite [i] » requise pour activer « i » , 1 ≤ limite [i] ≤ n ,
Règle d'activation Vous pouvez activer un élément seulement si le compte actif actuel `< limit[i]`. Autres
Après une activation, si le nombre actif devient `x`, **chaque élément** `j` avec `limit[j] ≤ x` est définitivement désactivé (même celui que vous venez d'activer). Autres

Tous les éléments commencent inactifs.
Vous pouvez activer au plus une fois par élément.
Retournez la valeur totale maximale que vous pouvez obtenir.

---

#### 2-

Lorsque le compte actif atteint finalement une valeur `L`, **chaque** élément avec `limit ≤L` disparaît.
Ainsi, pour une limite fixe `L`:

* Nous pouvons activer au maximum des éléments `L` dont la limite est égale à `L`.
* La meilleure stratégie consiste à choisir parmi ces éléments les valeurs "L" les plus élevées.

Pourquoi ?
Avant d'atteindre `active = L`, nous devons garder `active < L`.
Nous pouvons donc activer les éléments `L‐1` avec la limite `L` pendant que `active` reste `< L`.
Sur l'activation `L`, nous atteignons `active = L`; la valeur de l'élément activé est comptée, et *après* toutes les limites ≤ L disparaissent.

Ainsi, le total optimal est simplement la somme, sur chaque limite distincte `L`, des plus grandes valeurs `min(L, count(L)`.

---

Algorithme (gredi + seau)

1. **Bucket** toutes les valeurs par leur "limite".
`buckets[L] = { valeur[i] Limites
2. Pour chaque seau `L`:
* Trier ses valeurs **descendant**.
* Ajouter la somme des premières valeurs `min(L, seau.size()` à la réponse.
3. Retourne la somme accumulée.

#### Modèle d'exactitude

*Tout ordre d'activation peut être transformé en ordre gourmand sans diminuer le total:
- Pour un `L` fixe, vous pouvez activer au plus des éléments `L` avec cette limite.
- Oui. En prenant les plus grandes vous ne pouvez jamais blesser la somme.
- Parce que nous traitons les limites en ordre croissant, quand nous terminons avec la limite `L` toutes les limites inférieures sont déjà mortes, donc nous ne bloquons jamais un élément de limite supérieure.

D'où la stratégie de seau gourmand donne le total maximum.

---

Analyse de complexité

Opération Temps Mémoire
C'est quoi ?
Bouteilles de construction
Valeurs de tri à l'intérieur des seaux (valeurs totales = n)
Résumé
**O(n log n)**

---

Code – 3 langues

> Toutes les implémentations fonctionnent dans le même espace \(O(n\log n)\) et utilisent \(O(n)\).

---

Python 3

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxTotal(self, valeur: List[int], limite: List[int]) -> Int:
1. seau par limite
seaux = defaultdict(list)
pour v, l en zip(valeur, limite):
les seaux[l].append(v)

# 2. Avide
ans = 0
pour l, vals dans des seaux.items():
vals.sort(reverse=True) # descendant
as += somme(vals[:l]) # prendre au maximum les éléments l
retour et
«» "

> **Pourquoi `int` est très bien** – les entiers de Python sont débordés, donc pas de soucis de débordement.

---

Java

"Java
Importation de java.util.*;

solution de classe publique {
public long maxTotal(int[] valeur, int[] limite) {
int n = valeur. longueur;
Liste <Liste<entier>> seaux = nouvelle liste <>(n + 1);
pour (int i = 0; i <= n; i++) seaux.add(new ArrayList<>());

// 1. seau par limite
pour (int i = 0; i < n; i++) {
les seaux.get(limit[i]).add(value[i]);
}

long ans = 0L;
// 2. avide
pour (int l = 1; l <= n; l++) {
Liste <entier> liste = seaux.get(l);
si (list.isEmpty()) continue;
list.sort(Collections.reverseOrder());
prise int = Math.min(l, list.size());
pour (int i = 0; i < take; i++) {
as += list.get(i);
}
}
le retour des an;
}
}
«» "

> **Type de retour:** `long` (64-bit) – le problème garantit la somme correspond à un entier signé 64-bit.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long maxTotal(vecteur<int>& valeur, vecteur<int>& limite) {
int n = valeur.size();
les seaux vectoriels<vector<int>>(n + 1);

// 1. seau par limite
pour (int i = 0; i < n; ++i) {
les seaux[limit[i]].push_back(value[i]);
}

long an = 0;
// 2. avide
pour (int l = 1; l <= n; ++l) {
Auto &vec = seaux[l];
si (vec.vide()) se poursuit;
tri(vec.rbegin(), vec.rend()); // descendant
prise = min(l, (int)vec.size());
pour (int i = 0; i < prendre; ++i) {
le nombre d'heures de travail est égal au nombre d'heures de travail.
}
}
le retour des an;
}
};
«» "

> **Note:** Utilisez `long' pour la réponse pour éviter les débordements.

---

C'est vrai. Exemple travaillé

Valeur limite
- Oui.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
* * * * * *
C'est vrai.
C'est ce qu'on a dit.
- C'est pas vrai.

Boucles
- L = 1 → {10} → prendre 1 → 10
- L = 2 → {20,30} → prendre 2 → 50
- L = 3 → {15,5} → prendre 2 (depuis la taille du seau = 2 < L) → 20

**Total = 10 + 50 + 20 = 80** – la somme maximale possible.

---

- Oui. Quand ce code est-il *LeetCode‐Ready*?

- Oui.
- Oui.
Utiliser le temps "O(n log n)" (assez rapide pour tous les essais)
Comprend la manipulation des caisses de bord (seaux vides, grandes limites)

---

### # 7=" SEO‐Ready Blog – =Cracking LeetCode #3645 & Landing Your Dream Software‐Engineer Emploi

> **Meta‐Titre**: Code de cap 3645 – Total maximal de l'ordre d'activation optimal
> **Méta-Description**: Apprenez l'algorithme de seau gourmand pour LeetCode #3645, obtenez des extraits de code en Java, Python et C++, et découvrez comment aser ce problème d'interview pour votre prochain rôle d'ingénierie logicielle. (en milliers de dollars)

---

Pourquoi ce blog vous aide à être embauché

1. **Real‐world Problem‐Solving** – Les intervieweurs aiment les candidats qui peuvent réduire une règle complexe à une solution cupide propre.
2. **Maîtrise multi-langue** – Montrez que vous pouvez résoudre le même problème en Java, Python et C++ – la trinité *sainte* des interviews de codage.
3. **Complexité-Première pensée** – Nous présentons une solution O(n log n) claire qui s'élève au maximum des contraintes – quelque chose que les gestionnaires d'embauche recherchent.
4. **L'écriture claire, structurée** – Facile à lire, avec des blocs de code, des tableaux et des points de puce – démontre vos compétences en communication.
5. **SEO-optimisé** – En incluant des mots-clés comme *LeetCode*, *Maximum Total de Optimal Activation Order*, *Java*, *Python*, *C++*, *Entretien d'ingénieur logiciel*, vous augmentez la visibilité pour les recruteurs à la recherche de pratique d'entrevue.

---

TL; RD

Chaque limite `L` peut contribuer au maximum aux valeurs `L`.
- **Règle générale :** Choisissez le plus grand `min(L, count(L)` valeurs de chaque seau.
- **Complexité:** temps "O(n log n)", espace "O(n)".
- **Code:** Extraits prêts à copier dans **Java, Python et C++** ci-dessous.

---

Résumé du code

Python 3

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxTotal(self, valeur: List[int], limite: List[int]) -> Int:
seaux = defaultdict(list)
pour v, l en zip(valeur, limite):
les seaux[l].append(v)

Total = 0
pour l, vals dans des seaux.items():
vals.sort(reverse=True)
total += somme(vals[:l]) # prendre au maximum les valeurs l
retour total
«» "

---

- Oui. Java 8+

"Java
Importation de java.util.*;

solution de classe publique {
public long maxTotal(int[] valeur, int[] limite) {
int n = valeur. longueur;
Liste <Liste<entier>> seaux = nouvelle liste <>(n + 1);
pour (int i = 0; i <= n; i++) seaux.add(new ArrayList<>());

pour (int i = 0; i < n; i++) {
les seaux.get(limit[i]).add(value[i]);
}

long ans = 0;
pour (int l = 1; l <= n; l++) {
Liste <entier> liste = seaux.get(l);
si (list.isEmpty()) continue;
list.sort(Collections.reverseOrder());
prise int = Math.min(l, list.size());
pour (int i = 0; i < take; i++) {
as += list.get(i);
}
}
le retour des an;
}
}
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long maxTotal(vecteur<int>& valeur, vecteur<int>& limite) {
int n = valeur.size();
les seaux vectoriels<vector<int>>(n + 1);

pour (int i = 0; i < n; ++i)
les seaux[limit[i]].push_back(value[i]);

long an = 0;
pour (int l = 1; l <= n; ++l) {
Auto &vec = seaux[l];
si (vec.vide()) se poursuit;
tri(vec.rbegin(), vec.rend()); // descendant
prise = min(l, (int)vec.size());
pour (int i = 0; i < prendre; ++i)
le nombre d'heures de travail est égal au nombre d'heures de travail.
}
le retour des an;
}
};
«» "

---

À emporter

- **Problème** → *Greedy + Seautage*
- **Solution** → *Trier chaque seau, choisir les valeurs "L` supérieures*
- **Pourquoi ça marche** → *Ligne supérieure des activations `L` par limite; prendre les plus grandes ne fait jamais mal*

Montrez cette approche lors de votre prochaine entrevue – elle démontre un raisonnement clair, une preuve d'optimalité et la résolution de problèmes linguistiques.

Bonne chance, et le codage heureux! C'est ce qu'il a dit