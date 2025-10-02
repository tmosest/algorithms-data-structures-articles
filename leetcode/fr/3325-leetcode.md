---
titre: LeetCode 3325. Compter les sous-chaînes avec les caractères de fréquence K Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Leetcode 3325 – Sous-chaînes de comptage avec caractères de fréquence K I
**Solution en Java / Python / C++**
**Heure:** "O(n)" **Espace:** "O(1)"

> **Problème**
> Compter le nombre de sous-chaînes de `s` dans lesquelles *au moins un* caractère apparaît **au moins `k` fois**.

> **Exemples**
> *Input* `s = "abacb"`, `k = 2` → ** Sortie:** `4`
> *Input* `s = "abcde"`, `k = 1` → ** Sortie:** `15` (chaque sous-chaîne est valide)

> **Constraints**
> * 1 ≤ "s.longueur" ≤ 3000
> * `k` ≤ `s.longueur "
> * `s` ne contient que des lettres minuscules (`a``z`)

L'astuce de la fenêtre coulissante ci-dessous transforme un problème apparemment des caractères du compte en un balayage linéaire.

---

- Oui. 2. Idée de base – Fenêtre coulissante sur les personnages trop nombreux

1. **Total des sous-chaînes** d'une chaîne de longueur `n` = `(n + 1) * n / 2`.
2. Si une sous-chaîne a un caractère **no** avec une fréquence ≥ k, elle est *invalide*.
3. Nous maintenons une fenêtre coulissante `[l, r]` telle que **no** caractère à l'intérieur de la fenêtre se produit `k` ou plus fois.
4. Pour chaque extrémité droite `r`, le nombre de sous-chaînes *invalides* se terminant par `r` est exactement `r - l + 1`.
5. Soustrayez ceci du total pour obtenir la réponse.

La fenêtre se rétrécit seulement lorsque le caractère à `s[r]` atteint une fréquence de `k`.
Parce que chaque caractère est ajouté et supprimé au maximum une fois, l'algorithme entier tourne dans `O(n)`.

---

- Oui. 3. Exécution

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
Nombre d'entrées publiques DeSous-chaînes(String s, int k) {
int n = s.longueur();
// Toutes les sous-chaînes moins les "mauvaises"
résultat int = (n + 1) * n / 2;
int[] freq = nouvelle int[26]; // fréquence de chaque lettre
int gauche = 0; // pointeur gauche de la fenêtre

pour (int right = 0; right < n; right++) {
char c = s.charÀ droite;
freq[c - 'a']++;

// Réduire la fenêtre pendant que nous avons un caractère avec >= k occurrences
pendant que (freq[c - 'a'] >= k) {
freq[s.charA (à gauche) - 'a']--;
gauche++;
}

// Toutes les sous-chaînes se terminant à 'à droite' qui sont *mauvais*
-= (droite - gauche + 1);
}
le résultat du retour;
}

// Pour des essais manuels rapides
public statique vide principal(String[] args) {
System.out.println(nouvelle solution().numberOfSubstrings("abacb", 2)); // 4
System.out.println(nouvelle solution().numberOfSubstrings("abcde", 1)); // 15
}
}
«» "

3.2 Python

'`python
Importations provenant des collections Compteur

Solution de classe:
Numéro DeSous-chaînes(self, s: str, k: int) -> Int:
n = len(s)
résultat = (n + 1) * n // 2
freq = compteur()
gauche = 0

pour droite, ch en énumération(s):
[ch] += 1
pendant que freq[ch] >= k:
freq[s[gauche]] -= 1
gauche += 1
résultat -= (droite - gauche + 1)

résultat du retour


Essais rapides
si __nom__ == "__main__" :
print(Solution().numberOfSubstrings("abacb", 2)) # 4
print(Solution().numberOfSubstrings("abcde", 1)) # 15
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Numéro int DeSous-chaînes(chaîne s, int k) {
int n = s.size();
longue rés = 1LL * (n + 1) * n / 2; // total des sous-chaînes
vecteur <int> freq(26, 0);
Int gauche = 0;

pour (int droite = 0; droite < n; ++ droite) {
int idx = s[right] - 'a';
++freq[idx];

pendant que (freq[idx] >= k) {
--freq[s[gauche] - 'a'];
+ + gauche;
}

res -= (droite - gauche + 1); // mauvaises sous-chaînes
}
retour (int)res;
}
};

// Pour des essais manuels rapides
Int main() {
Solution sol;
Cout << sol.number OfSubstrings("abacb", 2) << endl; // 4
cout << sol.numberOfSubstrings("abcde", 1) << endl; // 15
}
«» "

