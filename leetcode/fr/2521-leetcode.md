---
titre: LeetCode 2521. Facteurs principaux distincts du produit d'array -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes
**2521. Facteurs principaux distincts du produit d'array* *
Compte tenu d'un tableau "nums" d'entiers positifs (`2 ≤ nums[i] ≤ 1000`), retourner le nombre de **facteurs principaux distincts** qui apparaissent dans le produit de tous les éléments.

> **Exemples**
> *Input*: `[2,4,3,7,10,6]` → **Output**: `4` (facteurs: 2, 3, 5, 7)
> *Input*: `[2,4,8,16]` → **Output**: `1` (facteur: 2)

La simple multiplie tous les nombres et facteur le produit déborde instantanément. L'astuce est de considérer chaque élément *individuellement* et de fusionner les résultats en un ensemble de premiers.

---

Pourquoi ce blog ?
- **Mots-clés de référence**: *code 2521, facteurs principaux distincts, produit tableau, solution Java, solution Python, solution C++*
- Couvertures ** Bon**, ** Mauvais** et ** Aspects exceptionnels** des approches communes
- Vous aide à vous démarquer dans les interviews techniques et les interviews de codage

---

## Solution optimale – Sieve + Factorisation

- Oui. Pourquoi ça marche ?
* Le nombre maximum possible dans le tableau est seulement 1 000, donc tous les facteurs principaux sont ≤ 1000.
* Nous précalculons tous les premiers jusqu'à 1 000 avec le Sieve d'Eratosthenes (O( √1000)).
* Pour chaque nombre, nous divisons par premier jusqu'à ce qu'il ne puisse plus être divisé.
* Un `HashSet` (Java), `set` (Python), ou `unordered_set` (C++) recueille les premiers.

