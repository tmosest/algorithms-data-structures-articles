---
titre: LeetCode 2386. Trouvez le K-Sum d'un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Récapitulation des problèmes
**LeetCode 2386 – Trouvez le K‐Sum d'un tableau* *

> *Avec un tableau entier `nums` et un entier `k` positif, vous pouvez choisir n'importe quelle séquence du tableau et résumer tous ses éléments.
> Le **K-Sum** est la somme de **k-th la plus importante des sous-séquences** (les sommes de suite sont **non** requises pour être distinctes).
> Retournez le K‐Sum du tableau. *

* subséquence* = conserver l'ordre original, supprimer zéro ou plus d'éléments.
La séquence résiduelle vide compte et a une somme de « 0 ».
«1 ≤ n ≤ 105», «-109 ≤ nums[i] ≤ 109», «1 ≤ k ≤ min(2000, 2n)».

---

- Oui. 2. Principales perspectives

Laissez

«» "
P = somme de tous les éléments positifs en nombres
«» "

Si nous **flip** chaque élément à sa valeur absolue, le tableau devient non-négatif.
Pour un tableau non négatif, il est facile de générer la somme de sous-séquence **k‐th la plus petite** à l'aide d'une somme minimale (problème classique de la somme de sous-séquence de la somme de la plus petite valeur de KK).

Pourquoi ça aide ?

* La plus grande somme subséquemment du tableau original est `P` – prenez juste chaque élément positif.
* Chaque sous-séquence du tableau original peut être représentée comme suit :
`P – (somme des éléments que nous *excluons* de P)'.
L'exclusion des éléments est équivalente à l'ajout des valeurs absolues correspondantes à un tableau non négatif.
* Par conséquent, la somme **k‐th la plus importante** du tableau original est
`P – (k‐th plus petite somme subséquemment du tableau de valeurs absolues)».

Ainsi, le problème se réduit à : **trouver la plus petite somme de sous-séquence k d'un tableau non négatif**.

---

- Oui. 3. Algorithme (Heap + Trick à deux points)

