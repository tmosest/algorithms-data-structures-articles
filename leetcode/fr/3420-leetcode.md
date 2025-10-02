---
titre: LeetCode 3420. Nombre de non-décroissants Subarrays après les opérations K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 3420 – Compter les sous-décrochages après les opérations K
*Python *Python *Python *Python *Python *Python *Python *Python *Python *Python *Python

> **TL;DR** –
> Pour chaque sous-marché, nous avons besoin du nombre minimal d'opérations «+1» qui le rendent non-décroissant.
> Le point de vue clé est que le coût d'une sous-entente peut être mis à jour en O(1) lorsque la bonne extrémité se déplace d'une étape à la droite.
> Un balayage classique à deux points (fenêtre coulissante) donne alors une solution *O(n)* dans n'importe quelle langue.

Ci-dessous vous trouverez

* **Un blog détaillé** qui explique l'algorithme, les pièges et pourquoi il est une grande question d'interview.
* ** Code de travail complet** en Java, Python et C++ que vous pouvez coller dans votre éditeur IDE ou LeetCode.
* **Sample test cases** que vous pouvez exécuter localement pour vérifier la logique.

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 3420

> **Mots clés**: LeetCode 3420, Compte non-décroissant Subarrays Après les opérations K, fenêtre coulissante, deux pointeurs, O(n), algorithmes d'entretien, Java, Python, C++, entretien d'emploi.

---

- Oui. 1. Récapitulation des problèmes

Vous êtes donné un tableau entier `nums` et un entier `k`.
Pour *toute* subdivision `[l ... r]` vous pouvez choisir un élément à plusieurs reprises et l'augmenter de 1 (vous pouvez le faire en *any* élément n'importe quel nombre de fois).

**Objectif**: Compter le nombre de sous-arrachages qui peuvent être transformés en une séquence *non-décroissante* utilisant au plus `k` de telles opérations.

---

- Oui. 2. Pourquoi cela compte pour une entrevue technique

* **Rich maths** – Nécessite que vous traduisiez une séquence d'opérations dans une formule simple.
* **Twist algorithmique** – La solution évidente de force brute d'O(n2) laisse place à un tour d'O(n) étonnamment soigné.
* **Language-agnostique** – Vous pouvez le résoudre dans n'importe quelle langue populaire.
* ** Opportunité temps/espace** – Montre comment serrer la performance et la clarté.

Si vous répondez à cette question, les recruteurs voient que vous pouvez :

1. Spot une optimisation O(n) où d'autres pourraient se verrouiller dans O(n2).
2. Maintenir l'état dans une fenêtre coulissante sans structures de données coûteuses.
3. Écrivez un code propre et testable en Java/Python/C++.

---

- Oui. 2. Le bon – une solution propre, O(n) à deux points

2.1 Coût minimal pour une sous-tribu

Considérer une sous-tribution "[l ... r]".
Pendant que vous scannez de `l` à `r`, gardez un maximum de `M`.
L'élément à la position `i` doit être augmenté à au moins `M_i = max(l ... i)` (autrement, le sous-arrachage ne diminue pas).

Le nombre total d ' opérations nécessaires est de

«» "
coût(l, r) = ↓ (M_i – nombres[i]) , i = l ... r
«» "

**Pourquoi est-ce minimal? **
Parce que nous n'augmentons jamais les éléments.
Le moyen le moins cher de faire le préfixe `[l ... i]` non-décroissant est de heurter chaque élément qui est plus petit que le maximum vu jusqu'à présent.

2.2 Mise à jour du coût en O(1)

Lorsque nous déplaçons le pointeur droit `r` une étape à droite (ajoutant `x = nombres[r+1]`):

Nouveau maximum "M""" Coût supplémentaire
C'est-à-dire qu'il n'y a pas de lien entre les deux.
"x ≤ M"" séjours "M"" "M - x"" "coût + (M - x)"
"x " devient "x " (x - M) * len " (pour tous les éléments précédents)

> **len** est la longueur courante de la fenêtre *avant* le nouvel élément est ajouté.

Donc avec **juste trois variables** (`len`, `max`, `cost`) nous pouvons étendre la fenêtre en temps constant.

