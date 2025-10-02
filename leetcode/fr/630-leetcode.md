---
titre: LeetCode 630. Horaire des cours III –
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# Le Puzzle d'entrevue de l'annexe III
**LeetCode 630 – Hard**
*Quels recruteurs veulent voir? Comment le résoudre en Java, Python, & C++. *

---

TL;DR

Code de la langue
C'est quoi, ça ?
[Voir et copier]
[Voir et copier](#python-code)
[Voir et copier](#c-code)

> **Algorithme** – Greedy + Max-Heap
> **Heure** – 'O(n log n) "
> **Espace** – «O(n)»

---

- Oui. Pourquoi ce problème se pose dans un entretien d'embauche

* **Une preuve de mariage** – Montre que vous pouvez raisonner sur l'optimalité.
* **Structure de données de masse** – Vous donne une chance de démontrer la familiarité avec les files d'attente prioritaires.
* **Vibe réelle** – Les cours d'agenda sont comme la gestion de projet. Les recruteurs adorent l'entendre.

---

Récapitulation du problème

Vous êtes donné `cours`, un tableau où chaque élément est `[durée, dernier jour]`.
Vous commencez le jour 1, les cours peuvent se chevaucher, et chaque cours doit finir ** par** son `dernier jour`.
Retournez le nombre ** maximum** de cours que vous pouvez suivre.

---

- Oui. Le bien – Un cupidité propre et optimal

1. **Cours de base par date limite («dernier jour»)** –
Essayez toujours de terminer le cours le plus tôt possible.
2. **Tenir un maximum de durées** –
le tas tient tous les cours que vous avez accepté jusqu'à présent.
3. **Si l'ajout d'un nouveau cours vous maintient à temps** → l'accepter.
Mettre à jour l'heure actuelle et pousser sa durée sur le tas.
4. **Si l'ajout vous rendrait en retard** →
Regardez le cours le plus long que vous êtes déjà en train de suivre ('heap.peek()').
Si la durée la plus longue est **plus grande** que la nouvelle, remplacez-la:
* supprimer le plus long, ajouter le nouveau, ajuster le temps total.
Cela libère le temps et maintient le calendrier serré.
5. **Résultat** – la taille du tas est le nombre maximum de cours.

Pourquoi ça marche ?
Parce que le tas stocke toujours les **périodes les plus courtes** qui permettent de respecter les plus tôt les délais.
Si nous sommes en retard, remplacer le cours le plus long par un cours plus court ne peut qu'aider.

---

- Oui. L'Événement – Ce qu'il faut faire attention

Pourquoi ça compte ?
- Oui.
**Traitement dans les délais** Utilisez un tri stable ou ajoutez une clé secondaire (durée) si désiré. Autres
**La plus grande entrée**. Utiliser la solution `O(n log n)` ci-dessus. Autres
**Temps cumulé peut dépasser 231-1. Autres

---

- Oui. L'Ugly – Pièges communs et cas de bord

Problème Solution
C'est quoi ?
Autres **Le cours prend plus de temps que la date limite.** L'algorithme va le sauter automatiquement. Autres
Exemple 3: `[[3,2],[4,3]`. 0.
**Dupliquer les délais et les durées**. Le comparateur ne doit utiliser que le dernier jour. Autres
Autres **Très longues durées, mais peu de délais** Utiliser des entiers 64 bits. Autres
**Les valeurs négatives**=Les contraintes garantissent des valeurs positives, mais le codage défensif est bon. Assister ou protéger contre les négatifs. Autres

---

- Oui. Le code

Ci-dessous sont les solutions prêtes à coller pour **Java**, **Python** et **C++**.
Tous les trois utilisent la même idée algorithmique.

### Java

"Java
Importation de java.util.*;

solution de classe publique {
programme d'internat publicCours[int[]]
Tri en dernier Jour
Arrays.sort(cours, Comparateur.comparingInt(a -> a[1]));

// 2-pap max (plus grande durée en haut)
Priorité Queue<Integer> maxHeap = nouveau PriorityQueue<>(Collections.reverseOrder());

courant longTime = 0; // 64-bit pour éviter le débordement

pour (int[] cours : cours) {
durée int = cours[0];
délai int = cours[1];

si (temps actuel + durée <= délai) {
// Accepter le cours
maxHeap.offre(durée);
actuel Durée +=;
} sinon si (!maxHeap.isEmpty() && maxHeap.peek() > durée) {
// 4 Remplacer le cours le plus long
currentTime += durée - maxHeap.poll();
maxHeap.offre(durée);
}
// sinon: saute ce cours
}
retour maxHeap.size();
}
}
«» "

Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
programme Cours(soi-même, cours: Liste[Liste[int]]) -> Int:
# Trier par date limite
cours.sort(key=lambda x: x[1])

# Max-heap utilisant des durées négatives
max_heap = []
_temps courant = 0

pour la durée, délai dans les cours:
if current_time + durée <= date limite:
heapq.heappush(pape maximale, durée)
_temps courant += durée
elif max_heap et -max_heap[0] > durée:
current_time += duration + heapq.heappop(max_heap) # pop le plus grand, ajouter nouveau
heapq.heappush(pape maximale, durée)

retour len(max_heap)
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int programme Cours(vecteur<vecteur<int>&cours) {
Classer par date limite
tri(cours.degin(), cours.end(),
[](const vector<int>& a, const vector<int>& b) {
retour a[1] < b[1];
});

Nombre maximal de durées
priority_queue<int> maxHeap;
longue durée de temps = 0; // 64-bit

pour (const auto& c : cours) {
int dur = c[0], dl = c[1];
si (curTime + durée <= dl) {
maxHeap.push(dur);
curTime += durée;
} sinon si (!maxHeap.vide() && maxHeap.top() > dur) {
curTime += durée - maxHeap.top();
le point d'entrée est remplacé par le texte suivant:
maxHeap.push(dur);
}
}
retour (int)maxHeap.size();
}
};
«» "

