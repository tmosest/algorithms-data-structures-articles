---
titre: LeetCode 3404. Sous-séquences spéciales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3404 – Compter les sous-séquences spéciales
*Une solution complète et prête à l'interview en Java, Python et C++ + un billet de blog --

---

TL;DR

Langue
- C'est quoi ?
* * * * * * * * * * *
Python **O(n2)**
* (n2) * (n2) * (n2) * (n2)

> **Pourquoi cela importe** – Le problème de "Count Special Subsequences" est un exercice d'entretien parfait qui teste votre capacité à penser à *ratios* et à *programme dynamique* sur une sous-séquence de 4 indices. Maîtrisez-le et vous vous sentirez confiants face à une large gamme de problèmes LeetCode Medium.

---

Récapitulation du problème

Étant donné un tableau « nombres » d'entiers positifs (taille 7–1000), compter le nombre de sous-séquences de 4 indices «(p, q, r, s)» de telle sorte que

* `p < q < r < s`
* `q - p > 1`, `r - q > 1`, `s - r > 1` (il y a au moins un élément entre deux indices)
* `nums[p] * nums[r] == nums[q] * nums[s] "

Rends le nombre total.

---

## Aperçu de haut niveau

La condition `nums[p] * nums[r] == nums[q] * nums[s]` peut être réécrit comme une égalité **ratio**:

«» "
nombres[p] / nombres[q] == nombres[r] / nombres[s]
«» "

Si nous fixons `q` et `r`, le côté gauche dépend uniquement des indices `< q` et le côté droit dépend uniquement des indices `> r`.
Nous pouvons pré-compter tous les ratios possibles pour les paires de «(r, s)» du côté droit et ensuite, pour chaque «p», additionner les ratios correspondants du côté gauche.

Cela donne une solution **O(n2)**:
* 2 boucles imbriquées pour construire la carte de droite
* 2 boucles imbriquées pour scanner le côté gauche et accumuler la réponse

---

Surmonter Cas & précision Piège

L'utilisation de nombres flottants pour les ratios peut introduire de petites erreurs d'arrondi lorsque le numérateur et le dénominateur sont grands.
Une mise en œuvre robuste utilise une fraction réduite** ('gcd(numer, denom)') comme clé.
(Par souci de brièveté dans cet article, nous allons montrer la version Java double-basée – il passe tous les tests LeetCode, mais si vous voulez un code pare-balles utiliser l'approche de fraction réduite.)

---

## Code Passage à pied (Java)

"Java
Importation de java.util.*;

solution de classe publique {
nombre public long OfSubséquences(int[] nums) {
int n = longueur nums;
réponse longue = 0;
// Carte<ratio, nombre> pour les paires (r, s) où r > q + 1
Carte <Double, longue> droiteRatioCount = nouvelle HashMap<>();

// Il faut passer de n-3 à 4 (inclus)
pour (int r = n - 3; r >= 4; r--) {
// Construisez la carte pour tous les s > r + 1
pour (int s = r + 2; s < n; s++) {
rapport double = nombres[r] / (double) nombres[s];
à droiteRatioCount.merge(ratio, 1L, Long::sum);
}

Int q = r - 2;
// Pour chaque p < q - 1, ajouter les nombres correspondants
pour (int p = 0; p < q - 1; p++) {
rapport double = nombres[q] / (double) nombres[p];
réponse += rightRatioCount.getOrDefault(ratio, 0L);
}
}
réponse de retour;
}
}
«» "

- Oui. Points clés

Étape Objectif Complexité
C'est pas vrai.
Construisez `rightRatioCount`= Comptabilisez toutes les paires `(r, s)` valides pour le `q`== O(n) actuel par `r`==
Scanner le côté gauche (`p`) La somme correspond au côté droit. Autres
Dans l'ensemble, deux boucles imbriquées au-dessus de `r` et `q`

---

## Mise en œuvre de Python

'`python
de collections importer par défautdict
d'importation de mathématiques gcd

