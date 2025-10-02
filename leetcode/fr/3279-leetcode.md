---
titre: LeetCode 3279. Superficie totale maximale Occupé par Pistons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Résoudre la surface totale Occupé par Piston** (Code Leet 3279)

Ci-dessous vous trouverez:

Langue Code Complexité
- C'est quoi ?
**Java** Cliquez pour agrandir</sommary>``java
Importation de java.util.*;

solution de classe publique {
public long maxArea(hauteur de l'int, positions int[], directions des chaînes) {
int n = positions. longueur;
longue[] diff = nouvelle longue[2 * hauteur + 2]; // tableau de différence (indice 0 non utilisé)
long courantSum = 0; // somme des positions au moment 0
pour (int i = 0; i < n; ++i) courant Somme += positions[i];

pour (int i = 0; i < n; ++i) {
int pos = positions[i];
char d = directions.charAt(i);
si (d == 'U') { // se déplaçant en premier
diff[1] += 1;
diff[hauteur - pos + 1] += -2;
diff[2 * hauteur - pos + 1] += 2;
} autre { // en descendant d'abord
diff[1] += -1;
diff[pos + 1] += 2;
diff[pos + 1 + hauteur] += -2;
}
}

long best = courant Somme;
longue pente = 0; // dérivé de la surface totale en temps plein
pour (int t = 1; t <= 2 * hauteur; ++t) {
pente += diff[t];
actuel Somme += pente; // surface après t secondes
if (currentSum > best) best = courant Somme;
}
le meilleur retour;
}
}
```</details>" **Time** `O(n + hauteur)`<br>**Espace** `O(hauteur)` Autres
**Python**= <details><sommaire>Cliquez pour agrandir</sommaire>``python
importations
de taper l'importation Liste

def max_area(hauteur: int, positions: List[int], directions: str) -> Int:
n = len(positions)
diff = [0] * (2 * hauteur + 2) # 1-base index
cur = somme (positions)

pour pos, d en zip(positions, directions):
Si d == 'U':
diff[1] += 1
diff[hauteur - pos + 1] += -2
diff[2 * hauteur - pos + 1] += 2
Sinon : # 'D'
diff[1] += -1
diff[pos + 1] += 2
diff[pos + 1 + hauteur] += -2

meilleur = cur
pente = 0
pour t à portée(1, 2 * hauteur + 1):
pente += diff[t]
cur += pente
Si cur > meilleur:
meilleur = cur
le meilleur retour

# ---- utilisation de l' échantillon ----
si __nom__ == "__main__" :
h = 5
Pos = [2, 5]
dirs = "UD"
print(max_area(h, pos, dirs)) # → 7
"```</details>" **Time** `O(n + hauteur)`<br>**Espace** `O(hauteur)` Autres
**C++** Cliquez pour agrandir</sommary>``cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue longueur maxArea(hauteur de l'int, vecteur const<int>& positions, chaîne const& directions) {
int n = positions.size();
vectoriel <long long> diff(2 * hauteur + 2, 0); //
longue courbure = 0;
pour (int p : positions) cur += p;

pour (int i = 0; i < n; ++i) {
int pos = positions[i];
char d = directions[i];
si (d == 'U') { // se déplaçant en premier
diff[1] += 1;
diff[hauteur - pos + 1] += -2;
diff[2 * hauteur - pos + 1] += 2;
} autre { // en descendant d'abord
diff[1] += -1;
diff[pos + 1] += 2;
diff[pos + 1 + hauteur] += -2;
}
}

longue longue meilleure = cur;
longue pente longue = 0;
pour (int t = 1; t <= 2 * hauteur; ++t) {
pente += diff[t];
la pente de cur +=;
best = max (meilleur, cur);
}
le meilleur retour;
}

