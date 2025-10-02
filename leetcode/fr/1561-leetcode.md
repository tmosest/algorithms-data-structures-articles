---
titre: LeetCode 1561. Nombre maximum de pièces que vous pouvez obtenir -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1561 – *Nombre maximum de pièces que vous pouvez obtenir*
**Moyenne= 3 n piles= O(n) temps= O(max piles) espace**

---

Récapitulation des problèmes

- Oui.
-- -- -- -- -- --
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Processus****=Dans chaque tour, vous choisissez les 3 piles.
C'est la raison pour laquelle la Commission s'est prononcée en faveur de l'adoption d'une directive relative à l'étiquetage des denrées alimentaires. Alice prend la plus grosse pile.
Le présent règlement entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne. **Vous** prenez la prochaine plus grande pile.
La valeur de l'indice de prix à la consommation (IPCH) est calculée comme suit: Bob saisit le reste de la pile.
**Objectif**= Maximisez le nombre total de pièces avec lesquelles vous finissez.
**Output**="int` – pièces maximum que vous pouvez collecter. Autres

> **Exemples**
> 1. `piles = [2,4,1,2,7,8]` → **9**
> 2. `piles = [2,4,5]` → **4**
> 3. «piles = [9,8,7,6,5,1,2,3,4]

---

Les bons, les mauvais et les affreux

Aspect du bien
- C'est quoi ?
**Greedy Insight** Aucune – la stratégie d'avidité est certainement optimale. Une mauvaise compréhension de l'ordre peut conduire à un algorithme *wrong* O(n). Autres
**Complexité du temps**= `O(n)` (avec tri de comptage) ou `O(n log n)` (avec `sort`). Le tri est plus simple mais plus lent pour les entrées énormes. La force brute O(n2) (choisissant toutes les combinaisons) est *astronomiquement* lente. Autres
Autres **Complexité spatiale**= `O(maxValue)` – petite parce que la pièce compte ≤ 104.= `O(1)` espace auxiliaire lors de l'utilisation de `sort` & indexing. Il est impossible de conserver toutes les permutations. Autres
**Boîtes de corner** Doit gérer 3 piles ≤. longueur ≤ 105.- Dépassement ou indices négatifs si vous utilisez mal les tableaux. Autres
**Readability** Le code de tri est plus court mais légèrement moins intuitif. Le mélange des deux approches dans une solution peut être source de confusion. Autres

---

Deux approches classiques

#### 3.1 Compter-Sort Greedy (heure O(n))

1. Comptez combien de piles contiennent chaque quantité de pièce possible.
2. Descendez de la valeur maximale de la pièce, simulant les tours:
* Alice prend la première pile de cette valeur (skip).
* **Vous** prenez la deuxième pile (ajouter à la réponse).
* Bob prend la troisième pile (skip).
* Continuer jusqu'à ce que tous les tours `n/3` soient terminés.

Comme la valeur maximale de la pièce n'est que de 104, le tableau de fréquence est minuscule.

---

3.2 Tri de l'avidité (O(n log n))

1. Trier les «pilles» dans l'ordre ** décroissant**.
2. Après tri, Alice obtient des indices `0,3,6...'
vous obtenez des indices `1,4,7,...`
Bob obtient des indices "2,5,8,...".
3. Sommez les éléments aux indices `1,4,7,...` – c'est votre total.

C'est sans doute plus propre, mais un peu plus lent.

---

Code – 3 langues

> **Astuce** – Tous les extraits ci-dessous sont prêts à être collés dans l'éditeur de LeetCodes ou dans votre propre IDE.
> **Note** – Les méthodes `main` ne sont que pour les tests locaux rapides, ils ne sont pas requis sur LeetCode.

#### 4.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
// Solution cupidienne de comptage (temps O(n))
int public maxCoins(int[] piles) {
int n = longueur des pieux;
= 0;
pour (int v : piles) si (v > max) max = v;

int[] freq = nouveau int[max + 1];
pour (int v : piles) freq[v]++;

pièces int = 0; // vos pièces
rounds int = n / 3; // nombre de triplets
int tour = 1; // 1 → vous, 0 → sauter (Alice ou Bob)
Int val = max;

pendant la période (tours > 0) {
si (freq[val]] 0) {
val--; // passer à la valeur suivante plus petite
poursuivre;
}

Si (tourner) 1) { // vous choisissez
pièces += valeur;
tour = 0; // le tour suivant est skip
round--; // round terminé
} autre { // skip (Alice ou Bob)
tour = 1; // prochain tour sera le vôtre
}
freq[val]--; // supprimer la pile utilisée
}
les pièces retournées;
}

/* -------------------- Essai local facultatif -------------------- */
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.maxCoins(nouvelle int[]{2,4,1,2,7,8}); // 9
Système.out.println(s.maxCoins(nouvelle int[]{2,4.5}); // 4
Système.out.println(s.maxCoins(nouvelle int[]{9,8,7,6,5,1,2,3,4}); // 18
}
}
«» "

---

4.2 Python

'`python
Solution de classe:
# Solution de comptage et d'avidité (temps O(n))
def maxCoins(self, piles: list[int]) -> Int:
n = len(piles)
max_val = max(piles)

