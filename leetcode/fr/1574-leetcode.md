---
Titre: LeetCode 1574. Subarray le plus court à supprimer pour faire trier -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1574 – La Subarray la plus courte à supprimer pour faire trier

> *Problème*: Avec un tableau entier `arr`, supprimer une sous-tribuon contigu (peut être vide) de sorte que les éléments restants soient en ordre non décroissant. Retournez la longueur du sous-aire le plus court qui peut être enlevé.

Difficulté Moyen Contraintes
- Oui.
1 ≤ longueur de l'arrondi ≤ 105,0 ≤ arr[i] ≤ 109,0
Heure O(n) O(1) espace supplémentaire

Vous trouverez ci-dessous des solutions prêtes à la production dans **Java**, **Python** et **C++**.
Après le code, nous plongerons dans un article de blog complet qui explique le *bon, le mauvais et le laid* de ce problème – idéal pour polir vos notes d'entrevue ou écrire un article à la recherche d'emploi.

---

Solution Java

"Java
Importation de java.util.*;

solution de classe {
public int findLength OfShortestSubarray(int[] arr) {
int n = longueur de l'arrond;
Préfixe le plus long non décroissant
Int gauche = 0;
alors que (gauche + 1 < n && arr[gauche] <= arr[gauche + 1]) gauche++;

// Le tableau est déjà trié
si (à gauche) n - 1) retourner 0;

Le plus long suffixe non décroissant
int droite = n - 1;
(droite > 0 && arr[droite - 1] <= arr[droite]) droit--;

Commencez par les deux candidats évidents
int ans = Math.min(n - gauche - 1, droite);

2-pointer fusionner: conserver la partie préfixe de la longueur i,
// garder suffixe à partir de j, et vérifier l'écart
int i = 0, j = droite;
pendant que (i <= gauche && j < n) {
si (arr[i] <= arr[j]) { // peut conserver arr[i] et arr[j]
ans = Math.min(ans, j - i - 1); // supprimer milieu
i++; // essayer un préfixe plus long
} autre { // besoin de déplacer suffixe pointeur
j++;
}
}
le retour des an;
}
}
«» "

> **Complexité**:
> • Temps – **O(n)** (trois scans linéaires)
> • Espace – **O(1)**

---

2. Solution Python

'`python
de taper l'importation Liste

Solution de classe:
def findLengthOfShortestSubarray(self, arr: List[int]) -> Int:
n = len(arr)

# Préfixe non décroissant le plus long
gauche = 0
à gauche + 1 < n et arr[gauche] <= arr[gauche + 1]:
gauche += 1
Si gauche == n - 1: # déjà trié
retour 0

# Le plus long suffixe non décroissant
droite = n - 1
alors que droit > 0 et arr[droit - 1] <= arr[droit]:
droite -= 1

ans = min(n - gauche - 1, droite) # deux suppressions triviales

i, j = 0, à droite
alors que i <= gauche et j < n:
si arr[i] <= arr[j]:
ans = min(ans, j - i - 1)
i += 1
Sinon:
j += 1
retour et
«» "

> **Complexité**
> • Temps – **O(n)**
> • Espace – **O(1)**

---

3. Solution C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int findLengthOfShortestSubarray(vector<int>& arr) {
int n = arr.size();
// Préfixe non décroissant le plus long
Int gauche = 0;
alors que (gauche + 1 < n && arr[gauche] <= arr[gauche + 1]) gauche++;

si (gauche == n - 1) retourner 0; // déjà trié

// Le plus long suffixe non décroissant
int droite = n - 1;
(droite > 0 && arr[droite - 1] <= arr[droite]) droit--;

int ans = min(n - gauche - 1, droite); // deux suppressions simples

// Fusion de deux points
int i = 0, j = droite;
pendant que (i <= gauche && j < n) {
si (arr[i] <= arr[j]) {
ans = min(ans, j - i - 1);
++i;
} autre {
++j;
}
}
le retour des an;
}
};
«» "

> **Complexité**
> • Temps – **O(n)**
> • Espace – **O(1)**

---

4. Article du blog – Le bon, le mauvais et le mauvais de LeetCode 1574

> **Titre**: *Le bon, le mauvais et le mauvais de LeetCode 1574 – Subarray le plus court à enlever pour faire trier*
> **Meta Description**: Master LeetCode 1574 avec une plongée profonde dans sa solution optimale, pièges, et l'explication prête à l'entrevue. Idéal pour les ingénieurs logiciels qui cherchent à impressionner les gestionnaires d'embauche.

