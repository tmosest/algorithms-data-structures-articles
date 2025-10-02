---
titre: LeetCode 902. Nombres au plus N donné jeu de chiffres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 902 – Nombres au plus N donné jeu de chiffres
**Java / Python / C++ – Des solutions complètes + un blog d'interviews "Bon / Mauvais / Ugly"* *

---

Résumé du problème

> **Grâce à un tableau trié `digits` (chaque élément est un seul chiffre `'1'...'9'`) et un entier `n`,
> **Retour** combien d'entiers positifs qui peuvent être écrits en utilisant seulement les chiffres dans les « chiffres » sont **.

*exemple*
` chiffres = ["1","3","5","7"]`, `n = 100` → **20** nombres: 1, 3, 5, 7, 11, 13, ..., 77.

**Contrôles* *

Valeur
- C'est quoi ?
1 ≤ chiffres longueur ≤ Les
Chaque chiffre [i]» est un caractère `'1'...'9'''
"1 ≤ n ≤ 109"

Le problème est un problème classique **numérique-DP / comptage** qui peut être résolu dans le temps *O(log n*) et *O(1)* avec une approche combinatoire simple.

---

## Description de la solution (la partie "Bien")

1. **Couvercle de tous les nombres avec moins de chiffres que `n`**
Si `n` a des chiffres `k`, tout nombre ayant des chiffres `1 ... k‐1` peut être formé à partir de chiffres `. choix de longueur pour chaque endroit.
«» "
Total = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
«» "

2. **Numéros à main avec le même nombre de chiffres**
Scanner les chiffres de `n` du plus significatif au moins significatif.
Pour la position actuelle «i» (0-basée à gauche):
* Compter le nombre de chiffres des « chiffres » ** strictement inférieur** à « n[i] ».
Chaque chiffre peut être suivi de toute combinaison des positions `k-i-1` restantes → ajouter
`(countLess) * (numériques.longueur)^{k-i-1}` à la réponse.
* Si ** aucun chiffre est égal** `n[i]`, nous sommes finis – le préfixe actuel dépasse déjà `n`.
* S'il y a ** est un chiffre égal** à `n[i]`, continuer à la position suivante.

3. **Ajouter 1 pour `n` si elle peut être formée* *
Si nous n'avons jamais éclaté tôt, tous les préfixes correspondent à `n`; ainsi `n` est un nombre valide → ajouter `1`.

L'algorithme fonctionne dans le temps linéaire dans le nombre de chiffres de `n` (10) et utilise un espace supplémentaire constant.

---

Code – Java

"Java
solution de classe {
Int public àMostNGivenDigitSet(chiffres de la chaîne[], int n) {
Chaîne N = chaîne.valeurOf(n);
int k = N.longueur(); // nombre de chiffres en n
int dlen = chiffres.longueur; // nombre de chiffres autorisés

long total = 0;

// 1) tous les chiffres ayant moins de chiffres que n
pour (int len = 1; len < k; len++) {
total += pow(dlen, len);
}

// 2) nombres de même longueur
pour (int i = 0; i < k; i++) {
Int cur = N.charAt(i) - '0';
booléen égal = faux;

pour (int j = 0; j < dlen; j++) {
int d = chiffres[j].charAt(0) - '0';
si (d < cur) {
le total += pow(dlen, k - i - 1);
} sinon si (d == cur) {
= vrai;
}
}

si (!egal) { // préfixe dépasse déjà n
retour (int) total;
}
}

// 3) n elle-même est valide
retour (int) (total + 1);
}

// puissance d'entier rapide pour petits exposants
long privé pow(int base, int exp) {
longue r = 1;
pendant la période 0) r *= base;
retour r;
}
}
«» "

**Complexités* *
- Temps: < < O(log n) > >
- Espace: `O(1)`

---

Code – Python

'`python
Solution de classe:
def atMostNGivenDigitSet(self, chiffres: Liste[str], n: int) -> Int:
N = str(n)
k = len(N)
dlen = len(chiffres)

# aide : puissance entière
def pow_int(b, e):
retour b ** e

Total = 0

# 1) tous les chiffres avec moins de chiffres
pour la longueur de portée(1, k):
Total += pow_int(dlen, longueur)

2) même longueur
pour i, ch dans l'énumération(N):
cur = int(ch)
= Faux
pour d en chiffres:
val = int(d)
si la valeur < cur:
Total += pow_int(dlen, k - i - 1)
val elif == cur:
= Vrai
si elle n'est pas égale:
retour total

# 3) n elle-même
total de retour + 1
«» "

---

Code – C++

