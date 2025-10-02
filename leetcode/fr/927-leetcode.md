---
titre: LeetCode 927. Trois parties égales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 0 327 – Trois parties égales
## Code de Leet – Hard-

---

### TL;DR
Étant donné un tableau binaire, le diviser en **trois parties contiguës non vides** dont les valeurs binaires sont identiques.
Retourner les indices `[i , j]` de telle sorte que

* `arr[0 ... i]` – première partie
* `arr[i+1 ... j-1]` – deuxième partie
* `arr[j ... n-1]` – troisième partie

Si une telle scission n'existe pas, retourner `[-1 , -1]`.
Les zéros de tête sont **autorisés**.

> **Toutes les solutions ci-dessous sont temps O(n), O(1) espace auxiliaire** et sont prêtes à coller dans votre portail LeetCode/Interview.

---

- Oui. 1. Ventilation des problèmes

Le raisonnement
- C'est quoi ?
Autres Le nombre total de 1s** doit être divisible par 3S Chaque partie doit contenir le même nombre de 1S.
Autres Si le tableau contient seulement **=0s**, nous pouvons diviser n'importe où.
Autres Trouvez le **premier index** de chaque partie en sautant le premier `k` 1=1=1 `k = total_ones / 3=1
Autres Le **suffix** du tableau définit la valeur binaire que nous avons besoin de correspondre.

---

- Oui. 2. La solution O(n)

Étapes

1. **Compte 1**
* Si `total_ones % 3 != 0` → impossible → `[-1,-1]`.
2. **Cause zéro**
* Si "total_ones". 0` → retourner `[0, 2]`.
3. **Trouver les positions de départ**
* Scanner de gauche à droite, en gardant un compteur de 1s vu.
* Lorsque le compteur touche `k`, `2k` et `3k`, stocker les indices `start1`, `start2`, `start3`.
4. **Aligner les trois parties**
Alors que les trois indices sont dans les limites ** et** `arr[start1] == arr[start2] == arr[start3]`, avancent les trois simultanément.
* Si une inadéquation survient → impossible.
5. **Vérifier que les pièces ne recouvrent pas* *
* `start1 + len - 1 < start2` et `start2 + len - 1 < start3 "
* `len = n - start3` – longueur du suffixe.
6. **Réponse au retour**
* `i = start1 + len - 1'
* `j = start2 + len`

Pourquoi ça marche ?

* Chaque partie doit avoir la même valeur binaire → la séquence de 1s et les 0s suivants doivent être identiques pour chaque partie.
* En alignant le **suffix** (`start3`) avec les deux parties précédentes, nous garantissons que la valeur est la même.
* Parce que nous passons au-dessus du nombre exact de 1, les pièces sont garanties d'être non-vide et non-overlaping.

---

- Oui. 3. Mise en œuvre du code

### Java

"Java
***
* 3.927 Trois parties égales – Java
* Heure: O(n)= Espace: O(1)
*/
solution de classe publique {
public int[] troisEqualParts(int[] arr) {
int n = longueur de l'arrond;
Int totalOnes = 0;
pour (int v : arr) si (v == 1) total Ones++;

// 1. les totaux doivent être divisibles par 3
si (totalOnes % 3 != 0) retourner la nouvelle int[]{-1, -1};

// 2. tous les cas zéros
si (totalOnes) 0) retourner la nouvelle int[]{0, 2};

les Par part = totalOnes / 3;
int first = -1, second = -1, troisième = -1;
Int vu = 0;
pour (int i = 0; i < n; i++) {
si (arr[i]) 1) {
vu++;
Si (vu) 1) premier = i;
sinon si (voir == lesPerPart + 1) seconde = i;
sinon si (voir == 2 * onesPerPart + 1) troisième = i;
}
}

// 3. aligner les suffixes
int i = premier, j = deuxième, k = troisième;
pendant que (k < n) {
si (arr[i] != arr[j]) arr[j]= arr[k]) retournent une nouvelle int[]{-1, -1};
i++; j++; k++;
}

int len = n - troisième; // longueur du motif
int finFirst = premier + len - 1;
début int Troisième = deuxième + len;

// 4. s'assurer que les étapes ci-dessus ne se chevauchent pas (généralement si elles sont passées)
si (endfirst + 1 < startTroisième) retourne le nouveau int[]{endfirst, démarrez Troisième};
retourner une nouvelle int[]{-1, -1};
}
}
«» "

---

Python

'`python
"""
3.927 Trois parties égales – Python
Heure: O(n)= Espace: O(1)
"""

Solution de classe:
def troisEqualParts(self, arr: list[int]) -> list[int]:
n = len(arr)
total = somme (arr)

# 1. total 1 doit être divisible par 3
si total % 3:
retour [-1, -1]

# 2. tous les zéros
si total == 0:
retour [0, 2]

k = total // 3 # 1's par partie
première = deuxième = troisième = -1
vu = 0
pour i, v in énumérate(arr):
si v:
vu += 1
si vu == 1 :
premier = i
Elif vu == k + 1:
seconde = i
elif vu == 2 * k + 1:
troisième = i

# 3. comparer les trois parties
alors que troisième < n:
si arr[premier] != arr[seconde] ou arr[seconde] != [troisième]:
retour [-1, -1]
premier += 1
deuxième += 1
troisième += 1

