---
titre: LeetCode 3506. Trouver le temps nécessaire pour éliminer les souches bactériennes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – 3506 – Trouver le temps nécessaire pour éliminer les souches bactériennes

La tâche est un problème classique de "combine-deux-smallest" – exactement la même stratégie utilisée dans le codage Huffman.
À chaque étape, nous choisissons les deux tâches WBC les plus rapides, les fusionnons en ajoutant le temps partagé, et poussons le
nouvelle tâche combinée de retour dans la piscine.
Quand une seule tâche reste, elle représente le temps total minimum nécessaire pour tout terminer.

Ci-dessous vous trouverez des solutions propres et prêtes à la production dans **Python 3**, **Java 17** et **C++17**.
Tous les trois utilisent un *min-heap* ( file d'attente prioritaire) pour un temps `O(n log n)` et `O(n)`.

---

1.1 Python 3

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
d ' élimination Time(self, timeReq: List[int], splitTime: int) -> Int:
"""
Combine les deux plus petites tâches à plusieurs reprises jusqu'à ce qu'une seule tâche soit laissée.
Équivalent à la construction d'un arbre binaire optimal (Huffman).
"""
# transformer la liste en un petit tas
heapq.heapify(timeReq)

Continuer à fusionner jusqu'à ce que nous ayons un seul élément
pendant que len(timeReq) > 1 :
t1 = heapq.heappop(timeReq) # plus petit
t2 = heapq.heappop(timeReq) # deuxième plus petit
combinés = max(t1, t2) + fraction Temps # WBC se divise une fois, tue max(t1, t2)
heapq.heappush(timeReq, combiné) # remettre la tâche combinée

temps de retourReq[0] # le seul élément restant est la réponse
«» "

---

#### 1.2 Java 17

"Java
Importer java.util. Priorité Demande;
Importer java.util. Recouvrements;

solution de classe {
public long minEliminationTime(int[] timeReq, int splitTime) {
// utiliser un minimum de poids (PriorityQuuee avec commande naturelle)
PriorityQueue<Long> pq = nouveau PriorityQueue<>();
pour (int t : timeReq) {
pq.offre((long) t);
}

pendant que (pq.size() > 1) {
long t1 = pq.poll(); //
longue t2 = pq.poll(); // seconde plus petite
longue combinaison = Math.max(t1, t2) + splitTime;
pq.offre(combinée);
}

// Un seul élément reste
retour pq.peek();
}
}
«» "

> **Pourquoi "long"?**
> La somme la plus défavorable peut aller jusqu'à `10^9 + 10^9 + ...` (-) `10^14`), ce qui correspond à un `long' 64 bits mais pas à un `int' 32 bits.

---

*## 1.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue durée minEliminationTime(vector<int>& timeReq, int splitTime) {
// min-heap utilisant un comparateur plus important
priorité_queue<long long, vecteur<long long>, plus grande<long long>> pq;
pour (int t : timeReq) pq.push(static_cast<long long>(t));

pendant que (pq.size() > 1) {
long t1 = pq.top(); pq.pop(); // plus petit
long long t2 = pq.top(); pq.pop(); // seconde plus petite
longue longue combinée = max(t1, t2) + splitTime;
pq.push(combiné);
}
retour pq.top(); // le seul élément restant
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le laid de résoudre le leetCode 3506

> **SEO Mots-clés**: LeetCode 3506, élimination des souches bactériennes, fractionnement des globules blancs, codage Huffman, file d'attente prioritaire, algorithme gourmand, préparation d'entrevue, complexité du temps, entretien d'emploi, conception d'algorithme.

---

2.1 Introduction

En 2025, le LeetCode (ID 3506) est apparu comme un défi d'entrevue difficile.
Le problème peut sembler biologiquement thématique, mais à son cœur il est un puzzle algorithmique classique: ** Fusionner les deux tâches les plus courtes jusqu'à ce qu'une seule demeure**.
La compréhension de ce puzzle est cruciale pour tout ingénieur logiciel qui se prépare à des entrevues de codage, en particulier pour ce qui est de la conception de systèmes ou des rôles lourds en algorithme.

---

2.2 Réévaluation des problèmes

- **Input**:
- `timeReq[ ]` – tableau d'entiers, `2 ≤ n ≤ 105`, chaque `1 ≤ timeReq[i] ≤ 109`.
- `splitTime` – entier, `1 ≤ splitTime ≤ 109`.

- **Scénaraire**:
- Un seul globule blanc commence.
- Un WBC peut tuer **une** souche bactérienne (temps égal "timeReq[i]".
- Après le meurtre, le WBC est épuisé.
- Un WBC peut *découper* en deux WBC au prix de "splitTime".
- Après la séparation, les deux WBC travaillent en parallèle.

- **Objectif**: Minimiser le temps total nécessaire pour éliminer les souches bactériennes.

---

Pourquoi Huffman Codage ? La solution *Bonne*

La stratégie optimale est identique à la construction d'un arbre Huffman:

1. **Confusionner toujours les deux plus petites tâches**.
2. Ajoute le coût fractionné une fois pour la nouvelle tâche .
3. Répétez jusqu'à ce qu'il reste une tâche.

> **Pourquoi ça marche* *
> Le temps de fin combiné des tâches équivaut au maximum de ses deux enfants plus le temps fractionné – tout comme la profondeur d'un nœud dans un arbre binaire.
> En fusionnant toujours les plus petites tâches, nous gardons l'arbre aussi équilibré que possible, minimisant ainsi le temps de finition global.

Étapes de l'algorithme

Texte
heap = min–heap de tous les temps
alors que le tas a > 1 élément:
a = pop le plus petit
b = pop seconde plus petite
newTime = max(a, b) + splitTime
pousser nouveau Temps écoulé
réponse = seul élément restant
«» "

- **Complexité temporelle**: `O(n log n)` – chacune des fusions `n-1` effectue deux `pop` et un `poush` sur un tas.
- **Complexité spatiale**: `O(n)` – le tas stocke toutes les heures intermédiaires.
- **Juges**:
- Tout `timeReq` égal → l'algorithme équilibre toujours l'arbre.
- `splitTime` énorme → l'algorithme pousse naturellement le coût fractionné dans la réponse finale.

L'implémentation propre dans Python (`heapq`), Java (`PriorityQueue`), et C++ (`priority_queue` avec `gross`) montre la maîtrise des structures de données et démontre votre capacité à traduire un optimum théorique en code.

---

2.4 Quand l'avidité fait défaut – la mauvaise approche

Beaucoup de codeurs essayent un "pick le plus petit, tuez-le, divisez, répétez.
Ce **regarde** cupide mais **doesn=t** explique correctement le parallélisme.

Erreur courante

'`python
pendant la file d'attente:
t = pop_small()
# tuer t
fractionné une fois
# ... supposer incorrectement que la tâche suivante commence après le meurtre
«» "

- **Pourquoi ça échoue**:
Après le premier meurtre, un nouveau WBC est créé seulement si une scission se produit.
Ne pas fusionner deux tâches ignore simultanément la nature *parallèle* et peut produire une réponse jusqu'à deux fois plus grande.

La preuve par contre-exemple

Let `timeReq = [1, 2, 100]`, `splitTime = 1`.

- Mauvaise cupidité :
1. Tuer la souche 1 («1 s»).
2. Séparer («+1 s»).
3. Tuer la souche 2 (« 2 s »).
4. Séparer («+1 s»).
5. Tuer la souche 3 (100 s).
**Total** = 1 + 1 + 2 + 1 + 100 = 105 s.

- Optimisé:
1. Fusionner 1 & 2 → combinés = `max(1,2)+1 = 3`.
2. Fusionner 3 & 100 → combinés = `max(3 100)+1 = 101`.
**Total** = 101 s.

La méthode d'avidité était 4 s plus lente – inacceptable dans une interview de hard.

---

### 2.5 La partie *Ugly* – traiter des grands nombres et des dépassements

Étant donné que «timeReq[i]» et «splitTime» peuvent être jusqu'à «109», la somme cumulée peut facilement dépasser les limites entières de 32 bits («» 1014»).
Si vous utilisez 32 bits `int` en Java ou `int` en C++, vous rencontrerez un débordement entier, produisant de mauvaises réponses sur le harnais de test.

**Fix**:
- Utilisez `long` (`int64_t` en C++, `long` en Java) pour retenir des sommes intermédiaires.
- En Python, `int` est déjà une précision arbitraire, donc il est sûr.

---

2.6 Conseils pratiques d'entrevue

Comment le problème le teste Comment le montrer dans votre mémoire
Il y a un problème.
**Le raisonnement de grêle**Le choix des deux tâches les plus petites est le mouvement optimal. Mentionnez la fusion de l'Huffman dans votre lettre de présentation ou votre portfolio. Autres
**Connaissance de la structure des données** Faites ressortir l'utilisation de `heapq`, `PriorityQueue` ou `priority_queue` dans vos projets. Autres
**La solution « O(n log n) » est nécessaire pour 105 éléments. Ajouter une section d'analyse de complexité à n'importe quel poteau d'algorithme. Autres
**Manipulation d'un cas d'urgence** Démontrez une gestion robuste de type (`long`/`int64_t`) dans votre code. Autres
**Test du stress sur les entrées aléatoires, les cas de bord. Utilisez des tests unitaires pour montrer que vous pouvez attraper des bugs subtils avant les entretiens. Autres

**Entrevue d'emploi Conseil** : Lors de l'examen de ce problème, soulignez que la solution n'est pas une simulation de la biologie mais une construction binaire optimale*. Ce niveau d'abstraction indique une forte pensée algorithmique.

---

2.7 Conclusion – Pourquoi 3506 est-il un must-now

- **Le Bon**: la fusion de style Huffman donne une solution propre et optimale "O(n log n)".
- **Le mauvais**: les approches naïves avides ou de simulation brisent la règle de fraction parallèle et produisent des temps sous-optimaux.
- **L'Ugly** : oublier l'arithmétique 64 bits conduit à un débordement silencieux – un bug subtil que les intervieweurs aiment repérer.

Mastering LeetCode 3506 démontre votre capacité à:

- Traduire un scénario réel en un modèle mathématique.
- Choisissez la bonne structure de données.
- Raisonner rigoureusement l'optimalité (codage Huffman).
- Attention aux cas de bord (dépassement, contraintes importantes).

Tous ces éléments sont exactement les compétences recherchées par les recruteurs dans les ingénieurs logiciels seniors et les prospects techniques.

Bonne chance d'obtenir ce travail – votre prochaine entrevue pourrait être un problème *white-blood-cell*!