1. **Pré-processus**
* `P` ← somme des nombres positifs.
* `abs[i] =="nums[i]=".
* Trier les « abs » de plus en plus.

2. **Min-heap**
Chaque magasin d'éléments en tas
* `sum` – la somme subséquemment actuelle.
* `idx` – l'indice du dernier élément inclus dans cette somme.
Le tas est commandé par "sum" (ascendant).

*Démarrer* avec `(abs[0], 0)` – la plus petite somme non vide possible.

3. **Générer k-th plus petit* *
Répéter "k-1" fois:
* Pop la plus petite paire `(sum, idx)` → `cur`.
* Les deux candidats suivants qui peuvent être dérivés de "cur" sont:

* ** À l ' exclusion** du dernier élément : `cur.sum - abs[idx]` (ceci est déjà représenté par `cur` après la première pop, donc nous le gardons juste pour la prochaine étape).
* **Inclure** l'élément suivant: `cur.sum - abs[idx] + abs[idx+1]`.
* Poussez les deux dans le tas (si `idx+1 < n`).
* Gardez le dernier `cur.sum` poppé – ce sera la k‐th plus petite somme après la fin de la boucle.

4. **Réponse**
«ans = P - cur.sum».

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Trier "O(n log n)" "O(1)" Autres
Opérations lourdes Autres

Avec `k ≤ 2000`, l'algorithme répond facilement aux limites même pour `n = 105`.

---

- Oui. 4. Mise en œuvre du code

#### 4.1 Java

"Java
Importer java.util. Les tableaux;
Importer java.util. Comparateur;
Importer java.util. Priorité Demande;

solution de classe publique {
public long kSum(int[] nums, int k) {
long possum = 0;
int n = longueur nums;
int[] abs = nouveau int[n];
pour (int i = 0; i < n; i++) {
si (nombres[i] > 0) PosSum += nombres[i];
abs[i] = Math.abs(nums[i]);
}
Tableau.sort(abs); // O(n log n)

// Élément de masse: [somme actuelle, dernier indice]
PrioritéQueue<long[]> pq = nouvelle PrioritéQueue<>(Comparator.comparingLong(o -> o[0])
pq.offre(nouvelle longue[]{abs[0], 0});

long curSum = 0;
pour (int t = 0; t < k; t++) {
long[] cur = pq.poll(); // O(log k)
curSum = cur[0];
int idx = (int) cur[1];
si (idx + 1 < n) {
// inclure l'élément suivant
longue inclus = curSum - abs[idx] + abs[idx + 1];
// exclure l'élément courant (il suffit de garder cur)
pq.offre(nouvelle longue[]{include, idx + 1});
pq.offre(cur);
}
}
retour PosSum - curSum; // réponse finale
}
}
«» "

4.2 Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def kSum(self, nombres: List[int], k: int) -> Int:
pos_sum = somme(x pour x en nombres si x > 0)
abs_vals = trié(abs(x) pour x en nombres)

# élément de masse : (current_sum, last_index)
[(abs_vals[0], 0)]
cur_sum = 0

pour _ dans la plage(k):
cur_sum, idx = heapq.heappop(heap)
si idx + 1 < len(abs_vals):
include = cur_sum - abs_vals[idx] + abs_vals[idx + 1]
heapq.heappush(heap, (inclus, idx + 1))
heapq.heappush(heap, (cur_sum, idx))

retour de pos_sum - cur_sum
«» "

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long long kSum(vector<int>& nums, int k) {
long et long pos Somme = 0;
int n = nombres.size();
vecteur <long> absVals(n);
pour (int i = 0; i < n; ++i) {
si (nombres[i] > 0) PosSum += nombres[i];
absVals[i] = llabs(nums[i]);
}
tri(absVals.begin(), absVals.end()); // O(n log n)

// min-heap de paires {current_sum, last_index}
en utilisant P = paire <long long, int>;
priorité_queue<P, vecteur<P>, plus grande<P>> pq;
pq.emplace(absVals[0], 0);

long curSum = 0;
pour (int step = 0; pas < k; + + step) {
auto [sum, idx] = pq.top(); pq.pop();
curSum = somme;
si (idx + 1 < n) {
longueur longue inclus = somme - absVals[idx] + absVals[idx + 1];
pq.emplace(include, idx + 1);
pq.emplace(sum, idx);
}
}
retour du sommum - curSum;
}
};
«» "

---

- Oui. 5. Article de blog (optimisé par le SEO)

> **Titre**
> _LeetCode 2386 – Trouvez le K‐Sum d'un tableau: Java / Python / C++ Solutions & Insightful Guide_

> **Description détaillée**
> Master LeetCode 2386 avec des solutions Java, Python et C++ claires. Apprenez l'algorithme basé sur le tas, l'analyse de l'espace temporel et des conseils pratiques pour surmonter ce difficile problème dans les entrevues.

> **Mots clés**
> LeetCode 2386, K‐Sum, somme de subséquence, algorithme de tas, solution Java, solution Python, solution C++, préparation d'entretien, analyse d'algorithme

---

Introduction

LeetCodes **2386 – Trouver le K-Sum d'un tableau** est un problème *hard* qui teste votre compréhension des subséquences, des tas et des astuces de réduction. Si vous vous préparez à des entretiens techniques, la résolution de ce problème mettra en évidence votre capacité à manipuler des sommes, à utiliser des files d'attente prioritaires et à penser en dehors de la boîte.

Dans cet article, nous passons par:

1. La perspicacité mathématique qui transforme une question plus importante en question plus petite.
2. Un algorithme basé sur un tas qui fonctionne dans **O(n log n + k log k)** time.
3. Code propre, prêt à la production en **Java, Python et C++**.
4. Le bon, le mauvais, et la laid de la solution – quoi aimer, quoi veiller, et comment s'améliorer.

Laisse plonger.

---

- Oui. 6. Le point de vue de base – positif ou non

- Oui. Pourquoi retourner à non-négatif?

- La somme **maximum** subséquemment de n'importe quel tableau est simplement la somme de tous les nombres positifs.
*Si vous ajoutez un nombre négatif, vous réduisez seulement la somme. *

- Pour un tableau **non-négatif**, les plus petites sommes de subséquence sont faciles à énumérer avec un peu de poids.
Chaque subséquence peut être représentée comme un chemin dans un arbre binaire où l'enfant gauche exclut l'élément suivant et l'enfant droit l'inclut.

Ainsi, la somme **k-th la plus importante** du tableau *original* est égale à :

«» "
(somme positive maximale) – (k-ième plus petite somme d'abs(nums))
«» "

---

- Oui. 7. Génération de k-th la plus petite somme basée sur le tas

Le problème classique de la somme du plus petit sous-ensemble peut être résolu en **O(k log k)** en utilisant un minimum.

Étapes

1. **Pré-processus**
* Calculer `P = somme des positifs`.
* Remplacer chaque élément par sa valeur absolue et trier.

2. **Initialiser le tas**
Poussez `(abs[0], 0)` – la plus petite somme non vide possible.

3. **Déterminer** "k-1" fois
Pop la plus petite paire `(sum, idx)`.
Générer deux enfants:
* Inclure l'élément suivant → `(sum - abs[idx] + abs[idx+1], idx+1)`.
* Gardez la même somme → `(sum, idx)` (pour la prochaine itération).

4. Après la boucle, le dernier "sum" est le **k‐th le plus petit**.
Soustrayez-le de `P` pour obtenir la réponse.

---

- Oui. 8. Échantillons de codes complets

* (voir les sections de code ci-dessus – Java, Python, C++)*

> **Astuce** – En Java, utilisez `long` pour toutes les sommes pour éviter le débordement.
> En C++, `long' est votre ami.
> Python's `int` est sans limite, donc vous êtes en sécurité.

