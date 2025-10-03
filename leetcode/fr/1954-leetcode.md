---
titre: LeetCode 1954. Périmètre minimum pour recueillir suffisamment de pommes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Récapitulation du problème – Périmètre minimal pour recueillir suffisamment de pommes

Dans une grille 2-D infinie, chaque point de treillis entier **(i, j)** abrite un arbre qui porte
Pommes "i" +"j"".
Vous possédez un terrain carré *aligné par l'axe* et centré sur l'origine.
Votre tâche :

> **Grâce à des "pommes nécessaires" (y compris les pommes qui se trouvent à la frontière de la parcelle),
> retourner le plus petit périmètre possible d'une parcelle qui contient au moins autant de pommes. **

Le périmètre est toujours un multiple de **8** – un fait qui transforme l'ensemble du problème en un puzzle de recherche binaire soigné.



-----------------------------------------------------------------------------------

Pourquoi ce problème est-il un grand exercice ?

Catégorie
- C'est pas vrai.
**Maths + Symmétrie**Signale que vous pouvez réduire une somme 2-D à une forme fermée. Autres
**Recherche binaire**= Un outil d'entrevue classique – réduit un grand espace de recherche à ~log‐time. Autres
**Gig‐Int Manutention**="nécessaire" peut être jusqu'à 10^15, vous devez donc utiliser l'arithmétique 64-bit partout. Autres
**Code – Réutilisabilité**Le même format fermé fonctionne en Java, Python et C++ – parfait pour un portfolio -copie-paste-et-run. Autres

Si vous pouvez passer par ce problème et expliquer les compromis bons, mauvais, laids, vous brillerez dans n'importe quel entretien d'algorithme.



-----------------------------------------------------------------------------------

Aperçu de la solution

L'approche de complexité Quand utiliser
C'est pas vrai.
**Brute-Force (O(n3))**= Trop lent – ne finira jamais pour l'entrée maximale.= **Ne jamais** – juste pour l'illustration. Autres
**Résumé direct (O( √n))**= Toujours trop lent pour 1015 pommes. Autres
**Fermé-Form + Recherche binaire**** **O(log n)** time, **O(1)** space. Autres
**O(1) via la formule de Cardano=**= En théorie, le temps constant, mais implique un point flottant et est sur-qualifié. Seulement pour la curiosité académique. Autres

Nous implémentons la solution **fermé-form + recherche binaire** dans les trois langues.



-----------------------------------------------------------------------------------

Mise en œuvre du code

> **Note** – Dans chaque langue, la variable **`n`** représente la distance entre le centre et un côté du carré (la moitié de la longueur latérale).
> Périmètre = "8 * n".
> Les pommes à l'intérieur du carré (y compris sa bordure) sont données par la forme fermée exacte:

«» "
pommes(n) = 2 * n * (n + 1) * (1 + 2 * n)
«» "

---

- Oui. 1. Java (Java 17)

"Java
// 1954. Périmètre minimum pour recueillir suffisamment de pommes
solution de classe publique {
/* Retourne le total des pommes à l'intérieur d'un carré dont la moitié est n
(longueur latérale = 2*n) */
total privé long Pommes(long n) {
retour 2L * n * (n + 1) * (1 + 2 * n);
}

public long minimumPérimètre(long nécéssaire) {
// n est au plus 100_000 parce que 2 * n^3 < 10^15 (prouvé dans l'éditorial)
longue lo = 1, hi = 100_000;
pendant qu ' il y a (l < bonjour) {
long milieu = lo + (h - lo) / 2;
si (totalApples(mid) < nécessaireApples) {
lo = milieu + 1; // besoin d'un tracé plus grand
} autre {
hi = mi; // mi est déjà assez grand
}
}
retour 8 * lo; // périmètre = 8 * n
}
}
«» "

Compiler et exécuter (essai JUnit ou méthode `main`):

