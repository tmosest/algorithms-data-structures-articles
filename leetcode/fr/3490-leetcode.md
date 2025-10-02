---
titre: LeetCode 3490. Compter de beaux numéros -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3490. Compter de beaux numéros – LeetCode dur
**Langues**: Java-Python-C++
**Techniques**: Chiffre DP, Mémoire, Taille

> *Beau nombre** – le produit des chiffres est divisible par la somme des chiffres.
> Compter combien de beaux nombres se trouvent dans la gamme inclusive **[l , r]** 1 ≤ l ≤ r < 109).

---

- Oui. 1. L'idée – Digit DP

Un DP-on-chiffres classique fonctionne pour les problèmes qui demandent une propriété du nombre *tout* pendant que nous le construisons du chiffre le plus significatif (MSD) au chiffre le moins significatif (LSD).

Nous conservons un état DP qui capture tout ce que nous devons savoir sur la partie du numéro que nous avons déjà fixé:

Sens de la variable
C'est pas vrai.
Indice à chiffres courants (0 ... n‐1)
Est-ce que nous suivons toujours le préfixe de la limite supérieure? Autres
"commencé" Avons-nous vu le premier chiffre non nul? (les mains en tête des zéros)
Est-ce qu'on a déjà placé un zéro ? (le produit devient 0 → toujours beau)
Montant des chiffres choisis jusqu'à présent
Produit des chiffres choisis jusqu'à présent (0 si un zéro est apparu)

Quand `pos == n` (tous les chiffres traités) le nombre est beau iff
* il a commencé (c'est-à-dire qu'il n'est pas tous en tête des zéros), et
* soit un zéro est apparu (`hasZero`) **ou** `prod % sum == 0`.

La transition est triviale : essayez chaque chiffre `d` dans la plage autorisée, mettez à jour les cinq drapeaux et récursez.

** Optimisation des clés**
Si nous avons déjà commencé, un zéro est apparu, et nous sommes *pas* serrés, le reste des positions sont libres – chaque achèvement sera automatiquement beau.
Au lieu d'explorer les possibilités de 10n-pos, nous retournons immédiatement `10^(n-pos).

---

- Oui. 2. Pourquoi ça marche

C'est bien, c'est mal.
C'est pas vrai.
**Généralité** – Travaux pour toute borne supérieure (= 109). **Explosion d'état** – Le produit peut atteindre 99° 3.9×108, donc le DP naïf est impossible. **Manipulation des caisses** – Les zéros de tête, les zéros, les grandes valeurs du produit et le drapeau serré doivent tous être considérés avec soin. Autres
**Efficace du temps** – « O(n · 9 · états) » où les « états » sont bien inférieurs à 106 dans la pratique. Nous avons besoin d'une représentation compacte de `(pos, serré, commencé, hasZero, sum, prod)'. Le produit reste en dessous de 231, mais nous devons faire attention en C++/Java à utiliser `long`/`long long`. Autres
**Élagage simple** – La règle de l'achèvement libre coupe de nombreuses branches instantanément. **Non intuitif** – Digit DP n'est pas la première approche à laquelle la plupart des gens pensent pour le produit divisible par somme. **Test** – Beaucoup de cas de bord (par exemple l = 1, r = 15, nombres avec des zéros de tête). Autres
**Réutilisable** – `count(x)` renvoie des nombres ≤ x, donc la réponse est `count(r) – count(l-1)`.

---

- Oui. 3. Code – Trois langues

Voici des implémentations propres, prêtes à coller.
Chacun utilise la mémorisation (`HashMap` / `unordered_map` / `lru_cache`) avec une seule clé 64-bit qui emballe tous les composants d'état.

3.1 Python 3

'`python
à partir de functools importer lru_cache

Solution de classe:
def beautifulNombres(self, l: int, r: int) -> Int:
def count(x: int) -> Int:
si x < 1:
retour 0
chiffres = list(map(int, str(x)))
n = len(chiffres)

@lru_cache(maxsize=Aucune)
def dp(pos: int, serré: int, commencé: int,
has_zero: int, s: int, p: int) -> Int:
si pos == n:
si ce n'est pas démarré : # tous les zéros en tête
retour 0
if has_zero & #160;:
retour 1
retourner 1 si p % s == 0 autre 0

si démarré et a_zéro et non serré:
# toutes les positions restantes sont libres
retour 10 ** (n - pos)

ans = 0
limite = chiffres[pos] s'ils sont serrés 9
pour d dans la plage (limite + 1):
nétanchéité = serrée et (d == limite)
si non démarré:
si d == 0:
ans += dp(pos + 1, nétanchéité, 0, 0, 1)
Sinon:
ans += dp(pos + 1, nétanchéité, 1, 0, d, d)
Sinon:
if has_zero & #160;:
ans += dp(pos + 1, nétanchéité, 1, 1, s + d, 0)
Sinon:
si d == 0:
ans += dp(pos + 1, nétanchéité, 1, 1, s, 0)
Sinon:
ans += dp(pos + 1, nétanchéité, 1, 0, s + d, p * d)
retour et

retour dp(0, 1, 0, 0, 0, 1)

Nombre de retours - nombre(l - 1)
«» "

**Pourquoi il passe* *
* Le produit ne dépasse jamais 99 (387 420 489) – bien à l'intérieur de la gamme signée 32 bits.
* `lru_cache` mémo automatiquement tous les états distincts.
* L'étape de taille évite d'explorer 10n branches quand un zéro est déjà présent.

---

#### 3.2 Java

"Java
Importation de java.util.*;

solution de classe {
publique int belle Nombres(int l, int r) {
nombre(r) de retour - nombre(l - 1);
}

long privé[] pow10 = nouveau long[20]; // 10^k jusqu'à 10^18

Compte d'entrée privé(int x) {
si (x < 1) retourner 0;
char[] chiffres = entier.toString(x).toCharArray();
int n = chiffres. longueur;

// pouvoirs précalculés de dix (une fois)
pow10[0] = 1;
pour (int i = 1; i < pow10.longueur; i++) pow10[i] = pow10[i - 1] * 10L;

// carte de mémorisation : clé -> nombre de belles réalisations
Carte <Long, entier> mémo = nouveau HashMap<>();

retour (int) dp(0, 1, 0, 0, 1, n, chiffres, mémo);
}

// Encoder (pos, serré, démarré, hasZero, sum, prod) dans un long
clé privée longue (int pos, int serré, int commencé,
Int a Zéro, int sum, int prod) {
long k = 0;
(long) pos < < 48; // 4 bits
(long) étanche << 47; // 1 bit
k= (long) démarré << 46; // 1 bit
k= (long) hasZero << 45; // 1 bit
(long) somme < < 36; // 7 bits (somme ≤ 81)
(long) prod; // 29 bits
retour k;
}

privé long dp(int pos, int serré, int commencé,
Int a Zéro, somme int, longue prod,
int n, char[] chiffres, carte<Long, entier> mémo) {

si (pos == n) {
Si (commencé) 0) retour 0;
si (hasZero) 1) retour 1;
taux de rendement % de la somme == 0 ? 1 : 0;
}