---

## Article du blog : Le bon, le mauvais, et le mauvais de l'horaire de cours III

> **Titre** – *=Maîtrise du LeetCode 630 : Programme de cours III – Le bon, le mauvais et le mauvais*
> **Meta‐Description** – *Apprenez la solution cupide à LeetCode 630, plongez dans des boîtiers de bord et asez votre prochaine entrevue d'ingénierie logicielle. *

---

C'est pas vrai. Le bon : pourquoi cette solution se transforme

- **Simplicité + Puissance** – Une seule passe après tri donne la réponse optimale.
- **Intuitive Greedy** – Prenez le cours avec la première date limite. (en milliers de dollars)
- **Heap Leverage** – Remplacer le cours le plus long est O(log n), en maintenant le calendrier serré.
- **Real-World Parallel** – Similaire à la planification des tâches, à la planification des projets ou à la planification des tâches du CPU.

C'est vrai. Les mauvaises: les pièges communs à éviter

Piège
- Oui.
Utiliser `int` pour le temps cumulatif. Autres
Autres Ignorer la possibilité d'échéances précoces Toujours trier par échéance; un mauvais genre donne des résultats sous-optimaux. Autres
Autres L'algorithme saute automatiquement les cours impossibles. Autres
Une solution « O(n2) » naïve (p. ex. rétrotraçage) sera utilisée pour 104 entrées. Autres

C'est vrai. L'horrible : les cas de bord et le tuning

- **Calendrier exact** – La fin du cours le dernier jour est autorisée.
- ** Grandes durées** – Même si la durée d'un cours est supérieure à sa date limite, l'algorithme le rejette naturellement.
- **Attaches dans les délais** – L'ordre des cours avec le "dernier jour" identique n'affecte pas la justesse, mais un genre stable garde la logique claire.
- ** Empreinte de mémoire** – Les dépôts de masse à la durée `n` au plus, donc la mémoire `O(n)` est acceptable.

---

## Conseils d'entrevue : parler de ce problème

1. ** Expliquez l'invariant gourmand** – Si vous pouvez terminer un cours avant sa date limite, il est toujours sûr de le prendre; sinon, nous remplaçons le plus long si elle libère du temps. (en milliers de dollars)
2. **Montrer l'intuition du tas** – Nous avons besoin d'un accès rapide à la plus longue durée pour pouvoir l'échanger. (en milliers de dollars)
3. **Complexité de la concentration** – Déploiement `O(n log n)`, chaque opération de tas `O(log n)`, total `O(n log n)`.
4. **Discuss cas de bord** – Et si un cours dépasse sa durée? Notre algorithme le saute. (en milliers de dollars)

---

## SEO & Job-Hunting Boost

Mots-clés Pourquoi ça aide
C'est quoi ?
`LeetCode 630`== match direct pour les recruteurs qui cherchent ce problème. Autres
Calendrier des cours III solution '. Autres
`Java file d'attente prioritaire LeetCode`. Autres
"Python heapq interview" "Showcases Python compétences. Autres
"C++ priority_queue scheduling". Autres
"Greedy algorithme interview" Démontre la pensée algorithmique. Autres
"Conseils d'entretien de l'ingénieur logiciel" Autres

**Inclure ces mots clés naturellement dans les rubriques, les puces et la méta description**. Un article bien structuré avec des extraits de code clairs sera classé plus haut et attraper les yeux des recruteurs.

---

### Liste de contrôle finale avant de soumettre

- Le code compile en Java 17 / Python 3.10 / C++17.
- Tous les cas de bord couverts.
- C'est la complexité.
- Un article de blog prêt pour Medium, Dev.to, ou votre propre portfolio.
- Mots clés parsemés.

Bonne chance ! C'est ce qu'il a dit.

---