---
titre: LeetCode 2453. Détruire les objectifs séquentiels -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* Les cibles séquentielles de Destroy – Une plongée profonde (Java / Python / C++)**

> **LeetCode #2453 – Détruire les cibles séquentielles* *
> **Difficulté:** Moyenne
> **Mots clés:** *hash map, modulo, comptage de fréquence, gourmandise, optimisation*

---

Récapitulation des problèmes

Vous êtes donné un tableau `nums` de **entiers positifs** et une valeur `espace`.
Si la machine avec n'importe quel "nums[i]`, elle peut détruire chaque cible qui égale

«» "
semis + c * espace (c ≥ 0, entier)
«» "

Votre objectif : **Détruire le nombre maximal de cibles**.
Retour **la plus petite valeur de graine** qui atteint ce maximum.

---

L'intuition – Pourquoi le Modulo est la clé

Tous les nombres qui sont congruent modulo "espace" peuvent être détruits par la même graine**.
Par exemple, avec "espace = 2" :

«» "
1, 3, 5, 7, ... → 1 mod 2
2, 4, 6, 8, ... → 0 mod 2
«» "

* La machine ne se soucie que du reste de chaque cible lorsqu'elle est divisée par « espace ».
* Par conséquent, le problème se résume à:
* **Combien de fois chaque reste apparaît** en "nums".
* Choisissez le reste avec le nombre le plus élevé (années → plus petite valeur originale).

La règle "destroy" est basée sur *équivalence-classe* et non sur une plage séquentielle. C'est la magie derrière la solution modulo.

---

Algorithme (O(n) Temps, O(k) Espace)

1. **Fréquences des pays* *
Calculer une fois à travers `nums`, calculer `r = nums[i] % espace`, incrémenter un compteur de cartes de hachage.

2. **Trouver le reste optimal* *
* `maxFreq` = fréquence maximale trouvée.
* `réponse` = minimum `nums[i]` parmi tous les nombres dont le reste est égal à "maxFreq".

3. Retourner la réponse.

Parce que `espace` peut être aussi grand que \(10^9\) mais que la longueur du tableau n'est que jusqu'à \(10^5\), la carte contiendra au maximum les entrées \(10^5\) – parfaitement bien.

---

Mise en œuvre

#### 4.1 Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
public int détruireTargets(int[] nums, int espace) {
// Étape 1: tableau de fréquence des restes
Carte<integer, integer> freq = nouveau HashMap<>();
int maxFreq = 0;
pour (int n : nombres) {
int r = n % d'espace;
int newFreq = freq.merge(r, 1, Integer::sum); // même que freq.getOrDefault(r,0)+1
si (newFreq > maxFreq) maxFreq = newFreq;
}

// Étape 2: trouver des graines minimales avec cette fréquence
réponse int = entier. MAX_VALEUR;
pour (int n : nombres) {
int r = n % d'espace;
si [freq.get(r)] maxFreq && n < réponse) {
réponse = n;
}
}
réponse de retour;
}
}
«» "

**Pourquoi "merger"?**
`merger` à la fois les inserts et les mises à jour dans un appel. Il est plus propre que `put/getOrDefault`.

---

#### 4.2 Python (3)

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def deathTargets(self, nombres: List[int], espace: int) -> Int:
# Fréquence de chaque reste
freq = compteur([x % d'espace pour x en nombres])
max_freq = max(freq.values())

# Graines minimales parmi les nombres appartenant au reste le plus fréquent
réponse = min(
(x pour x en nombres si freq[x % d'espace] == max_freq),
par défaut=0
)
réponse de retour
«» "

*`min()` avec un générateur maintient la mémoire faible. *
Si tous les nombres sont de longueur zéro (impossible par des contraintes), `default` assure la sécurité.

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int destructTargets(vecteur<int>& nums, espace int) {
unordered_map<int, int> freq;
int maxFreq = 0;

pour (int n : nombres) {
int r = n % d'espace;
int f = ++freq[r]; // incrémenter et stocker une nouvelle valeur
si (f > maxFreq) maxFreq = f; // fréquence maximale de piste
}

réponse int = INT_MAX;
pour (int n : nombres) {
int r = n % d'espace;
si (freq[r] == maxFreq && n < réponse)
réponse = n;
}
réponse de retour;
}
};
«» "

*C++17+ optionnel `unordered_map` construit par défaut à 0, donc `++freq[r]` fonctionne hors de la boîte. *

---

Analyse de complexité

Démarche Temps Espace supplémentaire
- C'est quoi ?
Java (un pass + un pass)
Python "O(n)" Autres
* C++ * O(n) * O(k) * Autres

Les trois solutions conviennent parfaitement aux limites (`n ≤ 105`).

---

# # # 6 Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Concept** Aucun – la logique est linéaire. Vous le prenez mal pour une force brute d'O(n2). Autres
**Mise en œuvre**=L'utilisation de la carte de hachage propre.=Le terme "merge" de Java peut ne pas être familier avec les débutants. C++ `unordered_map` peut obtenir une attaque *hash collision* dans de rares cas (sans importance pour LeetCode). Autres
**Cas d'Edge**= Fonctionne avec un très grand "espace" (pas d'attribution de réseau). Si `espace` > max(nums), tous les restes sont uniques – toujours corrects, mais peuvent confondre les nouveaux venus. Autres
Un facteur linéaire mais petit constant. Autres

**Ligne de bottom:** La solution modulo-fréquence est l'approche *correcte* et *optimale*. Évitez les pièges en s'en tenant à une carte de hachage et à un seul passage.

---

## 7-=SEO-Takeaway optimisé

- **Mots-clés:** Destroy Sequential Targets, LeetCode 2453 solution, ...
- **Méta—description:** Découvrez comment résoudre le LeetCode 2453 – Destroy Sequential Targets – avec un temps linéaire, l'algorithme O(n) utilisant le comptage de fréquence modulo. Des exemples complets de code Java, Python et C++, une analyse de complexité et un guide convivial SEO. (en milliers de dollars)

---

- Oui. Réflexions finales

- Oui. L'essence du problème est **classes d'équivalence modulo `espace`**.
- Une seule passe pour compter les fréquences, suivie d'une seconde passe pour choisir la graine minimale, donne la solution optimale.
- Oui. Le même motif (modulo → fréquence → tie-break gourmand) réapparaît dans de nombreux problèmes de LeetCode : *Maximum Subarray avec Mod*, *Longest Substring avec K Distinct*, etc.

Bon codage ! C'est ce qu'il a dit