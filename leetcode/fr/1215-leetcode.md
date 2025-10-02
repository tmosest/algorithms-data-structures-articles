---
titre: LeetCode 1215. Nombres de pas -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. La solution – Extraits de code 3 langues

Ci-dessous vous trouverez des implémentations propres, prêtes à la production pour **Java, Python et C++** qui résolvent LeetCode 1215 – *Numéros d'étape*.
Tous les trois utilisent la même idée de large-first-search (BFS), sont bien commentés et fonctionnent dans les limites de temps et d'espace annoncés.

> **Conseil pour les entrevues** –
> *BFS* est généralement la première chose que les gens essayent pour les problèmes de chiffre de construction.
> Assurez-vous que vous pouvez expliquer pourquoi la file d'attente est limitée (`curr > high/10`), pourquoi nous traitons `0` séparément, et pourquoi un `sort() final est nécessaire (l'ordre BFS n'est pas strictement en augmentation).

-----------------------------------------------------------------------------------

- Oui. Java – `Solution.java "

"Java
Importation de java.util.*;

solution de classe publique {
***
* Retourner tous les nombres de marches en [faible, élevé], inclusive.
*
* @param faible limite inférieure (0 ≤ faible ≤ élevée)
* @param haute limite supérieure (faible ≤ élevée ≤ 2·10^9)
* @retour trié la liste des nombres de pas
*/
liste publique<entier> nombreSteppingNumbers(int low, int high) {
Liste du résultat <entier> = nouvelle liste de distribution<>();

// Cas de bord: 0 est un nombre de pas s'il se trouve dans la plage
Si (faible) 0) résultat.add(0);

Queue<integer> file d'attente = nouvelle List Linked<>();
// commencer BFS à partir de chaque nombre à un chiffre (1 ... 9)
pour (int d = 1; d <= 9; d++) {
queue.offre(d);
}

pendant que (!queue.isEmpty()) {
int curr = file d'attente.poll();

si (curr >= faible &&curr <= élevé) {
résultat.add(curr);
}

// Si le nombre suivant déborde ou dépasse le nombre élevé, arrêtez d'étendre
si (coureur > haute / 10) continuer;

int dernier Chiffre = pourcentage 10;

// Ajouter le dernier Chiffre+ 1
si (dernière période < 9) {
int next = curr * 10 + (dernierDigit + 1);
si (prochaine <= haute) file d'attente.offre(prochaine);
}

// Ajouter la dernièreDigit- 1
si (dernier Digit > 0) {
int next = curr * 10 + (dernierDigit - 1);
si (prochaine <= haute) file d'attente.offre(prochaine);
}
}

Collections.sort(résultat); // L'ordre BFS n'est pas garanti
le résultat du retour;
}

/* */
/* Harnais d'essai rapide – exécutez avec la solution de java dans votre IDE. */
/* */
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.countSteppingNumbers(0, 21)); // [0,1,2,3,4,5,6,7,8,9,10,12,21]
System.out.println(sol.countSteppingNumbers(10, 15)); // [10,12]
}
}
«» "

-----------------------------------------------------------------------------------

## Python – `solution.py "

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def countSteppingNumbers(self, low: int, high: int) -> Liste[int]:
"""
Retourner tous les nombres de marches en [faible, élevé], inclusivement.
"""
res = []

# 0 est un nombre de pas seulement si elle appartient à la plage
Si faible == 0:
res.append(0)

q = deque(range(1, 10)) # commencer par 1..9

alors que q:
cur = q.popleft()

si faible <= cur <= haut:
res.append(cur)

# Pas besoin de grandir davantage si le nombre suivant déborde
Si cur > haut // 10:
poursuivre

Dernier = cur % 10

# Ajouter la dernière+1
si la dernière est < 9:
nxt = cur * 10 + dernier + 1
si nxt <= élevé:
q.annexe(nxt)

# Ajouter le dernier-1
si la dernière > 0:
nxt = cur * 10 + dernier - 1
si nxt <= élevé:
q.annexe(nxt)

retour trié(s)


♪ ----------------------------------------------------------------------------------
# Essai manuel rapide
♪ ----------------------------------------------------------------------------------
si __nom__ == "__main__" :
sol = Solution()
print(sol.countSteppingNumbers(0, 21)) # [0,1,2,3,4,5,6,7,8,9,10,12,21]
print(sol.countSteppingNumbers(10, 15)) # [10,12]
«» "

-----------------------------------------------------------------------------------

## C++ – `solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> countSteppingNumbers(int low, int high) {
vecteur<int> rés;

// 0 n'est un nombre de pas que s'il se trouve à l'intérieur de la plage
Si (faible) 0) res.push_back(0);

file d'attente <int> q;
pour (int d = 1; d <= 9; ++d) q.push(d); // commencer BFS à partir de 1..9

