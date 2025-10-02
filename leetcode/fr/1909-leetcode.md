---
titre: LeetCode 1909. Supprimez un élément pour rendre le tableau en augmentation stricte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 1909 – Retirez un élément pour rendre le tableau strictement croissant

Récapitulation du problème

> **Input:** `int[] nums "
> **Output:** `boolean` – `true` si nous pouvons supprimer *exactement un* élément de sorte que le tableau restant augmente strictement, sinon `faux`.
> **Définition:** *L'augmentation stricte* signifie «nums[i‐1] < nums[i]» pour chaque «i > 0».

**Principales contraintes *

Valeur des contraintes
C'est pas vrai.
"2 ≤ longueur nominale ≤ 1000"
< 1 ≤ nums[i] ≤ 1000 '

---

Solution O(n) à passe unique (Java / Python / C++)

L'idée centrale est de scanner le tableau une fois, en comptant le nombre de violations de l'endroit où le tableau cesse d'augmenter strictement.
Si nous trouvons **plus d'une violation**, nous ne pouvons jamais corriger le tableau avec une seule suppression → `false`.
Si nous trouvons **zéro** violations, le tableau est déjà en pleine augmentation → `true`.
Si nous trouvons **exactement une** violation à index `p`, nous devons vérifier si la suppression `nums[p]` ou `nums[p+1]` corrige le tableau & #160;:

- **Edge cas** – si la violation est à la première ou dernière position, nous pouvons toujours supprimer cet élément.
- ** Violation moyenne** – nous devons nous assurer qu'au moins une des conditions suivantes :
- Enlever `nums[p]` donne `nums[p‐1] < nums[p+1] "
- Enlever `nums[p+1]` donne `nums[p] < nums[p+2] "

Si aucune condition n'est remplie → `faux`.

---

### Java (temps O(n), espace O(1))

"Java
solution de classe {
public boolean canBeIncreasing(int[] nums) {
violations int = 0; // nombre de paires adjacentes problématiques
int idx = -1; // position de la dernière violation

pour (int i = 0; i < nombres.longueur - 1; i++) {
si (nums[i] >= nombres[i + 1]) {
violations++;
idx = i;
i (violations > 1) retourner faux; // sortie anticipée
}
}

// Déjà en augmentation stricte
si (violations) 0) retour vrai;

// Une violation
// 1) La suppression à une extrémité du tableau fonctionne toujours
si (idx) = 0.

// 2) Vérifiez si la suppression des nombres[idx] ou des nombres[idx+1] corrige la séquence
booléen supprimerIdx = nombres[idx - 1] < nombres[idx + 1];
booléen supprimerIdx1 = nombres[idx] < nombres[idx + 2];
retour supprimer RetirezIdx1;
}
}
«» "

---

### Python (temps O(n), espace O(1))

'`python
Solution de classe:
def canBeIncreasing(self, nombres: list[int]) -> bool:
violations = 0
idx = -1

pour i dans la plage (len(nums) - 1):
si nombres[i] >= Nombres[i + 1]:
violations += 1
idx = i
si des violations > 1 :
Retour Faux

en cas de violation 0:
retour Vrai

Si idx == 0 ou idx == len(nums) - 2:
retour Vrai

remove_idx = nombres[idx - 1] < nombres[idx + 1]
remove_idx1 = nombres[idx] < nombres[idx + 2]
retourner supprimer_idx ou supprimer_idx1
«» "

---

### C++ (temps O(n), espace O(1))

'`cpp
solution de classe {
public:
bool canBeIncreasing(vector<int>& nums) {
violations int = 0;
int idx = -1;

pour (int i = 0; i < (int)nums.size() - 1; ++i) {
si (nums[i] >= nombres[i + 1]) {
++violations;
idx = i;
i (violations > 1) retourner faux;
}
}

si (violations) 0) retour vrai;

si (idx) = (int)nums.size() - 2) retourner true;

bool removeIdx = nombres[idx - 1] < nombres[idx + 1];
bool removeIdx1 = nombres[idx] < nombres[idx + 2];
retour supprimer RetirezIdx1;
}
};
«» "

---

Billet de blog – Le bon, le mauvais et le mauvais de LeetCode 1909

- Oui. 1. Présentation

Si vous préparez des entrevues d'ingénierie logicielle, les problèmes de LeetCode sont votre meilleur ami.
Aujourd'hui, nous disséquerons **Problème 1909 – *Supprimer un élément pour faire en sorte que le tableau augmente strictement***.
Nous allons parcourir l'algorithme, analyser les cas de bord, comparer les compromis, et présenter un code propre, prêt à la production en **Java, Python et C++**.
Que vous soyez un codeur junior ou un candidat à l'entrevue senior, les idées ci-dessous renforceront votre confiance et brilleront sur votre CV.

> **SEO Mots-clés:** LeetCode 1909, supprimer un élément, tableau en augmentation stricte, codage d'entretien, solution Java, solution Python, solution C++, interview d'algorithme, conseils d'entretien de codage

---

- Oui. 2. La bonne solution – Pourquoi une seule passe gagne

