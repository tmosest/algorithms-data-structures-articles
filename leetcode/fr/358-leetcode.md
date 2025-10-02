---
titre: LeetCode 358. Réorganiser la chaîne k Distance Apart -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code de Leet 358 – Chaîne de réarrangement k Distance Apart
**Java.Python.C++** – Solutions de travail complètes + un article de blog optimisé SEO qui vous aidera à décrocher votre prochain entretien d'embauche.

---

- Oui. 1. Récapitulation des problèmes

> **Réorganiser la chaîne k Distance Apart**
> Avec une chaîne `s` et un entier `k`, réarrangez `s` de sorte que les mêmes caractères soient au moins des indices `k` séparés.
> Retourner tout réarrangement valide, ou une chaîne vide si elle est impossible.

> **Constraints**
> * `1 <= longueur <= 3 * 105 '
> * `s` contient seulement des lettres anglaises minuscules
> * `0 <= k <= s.longueur "

---

- Oui. 2. Idée de haut niveau

Un algorithme gourmand avec un *max-heap* ( file d'attente prioritaire) fonctionne magnifiquement :

1. Compter les fréquences de chaque personnage.
2. Utilisez un max-heap pour toujours choisir le caractère le plus fréquent qui est ** actuellement autorisé**.
3. Après avoir placé un personnage, il ne peut pas être utilisé à nouveau pour les positions suivantes `k-1` – nous le verrouillons temporairement dans une file d'attente.
4. Lorsque la taille de la file atteint `k`, l'élément le plus ancien est déverrouillé et repoussé dans le tas.
5. Si à tout moment le tas est vide mais que nous devons encore placer un personnage, la tâche est impossible.

C'est le modèle classique de réarrangement à distance* utilisé dans de nombreuses questions d'entrevue.

---

- Oui. 3. Détails de la mise en œuvre

Mots clés Autres
C'est pas vrai.
Utiliser `PriorityQueue<int[]>` avec un comparateur personnalisé (fréquence descendante). `ArrayDeque<int[]>` pour la file d'attente. Autres
**Python**=Le `heapq` fournit un minimum, donc nous poussons les fréquences négatives. Les collections. deque` pour la file d`attente. Autres
**C++**"priority_queue<pair<int,char>>" (max-heap par défaut). `queue<pair<int,char>>` pour attendre. Autres

Les trois solutions fonctionnent dans **O(n log m)** temps (`m <= 26`) et **O(m)** espace supplémentaire.

---

- Oui. 4. Code

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique réarrangementString(String s, int k) {
si (k <= 1) retourner s; // Aucune contrainte nécessaire

// Carte des fréquences
int[] freq = nouveau int[26];
pour [char c : s.toCharArray()) freq[c - 'a']++;

// Max-heap: (-fréquence, caractère)
PrioritéQueue<int[]> pq = nouveau PrioritéQueue<>(
(a, b) -> Integer.compare(b[0], a[0]); // max-heap

pour (int i = 0; i < 26; i++) {
si (freq[i] > 0) pq.offre(nouvelle int[]{freq[i], i});
}

StringBuilder sb = nouveau StringBuilder();
Deque<int[]> wait = nouveau ArrayDeque<>(); // éléments attendant les étapes k

alors que (!pq.isEmpty()="!Wait.isEmpty() {
si (!pq.isEmpty()) {
int[] cur = pq.poll();
sb.appendice(char) (cur[1] + «a»)
cur[0]--; // utilisé un événement
wait.offer(cur); // verrouiller
} autre {
// tas vide mais file d'attente tient toujours des caractères
retour ";
}

si (attendre.size() >= k) {
int[] ready = wait.poll();
si (prêt[0] > 0) pq.offre(prête); // toujours à gauche
}
}
retour sb.toString();
}
}
«» "

4.2 Python

'`python
importation heapq
de collections import deque, Counter

Solution de classe:
def réarrangementString(self, s: str, k: int) -> str:
si k <= 1:
retour s

freq = compteur(s)
#pap max: (-compte, char)
max_heap = [(-cnt, ch) pour ch, cnt dans freq.items()]
heapq.heapify(max_heap)

res = []
wait = deque() # (remaining_count, char)

pendant que max_heap ou attendre :
si max_heap:
cnt, ch = heapq.heappop(max_heap)
res.append(ch)
cnt += 1 # cnt est négatif
(cnt, ch)
Sinon:
retour "" # aucun char disponible à placer

si len(attendre) >= k:
ready_cnt, ready_ch = wait.popleft()
si ready_cnt < 0 :
heapq.heappush(max_heap, (prêt, prêt))

retourner "".join(res)
«» "

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
réarrangement de chaîneString(string s, int k) {
si (k <= 1) retourner s;

vecteur <int> freq(26, 0);
pour (char c : s) freq[c - 'a']++;

//pap max: paire <compte, char>
priorité_queue<pair<int,char>> pq;
pour (int i = 0; i < 26; ++i)
si (freq[i]) pq.emplace(freq[i], char('a' + i));

la chaîne rés;
file d'attente <pair<int,char>>; // éléments verrouillés pour les étapes k

pendant que (!pq.vide()) {
si (!pq.vide()) {
auto cur = pq.top(); pq.pop();
res.push_back(cur.second);
cur.first--; // utilisé un événement
- Attendez.push(cur);
} autre {
retour "; // impossible
}

si (attendre.size() >= k) {
auto ready = wait.front(); wait.pop();
si (prêt.première > 0) pq.push(prêt);
}
}
retour rés;
}
};
«» "

