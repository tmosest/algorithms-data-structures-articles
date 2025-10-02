---
titre: LeetCode 2301. Sous-chaîne de correspondance après remplacement -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Leetcode 2024 – *Remplacement du lot**
**Les bons, les mauvais, les méchants**
*Pourquoi une simple force brute fonctionne, pourquoi KMP échoue, et un coup d'œil au hack FFT. *

---

- Oui. 1. Récapitulation des problèmes

Titre Lien
- Oui.
2024 **Remplacement des lots** Autres

> **Définition**
> Trois chaînes vous sont données : `s`, `sub` et une liste de `mappings` (chaque carte est une paire `old → new`).
> Vous pouvez **remplacer chaque caractère de `sous` au plus une fois** avec n'importe quel `nouveau` qu'il map à (y compris lui-même).
> Après tous les remplacements facultatifs, le "sous" doit apparaître comme un substring contigu de "s".
> Retourner `true` si une telle correspondance existe, sinon `faux`.

**Exemples**

S. S. S. S. S. S. S.
C'est pas vrai.
`aaaa`" `['a','b'] ]`"true` (replacer les deux `a`" avec `b` → `bb`, `bb` se produit à l'index 1 )
`abac`abac`aba`aba `[ ['a','b'] ]`abac`abac `abac`aba`aba`aba`aba`aa,'b'aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aba`aa,'b'aba`aaa,'b'aaa,'b'aba`aaa,'b'aaa'aaaa,'b'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa ne peut pas être remplacé pour correspondre à la `a` dans `s`) Autres

**Contrôles* *

* `1 ≤ longueur inférieure ≤ longueur inférieure ≤ longueur inférieure ≤ 104 "
* `0 ≤ mappages longueur ≤ 105 "
* Tous les caractères sont imprimables ASCII (`0–9`, `A–Z`, `a–z`)

---

- Oui. 2. Pourquoi la Force Brute est acceptée

- Oui. L'alphabet est minuscule (62 caractères imprimables).
- Oui. Nous pouvons construire une matrice 62×62 booléenne `canReplace[old][new]` dans le temps `O(mappings)`.
- Une fois que nous avons cette matrice, en vérifiant une fenêtre `[i, i+=2-]' dans `s` est seulement un balayage linéaire sur `sub`.
- La complexité globale est "O(.S.S.S.S.)" = " 108" opérations - bien dans le délai fixé pour les limites données.

**Les astuces de style KMP ne fonctionnent pas** parce que l'appariement est dépendant du contexte*.
Si `sub[i] → x` et `sub[j] → x`, le caractère `x` dans `s` pourrait être le résultat d'un remplacement *ni l'un ni l'autre, de sorte que la fonction d'échec dans KMP ne peut pas savoir où faire marche arrière.

> **Bien** – Facile à coder, fonctionne assez vite.
> **Bad** – Des astuces plus intelligentes (FFT, NTT, ou KMP fantaisie) ajoutent de la complexité pour peu de gain.
> **Ugly** – La plupart des solutions KMP dans la discussion échouent sur des cas de test subtils.

---

- Oui. 3. Détails de la mise en œuvre

### 3.1 Caractère → Index Mapping

Indice
- Oui.
0 à 25 % "a à z"
26-51-A-Z-
52-61-0-9-

La cartographie est choisie de telle sorte qu'une matrice de 62×62 booléenne s'adapte confortablement en mémoire (~3.8 kB).

3.2 Brute- Logique de base de la force

Pour chaque position de départ «i» dans «s»:

«» "
pour j en 0 ... sub.longueur-1
si s[i+j]== Sub[j] → ok
Sinon, si peutRemplacer[sub[j]][s[i+j]] → ok
sinon casse
if j == sub.longueur → correspond à trouvé
«» "

La vérification s'arrête immédiatement sur une inadéquation, en maintenant l'algorithme linéaire dans la pratique.

---

- Oui. 4. Code (trois langues)

> **Note** – Les trois solutions mettent en œuvre l'idée *brute-force*.
> Ils compilent avec des versions standard: Java 17, Python 3.10+ et GNU‐C++17.

#### 4.1 Java

"Java
// Fichier: Solution.java
Importation de java.util.*;

solution de classe publique {
// Carte 'a'-'z' → 0..25, 'A'-'Z' → 26..51, '0'-'9' → 52.61
ALPHABET = 62;

match public booléenRemplacement(String s, String sub, char[][] mappages) {
int n = s.longueur(), m = sous-longueur();
booléen[][] remplacer = nouveau booléen[ALPHABET][ALPHABET];

// automatisation
pour (int i = 0; i < ALPHABET; ++i) remplacer[i][i] = vrai;

// Remplir les cartes utilisateur
pour (char[] mp : mappings) {
= idx(mp[0]); //
Int à = idx(mp[1]); // s‐char
remplacer [de][à] = vrai;
}

// recherche de force brute
pour (int i = 0; i <= n - m; ++i) {
int j = 0;
pendant que (j < m) {
int subIdx = idx(sub.charAt(j));
int sIdx = idx(s.charAt(i + j));
si (!replacer [subIdx][sIdx]) pause;
++j;
}
si (j == m) retourner true; // match complet
}
retourner faux;
}

// helper: carte à 0..61
interne statique privé idx(char c) {
si ('a' <= c && c <= 'z') retourner c - 'a';
si ('A' <= c && c <= 'Z') déclaration 26 + c - 'A';
retour 52 + c - '0'; // '0'..'9 '
}

// harnais d'essai simple
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();

char[][] maps1 = { {'a', 'b'}, {'a', 'c'} };
System.out.println(sol.matchRemplacement("abac", "aa", maps1)); // true

char[][] maps2 = { {'a', 'b'} };
System.out.println(sol.matchReplacement("abac", "bb", maps2)); // false

char[][] maps3 = { {'a', 'b'}, {'b', 'c'} };
Système.out.println(sol.matchRemplacement("abac", "ac", cartes3)); // true
}
}
«» "

