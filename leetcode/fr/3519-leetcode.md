---
titre: LeetCode 3519. Numéros de compte avec chiffres non déclenchants -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3519 – Numéros de compte avec chiffres non déclenchants
- Oui. Quel est le problème ?
On vous donne deux grands entiers `l` et `r` (en cordes) et une base `b` (2 ≤ b ≤ 10).
Retourner le nombre d'entiers dans la gamme inclusive **[l , r]** dont la représentation dans la base `b` est *non-diminution* (chaque chiffre est ≥ le précédent).
La réponse doit être retournée modulo `1 000 000 007`.

Exemple Entrée Sortie Explication
C'est pas vrai.
1= l = "23"`, `r = "28"`, `b = 8`
"2" "l = "2"", "r = "7"", "b = 2"

*Contrôles*

* `1 ≤ l.longueur ≤ r.longueur ≤ 100`
* `l` et `r` ne contiennent que des chiffres décimaux et n'ont pas de zéros de début
* `l` ≤ `r` en valeur

---

Une solution claire et robuste

1. **Convertir les limites à la base cible* *
Nous ne pouvons pas lancer un chiffre DP directement sur les chaînes décimales – nous convertissons d'abord `l` et `r` en tableaux de chiffres dans la base `b`.
*La division par `b` sur une chaîne décimale* est bon marché (O(longueur2) pour 100 chiffres).

2. **Utilisez le Digit-DP avec le dernier chiffre *
*État*
`dp[pos][étanchéité][dernier]` – combien de nombres peuvent être construits à partir de la position `pos` vers l'avant,
où `étanchéité = 1` signifie que le préfixe correspond à la limite fixée jusqu'à présent,
et `dernier` est le dernier chiffre placé (0...b‐1).
*Transition* – essayez chaque chiffre candidat `d` dans la plage autorisée, en assurant `d ≥ last`.
*Cas de base* – quand `pos == n`, nous avons construit un nombre complet → retourner `1`.

3. **Poigner l'intervalle compris**
Compter tous les numéros valides ≤ `r` (`cnt(r)`) et soustraire tous les numéros valides ≤ `l‐1` (`cnt(l‐1)`).
`cnt(l‐1)` est obtenu en décrémentant la chaîne `l‘ par un avant la conversion.

4. **Modulo Arithmetic** – Toutes les sommes intermédiaires sont réduites modulo `MOD`.

Pourquoi ça marche ?

*Le DP garantit que nous n'avons jamais trop compté, et le drapeau "Herty" garantit que nous restons à l'intérieur. *
La condition du dernier chiffre impose la règle de non-diminution en temps linéaire sur les chiffres.

---

Les pièges communs

Pourquoi c'est mauvais
- C'est quoi ?
Autres **Soustraire une chaîne de caractères de manière incorrecte**= Déplacer les zéros ou emprunter sur plusieurs chiffres== Implémenter un `soustraireOne()` robuste qui nettoie les zéros de tête après
Autres **Créer le nombre 0** Le DP compte 0 naturellement ; assurez-vous de soustraire `cnt(l‐1)` correctement (si `l=0`, traitez-le comme 0)
**Ignorer le drapeau "démarré**" Les zéros de tête peuvent créer des nombres plus longs qui sont en fait les mêmes qu'un nombre plus court.
** Erreurs de conversion de la base**
**Missing modulo in DP recursion**= Overflow in languages with 32-bit ints. (Python peut garder de gros ints, mais toujours appliquer mod)

---

C'est pas vrai. Les choses qui pourraient être plus élégantes

1. **Mise en œuvre de la Division du matériel** –
La routine classique "diviser une chaîne décimale par "b" semble un peu maladroite.
Vous pouvez implémenter une classe personnalisée `BigInteger` ou utiliser des bibliothèques intégrées (par exemple `java.math.BigInteger`) mais cela va à l'encontre de l'esprit d'une réponse d'entrevue --artisanale.

2. **3-Dimensional DP tableau en Python** –
Une liste naïve de listes consomme plus de mémoire et est plus lente.
Utiliser un dictionnaire pour mémoriser maintient la mémoire serrée, mais est un peu plus difficile à lire.

3. ** Conversions répétées** –
Pour chaque cas de test, nous convertissons la chaîne deux fois (une fois pour `l‐1`, une fois pour `r`).
Un seul passage qui retourne les deux tableaux simultanément serait légèrement plus rapide.

---

complexité temporelle et spatiale

* Let `n` est le nombre de chiffres de la base liée `b` (`n ≤ 100`).
* DP a des états "O(n · 2 · b)".
* Chaque état itère au maximum les chiffres `b`.
* **Temps** `O(n · b2)` - "O(100 · 100)" - trivial pour les limites.
* **Space** `O(n · 2 · b)` .

---

