---
titre: LeetCode 3371. Identifier le plus grand écart dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3371 – Identifier le plus grand écart dans un tableau
**Difficulté:** Moyenne
**Tags:** Array, HashMap, deux points, Greedy

---

Aperçu du problème

On vous donne un tableau entier `nums`.
Exactement les éléments `n‐2` sont *numéros spéciaux*.
L'un des deux éléments restants est **la somme** de ces chiffres spéciaux,
et l'autre est un *outlier* – un nombre qui n'est ni un nombre spécial ni l'élément de somme.

Les trois éléments ont des indices distincts, mais ils peuvent avoir la même valeur.

> **Objectif:** Retourne le **plus grand** possible aberrant qui peut exister dans le tableau.

---

- Oui. Principales observations

Laissez

Symbole Signification
C'est quoi ?
Ensemble de numéros spéciaux (taille `n‐2`) Autres
Somme de tous les éléments dans "S"
L'élément qui correspond à "sumS"
Le plus important
Total de tous les éléments du tableau

De la définition nous avons:

«» "
Total = sommeS + x + o
«» "

Mais `x = sumS`, donc

«» "
Total = 2 * x + o
=> o = total - 2 * x
«» "

Ainsi, si nous choisissons un élément `x` comme élément *sum*, l'élément aberrant est forcé d'être
Total - 2 * x '
La seule vérification restante est de savoir si cette aberration apparaît réellement dans le tableau
à un indice différent.

---

C'est vrai. Algorithme

1. **Précalculer** la somme totale du tableau.
2. Construire une carte **fréquence** (`valeur → count`) de tous les nombres pour les contrôles d'existence O(1).
3. Pour chaque élément `x` dans le tableau
* calculer `o = total - 2 * x`.
* Vérifier que `o` existe dans la carte.
* Si `o != x`, tout nombre ≥ 1 est suffisant.
* Si `o == x`, nous avons besoin d'au moins deux occurrences (`compte > 1`).
4. Gardez le **maximum** valide plus aberrant trouvé.
5. Rends ce maximum.

---

C'est pas vrai. Preuve d'exactitude

Nous prouvons que l'algorithme rend le plus aberrant possible.

*Lemme 1:*
Si un élément `x` est l'élément de somme, alors l'élément aberrant doit être `o = total - 2 * x`.

*Proof. *
Par définition, `total = sommeS + x + o` et `sumS = x`.
Ainsi, `total = 2x + o` → `o = total - 2x`. *

*Lemme 2: *
Pour tout élément de somme de candidats `x`, l'algorithme déclare `o` valide s'il existe un indice `j ' i` tel que `nums[j] = o`.

*Proof. *
La carte de fréquence contient le nombre exact de chaque valeur.
- Si l ' on entend par < < o > > x > , tout événement de < < o > > à un indice différent satisfait aux prescriptions.
- Si `o = x`, nous avons besoin d'une deuxième occurrence pour garantir des indices distincts; donc `compte > 1`.
Ainsi, l'algorithme est à la fois nécessaire et suffisant. *

* Théorème: *
L'algorithme produit le maximum aberrant possible.

*Proof. *
Considérez toute configuration valide du tableau.
Laissez `x` être l'élément de somme choisi.
Par Lemma 1, l'écart est «o = total - 2x».
Lorsque l'algorithme itère sur ce `x`, il calculera exactement ce `o` et, par Lemma 2, le jugera valide.
Ainsi l'algorithme considère **chaque** possible aberrant.
Il conserve le maximum de tous les `o` valides, de sorte que la valeur retournée est la plus aberrante possible. *

---

C'est vrai. Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Autres Construction de la somme et de la carte
Autres Itération sur tous les éléments
**O(n)**

`n ≤ 105`, de sorte que cela s'inscrit facilement dans les limites.

---

Cas de bord

Motif de l'algorithme
- C'est pas vrai.
Dupliquer les valeurs de la somme et de l'extrant Différents indices Les nombres vérifiés (`>1` quand les valeurs sont égales)
Numéros négatifs Calcul de la somme fonctionne normalement Aucune manipulation spéciale nécessaire
Autres Tous les éléments sont identiques.
Autres Le maximum parmi les négatifs encore choisis

---

Mise en œuvre du code

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public int getLargestOutlier(int[] nums) {
= 0;
Carte<integer, integer> freq = nouveau HashMap<>();

pour (int num : nombres) {
total += nombre;
freq.put(num, freq.getOrDefault(num, 0) + 1);
}

int best = Integer.MIN_VALUE;

pour (int num : nombres) {
candidat Somme = nombre;
int aber = total - 2 * candidat Somme;

Nombre entier = freq.get (plus important);
si (compter == null) continuer;

si (plus loin) le candidatSum) {
si (compter > 1) meilleur = Math.max (meilleur, plus aberrant);
} autre {
best = Math.max (best, aberrant);
}
}
le meilleur retour;
}
}
«» "

---

Python 3

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def getLargestOutlier(self, nombres: List[int]) -> Int:
total = somme(s)
freq = compteur(s)

meilleure = flotteur('-inf')

pour x en nombres:
aberration = total - 2 * x
cnt = freq.get(autre, 0)

si aberrant == x:
si cnt > 1:
best = max (meilleur, meilleur)
Sinon:
si cnt:
best = max (meilleur, meilleur)

