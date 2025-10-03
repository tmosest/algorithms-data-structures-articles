---
titre: LeetCode 3344. Tableau du débit maximal -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème

**LeetCode 3344 – maximum Tableau de bord**
> **Difficulté:** Moyenne
> **Tags:** Recherche binaire, Manipulation bit, Mathématiques

> ** Exposé des problèmes* *
> On vous donne un entier positif `s`.
> Définir un tableau 3-D `A` de la taille `n × n × n` comme
> `A[i][j][k] = i * (j OR k)` pour tous `0 ≤ i, j, k < n`.
> Trouvez le plus grand entier `n` de sorte que la somme de *tous* éléments dans `A` ne dépasse pas `s`.

---

- Oui. 2. Intuition

La solution naïve serait de construire le tableau et de le résumer – impossible pour `n` > 10.
La clé est d'obtenir une formule **fermée** pour la somme qui peut être évaluée en temps O(log n).

Laissez

«» "
T(n) = 0...n-1 0...n-1
«» "

Alors la somme totale est

«» "
Total(n) = 0..n-1 i * T(n)
= T(n) * (n-1) * n / 2 (1)
«» "

Donc tout le problème se réduit à l'informatique `T(n)` efficacement.



### 2.1 Informatique `T(n)`

Pour un seul bit `b` (valeur `2^b`), la contribution de ce bit à `(j OR k)` est `2^b` chaque fois que **au moins un** de `j` ou `k` a ce jeu de bits.

«» "
paires où bit b est 0 en (j OR k) = (nombre de j avec bit b = 0)2
«» "

Si `cntZero(b)` est le nombre de nombres `< n` dont `b`‐th bits est 0, alors

«» "
bit_contribution(b) = (n2 - cntZero(b)2) * 2^b
«» "

«cntZero(b)» peut être trouvé en observant le modèle périodique du bit:

«» "
période = 2^(b+1)
Période complète = n / période
restant = n % période
cntZero(b) = pleinPériodes * 2^b + max(0, reste - 2^b)
«» "

Sommer la contribution pour tous les bits où `2^b < n` donne `T(n)`.



### 2.2 Recherche binaire

Une fois que nous pouvons évaluer `total(n)` en temps O(log n), nous recherchons le plus grand `n` avec
«total(n) ≤ s».

La portée de recherche peut être trouvée en doublant une limite supérieure jusqu'à ce que la somme dépasse `s` – ce qui garantit une limite supérieure serrée.



---

- Oui. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le maximum `n` satisfaisant à la condition.

Lemma 1
Pour tout «n», «total(n) = T(n) * (n-1) * n / 2».

*Proof. *
Total(n) = 0..n-1 i * 0.0j (j OR k)».
La somme intérieure double ne dépend pas de `i`; que ce soit `T(n)`.
C'est ainsi que "total(n) = T(n) * i i"
La somme des premiers entiers `n-1` est `(n-1)n/2`. *



Lemma 2
Pour toute position de bit `b`, le nombre de paires `(j,k)` où le bit `b`-th de `(j OR k)` est égal à 1
«n2 – cntZero(b)2».

*Proof. *
`(j OR k)` a bit `b` égal à 0 iff les deux `j` et `k` ont bit `b` égal à 0.
Il y a `cntZero(b)` ces numéros pour chacun des numéros `j` et `k`.
D'où le nombre de paires où le bit est 0 est `cntZero(b)2`.
Toutes les paires restantes (`n2 – cntZero(b)2`) définissent le bit. *



Lemma 3
La fonction `calcT(n)` retourne la valeur exacte de `T(n)`.

*Proof. *
Pour chaque bit `b` avec `2^b < n`, l'algorithme:

1. Calcule `cntZero(b)` par la formule de la période (exacte, dérivé du modèle binaire).
2. Ajouter `(n2 – cntZero(b)2) * 2^b` à l'accumulateur.

Par Lemma 2 c'est précisément la contribution de bit `b` à `T(n)`.
Le résumé de tous les bits pertinents reconstitue la somme double. *



- Oui. Théorème
`maxSizedArray(s)` renvoie le nombre maximal entier `n` de telle sorte que la somme de tous les éléments de `A` ne dépasse pas `s`.

