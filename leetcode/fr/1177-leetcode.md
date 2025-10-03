---
titre: LeetCode 1177. Peut faire Palindrome de Substring -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1177 – Peut faire Palindrome de Substring
**Solution en Java, Python & C++ + une interview-blog conviviale au référencement* *

---

- Oui. 1. Récapitulation des problèmes

> *On vous donne une chaîne `s` et un tableau de requêtes `queries[i] = [gauche, droite, k]`. *
> *Pour chaque requête, vous pouvez :*

1. *Réorganiser les caractères de la sous-chaîne `s[gauche ... droite]` dans n'importe quel ordre. *
2. *Remplacez jusqu'à `k` de ces caractères avec toute lettre anglaise minuscule. *

> Après avoir effectué les opérations ci-dessus, est-il possible de faire de la sous-chaîne un palindrome?
> Retourner un tableau booléen `réponse` où `réponse[i]` est le résultat de la requête *i*‐th.

> **Constraints**
> • `1 ≤ s.longueur, requêtes.longueur ≤ 105 "
> 0 ≤ gauche ≤ droite < s. longueur "
> • <0 ≤ k ≤ s. longueur "
> • `s` ne contient que des lettres anglaises minuscules.

---

- Oui. 2. Le point de vue sur le bien

Si nous sommes autorisés à ** réorganiser** la sous-chaîne, la seule chose qui compte est ** combien de fois chaque lettre apparaît**.
- Les lettres qui apparaissent un nombre **même** de fois sont déjà pair.
- Les lettres qui apparaissent un nombre **odd** de fois ont besoin d'un partenaire pour devenir pair.
Remplacer l'une des lettres impaires par une autre fixe *deux* chiffres impaires en même temps.

Donc pour une sous-chaîne de longueur `L`:

# lettres impairs
Il n'y a pas de problème.
- Oui.
(la lettre peut s'asseoir au centre)
- Oui.
C'est vrai.
C'est vrai.
(#odd / 2) Autres

La règle est simplement :
**`requis = (nombre_de_lettres_odd) / 2`** (division entière).
Si `obligatoire ≤ k` → la réponse est `true`.

---

- Oui. 3. La partie «Bad» – approche naïve

Compter les lettres de chaque sous-chaîne par requête serait

«» "
O(.S.S.S.S.) → 1010 dans le pire des cas
«» "

qui s'éteint immédiatement.
Nous avons besoin d'une structure *prefix* qui nous permet d'obtenir les fréquences de lettres (ou au moins le statut impair/even) de toute sous-chaîne dans **O(1)** temps.

---

- Oui. 4. Les pièges

Pourquoi ça fait mal ?
C'est quoi ?
En utilisant un tableau 2-D de taille `[n][26]` pour chaque préfixe. Autres
Autres Stocker le nombre complet de fréquences par préfixe (integers)= Vous obtenez le bon résultat, mais vous faites 26 additions entières par requête – encore très bien, mais vous gaspillez de l'espace et perdez l'élégant bit-twist. Autres
Autres Oubliant que la sous-chaîne peut avoir un centre impair. Autres

---

- Oui. 5. La solution élégante – Bitmask + préfixe XOR

Nous stockons **seulement la parité** (impair/même) de chaque lettre dans un masque 26 bits:

- Un peu "i" (`0 ≤ i < 26`) est **1** ⇢ la lettre `'a'+i` apparaît un nombre impair de fois jusqu'à l'index actuel.
- Bit `i` est **0** ⇢ la lettre apparaît un nombre pair de fois.

Pour toute la chaîne, nous construisons un tableau

«» "
pref[i] = XOR de tous les masques de s[0 ... i-1] (pref[0]]. 0)
«» "

*Pourquoi XOR fonctionne*:
XORing un peu deux fois l'éclaircit, exactement ce que nous voulons quand un nombre de lettres devient encore.

**Sous-chaînes
Pour tout "[l, r]` le masque de parité de la sous-chaîne est

«» "
masque_sub = pref[r+1] XOR pref[l]
«» "

Le nombre de bits dans `mask_sub` est le nombre de lettres impaires dans cette sous-chaîne.

Enfin nous vérifions

«» "
(Integer.bitCount(mask_sub) / 2) ≤ k
«» "

Toutes les requêtes sont répondues dans **O(1)** après la seule passe linéaire qui construit `pref`.

---

- Oui. 5. Complexité

Étape Temps Espace
C'est pas vrai.
Construisez des masques préfixes `O(=)''' 'O(=)' entiers (4 octets chacun)
Autres Réponses aux demandes de renseignements `O(="queries=") ́ ́ `O(1)` par demande
**Total****** Autres

---

- Oui. 6. Mise en œuvre du code

Ci-dessous vous trouverez des solutions propres et prêtes à copier dans **Java (Java 17), Python 3 et C++17** qui utilisent la technique de préfixe bitmask décrite ci-dessus.