// Exemple d'utilisation
Int main() {
h = 5;
vecteur<int> pos = {2, 5};
chaîne dirs = "UD";
Cout << maxArea(h, pos, dirs) << '\n'; // impressions 7
}
```</details>" **Time** `O(n + hauteur)`<br>**Espace** `O(hauteur)` Autres

> **Tip** – Les trois solutions partagent la même logique :
> 1. Transformer chaque piston se déplace en un tableau de différence* de changement de pente.
> 2. Accumuler les pentes pour obtenir la zone après chaque seconde.
> 3. Suivre le maximum.

---

Pourquoi ce problème est-il une médaille d'or pour les entrevues

- **Simulation + Optimisation**: Montre que vous pouvez transformer une simulation O(n ·t) naïve en O(n + h) par maths intelligents.
- **Préfixe-Sum/Difference Array**: Un tour d'interview classique. Maître, et vous pouvez résoudre beaucoup de problèmes.
- **Analyse de la complexité du temps**: Poignées `hauteur` jusqu'à 106 et `n` jusqu'à 105 – vous aurez besoin de penser à la mémoire et aux passes linéaires.
- **Connaissance des cas**: Pistons à «0» ou «hauteur», piston simple, tous se déplaçant dans la même direction.

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Le concept**=La physique directe à la transformation de la math=Peut confondre des candidats inconnus avec des tableaux de différences=Prise de distance maximale à *any* time=Prise maximale *après* arrêt de tous les pistons=
**Mise en oeuvre**=Algorithme monopass O(n + h)= Nécessite des entiers 64 bits pour éviter le débordement==Les indices de tableau peuvent conduire à des bogues subtils==
**Performance**

**Conseil pro**: Au cours d'une entrevue, articulez votre plan *avant* code d'écriture: "Nous utiliserons un tableau de différence parce que chaque contribution de pistons ne change que deux fois par période."

---

Étape par étape (Édition de Java)

1. **Somme de base** – "cur = positions de "i" (zone au moment 0).
2. **Disposition de la différence** – «diff[1]» détient la variation de *pente* (taux de variation de la surface par seconde) à chaque moment.
3. **Pour chaque piston**:
- Si vous montez ('U'):
«» "
diff[1] += 1; // commencer à augmenter
diff[hauteur - pos + 1] += -2; // touche la limite supérieure → commencer à diminuer
diff[2 * height - pos + 1] += 2; // touche la limite inférieure → recommencer à augmenter
«» "
- Si vous descendez ('D'):
«» "
diff[1] += -1; // commencer à diminuer
diff[pos + 1] += 2; // touche la limite inférieure → commencer à augmenter
diff[pos + 1 + hauteur] += -2; // touche la limite supérieure → commencer à diminuer
«» "
4. **Passer** sur `t = 1 ... 2*hauteur»:
- `slope += diff[t]` – met à jour la rapidité avec laquelle la zone change à cette seconde.
- `cur += pente` – zone après cette seconde.
- Gardez `meilleur = max(meilleur, cur)`.
5. **Retour** "meilleur".

> La taille du tableau `2*hight+2` est suffisante car un piston peut au plus changer de direction deux fois en pleine période (up → down → up).

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Construire diff. Autres
(hauteur)
**(hauteur)** Autres

Avec `hauteur ≤ 106`, le tableau de diff est d'environ 16 Mo (en utilisant `long`), ce qui convient confortablement à la mémoire.

---