- **Temps linéaire** – `O(n)` assure les balances de solution même pour le maximum `n = 1000`.
- **Espace continu** – Le stockage auxiliaire `O(1)` signifie que vous n'ajoutez pas de frais généraux.
- ** Logique claire** – Dénombrement des violations, des bords de la poignée, aucune récursion ou des structures de données supplémentaires.
- **Fast on LeetCode** – Benchmarks montrent ~0 ms runtime, battant les solutions les plus naïves.

**À emporter :** Un seul laissez-passer avec simple vérification conditionnelle est une réponse d'entrevue standard.

---

- Oui. 3. Les pièges communs

Pourquoi il échoue
- C'est quoi ?
**En supposant que le plus petit des deux fonctionne toujours**Vous pouvez supprimer l'élément incorrect lorsque le plus petit fait partie d'une tendance à la baisse plus longue. Autres Utilisez l'index * de la violation* et testez les deux scénarios de suppression. Autres
Les indices de répartition `i-1`, `i+1`, `i+2` sont délicats à la fin. Vérifier explicitement `idx=0` ou `idx=n-2` en premier. Autres
Utiliser `<` partout. Autres
**Suppression de la force brute**= O(n2) temps pour chaque cas d'essai. Utilisez l'approche de comptage et de vérification d'un seul passage. Autres

---

- Oui. 4. L'Ugly – Un Brute malléable Force alternative (et pourquoi nous l'évitons)

"Java
// Très lent – O(n^2)
public booléen peut êtreaugmenterBruteforce(int[] nums) {
pour (int i = 0; i < nombres de longueur; i++) {
int[] copie = nouvelle int[nums.longueur - 1];
pour (int j = 0, k = 0; j < nombres.longueur; j++) {
si (j != i) copie[k++] = nombres[j];
}
si (strictlyIncreasing(copie)) retourne vrai;
}
retourner faux;
}
«» "

- **Pourquoi c'est moche**:
- Temps quadratique (10002 = 1.000.000 ops) – encore rapide, mais loin d'être optimal.
- Allocation supplémentaire pour chaque suppression.
- Difficile à lire, plus difficile à expliquer dans une interview.

**Ligne de bottom:** Utilisez la logique monopass à moins que les contraintes n'autorisent explicitement la force brute.

---

- Oui. 5. Passage du code

C'est vrai. Java
- "violations" compte de mauvaises paires.
- `idx` enregistre la dernière violation de l'index gauche.
- Retour précoce en cas de violation > 1.
- Manipulation des bords pour le premier/dernier index.
- Contrôle final de la violation du milieu.

Python
- Miroirs de la logique Java; utilise une syntaxe concise (`len(nums)` et "pour moi à portée de main".
- Pas besoin de conseils de type `int` en Python 3.9+ (facultatif).

C++
- Utilise les indices "vector<int>" et "int".
- `static_cast<int>` pour éviter l'inadéquation signée.
- Même stratégie de sortie précoce.

---

- Oui. 6. Essais et validation

Autres Tests attendus Pourquoi
C'est pas vrai.
"[1,2,10,5,7] """ "true"" Enlever `10` corrige le tableau
"[2,3,1,2]"" "false"" "Aucune suppression ne donne une augmentation stricte"
Tous les congés de suppression `[1,1]` Autres
{\pos(192,210)}[1,2]} {\pos(192,210)}Déjà en pleine augmentation
Deux violations – impossibles
Enlever `5` ou `4`? Suppression Ouvrages

Exécutez ces cas de test dans votre boîte à sable IDE ou LeetCode préférée pour vérifier l'exactitude.

---

- Oui. 7. Conseils d'entrevue

1. ** Expliquez votre approche verbalement d'abord** – montrez l'idée de «one‐pass» et la manipulation de cas de bord.
2. ** Dessiner un diagramme** de la logique de violation; l'aide visuelle démontre la clarté.
3. **La complexité du temps et de l'espace** en amont.
4. **Parler des pièges de l'Ébau**; montrer la conscience des erreurs courantes impressionne les intervieweurs.
5. **Offre une implémentation concise** et demande s'ils aimeraient une version différente de la langue (Java, Python, C++).

---

- Oui. 8. Conclusion

LeetCode 1909 est un problème classique de moderate, qui teste la manipulation du tableau, la prise de conscience des cas de bord et l'efficacité algorithmique.
Une solution propre et unique en Java, Python ou C++ présente :

- Compréhension des règles d'inégalité strictes
- Capacité de raisonner sur les indices de tableau
- Lisibilité et performance du code

Déployez ces stratégies dans votre prochain entretien de codage et regardez le taux de montée de -yes. Bonne chance, et continuez à coder ! C'est ce qu'il a dit.

---

- Oui. 9. Bonus: SEO-Optimized Title & Meta Description

**Titre:**
*LeetCode 1909: Supprimez un élément pour rendre la répartition strictement croissante – Java, Python, C++ Solutions & Conseils d'entrevue*

**Meta Description:**
*Master LeetCode 1909 avec une solution rapide et unique en Java, Python et C++. Apprenez à gérer les cas de pointe, les pièges communs et les stratégies d'entrevue pour décrocher votre prochain travail d'ingénierie logicielle. *

---