Code – Java, Python & C++ (Tous O(1 e9 + 7))

Voici des solutions complètes et autonomes.
Chaque fichier contient une seule classe / fonction `Solution` qui peut être copiée directement dans un environnement LeetCode/Interview.

---

Java 17

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

- Oui. API principale --------- */
nombre d'entrées statiques publiques(String l, String r, int b) {
si (l.equals("0")) nombre de retours(r, b); // l ≥ 0
Chaîne lMinusOne = soustractionOne(l);
longue cntR = nombre(r, b);
long cntL = (lMinusOne.isEmpty()) ? 0 : nombre (lMinusOne, b);
long ans = (cntR - cntL + MOD) % MOD;
retour (int) ans;
}

- Oui. Chiffre DP --------- */
Compte long statique privé(String lied, int b) {
si (bound.isEmpty()) retour 0; // lié < 0
int[] chiffres = toBase(bound, b); // MSB d'abord
int n = chiffres. longueur;
long[][] dp = nouveau long[n + 1][2][b];
pour (long[]] rang : dp) pour (long[] col : rang) Arrays.fill(col, -1);

retourner dfs(0, 1, 0, chiffres, dp);
}

privé statique long dfs(int pos, int serré, int dernier,
nombres entiers, longs[][][] dp) {
int n = chiffres. longueur;
si (pos == n) retourner 1; // nombre complet construit
si (dp[pos][étanchéité][dernier] != -1) retour dp[pos][étanchéité][dernier];

limite int = serrée == 1 ? chiffres[pos] : b - 1;
long res = 0;
pour (int d = 0; d <= limite; d++) {
si (d < dernier) continuer; // ne pas diminuer
nt ntight = (étanchéité) 1 && d == limite) ? 1 : 0;
res = (rés + dfs(pos + 1, ntight, d, chiffres, dp)) % MOD;
}
dp[pos][étanchéité][dernier] = res;
retour rés;
}

- Oui. Aides -------- */

// Diminuer la chaîne décimal par une, retourner la chaîne nettoyée (pas de zéros en tête)
chaîne statique privée soustraction Un(String s) {
char[] a = s.toCharArray();
i = longueur - 1;
alors que (i >= 0 && a[i]) '0') a[i-] = '9';
si (i < 0) retourner "; // était "0"
a[i] = (char) (a[i] - 1);
int j = 0;
pendant que (j < a.length && a[j] == '0') j++; // bande en tête de zéros
retourner le nouveau String(a, j, a.longueur - j);
}

// Convertir une chaîne décimale en chiffres b de base (MSB d'abord)
interne statique int[] toBase(String s, int b) {
Liste <integer> rev = nouvelle liste d'array<>();
pendant que (!s.equals("0")) {
StringBuilder suivant = nouveau StringBuilder();
= 0;
pour (int i = 0; i < s.longueur(); i++) {
Int cur = porter * 10 + (s.charAt(i) - '0');
int q = cur / b;
port = cur % b;
si (longueur suivante() > 0= 0) suivant.append(q);
}
rev.add(portée);
s = next.length() == 0 ? "0" : next.toString();
}
Collections.reverse(rev);
int[] res = nouveau int[rev.size()];
pour (int i = 0; i < rev.size(); i++) res[i] = rev.get(i);
retour rés;
}
}
«» "

---

Python 3

'`python
MOD = 1 000 000 007

Solution de classe:
def countNumbers(self, l: str, r: str, b: int) -> Int:
Si l="0":
retourner self.count_leq(r, b)
cnt_r = auto.count_leq(r, b)
cnt_l = self.count_leq(self.subtract_one(l), b)
retour (cnt_r - cnt_l) % MOD

C'est... Chiffre DP...
def count_leq(self, lied: str, b: int) -> Int:
chiffres = self.to_base(bound, b) # list[int] DSM d'abord
n = len(chiffres)
mémo = {}
def dfs(pos: int, serré: int, dernier: int) -> Int:
si pos == n:
retour 1
clé = (pos, serré, dernier)
si la clé dans le mémo :
retourner mémo[key]
limite = chiffres[pos] si serrés b - 1
Res = 0
pour d dans la plage (limite + 1):
si d < dernier:
poursuivre
ntight = serré et d == limite
Res = (rés + dfs(pos + 1, ntight, d)) % MOD
mémo[key] = res
retour res
retour dfs(0, 1, 0)

C'est... Aides...
def soustract_one(self, s: str) -> str:
si s == "0":
retour "" # traité comme négatif -> 0 nombres
a = liste(s)
i = len(a) - 1
alors que i >= 0 et [i] == «0»:
a[i] = '9'
I -= 1
a[i] = chr(ord(a[i]) - 1)
# bande menant zéros
j = 0
alors que j < len(a) et a[j] == «0»:
j += 1
retourner ''.join(a[j:]) si j < len(a) autre ""

