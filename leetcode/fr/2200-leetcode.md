---
titre: LeetCode 2200. Trouver tous les indices K dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Trouver tous les indices K-distants dans un tableau
**(LeetCode 2200 – Facile)* *

> *Le bon, le mauvais et le laid – une plongée profonde dans un problème apparemment simple, comment le résoudre rapidement, et comment vous pouvez le montrer dans une interview. *

---

Pourquoi ce problème compte

* **Traitement d'entrevue** – C'est une question fréquente sur LeetCode et c'est un point de départ dans de nombreuses entrevues sur la structure des données.
* **Showcases comprehension of bi-pointer & prefix-sum tricks** – Une solution propre démontre une bonne compréhension de la pensée algorithmique.
* ** Facile à optimiser** – La solution naïve est \(O(n^2)\; l'optimum est \(O(n)\) et l'espace constant.

Si vous pouvez expliquer les compromis et donner une implémentation propre en Java, Python ou C++, vous impressionnerez n'importe quel gestionnaire d'embauche.

---

Déclaration du problème (supprimée)

> Avec un tableau entier `nums`, une valeur `key` qui apparaît dans `nums` et un entier `k`,
> retourner une liste **triée** de tous les indices `i` de sorte qu'il existe au moins un indice `j` avec
> \[
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * clé
> \]
>
> 1 ≤ "longueur en chiffres" ≤ 1 000
> 1 ≤ "nums[i]" ≤ 1 000
> 1 ≤ `k` ≤ `nums. longueur "

---

Deux solutions

L'approche du temps L'espace Pourquoi ça compte
-- -- -- -- -- -- -- -- -- -- -- -- --
**Brute-Force** – vérifier chaque paire de produits \(O(n^2)\)= \(O(1)\)= Facile à mettre en œuvre, mais lent pour n =1 000. Autres
**One-passe avec marquage** – **Optimal****[(O(n)\]**] \(O(1)\]=Scans une fois, pas de boucles imbriquées, seulement des maths entiers. Autres

Nous nous concentrons sur la solution optimale et fournissons le code en trois langues populaires.

---

Stratégie optimale – marquage à un seul passage

1. **Traverse** le tableau une fois.
2. Quand `nums[j]] == clé', les indices qui deviennent **k-distant** sont la gamme
\[
\text{left} = \max(0, j - k) \quad\text{à}\quad \text{right} = \min(n-1, j + k)
\]
3. Au lieu d'ajouter chaque indice dans cette plage **nativement**, gardez un pointeur de course `nextFree`.
* `nextFree` est le plus petit indice **non** encore ajouté.
* Pour chaque clé, nous ajoutons seulement l'intervalle `[max(nextFree, gauche), droite]`.
4. Après le traitement d'une clé, définissez `nextFree = droite + 1`.
5. Enfin, retournez les indices collectés.

L'idée est similaire à la ligne de "sweep" ou "interval fusion" – nous ne revoyons jamais un index qui a déjà été ajouté.

---

Cas d'essai

Produit escompté
-- -- -- -- -- -- -- --
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
"nums=[2,2,2,2]", "key=2", "k=2" "[0,1,2,34]" Autres
"nums=[1,2,3,4,5]`, `key=3`, `k=0`
"nums=[1,3,1,1]", "key=1", "k=1" "[0,1,2,34]" Autres

---

Code

### Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> findKDistantIndices(int[] nums, int key, int k) {
Liste <Integer> res = nouvelle liste de distribution<>();
int n = longueur nums;
int nextFree = 0; // plus petit indice non encore ajouté

pour (int j = 0; j < n; j++) {
si (nums[j] == clé) {
int gauche = Math.max(0, j - k);
int droite = Math.min(n - 1, j + k);

début int = Math.max(à gauche, suivantFree);
pour (int i = début; i <= droite; i++) {
l'alinéa i est remplacé par le texte suivant:
}
nextFree = droite + 1; // éviter les duplications
}
}
retour rés;
}

public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.findKIndicesdistants(
nouveaux int[]{3,4,9,1,3,5}, 9, 1)); // [1,2,3,4,5,6]
}
}
«» "

Python

'`python
de taper l'importation Liste

Solution de classe:
def findKDistantIndices(self, nombres: List[int], clé: int, k: int) -> Liste[int]:
n = len(nums)
res = []
next_free = 0 # premier index qui n'a pas été ajouté

pour j, val dans l'énumération(nombres):
if val == clé:
gauche = max(0, j - k)
droite = min(n - 1, j + k)

début = max(à gauche, sans _suivant)
res.extend(range(démarrage, droite + 1))
next_free = droite + 1

retour res

si __nom__ == "__main__" :
sol = Solution()
print(sol.findKIndices distants([3,4,9,1,3,9,5], 9, 1)) [1,2,3,4,5,6]
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findKDistantIndices(vecteur<int>& nums, touche int, int k) {
vecteur<int> rés;
int n = nombres.size();
int nextFree = 0; // plus petit indice non encore joint

pour (int j = 0; j < n; ++j) {
si (nums[j] == clé) {
int gauche = max(0, j - k);
int droite = min(n - 1, j + k);

int start = max (à gauche, à côté);
pour (int i = début; i <= droite; ++i)
res.push_back(i);
nextFree = droite + 1; // sauter les indices déjà ajoutés
}
}
retour rés;
}
};

