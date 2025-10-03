---
titre: LeetCode 1960. Produit maximum de la longueur de deux sous-chaînes palindromiques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème – 1960. Produit maximal de la longueur de deux sous-chaînes palindromiques

> **Donné** d'une chaîne `s` (2 ≤ ≤ ≤ 105), trouver **deux sous-chaînes palindromiques de longueurs impaires dont le produit est maximal.
> Retourne ce produit maximum.

Exemple Entrée Sortie Explication
C'est pas vrai.
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" (3) → 3 × 3 = 9
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" (3) → 3 × 3 = 9

**Pourquoi est-ce difficile? **
- Oui. Nous devons vérifier *chaque* palindrome de longueur étrange.
- Oui. La chaîne peut être longue de 100 000 caractères, donc une approche O(n2) est impossible.
- Oui. Les deux sous-chaînes ne doivent pas se chevaucher, ce qui signifie que nous devons combiner les informations des deux côtés de la chaîne.

La clé est d'utiliser l'algorithme **Manachers** pour obtenir tous les palindromes de longueur bizarre dans le temps linéaire, puis combiner préfixe‐ et suffixe‐maximums.

---

- Oui. 2. Aperçu de l'algorithme

1. ** Calculer le plus long palindrome impair à chaque centre* *
`odd[i]` = longueur maximale impair d'un palindrome centré sur l'index `i` (Manacher).
(La longueur est garantie pour être étrange.)

2. **Préfixe de construction tableau maximum**
`pref[i]` = longueur de palindrome la plus longue dans `s[0...i]`.
Récurrence: `pref[i] = max(pref[i-1], impair[i])`.

3. **Suffixe de construction tableau maximum**
`suff[i]` = longueur de palindrome la plus longue dans `s[i...n-1]`.
Récurrence: `suff[i] = max(suff[i+1], impair[i])`.

4. **Split la chaîne une fois**
Pour chaque position fractionnée «i» (0 ≤ i < n‐1), le premier palindrome doit se terminer à «i» ou avant, le second doit commencer à «i+1» ou après.
Le meilleur produit pour cette fraction est "pref[i] * suff[i+1]".

5. **Prendre le maximum sur toutes les scissions**.

**Complexités* *

- Temps : **O(n)** – un passage pour Manacher, deux passages linéaires pour préfixe/suffixe, un passage linéaire pour la fraction.
- Mémoire : **O(n)** – tableaux «odd», «pref», «suff».

---

- Oui. 3. Code

Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous les trois résolvent le problème dans le même espace O(n) et O(n).

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
Int public maxProduct(String s) {
int n = s.longueur();
int[] impair = manacherOdd(s);
int[] pref = nouvelle int[n];
int[] suff = nouvelle int[n];

// préfixe max
pref[0] = impair[0];
pour (int i = 1; i < n; i++) {
pref[i] = Math.max(pref[i - 1], impair[i]);
}

// suffixe max
suff[n - 1] = impair[n - 1];
pour (int i = n - 2; i >= 0; i--) {
suff[i] = Math.max(suff[i + 1], impair[i]);
}

int best = 0;
pour (int i = 0; i < n - 1; i++) {
best = Math.max(best, pref[i] * suff[i + 1]);
}
le meilleur retour;
}

/** Manacher pour palindromes impairs seulement */
Int privé[] manucure Difficile(String s) {
int n = s.longueur();
int[] d = nouvelle int[n]; // d[i] = rayon max (demi-longueur)
centre int = 0, droite = 0;
pour (int i = 0; i < n; i++) {
int k = (i < droite) ? Math.min(d[center + droite - i], droite - i) : 1;
pendant que (i - k >= 0 && i + k < n & s.charAt(i - k) == s.charAt(i + k)) {
k++;
}
d[i] = k;
si (i + k > droite) {
centre = i;
droite = i + k;
}
}
int[] impairLen = nouveau int[n];
pour (int i = 0; i < n; i++) {
impairLen[i] = d[i] * 2 - 1; // convertir le rayon en longueur
}
retour impairLen;
}