pendant que (!q.vide()) {
int cur = q.front(); q.pop();

si (cur >= faible && cur <= élevé)
res.push_back(cur);

// Si le nombre suivant dépasse le nombre élevé, arrêtez d'étendre
si (cur > haut / 10) continuer;

int last = cur % 10;

// Ajouter le dernier+ 1
si (dernier < 9) {
long long nxt = 1LL * cur * 10 + (dernier + 1);
si (nxt <= high) q.push(static_cast<int>(nxt));
}

// Annexe 1
si (dernier > 0) {
long long nxt = 1LL * cur * 10 + (dernier - 1);
si (nxt <= high) q.push(static_cast<int>(nxt));
}
}

tri(res.begin(), res.end());
retour rés;
}
};

/* ----------------------------------------------------------------------------------
* harnais d'essai rapide – compiler avec
* g++ -std=c++17 solution.cpp -o solution && ./solution
* ------------------------------------------------------------------ */
Int main() {
Solution sol;
auto v1 = sol.countSteppingNumbers(0, 21);
pour (int x : v1) cout << x << ' ';
cout << endl;

auto v2 = sol.countSteppingNumbers(10, 15);
pour (int x : v2) cout << x << ' ';
cout << endl;
}
«» "

-----------------------------------------------------------------------------------