Les trois implémentations partagent la même logique :
*Couvercle de tous les sous-chaînes → soustrayez les deux autres avec une fenêtre coulissante rétrécie. *

---

- Oui. 4. Article de blog – Leetcode 3325: Mastering the Sliding Window to Crack the K‐Frequecy Substrings Interview

> **Meta‐Description** – Vous voulez décrocher ce travail d'ingénierie logicielle? Apprenez la solution Slick O(n) à Leetcode 3325 -Count Substrings with K‐Frequence Characters I-- en Java, Python et C++. Obtenez la panne de la technique de la fenêtre coulissante, les pièges, et comment l'expliquer sur un tableau blanc.

### 4.1 Pourquoi ce problème agit votre portefeuille d'entrevues

- **String + Sliding Window** – Un combo classique que beaucoup d'intervieweurs aiment.
- **Temps-Espace – O(n) temps, O(1) espace montre que vous pouvez raisonner sur les limites asymptotiques.
- ** Contraintes évolutives** – 3000 caractères → force brute O(n2) sera TLE.
- **Maîtrise de la langue brute** – Vous pouvez implémenter le même algorithme en Java, Python ou C++.

### 4.2 Le bon – ce qui rend la fenêtre coulissante O(n)

1. ** Scan linéaire** – Chaque personnage entre et quitte la fenêtre une fois.
2. **Constant Extra Space** – Seulement 26 compteurs pour les lettres minuscules.
3. **Explication intuitive** – Gardez la fenêtre aussi longtemps que le caractère *no* frappe `k`.
4. ** Facilement extensible** – Le même motif fonctionne pour au moins k, k ou k.

### 4.3 Les pièges communs que vous devez éviter

Pourquoi ça arrive ?
- Oui.
Oubliez que `(n+1)*n/2` compte *toutes* sous-chaînes. Précalculer le total et soustraire les invalides. Autres
Autres Utiliser une carte au lieu d'un tableau fixe. Utiliser `int[26]` pour les lettres minuscules. Autres
Autres Réduire la fenêtre de manière incorrecte. Alors que `freq[cur] >= k`, décrément gauche et déplacer `left++`. Autres
Pas de réinitialisation de l'index gauche, mais le freq du char enlevé n'est pas mis à jour. Décret le compteur de `s[gauche]` chaque fois que nous tournons à gauche. Autres

### 4.4 Les cas de bord qui vous font transpirer

«k = 1»: Chaque sous-chaîne est valide → la réponse est `(n+1)*n/2`.
- "k > n" : Aucune sous-chaîne ne peut avoir un caractère ≥ k → la réponse est 0.
- Oui. Tous les caractères identiques : La fenêtre se rétrécira agressivement.
- Grande `n`: Assurez-vous d'utiliser `long long` ou `int64_t` pour le nombre total pour éviter le débordement.

#### 4.5 Marche pas à pas (amiable au tableau blanc)

1. **Toutes les sous-chaînes**
Texte
total = (n + 1) * n / 2
«» "
2. **Initialiser la fenêtre**
`l = 0` (à gauche), `freq[26] = 0`
3. **Scan Droite* *
Pour chaque `r` de `0` à `n-1`:
- `freq[s[r]]++`
- Tandis que `freq[s[r]] >= k`:
"freq[s[l]]--", `l++`
- Soustraire les mauvaises sous-chaînes: `total -= (r - l + 1)`
4. **Résultat**
Retour "total".

Cette séquence est parfaite pour une explication de 5 minutes lors d'une entrevue.

#### 4.6 SEO— Mots clés optimisés

- Leetcode 3325
- Compter les sous-chaînes avec les caractères de fréquence K I
- Algorithme de la fenêtre coulissante
- Problème de chaîne Java
- Question d'entrevue de Python
- C++ code d'entrevue
- Conseils d'entretien de l'ingénieur logiciel
- Manipulation de chaînes dans les interviews
- Nombre de chaînes O(n)

Inclure ces phrases dans votre lien En post, CV ou article portfolio permettra aux gestionnaires d'embauche de repérer votre expertise dans exactement les sujets qui les intéressent.

---

- Oui. 5. Dernier départ

> Gardez la fenêtre jusqu'à ce qu'un personnage atteigne `k`, puis glissez à gauche, et soustrayez les mauvaises sous-chaînes.
> C'est la ligne de base du raisonnement qui vous permet de résoudre le Leetcode 3325 dans **O(n)** avec la mémoire **O(1)**, et explique à tout intervieweur que vous pouvez transformer un problème de comptage apparemment lourd en un scan linéaire propre.

Bon codage – et bonne chance pour cette prochaine interview!