Int main() {
Solution s;
vector<int> ans = s.findKDistantIndices({3,4,9,1,9,5}, 9, 1);
pour (int x : ans) cout << x << ' ';
// Produit: 1 2 3 4 5 6
}
«» "

> **Conseil** – Dans les trois langues, la logique fondamentale est identique :
> *Trouver l'intervalle autour de chaque clé, le fusionner avec l'intervalle déjà visité, et garder un pointeur libre de la fin. *

---

Analyse de complexité

Métrique Brute-Force
C'est pas vrai.
Temps Autres
**Espace auxiliaire** (hors de la liste des résultats)
**Taille du résultat** Autres

Avec `n ≤ 1 000', la solution optimale se terminera en millisecondes, tandis que la force brute peut prendre plusieurs centaines de millisecondes – assez souvent pour provoquer un avertissement lors d'un entretien chronométré.

---

Les pièges communs

Piège
- Oui.
**Ajouter des indices à l'intérieur de la totalité `[gauche, droite]` intervalle pour chaque clé** – conduit à des duplications. Utilisez le pointeur `nextFree` ou un `boolean[] vu`. Autres
** Erreurs hors-par-un lors de la mise à jour de `next Gratuit'**= N'oubliez pas: `nextFree = droite + 1`. Autres
**Ignorer les limites du tableau** (`j-k` < 0 ou `j+k` ≥ n)= Clamp avec `Math.max(0, ...)` et `Math.min(n-1, ...)`. Autres
**Utiliser un `Set` pour déduper des indices** – fonctionne mais utilise \(O(n)\) espace supplémentaire et peut ruiner la revendication \(O(1)\). Préférez l'astuce pointeur. Autres

---

À emporter pour les entrevues

1. ** Expliquez l'intuition** d'abord – parlez de chaque clé influence un intervalle contigu.
2. **Discute des compromis de complexité** – pourquoi vous éviterez \(O(n^2)\) quand vous pouvez faire \(O(n)\).
3. **Afficher le marquage d'un passage** – c'est un motif classique qui apparaît dans de nombreux problèmes d'intervalle (p. ex., le nombre maximum de robinets consécutifs II, le nombre minimum de robinets pour arroser un jardin).
4. ** Testabilité de Mention** – fournir quelques cas d'angle (k = 0, k ≥ n, tous les éléments égaux à la clé).

---

Liste de contrôle du référencement (si vous publiez ce message)

Comment optimiser pour les moteurs de recherche
-- -- -- -- -- ----------------------------------
**Titre** – ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Meta Description**=Découvrez comment résoudre LeetCode 2200, trouvez tous les indices K-Distants, avec un algorithme \(O(n)\) et nettoyez Java, Python et C++. Perfect interview prep. Autres
**En-têtes**= Utiliser H1 pour le titre, H2 pour les sections (Problème, Brute-Force, Optimal, Code, Complexité), H3 pour le code spécifique à la langue. Autres
**Liens internes**= Référence d'autres messages d'entrevue-prép sur les Tricks Two-Pointer ou les Sum préfixe pour les intervalles. Autres
**Liens externes**= Lien vers la page de problème LeetCode, vers votre repo GitHub, vers les ressources de recherche d'emploi. Autres
**Longueur du contenu**= 800–1,200 mots; assez pour couvrir le problème, le code et l'analyse sans être trop verbeux. Autres
**Images**= Inclure un petit diagramme du concept de ligne de balayage (facultatif). Autres
**Mots clés**= Indices à distance de k, code de leet 2200=, algorithme à deux points, interview de structure de données, code d'entrevue d'emploi. Autres

---

Comment utiliser cet article dans votre recherche d'emploi

1. **GitHub Gist** – Publiez le code Java/Python/C++ dans une repo publique et incluez le lien de repo dans votre CV.
2. **Portfolio** – Intégrez l'extrait de code et l'explication dans votre site personnel.
3. **Interview Prep** – Pratique expliquant les parties «good» (optimal), «bad» (brute-force) et «ugly» (bogues limites).
4. **Réseau** – Partagez le billet de blog sur LinkedIn avec une légende :
> J'ai juste craqué un problème de LeetCode que beaucoup d'intervieweurs aiment. #Java #Python #C++ #Structures de données #InterviewPréparer

---

Dernier verdict

*Le problème « Trouver tous les indices K‐Distants» est trompeurment simple, mais il cache un motif algorithmique soigné. En présentant une solution claire \(O(n)\) one-pass, vous prouvez que vous n'êtes pas seulement un codeur, vous êtes un problème-solveur efficace qui peut réduire la complexité du temps sans sacrifier la clarté. *

Bon codage, et bonne chance pour ces interviews !