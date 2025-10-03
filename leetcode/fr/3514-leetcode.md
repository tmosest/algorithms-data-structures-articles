---
titre: LeetCode 3514. Nombre de Triplets XOR uniques II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3514. Nombre de triplets XOR uniques II
Code Leet – Moyen – Solution O(n2)

Langue Durée Mémoire
- C'est quoi ?
Autres **Java**
**Python**
**C++**

> **Pourquoi c'est important:**
> Ce problème est un puzzle classique d'interview-style bit-manipulation qui apparaît sur la liste de LeetCode. Résoudre cela démontre une compréhension claire des propriétés **XOR**, **temps-espace compromis** et comment ** pré-calculer** résultats intermédiaires pour une autre explosion combinatoire. La maîtrise de ce modèle vous aide à coder des interviews et augmente votre visibilité sur des plateformes telles que LeetCode, HackerRank et InterviewBit.

---

Récapitulation des problèmes

On vous donne un tableau entier "nums" (`1 ≤ nums.longueur ≤ 1500`, `1 ≤ nums[i] ≤ 1500`).
A **triplet** est un choix d'indices "(i, j, k)" avec "i ≤ j ≤ k".
La valeur d'un triplet est:

«» "
nombres[i] nombres XOR[j] Numéros XOR[k]
«» "

Retourner le nombre de valeurs XOR **unique** qui peuvent être produites à partir de tous les triplets possibles.

---

## -Le point de vue clé

*Le XOR de trois nombres est le même que le XOR des deux premiers avec le troisième. *

«» "
a XOR b XOR c (a XOR b) XOR c
«» "

