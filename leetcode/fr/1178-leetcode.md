---
titre: LeetCode 1178. Nombre de mots valides pour chaque Puzzle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour un mot être *valable* pour un puzzle

* chaque lettre du mot doit apparaître dans le puzzle
* la première lettre du puzzle doit apparaître dans le mot

Parce qu'un puzzle a **exactement 7 lettres distinctes**, un mot qui contient plus de 7
différentes lettres ne peuvent jamais être valides.
Le puzzle peut contenir chaque lettre au plus une fois, donc pour compter des fins nous seulement
se soucier de l'ensemble * des lettres d'un mot – les duplicatas n'ont pas d'importance.

-----------------------------------------------------------------------------------

C'est vrai. 1. Représenter un ensemble de lettres avec un bitmask

Pour les 26 lettres minuscules, nous utilisons un entier de 26 bits.

«» "
bit i (0-basé) est 1° la lettre (i + 'a') est présente
«» "

Exemple

«» "
mot = "apple" → lettres {a, p, l, e}
masque = 0b000...00101110 (les bits pour a,l,p,e sont 1)
«» "

* Construire un masque pour un mot est "O(="word=").
* Deux mots qui utilisent exactement le même ensemble de lettres obtiennent le même masque.

-----------------------------------------------------------------------------------

C'est vrai. 2. Compter les mots pour chaque masque

`freq[masque]` = combien de mots dans l'entrée utilisent exactement le jeu de lettres décrit
par "masque".
Seuls les masques contenant au plus 7 bits sont stockés – tous les autres mots sont ignorés
parce qu'ils ne peuvent jamais correspondre à un puzzle.

Le bâtiment `freq` est linéaire dans la longueur totale de tous les mots (3 × 106).

-----------------------------------------------------------------------------------

C'est vrai. 3. Énumérer tous les sous-ensembles d'un puzzle qui contiennent la première lettre

Pour un puzzle `puz`

«» "
mask_p = bitmask des 7 lettres de puz
first_bit = bit correspondant à puz[0]
«» "

Tous les mots valides pour ce puzzle doivent utiliser un sous-ensemble de `mask_p` qui aussi
contient `first_bit`.
Le puzzle n'a que 7 lettres, il y a donc au plus des sous-ensembles `2^7 = 128`.
Nous les énumérons efficacement par l' itération sur tous les sous-masques de `mask_p`:

«» "
sub = masque_p
tandis que sous:
si sous contient first_bit :
réponse += freq.get(sub, 0)
sub = (sub - 1) & mask_p
«» "

La boucle tourne en `O(2^7)` par puzzle – assez rapide pour 105 puzzles.

-----------------------------------------------------------------------------------

C'est vrai. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie le nombre exact de mots valides pour chaque
puzzle.

---