'`cpp
solution de classe {
public:
int atMostNGivenDigitSet(vecteur<string>& chiffres, int n) {
chaîne N = to_string(n);
int k = N.size(); // chiffres en n
int dlen = chiffres.size(); // chiffres autorisés

long total = 0;

// 1) moins de chiffres
pour (int len = 1; len < k; + len)
total += pow_int(dlen, len);

// 2) même longueur
pour (int i = 0; i < k; ++i) {
Int cur = N[i] - '0';
bool égal = faux;
pour (chaîne de caractères &d : chiffres) {
Int val = d[0] - '0';
Si (val < cur)
total += pow_int(dlen, k - i - 1);
sinon si (val)
= vrai;
}
si (!egal) retourne static_cast<int>(total);
}

3) n elle-même
retourner static_cast<int>(total + 1);
}

particulier:
longue longue pow_int(int base, int exp) {
long r = 1;
pendant que (exp-) r *= base;
retour r;
}
};
«» "

---

Les pièges communs

Pourquoi il échoue
- C'est quoi ?
En utilisant `Math.pow` (Java) / `pow` (C++) qui retourne **double**
Autres Oubliant de gérer le cas où `n` est lui-même **non** constructible.
En supposant que `n` ait le même nombre de chiffres que le nombre le plus long possible.
Récursion avec mémoisation mais oublier d'utiliser "long long" Dépassement quand `digets.length` = 9 et la longueur = 10= Utilisez `long long` (64-bit) pour les sommes intermédiaires=
"(k-i-1)" Une mauvaise valeur de puissance. Vérifier soigneusement les indices.

---

Alternative: Digit-DP (l'Uglier, mais plus général)

Si vous avez besoin de supporter *différents* ensembles de chiffres par position ou plus de contraintes (p. ex., somme de chiffres, pas de zéros), le chiffre classique– DP avec mémoisation devient pratique.

"Java
// squelette Java
solution de classe {
int[] dp; // table de mémo
booléen[] vis-à-vis;
les chiffres des chaînes;
d'une puissance n'excédant pas 50 kW

Int public àMostNGivenDigitSet(chiffres de la chaîne[], int n) {
ce.chiffres = chiffres;
Chaîne s = Chaîne.valeurOf(n);
nDigits = longueur();
dp = nouvelle int[n Chiffres + 1;
vis = nouveau booléen[nDigits + 1][1];
les tableaux.fill(dp, -1);
retour dfs(0, true);
}

Int dfs(int pos, booléen serré) {
si (pos == nDigits) retourne 1;
si (!tight && vis[pos][0]) retourner dp[pos];
limite d'int = étroite ? (valeur de string.de(n)).charAt(pos) - '0' : 9;
Int ans = 0;
pour (String d : chiffres) {
Int val = d.charAt(0) - '0';
en cas de rupture (val > limite);
ans += dfs(pos + 1, limite serrée && val ==);
}
si (!standard) { vis[pos][0] = true; dp[pos] = ans; }
le retour des an;
}
}
«» "

Cette version est plus verbeuse mais montre comment la même logique se généralise.

---

Référencement et entrevues

- **Mots-clés**: *Code de leet 902*, *Nombres au plus N donnés ensemble de chiffres*, *solution de Java*, *solution de Python*, *solution de C++*, *entrevue de codage*, *chiffre DP*, *aide à l'entrevue d'emploi*.
- **Meta Description** (pour un billet de blog):
Voir les solutions Java, Python et C++, les explications détaillées et les pièges communs à éviter. Augmentez votre performance d'entrevue de codage! (en milliers de dollars)
- **Call‐to‐Action**: - Comme, partagez et inscrivez-vous pour plus de tutoriels prêts à l'entrevue. (en milliers de dollars)

**Conseil d'entrevue** :
- Commencez par l'idée de haut niveau (compter avec moins de chiffres).
- Préciser les hypothèses relatives à l'entrée (longueur de la donnée).
- Montrez le comptage combinatoire avant le codage.
- Discutez des cas de bord (=n'est-ce pas?=).
- Mentionnez la solution *O(log n*) comme une réponse propre et prête à la production.

---

Liste de contrôle finale

Mettre en œuvre le comptage combinatoire avec des pouvoirs entiers.
- [ ] Pré-ajoutez tous les numéros plus courts.
- [ ] Poignez le préfixe correctement.
- [ ] Ajouter `+1` seulement lorsque `n` est constructible.
- [ ] Utilisez des entiers 64 bits pour éviter les débordements.
- [ ] Effectuer des essais unitaires sur les entrées d'échantillons (`[1,35,7]`, `100`) et les cas bords (``["1","2","3"]`, «1234».

Bon codage et bonne chance dans votre prochaine interview! C'est ce qu'il a dit.

---

**Référence**:
- Énoncé du problème de LeetCode: https://leetcode.com/problèmes/numbers-at-most-n-gift-numer-set/
- Ressource numérique classique: https://cp-algorithms.com/algebra/digit-dp.html

---

*Préparé par: ChatGPT – Votre coach d'entrevue de codage AI. *