part_len = n - troisième # longueur du suffixe
i = première - partie_len # fin de première partie
j = deuxième - partie_len # début de la troisième partie

retour [i, j]
«» "

---

C++

'`cpp
***
* 3.927 Trois parties égales – C++
* Heure: O(n)= Espace: O(1)
*/
solution de classe {
public:
vecteur<int> troisEqualParts(vecteur<int>& arr) {
int n = arr.size();
int total = accumuler(arr.begin(), arr.end(), 0);
si (total % 3 != 0) retourner {-1, -1};
si (total) 0) retour {0, 2};

int k = total / 3;
int first = -1, second = -1, troisième = -1;
Int vu = 0;
pour (int i = 0; i < n; ++i) {
si (arr[i]) 1) {
++vus;
Si (vu) 1) premier = i;
sinon si (voir == k + 1) seconde = i;
sinon si (voir == 2 * k + 1) troisième = i;
}
}

// Alignez les trois parties
int i = premier, j = deuxième, kIdx = troisième;
pendant que (kIdx < n) {
si (arr[i] != arr[j]) arr[j]= arr[kIdx]) retourne {-1, -1};
++i; ++j; ++kIdx;
}

partie intLen = n - troisième;
Int finFirst = first + partLen - 1;
début int Troisième = deuxième + partie Len;

si (endfirst + 1 < startTroisième) retour {endfirst, startTroisième};
retour {-1, -1};
}
};
«» "

---

- Oui. 4. Article de blog – Le bon, le mauvais, et l'indulgence de LeetCode 927

> **Titre**
> * Trois parties égales – le bon, le mauvais et le mauvais (Java, Python, C++)*

> **Méta-description* *
> Master LeetCode 927 en quelques minutes. Lisez la solution complète, comprenez les pièges et obtenez une réponse prête à l'emploi. Comprend Java, Python, code C++.

> **Mots clés**
> `Three Equal Parts Leetcode`, `Java solution`, `Python solution`, `C++ solution`, `biary array split`, `job interview coding`, `binary number comparison`, `O(n) algorithme`, `array partitioning "

---

C'est pas vrai. Le bon : pourquoi ce problème se complique

* **Vibe réelle** – Pensez aux paquets de données qui doivent être divisés en segments égaux.
* **Défi algorithmique pur** – Pas de maths lourds, juste une manipulation astucieuse.
* **Test d'entrevue parfait** – Montrez votre compréhension de *array traversal*, *edge case* et *time-space compromis*.

- Oui. Les mauvaises: pièges communs

Pourquoi ça casse
C'est-à-dire
La valeur binaire de `[0,1]` est la même que `[1,1]`. Autres
*En supposant que n'importe quelle fraction fonctionne lorsque tous les zéros * , vous devez toujours retourner `[0,2]` – la réponse la plus simple valide. Autres
*L'utilisation d'une carte de hachage des préfixes *= O(n) espace pour un problème qui peut être fait en O(1). Autres
*Vérifier seulement le nombre de 1=s*= Deux tableaux peuvent avoir le même nombre de 1 mais un modèle différent. Autres

C'est vrai. L'horrible : les cas de bords cachés

1. **Tous les zéros** – Votre algorithme doit toujours retourner une fraction valide.
2. **Trainer des zéros après la dernière partie** – Ils doivent être comptés dans l'alignement suffisant.
3. **Les tableaux très courts** – Par exemple, `[1,0,1]` → impossible.
4. **Grandes entrées** – `arr.length=30000` – assurez-vous que vous ne *pas* créer des tableaux supplémentaires ou utiliser la récursion.

---

- Oui. 5. SEO-optimisé rapide- Démarrer la feuille de chaleur

Code de démarrage rapide
Il y a un problème.
{/* code */ }\n``" Autres
**Python** Solution:\n def troisEqualParts(self, arr: List[int]) -> Liste[int]:\n # code\n`` Autres
*C++ * * ``cpp\nclass Solution {\npublic:\n vector<int> troisEqualParts(vecteur<int>& arr) {\n // code\n }\n};\n`` Autres

**Astuce:** Lorsque vous collez dans LeetCode, remplacez simplement le squelette par le code ci-dessus et exécutez.

---

- Oui. 6. Pensées finales

* ** Pratique** – Exécutez le code avec des tableaux aléatoires pour voir les cas de bord en action.
* **Explain** – Dans les entrevues, passer en revue *totales*, *indices de départ*, *alignement suffixe*, *non-overlap*.
* **Portfolio** – Ajouter cette solution à votre repo GitHub, la marquer avec `#LeetCode927`. Les recruteurs adorent voir un code propre et bien commenté.

> * Prêt à atterrir cette prochaine entrevue de codage?* C'est ce qu'il a dit.
> Déposez la solution dans votre IDE, testez-la et expliquez la logique – vous êtes tous ensemble !

---

* Bon codage et bonne chance ! *

---

> **Auteur** – Codage Interview Ninja
> **Suivez** pour plus d'informations LeetCode: LinkedIn, Twitter, Medium
> **S'abonner** à notre bulletin d'information : plan de préparation d'entrevue de 30 jours.

---

Fin de l'article

---

Avec cet article, les lecteurs apprennent non seulement l'algorithme, mais comprennent aussi *pourquoi* il vaut la peine d'interviewer, ce qui renforce la confiance et la performance d'entrevues – clé pour obtenir ce rôle d'ingénierie logicielle de rêve.