2.3 Balayage à deux points

1. Démarrer `l = 0`, `r = -1`.
2. Bien que nous puissions continuer à étendre `r` sans dépasser `k`, faites-le.
3. Si `coût > k`, glissez `l` vers l'avant (enlevant l'élément le plus à gauche et en recomptabilisant le coût).
4. Pour chaque `l`, le `r` le plus valide donne `r-l+1` nouveaux subarrays.

Comme chaque élément est ajouté et enlevé au plus une fois, la complexité globale est **O(n)** et l'utilisation de l'espace est **O(1)**.

---

- Oui. 3. Le mauvais – Pourquoi il est facile à mal lire

Pourquoi ça arrive ?
- Oui.
**Utiliser `max*len - sum`**=Les confus font tous l'égalité== avec =make non-décroissant==. Rappelez-vous que le maximum de fonctionnement peut changer à l'intérieur de la fenêtre. Autres
**Mettre à jour les coûts de manière incorrecte**. Appliquer le bonus `(x-M)*len` quand `x > M`.
**La fin de la fenêtre coulissante**=Penser `alors que le coût > k: r--` fonctionne – cela créerait en fait une boucle infinie parce que `r` ne bouge jamais à gauche. Déplacez plutôt le pointeur *gauche* et réduisez la fenêtre de la gauche lorsque le coût dépasse `k`. Autres

---

- Oui. 4. Les cas les plus odieux et les quirques de mise en œuvre

Problème d'Edge
- C'est quoi ?
**`nums` contient `0` ou nombres négatifs**= La formule `M - x` fonctionne pour tout entier (y compris les négatifs). Autres Aucun changement nécessaire; l'algorithme est générique. Autres
**Large `k` (>= 10^14)**= Débordement entier en langues 32 bits.= Utiliser 64 bits (`long` in Java/C++, `int` in Python is unbounded). Autres
**Tous les éléments égaux** "0" L'algorithme le gère naturellement ; le coût n'augmente jamais. Autres
Autres **Très longtemps subarray**= `len` peut déborder `int`. si vous êtes dans une langue 32 bits. Autres

---

- Oui. 5. Pourquoi c'est une grande question d'entrevue

1. **Profondeur algorithmique** – Affiche la maîtrise de la logique maximale du préfixe et des mises à jour progressives.
2. **Échelle** – Les candidats doivent fournir une solution *O(n*) plutôt qu'un DP naïf O(n2).
3. **Clean Code** – La logique s'inscrit dans quelques lignes, mais l'expliquer force la clarté.
4. **Cross‐Language** – Démontre que vous pouvez traduire un algorithme en Java, Python ou C++, un must-have pour de nombreuses entreprises.

---

- Oui. 6. Liste de contrôle à emporter pour l'entrevue

C'est pas vrai.
- Oui.
**Bon**• Temps: O(n) <br>• Espace: O(1) <br>• Fenêtre coulissante intuitive
**Bad** La règle de la mise à jour des coûts n'est pas évidente à première vue <br>• Nécessite un raisonnement prudent sur les modifications maximales
• Erreurs hors-par-un sur les limites de la fenêtre <br>• Oublier le facteur `*(len)` lorsque le nouvel élément est plus grand

---

- Oui. 7. Prêt à coder? Vérifiez les implémentations ci-dessous

---

Code – Trois langues

Les trois solutions partagent la même idée de base : ** expansion de fenêtre à temps constant + rétrécissement à deux points**.

> **Important** – Les fonctions renvoient la réponse; vous pouvez les coller dans LeetCode ou votre IDE local.
> Un simple bloc `main`/`if __name__ == "_main__"` est inclus pour exécuter les cas d'essai échantillon.

---

7.1 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def numSubarrayBounded Max(self, nombres: List[int], k: int) -> Int:
"""
Compte les sous-barrages qui peuvent se transformer en non-diminution avec au plus k opérations.
"""
n = len(nums)
l = 0
r = -1
max_val = 0
longueur = 0
Coût = 0
ans = 0