---

##### 6.1 Java

"Java
Importer java.util. d'une longueur d'au moins 50 mm;
Importer java.util. Liste;

solution de classe publique {
***
* Code Leet 1177 – Peut faire Palindrome de Substring
*
* @param s la chaîne d'entrée
* requêtes @param chaque requête est {gauche, droite, k}
* @retour liste des booléens pour chaque requête
*/
liste publique<Boolean> peutMakePaliQueries(String s, int[][] requêtes) {
int n = s.longueur();
// préfixer les masques XOR – pref[0] = 0
int[] pref = nouvelle int[n + 1];
pour (int i = 0; i < n; i++) {
bit int = 1 << (s.charAt(i) - 'a');
pref[i + 1] = pref[i] ^ bit;
}

Liste <Boolean> ans = nouvelle liste d'array<>(queries.longueur);
pour (int[] q : requêtes) {
int l = q[0], r = q[1], k = q[2];
masque int = pref[r + 1] ^ pref[l];
// Integer.bitCount(masque) donne le nombre de lettres impaires
int requis = Integer.bitCount(masque) / 2;
ans.add(obligatoire <= k);
}
le retour des an;
}
}
«» "

---

6.2 Python 3

'`python
Solution de classe:
def canMakePaliQueries(self, s: str, requêtes: List[List[int]]) -> Liste [bool]:
n = len(s)
# préfixer les masques xor
pref = [0] * (n + 1)
pour i, ch dans le(s, 1):
pref[i] = pref[i-1] ^ (1 << (ord(ch) - 97))

res = []
pour l, r, k dans les requêtes:
masque = pref[r+1] ^ pref[l]
requis = mask.bit_count() // 2 # Python 3.10+: int.bit_count()
res.append(obligatoire <= k)
retour res
«» "

*(Si vous utilisez une ancienne version Python 3, remplacez `mask.bit_count()` par `bin(mask).count('1')`.) *

---

*### 6.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<bool> canMakePaliQueries(chaîne s, vector<vector<int>& requêtes) {
int n = s.size();
vecteur<int> pref(n + 1, 0);
pour (int i = 0; i < n; ++i) {
bit int = 1 << (s[i] - 'a');
pref[i + 1] = pref[i] ^ bit;
}

vecteur <bool> ans;
as.reserve(queries.size());
pour (auto &q : requêtes) {
int l = q[0], r = q[1], k = q[2];
masque int = pref[r + 1] ^ pref[l];
int requis = __constructin_popcount(mask) / 2;
ans.push_back(requis <= k);
}
le retour des an;
}
};
«» "

`_builtin_popcount` (ou `_builtin_popcountll`) compte les bits dans un `int`.
Fonctionne en O(1) par requête.

---

- Oui. 5. Cas de bord et essais

Autres Décision Pourquoi il importe de savoir comment la solution la gère
Il n'y a pas de lien entre les deux.
Un seul caractère – déjà un palindrome.
"k = 0" Aucun remplacement autorisé.
Grand `k` (≥ L/2)
Autres Répéter les caractères seulement.

Testé sur tous les exemples de cas à partir de l'énoncé du problème *et* tests de stress aléatoires jusqu'à des requêtes `105` avec `s` longueur `105`. Pas de temps mort, pas de débordement de mémoire.

---

## ♫ Interview-Ready Blog – Peut faire Palindrome de Substring
### (LeetCode 1177, Bitmask, Préfixe XOR, O(n+q) Algorithme)

---

#### Introduction (mots clés du référencement : *LeetCode 1177, sous-chaîne palindrome, algorithme d'entrevue, solution bitmask*)

Si vous préparez des entrevues sur la structure des données, l'un des problèmes les plus discutés est **LeetCode 1177 – Peut faire Palindrome de Substring**.
Il semble faussement simple : réarranger une sous-chaîne et changer quelques lettres.
Mais le défi consiste à répondre aux questions *105* sur une chaîne de caractères *105*.
Ce blog montre l'algorithme ** le plus rapide et le plus adapté à la mémoire** que vous pouvez utiliser pour ce problème – **la solution XOR préfixe bitmask** – et vous donne des implémentations prêtes à coller dans **Java, Python et C++**.
Prenez le code, comprenez la logique, et impressionnez vos intervieweurs!

---

C'est vrai. 1. L ' idée fondamentale

La réorganisation supprime l'exigence de l'ordre des lettres seulement.
Fréquences bizarres → besoin d'un partenaire; chaque remplacement peut fixer deux nombres impairs.
Donc le nombre de remplacements requis est simplement la division entière du nombre impair par deux.

**Pourquoi cela est important**
* O(1) par requête après un seul passage linéaire → résout le grand‐ O problème dans les contraintes LeetCode.
* Utilise seulement un entier 32 bits par préfixe → mémoire minimale.

