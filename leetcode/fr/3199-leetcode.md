---
titre: LeetCode 3199. Comptez les Triplets avec même les bits XOR Set Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# 3199 – Comptez les Triplettes avec même des bits XOR Set
**Java-Optimized Blog Post**

---

- Oui. 1. Récapitulation des problèmes

Avec trois tableaux entiers `a`, `b` et `c` (chaque longueur 1 ... 100, valeurs 0 ... 100), compter le nombre de triplets
`a[i], b[j], c[k]` de telle sorte que le **bitwise XOR** des trois nombres contient un **même nombre de bits** (c'est-à-dire un poids de Hamming).

> Exemple
> `a=[1]`, `b=[2]`, `c=[3]` → `1=2=3=0` (0 set bits → even) → response = 1.

---

- Oui. 2. Observations et idées optimisées

Observation Pourquoi ça compte
C'est-à-dire
Autres La parité (even/odd) d'un nombre est **additive modulo 2** sous XOR. Autres Si nous ne nous intéressons qu'à la parité, nous pouvons traiter chaque nombre comme un nombre égal ou un nombre égal et oublier la valeur exacte. Autres
Autres Pour trois nombres, la parité XOR est même si **soit** (i) les trois sont **ou** (ii) exactement deux sont bizarres. Ce sont les seules façons d'obtenir un résultat uniforme. Autres
Autres Nous n'avons besoin que de **quatre nombres**: nombre d'éléments de parité dans chaque tableau. Une fois que nous en aurons, nous pourrons calculer tous les triplets valides combinatoirement. Autres

Ainsi l'algorithme est **O(n)** avec **O(1)** mémoire supplémentaire – parfait pour les contraintes.

---

- Oui. 3. Code en 3 langues

> *Les trois implémentations utilisent la même logique : compter la parité pair/odd et multiplier les combinaisons pertinentes. *

#### 3.1 Java

"Java
// 3199. Comptez les triplets avec même les bits XOR Set – Java Implementation
solution de classe publique {
Int public tripletCount(int[] a, int[] b, int[] c) {
int[] evens = nouveau int[3];
int[] probabilités = nouvelle int[3];

// Compter la parité pair/odd par tableau
evens[0] = nombreEvenParity(a);
evens[1] = nombreEvenParity(b);
evens[2] = nombreEvenParity(c);

probabilités[0] = longueur - paires[0];
cotes[1] = longueur b. - paires[1];
les cotes[2] = c.longueur - paires[2];

long total = 0L;

// Tous les trois même
total += (long) paires[0] * paires[1] * paires[2];

// Exactement deux chances
total += (long) cotes[0] * cotes[1] * paires[2]; // impair, impair, pair
total += (long) cotes[0] * paires[1] * cotes[2]; // impair, pair, impair
total += (long) paires[0] * cotes[1] * cotes[2]; // pair, impair, impair

retour (int) total; // résultat correspond à int (<= 1 000 000)
}

// Compter les nombres en arr avec un nombre pair de bits
Compte d'entrée privéEvenParity(int[] arr) {
même Cnt = 0;
pour (int num : arr) {
si [Integer.bitCount(num) % 2] 0) {
evenCnt++;
}
}
même retour Cnt;
}
}
«» "

3.2 Python

'`python
# 3199. Comptez les Triplets avec même les bits XOR – Implémentation Python
def triplet_count(a: list[int], b: list[int], c: list[int]) -> Int:
# Helper : comptez les numéros de parité dans une liste
def even_parity_count(arr: list[int]) -> Int:
retour sum(1 pour x in arr si bin(x).count('1') % 2 == 0)

evens = [even_parity_count(a), even_parity_count(b), even_parity_count(c)]
cotes = [len(a) - paires[0], len(b) - paires[1], len(c) - paires[2]]

Total = 0
# Tous les trois même
total += paires[0] * paires[1] * paires[2]
# exactement deux chances
Total += cotes[0] * cotes[1] * paires[2]
Total += cotes[0] * paires[1] * cotes[2]
total += paires[0] * cotes[1] * cotes[2]
retour total
«» "