// Pour des tests rapides
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.maxProduit("abbb")); // 9
Système.out.println(sol.maxProduit("zaaaxbbby"); // 9
}
}
«» "

**Points clés* *

- "mancher" Odd` retourne directement les longueurs du palindrome.
- Les tableaux de préfixe/suffixe stockent la longueur maximale jusqu'à présent / de la fin.
- Oui. La boucle finale considère chaque fraction une fois.

---

3.2 Python

'`python
Solution de classe:
def maxProduct(self, s: str) -> Int:
n = len(s)

Manacher pour les étranges palindromes
d = [0] * n # rayon
centre = droite = 0
pour i dans la plage(n):
k = 1 si i >= droite autre min(d[center + droite - i], droite - i)
pendant que i - k >= 0 et i + k < n et s[i - k] == [i + k]:
k += 1
d[i] = k
i + k > à droite :
centre, à droite = i, i + k

impair = [2 * r - 1 pour r en d] # longueur impair à chaque centre

# ----- préfixe et suffixe maximums -----
pref = [0] * n
suff = [0] * n
pref[0] = impair[0]
pour i dans la plage (1, n):
pref[i] = max(pref[i - 1], impair[i])

suff[n - 1] = impair[n - 1]
pour i dans la plage (n - 2, -1, -1):
suff[i] = max(suff[i + 1], impair[i])

# ----- combiner sur les fractions -----
meilleur = 0
pour i dans la plage (n - 1):
best = max(best, pref[i] * suffi[i + 1])

le meilleur retour