freq = [0] * (max_val + 1)
pour v en piles:
freq[v] += 1

pièces = 0 # vos pièces
ronde = n // 3 Nombre de triplets
tour = 1 # 1 -> vous, 0 -> sauter
val = max_val

pendant les rondes > 0:
si freq[val] == 0:
Valeur 1
poursuivre

si tour == 1: # tu choisis
pièces += valeur
tour = 0
rondes -= 1
Sinon: # sauter
tour = 1

[val] -= 1

pièces retournées

♪ -------------------- Essai local facultatif --------------------
si __nom__ == "__main__" :
sol = Solution()
print(sol.maxCoins([2, 4, 1, 2, 7, 8])) # 9
print(sol.maxCoins([2, 4, 5))) # 4
print(sol.maxCoins([9, 8, 7, 6, 5, 1, 2, 3,])) # 18
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Solution cupidienne de comptage (temps O(n))
int maxCoins(vecteur<int>& piles) {
int n = piles.size();
Int maxVal = *max_element(piles.begin(), piles.end());

vecteur<int> freq(maxVal + 1, 0);
pour (int v : piles) freq[v]++;

pièces int = 0; // vos pièces
rounds int = n / 3; // nombre de triplets
int tour = 1; // 1 -> vous, 0 -> sauter
Int val = max Val;

pendant la période (tours > 0) {
si (!freq[val]) { // aucune pile de cette valeur
--val;
poursuivre;
}

Si (tourner) 1) { // vous choisissez
pièces += valeur;
tour = 0;
round--; // round terminé
} autre { // skip (Alice ou Bob)
tour = 1;
}
--freq[val]; // utiliser une pile
}
les pièces retournées;
}
};

/* -------------------- Essai local facultatif -------------------- */
Int main() {
Solution s;
<< s.maxCoins({2,4,1,2,7,8}) << endl; // 9
Cout << s.maxCoins({2,4.5}) << endl; // 4
Cout << s.maxCoins({9,8,7,6,5,1,2,3,4}) << endl; // 18
retour 0;
}
«» "

> Si vous préférez la version **triage**, remplacez simplement le corps de chaque méthode par un seul liner (Python) ou le tour `Arrays.sort` (Java/C++). La complexité du temps passera à `O(n log n)` mais l'utilisation de la mémoire restera `O(1)`.

---

C'est pas vrai. Pourquoi ce problème compte pour votre chasse à l'emploi

1. **Question d'entrevue classique** – De nombreux recruteurs techniques utilisent le LeetCode 1561 comme test litmus pour les compétences *gredy* et *sorting*.
2. **Modèle mental clair** – Démontre votre capacité à *transférer un processus réel* (trois personnes cueillant des piles) dans un algorithme formel.
3. **Réflexion efficace** – Vous pouvez repérer quand un tour de comptage-sort bat un genre naïf.
4. **Language-agnostic** – Fournir du code de travail en Java, Python et C++ prouve que vous pouvez vous adapter à la pile que votre futur employeur utilise.
5. **Blog‐Ready** – Écrire un message propre et convivial (comme celui-ci) démontre * compétences en communication* – la deuxième compétence d'entrevue la plus importante après le codage.

---

## 6-SEO-Friendly Take-away

**Mots clés** (pour votre blog, Linked Dans l'article, ou site web personnel):
- **LeetCode 1561**
- *Nombre maximum de pièces que vous pouvez obtenir*
- *Algorithme de greffe *
- *Traitement de la composition*
C'est avide.
- *Questions relatives au codage des entretiens*
- *Java, Python, solutions C++*
- *O(n) Solutions LeetCode
- *Préparation des entretiens techniques*
- *Conseils d'entretien pour l'ingénierie logiciel*

**Description détaillée** (155 caractères) :
> Code du leet 1561 – Nombre maximum de pièces que vous pouvez obtenir – en Java, Python et C++. Apprenez l'astuce, la complexité et les conseils d'entrevue. (en milliers de dollars)

---

Liste de contrôle finale pour votre CV / portfolio

- *Problème**: Code Leet 1561 – *Nombre maximum de pièces que vous pouvez obtenir*
- **Langues**: Java, Python, C++
- **Temps**: tri O(n) de comptage (= 104 valeurs) ou O(n log n)
* Espace**: valeur O(max) (minute) ou O(1) auxiliaire
- **Proof** : La sélection Greedy, deuxième plus grande, est optimale car Alice prend toujours la plus grande.

> ** Prêt à impressionner les recruteurs ? **
> Partagez le code et l'article sur GitHub, liez-le dans votre lien Dans le profil, et le montrer lors de votre prochaine entrevue de codage. Bonne chance ! C'est ce qu'il a dit