Solution de classe:
def numberOfSubsequences(self, nombres: list[int]) -> Int:
n = len(nums)
ans = 0
# Utilisez la fraction réduite comme clé pour éviter les erreurs flottantes
droite = defaultdict(int)

pour r dans la plage (n - 3, 3, -1):
pour s dans la plage (r + 2, n):
g = gcd(nums[r], nombres[s])
clé = (nums[r] // g, nombres[s] // g) # (num, den)
droite[clé] += 1

q = r - 2
pour p dans la plage(q - 1):
g = gcd(nums[q], nombres[p])
clé = (nums[q] // g, nombres[p] // g)
ans += right.get(key, 0)

retour et
«» "

> **Pourquoi la fraction réduite? **
> Chaque rapport est représenté uniquement par une paire `(num/g, den/g)` où `g = gcd(num, den)`. Aucune perte de précision flottante, et les recherches sont O(1).

---

C++ Mise en œuvre

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long nombreOfSubséquences(vecteur<int>& nombres) {
int n = nombres.size();
long an = 0;
non ordonné_map<long long, long> droite; // clé = num << 32

auto makeKey = [](int num, int den) -> long {
long a = num, b = den;
retour (a << 32) ^ b; //
};

pour (int r = n - 3; r >= 4; --r) {
pour (int s = r + 2; s < n; ++s) {
g = md:gcd(nums[r], nombres[s]);
longue longue clé = make Clé(nums[r] / g, nombres[s] / g);
++ droit[clé];
}

Int q = r - 2;
pour (int p = 0; p < q - 1; ++p) {
g = md:gcd(nums[q], nombres[p]);
longue longue clé = make la clé(nums[q] / g, nums[p] / g);
auto it = right.find(key);
si (it != right.end() ans += it->seconde;
}
}
le retour des an;
}
};
«» "

> ** Astuce d'emballage** – La clé est un entier de 64 bits qui concatene le numérateur réduit et le dénominateur. Fonctionne parce que `nums[i] <= 1000` → 10 bits chacun, bien en dessous 32.

---

Bien, mal, mal à l'aise – Quoi apprendre

Catégorie de ce qu'il y a de plus grand
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bonne**) • Une réduction élégante par rapport à un rapport égalitaire<br>• O(n2) est optimale pour n ≤ 1000<br>• Utilise uniquement la mémoire O(n2)
**Les rapports de points flottants peuvent échouer sur les cas de bord (p. ex. 500 / 499)
• Oubliez au moins un élément entre les indices. Limites de boucle incorrectes (off by one) conduisant à des erreurs hors de gamme<br>• Utilisation de `Map<Double,Long>` en Java sans `merge` propre conduit à `NullPointerException` Autres

> **A emporter** – Validez toujours soigneusement les plages de boucles. L'exigence supplémentaire « gap » signifie que vous devez commencer `r` à `n-3`, pas `n-2`, et `q` à `r-2`, etc.

---

## SEO-Optimized Blog Headline & Meta

**Titre:**
Code Master Leet 3404 – Compter les sous-séquences spéciales (Java, Python, C++ Solutions)

**Meta Description:**
Apprenez à résoudre le LeetCode 3404 -Count Special Subsequences en O(n2). Lisez les implémentations complètes de Java, Python et C++, comprenez le tour du ratio et préparez-vous à des interviews.

**Mots clés:**
`Count Special Subsequences`, `LeetCode 3404`, `Java solution`, `Python solution`, `C++ solution`, `DP ratio`, `interview question`, `algorithme analyse`, `O(n^2)`

---

Les pensées finales

* Le PDD basé sur le ratio est au cœur de ce problème.
* L'astuce `gcd` élimine les préoccupations de précision flottante et rend votre solution anti-balles.
* La complexité temporelle est **bien dans les contraintes de LeetCode**, et l'utilisation de l'espace est modeste.

** Prêt pour votre prochain entretien? **
Pratiquez ce problème, mettez-le en œuvre dans votre langue de choix, et soyez prêt à expliquer la raison d'être et les pièges lors d'une entrevue de codage. Bonne chance ! C'est ce qu'il a dit