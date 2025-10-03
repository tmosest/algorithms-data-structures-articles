---
titre: LeetCode 1788. Maximiser la beauté du jardin -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1788. Maximisez la beauté du jardin
**Hard – Code de Leet**

---

## Titre du blog
* Maximiser la beauté du jardin – 1788 LeetCode : une solution 3 langues (Java, Python, C++)* *

> **SEO Mots-clés** – LeetCode 1788, Maximiser la beauté du jardin, problème de jardin, préfixe somme, programmation dynamique, entretien de codage, solution Java, solution Python, solution C++, défi de codage d'entretien d'emploi

---

- Oui. 1. Aperçu du problème

On vous donne un tableau `fleurs` de longueur `n` (`2 ≤ n ≤ 105`).
Chaque élément est la valeur beauté d'une fleur et peut être négatif.
Vous pouvez supprimer n'importe quel nombre de fleurs (dont aucune).
Après les suppressions, vous devez avoir un **jardin valide**:

1. Il reste au moins deux fleurs.
2. La première et la dernière fleur dans la séquence restante ont la même valeur de beauté**.

La beauté d'un jardin est la somme de toutes les fleurs restantes.
Retournez la beauté **maximum** possible de tout jardin valide.

---

- Oui. 2. Intuition – La première et dernière matière

Seul le premier et le dernier élément de la subséquence choisie influencent la faisabilité du jardin.
Tout entre les deux peut être conservé ou enlevé librement.

*Si on garde une fleur positive entre les deux extrémités égales, on gagne de la valeur; si elle est négative, on peut la laisser tomber sans blesser la beauté. *

La stratégie optimale est donc :

1. Choisissez une valeur `v`.
2. Gardez le **premier** événement de "v" comme l'extrémité gauche.
3. Gardez l'événement **dernier** de `v` comme fin droite.
4. Gardez chaque fleur positive strictement entre ces deux positions.

Cela donne la beauté maximale pour cette valeur particulière "v".
Nous devons essayer chaque valeur distincte et prendre le meilleur résultat.

---

- Oui. 3. Algorithme (temps O(n), espace O(n))

Étape
- C'est quoi ?
Autres **1**=Scan `flowers` une fois pour enregistrer pour chaque valeur son premier et dernier indice. Autres
Autres **2**= Calculer un tableau préfixe `pref[i]` = somme des fleurs **positives** jusqu'à l'index `i` (inclus). Autres
Autres Pour chaque valeur qui apparaît au moins deux fois ("dernier > premier"):
`beauty = 2 * v + (pref[last-1] - pref[first])` Autres
Autres **4**= Gardez le maximum de toutes ces beautés. Autres

*Pourquoi la formule fonctionne*
`pref[last-1] - pref[first]` équivaut à la somme des fleurs positives strictement entre les deux occurrences.
L'ajout de `2 * v` rend compte des deux fleurs de fin égale.
Les fleurs négatives dans l'intervalle sont tout simplement ignorées.

---

- Oui. 4. Cas de bord

Explication
- C'est quoi ?
Autres **Une seule occurrence d'une valeur**= Ne peut pas former un jardin valide → skip. Autres
**Toutes les fleurs doivent toujours garder deux négatifs égaux. La formule gère cela parce que la somme préfixe entre eux est 0. Autres
Le meilleur jardin est l'ensemble (le premier et le dernier sont la même valeur, généralement le maximum). Autres

---

- Oui. 5. Mise en œuvre du code

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.
Tous les trois utilisent la même logique O(n) et gèrent les limites entières 32 bits en toute sécurité en utilisant `long`/`long long` pour les sommes.

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe {
Int maximum publicBeauty(int[] fleurs) {
int n = fleurs. longueur;

// 1. Enregistrer la première et la dernière occurrence de chaque valeur
Carte <entier, entier> d'abord = nouveau HashMap<>();
Carte<entier,entier>dernière = nouveau HashMap<>();
pour (int i = 0; i < n; i++) {
int v = fleurs[i];
si (!first.contientKey(v)) first.put(v, i);
last.put(v, i); // conserve le dernier index
}

// 2. Préfixer la somme des valeurs positives
long[] pref = nouveau long[n];
pref[0] = Math.max(0, fleurs[0]);
pour (int i = 1; i < n; i++) {
pref[i] = pref[i - 1] + Math.max(0, fleurs[i]);
}

long best = Long.MIN_VALUE;

// 3. Essayez chaque valeur qui se produit au moins deux fois
pour (int v : first.keySet()) {
int l = premier.get(v);
int r = last.get(v);
si (l == r) continuer; // avoir besoin d'au moins deux fleurs

long milieu = pref[r - 1] - pref[l]; // positif entre l et r
long candidat = 2L * v + milieu;
meilleur = Math.max (meilleur candidat);
}

return (int) best; // result correspond à int par des contraintes de problème
}
}
«» "

5.2 Python

'`python
de taper l'importation Liste
de collections importer par défautdict

Solution de classe:
def maximumBeauté(même, fleurs: Liste[int]) -> Int:
n = len(fleurs)

# premier et dernier indices
premier = {}
Dernier = {}
pour i, v dans l'énumération:
si v n'est pas en premier:
premier[v] = i
last[v] = i

# Préfixer la somme des positifs
pref = [0] * n
pref[0] = max(0, fleurs[0])
pour i dans la plage (1, n):
pref[i] = pref[i - 1] + max(0, fleurs[i])

