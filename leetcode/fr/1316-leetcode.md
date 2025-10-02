---
Titre: LeetCode 1316. Sous-chaînes Echo distinctes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Sous-chaînes Echo distinctes – LeetCode 1316
- Oui. Un guide approfondi du problème, de l'algorithme et des pièges

> **Mots clés** – *Distinct Echo Substrings*, *LeetCode 1316*, *echo substring algorithme*, *rolling hash*, *string manipulation*, *C++ solution*, *Java solution*, *Python solution*, *O(n2) algorithme*, *hashing for strings*, *leetcode interview questions*

---

- Oui. 1. Déclaration de problème (Codeleet 1316)

On vous donne une chaîne **`text`** (seulement lettres minuscules, `1 ≤ text.length ≤ 2000`).
Une sous-chaîne est une sous-chaîne **echo** si elle peut être écrite comme **`XY`** où les deux moitiés sont identiques (`X== Y`).
Par exemple, dans `"abcabc"`, `"abcabc"` est une sous-chaîne d'échos car elle peut être divisée en `"abc"` + `"abc"`.
Votre tâche est de retourner le nombre de sous-chaînes d'échos de **`text`**.

---

- Oui. 2. Ce qui rend ce problème intéressant

C'est bien, c'est mal.
C'est pas vrai.
Autres **Définition simple** – La moitié équivaut à la moitié d'entre eux se sent intuitif. **Contrôler chaque sous-chaîne ("O(n3)") est un cauchemar même pour "n = 2000". Autres
**O(n2) solutions existent** – LeetCode permet jusqu'à 2000 caractères, donc un algorithme quadratique est bien. **TLE pour la comparaison des chaînes naïve** – chaque test d'égalité peut scanner les caractères `O(n)`. Autres
**Technique réutilisable** – l'idée de rolling-hash est un élément de construction pour de nombreux problèmes de cordes. **Choisir la base et le module** – choisir une mauvaise base ou le module peut entraîner de nombreuses collisions ou débordement. **Les solutions Python naïfs peuvent facilement atteindre des limites de temps sur de grandes entrées. Autres

---

- Oui. 3. Idée de base – approche de rolling-hash O(n2)

1. **Hashes pré-calculées** –
`H[i] = (texte[0] * p^(i-1) + texte[1] * p^(i-2) + ... + texte[i-1]) mod M`.
Avec une base `p` (par exemple 91138233) et une grande prime `M` (par exemple 109+7).
Nous pouvons également doubler la masse avec un autre module (`M2`) pour nous protéger contre les collisions.

2. **Vérifier chaque sous-chaîne de longueur uniforme** –
Pour chaque indice de départ `i` et pour chaque demi-longueur `len` (`1 ... (n-i)/2`):
* `hash1 = getHash(i, i+len-1) "
* `hash2 = getHash(i+len, i+2*len-1) "
Si `hash1 == hash2` la sous-chaîne `text[i:i+2*len]` est une sous-chaîne d'écho.

3. **Tenir des sous-chaînes distinctes** –
Conservez la chaîne réelle dans un `HashSet` (Java), `set` (Python) ou `unordered_set` (C++).
L'utilisation d'une paire de hachage (deux valeurs mod) dans l'ensemble est sûre et plus rapide que la construction de la chaîne, mais la chaîne garantit la justesse.

4. **Retourner la taille de l'ensemble**.

> **Pourquoi fonctionne-t-il en O(n2)? * *
> Nous inspectons les paires `O(n2)` `(i, len)` et chaque récupération de hachage est O(1).
> L'insertion finale « substring » ou « hash pair » est amortie par O(1).

---

- Oui. 4. Alternatives et pourquoi elles ne sont pas choisies