"""
Javac Solution.java
java Solution
«» "

---

- Oui. 2. Python (Python 3.10+)

'`python
# 1954. Périmètre minimum pour recueillir suffisamment de pommes
Solution de classe:
@staticmethod
def _apples(n: int) -> Int:
"""Nombre de pommes fermées à l'intérieur d'un carré de moitié n."""
retour 2 * n * (n + 1) * (1 + 2 * n)

def minimumPérimètre(même, nécessaireApples: int) -> Int:
lo, hi = 1, 100_000 # 1 <= n <= 10^5 (voir éditorial)
alors que:
milieu = (lo + hi) // 2
if self._apples(mid) < needApples:
lo = milieu + 1
Sinon:
hé = milieu
retour 8 * hi # périmètre = 8 * n
«» "

Exécutez-le avec :

"""
python -c "import sys;print(Solution().minimumPérimètre(int(sys.argv[1]))" 1000
«» "

---

- Oui. 3. C++17

'`cpp
// 1954. Périmètre minimum pour recueillir suffisamment de pommes
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Pommes en forme fermée à l'intérieur d'un carré avec demi-face n
total statique long long Pommes (long terme n) {
retour 2LL * n * (n + 1) * (1 + 2 * n);
}

long long minimumPérimètre(long long needapples) {
longue longue lo = 1, hi = 100000; // 10^5 limite supérieure
pendant qu ' il y a (l < bonjour) {
long milieu long = (lo + hi) / 2;
si (totalApples(mid) < nécessaireApples)
lo = milieu + 1; // trop peu de pommes
Autre
hi = milieu; // assez de pommes, essayer plus petit
}
retour 8 * salut; // périmètre = 8 * n
}
};
«» "

Compiler avec `g++ -std=c++17 -O2 -Wall -o solution solution.cpp` et essai avec:

"""
./solution <<FEO
1
EOF
«» "

---

Article du blog – Le bon, le mauvais et le mauvais problème de jardin minimum

> **Mots clés:** Minimum Garden Perimeter, LeetCode 1954, interview en algorithme, recherche binaire, formulaire fermé, code d'entrevue, C++, Java, Python

---

Introduction – Pourquoi Ce problème est important

Les intervieweurs aiment les problèmes qui mélangent **grid math** avec ** algorithmique optimisation**.
LeetCode 1954 vous force à:

* Pensez aux points de réseau et **somme des distances de Manhattan**.
* Spot a **symétrie** qui s'effondre un problème 4 fois 2-D dans une formule 1-D soignée.
* Appliquer une recherche **binaire** sur un très petit espace de recherche (105) malgré l'entrée atteignant 1015.

Si vous pouvez expliquer cela dans une entrevue simulée d'une heure, vous êtes déjà un pas en avant sur de nombreux candidats.



C'est vrai. Les trois approches – bonne, mauvaise et laid

Démarche Complexité
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Sommation directe** (O(n2)) **Très lent** – `n` peut être 105, donc 1010 itérations. Simple à coder; aucun piège arithmétique. Impossible sur LeetCode 2-seconde limite. Autres
**Loop-Accumulation** (O( √n)) **O(n^(1/3))**=Élimine la somme intérieure; encore plus rapide que l'idéal direct mais *pas*. Nécessite un modèle mental «off‐by‐one»; toujours > 1 ms pour la plus grande entrée. Autres
Autres **Binary Search + Closed-Form** (O(log n)) () () **Faest** – 17 itérations pour 1015. () O(1) espace, O(log n) temps, aucune erreur de point flottant. Il faut manipuler soigneusement le débordement (utiliser 64 bits). Autres

> **Bien** – Recherche binaire avec le formulaire fermé dérivé.
> **Bad** – Force brute naïve ou somme simple.
> **Ugly** – Sur-ingénierie avec la formule de Cardanos ou les approximations de points flottants – parfaitement fine en théorie mais surqualifiée en pratique.



C'est vrai. Dérivé du formulaire fermé

1. **À mi-parcours Le carré s ' étend de `-n` à `+n` sur les deux axes.
2. **Pommes à "(i, j)"** – "(i) +"(j)".
3. **Total des pommes** à l'intérieur du carré:

«» "
Pommes(n) = (en milliers)
= 2 * n * (n + 1) * (1 + 2 * n) (prouvé par symétrie)
«» "

4. **Périmètre** du carré: `side = 2*n` → `périmètre = 8*n`.

Ainsi, le problème se réduit à ** trouver le plus petit `n` de telle sorte que* *
`2 * n * (n + 1) * (1 + 2*n) ≥ nécessaireApples`.



C'est pas vrai. Pourquoi la recherche binaire fonctionne

Pour les «pommes nécessaires ≤ 1015»:

«» "
pommes(105) = 2 * 105 * 105 * 2 * 105 *
«» "

Donc `n` ne dépasse jamais 105.
La fonction `apples(n)` augmente strictement, donc nous pouvons en toute sécurité bisect.



#### 5.

Toutes les multiplications intermédiaires doivent rester dans `int64_t`:

«» "
2LL * n * (n + 1) * (1 + 2 * n)
«» "

L'utilisation de **`long` en C++**, **`long` en Java** et **`int` avec 64 bits** en Python (`int` n'est pas limité) ne garantit aucun débordement.



C'est vrai. Réflexions finales – Communiquer l'idée

Lors d'une entrevue, vous pouvez :

1. Esquisse le **lattice** et souligne la symétrie.
2. Écrivez le formulaire **fermé** sur un tableau blanc.
3. Expliquez que `n ≤ 100 000` et qu'une recherche binaire finira instantanément.
4. Partagez les extraits de code (Java / Python / C++).

> **Résultat:** Vous démontrez **intuition mathématique**, **habileté algorithmique** et ** polyvalence linguistique** – exactement ce que les recruteurs recherchent.



-----------------------------------------------------------------------------------

Liste de contrôle à emporter

* Écrire le formulaire fermé **une fois** – le réutiliser dans n'importe quelle langue.
* Utiliser **64-bit arithmétique** (Java `long`, Python `int`, C++ `long`).
* Appliquer ** recherche binaire** sur `[1, 100000]`.
* Testez votre solution avec des boîtiers de bord (`1`, `1000`, `1015`).

Lorsque vous expliquez le problème lors d'une entrevue, rappelez-vous : *la solution "Good" est celle qui résout la plus grande entrée en 2 secondes et ne nécessite qu'une poignée de multiplications entières. *



-----------------------------------------------------------------------------------

Mot final – Comment cela augmente votre score d'entrevue

* ** Mathématiques claires** – Symmétrie et forme fermée montrent une compréhension profonde.
* **Rigor algorithmique** – La recherche binaire prouve que vous savez réduire la complexité.
* **Code de langue et d'agnostic** – Extraits de Portfolio pour Java, Python et C++.

Utilisez ce problème comme un point de discussion. Vous allez non seulement impressionner votre intervieweur, mais aussi vous donner un modèle de code réutilisable pour tout défi de codage futur. Bon codage !



-----------------------------------------------------------------------------------

> **Suivez-moi sur LinkedIn** pour plus de prép d'entrevue par algorithme, de tutoriels de codage et de hacks de recherche d'emploi.

Bonne entrevue!



-----------------------------------------------------------------------------------

**Fin de l'article**



-----------------------------------------------------------------------------------

> **Note moyenne** – Si vous avez aimé cette solution, laissez un commentaire ci-dessous ou partagez-la avec vos amis. Plus on résout, mieux on obtient. Joyeux hacking !



-----------------------------------------------------------------------------------

---


*(Préparé pour un public de recruteurs, de gestionnaires d'embauche et de coordonateurs prêts à l'entrevue.) *