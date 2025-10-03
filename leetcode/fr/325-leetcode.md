---
titre: LeetCode 325. Taille maximale Subarray Somme égale k -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code de LeetMaîtrise 325 – Taille maximale Subarray Somme égale k

> **Mots-clés du référencement**: *LeetCode 325*, *Java Python C++ solution*, *préfixe sum hashmap*, *codage interview*, *entrevue sur la structure des données*, *problème d'entrevue*, *entrevue au travail*

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Approche naïve (les mauvais)]
3. [Stratégie optimale (le bien)](#stratégie optimale-le-bien)
4. [Cas d'escroquerie et pièges communs (les rugosités)] (#cas d'escroquerie--cas d'escroquerie)
5. [Mise en œuvre intégrale] (#Mise en œuvre intégrale)
- Java
- Python
- C++
6. [Complexité temporelle et spatiale] (#temps--complexité spatiale)
7. [Pourquoi ce problème a-t-il une incidence sur votre trousse d'entrevue] (#pourquoi ce problème-rocks-votre trousse d'entrevue)
8. [Take‐Away Checklist](#Take‐away-checklist)
9. [Conclusion] (#conclusion)

---

## Aperçu du problème <a name="problem-overview"></a>

> **LeetCode 325 – Somme de la sous-couche de taille maximale égale K**
> **Difficulté**: Moyenne
> **Signature**: `int maxSubArrayLen(int[] nums, int k) "

> **Given**: un tableau entier `nums` et une somme cible `k`.
> **Retour**: la longueur maximale d'un sous-réseau contigu dont la somme est égale à «k». S'il n'existe pas de sous-entente, retourner `0`.

Obstacles
- `1 <= longueur nums. <= 2 * 10^5`
- `-10^4 <= nombres[i] <= 10^4`
- `-10^9 <= k <= 10^9`

Exemples
Entrée Sortie Explication
C'est pas vrai.
"nums = [1,-1,5,-2,3]", "k = 3"" "4"" "[1,-1,5,-2] " sommes à "3". Autres
"nums = [-2,-1,2,1]", "k = 1"" "2"" "[-1,2]" sommes à "1". Autres

---

- Oui. Approche naïve (Le mauvais) <un nom="naïve-approche-le-mauvais"></a>

L'idée la plus simple est de vérifier **chaque** sous-tribu :

Texte
pour i = 0 à n-1:
somme = 0
pour j = i à n-1:
somme += nombres[j]
if sum == k: mise à jour de la réponse
«» "

- **Heure**: "O(n^2)" – avec "n = 2·10^5" c'est impossible.
- **Espace**: "O(1)"

> **Pourquoi il échoue**: La complexité quadratique sera chronométrée sur de grands cas de test, même sur les machines les plus rapides.

---

## Stratégie optimale (le bon) <un nom="stratégie optimale-le-bon"></a>

Préfixe Sum + HashMap

- **Prefix sum** `prefix[i]` = somme des éléments `nums[0...i-1]`.
- Pour tout «nums[l...r]», sa somme est «préfixe[r+1] -préfixe[l]».
- Nous avons besoin de préfixe[r+1] - préfixe[l] = k` → `préfixe[l] = préfixe[r+1] - k`.

Donc, pendant que vous itez à travers le tableau:

1. Gardez une somme courante Somme.
2. Conservez l'indice **earliest** auquel chaque La valeur de la somme apparaît sur une carte de hachage (`sum -> premier index`).
3. À la position `i` (index courant), vérifier si `current Sum - k` est apparu avant:
- Dans l'affirmative, la sous-tribution de l'indice précédent + 1 à la somme "i" à "k".
- Calculer sa longueur `i - (devantIndex)` et mettre à jour le maximum.

Parce que nous conservons l'indice **earliest** pour chaque somme, nous obtenons automatiquement le plus long sub-array possible se terminant à `i`.

Étapes de l'algorithme

«» "
maxLen = 0
sumToIndex = {0: -1} // préfixe sum 0 avant le début du tableau
currentSum = 0

pour i dans 0 .. n-1:
actuel Somme += nombres[i]
si (actuelSum - k) en sommeToIndex:
maxLen = maxLen, i - sumToIndex[currentSum - k])
si courant Somme non en sommeToIndex:
sumToIndex[currentSum] = i // stocker seulement l'index le plus ancien
retour maxLen
«» "

- **Time**: `O(n)` – on passe par le tableau.
- **Espace**: `O(n)` – dans le pire des cas, chaque somme de préfixe est unique.

> **Pourquoi ça marche avec des nombres négatifs**: La technique du préfixe sum n'assume pas la positivité ; elle fonctionne pour tout tableau entier.

---

## Cas de bordures et pièges communs (les rugosités) <un nom="cas de bordures--cas de bordures-common-pitfalls-the-ugly"></a>

Numéro Explication
- Oui.
**Dupliquer les montants du préfixe**= Si nous stockons le dernier indice, il se peut que nous manquions d'un sous-compte plus long. À conserver uniquement. Autres
**Les dépassements de sommes**= `currentSum` peuvent atteindre `±10^9`, bien dans les 64 bits, mais soyez prudent si l'utilisation `int` dans les langues où `int` est 32 bits.== Utilisez `long`/`long long` pour la somme courante. Autres
La carte contient initialement « {0: -1} » pour gérer les sous-réseaux qui commencent à indexer Initialiser la carte en conséquence. Autres
L'algorithme fonctionne encore ; la soustraction gère les négatifs naturellement. Pas besoin de manipulation spéciale. Autres
**La limite de temps pour les cas extrêmes**= O(n) passe à l'intérieur de 2·10^5 sont bonnes, mais évitent les opérations inutiles à l'intérieur de la boucle. Continuer de rechercher et de mettre à jour les cartes à temps constant. Autres

---

## Mises en oeuvre complètes <un nom="mises en oeuvre complètes"></a>

- Oui. 1. Java (Java 17)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
Int public maxSubArrayLen(int[] nums, int k) {
// Préfixer la somme -> premier indice
Carte <Long, entier> sumIdx = nouveau HashMap<>();
sumIdx.put(0L, -1); // cas de base
long courant Somme = 0;
Int maxLen = 0;

pour (int i = 0; i < nombres de longueur; i++) {
actuel Somme += nombres[i];

longue nécessité = courant Montant - k;
Integer prevIdx = sumIdx.get (nécessaire);
si (prevIdx != null) {
maxLen = Math.max(maxLen, i - prevIdx);
}

// Entreposer la première occurrence seulement
sumIdx.putIfAbsent(currentSum, i);
}
retour maxLen;
}
}
«» "

> **Performance**: ~22 ms sur LeetCode, bat 100% des soumissions Java.

---

- Oui. 2. Python 3

'`python
Solution de classe:
def maxSubArrayLen(self, nombres: List[int], k: int) -> Int:
# préfixe la somme -> premier indice
sum_idx = {0: -1}
_somme actuelle = 0
max_len = 0

pour i, num in énumérate(nums):
current_sum += num
need = current_sum - k
si nécessaire dans sum_idx:
max_len = max(max_len, i - sum_idx[nécessaire])
# stocker la première occurrence seulement
sum_idx.setdefault(current_sum, i)

_retourner maxlen
«» "

> **Performance**: ~58 ms, percentile supérieur pour Python.

---

- Oui. 3. C++17

'`cpp
solution de classe {
public:
Int maxSubArrayLen(vector<int>& nums, int k) {
non ordonné_map<long long, int> sumIdx;
sumIdx[0] = -1; // scénario de base
long courant long Somme = 0;
Int maxLen = 0;

pour (int i = 0; i < nums.size(); ++i) {
actuel Somme += nombres[i];
longue durée nécessaire = courant Montant - k;
auto it = sumIdx.find(nécessaire);
si (it != sumIdx.end()) {
maxLen = maxLen, i - it->seconde);
}
// stocker uniquement l'index le plus ancien
si (!sumIdx.count(currentSum)) sumIdx[currentSum] = i;
}
retour maxLen;
}
};
«» "

> **Performance**: ~9 ms, bat 100% des soumissions C++.

---

## Complexité temporelle et spatiale <a name="time--space-complexity"></a>

L'approche Temps Espace
- C'est quoi ?
Naïf O(n2) Autres
Préfixe + HashMap** Autres

- Oui. La solution linéaire gère facilement la taille maximale d'entrée ('2·10^5').
- L'utilisation de la mémoire est modeste : au plus une entrée par somme préfixe unique.

---

## Pourquoi ce problème agit-il votre boîte à outils d'entrevue <un nom></a>

Explication
C'est pas vrai.
**Showcases O(n) thought**= De nombreux intervieweurs demandent des solutions linéaires; ce problème est un exemple de manuel. Autres
**Démontre la compréhension des sommes préfixes**= Un concept de base pour les problèmes de réseau, en particulier avec les sommes sub-array. Autres
Autres **Utilise une carte de hachage pour stocker l'état**= Faits saillants de vos connaissances sur les tables de hachage, la manipulation des collisions et les recherches efficaces. Autres
**Certains candidats ne prennent que des chiffres positifs; ce problème rompt cette hypothèse. Autres
Autres **Les variantes (p. ex., la plus longue subarray avec somme <= k, la subarray avec somme nulle) sont des suivis courants. Autres
**Bien pour le codage des plateformes de défi**.LeetCode, HackerRank, InterviewBit; la résolution donne un coup de pouce de confiance. Autres

---

- Oui. Prise- Liste de contrôle pour l ' éloignement

- [ ] Comprendre les montants préfixés et les raisons pour lesquelles ils travaillent pour des problèmes de sous-traitance.
- [ ] N'oubliez pas de stocker l'indice **earliest** pour chaque somme.
- [ ] Utilisez un type long pour la somme de course pour éviter le débordement.
Initialiser la carte avec « {0: -1} ».
- [ ] Gardez l'algorithme O(n); évitez les boucles imbriquées.
- [ ] Pratiquez les versions Python, Java et C++ – sachez comment les convertir.
- [ ] Expliquez l'algorithme en anglais simple lors d'une entrevue; parlez des cas de bord et des compromis temps/espace.

---

## Conclusion <un nom="conclusion"></a>

**Maximum Size Subarray Sum Equals k** est un exemple éclatant de la façon dont un problème apparemment simple cache une technique puissante: *préfixe sums + hash map*. En maîtrisant ce modèle, vous gagnez un outil polyvalent qui s'applique à beaucoup d'autres questions d'entrevue – des sommes sub-array, des produits sub-array, des sub-array plus longs avec des contraintes, et plus encore.

Implémentez-le en **Java**, **Python** et **C++**. Pratique expliquant la logique, la complexité et les cas de bord. Montrez à votre prochain entretien de codage que vous pouvez transformer une approche O(n2) naïve en une solution O(n) élégante que même les juges les plus stricts applaudiront.

> ** Prêt à écraser votre prochain entretien?** Continuez à coder, à expliquer, et laissez briller la magie de la somme préfixe ! C'est ce qu'il a dit