---

Introduction

Lorsque les recruteurs vérifient la netteté algorithmique, ils vous donnent souvent des problèmes qui *regardent* facilement mais cachent des pièges cachés. **LeetCode 1574** est l'un de ces problèmes : *Supprimer un sous-appel pour que le reste du tableau ne diminue pas.* Sur la surface, on sent comme une simple question "supprimer le plus grand mauvais segment", mais la solution optimale repose sur une fusion à deux pointeurs et une manipulation soigneuse des cas de bord.

Dans cet article, nous allons:

- Expliquer pourquoi une approche naïve échoue
- Afficher la solution optimale **O(n)** en 3 langues
- Discutez des bons, des mauvais et des laids du point de vue de l'interview
- Fournir des conseils d'entrevue que vous pouvez mentionner au téléphone

---

- Oui. Le problème en anglais clair

Vous êtes donné un tableau entier `arr`. Vous pouvez supprimer *un* sub-array contigu (les éléments que vous supprimez ne doivent pas être contigus dans le tableau final, ils sont simplement supprimés). Après la suppression, les éléments restants doivent être triés en ordre non décroissant**.

Votre tâche : retourner le nombre minimum d'éléments ** que vous devez supprimer.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Supprimer `[10, 4, 2]` → `[1, 2, 3, 3, 5]`. Autres
`[5, 4, 3, 2, 1] ́ ́ ́ ́ ́ ́ ` ` ` Le tableau est en train de décroître; conservez n'importe quel élément. Autres
"[1, 2, 3]" "0" Déjà trié. Autres

---

C'est vrai. Pourquoi les solutions naïves luttent

Une première pensée commune: *=Trouver le plus long préfixe trié et suffixe, puis supprimer tout entre les deux.
Cela vous donne une réponse de `droite - gauche - 1`, mais ce n'est pas toujours optimal. Par exemple:

«» "
[1, 3, 5, 2, 4, 6]
«» "

- Préfixe le plus long: `[1, 3, 5]`
- Le suffixe le plus long: `[2, 4, 6]`
- Supprimer le milieu → `3` éléments supprimés.

Mais en fait nous pouvons supprimer `[5, 2]` (2 éléments) et avoir toujours `[1, 3, 4, 6]` trié.
Le défaut est que nous ** devons garder au moins un élément du suffixe** qui *fit* après le préfixe.

Une autre idée naïve : essayer toutes les suppressions possibles via deux boucles imbriquées (« O(n2) »), qui seront time-out pour « n = 105 ».

Nous avons donc besoin d'un algorithme **O(n)** qui fusionne intelligemment le préfixe et le suffixe tout en respectant la contrainte de commande.

---

#### 4=" La stratégie O(n) optimale – Fusion à deux points

1. **Identifiez le préfixe le plus long non déclenchant**
Scanner de gauche à `arr[i] > arr[i+1]`. Que cet indice soit "gauche".

2. **Identifiez le suffixe le plus long non déclenchant**
Scanner de droite jusqu'à `arr[j-1] > arr[j]`. Que cet indice soit "juste".

3. **Si le tableau entier est déjà trié** (`gauche == n-1`), la réponse est `0`.

4. **Initialiser la réponse** avec deux candidats évidents :
- Supprimer tout après le préfixe → `n - gauche - 1`
- Supprimer tout avant le suffixe → `right`

4. **Merge avec deux pointeurs**
- Définir `i = 0`, `j = droite`.
- Alors que `i <= gauche` et `j < n`:
- Si `arr[i] <= arr[j]` Tu peux garder les deux.
*Supprimer le segment moyen* → candidat = `j - i - 1`.
Incrément "i" pour tester un préfixe plus long.
- Sinon ('arr[i] > arr[j]') l'élément suffixe actuel ne peut pas rester après «arr[i]».
Déplacez `j` vers l'avant pour trouver un élément suffixe assez grand.

4. **Retour minimum**

Cet algorithme visite chaque élément au plus deux fois → **O(n)** temps et **O(1)** espace.

---

C'est vrai. Le Code – -Bon, le mauvais et l'Ugly-

##### 5.1 Bon – L'explication de l'entrevue