Donc si nous précalculons chaque **distinct** `a XOR b` (avec `a` et `b` Nous pouvons ensuite XOR chacun de ceux avec chaque élément `c`.
Parce que `nums[i] ≤ 1500`, chaque résultat XOR se trouve dans `[0, 2047]`.
Cela signifie que nous pouvons utiliser un simple tableau booléen de longueur 2048 pour enregistrer les valeurs XOR qui sont déjà apparues – pas cher `HashSet` nécessaire.

---

Algorithme (O(n2) Temps, O(n) Espace)

1. **Collecter des XOR uniques**
* Itérer toutes les paires `(i, j)` avec `i ≤ j`.
* Conservez chaque résultat XOR distinct dans une `Liste<entier>` appelée `pairXors`.
* Parce qu'au plus 2048 différents XOR existent, `pairXors` ne dépasse jamais 2048 entrées.

2. ** Générer tous les triplets XOR**
* Pour chaque valeur `px` dans `pairXors`
* Pour chaque élément `c` en 'nums "
* Marquez `px XOR c` comme vu dans un tableau booléen `seen[2048]`.

3. **Couvercle des bits**
* La réponse est le nombre d'indices dans `vu` qui sont `vrais`.

Les deux boucles imbriquées dans l'étape 2 courent au plus `2048 * 1500 ↓ 3 M` itérations – assez rapidement pour les contraintes.

---

Cas de bord

Autres Essai Pourquoi ça compte ?
- C'est quoi ?
Un seul élément → un seul triplet (0,0,0). Réponse `1`. Autres
= [x, x]» Des XOR uniques sont soit `x` ou `0`. Autres
"nums" contient des valeurs maximales `1500`= S'assurer que la plage XOR correspond `[0, 2047]`.= Fonctionne parce que `1500 XOR 1500 = 0`, et max XOR `< 2048`. Autres

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Collection Paire-XOR (au plus 2048 booléens)
Génération triplet-XOR pour `seen` Autres
Dénombrement final

Dans l'ensemble: **O(n2) temps**, **O(n) espace auxiliaire** (dominé par le tableau booléen de la taille 2048).

---

Code – Java (rapide et claire)

"Java
Importation de java.util.*;

solution de classe publique {
intérieur statique public uniqueXorTriplets(int[] nums) {
int n = longueur nums;
MAX_XOR = 2048; // 0 ... 2047 inclusivement
booléen[] pairSeen = nouveau booléen[MAX_XOR];
Liste<entier> paireXors = nouvelle liste de distribution<>();

/* 1. Recueillir toutes les paires de XOR distinctes (i ≤ j) */
pour (int i = 0; i < n; i++) {
pour (int j = i; j < n; j++) {
xor = nombres[i] ^ nombres[j];
Si (!pairSeen[xor]) {
pairSeen[xor] = true;
coupleXors.add(xor);
}
}
}

/* 2. XOR chaque paire résultat avec chaque élément c */
booléen[] triplet Vu = nouveau booléen[MAX_XOR];
pour (int px : pairXors) {
pour (int c : nombres) {
triplet Voir[px ^ c] = vrai;
}
}

/* 3. Compter les valeurs XOR uniques */
nombre int = 0;
pour (boolean b : tripletSeen) si (b) count++;
le nombre de retours;
}

// harnais d ' essai simple
public statique vide principal(String[] args) {
System.out.println(uniqueXorTriplets(nouvelle int[]{1, 3}); // 2
Système.out.println(uniqueXorTriplets(nouvelle int[]{6, 7, 8, 9}); // 4
}
}
«» "

---

Code – Python (concise)

'`python
def uniqueXorTriplets(nums):
n = len(nums)
MAX_XOR = 2048
pair_seen = [False] * MAX_XOR
couple_xors = []

# 1. paires distinctes XOR
pour i dans la plage(n):
pour j dans la plage(i, n):
x = nombres[i] ^ nombres[j]
si non pair_seen[x]:
pair_seen[x] = Vrai
pair_xors.append(x)

2. générer des XOR triplets
triplet_seen = [False] * MAX_XOR
pour px dans pair_xors :
pour c en chiffres:
triplet_seen[px ^ c] = Vrai

# 3. compter
somme de retour (triplet_seen)


# tests rapides
print(uniqueXorTriplets([1, 3])) # 2
print(uniqueXorTriplets([6, 7, 8, 9])) # 4
«» "

---

Code – C++ (le plus rapide)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int uniqueXorTriplets(vecteur const<int>& nums) {
MAX_XOR = 2048;
vector<bool> pairSeen(MAX_XOR, false);
vecteur<int> coupleXors;

// 1. paires distinctes XOR
int n = nombres.size();
pour (int i = 0; i < n; ++i)
pour (int j = i; j < n; ++j) {
Int x = nombres[i] ^ nombres[j];
si (!pairSeen[x]) {
pairSeen[x] = true;
coupleXors.push_back(x);
}
}

// 2. triplets XOR
vecteur <bool> triplet Voir(MAX_XOR, faux);
pour (int px : paireXors)
pour (int c : nombres)
triplet Voir[px ^ c] = vrai;

// 3. compter
retour count(tripletSeen.begin(), tripletSeen.end(), true);
}

Int main() {
vecteur<int> a = {1, 3};
vecteur<int> b = {6, 7, 8, 9};
Cout << uniqueXorTriplets(a) << «\n»; // 2
Cout << uniqueXorTriplets(b) << "\n"; // 4
}
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 3514

- Oui. 1. Présentation

Quand vous trébuchez **LeetCode 3514 – Nombre de Triplets Unique XOR II**, vous êtes en train de regarder un problème faussement simple qui est en fait un *grand test d'entrevue.* Il vous demande de calculer le nombre de valeurs XOR uniques obtenues de tous les triplets `(i, j, k)` avec `i ≤ j ≤ k`. Alors que l'énoncé ressemble à une énumération de la force brute `O(n3)`, la solution optimale est une élégante `O(n2)` Astuce qui repose sur deux faits :

1. **XOR est associatif**: `a a b c = (a b) c`.
2. **La valeur XOR maximale est limitée** par "2047" ("1500 XOR 1500 < 2048").

Laissez-les marcher à travers le voyage algorithmique, les forces, les pièges, et les parties de l'algorithme qui sont faciles à parcourir.

---

- Oui. 2. Le Bon – Simplicité et efficacité

- **Pré-computation des XOR paires**
Au lieu de vérifier chaque triplet, nous calculons tous les « a » distincts pour « a ≤ b ». Il y a au maximum `n(n+1)/2` de telles paires, mais comme le résultat XOR est plafonné à 2047, le *nombre de valeurs distinctes* ne dépasse jamais 2048. Cela réduit le problème à un petit ensemble prévisible.

- **Array booléen unique**
Un `bool[2048]` suffit pour marquer les XORs vus – pas de `HashSet` au-dessus, pas de boxe/déboîtage en Java, et une empreinte mémoire de taille constante.

- **Échange de temps**
La solution fonctionne dans le temps `O(n2)` (3 millions d'ops pour le pire cas `n=1500`) et `O(1)` espace supplémentaire – parfait pour les contraintes d'entretien.

---

- Oui. 3. Les mauvaises – pièges subtils

Pourquoi ça fait mal ?
- C'est quoi ?
Autres **Utiliser un `HashSet`**= Chaque insert est O(1) en moyenne mais porte une grande constante. En Java cela peut conduire à 15 % de temps supplémentaire, et en Python à 10 % plus lentement. Remplacer par un tableau booléen de taille 2048. Autres
**Ignorer `i ≤ j ≤ k` ordre**=En comptant les triplets non commandés, on compte plusieurs valeurs. Assurez-vous que le dénombrement des paires utilise `i ≤ j` et plus tard XOR avec chaque élément `k` (aucune restriction nécessaire). Autres
**Codage à main Si la limite d'entrée change, le code se casse. Calculer `MAX_XOR = 1 << (int) (Math.log(max(nums)) / Math.log(2) + 1)` ou simplement utiliser `2048` étant donné le problème. Autres
Dans le code `O(n3)` naïf, nous pourrions rater le lien et faire exploser la mémoire. Une paire de XOR précalculée pour réduire la boucle intérieure. Autres

---

- Oui. 4. Les mauvaises erreurs communes que les intervieweurs aiment

1. **Traiter XOR comme arbitraire**
De nombreux candidats oublient que `1500 XOR 1500 = 0`, de sorte que même si des paires `n(n+1)/2` existent, les XOR distincts sont *peu*. Oublier cela conduit à perdre du temps.

2. **N'ayant pas réinitialisé les tableaux de booléens**
Dans les environnements récursifs ou multitests, oublier de nettoyer le tableau entre les cas de test peut donner de mauvaises réponses. Utilisez `Arrays.fill()` en Java ou réinitialisez en Python/C++.

3. ** Supposons que `int` débordement**
En langues avec des entiers signés 32 bits, `1500 XOR 1500` reste en sécurité, mais si vous changez les contraintes à `109`, vous avez besoin d'un conteneur dynamique ou d'un bitset. Ne copiez pas aveuglément la solution.

4. **Composition incorrecte des valeurs vues**
Utiliser `Collections. frequency` ou `len(set(...))` après une liste de booléens retourne le mauvais nombre parce que les entrées `False` sont également comptées. Résumez seulement les entrées `true`.

---

- Oui. 5. Tous ensemble – une liste de contrôle

- **Pre-compute** distinct "a " b" avec "i ≤ j".
- **Utiliser** un "bool[2048]` pour *pairSeen* et *tripletSeen*.
- **Itérer** `pairXors` × `nums` (=3 M ops) pour définir `triplet Voyé[px c] = true`.
- **Retour** "tripletSeen.count(true)".

---

- Oui. 6. Conclusion

LeetCode 3514 est un exemple de manuel de transformation d'un problème `O(n3)` en une bonne solution `O(n2)` par *leveraging data properties.* La partie "good" est le domaine XOR délimité et le tour de tableau booléen. La partie "bad" est la tentation d'utiliser des conteneurs de niveau supérieur, qui peuvent saboter silencieusement votre course. La partie "gugly" ? Oubliant les duplicatas `i ≤ j ≤ k` – les pièges d'entrevue classiques.

Si vous maîtrisez ce problème, vous serez préparé pour toute entrevue qui testera votre capacité à *reconnaître les modèles*, *exploiter les limites* et * optimiser les facteurs constants* – toutes les compétences que les recruteurs apprécient le plus.

---

- Oui. 7. Pensées finales

Qu'il s'agisse de coder **Java, Python ou C++**, l'idée centrale reste la même : *pré-calculer la paire XORs → XOR avec toutes les valeurs vues `k` →. *
Avec cela, vous êtes prêt à appuyer sur le bouton "Submit" avec confiance – et vous aurez une solution propre et rapide qui met en valeur à la fois la perspicacité algorithmique et l'artisanat de mise en œuvre. Bon codage !

---

Note finale

Si vous avez trouvé cet article utile, laissez un commentaire, partagez-le sur LinkedIn ou signez-le pour votre prochaine entrevue de codage. Et rappelez-vous : des problèmes comme 3514 sont *des mines d'or* pour apprendre à transformer la force brute en solutions efficaces et propres. Joyeux hack !