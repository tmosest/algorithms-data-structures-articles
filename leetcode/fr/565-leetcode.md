---
titre: LeetCode 565. Arrayage - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 565. Array Nesting – Java / Python / C++ Solutions + Blog In‐Depth

> **Objectif** – Promenez-vous à travers une solution propre O(n) à LeetCode 565 et montrez-vous un article **blog** qui est **SEO-friendly** afin que vous puissiez atterrir une interview technique.

---

Récapitulation des problèmes (Code de bord 565)

On vous donne une permutation "nums" de longueur `n` (`0 ... n‐1`).
Pour chaque index `k`, construire un ensemble

«» "
s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], ... }
«» "

arrêter quand une valeur se répète.
Retourne la longueur maximale ** de tous ces ensembles.

---

- Oui. Aperçu clé

Parce que "nums" est une permutation, suivre les indices de n'importe quel point de départ formera un **cycle**.
Ainsi le problème se réduit à : *trouver le plus long cycle dans un graphique dirigé où chaque noeud a exactement un bord sortant. *

Vous pouvez détecter les cycles **en place** en marquant les nœuds visités (p. ex. en les configurant à une valeur sentinelle).
Cela donne **O(n)** temps et **O(1)** espace supplémentaire.

---

- Oui. Code de référence (Java / Python / C++)

On trouvera ci-dessous des implémentations autonomes prêtes à être collées.
Tous les trois suivent la stratégie de marquage en place.

---

#### 3.1 Java

"Java
solution de classe publique {
tableau d'entrée publicNesting(int[] nums) {
Int maxLen = 0;
Int final MARK = entier.MAX_VALUE; // sentinelle pour visite

pour (int i = 0; i < nombres de longueur; i++) {
si (nums[i] == MARK) continue; // déjà visité

début int = i;
nt currLen = 0;

// marcher le cycle, marquer les indices visités
pendant que (nums[start] != MARQUE) {
int next = nombres[départ];
nums[start] = MARK; // marque visitée
début = suivant;
pour Len++;
}
maxLen = Math.max(maxLen, currLen);
}
retour maxLen;
}
}
«» "

> **Pourquoi `int start = i`? **
> La boucle externe commence à chaque index; `start` suit la chaîne.
> Marquage avec des garanties `MARK` nous ne revisitons jamais un noeud.

---

3.2 Python

'`python
Solution de classe:
def arrayNesting(self, nombres: List[int]) -> Int:
max_len = 0
MARQUE = flotteur('inf') # sentinelle pour visite

pour i dans la plage(len(nums)):
si des nombres [i] == MARQUE:
poursuivre

curr = i
cnt = 0
alors que nums[curr] != MARQUE:
nxt = nombres[curr]
nombres[curr] = MARQUE # marque visitée
pourr = nxt
cnt += 1

max_len = max_len, cnt)

_retourner maxlen
«» "

> **Astuce** – Utiliser `float('inf')' fonctionne parce que toutes les valeurs du tableau sont `< n`.

---

### 3.3 C++

'`cpp
solution de classe {
public:
tableau intNesting(vector<int>& nums) {
const int MARK = INT_MAX; // sentinelle
Int maxLen = 0;

pour (int i = 0; i < nums.size(); ++i) {
si (nums[i] == MARK) continue; // déjà visité

nt curr = i;
cnt = 0;
pendant que (nums[curr] != MARQUE) {
Int nxt = nombres[curr];
nombres[curr] = MARK; // marque visitée
curr = nxt;
++cnt;
}
maxLen = maxLen, cnt;
}
retour maxLen;
}
};
«» "

> **Pourquoi `INT_MAX`?**
> Tous les éléments sont dans `[0, n-1]`, de sorte que `INT_MAX` est un marqueur sûr.

---

Article du blog – Array Nesting: The Good, The Bad, and The Ugly

> **Référencement à des mots clés* *
> *LeetCode 565 Nesting*, *solution de nidification d'arras*, *Java Python C++*, *Questions d'entrevue de LeetCode*, *explication de nidification d'arras*, *détection du cycle graphique*, *solutions optimales de LeetCode*

---

4.1 Introduction

> *LeetCode 565 – Array Nesting* est un puzzle apparemment simple qui vous apprend beaucoup sur **graph traversal**, **cycle de détection** et **algorithmes en place**. Dans cet article, je vais passer par le problème, la solution la plus propre, les pièges (-) et les cas de bord moins évidents (-). À la fin, vous serez prêt à répondre à cette question dans une interview.

---

4.2 Énoncé du problème (réécrit)

> Vous recevez un tableau entier `nums` de longueur `n` où chaque valeur est un entier unique dans `[0, n-1]`.
> Pour tout indice de départ `k`, définir une séquence: `nums[k]`, `nums[nums[k]]`, `nums[nums[nums[k]]]`, ...
> Arrêtez **avant** vous répéteriez une valeur.
> Retourne la longueur maximale de toutes ces séquences.

> **Exemples**

Nombres d'extrants Explication
C'est quoi ?
Un ensemble plus long: "{5,6,2,0}" Autres
Chaque élément forme une boucle de soi. Autres

---

### 4.3 La bonne : Compte du cycle de localisation

