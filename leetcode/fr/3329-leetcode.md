---
titre: LeetCode 3329. Sous-chaînes de comptage avec caractères de fréquence K II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Aperçu de la solution – Sous-chaînes de comptage avec caractères de fréquence K II**

Langue Heure Espace
- C'est quoi ?
**O(n)**
Python **O(n)**
**O(26)**

*`n = s.longueur()` – jusqu'à 3 × 105*

L'idée clé est une fenêtre coulissante à deux points**.
Pendant que la fenêtre `[l ... r]` contient **au moins un caractère qui apparaît ≥ k fois**, chaque fenêtre plus longue qui commence à `l` et se termine à n'importe quel index `>= r` est également valide.
Ainsi, lorsque la fenêtre devient valide, nous pouvons ajouter `n – r` à la réponse, puis réduire la fenêtre de gauche jusqu'à ce qu'elle ne soit plus valide.

Voici des implémentations propres et prêtes à la production en Java, Python et C++.

---

## Java

"Java
Importation de java.util.*;

solution de classe publique {
// helper: la fenêtre contient-elle un char avec count >= k?
booléen statique privé aKFrequence(int[] freq, int k) {
pour (int c : freq) {
si (c >= k) retourne true;
}
retourner faux;
}

grand nombre DeSous-chaînes(String s, int k) {
int n = s.longueur();
long ans = 0;
int[] freq = nouveau int[26];

Int l = 0;
pour (int r = 0; r < n; r++) {
freq[s.charAt(r) - 'a']++;

// rétrécir à partir de la gauche pendant que la fenêtre est valide
pendant que (hasKFrequecy(freq, k)) {
ans += n - r; // toutes les fenêtres [l, r..n-1] sont valides
[s.charAt(l) - 'a']--;
l++;
}
}
le retour des an;
}

public statique vide principal(String[] args) {
System.out.println(nouvelle solution().numberOfSubstrings("abacb", 2)); // 4
System.out.println(nouvelle solution().numberOfSubstrings("abcde", 1)); // 15
}
}
«» "

---

Python

'`python
Solution de classe:
Numéro DeSous-chaînes(self, s: str, k: int) -> Int:
n = len(s)
freq = [0] * 26
l = 0
ans = 0

def valid() -> bool:
retourner n'importe quel(c >= k pour c en freq)

pour r, ch dans le ou les énuméré(s):
freq[ord(ch) - 97] += 1

en cours de validité():
ans += n - r # toutes les fenêtres plus longues commençant à l
[ord(s[l]) - 97] -= 1
l += 1

retour et


# tests rapides
si __nom__ == "__main__" :
print(Solution().numberOfSubstrings("abacb", 2)) # 4
print(Solution().numberOfSubstrings("abcde", 1)) # 15
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long nombre DeSous-chaînes(chaîne s, int k) {
int n = s.size();
vecteur <int> freq(26, 0);
long an = 0;
Int l = 0;

auto valide = [&]() -> bool {
pour (int c : freq) si (c >= k) retourner vrai;
retourner faux;
};

pour (int r = 0; r < n; ++r) {
[s[r] - 'a']++;

pendant la période (valable()) {
ans += n - r; // toutes les fenêtres plus longues sont valides
[s[l] - 'a']--;
++l;
}
}
le retour des an;
}
};

Int main() {
Solution sol;
Cout << sol.numberOfSubstrings("abacb", 2) << '\n'; // 4
Cout << sol.numberOfSubstrings("abcde", 1) << '\n'; // 15
}
«» "

---

## Article du blog – *Le bon, le mauvais, le mauvais de LeetCode 3329*

Pourquoi LeetCode 3329 compte dans les entrevues techniques

- **Mot-clef-Rich**: Sous-chaînes de nombres avec caractères K-Fréquence II, Code Leet Hard, fenêtre coulissante, Code Java Python C++.
- **Recruteur-Amis**: Démontre la maîtrise de la technique à deux points, de la complexité linéaire et de la manipulation de grandes entrées.
- **Career Boost** : Une solution concise et bien commentée est un bon point de conversation dans une entrevue comportementale.

---

### Le bon – Ce qui fait de ce problème une victoire

