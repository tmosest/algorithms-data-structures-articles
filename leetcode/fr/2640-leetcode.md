---
titre: LeetCode 2640. Trouvez le score de tous les préfixes d'un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2640. Trouvez le score de tous les préfixes d'un tableau
**A Complet, SEO-Optimized Blog Post + 3-Language Solution**

> *LeetCode 2640 – ♫Trouver la partition de tous les préfixes d'un tableau*
> *Java, Python, implémentations C++*
> *Interview-ready, O(n) time et O(1) space solution*

---

- Oui. 1. Récapitulation des problèmes

On vous donne un tableau entier indexé à 0 **nums** de longueur *n* (1 ≤ *n* ≤ 105).
Pour chaque préfixe `nums[0..i]` vous devez:

1. Construire le tableau *conversion*
`conver[j] = nombres[j] + max(nums[0..j]) "
2. Sommez le tableau de conversion → le *score* de ce préfixe.

Retourner un tableau `ans` où `ans[i]` est le score du préfixe se terminant à l'index `i`.

> **Exemple**
> nombres = `[2,3,7,5,10]` → ans = `[4,10,24,36,56]`

---

- Oui. 2. Pourquoi ça a l'air dur (la partie "Ugly")

À première vue, vous pourriez penser que vous devez recalculer le maximum pour chaque préfixe, conduisant à **O(n2)**.
La torsion est que **max(nums[0..j])** peut être maintenu *online* comme vous itérer – un seul passage suffit.

---

- Oui. 3. La solution Élégante --Bien – Préfixe Somme + Running Maximum

Étape Ce que nous conservons Pourquoi ça marche
- C'est quoi ?
"currMax" – valeur maximale vue jusqu'à présent" `max(nums[0..i]) est exactement le maximum en cours d'exécution. Autres
Chaque nouvelle valeur de conversion est `nums[i] + currMax`; ajoutez-la au total précédent. Autres

C'est ça – **une boucle** sur le tableau.

Code Pseudo

«» "
currMax = 0
Total général Note = 0
pour chaque nombre en nombres:
currMax = max(currMax, num)
Total général Score += nombre + currMax
Total du stockage Score dans le tableau de réponses
«» "

Aucun tableau supplémentaire pour les valeurs de conversion n'est nécessaire – nous les calculons à la volée.
Complexités:

- **Heure**: `O(n)` – un laissez-passer.
- **Espace**: "O(1)" – seulement quelques scalars plus le tableau de sortie.

---

- Oui. 4. Mise en œuvre intégrale

On trouvera ci-dessous des solutions propres, prêtes à être copiées dans **Java**, **Python** et **C++**.

> **Note:** Tous les trois utilisent `long`/`long` pour éviter le débordement (nums[i] ≤ 109, n ≤ 105 → somme ≤ 2 × 1014).

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public long[] findPrefixScore(int[] nums) {
int n = longueur nums;
long[] ans = nouveau long[n];

nt currMax = 0;
long total = 0;
pour (int i = 0; i < n; i++) {
currMax = Math.max(currMax, nombres[i]);
Total += nombres[i] + currMax;
ans[i] = total;
}
le retour des an;
}

// Pilote simple pour des tests rapides
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
nombres int[] = {2, 3, 7, 5, 10};
Système.out.println(Arrays.toString(s.findPrefixScore(nums)));
}
}
«» "

---

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def trouver PréfixeScore(self, nombres: List[int]) -> Liste[int]:
ans = []
_max_curr = 0
Total = 0
pour num in nums:
curr_max = max(curr_max, num)
Total += num + curr_max
(total)
retour et

# Test rapide
si __nom__ == "__main__" :
s = Solution()
print(s.findPrefixScore([2, 3, 7, 5, 10]))
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<long> findPrefixScore(vector<int>& nums) {
vecteur <long> ans;
ans.reserve(nums.size());

nt currMax = 0;
long total = 0;
pour (int num : nombres) {
currMax = max(currMax, num);
Total += nombre + currMax;
ans.push_back(total);
}
le retour des an;
}
};

// harnais d'essai simple
Int main() {
Solution s;
vecteur<int> nombres = {2, 3, 7, 5, 10};
auto res = s.findPrefixScore(nums);
pour (auto v : res) cout << v << " ";
cout << endl;
}
«» "

---

- Oui. 5. Cas de bord et pièges communs

Autres Décision Quoi faire ?
-- -- -- -- -- -- -- -- -- -- --
**Les plus grands nombres**= Utiliser 64 bits (`long` / `long`). Autres
**Tous les éléments égaux**. Autres
**Les mises à jour `currMax` sont strictement décroissantes seulement au premier élément. Autres
**Longueur de l'entrée = 1**. Autres
**Nombres négatifs** (pas dans les contraintes) Autres

---

- Oui. 6. Pourquoi cette solution gagne des entrevues

1. **Simplicité** – une boucle, variables minimales.
2. **Optimalité** – passe toutes les limites du leetcode (105 éléments).
3. **Readability** – noms de variables clairs (`currMax`, `total`).
4. **Langue Agnostique** – la logique est la même à travers Java, Python, C++.

Les intervieweurs demandent souvent : *=Pouvez-vous éviter de recalculer le maximum pour chaque préfixe ?===* – répondre avec le tour maximum en cours.

---

- Oui. 7. Autres améliorations (facultatives)

Idées Avantages
C'est pas vrai.
**Streaming** – si l'entrée vient comme un flux, vous pouvez afficher des scores immédiatement. Pas besoin de tableau supplémentaire. Il faut gérer le formatage de sortie. Autres
**Parallel prefix sum** – pour les tableaux massifs sur GPU. Accélération sur les grandes données. Overkill pour les contraintes LeetCode. Autres

---

- Oui. 8. Tâches finales

- **Score préfixe** = somme cumulée de "nums[i] + runningMax".
- Maintenir un seul "currMax" et un "total".
- **O(n) temps, O(1) espace auxiliaire** – la solution la plus propre.
- Fonctionne parfaitement en Java, Python et C++.

N'hésitez pas à déposer cela dans votre trousse d'entrevue!

---

- Oui. 9. Mots clés du référencement

- LeetCode 2640
- Trouvez le score de tous les préfixes d'un tableau
- Algorithme de somme préfixe
- Solution de préfixe Java
- Solution de préfixe Python
- Solution de préfixe C++
- Problèmes de codage des entretiens
- complexité du temps O(n)
- O(1) complexité spatiale
- Courant maximum
- Résolution de problèmes algorithmiques

Bon codage, et bonne chance pour ce travail !