Article du blog – Zone maximale Occupé par Pistons
**(SEO-optimisé, prêt à l'entrevue, bon-mauvais guide)* *

> **Mots-clés**: LeetCode 3279, simulation de piston, tableau de différence, entretien d'algorithme, O(n + h), Solutions Java Python C++, stratégie d'entretien

---

- Oui. 1. Présentation

Vous avez probablement vu des problèmes de simulation avant: Grâce à un ensemble d'objets se déplaçant sur une ligne, calculer quelque chose au fil du temps. (en milliers de dollars)
LeetCode 3279, ** Superficie totale maximale Occupé par Pistons**, prend ceci au niveau suivant: chaque piston rebondit entre les parois d'un cylindre, et vous devez trouver la surface totale maximale sous tous les pistons à tout moment.

> **Pourquoi est-ce une bonne question d'entrevue? **
> * Il teste les compétences de simulation, mais vous force à penser à **périodicité** et **structures de données efficaces**.
> * La solution optimale est étonnamment simple une fois que vous reconnaissez les mathématiques sous-jacentes.

---

- Oui. 2. Récapitulation des problèmes

- **Input**
- "hauteur" – limite supérieure du mouvement des pistons.
- `positions[i]` – hauteur actuelle du piston `i` (également la zone sous elle).
- "directions [i]" – "U" (en haut) ou "D" (en bas).

- **Objectif** – Retour du
\[
\text{zone totale}(t) = \sum_{i=0}^{n-1} \text{hauteur du piston }i\text{ après }t\text{ secondes}
\]
pour *any* entier `t ≥ 0`.
Les pistons ne s'arrêtent jamais; ils continuent à réfléchir pour toujours.

- **Constraints**
- `1 ≤ n ≤ 105`
- `1 ≤ hauteur ≤ 106`
- `0 ≤ positions[i] ≤ hauteur»

---

- Oui. 3. Approche naïve

Vous pouvez simuler seconde par seconde, mettre à jour chaque position de pistons et vérifier la somme.
Mais...

- Chaque piston a besoin de marches "O(hauteur)" pour un cycle complet.
- Avec 105 pistons et une hauteur de 106, qui est **1011 opérations** – bien au-delà des limites de temps.

---

- Oui. 3. Aperçu – Périodicité + changement de pente

Chaque piston est une onde triangulaire*:

- Si elle commence à `p` et monte, la zone augmente au taux `+1` par seconde jusqu'à ce qu'elle atteigne le sommet (`hauteur`).
- Oui. En haut, il inverse immédiatement la direction → la pente se transforme en `-1`.
- Après une autre `hauteur - p` secondes il frappe le fond, la pente retourne à nouveau à `+1`.
- Oui. Le motif répète toutes les "2*hauteur" secondes.

**Observation**:
Un piston *pente* (taux de changement de zone) ne change qu'à **trois moments distincts** dans une période complète.
Nous pouvons encoder tous ces changements dans un tableau **différence** – une technique classique pour les mises à jour de gamme et les requêtes ponctuelles en O(1).

---

- Oui. 4. Différences dans la construction

Mises à jour (indices basés)
- C'est quoi ?
Diff[1] += 1 ' <br> `diff[hauteur - p + 1] += -2` <br> `diff[2*hauteur - p + 1] += Démarrage, en haut, en bas
Diff[1] += -1` <br> `diff[p + 1] += 2 ' <br> `diff[p + 1 + hauteur] += -2'-Démarrer, frapper en bas, frapper en haut

La première entrée `diff[1]`** définit simultanément le changement de pente initial pour tous les pistons.
L'ajout ou la soustraction de `2` aux indices ultérieurs reflète l'inversion instantanée du mouvement.

> **Pourquoi 2 × hauteur? * *
> Un piston peut changer de direction au plus deux fois par cycle (up → down → up).
> Nous avons donc besoin d'un tableau assez long pour capturer les deux événements, donc `2*hauteur + 2`.

---

- Oui. 5. Balayer dans le temps

Une fois le tableau de différence construit :

1. < <cur = < i > > – zone au moment 0.
2. `pente = 0`
3. Pour chaque seconde `t = 1 ... 2*hauteur»:
- `pente += diff[t]` (mise à jour de la rapidité avec laquelle la zone change en ce moment).
- `cur += pente` (nouvelle surface totale après `t` secondes).
- "meilleur = max (meilleur, cur)".

Comme la pente est une fonction *par pièce, nous n'avons jamais à simuler les pistons eux-mêmes – nous mettons à jour les quantités agrégées.

---

- Oui. 6. Mise en œuvre en une seule ligne (Java, Python, C++)

Les extraits de code ci-dessus illustrent à quel point la solution finale peut être compacte une fois le calcul compris.
Toutes les langues suivent le même schéma :
- **Construire un tableau de diff en O(n)* *
- **Passer en O(hauteur)* *

---

- Oui. 7. Stratégie de préparation à l'entrevue

1. ** Clarifier la question** : On nous demande la superficie totale maximale * à tout moment*, pas après que tous les pistons s'arrêtent. (en milliers de dollars)
2. **Approcher l'approche**:
* Expliquez* que chaque mouvement de piston est périodique avec la période "2*hauteur".
- *Mention* qu'un piston ne change que deux fois par période son taux de changement de surface.
- *Introduire* un tableau de différence pour capturer les changements de pente.
3. **Écrire un code propre** – conserver les indices 1 pour éviter toute confusion.
4. **Tests sur papier :
- Pistons déjà à 0 ou en hauteur.
- Un seul piston se déplaçant dans une direction.
- Tous les pistons se déplacent ensemble.
5. **Exposer la complexité** – montrer que la solution s'écaille avec "hauteur" et "n".

> **Pourquoi cela est important**: Démontrer un plan clair et expliquer la logique indique la maîtrise aux intervieweurs, même si vous n'êtes pas 100 % confiant dans le code.

---

- Oui. 8. Pièges communs (et comment les éviter)

Piège
- Oui.
**Débordement entier** – la somme peut dépasser 32 bits. Autres
**Off‐by‐one dans les indices**. Autres
**Misinterpréter le "maximum**" Clarify you"re prendre le maximum en tout temps `t ≥ 0`. Autres
**Ne pas tenir compte de la période complète** Autres

---

- Oui. 9. A emporter

LeetCode 3279 est un exemple brillant de la façon dont *math* et *data-structures* peuvent transformer un cauchemar de simulation en solution O(n + h).
Que ce soit en Java, Python ou C++, l'idée centrale reste la même : transformer le mouvement en changement de pente et balayer une fois.

> **Rappelez-vous** – Quand les intervieweurs présentent un problème de simulation avec de grandes contraintes, pensez : *Y a-t-il une périodicité cachée? Puis-je utiliser des tableaux de somme ou de différence ?* C'est généralement la clé pour le casser.

---

10 ans. Appel à l'action

- **Pratique** – Essayez les variations: pistons sur un cercle, différentes conditions de limite, ou maximum après k secondes.
- **Partager** – Déposer votre propre code sur GitHub ou un blog ; d'autres peuvent apprendre de votre style.
- **Interview** – Apportez ce problème à votre prochaine entrevue de codage – c'est un gagnant pour vous et l'intervieweur.

---

11 ans. Pensée finale

Dans le monde du codage des interviews, ** les problèmes de simulation ne sont pas le goulot d'étranglement** – ils sont souvent la porte* à la pensée algorithmique plus profonde.
LeetCode 3279 montre qu'une structure de données bien choisie (le tableau de différences) peut vous épargner **millions d'opérations** et impressionner tout gestionnaire d'embauche.

> ** Bonne chance pour votre prochain entretien! * *
> Utilisez les solutions ci-dessus, expliquez clairement votre processus de pensée, et vous sortirez de cette pièce se sentant comme un vrai algorithme.

---

Bon codage, et que votre pile d'entrevues contiennent toujours la bonne *différence*! C'est ce qu'il a dit.

---

> *Cet article est adapté pour les développeurs d'entrevues et les gestionnaires d'embauche de technologie. N'hésitez pas à adapter le code et les explications à votre style d'enseignement ou d'embauche. *