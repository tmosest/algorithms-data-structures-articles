---
titre: LeetCode 3153. Somme des différences numériques de toutes les paires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Somme des différences numériques de toutes les paires – un guide complet
*(LeetCode 3153 – Moyen)*

---

Récapitulation des problèmes

Vous êtes donné un tableau "nums" de ** entiers positifs**.
Tous les entiers contiennent le même nombre de chiffres** (les lettres l'appellent `m`).

La différence de nombre **** entre deux entiers est le nombre de positions où les chiffres diffèrent.
Par exemple, `13` vs. `23` → `1` (seul le premier chiffre diffère).

**Tâche** – retourner la somme des différences de chiffres sur **toutes les paires non ordonnées** d'entiers dans le tableau.

> **Input**: `nums = [13, 23, 12] "
> ** Sortie**: `4`
> (1 + 1 + 2 de l'exemple ci-dessus)

Contraintes
- "2 ≤ longueur nominale ≤ 105 "
- `1 ≤ nombres[i] < 109'
- Chaque numéro a le même nombre de chiffres.

---

Pourquoi est-ce un LeetCode ?

- **Array et manipulation des chiffres** – teste la familiarité avec les boucles, les maths entiers et la manipulation des tableaux.
- **Complexité optimale** – la solution optimale est "O(n · m)" qui est nécessaire pour la grande limite d'entrée.
- **Attention aux détails** – division par 2, la manipulation du débordement, et l'état de la longueur du même chiffre.

---

## Aperçu de la solution – Compte de la colonne numérique

Intuition
Au lieu de comparer chaque paire (qui serait « O(n2) »), nous observons que les différences de chiffres peuvent être comptées **colonne‐par‐colonne**.

Pour une position à chiffres fixes `p` (du moins significatif au plus significatif):
1. Compter combien de nombres ont chaque chiffre `0–9`.
2. Les deux nombres qui ont *différent* chiffres à cette position contribuent **1** à la différence de la paire.
3. Pour un chiffre particulier qui apparaît «c» fois, le nombre de paires qui contiennent un nombre avec ce chiffre et un nombre avec un chiffre *différent** est «c × (n − c)».

Sommez cette quantité sur tous les chiffres `0–9` pour la colonne actuelle.
Faites cela pour chacune des colonnes `m`, puis divisez par `2` parce que chaque paire non ordonnée est comptée deux fois (une fois dans la perspective de chaque nombre).

Algorithme
Texte
n ← longueur(s)
m ← nombre de chiffres dans n'importe quel nombre[i]
réponse ← 0

pour chaque colonne de 0 à m-1
freq[10] ← {0}
pour i de 0 à n-1
chiffre ← nombres[i] % 10
freq[chiffre] += 1
nombres[i] //= 10 // supprimer le chiffre traité
pour d de 0 à 9 faire
réponse += freq[d] * (n - freq[d])

réponse de retour / 2
«» "

*Temps*: "O(n · m)"
*Espace*: "O(1)" (seulement un tableau de 10 éléments par colonne)

> **Pourquoi la division par 2? **
> Chaque paire `(i, j)` est comptée une fois lorsque `i` traite son chiffre et une fois lorsque `j` traite le même chiffre. Donc on réduit de moitié le total.

---

Cas et pièges

Qu'est-ce qu'il faut regarder ?
- C'est pas vrai.
La réponse est `0`. Notre algorithme donne naturellement `0` parce que `freq[d] = n` → `n * (n-n) = 0`.
Autres 2= Nombres importants (`< 109`)= Utiliser `long`/`int64` pour la réponse; `freq[d] * (n - freq[d])` peut dépasser 32 bits. Autres
Autres Division par 2 Réalisez après la boucle pour garder le résultat entier. Autres
Autres Si vous ne voulez pas modifier l'entrée, copiez le tableau d'abord ou extraire les chiffres par manipulation de chaîne. Autres
Autres 5 : zéros de tête ? Le problème garantit la même longueur de chiffre, de sorte que les nombres sont donnés sans tête zéro. Autres

---

Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

> Chaque solution suit les mêmes étapes algorithmiques.
> N'hésitez pas à copier-coller dans votre IDE ou éditeur en ligne pour tester.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public long sumDigitDifférences(int[] nums) {
int n = longueur nums;
// Déterminer le nombre de chiffres une fois
int m = chaîne.valeurDe(nums[0]).longueur();

long total = 0;
// Colonne de travail par colonne
pour (int col = 0; col < m; col++) {
int[] freq = nouvelle int[10];
// Nombre de chiffres dans cette colonne
pour (int i = 0; i < n; i++) {
nombre int = nombres[i] % 10;
freq[digit]++;
nombres[i] /= 10; // Supprimer le chiffre traité
}
// Ajouter les contributions de cette colonne
pour (int c : freq) {
Total += (long) c * (n - c);
}
}
total de retour / 2; // chaque paire comptée deux fois
}