L'approche Temps L'espace Commentaires
C'est pas vrai.
Une triple boucle Brute-force ('O(n3)') 8 milliards d'ops pour `n=2000' O(1)' Trop lent
Two‐loop + égalité de chaîne (`O(n3)`) Même que ci-dessus. O(1).
**Rolling hasch + set** ('O(n2)`)
Tableau suffixe + LCP Dépassement pour cette contrainte

---

- Oui. 5. Pièges dans les caisses de bord

* **Contrôles en vol** – un seul hachage mod 64 bits peut théoriquement entrer en collision. Double-hachage réduit la probabilité à négligeable.
* **Très longs motifs répétés** – par exemple « aaaa...a » crée de nombreuses sous-chaînes d'écho; l'utilisation de la mémoire de l'ensemble pourrait croître.
L'utilisation d'une paire de hachage dans l'ensemble maintient la mémoire limitée.
* **Python string slice** – il crée de nouvelles chaînes à chaque fois. Pour 2000 caractères, cela est très bien, mais dans des délais serrés, vous pouvez avoir besoin d'utiliser `hash` ou `int` représentation.

---

- Oui. 6. Les solutions finales

Ci-dessous vous trouverez le code prêt à courir dans **Java, Python et C++**.
Tous les trois utilisent une technique de laminage avec double hachage (sauf Python où le hachage intégré 64 bits est généralement suffisant pour les tests cachés de LeetCode).

> **Conseil**: Si vous soumettez à LeetCode, choisissez la langue avec laquelle vous êtes le plus à l'aise – les différences d'exécution sont négligeables pour ce problème.

---

## Solution Java (Code Leet 1316)

"Java
Importation de java.util.*;

solution de classe publique {
secteur public EchoSubstrings (texte en attente) {
int n = text.length();
// Deux moduli pour le double hachage
longueur finale MOD1 = 1_000_000_007L;
longueur finale MOD2 = 1_000_000_009L;
base longue finale = 91138233L; // base aléatoire

// Préfixe
long[] pref1 = nouveau long[n + 1];
long[] pref2 = nouveau long[n + 1];
long[] pow1 = nouveau long[n + 1];
long[] pow2 = nouveau long[n + 1];
pow1[0] = pow2[0] = 1;
pour (int i = 0; i < n; i++) {
Int c = text.charAt(i) - 'a' + 1; // 1..26
pref1[i + 1] = (pref1[i] * BASE + c) % MOD1;
pref2[i + 1] = (pref2[i] * BASE + c) % MOD2;
pow1[i + 1] = (pow1[i] * BASE) % MOD1;
pow2[i + 1] = (pow2[i] * BASE) % MOD2;
}

// Aide au calcul du hash de la sous-chaîne [l, r] (inclus)
java.util.fonction.BiFunction<entier, entier, long[]> getHash =
(l, r) -> nouveau Long[] {
(pref1[r + 1] - pref1[l] * pow1[r - l + 1] % MOD1 + MOD1) % MOD1,
(pref2[r + 1] - pref2[l] * pow2[r - l + 1] % MOD2 + MOD2) % MOD2
};

Set<String> échos = nouveau HashSet<>();
pour (int i = 0; i < n; i++) {
pour (int len = 1; i + 2 * len <= n; len++) {
Long[] h1 = getHash.apply(i, i + len - 1);
Long[] h2 = getHash.apply(i + len, i + 2 * len - 1);
Si h1[0].egals(h2[0]) && h1[1].egals(h2[1]) {
echoes.add(text.substring(i, i + 2 * len));
}
}
}
retour echoes.size();
}
}
«» "

---

Solution Python

'`python
def distinct EchoSubstrings(texte: str) -> Int:
n = len(texte)
MOD1, MOD2 = 10**9 + 7, 10**9 + 9
BASE = 91138233

# Préfixe hachages
pref1, pref2 = [0] * (n + 1), [0] * (n + 1)
pow1, pow2 = [1] * (n + 1), [1] * (n + 1)
pour i, ch en énumération (texte, 1):
val = ord(ch) - 96 # a->1, b->2 ...
pref1[i] = (pref1[i-1] * BASE + valeur) % MOD1
pref2[i] = (pref2[i-1] * BASE + valeur) % MOD2
pow1[i] = (pow1[i-1] * BASE) % MOD1
pow2[i] = (pow2[i-1] * BASE + valeur) % MOD2

Def get_hash(l: int, r: int):
"""Hash of text[l:r+1], 0-based inclusive."""
h1 = (pref1[r+1] - pref1[l] * pow1[r-l+1]) % MOD1
h2 = (pref2[r+1] - pref2[l] * pow2[r-l+1]) % MOD2
retour (h1, h2)

échos = set()
pour i dans la plage(n):
pour la longueur de portée(1, n-i)//2 + 1):
h1 = get_hash(i, i+longueur-1)
h2 = get_hash(i+longueur, i+2*longueur-1)
si h1 == h2:
echoes.add(texte[i:i+2*longueur])
retour len(echoes)
«» "

> **Pourquoi cela fonctionne sur LeetCode**
> LeetCodeS test harnais utilise des graines aléatoires cachées et une limite de temps de 1 s, mais un hachage de 64 bits avec deux modules est effectivement sans collision pour tous les cas d'essai.

---

C++ Solution

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int distinct EchoSubstrings(texte chaîne) {
int n = text.size();
longue MOD1 = 1'000'000'007LL;
longue MOD2 = 1'000'000'009LL;
longue BASE = 91138233LL;

vecteur <long> pref1(n+1,0), pref2(n+1,0);
vecteur <long> pow1(n+1,1), pow2(n+1,1);

pour (int i=0;i<n;i++){
int val = texte[i]-'a'+1; // 1..26
pref1[i+1] = (pref1[i]*BASE + val)%MOD1;
pref2[i+1] = (pref2[i]*BASE + val)%MOD2;
pow1[i+1] = (pow1[i]*BASE)%MOD1;
pow2[i+1] = (pow2[i]*BASE)%MOD2;
}

getHash = [&](int l,int r)->array<long long,2>{
long h1 = (pref1[r+1] - pref1[l]*pow1[r-l+1])%MOD1;
si(h1<0) h1+=MOD1;
long h2 = (pref2[r+1] - pref2[l]*pow2[r-l+1])%MOD2;
si(h2<0) h2+=MOD2;
retour {h1,h2};
};

_set non ordonné<string> les échos;
pour (int i=0;i<n;i++){
pour (int len=1; i+2*len<=n; ++len){
auto h1 = getHash(i,i+len-1);
auto h2 = getHash(i+len,i+2*len-1);
si (h1==h2)
echoes.insert(text.substr(i,2*len));
}
}
retour echoes.size();
}
};
«» "

---

- Oui. 7. Mots définitifs

*La moitié équivaut à la moitié de la définition est faussement simple, mais une approche de rolling-hash quadratique transforme le problème en une routine propre et efficace. *
N'hésitez pas à copier l'une des trois solutions ci-dessus, à modifier la base ou le module si vous rencontrez une case d'angle, et vous aurez une réponse rapide et sans bug à **LeetCode 1316** – et vous aurez également appris un modèle qui vous aidera à résoudre de nombreuses autres questions d'entrevue de manipulation de cordes. Bon codage !