4.2 Python

'`python
# Fichier : solution. py
de taper l'importation Liste

Solution de classe:
ALPHABET = 62 # 26 inférieur + 26 supérieur + 10 chiffres

@staticmethod
def _idx(c: str) -> Int:
""Carte 'a'-'z', 'A'-'Z', '0'-'9' → 0..61.""
si 'a' <= c <= 'z':
retour ord(c) - ord('a')
si 'A' <= c <= 'Z':
retour 26 + ord(c) - ord('A')
retour 52 + ord(c) - ord('0')

def matchRemplacement(
soi-même,
s: str,
sous: str,
mappages: Liste[Liste[str]],
-> Bool:
n, m = len(s), len(sub)

# remplacer[ancien][nouveau] == Vrai (vieux = char de `sub`, nouveau = char de `s`)
remplacer = [[Faux] * soi-même. ALPHABET pour _ dans la plage (self. ALPHABET)]
pour i à portée (même. - Oui.
remplacer[i][i] = Vrai # auto-cartographie

pour les anciens, nouveaux dans les cartes:
remplacer [self._idx(old)][self._idx(new)] = Vrai

# Recherche de force brute
pour i dans la plage (n - m + 1):
j = 0
alors que j < m:
si elle ne se remplace pas[self._idx(sub[j])][self._idx(s[i + j])]:
pause
j += 1
Si j == m:
retour Vrai
Retour Faux

♪ ----------------------------------------------------------------
# Tests manuels rapides (vous pouvez coller dans le coureur interactif de Leetcode)
si __nom__ == "__main__" :
sol = Solution()

maps1 = [['a', 'b'], ['a', 'c']]
print(sol.matchRemplacement("abac", "aa", cartes1)) Vrai

cartes2 = [['a', 'b']]
print(sol.matchRemplacement("abac", "bb", cartes2)) # Faux

cartes3 = [['a', 'b'], ['b', 'c']]
print(sol.matchRemplacement("abac", "ac", cartes3)) Vrai
«» "

### 4.3 C++17

'`cpp
// Fichier: solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
ALPHA = 62; // a-z, A-Z, 0-9

// helper: carte à 0..61
statique int idx(char c) {
si ('a' <= c && c <= 'z') retourner c - 'a';
si ('A' <= c && c <= 'Z') déclaration 26 + c - 'A';
retour 52 + c - '0';
}

match boolRemplacement(chaîne s, chaîne sous, vecteur<vector<char>> mappages) {
int n = s.size(), m = sub.size();
vecteur<array<bool, ALPHA>> remplacer(ALPHA);
pour (int i = 0; i < ALPHA; ++i) remplacer[i].fill(false);

// automatisation
pour (int i = 0; i < ALPHA; ++i) remplacer[i]i] = vrai;

// cartes utilisateur
pour (auto &mp : mappings) {
= idx(mp[0]); //
Int à = idx(mp[1]); // s‐char
remplacer [de][à] = vrai;
}

// recherche de force brute
pour (int i = 0; i <= n - m; ++i) {
int j = 0;
pendant que (j < m) {
int subIdx = idx(sub[j]);
la valeur de l'unité de mesure est égale à la valeur de l'unité de mesure de l'unité de mesure.
si (!replacer [subIdx][sIdx]) pause;
++j;
}
si (j == m) retourner true; // match complet
}
retourner faux;
}

// harnais d'essai simple
vide statique runTests() {
Solution sol;

vector<vector<char>> maps1 = {'a', 'b'}, {'a', 'c'} };
Cout << boolalpha << sol.matchRemplacement("abac", "aa", cartes1) << '\n'; // true

le vecteur<vector<char>> maps2 = {'a', 'b'} };
cout << sol.matchRemplacement("abac", "bb", cartes2) << '\n'; // faux

vector<vector<char>> maps3 = {'a', 'b'}, {'b', 'c'} };
cout << sol.matchRemplacement("abac", "ac", cartes3) << '\n'; // true
}
};

Int main() {
Solution::runTests();
retour 0;
}
«» "

---

- Oui. 5. Résumé de la complexité

L'approche Temps Espace Remarques
C'est pas vrai.
**Brute-Force**
**KMP (toute variante)**="O"+"sub"="O"(ALPHABET2)=" *Fails* sur les cas où un remplacement peut produire le même caractère dans `s". Autres
**FFT/NTT** Sur-ingénierie; accepté seulement pour le plaisir. Autres

---

- Oui. 6. Pensées finales

* **Le Bon** – Une seule matrice 62×62 + balayage linéaire de fenêtre est *exactement ce que le problème exige* et il est ** rapide, sûr et facile à comprendre**.
* **Le mauvais** – Sur-ingénierie (FFT, NTT, rétro-suivi fantaisie) ne cache que la difficulté *true* : la relation "matching" est *non déterministe* par caractère.
* **Les Ugly** – De nombreux messages de discussion montrent KMP ou tentatives cupides que *slip sur les cas de bord* parce qu'ils ignorent que `sub[i] → x` et `sub[j] → x` créer *deux* différentes possibilités de remplacement pour le même `x` dans `s`.

Si vous êtes un débutant de Leetcode ou un ingénieur de production, allez directement à l'approche de la matrice de force brute.
Si vous êtes curieux de la théorie, fouillez dans l'implémentation de la FFT (voir la discussion sur le Leetcode) – c'est un grand exercice de "look-at-the-code" mais vous n'en aurez jamais besoin pour ce problème.

Bon codage, et que vos sous-chaînes soient toujours alignées !