*Proof. *
*Monotonicité. *
`total(n)` augmente strictement en `n` parce que chaque couche ajoutée contribue à une quantité non négative.
Par conséquent, le critère `total(n) ≤ s` est monotone: vrai pour tous `n ≤ n*` et faux pour tous `n > n*`, où `n*` est la réponse souhaitée.

*Binary Search Correctness. *
L'algorithme double la limite supérieure jusqu'à ce que `total(r) > s`, assurant la vraie réponse se trouve dans `[l, r]`.
La recherche binaire réduit ensuite à plusieurs reprises l'intervalle tout en préservant l'invariant que la vraie réponse se trouve dans les limites actuelles.
Lorsque la boucle se termine, `l` est la plus petite valeur avec `total(l) > s`, de sorte que `l-1` est la plus grande valeur avec `total(l-1) ≤ s`.
Ainsi, l'algorithme retourne le bon maximum `n`.



---

- Oui. 4. Analyse de la complexité

Laissez `B = -log2 n-- + 1` – le nombre de bits pertinents.

Étape
C'est quoi ?
"calcT(n)"" **O(B)**
Total(n)* **O(log)*
Recherche binaire (itérations de log n) Autres
Dans l'ensemble **O((log n)2)** temps, **O(1)** espace supplémentaire

Avec `s ≤ 1015`, `n` ne dépasse jamais environ `2·106`, de sorte que l'algorithme est assez rapide.



---

- Oui. 5. Mise en oeuvre des références

Voici trois solutions complètes et compilables : **Java**, **Python** et **C++**.
Tous utilisent l'arithmétique 64 bits («long» / «long long») parce que les résultats intermédiaires peuvent atteindre ~1018.

---

#### 5.1 Java

"Java
Importer java.io. Lecteur tamponné;
Importer java.io. InputStreamReader;
importer java.util.StringTokenizer;

solution de classe publique {
* ------- Nombre de nombres < n avec bit b = 0 -------- */
Zéros longs privés EnBit(long n, int b) {
longue période = 1L << (b + 1);
longue pleine = n/période;
longue rem = période n %;
longue cntZero = pleine * (1L << b);
long extra = Math.max(0L, rem - (1L << b));
retour cntZero + extra;
}

* ------- Somme de (j OU k) sur 0 <= j,k < n ------- */
calcT privé long(long n) {
somme longue = 0;
pour (int b = 0; (1L << b) < n; ++b) {
long cntZero = zérosInBit(n, b);
paires longues AvecBit = n * n - cntZero * cnt Zéro;
somme += pairesWithBit * (1L << b);
}
la somme de retour;
}

* ------- Somme totale du tableau 3-D pour la taille n
total privé long(long n) {
longue t = calcT(n);
long coeff = n * (n - 1) / 2; // φ i de 0 à n-1
retour t * coeff;
}

Int public maxSized Tableau(long s) {
longue basse = 1, élevée = 1;
alors que (total(élevé) <= s) { // trouver la limite supérieure
haut <<= 1; // double
}
pendant que (faible < haut) {
long milieu = (faible + élevé) / 2;
si (total(mid) <= s) {
faible = milieu + 1;
} autre {
haute = moyenne;
}
}
retour (int) (faible - 1);
}

* ----------------- Conducteur (pour les essais manuels) ----------------- */
public statique vide main(String[] args) lance Exception {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
StringTokenizer st = nouveau StringTokenizer(br.readLine());
long s = Long.parseLong(st.nextToken());
System.out.println(nouvelle solution().maxSizedArray(s));
}
}
«» "

---

#### 5.2 Python 3

'`python
importations

Solution de classe:
def zéros_in_bit(self, n: int, b: int) -> Int:
période = 1 << (b + 1)
pleine = n // période
rem = période n %
cnt_zero = pleine * (1 << b)
extra = max(0, rem - (1 << b))
retour cnt_zero + extra

def calc_t(self, n: int) -> Int:
Res = 0
b = 0
alors que (1 << b) < n:
cnt_zero = auto.zeros_in_bit(n, b)
paires_with_bit = n * n - cnt_zero * cnt_zero
Res += paires_with_bit * (1 << b)
b = 1
retour res

def total(self, n: int) -> Int:
t = auto.calc_t(n)
coeff = n * (n - 1) // 2
retour t * coeff