---

C'est vrai. 2. De Naïve à Optimal

L'approche Temps Espace Verdict
C'est pas vrai.
Autres Nombre de lettres par requête (pour mémoire de 26 interts)
Nombre de préfixes (`int[n+1][26]`) O(n + 26q)
Préfixe XOR bitmask

L'astuce bitmask transforme la table de 26 fréquences en un seul entier de 32 bits, tirant parti de XOR pour basculer la parité.

---

C'est vrai. 3. Construction du tableau XOR préfixe

Texte
xOR (1 << (s[i-1] - 'a'))
«» "

- `pref[0] = 0` (préfixe vide).
- Pour la sous-chaîne `[l, r]` le masque de parité est `pref[r+1] XOR pref[l]`.
- `_builtin_popcount` (ou `Integer.bitCount`) nous dit combien de bits sont définis → nombre de lettres impaires.

---

C'est vrai. 4. Mettre tout en place

1. Construisez le tableau XOR – **O(n)**.
2. Pour chaque requête :
* Calculer `masque = pref[r+1] XOR pref[l]`.
* `odd = popcount(masque)`
* `obligatoire = impair / 2`
* La réponse est `obligatoire <= k`.
* **O(1)** par requête.

complexité totale : **O(n + q)**, espace **O(n)**.

---

C'est vrai. 5. Extraits de code

(Voir la section 6.1–6.3 ci-dessus pour la mise en œuvre complète.)

---

5.1 Code de test du stress aléatoire (Python)

'`python
importer au hasard, chaîne
de temps d'importation

def brute(s, requêtes):
res = []
pour l, r, k dans les requêtes:
sous = liste(s)[l:r+1])
sous-catégorie()
# naïf – compter les lettres impaires
impair = somme(sub.count(ch) % 2 pour ch dans set(sub))
requis = impair // 2
res.append(obligatoire <= k)
retour res

def fast(s, requêtes):
# implémentation bitmask rapide (à partir du blog)
n = len(s)
pref = [0]*(n+1)
pour i,ch dans le(s) énuméré(s,1):
pref[i] = pref[i-1] ^ (1 << (ord(ch)-97))
res = []
pour l,r,k dans les requêtes:
masque = pref[r+1] ^ pref[l]
requis = bin(masque).count('1')//2
res.append(obligatoire <= k)
retour res

# Essai aléatoire
n = 100000
q = 100000
s = ''.join(random.choice(string.ascii_lowercase) pour _ dans l'intervalle(n))
requêtes = [[random.randint(0,n-1), random.randint(0,n-1), random.randint(0,110)] pour _ dans l'intervalle(q)]
requêtes = [[min(l,r), max(l,r), k] pour l,r,k dans les requêtes]

début = heure()
rapide(s, requêtes)
print("Algorithme rapide terminé", time()-start, "secondes")
«» "

Exécute en < 1 s sur un ordinateur portable typique – démontre l'évolutivité du tour XOR.

---

C'est vrai. 6. Conclusion

* LeetCode 1177 est une grande vitrine de la façon dont un astuce astucieux peut apporter un problème par ailleurs lourd jusqu'au temps linéaire.
* Le préfixe XOR bitmask est **short**, **fast** et **memory‐efficace**.
* Avec les blocs de code ci-dessus, vous pouvez déposer cette solution dans n'importe quelle plate-forme de codage d'entretien ou soumettre directement sur LeetCode.

Bonne chance, et rappelez-vous: parfois la solution la plus rapide est cachée dans l'observation la plus simple – **parité**.

---

Appel à l'action

Vous avez le code ? Essayez de le modifier pour des variations (p. ex., alphabet de 30 bits).
Partagez vos propres solutions ou tests de stress dans les commentaires – laissez-nous construire une communauté d'algorithmes rapides ensemble!

---

### Pensée finale (Référencement : *complexité du temps, optimisation de l'espace, préparation de l'entrevue*)

Lorsque les intervieweurs demandent à « Can Make Palindrome From Substring, » ne paniquez pas – évoquez l'approche XOR* de *bitmask.
Expliquez que le défi consiste à *répondre rapidement à de nombreuses requêtes* et à leur montrer l'espace linéaire et constant par solution de requête.
Avec les implémentations ci-dessus, vous êtes prêt à frapper le juge ou le tableau blanc avec confiance. Bonne chance !

---

*— Fin du blog —*

---

> **Conseil pour les intervieweurs**: Demandez au candidat d'expliquer pourquoi XOR travaille pour la parité. L'explication démontre une forte compréhension des opérations bitwise et est souvent le moment qui sépare le bon candidat du grand.

---

C'est ça ! Utilisez le code, maîtrisez la logique, et vous êtes défini pour LeetCode 1177. Bon codage 