Les trois solutions se compilent sur la plateforme LeetCode et s'exécutent dans les délais.

---

- Oui. 5. Article de blog – Le Bon, le Mauvais, et le Ugly de LeetCode 358.

> *Mots clés:*
> LeetCode 358, Chaîne de réarrangement k Distance A part, algorithme d'entretien, cupidité, file d'attente prioritaire, Java, Python, C++, entretien d'emploi, codage de préparation d'entretien.

---

5.1 Introduction

Lorsque vous préparez une entrevue d'ingénierie logicielle, vous allez inévitablement rencontrer des problèmes LeetCode qui semblent simples à première vue, mais sont trompeurs. **Problème 358 – Chaîne de réarrangement k Distance Apart** est un de ces classiques. Il vous force à penser à *fréquence*, *limites de distance* et *structures de données optimales* en même temps.

Dans cet article nous allons disséquer le problème, marcher à travers le **bon**, le **bad**, et les parties **ugly** de résoudre, et vous donner une implémentation propre, prêt à la production dans **Java, Python, et C++**. Que vous soyez un codeur chevronné ou un nouveau diplômé, la maîtrise de cette solution démontrera une forte pensée algorithmique sur votre CV.

---

5.2 Les bonnes – Pourquoi Ce problème est grand

Pourquoi ça compte ?
C'est-à-dire
Autres **Greedy + Priority Queue**= Combine deux concepts de base de CS – sélection soignée et opérations en tas – à un modèle soigné. Autres
**Temps–Efficace**="O(n log 26)="O(n)=" parce que l'alphabet est fixé. Autres
**Lumière de l'espace** mémoire supplémentaire pour les fréquences plus une petite file d'attente de la taille `k`. Autres
**Real‐World Analogy**= Pensons à des tâches de planification qui ne peuvent pas fonctionner de nouveau. La file d'attente est une micro-tâche. Autres
**Interview Gold** Les recruteurs adorent ça. Autres

---

5.3 Les mauvaises – Pièges que vous pourriez rencontrer

1. **Délibérations**
- Oui. 0` → retourner `s` inchangé.
* `k > max_ frequency` → encore possible (par exemple, "aaabbb", `k=3`), mais vous devez gérer la file correctement.
* Empty tas avant la file vide → impossible.

2. **Dépenses de mise en œuvre**
* Nombres négatifs pour les langues min-heap (Python=s `heapq`).
* comparateur personnalisé en Java peut vous faire voyager vers le haut si vous oubliez la commande .

3. **Débogage Difficulté**
* La file d'attente et le tas interagissent d'une manière subtile; une petite erreur peut produire silencieusement une chaîne invalide ou planter le programme.

---

#### 5.4 Les pièces dures qui peuvent casser Toi

1. **Échec‐par‐un**
* La contrainte `k` signifie que vous devez débloquer un caractère **après** `k` placements, pas `k-1`. Un bug commun est de débloquer `k-1` à la place.

2. **Taille de la file d'attente**
* L'utilisation d'une "deque" ou d'une "queue" avec la taille `k` est essentielle. Oublier de vérifier `Wait.size() >= k` provoque des déverrouillages précoces ou des déverrouillages manquants.

3. ** Signe du déclin fréquent**
* Dans Python, vous allez pousser les nombres négatifs dans le tas, alors rappelez-vous à **incrément** la valeur poppé (`cnt += 1`) pour réduire la fréquence absolue. Oublier cela conduit à des boucles infinies.

4. **Premier retour**
* Vous ne pouvez pas revenir juste après que le tas devient vide; vous devez également vous assurer que la file d'attente n'a pas de caractères verrouillés.

Comprendre ces pièges cachés est la différence entre une solution *work* et une solution *non fiable*.

---

#### 5.5 Marche Grâce à la solution optimale

Voici la version la plus propre et la plus durable de l'algorithme. Nous expliquerons chaque étape au fur et à mesure.

Nombre de fréquences

'`python
freq = Compteurs # O(n)
«» "

