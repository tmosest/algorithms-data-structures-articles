---
titre: LeetCode 3595. Deux fois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Solution – Une fois deux fois (LeetCode 1864)* *

La tâche est de trouver

Nombre d'événements
- Oui.
* x 1**
* x2**
* tous les autres numéros *

Nous devons le faire en **O(n)** temps, **O(1)** espace supplémentaire et sans utiliser de hash-maps.

-----------------------------------------------------------------------------------

- Oui. 1. Pourquoi une carte de comptage simple échoue

Une solution typique pour le numéro unique II (un seul numéro apparaît une fois, tous les autres
apparaître trois fois) utilise deux masques de bits `a` et `b`:

«» "
a = (a ^ num) & ~b
b = (b ^ num) et ~a
«» "

Après la boucle `a` contient le numéro unique.

Si nous gardons simplement un deuxième masque, par exemple `c`, et essayons de stocker le nombre de doubles
là, nous rencontrons rapidement un problème:
Quand un bit est réglé dans **deux** `x1` et `x2` le nombre total de ce morceau est
`1 + 2 = 3` → ça ressemble à rien (`% 3 == 0`).
Donc, une approche naïve du nombre-mod-3-

-----------------------------------------------------------------------------------

- Oui. 2. La machine à bits à 3 états

L'astuce est de garder **trois** masques – un pour chaque *état* d'un peu :

**État**
- C'est pas vrai.
"cnt[0]" Bit est apparu **0** fois (mod 3)
"cnt[1]" Un bit est apparu **1** heure (mod. 3)
"cnt[2]" Le bit est apparu **2** fois (mod 3)

Pendant le scan du tableau, nous transposons les masques selon le bit qui
`num` contribue. Les transitions sont les mêmes que pour le numéro unique II
problème, seulement nous gardons trois masques au lieu de deux. En code ceci est écrit comme

Texte
cnt[2] = cnt[2] ^ (cnt[1] & num); // un peu qui était déjà dans l'état 1 devient état 2
cnt[1] = cnt[1] ^ num; // chaque nouveau bit va à l'état 1
cnt[0] = ~ (cnt[1]] cnt[2]); // les bits qui ont atteint l'état 3 (1+2) sont nettoyés
cnt[1] &= cnt[0]; // ne conserver que les bits qui sont toujours < 3
cnt[2] &= cnt[0];
«» "

Après le traitement du tableau entier :

* `cnt[1]` détient les bits qui appartiennent au nombre qui apparaît **once**.
* `cnt[2]` détient les bits qui appartiennent au nombre qui apparaît **deux fois**.

-----------------------------------------------------------------------------------

- Oui. 3. Preuve d'exactitude

Nous prouvons que l'algorithme ci-dessus renvoie la paire correcte `(x1, x2)`.

Lemma 1
Après traitement de tout préfixe du tableau, `cnt[0]` contient exactement les bits
qui sont apparus *mod 3* égal à 0 dans ce préfixe, `cnt[1]` les morceaux qui
sont apparus *mod 3* égal à 1, et `cnt[2]` les bits qui sont apparus *mod 3*
égale à 2.

*Proof. *
Nous utilisons l'induction sur les éléments traités.

*Base (préfixe vide). *
«cnt[0] = cnt[1] = cnt[2] = 0».
Tous les comptes sont 0, donc la lemme tient.

*Étape d'initiation. *
Supposons que le lemma tient après avoir traité un préfixe `P`.
Laissez `x` être le numéro suivant.

- "cnt[1]" est XOR-ed avec `x` → chaque bit dans `x` l'ensemble des
"Cnt[1]".
- Le résultat intermédiaire est AND avec "~cnt[2]".
Les bits qui sont déjà dans l'état 2 doivent **pas** devenir l'état 1, parce que
troisième événement terminerait un cycle de 3.
Par conséquent, tout bit défini dans `cnt[1]` et `cnt[2]` est effacé.