meilleure = flotteur('-inf')

pour v en premier:
l, r = premier[v], dernier[v]
si l == r:
poursuivre
milieu = pref[r - 1] - pref[l]
candidat = 2 * v + milieu
best = max (meilleur candidat)

le meilleur retour
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximumBeauté(vecteur<int>& fleurs) {
int n = fleurs.taille();

unordered_map<int, int> premier, dernier;
pour (int i = 0; i < n; ++i) {
int v = fleurs[i];
si (!first.count(v)) first[v] = i; // première occurrence
dernière[v] = i; // dernière (dernière) occurrence
}

vecteur <long> pref(n);
préf[0] = max(0LL, fleurs[0]);
pour (int i = 1; i < n; ++i) {
pref[i] = pref[i-1] + max(0LL, fleurs[i]);
}

longue longue meilleure = LLONG_MIN;

pour (const auto &kv : first) {
int v = kv.first;
int l = kv.seconde;
int r = last[v];
si (l == r) continuer; // besoin de deux fleurs

long moyen long = pref[r-1] - pref[l];
long cand = 2LL * v + milieu;
best = max (meilleur, cand);
}

retourner static_cast<int>(meilleur);
}
};
«» "

Les trois codes fonctionnent dans le temps ** linéaire** ('O(n)') et utilisent l'espace auxiliaire ** linéaire** ('O(n)').

---

- Oui. 6. Analyse de la complexité

Métrique
- C'est quoi ?
**Heure** Autres
**L'espace**="O(n)" (deux cartes + tableau préfixe)="O(n)=" Autres
**Pourquoi c'est acceptable**= `n ≤ 105`, `="fleurs[i]=" ≤ 104` → sommes ≤ 109, en toute sécurité en entier signé 32 bits. Autres

---

- Oui. 7. Bonne, mauvaise, et lugubre de la solution

Aspect du bien
- C'est quoi ?
**Bien**. • Pass unique, pas de récursion. <br>• Poigne avec élégance les valeurs négatives. <br>• Utilise uniquement des conteneurs intégrés → rapides et efficaces en mémoire. Autres
**Bad**) • Nécessite la numérisation du tableau deux fois (une fois pour les indices, une fois pour le préfixe). <br>• Il faut deux cartes de hachage – un peu plus de mémoire que nécessaire. Autres
• Quelques solutions naïves (p. ex., "pick any two egal end and sum everything") ajoutent accidentellement des nombres négatifs au milieu, donnant des résultats sous-optimaux. <br>• Les approches de PDD récursives qui tentent d'évaluer chaque subséquence explosent en temps exponentiel à cette échelle. Autres

---

- Oui. 8. Autres approches et pourquoi nous les évitons

1. ** Force brute (O(n2))** – Énumérer chaque paire de valeurs égales et résumer les positifs entre. Trop lent pour `n = 105`.
2. ** Programmation dynamique (DP)** – Le problème est *pas* un DP classique (il n'y a pas de structure de sous-problèmes qui se chevauchent) – utiliser DP ne ferait qu'ajouter une complexité inutile.
3. **Segment Tree / Binary Indexed Tree** – Overkill; préfixe des sommes donnent déjà des requêtes à intervalle de temps constant.

Ainsi, le préfixe-sum + premier/dernier tour est le bon endroit.

---

- Oui. 9. Comment expliquer Ceci pour les intervieweurs

> **Quand on vous demande comment résoudre LeetCode 1788 ?
>
J'ai d'abord remarqué que seuls les premiers et derniers éléments comptent. J'ai enregistré pour chaque valeur beauté le premier et dernier indice. J'ai ensuite construit une somme préfixe de fleurs seulement positives, ce qui me permet de calculer la meilleure somme entre deux extrémités égales en O(1). Enfin, j' itérer sur toutes les valeurs qui se produisent au moins deux fois et de garder le maximum. L'algorithme est O(n) et utilise l'espace supplémentaire O(n) – parfait pour 105 éléments.

Cette explication concise montre que vous pouvez **abstraire le problème**, repérer un **pattern**, et appliquer une technique **clean O(n)** – exactement ce que les intervieweurs recherchent.

---

- Oui. 10. Réflexions finales – Votre prochaine entrevue

- **Pratique**: Implémentez cette solution dans votre langue préférée à partir de zéro.
- **Timing**: Lancez-le contre 105 cas aléatoires pour vous convaincre de sa linéarité.
- **Expliquer**: Soyez prêt à discuter de l'astuce "préfixe" – c'est l'idée clé.

Maîtriser ce problème vous donne un modèle puissant: Quand seules les conditions limites comptent, gardez les extrêmes et incluez avec cupidité des positifs à l'intérieur.
Appliquez-le à des problèmes de subséquence similaires que vous rencontrerez dans des entretiens réels.

---

À emporter

- **LeetCode 1788** est solvable en *temps linéaire* en utilisant *préfixe des sommes*.
- Oui. La même logique se traduit par **Java, Python et C++** avec un minimum d'effort.
- Comprendre l'intuition derrière la première et la dernière solution vous permet d'expliquer couramment la solution dans un entretien de codage, en renforçant votre confiance et votre score.

Bon codage, et que votre jardin d'entretien d'emploi soit toujours *beau*!