def maxSized Arrayage(self, s: int) -> Int:
lo, salut = 1, 1
alors que self.total(hi) <= s:
Bonjour <<= 1
alors que:
milieu = (lo + hi) // 2
si self.total(mid) <= s:
lo = milieu + 1
Sinon:
hé = milieu
retour lo - 1

si __nom__ == "__main__" :
s = int(sys.stdin.readline().strip())
print(Solution().maxSizedArray(s))
«» "

---

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
/* ---- nombre de nombres < n avec bit b = 0 ---- */
longs zéros longs EnBit(long long n, int b) {
longue période = 1LL << (b + 1);
longueur longue pleine = n / période;
long terme = période n %;
long long cntZero = plein * (1LL << b);
long extra = max(0LL, rem - (1LL << b));
retour cntZero + extra;
}

/* ---- T(n) : somme de (j) k) sur 0 <= j,k < n ---- */
longue longue calcT(long long n) {
somme longue = 0;
pour (int b = 0; (1LL << b) < n; ++b) {
long long cntZero = zérosInBit(n, b);
longues paires longues AvecBit = n * n - cntZero * cnt Zéro;
somme += pairesWithBit * (1LL << b);
}
la somme de retour;
}

/* ---- total des 3 Tableau D pour la taille n ---- */
long total long(long long n) {
long t = calcT(n);
long long coeff = n * (n - 1) / 2; //
retour t * coeff;
}

public:
Int maxSized Tableau (long s) {
long lo = 1, hi = 1;
pendant que (total(hi) <= s) h <<= 1; //
pendant qu ' il y a (l < bonjour) {
long milieu long = (lo + hi) / 2;
si (total(mid) <= s) lo = milieu + 1;
Autre salut = milieu;
}
Déclaration (int) (lo - 1);
}
};

- Oui. Conducteur (facultatif)
Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);
longues longues s;
si (cin >> s) {
Cout << Solution().maxSizedArray(s) << '\n';
}
retour 0;
}
«» "

---

- Oui. 6. Cas d ' épreuve

Entrée Sortie
C'est quoi ?
Autres "5"
"13"
"60"
"1000000000000000"""2000000" (en haut à l'entrée maximale)

N'hésitez pas à coller n'importe lequel des extraits dans votre IDE et tester plus loin.



---

- Oui. 6. FAQ

Question Réponse
C'est pas vrai.
Autres **Pourquoi ne pas utiliser une double boucle naïve?** se développe quadratiquement; une boucle O(n2) naïve serait beaucoup trop lente pour `n 106`. Autres
Autres **Avons-nous besoin de grands entiers?****= 64 bits (long) suffit parce que la plus grande valeur intermédiaire est inférieure à 1018, confortablement à l'intérieur signé 64 bits. Autres
Autres **Pouvons-nous utiliser la formule de la période en Python?**= Oui – Les entiers de précision arbitraire de Python rendent le calcul sûr. Autres
Autres **Et si `s` est 0?**= Le problème garantit `s ≥ 1`; sinon la réponse serait `0`. Autres
**L'algorithme est-il stable pour un très grand `s`?**=Le doublement de la limite supérieure garantit que la recherche binaire commence avec une plage correcte; l'algorithme fonctionne jusqu'à la limite de 64 bits. Autres

---

- Oui. 7. Pensées finales

La principale idée est que **chaque bit se comporte indépendamment** et suit un modèle périodique simple.
En exploitant cette structure, nous réduisons un poids apparemment lourd 3‐ D problème à une poignée d'opérations logarithmiques, permettant une solution de recherche binaire élégante qui est proviennement correcte et rapide.



---

- Oui. 8. Références

- Oui. La méthode bit-pattern périodique est une astuce standard utilisée dans les problèmes impliquant des sommes OR/AND bitwise (voir, p.ex., le sum d'AND/OU de toutes les paires de LeetCode).
- La recherche binaire monotone est une technique algorithmique classique pour trouver des conditions limites dans un prédicat trié ou monotone.



---

- Oui. 9. TL;DR

1. ** Calculer `T(n)`** – somme de `(j OR k)` – par itération sur bits.
2. **Comptabiliser le total** avec le formulaire fermé «total(n) = T(n) * (n-1)n/2».
3. **Binary-search** le maximum `n` avec `total(n) ≤ s`.

Toutes les étapes s'exécutent dans le temps `O(log n)2)` et l'espace `O(1)`, donnant une solution rapide et correcte en Java, Python et C++.



---

**Codage heureux!**