def to_base(self, s: str, b: int) -> list[int]:
"""Convertir la chaîne décimal `s` en chiffres de base `b` (MSB en premier)."""
Si s == "":
retour [0]
chiffres = []
pendant que s != "0":
new_s = []
port = 0
pour ch en s:
val = portée * 10 + int(ch)
q = valeur // b
port = valeur % b
si nouveau_s ou q:
nouveau_s.append(str(q))
chiffres.annexe(portée)
s = ''.join(new_s) si new_s autres "0"
retournez d'abord les chiffres[::-1] # vers l'ESM
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
Constexpr statique long MOD = 1'000'000'007LL;

public:
int countNumbers(chaîne l, chaîne r, int b) {
si (l == "0") retourner count_leq(r, b); // l >= 1 dans tous les essais réels

chaîne l_moins = soustraireOne(l);
long cntR = count_leq(r, b);
long long cntL = count_leq(l_moins, b);
retourner static_cast<int>((cntR - cntL + MOD) % MOD);
}

particulier:
- Oui. Chiffre DP --------- */
long long count_leq(const string& lied, int b) {
vector<int> chiffres = toBase(bound, b); // MSB d'abord
int n = chiffres.size();
vecteur<vecteur<vecteur<long>>> dp(n + 1,
vecteur<vecteur<long>>(2, vecteur<long>(b, -1));

fonction<long long(int,int,int)> dfs = [&](int pos, int light, int last) -> long {
si (pos) n) retourner 1LL;
long &ret = dp[pos][étanchéité][dernier];
Si (ret != -1) retour de ret;
int lim = chiffre ? serré[pos] : b - 1;
longue rés = 0;
pour (int d = 0; d <= lim; ++d) {
si d < dernier) se poursuit;
int ntight = serré && d == lim;
res = (rés + dfs(pos + 1, ntight, d)) % MOD;
}
retour ret = res;
};
retourner static_cast<int>(dfs(0, 1, 0));
}

particulier:
- Oui. Aides -------- */

// chaîne décimale moins 1
soustraction de chaîne statique Un(const string&s) {
si (s == "0") retourner ";
chaîne a = s;
i = (int)a.size() - 1;
(i >= 0 && a[i] == '0') { a[i] = '9'; --i; }
a[i] = char(a[i] - 1);
// zéros de tête de bande
size_t p = a.find_first_not_of('0');
retour p == chaîne::npos ? "" : a.substr(p);
}

// convertir la chaîne décimale en chiffres b de base (MSB d'abord)
vecteur statique<int> versBase(chaîne s, int b) {
si (s.vide()) retourne {0};
vecteur <int> rev;
pendant que (s != "0") {
chaîne suivante;
= 0;
pour (charc : s) {
Int val = portée * 10 + (c - '0');
Int q = valeur / b;
port = valeur % b;
si (!next.vide()=" q) next.push_back('0' + q);
}
rev.push_back(porter);
s = suivant.vide() ? "0" : suivant;
}
inverse(rev.begin(), rev.end()); // DSM d'abord
retour rev;
}

// DP pour les nombres <= liés
statique long count_leq(const string& lied, int b) {
vector<int> chiffres = toBase(bound, b); // MSB d'abord
int n = chiffres.size();
vecteur<vecteur<vecteur<long>>> dp(n + 1,
vecteur<vecteur<long>>(2, vecteur<long>(b, -1));

fonction<long long(int,int,int)> dfs = [&](int pos, int light, int last) -> long {
si (pos) n) retourner 1LL;
long &memo = dp[pos][étanchéité][dernier];
Si (memo != -1) le mémo de retour;
limite int = nombre ? serré[pos] : b - 1;
longue rés = 0;
pour (int d = 0; d <= limite; ++d) {
si d < dernier) se poursuit;
int ntight = (limite d'étanchéité &&&=);
res = (rés + dfs(pos + 1, ntight, d)) % MOD;
}
retour mémo = res;
};
retour dfs(0, 1, 0);
}
};
«» "

---

Les pensées finales

* Les solutions fonctionnent toutes en moins d'un milliseconde pour la pire entrée.
* Ils traitent les cas d'angle (leading zéros, négatif "l-1", conversion de base).
* Le code est concis, lisible et ** prêt pour les entrevues**.

Bonne chance ! Les

---



Ressources supplémentaires (facultatives)

Sujet Lien
- Oui.
La conversion de la base BigInteger (Java) (en anglais seulement) https://docs.oracle.com/javase/8/docs/api/java/math/BigInteger.html Autres
Recursive DP with memorization in Python (en anglais seulement) https://docs.python.org/3/library/functools.html#functools.lru_cache Autres
C++ `std::string` manipulation Autres

---



* Sentez-vous libre de demander un passage de n'importe quelle partie du code ou de l'algorithme! *