♪ 2. Article du blog – Le bon, le mauvais et le mauvais de LeetCode 1215 (numéros d'étape)

> **Mots clés** – LeetCode 1215, nombres de pas, BFS, préparation d'entrevue, conception d'algorithmes, Java, Python, C++, entretien d'emploi

---

Présentation

Lorsque les recruteurs commencent à demander : Pouvez-vous résoudre le problème de nombre de pas ?
LeetCode 1215 est trompeurment simple : *trouver tous les entiers dans une plage où les chiffres adjacents diffèrent de 1*. Pourtant, ses contraintes (jusqu'à 2 × 109) et l'exigence de retourner les nombres dans l'ordre ** trié** donnent lieu à des pièges subtils.

Dans ce post, nous allons marcher à travers le **bon** (ce qui le rend élégant), le **mauvais** (erreurs courantes), et le **ugly** (symphonie de cas). Nous terminerons par une liste de contrôle pratique pour les chercheurs d'emploi : comment discuter du problème dans une entrevue et comment présenter votre code.

---

## Le problème, réaffirmé

> **Numero d'étape** – Un entier *x* où chaque paire de chiffres adjacents a une différence absolue de exactement 1.
> **Tâche** – Compte tenu des nombres entiers *bas* et *haut* (0 ≤ bas ≤ haut ≤ 2 × 109), retourner une liste triée de tous les nombres de marches dans la gamme inclusive [*bas*, *haut*].

Le défi n'est pas de trouver les nombres, mais de ** les générer efficacement** sans l'itérer sur chaque entier de la gamme.

---

## Le bon: Pourquoi BFS est le choix naturel

1. **Croissance semblable à celle des arbres**
Chaque nombre de marche peut être élargi en ajoutant un chiffre qui est ±1 loin de son dernier chiffre. Ceci forme un **trie** (arbre préfixe) de nombres valides.

2. **Profondeur apparente**
Le plus long nombre de pas sous 2 × 109 a au plus 10 chiffres. Par conséquent, l'arbre BFS a une profondeur ≤ 10, garantissant que la file d'attente n'explose jamais.

3. **Pas de nouvelle calcul**
BFS visite chaque numéro ** exactement une fois**. En revanche, un DFS naïf peut générer le même nombre via différents chemins si ce n'est prudent.

4. **Élagage naturel**
Avant d'interroger un enfant, nous pouvons vérifier si le nouveau nombre dépasserait *élevé*. Si oui, nous arrêtons d'explorer cette branche immédiatement.

5. **Simplicité**
L'algorithme de base se résume à une poignée de lignes (plus la plaque de queue habituelle). Les intervieweurs aiment le code *correcte, concis et clairement annoté*.

---

## Les mauvaises: erreurs courantes qui tuent votre solution

Pourquoi ça arrive ?
- Oui.
**Survol du cas 0**=0 est un nombre de pas, mais BFS qui commence de 1‐9 ne le génère jamais. Ajouter une vérification spéciale : si `faible == 0`, appuyez sur 0 dans la liste des résultats. Autres
**Utilisation du débordement d'int en C++** Digit` peut dépasser 2 × 109 (il convient toujours en 32-bit signé), mais la multiplication peut déborder si `cur` est grande. Utilisez `long long` pour les calculs intermédiaires, replacez `int` seulement après la vérification `<= high`. Autres
**Ne pas tailler avec `high / 10`**.La file d'attente peut croître indéfiniment si vous continuez à ajouter des chiffres même lorsque le nombre suivant déborde *high*. Autres
**En supposant que l'ordre BFS soit trié**.BFS visite les nœuds niveau par niveau, mais les nœuds à la même profondeur ne sont pas garantis être en ordre ascendant. Autres Triez le résultat final ou utilisez un `PriorityQueue` pour maintenir l'ordre pendant la traversée (coût). Autres
**Ignorer les limites 32-bit vs 64-bit**.En Java, `int` est 32-bit, donc 2 × 109 est sûr. Dans Python, pas de problème; dans C++ utiliser "long long" pour la sécurité. Gardez toujours le type de données conforme aux limites. Autres

---

- Oui. L'horrible : Tactiques et tri final

1. **Manipulation des chiffres *
* Lorsque le dernier chiffre est `9`, vous ne pouvez pas ajouter `10`.
* Quand il est `0`, vous ne pouvez pas ajouter `-1`.
Ils sont traités par les conditions "dernier Digit < 9" et "dernier Digit" Chiffre > 0 '.

2. ** Prévention en double**
L'arbre BFS peut produire le même nombre de parents différents si vous n'êtes pas prudent.
Avec les contraintes de profondeur (`cur > haut / 10`) et de chiffre, les duplicatas ne se produisent pas dans ce problème. Mais dans les variantes plus complexes, vous aviez besoin d'un `HashSet` pour dedupe.

3. ** Tri final**
Même si chaque nombre généré est unique, l'ordre BFS est **pas** en augmentation stricte. La correction la plus simple est `Collections.sort(result)` (Java), `sorted(res)` (Python), ou `sort(res.begin(), res.end())` (C++).
Alternativement, utilisez un `PriorityQueue` pendant la traversée – mais le facteur log supplémentaire l'emporte généralement sur les avantages.

---

Analyse de complexité

L'approche Temps Espace Remarques
C'est pas vrai.
**O( N )** où N est le nombre de nombres de pas ≤ élevé (= 2 × 109) **O( N )** pour la liste des files d'attente + résultats
DFS (récursive) : Même que BFS (profondeur de la pile de récursion) :
Brute-Force **O( high – bas )** Autres

Parce que `haut` peut être aussi grand que 2 × 109, *O(haut – bas)* est complètement impossible. BFS garantit un temps d'exécution qui dépend uniquement de la taille **output**.

---

Comment parler Dans une interview

1. **Énoncer clairement le problème** – Reformuler la définition d'un nombre d'étapes et le format de sortie requis.
2. **Choisissez BFS** – Mentionnez la propriété arborescente : à partir d'un nombre valide, vous pouvez seulement ajouter `last+1` ou `last-1`.
3. **Exposer la Queue Bound** – Montrez que si `cur > high / 10`, toute extension ultérieure déborderait, afin que vous puissiez arrêter.
4. **Edge Cases** – Ne pas oublier `0` et les limites de chiffres (`0` et `9`).
5. **Désormais** – Précisez que vous triez à la fin; BFS ne produit pas de nombres triés par défaut.
6. **Simplicité du code** – Gardez la solution courte, bien commentée, et discutez de toute préoccupation de type de données (Java `int` vs C++ `long').
7. **Demander des commentaires** – Si l'intervieweur suggère une solution de rechange (p. ex. en utilisant une file d'attente prioritaire), discuter des compromis.

---

## Liste de contrôle pour les demandeurs d'emploi

Étape Action Résultat
C'est pas vrai.
Rédiger des solutions multi-langues** Démontrer des compétences en Java, Python, C++
Ajouter **tests de l'unité**
Repères contre un testeur randomisé ** Générer des paires aléatoires basses/élevées, comparer votre sortie avec une force brute pour de petites gammes
Document **complexité temps/espace** Sur un tableau blanc ou README
Préparation ** points de discussion** – Bon/Bad/Ugly

---

Conclusion

LeetCode 1215 (Stepping Numbers) est un micro-gem** d'entrevues algorithmiques.
*Bien*: BFS exploite la propriété d'expansion naturelle et la profondeur limitée.
*Bad*: Des erreurs comme ignorer `0`, des contrôles de débordement manquants, ou supposer que l'ordre trié peut faire dérailler même une idée parfaite.
*Ugly*: La gymnastique et le tri final des caisses peuvent sembler banals, mais ils sont essentiels pour la justesse.

Votre arsenal de recherche d'emploi est maintenant prêt : vous pouvez **code** en Java, Python ou C++, et vous pouvez **expliquer** le raisonnement, les pièges et les optimisations.

Bonne chance – la prochaine interview pourrait être juste au coin de la rue, et vous allez entrer directement dans le succès! C'est ce qu'il a dit.

---

> *Soyez libre de partager cet article sur LinkedIn ou Twitter avec le hashtag #LeetCode1215 pour aider d'autres personnes à se préparer à leur prochaine interview. *

---

*Bon code ! *



---

**END**
-----------------------------------------------------------------------------------


> *Cet article a été écrit à l'origine pour la saison d'entrevue 2024. Tout le code est open-source sous la licence MIT (voir le lien du dépôt ci-dessus). *



---

Bonne chasse au travail !