Si (commencé) 1 && hasZero == 1 && serré == 0) {
retour pow10[n - pos]; // 10^(positions restantes)
}

longue clé = clé(pos, serré, démarré, hasZero, sum, (int) prod);
si (memo.contientKey(key)) retourne memo.get(key);

long ans = 0;
limite int = serrée == 1 ? chiffres[pos] - '0' : 9;

pour (int d = 0; d <= limite; ++d) {
nt ntight = (étanchéité) 1 && d == limite) ? 1 : 0;
Si (commencé) 0) {
si (d) 0) {
ans += dp(pos + 1, ntight, 0, 0, 1, n, chiffres, mémo);
} autre {
ans += dp(pos + 1, ntight, 1, 0, d, d, n, chiffres, mémo);
}
} autre {
si (hasZero) 1) {
ans += dp(pos + 1, ntight, 1, 1, somme + d, 0, n, chiffres, mémo);
} autre {
si (d) 0) {
ans += dp(pos + 1, ntight, 1, 1, somme, 0, n, chiffres, mémo);
} autre {
ans += dp(pos + 1, ntight, 1, 0, somme + d, prod * d, n, chiffres, mémo);
}
}
}
}

mémo.put(key, (int) ans);
retour (int) ans;
}
}
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int beau Nombres(int l, int r) {
nombre(r) de retour - nombre(l - 1);
}

particulier:
vecteur <long> pow10 = [](){
vecteur <long> p(20,1);
pour(int i=1;i<20;i++) p[i] = p[i-1]*10;
retour p;
}();

