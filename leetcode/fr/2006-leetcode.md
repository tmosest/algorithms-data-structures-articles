---
titre: LeetCode 2006. Nombre de paires avec différence absolue K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code

Ci-dessous sont trois solutions idiomatiques qui fonctionnent dans **O(n)** temps et **O(1)** espace supplémentaire (une table de fréquences de taille constante ou une carte de hachage).

Solution
C'est pas vrai.
*Java** Autres
**Python**
*C++**

---

### 1.1 Java – `Solution.java "

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
nombre d'entrées publiquesKDifférence(int[] nombres, int k) {
// Carte de fréquence : numéro -> son compte en nombres
Carte<integer, integer> freq = nouveau HashMap<>();

pour (int num : nombres) {
freq.put(num, freq.getOrDefault(num, 0) + 1);
}

nombre int = 0;
pour (int num : nombres) {
// Ne cherchez que num + k (la paire i < j garantit que nous ne doublerons pas)
cible int = num + k;
Total tCnt = freq.get(cible);
si (tCnt != null) {
nombre += tCnt;
}
}
le nombre de retours;
}
}
«» "

---

### 1.2 Python – `solution.py "

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

def countKDifférence(nums: List[int], k: int) -> Int:
freq = compteur(s) # O(n) temps, O(1) espace supplémentaire (max 100 clés distinctes)
nombre = 0
pour num in nums:
nombre += freq.get(num + k, 0)
Nombre de retours
«» "

---

### 1.3 C++ – `solution.cpp "

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>

solution de classe {
public:
nt countKDifférence(std::vector<int>& nums, int k) {
std::unordered_map<int, int> freq;
pour (int num : nums) freq[num]++; // construire la carte freq

Int ans = 0;
pour (int num : nombres) {
auto it = freq.find(num + k);
si (it != freq.end()) ans += it->seconde;
}
le retour des an;
}
};
«» "

> **Pourquoi ça marche* *
> Nous comptons chaque élément *once* et ajoutons le nombre d'occurrences de la valeur qui est exactement `k` plus grande. Parce que nous regardons seulement vers l'avant (`num + k`) la paire `(i, j)` avec `i < j` est comptée exactement une fois, pas de double comptage et pas de boucles imbriquées.

---

- Oui. 2. Article du blog

**Titre:**
* Nombre de paires avec différence absolue K – Le bon, le mauvais et le mauvais (Java/Python/C++)* *

**Description détaillée (SEO):* *
Master LeetCode 2006 en Java, Python et C++ avec une solution O(n). Apprenez les pièges, la manipulation des cas de bord et comment répondre à cette question d'entrevue. Parfait pour les ingénieurs logiciels de chasse.

---

2.1 Introduction

Vous avez obtenu un entretien de codage et l'intervieweur demande :
*=Avec un tableau `nums` et un entier `k`, compter les paires (i, j) où i < j and='nums[i] – nums[j]=== k.=*

Il s'agit du LeetCode 2006 – un problème apparemment simple de la différence-k. Dans ce post, nous disséquons le **good**, le **bad** et le **ugly**, et nous fournissons une solution propre et prête à la production en **Java, Python et C++**.

---

### 2.2 Énoncé du problème (clair et concis)

- **Input**
- "nums" : entier, longueur 1 ≤ n ≤ 200
- "k" : 1 ≤ k ≤ 99
- `1 ≤ nombres[i] ≤ 100`

- ** Sortie**
- Le nombre de paires d ' indices `(i, j)` où `i < j` et `=nums[i] - nums[j]=== k`.

- **Exemples**

Numéros de réponse
C'est pas vrai.
[1,2,2,1]
Aucune paire
[3,1,5,4]

---

2.3 La bonne solution – O(n)

**Idée** – Utilisez une table de fréquence (ou une carte de hachage) pour se rappeler combien de fois chaque nombre apparaît. Pour chaque élément `x`, le seul partenaire qui peut former une paire valide est `x + k` (parce que nous appliquons `i < j`). En ajoutant `freq[x + k]` à la réponse pour chaque `x`, nous obtenons le nombre total en temps linéaire.

Pourquoi c'est bon

Motif
C'est pas vrai.
**Heure**="O(n)" – deux passes linéaires, sans boucles imbriquées="
**L'espace**= `O(1)` – tableau de taille fixe (100 valeurs) ou `O(1)` pour carte de hachage (max. 100 clés)=
**Clarté** nombre de fréquences → scanner une fois de plus
**Échelle**= Fonctionne pour `n` jusqu`à des millions (toujours linéaire)=
*Testabilité *Test facile à tester avec de petits aides

Cas de bord traités

Explication
- C'est quoi ?
Les contraintes du problème interdisent `k = 0` (k ≥ 1), donc aucune manipulation particulière n'est requise. Autres
Des valeurs dupliquées Une carte de fréquence compte automatiquement la multiplicité. Autres
Négatif "k" Non autorisé, mais si présent, la formule fonctionnerait encore parce que la différence absolue est symétrique. Autres
Élément max Le tableau de fréquence de la taille 101 est suffisant. Autres

---

2.4 La mauvaise – Force de Brute Quadratique

Une approche commune mais naïve:

'`python
def bad(nums, k):
nombre = 0
pour i dans la plage(len(nums)):
pour j dans la plage(i + 1, len(nums)):
Si abs(nums[i] - nums[j]) == k:
nombre += 1
Nombre de retours
«» "