♪ harnais d'essai simple
si __nom__ == "__main__" :
sol = Solution()
print(sol.maxProduit("ababbb") # 9
print(sol.maxProduit("zaaaxbbby") # 9
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maxProduit(chaîne s) {
int n = s.size();
vector<int> impair = manacherOdd(s);
vecteur <int> pref(n), suff(n);

pref[0] = impair[0];
pour (int i = 1; i < n; ++i)
pref[i] = max(pref[i-1], impair[i]);

suff[n-1] = impair[n-1];
pour (int i = n-2; i >= 0; --i)
suff[i] = max(suff[i+1], impair[i]);

int best = 0;
pour (int i = 0; i < n-1; ++i)
best = max(best, pref[i] * suff[i+1]);

le meilleur retour;
}

particulier:
vector<int> manacherOdd(const string &s) {
int n = s.size();
vecteur <int> d(n, 1); // rayon
centre int = 0, droite = 0;
pour (int i = 0; i < n; ++i) {
int k = (i < droite) ? min(d[centre + droite - i], droite - i) : 1;
pendant que (i - k >= 0 && i + k < n && s[i-k] == s[i+k]) ++k;
d[i] = k;
si (i + k > droite) {
centre = i;
droite = i + k;
}
}
vecteur<int> impairLen(n);
pour (int i = 0; i < n; ++i)
impairLen[i] = d[i]*2 - 1; // longueur, non rayon
retour impairLen;
}
};

// Essai
Int main() {
Solution sol;
produit("abbb") << endl; // 9
cout << sol.maxProduit("zaaaxbbby") << endl; // 9
}
«» "

---

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais de Leetcode 1960

> **Titre** : *Le bon, le mauvais et le mauvais de Leetcode 1960 – Maîtriser le produit maximum de deux sous-chaînes palindromiques*
> **Description détaillée**: Découvrez comment résoudre le Leetcode 1960 en Java, Python et C++ avec une solution O(n). Comprendre les pièges, les compromis et l'approche conviviale de l'entrevue en utilisant l'algorithme Manacher.

---

4.1 Pourquoi ce problème est important

Les intervieweurs aiment les problèmes qui vous forcent à penser à **sous-structures optimales** et **temps linéaire**.
Leetcode 1960 est un mélange parfait:

- Oui. Il demande deux sous-chaînes palindromiques *non-overlaping*.
- La contrainte ≤ 105 garantit que vous ne pouvez pas vous permettre des contrôles quadratiques.
- Oui. La réponse repose sur les longueurs maximales du palindrome* de chaque côté d'une scission, et non sur les sous-chaînes réelles.

Craquer ce problème montre que vous pouvez:

- Utilisez l'algorithme *Manachers* pour calculer les rayons du palindrome en O(n).
- Fusionner les résultats en un seul passage.
- Poignez les conditions de limite.

---

4.2 Les bons

Aspect Ce que nous apprenons
C'est quoi, ça ?
**Temps linéaire**=Vous impressionnerez les intervieweurs avec une solution O(n) où les approches les plus naïves sont O(n2). Autres
Un algorithme lu une fois qui peut être réutilisé pour de nombreux problèmes de palindrome. Autres
**Prefix-suffix DP**= Technique classique pour combiner deux moitiés de chaîne. Autres
Les trois implémentations sont succinctes et faciles à lire – un plus pour la révision de code. Autres
**Les solutions Java, Python, C++ sont toutes disponibles, montrant votre polyvalence. Autres

---

Les mauvais

Comment l'éviter
C'est-à-dire
**Mixage du rayon et de la longueur**= Rappelez-vous toujours que le "d[i]" de Manacher est un "radius*; la longueur impair est "2*d[i] - 1'.
**Index off-by-one sur les scissions** Les scissions doivent être entre `i` et `i+1`. Une erreur courante est d'inclure des caractères qui se chevauchent. Autres
**Négligence d'exigences de longueurs impaires**** Si vous utilisez un algorithme de palindrome complet (y compris des longueurs paires), vous devez filtrer ou ignorer des longueurs égales. Autres
**Utiliser longtemps où l'int est suffisant**=Le produit de deux longueurs ≤ 105 chacune s'adapte à l'int signé 32 bits. Évitez les conversions 64 bits inutiles à moins que l'entrevue ne demande explicitement. Autres

---

#### 4.4 La moche

Autres Comportement laid
C'est quoi, ça ?
**O(n2) force brute**=L'essai de chaque paire de centres et d'expansion est tentant mais conduit à TLE sur 105 cordes. Autres
**Deuxième dimension Quelques solutions construisent par erreur une table `n x n` d'existence palindrome, faisant exploser la mémoire. Autres
**Le hachage complexe**Le hachage roulant peut détecter les palindromes en O(1) après le prétraitement O(n), mais les constantes sont énormes et le code est fragile. Autres
**Over-engineering the scinde**=Les gens essayent de trier les palindromes par la longueur, puis cupidement en choisir deux, ce qui échoue lorsque les palindromes se chevauchent de manière complexe. Autres

---

4.5 Comment faire tourner l'entrevue

1. **Exposer les contraintes** – Souligner le besoin de temps linéaire.
2. **Décrivez Manacher en mots** – Il garde une fenêtre palindrome et miroirs du côté gauche pour deviner les rayons. (en milliers de dollars)
3. **Afficher l'astuce préfixe-suffixe** – Nous avons seulement besoin du meilleur palindrome qui se termine avant une scission et le meilleur qui commence après. (en milliers de dollars)
4. **Cas de bord des discussions** – Et si aucun palindrome n'existe d'un côté ? La réponse est 0, qui est traitée automatiquement.
5. **Offre le code** – Fournir les extraits Java/Python/C++.
6. **Réponse aux questions de suivi** – Qu'en est-il si des longueurs égales étaient permises? (en milliers de dollars)

---

### 4.6 Mots clés du référencement (pour la chasse au travail)

- Leetcode 1960
- Produit maximal de deux sous-chaînes palindromiques
- Solution Java Leetcode 1960
- Solution Python Leetcode 1960
- Solution C++ Leetcode 1960
- Entretien avec l'algorithme Manacher
- Algorithme de sous-chaîne Palindrome
- Problème de palindrome linéaire
- Problèmes d'entretien de l'ingénieur logiciel
- Questions d'entrevue de codage

---

4.7 A emporter

> **Maîtrise du Leetcode 1960** est plus qu'un simple test de manipulation de cordes – c'est une vitrine de pensée algorithmique, d'élégance de code et de communication d'interview.
> En combinant la détection du palindrome linéaire de Manacher avec une fusion préfixe/suffixe simple, vous obtenez une solution propre et optimale qui impressionnera tout gestionnaire d'embauche.

Bon codage, et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit