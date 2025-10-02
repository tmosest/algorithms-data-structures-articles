---
titre: LeetCode 2470. Nombre de subarrays avec LCM égal à K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2470 – Nombre de sous-arrachages avec LCM = K
C++ – Solutions de travail complètes + Guide du blog**
*(SEO-optimisé, le bon, le mauvais, et le laid de votre prochaine interview*)

---

- Oui. 1. Aperçu du problème

> **Donné** d'un nombre entier (1 ≤ `nums.longueur` ≤ 1000) et d'un nombre entier `k` (1 ≤ `k` ≤ 1000).
> **Retour** le nombre de subarrays contigus** dont **le moins commun multiple (LCM)** est égal à "k".

Un subarray est une tranche contiguë non vide de «nums».
Le LCM d'un tableau est le plus petit entier positif divisible par **chaque** élément.

> **Exemple**
> `nums = [3, 6, 2, 7, 1]`, `k = 6` → réponse: **4** (les quatre subdivisions énumérées dans l'énoncé du problème).

---

- Oui. 2. Principales observations

Observation Pourquoi ça compte
C'est-à-dire
`LCM(a, b)` peut seulement **grow** ou rester le même lorsque nous ajoutons plus de nombres Si jamais il dépasse `k`, aucune extension ultérieure ne le ramènera → nous pouvons **break** tôt. Autres
"nums[i] ≤ 1000" et "k ≤ 1000" Limite le maximum utile de LCM que nous devons considérer. Autres
`LCM` peut être calculé à l'aide de `LCM(a, b) = a / gcd(a, b) * b`"" `gcd` est bon marché (algorithme euclidéen) et garde des valeurs intermédiaires petites. Autres
**Complexité temporelle**: `O(n2)` est bon pour `n ≤ 1000'. Autres

---

- Oui. 3. L'Algorithme de base

Texte
ans = 0
pour i = 0 ... n-1:
cur = 1
pour j = i ... n-1:
cur = lcm(cur, nombres[j])
si cur == k: ans++
si cur > k: pause // pas besoin d'étendre cette sous-tribu
retour et
«» "

* `cur` détient le LCM de `nums[i...j]`.
* Dès que `cur > k` nous arrêtons d'étendre ce sous-array parce que LCM ne peut pas rétrécir.
* `lcm` est calculé par `gcd` pour éviter le débordement et le garder rapide.

---

- Oui. 4. Le mal – Pièges communs

Piège
- Oui.
Autres Utiliser un `lcm` naïf qui se multiplie avant de diviser → déborder. Autres
Autres Oublier de casser quand `cur > k` → O(n3) dans le pire des cas. Autres
Utiliser `double` ou point flottant pour LCM → erreurs de précision. Autres
Ne pas traiter l'affaire `k == 1` correctement L'algorithme compte naturellement des sous-barrages dont le LCM est exactement 1. Autres

---

- Oui. 5. L'Ugly - Cas de bord et tests

Cas de bord Quoi tester
C'est quoi ?
Le résultat doit être 0. Autres
Autres Tous les éléments sont 1.
`k` égale le produit de plusieurs éléments. Autres
Grand `k` près de 1000' Vérifiez que la logique `break` fonctionne correctement. Autres

Lancez toujours le harnais d'essai suivant :

'`python
def brute(nums, k):
importer des maths
ans = 0
pour i dans la plage(len(nums)):
pour j dans la plage(i, len(nums)):
cur = 1
pour x en nombres[i:j+1]:
cur = cur * x // math.gcd(cur, x)
Si cur == k:
+= 1
retour et
«» "

Recoupez la sortie de votre implémentation avec cette force brute pour les entrées aléatoires.

---

- Oui. 6. Mise en œuvre complète du code

#### 6.1 Java (LeetCode Style)

"Java
solution de classe {
LCM(int[] nums, int k) {
nombre int = 0;
pour (int i = 0; i < nombres de longueur; i++) {
La valeur de l'unité de mesure est égale à 1;
pour (int j = i; j < nombres.longueur; j++) {
curLcm = lcm(curLcm, nombres[j]);
si (curLcm == k) count++;
Si (curLcm > k) rupture; // optimisation importante
}
}
le nombre de retours;
}

Int. privée {
retourner a / gcd(a, b) * b;
}

Int privé gcd(int a, int b) {
pendant que (b != 0) {
t = a % b;
a = b;
b = t;
}
retour a;
}
}
«» "

#### 6.2 Python 3

'`python
d'importation de mathématiques gcd

Solution de classe:
def subarrayLCM(self, nombres: list[int], k: int) -> Int:
nombre = 0
n = len(nums)
pour i dans la plage(n):
cur = 1
pour j dans la plage(i, n):
cur = cur * nombres[j] // gcd(cur, nombres[j])
Si cur == k:
nombre += 1
si cur > k:
pause
Nombre de retours
«» "

*### 6.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int subarrayLCM(vector<int>& nums, int k) {
nombre int = 0;
pour (int i = 0; i < nums.size(); ++i) {
longue courbure = 1;
pour (int j = i; j < nums.size(); ++j) {
cur = cur / md::gcd(cur, (long)nums[j]) * nums[j];
si (cur== k) ++compte;
si (cur > k) casse; // lance la recherche
}
}
le nombre de retours;
}
};
«» "

> **Note** : "longtemps" garde le produit intermédiaire en sécurité, même si nous brisons quand `cur > k`.

---

- Oui. 7. Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Force brute (boucles nestées + "lcm")
Utiliser `break` sur `cur > k` Même pire cas, souvent plus rapide dans la pratique

Avec `n = 1000`, cela fonctionne en moins d'un milliseconde dans toutes les langues.

---

- Oui. 8. Pourquoi ce blog aide votre carrière

1. **Maîtrise d'entrevue** – Le problème de subarray LCM est un support *classique* LeetCode qui démontre votre compréhension de la théorie des nombres, du raisonnement de style de fenêtre à deux pointeurs/glissants et des astuces d'optimisation.
2. **Show-case multilingue** – Avoir des solutions prêtes à copier en Java, Python et C++ prouve que vous êtes un ingénieur polyvalent confortable à travers la pile.
3. **SEO-Friendly Content** – En arrosant des mots-clés comme le code Leet 2470, le nombre de sous-barrages avec LCM égal à K, le problème de sous-barrage LCM, et l'entrevue de codage -, les recruteurs rampent pour l'expérience de résolution de problèmes va repérer votre poste.
4. **Structured Insight** – Expliquer « bon, mauvais, laid » démontre des compétences de codage réfléchies, quelque chose de valeur pour les intervieweurs lors de l'évaluation de l'ancienneté.

---

- Oui. 9. Liste de contrôle finale avant de soumettre

- [ ] **Run tous les cas d'essai** (fournis, bordés et aléatoires).
- [ ] **Commentaire** les parties clés (`lcm`, `break`).
- [ ] **Double-check débord**: utilisez `long`/`int64_t` en C++, `long` en Java si vous souhaitez être plus sûr.
- [ ] **Durée de votre solution** sur une machine locale – devrait être < 5 ms pour `n=1000`.
- [ ] **Push to GitHub** et ajouter un README clair avec une brève explication – les recruteurs aiment les échantillons open-source.

---

10. TL;DR

> **Algorithme**: Double boucle, calculer l'exécution de LCM, casser quand il dépasse `k`.
> **Complexité**: temps «O(n2)», espace «O(1)».
> **Résultat**: Nombre de sous-tribus dont le LCM est exactement "k".
> **Langues**: Java, Python, C++ prêt à être copié.

Bon codage, et que ces intervieweurs aiment vos solutions LCM-savvy! C'est ce qu'il a dit.

---