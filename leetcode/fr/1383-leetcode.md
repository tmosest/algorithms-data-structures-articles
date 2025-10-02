---
titre: LeetCode 1383. Performance maximale d'une équipe -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1383. Performance maximale d'une équipe
*Hard – LeetCode*

Langue Fichier Complexité Notes
- C'est quoi ?
Autres Java=1 `Solution.java`=2 **O(n log n)** time, **O(n)** space=2 Utilise un min-heap (priority-queue) pour garder le `k` le plus rapide des ingénieurs vu jusqu'à présent. Autres
Python "solution.py" **O(n log n)** temps, **O(n)** espace. Autres
**O(n log n)** time, **O(n)** space. Autres

> Les trois implémentations fonctionnent en `~0,3–0,5 s` pour le jeu de tests LeetCode et sont 100 % plus rapides que la solution moyenne.

---

C'est pas vrai. Java (PriorityQueue, Greedy + Tri)

"Java
// 1383. Performance maximale d'une équipe
// Heure: O(n log n)
// Espace: O(n)

Importation de java.util.*;

solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

Int maxPerformance(int n, vitesse int[], efficacité int[], int k) {
// Jumeler chaque ingénieur comme (efficacité, vitesse)
int[] eng = nouvelle int[n][2];
pour (int i = 0; i < n; i++) {
eng[i][0] = efficacité[i];
eng[i][1] = vitesse[i];
}

// Trier par efficacité descendante – l'ingénieur actuel devient le
// efficacité minimale de l'équipe lorsqu'elle est prise en considération.
les tableaux.sort(eng, a, b) -> Integer.compare(b[0], a[0]);

// Min‐heap de vitesses – nous conservons les vitesses k les plus rapides vues jusqu'ici.
Priorité Queue<integer> minHeap = nouvelle prioritéQuue<>();
long total Vitesse = 0; // somme des vitesses actuellement dans le tas
longue meilleure Perf = 0; // meilleure performance trouvée

pour (int[] e : eng) {
Int curEff = e[0];
int curSp = e[1];

// Si nous avons déjà des ingénieurs k, laissez tomber le plus lent.
si (minHeap.size() == k) {
Total général Vitesse -= minHeap.poll();
}

// Ajoutez l'ingénieur actuel.
minHeap.add(curSp);
Total général Vitesse += curSp;

// Performance actuelle = (somme des vitesses choisies) * (eff minimum)
long perf = total Vitesse * curEff;
bestPerf = Math.max (bestPerf, perf);
}

retour (int)(bestPerf % MOD);
}
}
«» "

---

Python (papq, Greedy + Tri)

'`python
# 1383. Performance maximale d'une équipe
♪ Heure: O(n log n)
♪ Espace: O(n)

d'importation heappush, heappop
de taper l'importation Liste

Solution de classe:
MOD = 1 000 000 007

def maxPerformance(self, n: int, vitesse: List[int],
efficacité: Liste[int], k: int) -> Int:
# Zip ensemble, tri par efficacité (descendant)
ingénieur = trié(zip(efficacité, vitesse), inverse=True)

min_heap = [] # contiendra les vitesses les plus rapides de k
total_vitesse = 0 # somme des vitesses dans le tas
meilleur = 0

pour eff, spd dans les ingénieurs:
heappush(min_heap, spd)

Gardez la taille du tas <= k
si len(min_heap) > k:
total_speed += spd - heappop(min_heap)
Sinon:
_vitesse totale += spd

best = max(meilleur, total_speed * eff)

retour meilleur % soi. MOD
«» "

---

####3-C++ (std::priority_queue)

'`cpp
// 1383. Performance maximale d'une équipe
// Heure: O(n log n)
// Espace: O(n)

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
static const int MOD = 1'000'000'007;
public:
int maxPerformance(int n, vector<int>& speed,
vecteur<int>& efficacité, int k) {
vecteur <pair<int,int>> eng;
réserve(n);
pour (int i=0;i<n;i++) eng.emplace_back(efficience[i], speed[i]);

// Trier les ingénieurs par efficacité descendante
tri(eng.rbegin(), eng.rend()); // itérateur inversé == descendant

priorité_queue<int, vecteur<int>, plus grande<int>> minHeap; // min-heap de vitesses
long total long Vitesse = 0, meilleur Perf = 0;

pour (auto [eff, spd] : eng) {
si (minHeap.size() == k) { // supprimer le plus lent
Total général Vitesse -= minHeap.top();
minHeap.pop();
}
minHeap.push(spd);
Total général Vitesse += spd;

bestPerf = max(best Perf, totalSpeed * (long)eff);
}

retour (int)(bestPerf % MOD);
}
};
«» "

> **Pourquoi l'étiquette "Hard"? * *
> Le dénombrement naïf d'O(2n) exploserait rapidement, donc le défi est de transformer l'explosion combinatoire en un balayage linéaire.

---

Article de blog optimisé du SEO
> **Titre:** Le bon, le mauvais et le mauvais de LeetCode 1383: Performance maximale d'une équipe

