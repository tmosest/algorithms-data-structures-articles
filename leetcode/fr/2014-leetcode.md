---
titre: LeetCode 2014. Subséquence la plus longue répétée k Times -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# La plus longue séquence répétée *k* Times – Un billet de blog prêt à travailler
*(Code Leet 2014 – dur, La séquence la plus longue se répète k Times

---

C'est pas vrai. Pourquoi ce problème est important

- **Interview-buzzword** – LeetCode Les problèmes difficiles sont une mine d'or pour les interviews sur la structure des données et les algorithmes.
- **Real-world pertinence** – La correspondance subséquence est au cœur du séquençage de l'ADN, de l'extraction de texte et de la compression.
- **Show‐case** – Résoudre en **Java, Python et C++** démontre la maîtrise des astuces spécifiques au langage (streams, itérateurs, I/O rapides).

Si vous pouvez expliquer l'idée, la complexité et présenter le code propre dans trois langues principales, vous serez un candidat fort pour les rôles qui vous demandent d'écrire -Clever, code prêt à la production.

---

Récapitulation des problèmes

> **Input**
> - `s` – une chaîne de lettres anglaises minuscules (`2 ≤=2 < min(2001, k·8)`)
> - `k` – le nombre de répétitions (`2 ≤ k ≤ 2000`)
> ** Sortie**
> La plus longue séquence « seq » de telle sorte que « seq » répétée « k » fois (« seq »k ») est toujours une séquence « s ».
> Si plusieurs subséquences partagent la longueur maximale, retournez la plus grande lexicographie. Retour `""` s'il n'y en a pas.

Exemples
Résultats
- C'est quoi ?
Code des lettres
"bb"
"ab""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

---

- Oui. Le point de vue fondamental

> **Un subséquence `seq` répète `k` fois si nous pouvons trouver `k` copies non-overlaping de `seq` dans l'ordre. **
> En d'autres termes, en marchant une fois à travers `s` nous devrions être en mesure de "consumer" les caractères de `seq` `k` temps.

Cela nous donne une aide linéaire:

Texte
nombre = 0, i = 0 // Indices suivants
pour ch en s:
Si ch == suite[i]:
i += 1
i == len(seq): // une copie terminée
i = 0
nombre += 1
k: retourner Vrai
Retour Faux
«» "

L'assistant travaille pour *any* `seq` dans le temps `O(=)'.

---

## 4- Force contre recherche optimisée

- **Brute-force** – Énumérer toutes les sous-séquences ('2^n') → impossible.
- ** Programmation Dynamique** – Trop d'états ('26^L') si nous stockons tous les subséquences possibles.
- **Breadth‐First Search (BFS) with Greedy Ordering** – Explorez les sous-séquences niveau par niveau, toujours en étendant avec `a...z`.
- Le **dernier** subséquence valide d'une longueur donnée sera le lexicographiquement le plus grand (puisque nous essayons des lettres en ordre ascendant).
- Nous nous arrêtons lorsque la file d'attente devient vide; la réponse est la plus longue valide que nous ayons vue.

Avec les contraintes («S» < 2001, k ≤ 2000, «S» < k·8»), la longueur maximale possible de subséquence est «S» / k» (8).
Ainsi, le BFS explore au maximum "26^8 " 2·10^11 " chaînes *en théorie*, mais dans la pratique, le contrôle "isK" coupe radicalement la recherche.

---

C'est pas vrai. L'algorithme (Greedy BFS)

1. **Initialiser**
- `queue` ← `[""]` (séquence vide).
- `réponse` ← `""`.

2. **Bien que la file d'attente ne soit pas vide* *
- C'est bon.
- Pour chaque `c` dans `'a` ... `'z``:
- `suivant = curr + c`.
- Si `isK(next, s, k)` est vrai:
- Mettre à jour `answer = next' (le plus long trouvé jusqu'à présent).
- Dans la file d'attente.

3. **Retour** "réponse".

> ** Pourquoi cupide ? **
> Parce que nous itérer des lettres dans l'ordre naturel, le *dernier* subséquence valide d'une longueur donnée est automatiquement le lexicographiquement le plus grand.
> **Pourquoi BFS? **
> Il garantit que nous terminons l'exploration de tous les subséquences de longueur `L` avant de passer à `L+1`, donc nous découvrons naturellement le plus long.

---

Analyse de complexité

Aspect Estimation
C'est pas vrai.
Temps "isK" Autres
Niveau max Taux de chômage
Autres Total a visité des chaînes de caractères, mais pratiquement beaucoup moins. Autres
**Temps**="O(="s · visités)" – en pratique quelques millisecondes. Autres
**L'espace**="O( visité · moyenne_longueur)=" – aussi minuscule pour des limites données. Autres

---

Les bons, les mauvais et les méchants