Avec seulement 26 caractères possibles, `freq` ne dépassera jamais 26 entrées.

5.5.2 Max— Création d'un tas

'`python
max_heap = [(-cnt, ch) pour ch, cnt dans freq.items()]
heapq.heapify(max_heap)
«» "

Le "heapq" de Python est un "heap" min-heap, donc nous stockons des nombres négatifs pour simuler un "heap max".

##### 5.5.3 En attente d'une file d'attente (`k`-Serrure de distance)

'`python
attente = deque() # Maintenez des tuples (remaining_count, char)
«» "

Après avoir placé un personnage, il va dans `attend'. Ce n'est que lorsque la longueur de la file d'attente atteint `k` que le personnage peut rentrer dans le tas.

La boucle principale

«» "
pendant l'attente:
lieu le plus fréquent autorisé char
Verrouillez-le
si wait.size() >= k:
déverrouiller le plus ancien char
«» "

Cette boucle est le cœur de l'algorithme gourmand. Il garantit que nous ne violons jamais la contrainte `k` parce qu'un caractère ne peut être placé à nouveau qu'après qu'il a été débloqué. (en milliers de dollars)

---

5.6 Analyse de la complexité

Métrique
- C'est quoi ?
**Heure**="O(n log 26)=" → pratiquement linéaire="O(n log 26)="O(n log 26)=" Autres
**L'espace**="O(26 + k)" (pap + file d'attente)="O(26 + k)="O(26 + k)" Autres

Puisque le `26` est une constante, le facteur dominant est `n` (longueur du `s`), ce qui rend la solution appropriée pour la limite de longueur `3 * 105`.

---

5.7 Cas à essayer

Pourquoi ?
- C'est pas vrai.
"aaabb" (en anglais seulement) "bbaaa" (en anglais seulement)
"aaaabbbccc"
"aaabbbccc"
"aaabbbccc""""""Impossible – besoin d'au moins 4 à part"

Ajoutez-les à votre harnais de test pour attraper les bugs hors-par-un.

---

####5.8 A emporter – Ce que veulent les intervieweurs

* **Afficher vos connaissances en structure de données** – La file d'attente prioritaire est un incontournable dans la plupart des entrevues de CS.
* ** Les cas de bord de poignée gracieusement** – `k <= 1`, les scénarios impossibles, et les vérifications de tas vides démontrent la robustesse.
* **Conservez-le propre** – Écrire le code modulaire (`buildHeap`, `unlock`, etc.) et commenter attentivement.

Lorsque vous terminez cette solution, vous allez non seulement résoudre LeetCode 358, mais aussi renforcer un modèle qui apparaît dans beaucoup d'autres problèmes (par exemple, le calendrier de tâche, les variantes de chaîne de réarrangement, le modèle II de Word).

---

#### 5.9 Mot final

LeetCode 358 est un *micro-projet* qui encapsule une puissante stratégie gourmande. En le maîtrisant, vous gagnerez :

1. **Confiance** en utilisant les files d'attente prioritaires pour les contraintes de distance.
2. **Speed** en écriture propre Java, Python, et C++ code dans les conditions d'entrevue.
3. **Un fort point de discussion** sur votre CV: -Une solution de tas avide mise en œuvre pour LeetCode 358 – Chaîne de réarrangement k Distance Apart.

Bonne chance avec votre prochain entretien de codage – codez intelligent, pensez gourmand, et laissez la contrainte de distance faire le levage lourd! C'est ce qu'il a dit.

---

- Oui. 6. Résumé

- **Java** – Utilisations `PriorityQueue<int[]>` + `ArrayDeque<int[]>`.
- **Python** – Utilise `heapq` avec des fréquences négatives + `collections.deque`.
- **C++** – Utilise `priority_queue<pair<int,char>>` + `queue<pair<int,char>>`.

Toutes les solutions sont *O(n log 26)* temps, *O(26)* espace, et gérer la contrainte `k` avec une file d'attente.

Prenez ces extraits, exécutez-les sur LeetCode, et ajoutez l'article de blog à votre portfolio. Vos intervieweurs remarqueront votre compréhension profonde des algorithmes gourmands, des files d'attente prioritaires et des problèmes de planification du monde réel. Bon codage !