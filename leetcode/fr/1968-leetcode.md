---
titre: LeetCode 1968. Tableau avec des éléments non égaux à la moyenne des voisins -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Aperçu du problème – LeetCode 1968
**Titre:** *Tableau avec des éléments qui ne sont pas égaux à la moyenne des voisins*
**Difficulté:** Moyenne
**Idée clé:** Triez le tableau et échangez chaque paire adjacente (un tableau d'onde). L'ordre qui en résulte garantit qu'aucun élément n'est la moyenne de ses deux voisins.

---

Pourquoi la vague fonctionne

Après tri des "nums" en ordre ascendant:

«» "
a0 ≤ a1 ≤ a2 ≤ ... ≤ an-1
«» "

Lorsque nous échangeons chaque paire `(ai, ai+1)` contre `i = 0, 2, 4 ...`, nous obtenons:

«» "
A1, A0, A3, A2, A5, A4, ...
«» "

- **À un indice pair `i`** (position originale impair) la valeur est la *large* des deux nombres qui étaient adjacents avant le tri.
Ses voisins sont tous deux **plus petits** parce que l'un vient d'une position inférieure et l'autre d'une position supérieure dans le tableau trié.
Par conséquent, la valeur moyenne ne peut jamais être la moyenne arithmétique des deux plus petits voisins.

- **À un indice impair `i`** (position uniforme originale) la valeur est la *plus petite* des deux nombres qui étaient adjacents avant le tri.
Ses voisins sont à la fois **plus grands** (ils proviennent des valeurs précédentes et suivantes triées).
Là encore, la valeur moyenne ne peut pas être la moyenne de deux nombres plus grands.

Puisque les éléments du tableau sont distincts, les deux voisins ne sont jamais égaux à l'élément du milieu, et la moyenne sera toujours différente de la valeur du milieu.

---

3 Solutions complètes

Code de la langue
C'est quoi, ça ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
[Python.py]**
*C++ **[C++].cpp**

> *Toutes les solutions sont exécutées en O(n log n)* en raison du tri; la passe linéaire suivante est O(n).

- Oui. 1. Java – Mise en œuvre de Greedy

"Java
// Solution Java – LeetCode 1968
Importer java.util. Les tableaux;

solution de classe publique {
[] réarrangement publicArray(int[] nombres) {
Trier le tableau
Tableaux.sort(nums);

// 2
pour (int i = 0; i + 1 < longueur nominale; i += 2) {
int tmp = nombres[i];
nombres[i] = nombres[i + 1];
nombres[i + 1] = tmp;
}

les numéros de retour;
}
}
«» "

**Pourquoi c'est bon:**
- Simple, lisible, pas de mémoire supplémentaire au-delà du tableau d'entrée.
- Fonctionne pour tous les "nums" valides (entiers distincts, longueur ≥ 3).

**Piège potentiel (la partie laid): * *
Si le tableau d'entrée était **pas** garanti distinct, l'échange pourrait encore fonctionner, mais la vérification -Moyenne devrait gérer des voisins égaux. Pour les contraintes de LeetCode, ce n'est pas un problème.

---

- Oui. 2. Python – Élégante vague uniligne

'`python
# Solution Python – LeetCode 1968
de taper l'importation Liste

Solution de classe:
def réarranger Tableau(s) : Liste[int] -> Liste[int]:
nombres.sort() # O(n log n)
retour [nums[i ^ 1] pour i in range(len(nums))]
«» "

**Explication:**
- `i ^ 1` retourne le dernier bit: `0→1`, `1→0`, `2→3`, `3→2`, ...
- Oui. La compilation de la liste construit le tableau d'ondes en un seul passage.

**Pour/contre :**
- **Bien:** Extrêmement concis, pas de boucle d'échange explicite.
- **Bad:** Peut-être plus difficile pour les débutants à lire.
- **Ugly:** Utilise l'astuce XOR – éviter si la clarté du code est primordiale.

---

- Oui. 3. C++ – Swap standard et bibliothèque

'`cpp
// C++ solution – LeetCode 1968
#incluez <algorithme>
#incluez <vecteur>

solution de classe {
public:
std::vector<int> réarrangementArray(std::vector<int>& nums) {
à:sort(nums.begin(), nums.end(); // O(n log n)

pour (size_t i = 0; i + 1 < nums.size(); i += 2) {/ O(n)
md::swap(nums[i], nombres[i + 1]); // onde
}
les numéros de retour;
}
};
«» "

**Pourquoi c'est propre:**
- Oui. Utilise la norme `std::swap`, aucune variable de température manuelle.
- Fonctionne pour toute "std::vector<int>` satisfaisant les contraintes de LeetCode.

---

Étape par étape (avec diagramme)

«» "
Original non trié: [6, 2, 0, 9, 7]
Après tri: [0, 2, 6, 7, 9]
Couples d'échange (0 & 1): [2, 0, 7, 6, 9]
Couples d'échange (2 & 3) : [2, 0, 9, 6, 7]
Résultat: [2, 0, 9, 6, 7]
«» "

- ** Même les indices (0,2,4):** valeurs `2, 9, 7` sont **plus grands** que leurs deux voisins.
- **Indices d'échéance (1,3):** les valeurs `0, 6` sont **plus petites** que leurs deux voisins.

Vérifiez i=1:
`(2 + 9)/2 = 5,5 φ 0`
Pour i=2:
"(0 + 6)/2 = 3 9 "
Pour i=3:
`(9 + 7)/2 = 8 φ 6`

Tous les chèques passent, confirmant la propriété.

---

Analyse du rendement

Étape Complexe Raison
C'est quoi, ça ?
Tri de **O(n log n)** Autres
Un passage linéaire sur le tableau. Autres
Total **O(n log n)** Autres
L'espace supplémentaire **O(1)** (en place) Autres

---

Nombre de cas de bord et validation

Résultat
C'est pas vrai.
La longueur = 3 , fonctionne; onde garantit la propriété. Autres
Autres Déjà une vague L'algorithme trie et échange, produisant une vague valide. Autres
Autres Tous les numéros sont distincts (garantie LeetCode) Autres
Les nombres aux limites extrêmes (0 et 105) Le tri des poignées sans débordement; calcul moyen utilise la division entière, mais nous comparons seulement l'égalité, pas calculer la moyenne réelle. Autres

---

Le bon, le mauvais et le mauvais de LeetCode 1968

> **Titre:** *LeetCode 1968 – Le Bon, le Mauvais, et le Lamentable de réorganiser une représentation*
> **Méta—Description:** Découvrez la solution d'onde gourmande, pourquoi elle fonctionne et comment la mettre en œuvre en Java, Python et C++. Parfait pour votre prochaine séance de codage.
> **Mots-clés cibles:** LeetCode 1968, Array with Elements Not Equal to Medium of Neighbors, solution Java, solution Python, solution C++, algorithme gourmand, tableau d'ondes, question d'entrevue.

---

- Oui. 1. Présentation

Lors de la préparation d'une entrevue sur l'ingénierie logicielle, vous rencontrerez souvent des problèmes de réarrangement de l'array. LeetCodes **1968** est un exemple premier : réorganiser un tableau entier distinct de sorte qu'aucun élément n'est la moyenne arithmétique de ses deux voisins**. Le problème semble délicat à première vue, mais un tour avide le transforme en un seul-liner.

---

- Oui. 2. Le problème en anglais clair

Vous recevez un tableau entier distinct `nums` (taille ≥ 3). Réorganiser de telle sorte que pour chaque indice interne «i» 1 ≤ i < n‐1):

«» "
nombres[i] (nums[i-1] + nombres[i+1]) / 2
«» "

Vous pouvez retourner ** n'importe quel** réarrangement valide.

---

- Oui. 3. Approches naïves (Pourquoi ils sont mauvais)

L'approche de la complexité Pourquoi il n'est pas idéal
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
La force brute permutations O(n!) Autres
# # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
Grêle sans tri de la graisse (O(n)) : Fails sur certaines entrées triées (par exemple, `[1,2,3]`). Autres

Ces méthodes explosent de façon combinatoire ou risquent des boucles infinies.

---

- Oui. 4. La solution des vagues d'avidité (le bon)

1. **Trier le tableau en ordre ascendant.
2. **Swap** toutes les paires d ' éléments adjacents (`0,01`, `2,23`, ...).

Pourquoi ça marche ?

- Après tri, les voisins de n'importe quel élément sont garantis d'être de côté en valeur.
- Les paires adjacentes à l'échange créent un motif *wave* : petit, grand, petit, grand, ...
- Oui. Dans une vague, chaque indice *même* détient une valeur *plus grande* que ses voisins, et chaque indice *od* détient une valeur *plus petite*.
- Par conséquent, l'élément intermédiaire ne peut jamais être la moyenne exacte de ses deux voisins (puisque les deux voisins diffèrent de magnitude sur le même côté).

**Proof Sketch:**
Laisser «a ≤ b ≤ c». Après tri, le triple est "[a, b, c]". L'échange donne "[b, a, c]".
- Pour l'indice intermédiaire (`a`), les voisins `b` et `c` sont tous deux plus grands → moyenne > `a`.
- Pour l'index `b`, les voisins `c` et `a` sont sur les côtés opposés → moyenne de l'index `b` (entiers distincts).

Ce raisonnement s'étend sur l'ensemble du tableau.

---

- Oui. 5. Extraits de mise en œuvre

C'est vrai. Java

"Java
[] réarrangement publicArray(int[] nombres) {
Tableaux.sort(nums);
pour (int i = 0; i + 1 < longueur nominale; i += 2) {
int tmp = nombres[i];
nombres[i] = nombres[i + 1];
nombres[i + 1] = tmp;
}
les numéros de retour;
}
«» "

Python

'`python
def réarranger Tableau(s) : Liste[int] -> Liste[int]:
nombres.sort()
retour [nums[i ^ 1] pour i in range(len(nums))]
«» "

C++

'`cpp
vecteur<int> réarrangementArray(vecteur<int>& nombres) {
(noms.begin(), nums.end());
pour (size_t i = 0; i + 1 < nums.size(); i += 2)
l'échange(nums[i], nombres[i + 1]);
les numéros de retour;
}
«» "

---

- Oui. 6. Les cas et les pièges les plus odieux

- **Numéros non distincts**: Le problème garantit la distinction, mais si vous abandonnez cette hypothèse, l'algorithme fonctionne toujours. Cependant, vous devez gérer l'égalité avec soin si vous calculez la moyenne réelle comme un flotteur.
- **Très petits tableaux** (`n = 3`): La vague tient toujours, mais double-vérifiez les limites de votre harnais d'essai pour éviter les erreurs hors-par-un.
- **Division entière** : Dans des langues comme Java, Python et C++, la division entière tronque. Puisque nous comparons seulement l'égalité, cela n'a pas d'importance. Si vous avez besoin de la moyenne exacte, jetez à "double".

---

- Oui. 7. Complexité temporelle et spatiale

Opération Complexité
C'est quoi ?
Tri de **O(n log n)** Autres
**O(n)** Autres
Total **O(n log n)**
Espace supplémentaire

---

- Oui. 8. Takeaway & Conseils d'entrevue

- Toujours lire les contraintes d'abord: le tri est bon marché et garantit la structure.
- Les patrons de Wave ou de Zig-zag sont puissants pour les problèmes impliquant des comparaisons locales.
- Lors de la présentation de la solution, passez par le raisonnement sur le tableau blanc – clarifiez le modèle d'échange et pourquoi les moyennes peuvent correspondre.
- Tester avec des données aléatoires et des cas de bord fabriqués à la main pour convaincre l'intervieweur de la justesse.

---

- Oui. 8. Conclusion

LeetCode **1968** est une vitrine de la façon dont un simple tour gourmand peut apprivoiser une contrainte apparemment complexe. La solution d'onde est propre, rapide et fiable sur toutes les entrées garanties par la plateforme. Maîtriser ce modèle vous donnera confiance pour un large éventail de questions d'entrevue de manipulation de réseau.

---

- Oui. 9. Appel à l'action

> **Les questions de réarrangement du tableau de l'as sont-elles prêtes? * *
> Pratiquer LeetCode 1968 en Java, Python, ou C++ et rejoindre notre série de prép interview hebdomadaire. **Inscrivez-vous gratuitement** et obtenez une liste de problèmes similaires!

---

10 ans. Lecture supplémentaire

- [LeetCode 150 – Évaluer la notation polonaise inversée]
- [Interview Cake – Tri et échangisme]
- [Cacher l'entrevue de codage – Array & String Problèmes]

---

**Fin de l'article**

---

À emporter

LeetCode 1968S cupidy wave strategy est à la fois **optimal** et **elegant**. Avec une implémentation claire en Java, Python et C++, vous allez non seulement résoudre le problème, mais aussi mettre en évidence la puissance d'un simple tri-et-swap dans votre prochaine interview de codage. Bonne chance, et le codage heureux!