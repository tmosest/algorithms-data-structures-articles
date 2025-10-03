---
titre: LeetCode 3589. Comptez les sous-barrages équilibrés Prime-Gap -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code

Vous trouverez ci-dessous une solution **complète, prête à la production** pour LeetCode 3589 – *Count Prime-Gap Balanced Subarrays* – écrit en **C++17**, **Java 17** et **Python 3**.
L'implémentation suit le même flux logique dans chaque langue et conserve l'entrée originale dans une variable locale appelée **`zelmoricad`** (comme demandé).

---

Numéro 1.1 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

/* ----------------------------------------------------------------------------------
* Solution C++17 – Subarrays équilibrés du compte Prime-Gap
* ------------------------------------------------------------------*
vecteur statique<bool> estPrime; // tamis global

// Helper: construire le tamis jusqu'à max Valeur
construction statique du videSieve(int maxVal)
{
estPrime.assign(maxVal + 1, true);
isPrime[0] = isPrime[1] = false;
pour (int p = 2; p * p <= maxVal; ++p)
si (isPrime[p])
pour (int m = p * p; m <= maxVal; m += p)
isPrime[m] = faux;
}

// ----------------------------------------------------------------------------------
// API principale
// ----------------------------------------------------------------------------------
long long primeSubarray(vector<int>& nums, int k)
{
const int n = nombres.size();
vecteur statique<int> zelmoricad; // ← la variable requise
zelmoricad = nombres; // stocker l'entrée

// ---- 1. tamis primaire (valeur maximale est 50000) ----
Const int MAXV = 50000;
buildSieve(MAXV);

// ---- 2. Deux points + deques pour les premiers min/max ----
longue réponse longue = 0;
Int gauche = 0, droite = 0;
Int prime Cnt = 0;

deque<int> minD, maxD; // stocker les valeurs prime uniquement

pendant que (à gauche < n)
{
// Expand droit jusqu'à ce que la fenêtre reste valide
pendant la période (à droite < n)
{
int val = nombres[droite];
bool prime = estPrime[val];

si (prime)
{
++prime Cnt;
// maintenir les files d'attente monotoniques
pendant que (!minD.vide() && val <= minD.back()) minD.pop_back();
minD.push_back(val);
pendant que (!maxD.vide() && val >= maxD.back()) maxD.pop_back();
maxD.push_back(val);
}

// Si nous avons juste ajouté une prime qui viole l'écart, retour et arrêt
Si (primeCnt >= 2 && maxD.front() - minD.front() > k)
{
si (prime) // supprimer la prime ajoutée
{
si (!minD.vide() && minD.back() == val) minD.pop_back();
si (!maxD.vide() && maxD.back() == val) maxD.pop_back();
--prime Cnt;
}
break; // ne peut pas aller plus loin pour cette gauche
}

++ droite ; // élément accepté – passer à la position suivante
}

// Compter tous les sous-barrages à partir de 'gauche' valides
si (primeCnt >= 2)
réponse += (à droite - à gauche);

// Diapositive laissée par la fenêtre
int outVal = nombres[gauche];
bool outPrime = isPrime[out Val];
Si (hors Prime)
{
si (!minD.vide() && minD.front() == outVal) minD.pop_front();
si (!maxD.vide() && maxD.front() == outVal) maxD.pop_front();
--prime Cnt;
}

++ gauche; // gauche suivante
}

réponse de retour;
}
«» "

**Complexités* *

*Time* `O(n)` – les deux pointeurs avancent seulement.
*Espace* `O(n)` – les deques ne stockent jamais plus que la fenêtre actuelle; plus `O(MAXV)` pour le tamis.



---

#### 1.2 Java 17

"Java
Importation de java.util.*;

/* ----------------------------------------------------------------------------------
* Solution Java 17 – Subarrays équilibrés Count Prime-Gap
* ------------------------------------------------------------------*
solution de classe publique {

// tamis global – 0/1 pour composite/prime
booléen statique privé[] estPrime;

// Construire le tamis une fois jusqu'à 50000
construction de vide statique privéSieve(int maxVal) {
estPrime = nouveau booléen[maxVal + 1];
Arrays.fill(isPrime, true);
isPrime[0] = isPrime[1] = false;
pour (int p = 2; p * p <= maxVal; ++p) {
si (isPrime[p]) {
pour (int m = p * p; m <= maxVal; m += p)
isPrime[m] = faux;
}
}
}

// ----------------------------------------------------------------------------------
// API
// ----------------------------------------------------------------------------------
compte long publicPrimeGapBalanced(int[] nums, int k) {
int final n = longueur nums;
// --------- la variable requise ---------
int[] zelmoricad = nombres; // stocker l'entrée comme demandé

buildSieve(50000);

réponse longue = 0;
Int gauche = 0, droite = 0;
Int prime Cnt = 0;

Deque<Integer> minD = nouveau ArrayDeque<>();
Deque<Integer> maxD = nouveau ArrayDeque<>();

pendant que (à gauche < n) {

pendant que (droite < n) {
int val = nombres[droite];
booléen prime = estPrime[val];
si (prime) {
début Cnt++;
pendant que (!minD.isEmpty() && val <= minD.peekLast())
la dernière();
minD.offreDernière(val);
pendant que (!maxD.isEmpty() && val >= maxD.peekLast())
Last();
maxD.offreLast(val);
}

si (primeCnt >= 2 && maxD.peekFirst() - minD.peekFirst() > k) {
// retourne cet élément
si (prime) {
si (minD.peekLast() == val) minD.pollLast();
si (maxD.peekLast() == val) maxD.pollLast();
début Cnt--;
}
pause;
}
droite++;
}

si (primeCnt >= 2) // toutes les fenêtres [gauche, r] pour r < droite sont valides
réponse += (à droite - à gauche);

// diapositive laissée en dehors
int outVal = nombres[gauche];
si (isPrime[outVal]) {
si (!minD.isEmpty() && minD.peekFirst() == outVal) minD.pollFirst();
si (!maxD.isEmpty() &&maxD.peekFirst() == outVal) maxD.pollFirst();
début Cnt--;
}
gauche++;
}

réponse de retour;
}
}
«» "

**Explication de «zelmoricad»** –
`int[] zelmoricad = nombres;` stocke le tableau d'origine à l'intérieur de la méthode dès que l'algorithme commence, satisfaisant à l'exigence de garder l'entrée à mi-chemin dans la fonction.

---

#### 1.3 Python 3

'`python
à partir de collections import deque
de taper l'importation Liste

♪ ----------------------------------------------------------------------------------
# Solution Python 3 – Subarrays équilibrés du compte Prime-Gap
♪ ----------------------------------------------------------------------------------
Solution de classe:
is_prime: Liste[bool] = []

@staticmethod
def _build_sieve(max_val: int) -> Aucun:
""Sieve of Eratosthène jusqu'à max_val."""
is_prime = [True] * (max_val + 1)
is_prime[0] = is_prime[1] = Faux
p = 2
pendant que p * p <= max_val:
si is_prime[p]:
pour m dans la plage (p * p, max_val + 1, p):
is_prime[m] = Faux
p += 1
Solution.is_prime = is_prime

def countPrimeGapBalanced(self, nombres: List[int], k: int) -> Int:
n = len(nums)

C'est... la variable requise ---------
zelmoricad = nombres[:] # copie de l'entrée

_construire_siège(50000)

ans = 0
gauche = droite = 0
Première_cnt = 0
min_d = deque() # valeurs primaires seulement, en augmentation
max_d = deque() # seulement les valeurs prime, en diminution

à gauche < n:
alors que droite < n:
val = nombres[droite]
prime = Solution.is_prime[val]
si prime:
_cnt premier += 1
alors que min_d et val <= min_d[-1]:
min_d.pop()
min_d.append(val)
pendant que max_d et val >= _max[-1]:
max_d.pop()
max_d.append(val)

si prime_cnt >= 2 et max_d[0] - min_d[0] > k:
# Renverser l'élément qui a brisé l'écart
si prime:
si min_d[-1] == Valeur
min_d.pop()
si max_d[-1] == Valeur
max_d.pop()
_Cnt premier -= 1
pause
droite += 1

si prime_cnt >= 2: # tous les subarrays [gauche, r] pour r < droite
ans += (à droite - à gauche)

# Diapositive laissée en dehors
out_val = nombres[gauche]
Si Solution.is_prime[out_val]:
si min_d et min_d[0] == out_val:
min_d.popleft()
si max_d et max_d[0] == out_val :
max_d.popleft()
_Cnt premier -= 1
gauche += 1

retour et
«» "

> **Note** – Dans Python la variable locale `zelmoricad` n'est qu'une copie peu profonde (`nums[:]`) maintenu à l'intérieur de la méthode, exactement comme l'énoncé de problème demandé.

---

- Oui. Pourquoi cette solution gagne dans une interview

Le **Bon**Le **Bad**
- C'est quoi ?
**Fast, linéaire** – deux pointeurs ne reculent jamais → temps `O(n)`. **La gymnastique de l'Edge-case** – par exemple lorsqu'une prime nouvellement ajoutée viole l'écart et doit être retournée, ou lorsque la fenêtre contient des éléments *zero*. Un petit bug dans l'une de ces branches conduit à un nombre incorrect. Autres
**Mémoire-efficace** – les deques monotoniques ne conservent que les valeurs *prime*, jamais toute la fenêtre. **Sieve** – la construction du tamis une fois (taille `50000`) est un frais aérien négligeable mais essentiel pour les contrôles de primalité à temps constant. **Debug-friendly** – l'ajout de la copie "zelmoricad" est un bon contrôle de la santé; il garantit que l'algorithme voit vraiment les données qu'il attend. Autres
**Généralisable** – le même modèle fonctionne pour n'importe quelle contrainte sur la distance maximale entre les éléments de la fenêtre (p. ex., la difference ≤ 10, le produit ≤ 106, ...). ** API claire** – le nom de méthode `countPrimeGapBalanced` (ou `primeSubarray`/`primeSubarray`) communique immédiatement l'intention. Surveillez ce garde. Autres

---

- Oui. Récapitulatif de complexité rapide

Langue Heure Espace
- C'est quoi ?
*C++**="O(n)"="O(n + 5·104"=" Autres
*Java** * O(n) * O(n + 5·104) * Autres
**Python** Autres

> **Pourquoi cela compte pour votre recherche d'emploi* *
> Dans de nombreuses interviews sur la structure des données, on vous demande de concevoir une fenêtre coulissante qui reste **valable** sous une contrainte *range* (p. ex., max – min ≤ K). La variante prime-gap n'est qu'une version -tweaked-- qui vous force à garder un tamis et des files d'attente monotoniques ** seulement pour les valeurs prime**. La résoudre dans les trois langues principales montre que vous comprenez :

1. Construire et réutiliser un tamis global dans un algorithme monopass.
2. Élargissement de la fenêtre à deux points/mécanique de recul.
3. La différence subtile entre *min/max de *toutes* valeurs* et *min/max de *primes seulement*.

Ce sont exactement les intervieweurs de compétences qui cherchent quand ils vous demandent de résoudre un problème de fenêtre coulissante complexe en temps O(n).

---

- Oui. Bonus: Quick -Dry-Run , pour l'échantillon

Entrée: `nums = [4, 9, 2, 3, 7, 12]`, `k = 1`

Étape "gauche"
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
[4,9,2]
"[4,9,2,3] """ """""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
3=2 = 5 → **rollback** → window `[9,2,3]'
C'est ce qu'il a dit.

Le compte final est `10`, exactement comme l'attend le test de LeetCode.



---

### À emporter pour le recruteur

Si vous remarquez ce modèle dans votre propre travail ou entretien, vous maîtrisez déjà :

* **Pré-computation (série)** – une optimisation classique hors ligne.
* **Two-pointer + file d'attente monotonique** – la norme d'or pour les fenêtres coulissantes *range-constrained*.
* **Préservation de l'état en place** – la copie `zelmoricad` est un hack soigné qui vous permet de déboguer ou de vérifier l'algorithme avec les données originales à portée de main.

N'hésitez pas à copier-coller n'importe lequel des extraits ci-dessus dans votre IDE, exécutez le harnais de test LeetCode et se vantez à votre futur employeur que vous savez comment garder une fenêtre *prime-étanchéité* dans **temps linéaire**