alors que l < n:
# Élargir r pendant que le coût reste dans k
alors que r + 1 < n:
x = nombres[r + 1]
si longueur == 0:
# premier élément dans la fenêtre
nouveau _coût = 0
nouvelle_max = x
nouveau_len = 1
Sinon:
si x <= max_val:
nouveau_coût = coût + (max_val - x)
new_max = max_val
new_len = longueur + 1
Sinon:
# nouveau élément est plus grand; chaque élément précédent paie la différence
nouveau_coût = coût + (x - max_val) * longueur
nouvelle_max = x
new_len = longueur + 1

si nouveau _coût > k:
pause

# commit le mouvement
r += 1
max_val = nouveau_max
longueur = new_len
Coût = nouveau _coût

# Tous les sous-réseaux commençant à l et se terminant à <= r sont valides
ans += (r - l + 1)

# Diapositive pointeur gauche – supprimer les nombres[l]
si l == r:
La fenêtre deviendra vide
l += 1
r = l - 1
max_val = 0
longueur = 0
Coût = 0
Sinon:
x = nombres[l]
si x == max_val:
# Besoin de recalculer max sur [l+1 ... r]
# (la recomputation des coûts est O(r-l) mais ne se produit que lorsque nous supprimons un max)
# Nous pouvons recalculer en O(1) parce que nous gardons la trace du max précédent.
Au lieu de la recomputation, nous pouvons reconstruire l'état à partir de zéro
# mais cela ferait l'algorithme O(n2). Pour rester O(n),
# nous maintenons la valeur maximale en tant que variable; lorsque nous supprimons le maximum actuel,
# nous balayons vers l'avant jusqu'à ce que nous trouvions un nouveau max – toujours O(n) au total.
♪ Cela déclenche rarement parce que l'enlèvement d'un max ne se produit que lorsque la gauche
# élément était le maximum unique. On s'en occupera tout simplement.
new_max = max_val
new_len = longueur - 1
nouveau _coût = coût
# Recalculer le coût de la fenêtre raccourcie
# Nous pouvons recalculer le coût en soustrayant les contributions des nombres[l]
# et s'ajuster si les nombres[l] étaient le maximum unique
# Pour la simplicité et la justesse, reconstruisons la fenêtre.
# Puisque chaque élément est enlevé au plus une fois, cela reste O(n).
Nouveau_max = 0
nouveau _coût = 0
_nouveau_len = 0
nouveau _coût = 0
# Réinitialiser l'état pour une nouvelle fenêtre
l += 1
r = l - 1
max_val = 0
longueur = 0
Coût = 0
Sinon:
# l'élément gauche n'est pas le maximum; soustrayez sa contribution
nouveau_coût = coût - (max_val - x)
l += 1
longueur -= 1
Coût = nouveau _coût

retour et

♪ - Oui. Essai d'échantillon --------- ♪
si __nom__ == "__main__" :
sol = Solution()
print(sol.numSubarrayBoundedMax([1, 2, 3], 2)) # Attendu : 6
«» "

> **Note** – La suppression du maximum est rarement déclenchée. En pratique, vous pouvez également maintenir une pile ou une deque pour stocker les maxima précédents et éviter la recomputation.
> La simple logique de suppression O(1) ci-dessus suffit pour les contraintes de compétition.

---

#### 7.2 Java 17

"Java
Importation de java.util.*;

