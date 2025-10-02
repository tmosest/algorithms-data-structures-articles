---
Titre: LeetCode 1834. CPU à simple fil - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1834 – CPU unique
**Python de Java** – Solutions complètes, prêtes à la production + un billet de blog complet* qui parle du **bon, du mauvais et du laid**.
Utilisez ceci pour aser votre prochaine entrevue de codage, augmenter votre CV et impressionner les recruteurs.

---

Récapitulation des problèmes

Vous êtes donné un éventail de tâches:

«» "
tâches[i] = [enquerueTimei, traitement Heurei]
«» "

* `enquerueTimei` – quand la tâche devient disponible.
* « ProcessingTimei » – combien de temps il faut pour terminer.

Le CPU est à jeun :
1. Si elle est au ralenti et qu'aucune tâche n'est prête → restez au ralenti.
2. Si c'est inactif et qu'il y a des tâches prêtes → choisissez celle avec le temps de traitement le plus court**.
- Tie → choisir le plus petit **index**.
3. Une fois qu'une tâche commence, elle s'achève.

Retourner l'ordre des indices que le processeur traitera.

---

Aperçu de la solution optimale

1. **Tâches de la Section** Heure.
2. Utilisez un **min-heap** (`PriorityQuue` en Java, `priority_queue` en C++, `heapq` en Python) clé par `(processingTime, index)`.
3. Passez par la liste triée pendant :
* Ajouter toutes les tâches dont `enquerue Temps <= courantTime` au tas.
* Si tas vide → sauter `currentTime` à la tâche suivante Heure.
* Pop de tas → tâche de processus → mettre à jour `current Temps += traitement.
4. Stocker les indices dans le tableau de réponses.

L'algorithme est `O(n log n)` en raison du tri + heap ops, avec la mémoire `O(n)`.

---

Mise en œuvre du code

### Java

"Java
Importation de java.util.*;

solution de classe publique {
classe statique privée Tâche {
int idx, enqueue, process;
Tâche(int idx, int enqueue, int process) {
ce.idx = idx;
Ça. demande = demande;
Ça. processus = processus;
}
}

public int[] getOrder(int[]] tâches) {
int n = tâches.longueur;
Tâche[] arr = nouvelle tâche[n];
pour (int i = 0; i < n; ++i)
arr[i] = nouvelle tâche(i, tâches[i][0], tâches[i][1];

Tri par heure d'attente
Tableau.sort(arr, Comparator.comparingInt(t -> t.enqueue);

// 2-heap: d'abord par processus, puis par idx
PriorityQueue<Task> pq = nouveau PriorityQueue<>(
Comparer.<Task>comparerInt(t -> t.process)
.thenComparingInt(t -> t.idx);

int[] ans = nouvelle int[n];
int ptr = 0; // pointeur dans arr trié
longue curTime = 0; // temps courant, utiliser longtemps pour éviter le débordement
Int ansIdx = 0;

pendant que (ptr < n.pq.isEmpty()) {
// Poussez toutes les tâches qui sont arrivées
pendant que (ptr < n& arr[ptr]. enqueue <= curTime) {
pq.offre(arr[ptr++]);
}

si (!pq.isEmpty()) {
Tâche cur = pq.poll();
ans[ansIdx++] = cur.idx;
curTime += processus cur;
} autre {
// Aucune tâche prête → sauter à l'arrivée suivante
curTime = arr[ptr].enqueue;
}
}
le retour des an;
}
}
«» "

Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def getOrder(self, tâches: List[List[int]]) -> Liste[int]:
# Joindre l'index
tâches = [(e, p, i) pour i, (e, p) dans le dénombrement(tâches)]
tasks.sort() # trier par enquue time

res = []
pq = [] # tas de (processus, index)
durée = 0
i = 0
n = len(tâches)

alors que i < n ou pq:
# Ajouter toutes les tâches prêtes
pendant que i < n et tâches[i][0] <= temps:
e, p, idx = tâches[i]
heapq.heappush(pq, (p, idx))
i += 1

si pq:
p, idx = heapq.heappop(pq)
durée += p
res.append(idx)
Sinon:
# Idle – sautez à la prochaine enquête
temps = tâches[i][0]

retour res
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> getOrder(vecteur<vecteur<int>>& tâches) {
struct Tâche { longue e, p; int idx; };
vecteur<Tâche> v;
pour (int i = 0; i < tasks.size(); ++i)
v.push_back({tâches[i][0], tâches[i][1], i});

tri(v.begin(), v.end(),
[](const Task& a, const Task& b) { retour a.e < b.e; });

priority_queue<pair<long long,int>,
vecteur<pair<long long,int>>,
supérieur<pair<long long,int>>> pq; // (processus, idx)

vecteur <int> ans;
longue courbure = 0;
i = 0, n = v.size();

pendant que (i < n.pq.vide()) {
(i < n& v[i].e <= cur) {
pq.emplace(v[i].p, v[i].idx);
++i;
}

si (!pq.vide()) {
auto [proc, idx] = pq.top(); pq.pop();
as.push_back(idx);
cur += proc;
} autre {
cur = v[i].e;
}
}
le retour des an;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 1834

> **Mots-clés du référencement**: *CPU LeetCode 1834*, *solution Java*, *solution Python*, *solution C++*, *programmation de tâches la plus rapide*, *codification de l'entrevue*, *préparation de l'entrevue d'emploi*, *explication de l'algorithme*, *min-heap*, *attente prioritaire*.

---

C'est pas vrai. Les bonnes

Pourquoi il est grand
- Oui.
**Linear scan + heap**. Autres
**Déterministe tie-breaking**= Le tri par index garantit la règle de l'indice le plus petit. Autres
**Jump‐ahead oisin logique** Autres
**Les versions Java, Python et C++ sont concises mais claires. Autres

- **Complexité temporelle**: `O(n log n) "
- **Complexité spatiale**: "O(n)" (pour le tas + liste triée)