le meilleur retour
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int getLargestOutlier(vecteur<int>& nums) {
long total = 0;
unordered_map<int, int> freq;
pour (int v : nombres) {
total += v;
++freq[v];
}

int best = INT_MIN;
pour (int x : nombres) {
= static_cast<int>(total - 2LL * x);
auto it = freq.find(outlier);
si [it] freq.end() continue;

si (supérieurement) x) {
si (it->seconde > 1) meilleur = max (meilleur, plus aberrant);
} autre {
best = max (meilleur, plus aberrant);
}
}
le meilleur retour;
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps et utilisation **O(n)** espace supplémentaire.

---

Article sur le blog – Le bon, le mauvais et le mauvais de LeetCode 3371

> *Mots clés:* LeetCode 3371, plus grand aberrant, problème de tableau, entretien de codage, conception d'algorithmes, préparation d'entrevue d'emploi

---

Introduction

Lorsque vous vous préparez à une entrevue technique, vous allez inévitablement tomber sur *puces de puzzle* qui semblent tester votre créativité plus que votre compétence de codage. Code du leet 3371 – *Identifiez le plus grand écart dans un tableau* – est un tel défi. Il semble simple à première vue, mais il cache une torsion subtile qui peut voyager même les développeurs assaisonnés.

Dans ce post, nous allons disséquer le problème, marcher à travers l'approche simple de "good" , pointer les écueils de "bad" qui peuvent vous faire trébucher, et révéler les cas bord de "gugly" vous ne devriez jamais ignorer. Enfin, nous partageons une solution polie et prête à la production en **Java**, **Python** et **C++**.

---

- Oui. Le problème en anglais clair

Vous êtes donné un tableau `nums` qui contient `n` entiers.
Exactement `n‐2` de ces nombres sont *spécial*.

- Oui. Un des deux autres nombres correspond au **somme** de tous les nombres spéciaux.
- Oui. L'autre numéro est le **outlier** – ce n'est ni un numéro spécial ni la somme.

Tous les indices sont distincts, mais la même valeur peut apparaître plus d'une fois.

**Tâche:** Trouvez le *plus grand* possible aberrant.

---

C'est vrai. La bonne solution – une solution propre, O(n)

Le point de vue clé :
Si nous choisissons un élément `x` pour être la somme de toutes les spéciales, l'aberration est forcée d'être `total – 2*x`.
Il suffit de vérifier si cette valeur calculée existe réellement ailleurs dans le tableau.

Texte
pour chaque x en nombres:
o = total - 2 * x
o existe en tableau et les indices diffèrent :
candidat = max (candidat, o)
«» "

Parce que nous précalculons la somme totale et une carte de fréquence, chaque vérification se déroule en O(1).
Donc tout l'algorithme est O(n) temps, O(n) espace.

---

C'est pas vrai. Les pièges communs

Pourquoi ça arrive ?
- Oui.
**O(n2) force brute** – Enumeration de toutes les paires de spéciaux
**Ne pas manipuler les duplicata** – en supposant que les valeurs sont uniques.
**Ignorer les nombres négatifs**
**En supposant que le tableau n'a que deux valeurs spéciales**

---

C'est vrai. Les cas de bord que vous devez couvrir

1. **Tous les mêmes nombres**
Exemple: `[5, 5, 5]` – ici l'élément de somme et le plus aberrant sont tous deux égaux `5`.
*Fix:* S'assurer qu'il y a au moins deux occurrences de «5».

2. ** Montants négatifs**
Exemple: `[-2, -1, -3, -6, 4]` – la somme des spéciaux est `-6`.
*Fix:* Poignées arithmétiques négatives naturellement; il suffit d'utiliser 64 bits entiers si vous vous inquiétez de débordement.

3. **Grands tableaux** (`n = 105`)
*Fix:* Solution O(n) avec carte de hachage simple.

4. **Plusieurs aberrations valides**
Il peut y avoir plusieurs candidats.
*Fix:* Garder la trace du maximum en itérant.

---

Code de préparation à la production

Vous trouverez ci-dessous des solutions concises et bien documentées dans les trois langues d'entrevue les plus populaires. Chaque mise en œuvre suit l'algorithme O(n) propre et comprend des commentaires pour faciliter la lisibilité.

*(Insérer des blocs de code Java, Python, C++ à partir de la section "Engagements de code" ci-dessus.) *

---

- Oui. Dernier départ

LeetCode 3371 est un exemple premier d'un problème de tableau *=look‐simple, en fait‐complex==*. La maîtrise vous donne :

- Confiance dans la manipulation algébrique des sommes.
- Expérience des contrôles d'existence par fréquence.
- Un modèle robuste que vous pouvez adapter à d'autres énigmes de type "outlier" ou "sum-based".

Lorsque vous atterrissez dans une salle d'entrevue de gestionnaire d'embauche, entrez avec cette solution, expliquez votre raisonnement, et vous allez non seulement impressionner avec le code, mais aussi avec le processus *pensé* – exactement ce que les recruteurs veulent.

---

Clôture

Les problèmes d'array sont souvent les héros méconnus de la préparation d'entrevue. Ils testent si vous pouvez traduire une observation mathématique en code, pas seulement si vous pouvez écrire des boucles et des conditions. LeetCode 3371 offre un terrain de jeu parfait pour cette compétence.

Pratiquez ce problème, modifiez les cas de bord, et vous serez prêt à relever tout défi *array aberlier* qui vient à votre manière – qu'il s'agisse de LeetCode, d'un concours de hackerrank ou d'une interview dans le monde réel. Bon codage !

---

N'hésitez pas à faire part de vos commentaires ou suggestions. Bonne chance pour ce travail de rêve ! C'est ce qu'il a dit.

---

* Fin de l'article. *