> *Si vous êtes sur Python 3.10+, vous pouvez remplacer `bin(x).count('1')` par `x.bit_count()` pour la vitesse. *

### 3.3 C++

'`cpp
// 3199. Comptez les Triplets avec même des bits XOR – C++ Mise en œuvre
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int tripletCount(vecteur<int> const &a, vecteur<int> Const &b, vecteur<int> const &c) {
Auto evenParityCount = [](vecteur<int> const &arr) -> Int {
cnt = 0;
pour (int x : arr)
si (_constructin_popcount(x) % 2 == 0) + cnt;
retour cnt;
};

evenA = evenParityCount(a), evenB = evenParityCount(b), evenC = evenParityCount(c);
int impairA = (int)a.size() - evenA;
int impairB = (int)b.size() - evenB;
int impairC = (int)c.size() - evenC;

long total = 0;
+= 1LL * evenA * evenB * evenC; // tous même
total += 1LL * impairA * impairB * evenC; // impair, impair, pair
Total += 1LL * impairA * evenB * impairC; // impair, pair, impair
Total += 1LL * evenA * impairB * impairC; // even, impair, impair

retour (int)total; // réponse ≤ 1 000 000
}
«» "

---

- Oui. 4. Article de blog – Le bon, le mauvais, et l'acharnement de compter les triples avec même des bits de XOR

> **Référencement:**
> *=Count Triplets avec même des bits XOR – Solutions Java, Python & C++

4.1 Introduction

Les LeetCodes **3199 – Compte Triplets avec Even XOR Set Bits** est un problème de simplicité trompeuse qui cache une torsion subtile: *vous avez seulement besoin de la parité du poids de Hamming*, pas le résultat exact XOR. Pour les intervieweurs, il teste votre compréhension des propriétés bitwise et du comptage combinatoire. Pour vous, c'est une excellente occasion de présenter un code propre et optimisé dans plusieurs langues.

Dans cet article, nous allons passer par:

1. **Le Bon** – Pourquoi l'approche de parité seulement est élégante et rapide.
2. **Le mauvais** – Pièges communs (boucles de force, débordement, compte erroné).
3. **L'Ugly** – Cas de bord qui voyagent jusqu'à des codeurs assaisonnés.

Nous avons terminé avec une implémentation polie, prête à la production en Java, Python et C++, prête à coller dans votre portfolio ou GitHub README.

> *Mots clés:* Comptez Triplets avec Even XOR Set Bits, LeetCode 3199, bitwise XOR, même set bits, entretien de codage, solution Java, solution Python, solution C++, optimisation des algorithmes, préparation d'entretien d'emploi.

#### 4.2 Le Bon – Une Parité- Seulement délice

Autres Ce que vous obtenez Pourquoi ça compte
C'est pas vrai.
**O(n)** time (temps) Avec des tableaux plafonnés à 100, la force brute serait encore bonne, mais la parité réduit considérablement les facteurs constants. Autres
**O(1)** espace. Autres
**Logique claire**.Tous les mêmes + exactement deux impairs sont les seuls modèles de parité valides. Ces cartes à quelques multiplications. Autres
La même idée fonctionne dans n'importe quelle langue qui peut compter les bits (Java `Integer.bitCount`, Python `int.bit_count` ou `bin().count('1')`, C++ `_builtin_popcount`). Autres

> * À emporter :* Pensez en termes de **parité** d'abord. Pour de nombreuses questions d'entrevue, cela peut transformer un problème cubique en un problème linéaire.

4.3 Les mauvaises – erreurs courantes

Erreurs dans les résultats
- C'est quoi ?
**Brute-force 3-loop** XOR ops → toujours ok, mais inutile dans les tests plus grands. La parité précalculée compte et se multiplie. Autres
**Utiliser `int` pour la réponse sans dispositif de protection de débordement**= Si les tableaux étaient plus grands, le produit pourrait dépasser 231‐1.=Utiliser `long long` (C++), `long` (Java) ou `int` mais avec un contrôle explicite. Autres
**Counting set bits incorrectement** Utilisez la langue-native popcount (`Integer.bitCount`, `_builtin_popcount`, `int.bit_count`). Autres
**Échec à une erreur dans la longueur du tableau** Calculer explicitement "odd = len - even". Autres
**En supposant que `0` a un nombre impair de bits de jeu** Laissez la fonction bitcount la gérer; aucun cas particulier n'est nécessaire. Autres