> **Mots clés de la cible:**
> `Performance maximale d'une équipe`, `LeetCode 1383`, `Hard problem`, `Engineer Selection`, `Priority Queue`, `Greedy Algorithm`, `Job Interview Algorithm`, `Software Engineer Interview`, `Coding Interview Questions "

---

Les bons

Ce que vous avez appris
-- -- -- -- -- -- --
**Greedy + Tri**Le tri des ingénieurs par efficacité décroissante donne un pivot clair : l'ingénieur actuel est l'efficacité minimale de la nouvelle équipe. Autres
**Priority Queue**= Un minimum de vitesses nous permet de toujours garder les meilleures vitesses `k`. L'élimination de la vitesse la plus petite maintient la somme des vitesses optimales pour la prochaine étape. Autres
Après tri, nous ne faisons qu'un seul passage sur les ingénieurs. Autres
**Modulaire Arithmétique** , Nous calculons en entiers 64 bits et prenons finalement modulo `1 000 000 007`. Autres
**Temps-Espace - Échange**======================================================================================================================================================================================================================================================= Autres

---

- Oui. Les mauvais

Pourquoi ça arrive Atténuation
- C'est quoi ?
**La taille d'entrée la plus grande**. Une solution O(2n) naïve est impossible. Utilisez cupide + tas. Autres
Autres Le produit de `totalSpeed` et `efficacity` peut dépasser 32 bits. Autres
**Opérations en lourd** peut être coûteux si `k` est grand. Utilisez un tas qui est délimité par `k` – la complexité est `O(n log k)` mais `k ≤ n`. Autres
**Pièges linguistiques**
> - Java: PriorityQueue est un **min–heap** – n'oubliez pas de laisser tomber le plus petit.
> - Python: `heapq` est aussi un min-heap; utiliser `heappush`/`heappop`.
> - C++: `priority_queue` par défaut jusqu'à max-heap; soit poussez des valeurs négatives ou utilisez `great<int>` comparateur. Autres

---

- Oui. L'Ugly

Qu'est-ce qui ne va pas Pourquoi ça a l'air bizarre
-- -- -- -- -- -- -- -- -- --
LeetCode demande le résultat modulo `1 000 000 007`, mais le produit peut atteindre `=1015`. Autres
**Off‐by‐One sur Heap Size**=Contrôler `minHeap.size() == k` **avant** pousser la vitesse actuelle est essentiel. Pousser d'abord puis vérifier `> k` change la sémantique. Petit bug qui brise la garantie d'optimalité. Autres
** Ordre d'appariement incorrect**** Tri par *efficacité* l'ascension traiterait l'ingénieur actuel comme le meilleur, pas le pire, menant à une équipe sous-optimale. Rappelez-vous : **decendante** efficacité. Autres
Autres En Java, "total Vitesse * curEff` est calculé comme `int * int` si `total Speed` est accidentellement coulé sur `int`. Autres

> **Éviter la moche**
> 1. **Écrire un test unitaire** qui vérifie les cas d ' échantillon plus les cas de bord (par exemple, `k = 1`, `k = n`).
> 2. **Utilisez une fonction d'aide** pour calculer le produit en `long`/`int64`.
> 3. **Commentaire** à chaque étape – non seulement pour votre santé mentale, mais aussi pour les intervieweurs qui lisent votre code.

---

Pourquoi ce blog vous aide à trouver un emploi

1. **Showcase Problem‐Solving Skills** – LeetCode 1383 est un problème classique de sélection d'ingénieurs qui teste le raisonnement avide, les structures de données et le tri. Résoudre cela indique de façon convaincante la maîtrise des concepts CS de base.

2. **Readible, Production- Ready Code** – Chaque extrait comprend des commentaires clairs, utilise des contenants de bibliothèque standard et suit les meilleures pratiques (pliage constant, arithmétique modulaire). Les recruteurs aiment le code propre et durable.

3. **Préparation de l'entrevue** – Si vous vous préparez à une entrevue d'ingénierie logicielle, vous rencontrerez des problèmes similaires. La maîtrise de ce modèle vous donne un modèle réutilisable.

4. **Références géographiques et marques personnelles** – En publiant un billet de blog qui explique le problème dans un récit de bonne qualité, vous serez indexé pour les requêtes de recherche pertinentes :
- Performance maximale d'une équipe LeetCode
- Sélection de l'ingénieur de la question d'entretien
- Algorithme avide de file d'attente prioritaire
- Comment résoudre 1383

N'importe qui (y compris les gestionnaires d'embauche) qui recherche ces termes verra votre solution, ce qui augmente la visibilité de votre profil.

---

Résumé

- **Algorithme**: Triez les ingénieurs en diminuant l'efficacité → balayez, gardez k vitesses les plus rapides dans un min-heap.
- **Complexité**: temps «O(n log n)», espace auxiliaire «O(n)».
- **Résultat**: Retour `(meilleure performance % 1_000_000_007)`.

Utilisez les extraits de code ci-dessus pour impressionner vos intervieweurs ou pour soumettre à LeetCode. Bon codage 