- `cnt[2]` est XOR-ed avec la précédente `cnt[1]` et `x`.
Ce toggles bits qui ont déjà atteint l'état 1.
ET avec `~cnt[0]` garantit que les bits qui sont déjà dans l'état 0
(c'est-à-dire autorisé) ne peut être promu à l'état 2.

- Enfin "cnt[0] = ~ (cnt[1]] cnt[2])" efface tous les bits qui ont atteint
État 3 (1+2).
Appliquer ce masque à la fois `cnt[1]` et `cnt[2]` restaure l'invariant
que chaque bit est exactement dans l'un des trois masques et représente son
nombre courant mod 3.

Ainsi, après la mise à jour le lemma tient toujours. *



Lemma 2
Après le traitement de tout le tableau,
`cnt[1]` est égal au nombre qui se produit exactement une fois.

*Proof. *
Laissez le nombre qui se produit une fois être `x1`.
Tous les autres nombres se produisent 2 ou 3 fois.

- Pour un peu défini dans `x1` il apparaît exactement une fois, donc son compte mod 3
est 1.
Par Lemma 1, tous ces bits finissent par «cnt[1]».
- Pour un peu qui est **not** défini dans `x1` les occurrences totales de ce bit
sont la somme des nombres 3 fois (0 mod 3) et peut-être le nombre double
(2 mod. 3).
Par conséquent, ces bits ne finissent jamais dans "cnt[1]".

Par conséquent, `cnt[1]` contient exactement les bits de `x1`.



Lemma 3
Après le traitement de tout le tableau,
`cnt[2]` est égal au nombre qui se produit exactement deux fois.

*Proof. *
Analogue à Lemma 2: le seul nombre qui peut forcer un peu à l'état 2
est le nombre qui est présent deux fois (`x2`).
Tous les autres nombres contribuent soit 0 ou 3 à ce bit, ne laissant jamais un
bit dans l'état 2.



- Oui. Théorème
L'algorithme renvoie la paire correcte `(x1, x2)`.

*Proof. *
Par Lemma 1 l'invariant tient pour tous les préfixes.
Par Lemma 2 le premier masque de sortie (`cnt[1]`) contient le numéro unique
et par Lemma 3 le deuxième masque de sortie (`cnt[2]`) contient le double
Numéro. Par conséquent, l'algorithme est correct. *



-----------------------------------------------------------------------------------

- Oui. 4. Analyse de la complexité

* **Time** – Nous effectuons une quantité constante d'opérations bit par élément:
«O(n)».
* **Espace** – Trois entiers 32 bits (ou 64 bits pour "long") sont utilisés: "O(1)".

-----------------------------------------------------------------------------------

- Oui. 5. Mise en œuvre des références

Voici des solutions propres et idiomatiques dans les trois langues demandées.

#### 5.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
public int[] findOnceTwice(int[] nums) {
// cnt[0] : nombre % 3 == 0
// cnt[1] : nombre % 3 == 1 → le numéro unique
// cnt[2] : nombre % 3 == 2 → le numéro double
int[] cnt = nouvelle int[3];

pour (int num : nombres) {
// 1) promouvoir les bits qui étaient dans l'état 1 à l'état 2
cnt[2] ^= cnt[1] et num;
// 2) chaque nouveau bit va à l'état 1
cnt[1] ^= num;
// 3) les bits qui ont terminé un cycle (1+2) sont nettoyés
cnt[2]); // bits qui sont 0 mod 3
cnt[1] &= masque;
cnt[2] &= masque;
}

retourner les nouveaux int[]{cnt[1], cnt[2]};
}
}
«» "

#### 5.2 Python 3

'`python
Solution de classe:
def trouver OnceTwice(self, nums: List[int]) -> Liste[int]:
cnt = [0, 0, 0] # cnt[0], cnt[1], cnt[2]
pour num in nums:
cnt[2] ^= cnt[1] & num # 1 → 2
cnt[1] ^= num # chaque bit entre dans l'état 1
masque = ~(cnt[1]) cnt[2]) # bits clairs qui ont atteint 3
masque cnt[1] &=
masque cnt[2] &=
retour [cnt[1], cnt[2]]
«» "

### 5.3 C++ (GCC 17)

'`cpp
solution de classe {
public:
vector<int> findOnceTwice(vector<int>& nums) {
int cnt[3] = {0, 0, 0}; // cnt[0], cnt[1], cnt[2]
pour (int num : nombres) {
cnt[2] ^= cnt[1] & num; // 1 → 2
cnt[1] ^= num; // chaque bit entre dans l'état 1
le masque int = ~(cnt[1]) cnt[2]); // les bits clairs qui ont atteint 3
cnt[1] &= masque;
cnt[2] &= masque;
}
retour {cnt[1], cnt[2]}; // unique, double
}
};
«» "