Aspect Pourquoi il est grand
-- -- -- -- -- --
**Temps linéaire**="O(n)` est le meilleur que vous pouvez faire; satisfait la contrainte 3 × 105. Autres
**Simple Structure de données**= 26 éléments (`int[26]`), aucune carte de hachage → espace constant. Autres
**Two-Pointer Intuition** Autres
**Évoluable vers plusieurs langues**L'implémentation est presque identique en Java, Python, C++ – parfait pour les portfolios multilingues. Autres

**Takeaway**: Le problème renforce un concept CS de base – maintenir une fenêtre *valide* et compter toutes les extensions en un seul coup.

---

### Les mauvaises – Pièges communs que vous devriez éviter

1. **L'utilisation d'une HashMap**
*Problème*: `O(n log ε)` par opération, et frais généraux supplémentaires.
*Fix* : Utilisez un tableau de taille fixe pour les 26 lettres minuscules.

2. **Oublier longtemps* *
*Problème*: Le nombre de sous-chaînes peut atteindre ~ (3 × 105)2 / 2 ↓ 4.5 × 1010, débordement d'ints 32 bits.
*Fix*: En Java `long`, en C++ `long`, en Python `int` (non consolidé).

3. **Incorrecte Valable— Vérification**
*Problème*: Vérifier seulement le caractère qui vient d'entrer conduit à des fenêtres manquées lorsque d'autres caractères satisfont à l'état `k`.
*Fix* : Réévaluer la fenêtre après chaque rétrécissement : numériser les 26 fréquences.

4. ** Erreurs hors‐un pour compter* *
*Problème*: Ajouter `n - r` est l'astuce clé; ajouter `n - r + 1` sur-comptes par un.
*Fix*: Rappelez-vous que `r` est basé sur zéro et inclusive.

---

### Les horribles – Les cas de bord qui peuvent vous faire trébucher

Pourquoi il brise des solutions naïves Comment le manipuler
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
- Oui. Chaque sous-chaîne est valide ; la fenêtre ne devient jamais invalide, causant une boucle infinie si vous rétrécissez incorrectement. L'algorithme compte naturellement `n - r` pour chaque `r`; aucun cas particulier n'est nécessaire. Autres
Longues répétitions ('aaaaaa...') Les décalages fréquents peuvent sembler coûteux, mais le tableau freq de taille constante le maintient rapidement. Assurez-vous que votre boucle de rétractation utilise correctement la mise à jour `l` et `r`. Autres
Quelques modèles vérifient `si (!s.length()) retourne 0;`. 1'; sûr de sauter. Autres

---

Liste de contrôle finale Avant l'entrevue

1. **Lisez les Contraintes** – utilisez `long` / `long' pour la réponse.
2. **Utilisez un tableau pour les fréquences** – 26 éléments, `freq[s[i]-'a']`.
3. **Valider la fenêtre** – `any(freq[c] >= k pour c in freq)».
4. **Ajouter `n - r` Quand Valide** – compte toutes les sous-chaînes plus longues à la fois.
5. **Retirer de la gauche** – diminuer la fréquence, déplacer `l`.
6. **Test Edge Cases** – `k=1`, `k=n`, tous les mêmes caractères, chaîne aléatoire.

---

### #= OBJECTIF SEO–Takeaway optimisé

> *"Solve LeetCode 3329 – Sous-chaînes de comptage avec caractères de fréquence K II – avec une fenêtre coulissante en Java, Python ou C++. Apprenez à gérer les grandes chaînes, à utiliser des tableaux de fréquences à espace constant et à éviter les pièges communs. Maîtrisez ce dur problème pour impressionner les recruteurs et augmenter votre score d'entrevue." *

Partagez cet article, ajoutez les extraits de code à votre GitHub, et vous aurez une vitrine solide LeetCode qui met en évidence:

- ** Compétences en résolution de problèmes** (algorithme de niveau dur).
- ** Compétence en langage brut** (Java/Python/C++).
- **Préparation à l'entretien** (fenêtre coulissante, optimisation du temps/de l'espace).

Bonne chance à l'atterrissage ce rôle de technologie de rêve!