---

- Oui. Les mauvais

Question / Atténuation Autres
Il y a un problème.
**Risque d'excès de débit**=Utilisez `long long`/`long` pour l'heure actuelle parce que les temps d'attente/de traitement peuvent atteindre 109. Autres
**Supprimer la stabilité**S'assurer que les tâches sont triées strictement par temps d'attente; l'index n'a pas d'importance après les tas par temps de traitement. Autres
**Cas d'Edge** - Toutes les tâches arrivent en même temps. <br>- CPU inactif pour toujours à la fin? (ne se produit jamais parce que les tâches sont finies). Autres

---

C'est vrai. L'Ugly

Qu'est-ce qui peut mal se passer ? Autres
- Oui.
**Comparateur de masse désordonné** Autres
**O(n2) boucle naïve**=Certaines solutions poussent toutes les tâches dans un tas et les pop toutes, même lorsque le CPU s'en va, cela fonctionne encore mais est sous-optimal. Autres
**Utiliser `queue` au lieu de `priority_queue`**.Une file d'attente FIFO ignore la règle -"temps de traitement le plus court". Autres
**Ne pas avancer le temps au ralenti** Autres

---

C'est pas vrai. Conseils de préparation à l'entrevue

1. ** Expliquez l'intuition d'abord** – parlez de la gamme de tâches à l'arrivée, utilisez-la pour les tâches prêtes.
2. **Discuse le temps/l'espace** – les recruteurs aiment voir l'argument "O(n log n)".
3. **Cas de bord de Mention** – montrez que vous avez pensé à toutes les tâches arrivant à la fois ou CPU au ralenti.
4. **Afficher les fonctions linguistiques à jour** – p.ex., Java=s `Comparator.comparing Int ', Python's 'heapq'.
5. **Fournir des cas de test** – les deux exemples donnés + quelques exemples personnalisés (p. ex., toutes les mêmes enquêtes, une seule tâche).

---

C'est vrai. Réflexions finales

LeetCode 1834 est un problème classique *priority-queue*.
L'astuce n'est pas de trop réfléchir à la structure des données ; une fois que vous voyez toujours choisir le travail le plus court, vous êtes essentiellement faire *Shortest‐Job‐First (SJF)* programmation.
Avec les extraits de code ci-dessus, vous êtes prêt à laisser tomber la bonne solution dans votre prochaine entrevue de codage et partir avec un renforcement de confiance.

---

Liens rapides

- [Code leet 1834 – CPU simple fileté](https://leetcode.com/problèmes/simple fileté-cpu/)
- [Solution de Java (GitHub Gist)] (https://gist.github.com/votrenom d'utilisateur/1234567)
- [Python Solution (Pastebin)] (https://pastebin.com/votrecode)
- [C++ Solution (GitHub)] (https://github.com/votrenom d'utilisateur/code de leet-1834)

Bonne chance, et que le CPU soit toujours en votre faveur! C'est ce qu'il a dit