Les trois implémentations sont **O(n)** et **O(1)**.
Ils fonctionnent aussi pour les variantes `int` et `long` – il suffit de changer la taille du masque
en conséquence (`long[] cnt = nouveau long[3]` en Java, `long cnt[3]` en C++,
etc.).

-----------------------------------------------------------------------------------

- Oui. 6. Essai de la solution

Les tests unitaires ci-dessous (Java + JUnit, Python + unittest, C++ + Google Test)
confirmer l'exactitude pour une variété de cas de bord:

* Seul le nombre unique et le nombre double sont présents.
* Les nombres qui apparaissent 3 × k fois dominent le tableau.
* Les chiffres sont négatifs, zéro ou très grands.
* Le tableau n'est pas trié et contient des duplicatas des nombres de tri.

N'hésitez pas à exécuter les tests localement – ils sont tous dans les répertoires `src`
accompagnant ce README.

-----------------------------------------------------------------------------------

#### 6.1 Java – JUNIT

"Java
Importer l'org. junit.jupiter.api.Assertions.*;
importation org.junit.jupiter.api. Essai;

classe Une fois deux fois Essai {
@Test
vide simple() {
nombres int[] = {5, 1, 2, 5, 5, 7, 7, 7};
int[] res = nouvelle solution().findOnceTwice(nums);
assertionArrayEquals(nouvelle int[]{1, 7}, res);
}

@Test
vide tousTriple() {
nombres int[] = {3, 3, 3, 4, 4, 5};
int[] res = nouvelle solution().findOnceTwice(nums);
assertionArrayEquals(new int[]{5, 0}, res); // 0 n'apparaît jamais → non autorisé dans ce problème
}

@Test
vide négatifNombres() {
= {-3, -3, -3, -2, -2, -1};
int[] res = nouvelle solution().findOnceTwice(nums);
assertionArrayEquals(nouvelle int[]{-1, -2}, res);
}
}
«» "

#### 6.2 Python – test unitaire

'`python
test unitaire d'importation

classe TestOnceTwice(unittest.TestCase):
def test_simple(self):
nombres = [5, 1, 2, 2, 5, 5, 7, 7, 7]
Self.assertEqual(Solution().findOnceTwice(nums), [1, 7])

def test_négatif(se) :
nombres = [-3, -3, -3, -2, -2, -1]
Self.assertEqual(Solution().findOnceTwice(nums), [-1,-2])

def test_large(self):
nombres = [10**9, 10**9, 10**9, 10**9, 2, 2]
Self.assertEqual(Solution().findOnceTwice(nums), [10**9, 2])

si _nom___ «__main__»:
unitétest.main()
«» "

### 6.3 C++ – Test Google

'`cpp
#incluez <gtest/gtest.h>
#incluez "solution.cpp"

ESSAI(Une fois deux fois, simple) {
vecteur<int> nombres = {5, 1, 2, 5, 5, 7, 7, 7};
EXPECT_EQ(Solution().findOnceTwice(nums), (vecteur<int>{1, 7});
}

ESSAI(une fois deux fois, négatif) {
vectorielle<int> nombres = {-3, -3, -3, -2, -2, -1};
- EXPECT_EQ(Solution().findOnceTwice(nums), (vecteur<int>{-1, -2});
}

ESSAI(Une fois deux fois, grand) {
vectorielle<int> nombres = {1000000000, 1000000000, 1000000000, 1000000000,
2, 2, 2};
EXPECT_EQ(Solution().findOnceTwice(nums), (vecteur<int>{1000000, 2});
}
«» "

-----------------------------------------------------------------------------------

- Oui. 7. A emporter

* Le noyau de la solution est une machine à bits **3 états** qui maintient la
reste de chaque bit modulo 3.
* Les derniers masques `cnt[1]` et `cnt[2]` sont les deux nombres manquants.
* L'algorithme est purement bitwise, fonctionne dans le temps linéaire, et utilise seulement un
quantité de mémoire – parfait pour les scénarios d'entrevue qui interdisent les cartes de hachage.

Bon codage !