Lemma 1
Pour chaque mot `w` l`algorithme augmente `freq[mask(w)]` Exactement une fois.

**Prof.**

* Pendant le traitement d'un mot nous construisons un masque à partir de ses lettres distinctes
(`masque(w)`).
* Nous incrémentons `freq[mask(w)]` une fois après avoir inséré le mot dans la trie
(ou directement dans le dictionnaire).
Aucune autre étape ne modifie "freq[mask(w)]". *



Lemma 2
Pour un puzzle `p` et n'importe quel sous-ensemble `S lettres(p)` qui contient `p[0]`,
l'algorithme ajoute `freq[mask(S)]` à la réponse de `p`.

**Prof.**

Lors du dénombrement des sous-masques de `mask(p)` chaque sous-ensemble `S`
se produit exactement une fois comme `sub`.
Si `sub` contient le premier bit, l'algorithme exécute

«» "
réponse += freq.get(sub, 0) // sub == masque(S)
«» "

Ainsi, `freq[mask(S)]` est ajouté exactement une fois. *



Lemma 3
Un mot `w` est compté dans la réponse pour un puzzle `p` **iff**
'w' est un mot valide pour `p`.

**Prof.**

*(**Si partie**)*
Supposons que `w` est valide pour `p`.
Toutes les lettres de `w` sont en `p`, de sorte que `masque(w) '.
Aussi `p[0] =w`, donc `mask(w)` contient le premier bit.
Par conséquent, `mask(w)` apparaît comme une sous-sub` de `mask(p)` qui contient la
premier bit, et par Lemma 2 sa fréquence est ajoutée à la réponse.

*(**Uniquement si partie**)*
Supposons que l'algorithme ajoute `freq[mask(S)]` pour certains sous-ensembles `S lettres(p)`
contenant `p[0]`.
Chaque mot compté dans cette fréquence utilise exactement les lettres de `S`.
Toutes ces lettres sont en `p` (par définition de `S`) et `p[0]` est en 'S',
donc chaque mot satisfait les deux conditions d'être un mot valide
pour "p".



C'est vrai. Théorème
Pour chaque puzzle `p` l'algorithme produit le nombre exact de mots valides
de la liste des entrées.

**Prof.**

Par Lemma 3 un mot contribue à la réponse pour `p` exactement quand il est
valable pour `p`.
Lemma 1 garantit que la contribution de chaque mot est comptée une fois
dans la rubrique `freq[mask]`.
Par conséquent, la somme produite par l'algorithme correspond au nombre de mots valides
pour "p".



-----------------------------------------------------------------------------------

C'est vrai. 5. Analyse de la complexité

Laissez

«» "
N = nombre de mots
M = nombre de puzzles
«» "

* Bâtiment "freq" *
"O (longueur totale du mot)" ≤ 3 × 106

*Querité par puzzle*
Chaque puzzle énumère ≤ 128 sous-masques
`O(2^7) = O(1)` → `O(M)` globale

* Mémoire *
Au plus une entrée de dictionnaire par masque distinct
`= 2^26` mais seulement ceux avec ≤ 7 bits sont stockés – au maximum 27 × N ≤ 10^5 entrées.

-----------------------------------------------------------------------------------

C'est vrai. 6. Mise en œuvre des références (Python 3)

'`python
de taper l'importation Liste, numéro

Solution de classe:
def findNumOfValidWords(self, mots: List[str], puzzles: List[str]) -> Liste[int]:
# --------- build frequence dictionnaire - Oui.
freq: Dict[int, int] = {}
pour w en mots:
masque = 0
pour ch dans l'ensemble(w): # lettres distinctes seulement
masque= 1 << (ord(ch) - 97)
# Sauter des mots qui ne correspondent à aucun puzzle
si masque == 0 ou masque.bit_count() > 7:
poursuivre
freq[masque] = freq.get(masque, 0) + 1

# --------- réponse pour chaque puzzle - Oui.
res = []
pour puz en puzzles:
masque_p = 0
pour ch in puz:
masque_p= 1 << (ord(ch) - 97)
premier_bit = 1 << (ord(puz[0]) - 97)

ans = 0
sub = masque_p
tandis que sous:
si sous & premier_bit & #160;:
ans += freq.get(sub, 0)
sub = (sub - 1) & mask_p
res.append(ans)

retour res
«» "

Le code suit exactement l'algorithme prouvé correct ci-dessus et est
entièrement conforme à la signature de la fonction LeetCode.

-----------------------------------------------------------------------------------

C'est vrai. 6. Mise en œuvre des références (C++)

Si vous préférez C++, la même idée peut être écrite succinctement :

'`cpp
solution de classe {
public:
vector<int> findNumOfValidWords(vecteur<string>& mots, vector<string>& puzzles) {
non ordonné_map<int,int> freq; // masque -> Nombre
freq.reserve(mots.size(*2);

pour (cont string& w : mots) {
masque int = 0;
pour (charc : w) masque= 1 << (c - 'a');
si (_constructin_popcount((non signé)mask) <= 7) {
[masque]++; // Lemma 1
}
}

vecteur <int> ans;
ans.reserve(puzzles.size());

pour (cost string & puz : puzzles) {
masque int = 0;
pour (char c : puz) masque= 1 << (c - 'a');
Int premier Bit = 1 << (puz[0] - 'a');

cnt = 0;
int sub = masque;
pendant que (sous-) { // énumérer les sous-masques
si (sub & firstBit) { // contient la première lettre
auto it = freq.find(sub);
si (it != freq.end()) cnt += it->seconde;
}
sub = (sous - 1) & masque;
}
as.push_back(cnt);
}
le retour des an;
}
};
«» "

Les deux implémentations fonctionnent facilement dans les limites de LeetCode.