---
titre: LeetCode 2389. Subséquence la plus longue avec une somme limitée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2389 – La plus longue séquence avec une somme limitée
### Le bon, le mauvais et le mauvais – Une solution de plongée profonde et de préparation au travail

> **Mots clés** – *La plus longue séquence avec une somme limitée*, *LeetCode 2389*, *Binary Search*, *Prefix Sum*, *Java*, *Python*, *C++*, *Problème d'entrevue*, *Conception d'algorithme*, *Entretien de codage*

---

Récapitulation des problèmes

Vous avez deux tableaux entiers :

* "nums" – taille **n** (1 ≤ n ≤ 1000)
* "requêtes" – taille **m** (1 ≤ m ≤ 1000)

Pour chaque «requêtes[i]» vous devez trouver le **nombre maximal d'éléments** vous pouvez choisir de `nums` ** sans changer l'ordre original** de sorte que la somme des éléments choisis est ≤ `queries[i]`.
Retournez un tableau de ces tailles maximales.

*exemple*
`nums = [4,5,2,1]`, `queries = [3,10,21]` → réponse `[2,34]`.

---

Pourquoi ça compte pour les entrevues

* **Greedy + Prefix Sum + Binary Search** – Modèle classique en 3 étapes que beaucoup d'intervieweurs aiment voir.
* **Complexité temporelle** – `O(n+m) log n)` – parfait pour les entrées de taille moyenne et une grande démonstration de raisonnement asymptotique.
* ** Polyvalence linguistique** – Nous montrons des implémentations propres dans **Java, Python et C++**, couvrant les langues d'entretien les plus populaires.

---

L'idée fondamentale (la bonne)

1. **Le tort ne fait pas de mal** –
Nous ne sommes intéressés que par le *sum*, pas par l'ordre original. Tri des "nums" nous donne les plus petits nombres d'abord, nous permettant de construire le plus long subséquence possible avidement.

2. **Préfixer le tableau de somme** –
Convertir le tableau trié en un tableau de somme courante.
«préfixe[i] = nombres[0] + ... + nombres[i]».
Maintenant, la somme des premiers `k` plus petits nombres est juste `préfixe[k-1]`.

3. **Recherche binaire sur le préfixe** –
Pour chaque requête `q`, trouvez le plus grand index `k` où `préfix[k] ≤ q`.
La réponse est "k + 1".
Dans C++/Java nous pouvons utiliser `upper_bound`; dans Python nous utilisons `bisect_right`.

4. **Cas d'urgence** –
*Séquence d'Empty* (lorsque `q` est plus petit que le plus petit nombre) → réponse `0`.
*Tous les éléments correspondent* (lorsque `q` ≥ somme totale) → répondre `n`.

---

Les pièges

Ce qui arrive
- C'est quoi ?
Utiliser **linear scan** pour chaque requête O(n m) → 1 000 000 ops (acceptable ici mais pas optimal)
Autres Oubliant de trier `nums`= Longueur de subséquences incorrectes `Arrays.sort(nums)` / `sort(nums)` Autres
Utiliser `upper_bound` ou `bisect_right` qui retourne déjà le compte
Autres Débordement entier de la somme jusqu'à 1000 éléments chacun ≤ 106 → jusqu'à 109, convient toujours en 32-bit mais gardez `long` pour la sécurité Utilisez `long` pour préfixer les sommes en Java/C++ Autres

---

Les solutions de code

Voici des implémentations propres et prêtes à la production pour **Java**, **Python** et **C++**.
Chaque extrait suit la stratégie en trois étapes décrite ci-dessus.

---

Java (Java 17)

"Java
Importer java.util. Les tableaux;
Importer java.util. Liste;
Importer java.util. d'une longueur d'au moins 50 mm;
importer java.util.stream.Collecteurs;