1. **Observation** – Le tableau est une permutation → chaque noeud a hors-degré 1 → le graphique est une collection de cycles disjoints.
2. **Objectif** – Trouvez le plus long cycle.
3. **Méthode** – Marcher de chaque nœud non visité, marquant les nœuds visités avec une sentinelle (`INT_MAX` / `float('inf')`).
4. **Complexité** –
*Time*: `O(n)` – chaque élément visité au plus une fois.
*Espace*: "O(1)" – seulement quelques variables entières (pas de conteneur supplémentaire).

> Cette approche est *la norme d'or* pour les entrevues : elle utilise une mémoire supplémentaire minimale et démontre une compréhension profonde des cycles graphiques.

---

### 4.4 Le "Bad" : Naïve HashSet ou Récursion

Pourquoi ça va mal
C'est pas vrai.
**HashSet** – Pour chaque `k` utiliser un `HashSet` pour enregistrer les valeurs visitées. "O(n)" espace supplémentaire par itération; dans le pire des cas, "O(n^2)" total s'il est appliqué incorrectement. Autres
**Récursive DFS** – Suivez de façon récursive les "nums" jusqu'à ce qu'ils se répètent. La profondeur de la cheminée peut atteindre `n`; risque de débordement de la cheminée pour les gros intrants (`n ≤ 105`). Autres

> Même si ceux-ci passent sur LeetCode, ils sont *unidiomatiques* pour les intervieweurs à la recherche de solutions efficaces.

---

### 4.5 Les cas de bord et les subtilités

Numéro Explication
- Oui.
**Collision deentielle** – Utilisation d'une valeur qui pourrait apparaître dans "nums". Dans ce problème toutes les valeurs `< n`, donc utiliser `INT_MAX` est sûr. Autres
**Large `n`** – Dépassement de la profondeur de récursion ou du marquage. Tenir aux boucles itératives. Autres
**Input de non-permutation** – LeetCode garantit une permutation, mais si vous devez généraliser, vous devez gérer des valeurs répétées ou des nombres manquants. Autres Utilisez un tableau `visited` ou un haschset pour garder. Autres

> La manipulation de ces subtilités montre maturité et attention au détail.

---

### 4.6 Passage du code (exemple de Java)

"Java
pour (int i = 0; i < nombres de longueur; i++) {
si (nums[i] == MARK) continue; // déjà visité

nt curr = i;
cnt = 0;
pendant que (nums[curr] != MARQUE) {
int next = nombres[curr];
nombres[curr] = MARQUE; // marque telle que visitée
curr = suivant;
cnt++;
}
maxLen = Math.max(maxLen, cnt);
}
«» "

*Chaque boucle `alors` suit un cycle distinct, ne revisite jamais aucun noeud parce que nous l'écraserons immédiatement avec la sentinelle. *

---

4.7 Conseils pour l'optimisation

Conseil Indemnité
- Oui.
**Utiliser `int` sentinelle** – `INT_MAX` ou `-1`" Évite d'attribuer un grand tableau auxiliaire. Autres
**Itérer en place** – Ne pas créer de nouvelles listes. Autres
**Profil** – Pour les très grands tableaux, vérifiez que la mise à jour sentinelle est alignée par le compilateur JVM/C++. Supprime les frais généraux cachés. Autres

---

### 4.8 Foire aux questions (FAQ)

Question Réponse
C'est pas vrai.
*Puis-je utiliser un HashSet pour marquer les nœuds visités?*= Oui, mais cela coûte de l'espace supplémentaire `O(n). Préférez le sentinelle en place. Autres
*La sentinelle modifiera-t-elle l'entrée pour les appels suivants?*=Dans LeetCode, chaque cas de test est isolé. Pour les projets réels, copiez d'abord le tableau. Autres
*Pourquoi ne pas utiliser Floyd? Il trouve un cycle commençant par un nœud spécifique, mais vous devez encore explorer tous les nœuds. Le marquage en place est plus simple. Autres

---

###4.9 Conclusion

> Le problème LeetCode 565 (Array Nesting) est une illustration classique de la détection du cycle** dans un graphique fonctionnel.
> En marquant les nœuds visités *en place*, nous obtenons **O(n) temps** et **O(1) espace**, qui est la solution la plus conviviale pour l'entrevue.
> Évitez les approches naïves HashSet ou récursives; elles sont --- pour la performance et la sécurité de la pile.
> Enfin, rappelez-vous les cas de bord (collisions deentielle, gros intrants) – les manipuler impressionnera les gestionnaires d'embauche.

> **Prochaines étapes**
> 1. Pratiquer le même modèle sur des problèmes comme -Nombre d'îles - ou -Liste liée Cycle -.
> 2. Partagez votre solution sur GitHub et écrivez un court blog (comme celui-ci) pour présenter votre processus de pensée.
> 3. Préparez-vous à expliquer l'approche dans un discours d'entrevue de 5 minutes.

Bon codage !

---

C'est pas vrai. Référence rapide – Meta pour moteur de recherche

Contenu du champ
C'est quoi ?
*Titre **= Arrayage du nid – LeetCode 565 Solution en Java, Python, C++
**Description**Découvrez l'algorithme optimal en place pour LeetCode 565. Full Java, Python, et C++ implémentations + interview-ready blog post. Autres
LeetCode 565, nicher dans un tableau, détection du cycle graphique, solution Java, solution Python, solution C++, codage d'entretien, algorithme O(n), problèmes optimaux LeetCode Autres
**URL Slug**

> L'inclusion de ces méta tags aidera les recruteurs à rechercher la solution de Nesting d'Array.

---

> ** Bonne chance pour vos interviews de codage!* *