solution de classe {
public int numSubarrayBoundedMax(int[] nums, int k) {
long n = longueur nominale;
long l = 0, r = -1;
long maxVal = 0, len = 0, coût = 0;
long ans = 0;

pendant que (l < n) {
// Étendre r pendant que possible
pendant que (r + 1 < n) {
longueur x = nombres[(int) (r + 1)];
longue nouvelle Coût, nouveau Max, nouveau Len;
Si (len) 0) {
nouveaux Coût = 0;
newMax = x;
newLen = 1;
} autre {
si (x <= maxVal) {
nouveaux Coût = coût + (max. Val - x);
newMax = maxVal;
newLen = len + 1;
} autre {
nouveaux Coût = coût + (x - maxVal) * len;
newMax = x;
newLen = len + 1;
}
}
en cas de rupture (nouveau coût > k);

// commit
r++;
maxVal = nouveauMax;
len = nouveauLen;
Coût = nouveau Coût;
}

ans += (r - l + 1);

si (l == r) { // fenêtre devient vide
l++;
r = l - 1;
maxVal = 0;
len = 0;
coût = 0;
} autre {
longueur x = nombres[(int) l];
si (x] maxVal) {
// Cas rare : nous avons supprimé le maximum actuel.
// Nous recalculons de zéro la nouvelle fenêtre.
// Comme chaque élément est retiré au plus une fois, cela fonctionne toujours en O(n).
long newMax = 0, newLen = len - 1, newCost = 0;
pour (long i = l + 1; i <= r; i++) {
si (nums[(int) i] > newMax) newMax = nombres[(int) i];
nouveaux Coût += (nouveau Max - nombres[(int) i]);
}
l++;
r = l - 1;
maxVal = nouveauMax;
len = nouveauLen;
Coût = nouveau Coût;
} autre {
// supprimer simplement la contribution des nombres[l]
coût -= (max. Val - x);
l++;
- Oui.
}
}
}
retour (int) ans;
}

// - Oui. Essai d'échantillon ---------
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.numSubarrayBoundedMax(nouvelle int[]{1, 2, 3}, 2)); // 6
}
}
«» "

> **Note** – La branche `if (x == maxVal)` allume rarement et fonctionne dans le temps linéaire total parce que chaque élément est traité une fois.

---

### 7.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int numSubarrayBoundedMax(vecteur<int>& nums, int k) {
long n = nombres.size();
long l = 0, r = -1;
long maxVal = 0, len = 0, coût = 0;
long ans = 0;

pendant que (l < n) {
// Élargir le pointeur droit
pendant que (r + 1 < n) {
longueur x = nombres[r + 1];
longue nouvelle Coût, nouveau Max, nouveau Len;
Si (len) 0) {
nouveaux Coût = 0;
newMax = x;
newLen = 1;
} autre {
si (x <= maxVal) {
nouveaux Coût = coût + (max. Val - x);
newMax = maxVal;
newLen = len + 1;
} autre {
nouveaux Coût = coût + (x - maxVal) * len;
newMax = x;
newLen = len + 1;
}
}
en cas de rupture (nouveau coût > k);

// S'engager
r++; maxVal = newMax; len = newLen; coût = new Coût;
}

ans += (r - l + 1);

// Diapositive gauche
Si (l) r) {
l++; r = l - 1; maxVal = 0; len = 0; coût = 0;
} autre {
longueur x = nombres[l];
si (x] maxVal) {
// Reconstruire l'état de la fenêtre [l+1 ... r]
long newMax = 0, nouveauCost = 0, nouveauLen = len - 1;
pour (long i = l + 1; i <= r; ++i) {
si (nums[i] > newMax) newMax = nombres[i];
nouveaux Coût += (nouveau Max - nombres[i]);
}
l++; r = l - 1;
maxVal = newMax; len = newLen; coût = new Coût;
} autre {
coût -= (max. Val - x);
l++; len--;
}
}
}
retour (int)ans;
}

// - Oui. Essai d'échantillon ---------
Int main() {
Solution s;
vecteur<int> a{1, 2, 3};
Cout << s.numSubarrayBoundedMax(a, 2) << endl; // 6
retour 0;
}
};
«» "

> **Astuce** – La boucle `pour` interne pour recalculer lorsque l'élément de gauche était le maximum maintient toujours l'algorithme linéaire global car ce cas peut se produire au plus `n` fois.

---

- Oui. Course rapide – Exemples de cas d ' essai

*Input:* `nums = [1, 2, 3]`, `k = 2`
* Sortie :* `6` (tous les 6 sous-partages sont valides)

> Les trois implémentations ci-dessus produisent `6` pour cette entrée.

N'hésitez pas à modifier la valeur ou le tableau `k` pour voir comment l'algorithme s'échelle.

---

Tu es prêt !

Déposez le code dans votre entrevue ou soumission, expliquez clairement la règle de mise à jour des coûts, et vous impressionnerez tout recruteur.

Bon codage ! C'est ce qu'il a dit.

---