4.4 Les cas les plus odieux – les cas de bord qui ont mordu

Pourquoi ça compte ?
- C'est quoi ?
**Tous les zéros** L'algorithme compte naturellement tous les nombres égaux, de sorte que `evenA*evenB*evenC` le couvre. Autres
**Parité mixte mais pas de combinaison valide**= Si chaque tableau n'a qu'un seul type de parité, par exemple, tout même, vous obtenez toujours des triplets valides (`even+even+even`). Le terme « even » garantit que ce cas est couvert. Autres
**Grand produit dépassant `int`**.Pas un problème ici mais une bonne pratique pour utiliser des temporaires 64 bits. Multipliez par `long`/`long`. Autres
**Utiliser Python="s `int` (non consolidé)**= Pas de problème de débordement, mais l'algorithme reste O(1) mémoire supplémentaire. Utiliser `int` retour; Python gérera les grands entiers automatiquement. Autres
**Types d'entrées non standard (chaînes, flotteurs)**=LeetCode utilise strictement des entiers, mais dans les projets réels vous pouvez obtenir d'autres types numériques. Conversion en type `int` ou `int`-compatible avant popcount. Autres

> * Conseil professionnel :* Ajouter un "assert" rapide ou des tests unitaires qui vérifient le nombre total de triplets égale `len(a)*len(b)*len(c)` lorsque tous les nombres sont nuls.

4.5 Mise en œuvre de la production

Nous avons déjà montré trois solutions propres. Ci-dessous nous soulignons pourquoi ils sont prêts pour la production:

- **Minimal ramification** – bitcount est une ligne; pas de boucles à l'intérieur des boucles.
- **Noms de variables clairs** – `evenA`, `oddB` rendent l'intention évidente.
- **Promotion de type explicite** – `1LL *` assure l'arithmétique 64 bits avant la troncation.
- **Aucune dépendance externe** – Tous les appels de bibliothèque standard.

N'hésitez pas à copier l'extrait de texte qui correspond à votre langue préférée dans un README, ou à l'engager dans une repo de codage-pratique. Ajouter une section `# TODO` pour vos optimisations futures (par exemple, le traitement parallèle) et vous aurez un excellent point de conversation d'entretien.

### 4.6 Conclusion

LeetCode 3199 peut être marqué "Easy", mais son idée fondamentale – réduire le problème à la parité et à la combinatoire – est un modèle puissant qui apparaît dans de nombreuses questions d'entrevue bit-wise. En spotant le "good" , en évitant le "bad" , et en manipulant le "ugly" , vous pouvez produire un code propre et efficace qui impressionne les intervieweurs et renforce votre portefeuille.

**Vous souhaitez plus de solutions LeetCode?** Découvrez le dépôt lié dans cet article, où chaque problème est résolu en Java, Python et C++, avec des commentaires et des notes de complexité.

> *Note finale:* L'algorithme que nous avons implémenté est une seule ligne** de mathématiques une fois que vous avez les comptes. C'est le genre de perspicacité que les intervieweurs aiment voir.

4.7 Appel à l'action

Si vous préparez votre prochain entretien d'embauche :

- ** Pratique** le tour de parité sur d'autres problèmes XOR.
- **Ajouter ces extraits** à votre profil GitHub (inclure un README avec l'énoncé du problème).
- **Partager** l'article sur LinkedIn avec les tags "LeetCode 3199" et "Coding interview".

Bonne chance – et que vos triplets toujours XOR à pair!

---

> *Tous les extraits de code sont disponibles sous la licence MIT de l'auteur. *

---

- Oui. 5. Résumé

- Oui. Nous avons découvert que **parité seule** suffit à résoudre efficacement LeetCode 3199.
- Fourniture d'implémentations propres et inter-langues.
- Proposé un article de blog détaillé pour vous aider à vous préparer aux entrevues et mettre en valeur vos compétences.

Bon codage, et bonne chance pour votre prochaine interview!