Complexité
Métrique
- C'est quoi ?
**Heure**=O(n * π(1000)=O(n * 168)=O(n * π(1000)=O(n * π(1000)=O(n * π(1000)=" Autres
**Espace** Même

---

Code en trois langues

C'est pas vrai. Java – Propre et idiomatique

"Java
Importation de java.util.*;

solution de classe publique {
// Primes précalculées jusqu'à 1000
liste finale statique privée<entier> PRIMES = tamis(1000);

liste statique privée<entier> sieve(int limit) {
Booléen[] isPrime = nouveau booléen[limite + 1];
Arrays.fill(isPrime, true);
isPrime[0] = isPrime[1] = false;
pour (int p = 2; p * p <= limite; p++) {
si (isPrime[p]) {
pour (int k = p * p; k <= limite; k += p) {
isPrime[k] = faux;
}
}
}
Liste <Integer> prime = nouvelle liste d'array<>();
pour (int i = 2; i <= limite; i++) {
si (isPrime[i]) prime.add(i);
}
les prime de retour;
}

secteur public PrimeFactors(int[] nums) {
Définir <Integer>primes uniques = nouveau HashSet<>();
pour (int val : nombres) {
facteur(val, primes uniques);
}
retour uniquePrimes.size();
}

facteur de vide privé(int num, Set<entier> résultat) {
pour (int p : PRIMES) {
en cas de rupture (p * p > num);
si (num % p == 0) {
résultat.add(p);
alors que (num % p) 0) num /= p;
}
}
si (num > 1) { // restant prime
résultat.add(num);
}
}
}
«» "

> **Bonne** – Réutilise une liste primaire précalculée, recherche de facteur O(1).
> **Bad** – Utilisations `Liste<Intégrée>` pour les premiers; un `int[]` serait légèrement plus rapide.
> **Ugly** – Aucun initialisateur statique pour le tamis; chaque objet `Solution` le recalcule si ce n'est `statical`. Le code ci-dessus déclare "statique" pour éviter cela.

---

Python – Concise & Pythonique

'`python
de maths import iskrt
de taper l'importation Liste

♪ Primes précalculées jusqu'à 1000
def sieve(limite: int) -> Liste[int]:
is_prime = [True] * (limite + 1)
is_prime[0] = is_prime[1] = Faux
pour p dans l'intervalle(2, iqrt(limite) + 1):
si is_prime[p]:
pour k dans l'intervalle (p * p, limite + 1, p):
is_prime[k] = Faux
retour [i pour i, v in énumérate(is_prime) si v]

PRIMES = tamis(1000)

Solution de classe:
def distinct PrimeFactors(self, nombres: Liste[int]) -> Int:
unique = set()
pour num in nums:
auto_facteur(num, unique)
retour len(unique)

def _factor(self, num: int, unique: set) -> Aucun:
pour p dans PRIMES:
si p * p > num:
pause
si num % p == 0:
unique.add(p)
alors que num % p == 0:
num //= p
si num > 1: # restant premier
unique.add(num)
«» "

> **Bien** – Leverages Python=s `set` et la compréhension de la liste.
> **Bad** – Le tamis est recalculé chaque fois que le module est importé (mais c'est bien pour LeetCode).
> **Ugly** – Le code itère toujours sur *all* prime jusqu'à 1000 pour chaque nombre, même si `num` est minuscule. Une approche plus intelligente s'arrêterait une fois "num".

---

C++ – Orientation vers la performance

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
particulier:
vecteur statique <int> premiers;

vecteur statique<int> buildPrimes(int limit) {
vector<bool> isPrime(limite + 1, true);
isPrime[0] = isPrime[1] = false;
pour (int p = 2; p * p <= limite; ++p)
si (isPrime[p])
pour (int k = p * p; k <= limite; k += p)
isPrime[k] = faux;
vecteur <int> premiers;
pour (int i = 2; i <= limite; ++i)
si (isPrime[i]) primes.push_back(i);
les prime de retour;
}

public:
Int distinctPrimeFactors(vector<int>& nums) {
unordered_set<int> uniq;
pour (int val : nombres) {
facteur (val, uniq);
}
retourner uniq.size();
}

particulier:
facteur de vide(int num, unordered_set<int>& uniq) {
pour (int p : prime) {
en cas de rupture (p * p > num);
si (num % p == 0) {
uniq.insert(p);
alors que (num % p) 0) num /= p;
}
}
si (num > 1) uniq.insert(num);
}
};

vecteur<int> Solution::primes = Solution::buildPrimes(1000);
«» "

> **Bien** – Utilise un membre statique pour construire les premiers une fois, partagé dans toutes les instances.
> **Bad** – L'en-tête `bits/stdc++.h` n'est pas standard mais pratique sur LeetCode.
> **Ugly** – Le `unordered_set` peut re-hash si le nombre de premiers uniques augmente; dans la pratique, cela est négligeable.

---

Les bons, les mauvais et les méchants

Catégorie Ce que vous allez aimer Ce que vous allez sur la sueur
- C'est-à-dire
**Bonne**) • Les primaires précalculées évitent la division d'essai répétée. <br>• Set/HashSet assure l'unicité en O(1). <br>• Linéaire dans `n` et trivial dans la pratique.
• Certaines solutions re-factorisent les mêmes premiers pour chaque élément (coûts mais toujours < 2 000 ops). <br>• L'utilisation de `Set` peut attribuer de nombreux petits objets en Java/Python.
• Multiplier tout le tableau (dépassement). <br>• Divisant récursivement sans condition de rupture. <br>• Entreposer le produit complet dans un "long long" puis l'affacturage (risque de dépassement). Autres

---

Démarrage rapide de la feuille de chaleur

Texte
1. Créer une liste de prime jusqu'à 1000 (Sieve of Eratosthène).
2. Pour chaque nombre en chiffres:
a. Pour chaque p principal:
i. Si p * p > num → pause.
ii. Si num % p == 0: ajouter p à définir; diviser num par p jusqu'à ce qu'il ne soit pas divisible.
b. Si num > 1: ajouter num (le reste de prime) à définir.
3. Retour set.size().
«» "

---

Pourquoi ce blog aide-t-il votre recherche d'emploi

1. **Titre et rubriques riches en mots clés** – Les moteurs de recherche l'affichent pour *leetcode*, *facteurs principaux distincts*, *solutions Java/Python/C++*.
2. **Exemples de code étape par étape** – Les recruteurs peuvent copier et exécuter instantanément.
3. **Plongée profonde dans les pièges** – Il vous montre non seulement la réponse de droite, mais pourquoi vous ne devriez pas le faire de cette façon.
4. **Meta-description adaptée au référencement** – Court, poinçonné et rempli de termes pertinents.
5. **Format professionnel** – Les blocs de code, les tables et une narration propre rendent l'article poli.

> **Désignation de la Méta (150 caractères)* *
> *Solve LeetCode 2521 – Distinct Facteurs principaux du produit d'aménagement. Java, Python, code C++, analyse d'approches bonnes/mauvaises/puces, et explications prêtes à l'entrevue. *

---

Appel à l'action

> Tu veux passer ton prochain entretien de codage ?
> - **Télécharger** la repo GitHub avec les trois solutions.
> - **Clone** et faire les tests.
> - **Partager** ce post sur LinkedIn/Dev.to et laisser les recruteurs voir votre style de résolution de problèmes!

Bon codage ! C'est ce qu'il a dit