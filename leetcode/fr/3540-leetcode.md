---
titre: LeetCode 3540. Temps minimum pour visiter toutes les maisons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Description du problème – Temps minimum pour visiter toutes les maisons

> **LeetCode 3540 – Temps minimum pour visiter toutes les maisons* *
> **Difficulté:** Moyenne

Vous avez des maisons 'n ' disposées en cercle.
Pour chaque paire de maisons adjacentes, nous connaissons **deux** longueurs de route dirigées:

Direction Liste des bords
- C'est quoi ?
Dans le sens des aiguilles d'une montre (avant) Autres
Dans le sens contraire des aiguilles d'une montre (en arrière) Autres

Vous marchez à **1 m/s**. À partir de la maison `0`, vous devez visiter les maisons dans l'ordre exact donné par `queries`.
`queries[0]` n'est jamais `0` et pas deux requêtes consécutives ne sont les mêmes.

**Objectif** – retourner le minimum de temps pour terminer le voyage.

---

Intuition – Voie la plus courte sur un cycle pondéré

Sur un simple cercle chaque paire de sommets a **exactement deux** chemins simples:

1. **Clockwise** (avant) – somme des poids du bord avant le long du chemin.
2. **Dans le sens inverse des aiguilles d'une montre** (en arrière) – somme des poids du bord arrière en cours de route.

La distance la plus courte entre deux maisons est juste le minimum de ces deux sommes.
Ainsi le problème se réduit à:

«» "
total = 1 min(distance_horaire(cur, nxt),
distance_contre-horaire(cur, nxt) )
«» "

L'astuce est de calculer chaque distance en O(1). C'est là que brillent **les sommes préfixes**.

---

Solution de préfixe

- Oui. 1. Construire deux tableaux préfixes-sommes

Définition
- C'est quoi ?
"fwd[i]"" Distance totale vers l'avant de la maison `0` à la maison `i` (exclusive). "fwd[i+1] = fwd[i] + avant[i]" Autres
Total distance arrière de la maison `0` à la maison `i` (exclusif). `bwd[i+1] = bwd[i] + rétrograde[i]` Autres

Les deux tableaux ont la longueur `n+1`.
"fwd[n]" est toute la circonférence dans le sens des aiguilles d'une montre, `bwd[n]` toute la circonférence dans le sens des aiguilles d'une montre (ils sont égaux).

- Oui. 2. Distance entre deux maisons `u` → `v`

*Clockwise* (en avant):

«» "
i u <= v: cw = fwd[v] - Oui.
Autrement : cw = fwd[n] - (fwd[u] - fwd[v])
«» "

*Dans le sens inverse des aiguilles d'une montre* (en reculant):

«» "
i u >= v: ccw = bwd[u] - bwd[v]
sinon : ccw = bwd[n] - (bwd[v] - bwd[u])
«» "

Les deux formules sont O(1).

- Oui. 3. Éliminer les requêtes

Gardez un pointeur `cur` (à partir de 0).
Pour chaque maison suivante:

«» "
Total += min(cw(cur, q), ccw(cur, q)
cur = q
«» "

Retour `total` à la fin.

**Complexité* *

Opération Temps Espace
- C'est quoi ?
"O(n)" Autres
Traitement des requêtes
Total "O(n + q)" Autres

Les deux contraintes (`n, q ≤ 105`) sont facilement satisfaites.

---

Mise en œuvre du code

Ci-dessous vous trouverez des implémentations propres et idiomatiques dans **Java**, **Python** et **C++**.
Tous utilisent la même logique de préfixe-sum décrite ci-dessus.

---

### Java

"Java
Importation de java.util.*;

solution de classe {
public long minTotalTime(int[] en avant, int[] en arrière, int[] requêtes) {
int n = avant. longueur;
long[] fwd = nouveau long[n + 1];
long[] bwd = nouveau long[n + 1];

// Construire des montants préfixés
pour (int i = 0; i < n; i++) {
fwd[i + 1] = fwd[i] + avant[i];
bwd[i + 1] = bwd[i] + rétrograde[i];
}

long total = 0;
Int cur = 0;

pour (int q : requêtes) {
long cw = (cur <= q) ? fwd[q] - fwd[cur]
- (fwd[cur] - fwd[q]);

longue ccw = (cur >= q) ? bwd[cur] - bwd[q]
: bwd[n] - (bwd[q] - bwd[cur]);

total += Math.min(cw, ccw);
cur = q;
}
le total des retours;
}
}
«» "

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def minTotalTime(self, forward: List[int], backback: List[int], requêtes: List[int]) -> Int:
n = len(avant)

# Préfixer les sommes
fwd = [0] * (n + 1)
bwd = [0] * (n + 1)
pour i dans la plage(n):
fwd[i + 1] = fwd[i] + avant[i]
bwd[i + 1] = bwd[i] + rétrograde[i]

Total = 0
pour = 0

pour q dans les requêtes :
si cur <= q:
cw = fwd[q] - fwd[cur]
Sinon:
cw = fwd[n] - (fwd[cur] - fwd[q])

si cur >= q:
ccw = bwd[cur] - bwd[q]
Sinon:
ccw = bwd[n] - (bwd[q] - bwd[cur])

Total += min(cw, ccw)
cur = q

retour total
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue minTotalTime(vecteur<int>& vers l'avant, vecteur<int>& vers l'arrière,
vectorielle<int>&questions) {
int n = forward.size();

vecteur <long> fwd(n + 1, 0), bwd(n + 1, 0);
pour (int i = 0; i < n; ++i) {
fwd[i + 1] = fwd[i] + avant[i];
bwd[i + 1] = bwd[i] + rétrograde[i];
}

long total = 0;
Int cur = 0;

pour (int q : requêtes) {
long long cw = (cur <= q) ? fwd[q] - fwd[cur]
- (fwd[cur] - fwd[q]);

long ccw = (cur >= q) ? bwd[cur] - bwd[q]
: bwd[n] - (bwd[q] - bwd[cur]);

total += min(cw, ccw);
cur = q;
}
le total des retours;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de résoudre le LeetCode 3540

- Oui. 1. Le Bon – Pourquoi Ce problème est un gemme

* **Simplicité conceptuelle** – Une fois que vous réalisez que vous marchez juste sur un cycle pondéré, l'ensemble du puzzle s'effondre en prendre le plus court de deux sommes. (en milliers de dollars)
* **Réutilisabilité** – La technique du préfixe-somme est une agrafe pour tout problème de distance circulaire, de la planification de la route GPS à la minimisation de la latence réseau.
* **Performance évolutive** – temps O(n + q) et espace O(n) fonctionnent confortablement pour les 105 limites – pas besoin de structures de données exotiques ou d'algorithmes lourds.

- Oui. 2. Les mauvaises – choses qui peuvent vous faire trébucher

Pourquoi ça arrive ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Off‐by‐one dans les sommes préfixes**. de "fwd[i]". Autres
**Mixer les indices vers l'avant et vers l'arrière**=Le préfixe vers l'arrière doit utiliser `backward[i]` où `i` pointe vers la *cible* du bord arrière, et non vers la source. Utiliser la même indexation que le tableau avant; `bwd[i+1] = bwd[i] + arriéré[i]`. Autres
La soustraction directe échoue lorsque `u > v` ou `u < v`. Autres
**Débordement entier**= Distances jusqu'à 105, mais `n` peut aussi être 105 → somme maximale ~1010.= Utiliser des entiers 64 bits (`long` in Java, `long` in C++, `int` is safe in Python). Autres

- Oui. 3. L'Ugly – Cas de bord avancé & Gotchas

Que regarder Comment manipuler
- C'est quoi ?
**Quêtes avec l'enroulement dos à dos**. Autres
**Poids égaux en avant et en arrière** Les montants dans le sens des aiguilles d'une montre et dans le sens des aiguilles d'une montre peuvent différer considérablement. Toujours utiliser `min(cw, ccw)` – aucun contrôle supplémentaire nécessaire. Autres
**Grande taille de l'entrée**. Utiliser `BufferedReader` + `StringTokenizer` ou `FastScanner`. Autres
**Indicateurs négatifs potentiels**= Si vous utilisez accidentellement `backward[0]` pour le bord arrière de `0` à `n-1`. Notre construction utilise automatiquement `backward[0]` quand `i = n-1` dans la boucle. Autres

---

Conclusion optimisée – Débarquez votre prochain emploi

> **Vous voulez impressionner les gestionnaires d'embauche lors d'entrevues techniques? * *
> Maîtriser le leetCodes Le temps minimum pour visiter toutes les maisons montre plusieurs compétences de haute valeur:

1. ** Pensée algorithmique** – repérer la structure du cycle et réduire à deux sommes de chemin.
2. **La maîtrise préfixe** – une technique classique qui apparaît dans de nombreuses entrevues.
3. **Attention au détail du cas de bord** – manipulation de l'enveloppe, arithmétique 64 bits et consistance de l'index.
4. **Clean, language-agnostic code** – nous avons montré Java, Python, et C++ solutions pour une couverture maximale.

Inclure ce problème (et les extraits de code propres ci-dessus) dans votre portfolio ou GitHub. Ajoutez une brève explication de votre processus de pensée et de votre analyse de complexité. Les recruteurs verront instantanément que vous pouvez :

* Traduire un scénario réel en algorithme propre.
* Optimisez le temps et l'espace.
* Écrire un code robuste et prêt à la production en plusieurs langues.

Bonne chance – allez code! - Oui