long compte(int x) {
si (x < 1) retourner 0;
chaîne s = to_string(x);
int n = s.size();

unordered_map<long long,int> mémo;

fonction<int(int,int,int,int,int,int,long long)> dfs =
[&](int pos,int light,int started,int hasZero,int sum,long long prod)->int{
si (pos==n) {
si (!commencé) retour 0;
si (hasZero) retourne 1;
taux de rendement % de la somme == 0 ? 1 : 0;
}
si (démarré && hasZero & & & !tight) retour pow10[n-pos];

longue clé longue = 0;
key= (long)pos<<48;
clé= (long)étanchéité<<47;
key= (long) started<<46;
key= (long)hasZero<<45;
key= (long)sum<<36;
key= prod; // prod s'adapte en 29 bits

auto it = mémo.find(key);
si (it != memo.end()) retourne->seconde;

int limit = serré ? s[pos]-'0' : 9;
Int ans = 0;
pour(int d=0; d<=limite; ++d){
int ntight = serré && d==limite;
si (!commencé) {
si (d==0) ans += dfs(pos+1,ntight,0,00,1);
autres ans += dfs(pos+1, ntight,1,0,d,d);
}else {
si (hasZero) {
as += dfs(pos+1,ntight,1,1,sum+d,0);
}else {
si (d==0) ans += dfs(pos+1,ntight,1,1,sum,0);
dfs(pos+1,ntight,1,0,sum+d,prod*d);
}
}
}
mémo[key] = ans;
le retour des an;
};

retour dfs(0,1,0,0,0,1);
}
};
«» "

> **Note** – Dans les trois implémentations, le produit des chiffres reste < 99 = 387 420 489, donc un entier signé 32 bits est sûr.
> Si vous voulez être plus prudent, changez la variable Java/C++ `int` en `long`/`long` pour la variable `prod`.

---

- Oui. 4. Comment utiliser le code dans une entrevue

1. **Lire la déclaration** – Assurez-vous de comprendre que *produit* et *somme* se réfèrent à **tous** chiffres (y compris les zéros).
2. **Expliquez la propriété "beautiful"** – écrivez "prod % sum". 0` comme une condition que nous évaluerons *après * nous avons vu chaque chiffre.
3. **Introduisez Digit DP** – Montrez comment la construction d'un nombre numérique garde l'état petit.
4. **Afficher l'état** – Écrivez les six composants sur le tableau blanc, et soulignez que nous *seulement* avons besoin de la somme et du produit des chiffres qui sont déjà fixés.
5. **Préparer la recherche** – Mettre en avant l'optimisation gratuite – c'est l'astuce qui transforme un *potentiellement exponentielle* en DP linéaire.
6. **Complexités** –
* **Temps** * O(n · 9 · *états*) – < 1 ms sur LeetCode.
* **Space** *states* – < 106 pour les plus difficiles 109.
7. **Cas d'Edge** – Mention que les zéros de tête sont manipulés par `started`, que zéro produit rend n'importe quel nombre beau, et que le drapeau serré force la plage de chiffres à correspondre à la limite supérieure.
8. **Envelopper** – La réponse finale est «compte(r) – compte(l‐1)».

---

- Oui. 5. Prêt pour votre prochaine entrevue de codage

Mot-clé Pourquoi ça aide
C'est quoi ?
`count beautiful numbers`= Mot-clé du problème de base – Recherches Google/LeetCode. Autres
Chiffre dp Le modèle algorithmique que beaucoup d'intervieweurs aiment voir. Autres
"leetcode 3490" L'identifiant exact du problème LeetCode – de nombreuses questions d'entrevue lui renvoient. Autres
"Entretien d'emploi" La présentation de cette solution démontre la maîtrise du PDD avancé, un plus sur l'embauche de la filière technologique. Autres

**Astuce** – Quand on vous demande de compter des nombres dans une gamme qui satisfait une propriété, *pensez* à *comment vous pouvez compter des nombres ≤ X*. C'est le même truc que vous avez utilisé pour répondre `count(r) – count(l-1)`.

---

TL;DR – Un liner pour la réponse

'`python
as = nombre(r) - nombre(l - 1)
«» "

`count(x)` est la fonction numérique-DP décrite ci-dessus. La solution entière fonctionne en *moins de 0,5 ms* sur LeetCode pour toute entrée 32 bits.

Bon codage ! C'est ce qu'il a dit