---

- Oui. 9. Bonne, mauvaise et moche

Les bons

- **Intuition-drivé** – Réduit une question difficile à un problème de tas bien connu.
- **Fast** – `k ≤ 2000` garantit que les opérations de tas sont triviales même pour les énormes `n`.
- **Mémoire-lumière** – Espace auxiliaire seulement « O(k) ».

- Oui. Les mauvais

- **Le prétraitement** nécessite le tri de l'ensemble du tableau – `O(n log n)`.
Si le tableau est déjà trié, vous pouvez sauter cette étape.

- **Cas d'urgence** – Si tous les nombres sont négatifs, `P = 0`.
L'algorithme fonctionne toujours parce que nous soustractons la somme la plus petite de `0`.

- Oui. L'Ugly

**Dupliquer les sommes** – Le tas peut générer la même somme plusieurs fois (par exemple, en excluant le même élément).
Dans notre implémentation simple, nous ignorons les duplicatas; une solution plus optimale utilise un jeu de hachage pour dédoubler avant de pousser.

- **Grand k** – Si une question d'entrevue pousse `k` près de `n` (disons `k = 105`), l'algorithme actuel deviendrait invraisemblable.
Pour de tels scénarios, vous auriez besoin d'une approche de partage et de conquête ou de PDD.

---

- Oui. 9. À emporter pour les entrevues

1. ** Expliquez la réduction** : les intervieweurs aiment entendre le "pourquoi" derrière votre algorithme.
2. **Discussion de l'espace-temps**: montrez que vous pouvez analyser la complexité dans le contexte des contraintes (k ≤ 2000).
3. **Gérer les bords de pointe**: indiquez comment vous évitez les débordements et assurez-vous que le tas ne manque jamais de candidats.
4. **Offre une optimisation**: si le temps le permet, montrez comment sauter les duplicatas ou utilisez un astuce à deux points pour éviter de repousser le même élément.

---

10. Pensées finales

LeetCode 2386 est un bel exemple de la façon dont une réduction intelligente transforme un problème intimidant en un problème gérable. Le truc du tas est propre, efficace et portable dans les langues principales.

Maintenant il est temps de s'entraîner. Exécutez le code, modifiez l'entrée et sentez l'intuition se solidifier. Bonne chance pour votre voyage d'entrevue ! C'est ce qu'il a dit.

---

Appel à l'action

- **Like** & **Share** si vous avez trouvé cela utile.
- **S'abonner** pour plus de LeetCode dur problèmes passants.
- **Commentaire** vos propres optimisations ou questions – laissez-nous continuer la discussion.

---

> **Codage heureux!**
> *— Votre sympathique mentor en algorithme*

---

Cela complète la solution complète : l'algorithme, le code et un billet de blog prêt à être interviewé. Joyeux entretien !