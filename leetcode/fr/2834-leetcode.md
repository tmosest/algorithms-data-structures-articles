---
titre: LeetCode 2834. Trouver la somme minimum possible d'un magnifique tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque nombre `x` la paire qui donne la somme `cible` est
«(x, cible-x)».

«» "
1 + (objectif 1)
2 + (objectif 2)
...
Cible/Cible/Cible/Cible
«» "

Si nous avons déjà utilisé tous les nombres `1 ...
nombre dans l'intervalle `=cible/2=1 ... cible-1` – chacun d'eux a
un partenaire qui est déjà pris et qui, ensemble, se résumerait à "cible".

Par conséquent,

* Tous les nombres `< cible` que nous pouvons utiliser sont exactement `1 ...
Ils forment une séquence arithmétique.
* Chaque nombre `≥ cible` est sûr – la somme avec n'importe quel entier positif
est plus grand que la "cible".
Ils forment la deuxième séquence arithmétique commençant par «cible».

Le but est de sélectionner les plus petits nombres `n` qui satisfont à ce qui précède
la restriction, c'est-à-dire prendre tous les petits nombres possibles d'abord et ensuite
poursuivre à partir de "cible" si plus de nombres sont encore nécessaires.

Les deux séquences sont

«» "
faible : 1 ... moitié (moitié = cible/2)
haut : cible ... cible+remaining-1
«» "

où

«» "
restant = n - min(n, moitié)
«» "

Les deux sommes peuvent être calculées selon la formule bien connue

«» "
somme(1 ... k) = k*(k+1)/2
«» "

et la somme d'une fourchette générale «[a ... b]» est

«» "
somme (1 ... b) – somme (1 ... a-1)
«» "

Tous les calculs sont effectués modulo «MOD = 1 000 000 007».

-----------------------------------------------------------------------------------

Algorithme
«» "
moitié = cible / 2
lowCount = min(n, moitié) // combien de nombres de la première partie
lowSum = lowCount*(lowCount+1)/2 (mod MOD)

restant = n - faible
si restant > 0
Début élevé = cible
élevé Fin = objectif + restant - 1
hautSum = (haut de gamme*(haut de gamme+1)/2
- (HighStart-1)*HighStart/2) (mod MOD)
Autre
élevé Somme = 0

réponse = (faible Somme + haute Somme) mod MOD
«» "

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie la somme minimale possible d'un
tableau anti-deux-somme de la longueur `n`.

---

Lemma 1
Si un nombre `x` satisfait `x < cible` et `x ≤ cible/2`, alors
tout nombre `y` avec `cible/2 < y < cible` a la propriété
`x + y = cible` et ne peut donc pas être choisi avec "x".

**Prof.**

`y` est dans l'intervalle `(cible/2, cible)` qui implique `cible-y`
appartient à `(0 , cible/2]`.
Parce que `x ≤ cible/2`, nous avons `cible-y ≥ cible-x ≥ 0`.
Ainsi "x + y = cible".



Lemma 2
Tout entier `z ≥ cible` peut être choisi avec tous les nombres
`1 ... cible-1` (c'est-à-dire avec un nombre inférieur à la cible).

**Prof.**

Pour chaque `x < cible` nous avons `x + z ≥ cible + 1 > cible`.
Par conséquent, la somme ne peut jamais égaler "cible".



Lemma 3
Le plus petit ensemble anti-deux-sommes de taille `n` est constitué de

* les premiers nombres `k = min(n, "cible/2") `1 ... k`
* si `n > k`, les numéros consécutifs `n-k` suivants à partir de `cible "

**Prof.**

À partir de Lemma 1 le jeu `{1,...,="cible/2=" contient le plus petit
éléments possibles.
Pas d'élément dans `(=cible/2=+1 , cible-1)` peut être ajouté,
Dans le cas contraire, il serait jumelé à un élément choisi pour la somme de "cible".
Ainsi, chaque élément de l'ensemble final doit être soit dans la première partie
ou au moins "cible".
Lemma 2 montre que tous les entiers `≥ cible` sont valides.
En prenant les plus petits nombres disponibles donne la somme minimale mondiale,
et c'est exactement la construction décrite. *



Lemma 4
"faible Sum` calculé par l`algorithme égale la somme du premier `k`
les entiers ('k = min(n, 'cible/2')').

**Prof.**

Par la formule de la série arithmétique

«» "
somme(1 ... k) = k(k+1)/2
«» "
L'algorithme applique cette formule modulo `MOD`.



Lemma 5
`highSum` calculé par l'algorithme est égal à la somme de la
entiers `cible ... cible+remaining-1`, où `remaining = n-k`.

**Prof.**

La somme d ' une fourchette est égale à [a ... b]

«» "
somme (1 ... b) – somme (1 ... a-1)
= b(b+1)/2 – (a-1)a/2
«» "

L'algorithme calcule exactement cette expression (modulo `MOD`).
Par conséquent, le «sum élevé» est la somme correcte des nombres requis. *



C'est vrai. Théorème
L'algorithme renvoie la somme minimale possible d'un tableau de longueur
`n` qui évite toute paire d'éléments en somme à `cible`.

**Prof.**

Laissez `S` être l'ensemble choisi par l'algorithme.
Par Lemma 3 `S` est exactement l`ensemble optimal de `n` plus petit
des éléments respectant la contrainte.
«lowSum» et «highSum» sont, par Lemma 4 et Lemma 5,
les sommes correspondant aux deux parties de «S».
Par conséquent, l'algorithme produit `sum(S)` (modulo `MOD`), qui est le
Montant minimum requis.



-----------------------------------------------------------------------------------

Analyse de complexité

Toutes les opérations sont simples arithmétiques; aucune boucle ou récursion n'est utilisée.

«» "
Heure : O(1)
Mémoire : O(1)
«» "

-----------------------------------------------------------------------------------

#### Mise en oeuvre des références (Java 17)

"Java
importation java.io.*;

classe publique {
Int final statique MOD = 1_000_000_007;

public statique int minimumPossibleSum(int n, int cible) {
moitié int = cible / 2;
int lowCount = Math.min(n, moitié); // nombres prélevés sur 1 ... moitié

// somme des premiers entiers positifs du compte bas
long lowSum = ((long) lowCount * (lowCount + 1) / 2) % MOD;

int restant = n - faibleConte; // nombres encore nécessaires
longue hauteur Somme = 0;
si (rester > 0) {
long départ = cible; // premier nombre du côté supérieur
long terme = cible + restant - 1; // dernier nombre nécessaire

// somme de 1 ... fin
longue sommeFin = fin * (fin + 1) / 2;
// somme de 1 ... (début-1)
longue sommeStartMinus1 = (démarrage - 1) *démarrage / 2;

hautSum = (somme Fin % MOD - sumStartMinus1 % MOD + MOD) % MOD;
}

retour (int) ((faible Somme + élevée Somme) % MOD);
}

/* --------------------------------------------- */

public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
StringTokenizer st = nouveau StringTokenizer(br.readLine());
int n = Integer.parseInt(st.nextToken());
cible int = Integer.parseInt(st.nextToken());
Système.out.println(minimumPossibleSum(n, cible));
}
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et
conforme à Java 17.