// Pour des essais manuels rapides
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.sumDigitDifférences(nouvelle int[]{13, 23, 12}); // 4
Système.out.println(s.sumDifférences(nouvelle int[]{10, 10, 10}); // 0
}
}
«» "

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def sumDigitDifférences(self, nombres: List[int]) -> Int:
n = len(nums)
m = len(str(nums[0]) # tous les nombres ont la même longueur

Total = 0
pour _ dans l'intervalle(m):
freq = [0] * 10
pour i dans la plage(n):
nombre = nombres[i] % 10
freq[chiffre] += 1
nombres[i] //= 10 nombre de gouttes
pour c en freq:
Total += c * (n - c)

total de retour // 2

♪ Démo
si __nom__ == "__main__" :
s = Solution()
print(s.sumDigitDifférences([13, 23, 12]) # 4
print(s.sumDigitDifférences([10, 10, 10, 10]) # 0
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue longue sommeDigitDifférences(vecteur<int>& nums) {
int n = nombres.size();
int m = to_string(nums[0]).size(); // nombre de chiffres

long total = 0;
pour (int col = 0; col < m; ++col) {
int freq[10] = {0};
pour (int i = 0; i < n; ++i) {
nombre int = nombres[i] % 10;
+freq[numérique];
nombres[i] /= 10; // supprimer le chiffre traité
}
pour (int c : freq) {
Total += 1LL * c * (n - c);
}
}
total de retour / 2; // chaque paire comptée deux fois
}
};

Int main() {
Solution s;
vecteur <int> a = {13, 23, 12};
<< s.sumDigitDifférences(a) << enl; // 4

vecteur<int> b = {10, 10, 10, 10};
cout << s.sumDigitDifférences(b) << endl; // 0
}
«» "

---

Bonne, mauvaise, sombre plongée

Aspect du bien
- C'est quoi ?
**Efficacité algorithmique** Aucun – l'approche optimale est déjà utilisée. Si vous utilisez par inadvertance l'approche naïve O(n2), la solution sera TLE sur de grandes entrées. Autres
Autres **L'utilisation de l'espace**=L'espace supplémentaire constant.==Aucun=La suringénierie avec des matrices ou des cartes de hachage augmente inutilement la mémoire. Autres
**Clarté de la mise en œuvre**=Loops rectilignes, noms de variables clairs. La division par 2 peut être négligée. Autres La modification du tableau d'entrée peut surprendre les appelants – mieux vaut copier ou utiliser des chaînes si l'immutabilité est requise. Autres
**Manipulation de l'excès de flux**= Utilise des entiers 64 bits.= Oublier de jeter `int` à `long` en C++/Python `int` peut déborder en Java (`int` trop petit). En Java, l'utilisation de `int` pour le résultat débordera pour de grandes entrées (par exemple, 100 000 numéros). Autres
**La robustesse d'un boîtier d'Edge** Si le tableau d'entrée n'est pas garanti d'avoir la même longueur, l'algorithme échoue silencieusement. Ne pas valider la longueur d'entrée ou la cohérence numérique peut conduire à des bogues subtils dans la production. Autres

---

Référencement et recherche d'emploi

- Oui. Méta Titre
**Sum des différences numériques de toutes les paires – Solutions Java, Python & C++

Description de la méta
Master LeetCode 3153 -Sum of Digit Differences of All Pairs avec des implémentations Java, Python et C++ claires. Apprenez la technique de comptage des colonnes O(n·m), la manipulation des cas de bord et les explications prêtes à l'entrevue.

- Oui.
Somme des différences numériques de toutes les paires – LeetCode 3153

- Oui.
- Exposé des problèmes
- Intuition et approche optimale
- Cas de bord et pièges communs
- Solution Java
- Solution Python
- C++ Solution
- Analyse de complexité
- Tant mieux. Méchant

### Mots-clés pour éparpiller
- LeetCode 3153
- Somme des différences numériques de toutes les paires
- Problème de codage des interviews Java
- Exemple d'algorithme Python
- Question d'entretien de programmation C++
- Solution O(n·m)
- Technique du tableau de fréquence
- Préparation des entretiens
- Entretien en génie logiciel

---

À emporter

La technique **chiffre-colonne** est un modèle puissant pour les problèmes qui demandent des différences par paires sur les représentations numériques à largeur fixe. En réduisant une force brute `O(n2)` à un seul passage sur les chiffres, nous obtenons à la fois vitesse et élégance – exactement ce que les intervieweurs veulent voir.

N'hésitez pas à adapter le code à votre propre style, à ajouter des tests unitaires ou à l'intégrer dans une base de codes plus grande. Bonne chance pour écraser cette interview ! C'est ce qu'il a dit