- **Scan linéaire** – montre que vous comprenez l'importance des indices de limites *pré-computing*.
- **La fusion de deux points** – montre des astuces avancées de pointeur (communes dans la séquence suivante la plus longue ou les suppressions minimales pour maintenir l'ordre).
- **Manipulation des caisses** – le "si (gauche) == n-1" garde prouve que vous pensez à des entrées déjà triées.

> *Astuce d'interview* : Dans une passe linéaire, je peux rapidement saisir les limites triées, puis les fusionner avec une technique à deux points pour respecter les contraintes de commande. (en milliers de dollars)

5.2 Mauvais – Les pièges communs

La raison de l'erreur
C'est quoi ?
**Ignorer l'état de l'ajustement après la suppression** Comparer l'élément préfixe pour la dernière fois avec l'élément suffixe pour la première fois. Autres
**Utiliser les boucles imbriquées**= O(n2) → TLE pour `n=105`.=Utilisez deux scans linéaires et un seul passe à deux points. Autres
**Cas de bord surdimensionnés** («arr=[1]», tous éléments égaux, ou strictement décroissant). Peut produire `-1` ou mauvais indice. Ajouter le début du trié et garder `i <= gauche` / `j < n` limites. Autres

##### 5.3 Ugly – Le Trick caché qui brise l'idée naïve

> **L'Ugly** est la réalisation que *vous ne pouvez pas juste coller le préfixe et suffixe arbitrairement*.
> Il est tentant de penser que vous pouvez "skip" le milieu et garder le suffixe. Mais si `arr[left] > arr[right]`, l'élément suffixe ne peut pas suivre le préfixe, vous devez donc déplacer le pointeur suffixe jusqu'à ce que vous trouviez un élément compatible.

Dans la pratique, de nombreux candidats sont coincés dans ce piège exact, ce qui entraîne des réponses incorrectes.
La clé est de traiter le pointeur suffixe comme un **search** plutôt qu'un segment fixe.

---

C'est vrai. Prise d'entrevues Toujours

1. **Énoncer votre plan en premier**
Il trouvera le plus long préfixe et suffixe croissant, puis essaiera de les fusionner tout en gardant l'ordre. (en milliers de dollars)
Cela vous montre comment structurer la solution.

2. **Expliquer la vérification des cas* *
Si le tableau est déjà trié, nous ne pouvons rien supprimer. (en milliers de dollars)
Cette petite ligne voyage souvent les candidats.

3. **Discussion de l'idée de deux points**
Je vais passer par le tableau de gauche et de droite, puis déplacer les pointeurs jusqu'à ce que je trouve une paire qui garde l'ordre. (en milliers de dollars)
Soulignez pourquoi c'est **linéaire**.

4. **Complexité des peines précoce* *
Mon algorithme fonctionne dans le temps O(n) et dans l'espace O(1), satisfaisant aux contraintes. (en milliers de dollars)

5. **Python optionnel/Java/C++ Extrait de code**
Partagez l'une des solutions ci-dessus sur le téléphone; recruteurs apprécient de voir que vous pouvez écrire le code correct sur place.

---

C'est vrai. Conclusion

LeetCode 1574 est un problème trompeurment subtil qui récompense ceux qui :

- Reconnaître le *boundary* du préfixe/suffixe trié
- Comprendre la nécessité d'une fusion qui préserve l'ordre
- Appliquer une technique **deux points** pour obtenir un temps linéaire

Avec les trois solutions langagières propres ci-dessus, vous êtes prêt à répondre à toute interview technique qui vous pose cette question. N'oubliez pas de souligner **pourquoi les solutions naïves échouent** – il démontre une compréhension algorithmique plus profonde.

Bon codage, et pourriez-vous écraser cette prochaine entrevue d'embauche! *

---

### ♫ Conseil d'entrevue Cheat- Feuille

Situation Que dire
C'est pas vrai.
**Écran de téléphone**=I=ll d'abord trouver le plus long préfixe trié et suffixe, puis les fusionner à l'aide d'un scan à deux points.= Autres
**Sur le site** Autres
**Review du code**Le truc clé est de s'assurer que l'élément suffixe que vous conservez est plus grand ou égal au dernier élément du préfixe choisi. Autres

---

Liens utiles

- LeetCode 1574 Discussion: https://leetcode.com/problèmes/shortest-subarray-to-be-removed-to-make-array-sorted/discuss/
- Guide technique à deux points : https://leetcode.com/articles/two-pointer-solution/
- Java Interview Prep: https://www.javaworld.com/article/3201234/learn-30-java-interview-questions.html

---

Joyeux entretien ! Si vous avez trouvé cet article utile, partagez-le sur LinkedIn ou Twitter avec #LeetCode #CodingInterview. C'est ce qu'il a dit