Catégorie
C'est pas vrai.
**Concept**=L'aide linéaire claire, intuitive et gourmande BFS=L'aide peut exploser combinatoirement dans les cas pathologiques=L'espace de recherche est naturellement limité par des contraintes=
**Code**=Clean, short, use only standard library== Nécessite une concaténation manuelle de la chaîne qui peut être plus lente en Python== Aucune – aucune dépendance externe==
**Readability**= Commentaires en ligne, étape par étape== Le nom `isK` peut être déroutant –=canRepeatedK?== Aucun

---

# # # 8.

- **Titre**: LeetCode 2014 – La plus longue séquence répétée k Times (solutions Java/Python/C++)
- **Méta-Description**: "Maîtriser le problème de LeetCode dur "Longest Subsequence Repeed k Times" avec le BFS étape par étape et des solutions gourmandes en Java, Python et C++. Apprenez la complexité du temps, les extraits de code et les explications favorables aux entrevues. (en milliers de dollars)
- **Mots clés**: LeetCode dur, la plus longue séquence, répété k Times, problème d'entrevue, BFS, Greedy, Java, Python, C++, Algorithm, Structures de données.

---

Code complet (trois langues)

> **Note** – Les trois solutions utilisent la même idée algorithmique mais s'adaptent aux idiomes du langage.
> Ils sont prêts à coller dans l'éditeur de LeetCode.

---

#### 9.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
// Entrée principale
public Chaîne la plus longueSous-séquenceRepeatedK(String s, int k) {
La meilleure chaîne = ";
Queue<String> q = nouvelle liste liée<>();
q.add(""); // commencer par une sous-séquence vide

alors que (!q.isEmpty()) {
Chaîne cur = q.poll();
pour (char ch = 'a'; ch <= 'z'; ch++) {
Chaîne nxt = cur + ch;
Si (estK(nxt, s, k)) {
best = nxt; // le plus long trouvé à ce jour
q.offre(nxt); // explorer les extensions
}
}
}
le meilleur retour;
}

// Vérifier si nxt répété k times est une séquence de s
booléen privé isK(String nxt, String s, int k) {
int idx = 0, nombre = 0; // idx -> position en nxt
pour (int i = 0; i < s.longueur(); i++) {
si (s.charAt(i) == nxt.charAt(idx)) {
idx++;
si (idx == nxt.length()) { // une copie terminée
idx = 0;
count++;
si (compte == k) retourne true;
}
}
}
retourner faux;
}
}
«» "

---

### 9.2 Python 3.10

'`python
à partir de collections import deque

Solution de classe:
def leastSubséquenceRepeatedK(self, s: str, k: int) -> str:
meilleure = ""
q = deque([""]) # file d'attente BFS

alors que q:
cur = q.popleft()
pour ch dans "abcdefghijklmnopqrstuvwxyz":
nxt = cur + ch
si self.is_k(nxt, s, k):
meilleure = nxt
q.annexe(nxt)
le meilleur retour

@staticmethod
def is_k(nxt: str, s: str, k: int) -> C'est vrai.
idx, nombre = 0, 0
pour ch en s:
si ch == nxt[idx]:
idx += 1
Si idx == len(nxt): # une copie terminée
idx = 0
nombre += 1
si le nombre == k:
retour Vrai
Retour Faux
«» "

> *La concaténation des cordes Python est bonne pour les cordes courtes produites par le BFS. *

---

### 9.3 C++ (17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne la plus longueConséquenceRépééeK(chaîne s, int k) {
string best = ";
file d'attente <string> q;
q.push(""); // commencer à partir de la séquence vide

pendant que (!q.vide()) {
chaîne cur = q.front(); q.pop();
pour (char ch = 'a'; ch <= 'z'; ++ch) {
chaîne nxt = cur + ch;
Si (estK(nxt, s, k)) {
best = nxt; // le plus long jusqu ' à présent
q.push(nxt); // explorer plus profondément
}
}
}
le meilleur retour;
}

particulier:
Bool isK(const string& nxt, const string& s, int k) {
int idx = 0, cnt = 0; // idx -> position en nxt
pour (charc : s) {
si (c) nxt[idx]) {
++idx;
si (idx == (int)nxt.size()) { // copie terminée
idx = 0;
++cnt;
si (cnt) k) retourne true;
}
}
}
retourner faux;
}
};
«» "

> *L'utilisation de `queue<string>` et de boucles simples maintient le code concis et rapide. *

---

Les pensées finales

- **Afficher votre capacité** de traduire un énoncé de problème en une stratégie algorithmique claire.
- **Mention de l'aide** `isK` – c'est le "magic" qui rend l'ensemble de la solution linéaire dans `="s".
- **Discuse la complexité** – les intervieweurs aiment vous voir parler du temps et de l'espace.
- **Fournir les trois langues** – faire preuve de polyvalence et de préparation pour une pile technologique diversifiée.

Bonne chance pour régler le problème et atterrir la prochaine interview ! C'est ce qu'il a dit