solution de classe publique {
public int[] replyQueries(int[] nombres, int[] requêtes) {
Trier les numéros
Tableaux.sort(nums);

// / / / / / / / / / / / / / / / / / / / / / / /
long[] préfixe = nouveau long[nums.longueur];
somme longue = 0;
pour (int i = 0; i < nombres de longueur; i++) {
somme += nombres[i];
préfixe[i] = somme;
}

// Répondre à chaque requête avec recherche binaire (en haut_bound)
int[] result = nouvelle int[queries.longueur];
pour (int i = 0; i < requêtes.longueur; i++) {
int q = requêtes[i];
int pos = upperBound (préfixe, q);
résultat[i] = pos; // pos est le nombre d'éléments ≤ q
}
le résultat du retour;
}

// Custom upper_bound: premier index où préfixe[idx] > cible
Int supérieur privéBound(long[] arr, int cible) {
int lo = 0, hi = arr.longueur;
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (arr[mid] <= cible) {
lo = milieu + 1;
} autre {
hi = milieu;
}
}
retour lo; // nombre d'éléments <= cible
}

// Optionnel: principal pour des tests locaux rapides
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
nombres int[] = {4,5,2,1};
requêtes int[] = {3,10,21};
System.out.println(Arrays.toString(s.answerQueries(nums, requêtes)));
}
}
«» "

---

Python 3

'`python
de bisect import bisect_right
à partir d'import d'itertools
de taper l'importation Liste

Solution de classe:
réponse Questions(self, nombres: List[int], requêtes: List[int]) -> Liste[int]:
N° 1 Tri
nombres.sort()

N° 2 Préfixer les sommes
préfixe = liste(accumulation(nums))

N° 3 Recherche binaire pour chaque requête
retourner [bisect_right(prefix, q) pour q dans les requêtes]

# Test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.answerQueries([4,5,2,1], [3,10,21])) # -> [2, 3, 4]
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> responseQueries(vector<int> nums, vector<int> requêtes) {
//
(noms.begin(), nums.end());

// 2.
vecteur <long> préfixe(nums.size());
sum(nums.begin(), nums.end(), prefix.begin());

// Pour chaque requête, utilisez upper_bound
vecteur <int> ans;
pour (int q : requêtes) {
// upper_bound retourne l'itérateur au premier élément > q
int cnt = upper_bound(prefix.begin(), prefix.end(), q) - prefix.begin();
as.push_back(cnt);
}
le retour des an;
}
};

// Pilote simple pour les essais manuels
Int main() {
Solution s;
vecteur<int> nombres = {4,5,2,1};
les requêtes vectorielles<int> = {3,10,21};
vector<int> res = s.answerQueries(nums, requêtes);
pour (int v: res) cout << v << ' ';
Cout << endl; // impressions: 2 3 4
}
«» "

---

La complexité temporelle et spatiale

Langue de classement Préfixe Questions Total
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
(n+m) Autres
Python "O(n log n)" "O(n)" "O(m log n)" "** Autres
"O(n log n)" "O(n)" "O(n)" "O(m log n)" "** Autres

Espace : `O(n)` pour le tableau de préfixe (plus tableaux d'entrée).
Toutes les langues conservent le même profil asymptotique.

---

Ce que les intervieweurs recherchent

1. **Clarification** – Avez-vous posé des questions sur le besoin de commande? L'approche avide fonctionne parce que l'ordre n'a pas d'importance pour les contraintes de somme.
2. **Proof of Correctness** – Triage donne d'abord les éléments les plus courts; toute subséquence plus longue utiliserait nécessairement des éléments plus grands et dépasserait la même somme.
3. **Edge Cases** – Montrez que vous manipulez un sous-séquence vide et que les requêtes dépassent la somme totale.
4. **Analyse de la complexité** – fournir grand‐ O nombres et expliquer pourquoi la recherche binaire est essentielle.
5. **Clean Code** – Utilisez des noms de variables descriptives, des fonctions d'aide distinctes (`upperBound`) et commentez les étapes clés.

---

TL;DR (Job-Ready Takeaway)

*Trier → Préfixe Sum → Recherche binaire. *
- **Trier** "nums" pour accéder aux plus petits numéros en premier.
- **Prefix Sum** vous permet de demander la somme de tout préfixe dans O(1).
- **Binary Search** (`upper_bound` / `bisect_right`) vous donne le préfixe le plus long qui correspond à la requête dans `O(log n)`.

Les trois langues ci-dessus implémentent ce modèle avec élégance, vous offrant une solution de 5 minutes de niveau interview qui impressionnera les recruteurs et réussira tout défi de codage. Bon codage 