C'est vrai. Pourquoi c'est mauvais

- **O(n2)** – Pour `n = 200`, toujours très bien, mais pour les scénarios d'entrevue vous pouvez affronter des tableaux jusqu'à 105.
- **Hard to Optimize** – Deux boucles imbriquées donnent peu de place pour une sortie anticipée à moins d'ajouter une taille complexe.
- **Readability** – L'intention est évidente, mais l'inefficacité montre un manque de pensée algorithmique.

---

2.5 La mauvaise utilisation de la radiofréquence

Parfois, les gens utilisent un tableau de fréquence mais oublient de rendre compte des paires de ** duplicata** ou de la contrainte **i < j**, ce qui entraîne un double comptage :

"Java
int[] freq = nouvelle int[101];
pour (int x : nombres) freq[x]++;

Int ans = 0;
pour (int x : nombres) {
si (x + k <= 100) ans += freq[x + k]; // faux si nous avons également compté freq[x] plus tôt
}
«» "

**Résultat** – compte chaque paire deux fois. La correction est de ** seulement ajouter** une fois par occurrence de `x`. C'est pourquoi nous:
- Itérer sur la carte *fréquence* elle-même: `pour (int x : freq) ans += freq[x] * freq[x + k]` (et diviser par 2 si k = 0).
- Oui. Ou gardez la boucle originale mais comptez sur `i < j` implicitement (en scannant le tableau original et en regardant seulement `x + k`).

---

#### 2.6 Passage complet – Code Java expliqué

"Java
nombre d'entrées publiquesKDifférence(int[] nombres, int k) {
// Créer une table de fréquence
int[] freq = nouvelle int[101]; // indices 1..100
pour (int n : nombres) freq[n]++;

Int ans = 0;
// Pour chaque élément, compter les partenaires qui sont k plus grands
pour (int n : nombres) {
cible int = n + k;
si (cible <= 100) ans += freq[cible];
}
le retour des an;
}
«» "

* Points clés: *

1. **Rayon de taille fixe** – évite le hachage au-dessus, grâce au «nums[i] ≤ 100».
2. ** Pass unique pour peupler** – Ops mémoire O(n).
3. **Deuxième passe** – nous ne regardons vers l'avant (`n + k`), donc chaque paire valide contribue exactement une fois.

---

2.7 Analyse de complexité (toutes langues confondues)

Mesure O(n) Solution
- C'est quoi ?
Temps **O(n)**
Espace supplémentaire
Le pire des cas

Parce que les contraintes sont minuscules, toutes les langues atteignent la même complexité asymptotique. Mais pour un ensemble de données plus grand ou interview, la solution linéaire est la seule pratique.

---

2.8 Pièges et conseils communs

Piège
- Oui.
**Comptabilité double**. Autres
**Off‐by‐one dans le tableau**= Lors de l'utilisation d'un tableau fixe, assurez-vous que les indices couvrent toute la gamme (1–100). Autres
**En supposant que k ≥ 0** Le problème garantit `k ≥ 1`, mais en général vous avez besoin de gérer k ou `k == 0`. Autres
**Ignorer les limites d'entrée**= Une carte de hachage est plus sûre lorsque les valeurs peuvent être grandes; mais si les limites sont petites, un tableau de fréquence est plus rapide. Autres
Si elle est autorisée, utiliser `freq[x] * (freq[x] - 1) / 2` pour éviter le double comptage. Autres

---

2.9 Prise- Loin

- Utilisez une carte **fréquence** (ou un tableau) pour réduire le problème de vérification des paires à un seul balayage linéaire.
- La condition **i < j** est naturellement appliquée en cherchant seulement `num + k`.
- Gardez votre solution **compact** et **bien documenté** – les intervieweurs apprécient le raisonnement clair autant que le code correct.

---

### 2.10 Mots-clés du référencement

- LeetCode 2006
- Nombre de paires avec différence absolue K
- Solution Java LeetCode 2006
- Solution Python LeetCode 2006
- Solution C++ Code Leet 2006
- Algorithme de comptage des paires O(n)
- questions de codage des entretiens
- résolution de problèmes algorithmiques
- questions d'entrevue sur la structure des données
- algorithme de table de fréquence

---

2.11 Conclusion

Le problème du nombre de paires avec différence absolue de K est un puzzle d'interview classique qui teste votre compréhension du comptage **fréquence**, des cartes deash** et de l'efficacité algorithmique**. En fournissant une solution O(n) propre en Java, Python et C++, vous ne résolvez pas seulement le problème, mais montrez également la capacité de repérer et corriger les mauvais et les mauvais modèles communs. Bonne chance pour ce travail, et un codage heureux!