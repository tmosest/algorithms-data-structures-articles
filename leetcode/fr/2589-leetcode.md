---
titre: LeetCode 2589. Temps minimum pour remplir toutes les tâches -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2589 – Temps minimum pour accomplir toutes les tâches
**Solutions en Java
**Guide optimisé par le SEO** qui couvre le *bon, le mauvais et le laid* de ce problème, parfait pour la préparation d'entrevues et la chasse au travail.

---

Récapitulation des problèmes

- **Input**: `tasks[i] = [start_i, end_i, duration_i] "
*La tâche doit s'exécuter pendant `duration_i` secondes (pas nécessairement continues) dans la fenêtre inclusive `[start_i, end_i]`. *
- **Computer**: peut exécuter un nombre illimité de tâches en même temps.
- **Objectif**: Trouver le **minimum des secondes** l'ordinateur doit être activé pour terminer *toutes* tâches.

> **Constraints**
> 1 ≤ tâches durée ≤ 2000
> * 1 ≤ start_i ≤ fin_i ≤ 2000
> 1 ≤ durée_i ≤ fin_i - début _i + 1

---

Pourquoi Cette solution Rocks

Pourquoi ça marche
C'est ce qu'on dit.
**Java**"O(n * w)" (mauvaise affaire) → "O(n * 2000)"
Même que Java
Même que Java

- **Greedy on the right-endpoint** garantit que chaque intervalle a déjà vérifié : tous les chevauchements possibles avec les intervalles qui se terminent plus tôt.
- Le tableau booléen/bit ('utilisé[1..2000]') marque à chaque seconde l'ordinateur est "on".
- Oui. Nous **first** consommons toutes les secondes déjà marquées à l'intérieur de la fenêtre de la tâche, puis nous **ajoutons les secondes restantes** à partir de l'intervalle "end" et se déplaçant à gauche.
- Oui. La réponse finale est simplement le nombre de secondes marquées.

---

Le code

> Les trois implémentations supposent l'environnement LeetCode: une seule méthode/fonction nommée `findMinimumTime` (ou la classe `Solution` de Python).

---

C'est vrai. Java (Java 17+)

"Java
Importer java.util. Les tableaux;
Importer java.util. Comparateur;

solution de classe publique {
***
* Code Leet 2589 – Temps minimum pour accomplir toutes les tâches
* Graisse + tableau booléen (indice maximal 2000)
*/
public int findMinimumTime[] tâches) {
// Trier par le bon paramètre
Arrays.sort(tâches, Comparator.comparingInt(a -> a[1]));

// Marked secondes: index 1..2000
booléen[] utilisé = nouveau booléen[2001];

pour (int[] t : tâches) {
début int = t[0];
l'extrémité int = t[1];
int dur = t[2];

Nombre de secondes déjà utilisées dans cette fenêtre
pour (int i = start; i <= fin && dur > 0; i++) {
si (utilisé [i]) {
Cette seconde compte pour la tâche
}
}

// 2-- Remplir les secondes restantes nécessaires avec cupidité de la droite
pour (int i = fin; durée > 0 && i >= début; i--) {
si (!utilisé[i]) {
used[i] = true; // allume l'ordinateur à cette seconde
// consommer une seconde de la tâche
}
}
}

// La somme de toutes les secondes marquées est la réponse
Int ans = 0;
pour (boolean b : utilisé) si (b) ans++;
le retour des an;
}
}
«» "

---

#### Python (Python 3.8+)

'`python
de taper l'importation Liste

Solution de classe:
def trouver MinimumTime(self, tâches: List[List[int]]) -> Int:
"""
Code du leet 2589 – Temps minimum pour accomplir toutes les tâches
Graisse + tableau booléen (taille 2001)
"""
# Trier par la fin de l'intervalle
tâches.sort(key=lambda x: x[1])

utilisé = [0] * 2001 # indice 1..2000

pour le début, la fin, la durée des tâches:
N° 1 Consommer des secondes déjà marquées dans la fenêtre
pour i dans la plage (départ, fin + 1):
si utilisé[i]:
durée -= 1
si la durée == 0:
pause

N° 2 Ajoutez les secondes manquantes avidement de droite à gauche
i = fin
pendant la durée > 0:
s'il est utilisé[i]] 0:
utilisé[i] = 1
durée -= 1
I -= 1

somme de retour (utilisée)
«» "

---

#### C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int findMinimumTime(vector<vector<int>>& tâches) {
// Trier par le bon paramètre
tri(tasks.begin(), tasks.end(),
[](const vector<int>& a, const vector<int>& b) {
retour a[1] < b[1];
});

vecteur<int> utilisé(2001, 0); // index 1..2000

pour (auto& t : tâches) {
int l = t[0], r = t[1], durée = t[2];

Nombre de secondes déjà utilisées dans cette fenêtre
pour (int i = l; i <= r && dur; ++i) {
si (utilisé(i)) plus--;
}

Annexe Ajouter les secondes manquantes avidement de la droite
pour (int i = r; i >= L && dur; --i) {
si (!utilisé[i]) {
utilisé[i] = 1;
d'autre part,
}
}
}

// Somme de toutes les secondes marquées
retour empty(used.begin(), used.end(), 0);
}
};
«» "

---

Le blog: Le bon, le mauvais, et le mal de résoudre le LeetCode 2589

> **Méta-description (SEO):* *
> * Apprendre à cracher LeetCode 2589 – Temps minimum pour accomplir toutes les tâches. Obtenez des solutions Java, Python et C++, une intuition algorithmique, une complexité temporelle et des conseils prêts à l'entrevue. *

---

C'est pas vrai. Ce que le problème veut (bon)

Pourquoi ça aide ?
C'est pas vrai.
**Intervalles + Durée** Autres
**Parallélisme illimité**= Fait le problème de *couverture* plutôt que de programmation classique. Autres
Autres **Échelle d'horizon temporel (=2000)**= Permet d'utiliser un simple tableau O(2000)=time line=. Autres

La partie **bon** est que les contraintes sont généreuses: vous pouvez marquer chaque seconde explicitement. Cela élimine le besoin de structures de données complexes comme les arbres de segment ou les arbres indexés binaires.

---

- Oui. L'intuition (bon)

1. **La surcharge est libre**
*Si deux tâches se partagent une seconde, l'ordinateur est déjà sur cette seconde; aucun coût supplémentaire. *
2. **Greedy from the Right**
*Pour toute tâche, nous essayons de terminer le plus de secondes possibles dans les dernières secondes de son intervalle. *
3. **Trier par fin**
*Lorsque les intervalles sont triés par leur extrémité droite, tous les chevauchements possibles avec les intervalles préalablement traités ont déjà été envisagés. *

> **Pourquoi trier par `start` échoue* *
> Si vous triez par l'extrémité gauche, une tâche qui commence tôt peut s'écouler une seconde à partir d'une tâche ultérieure qui nécessite cette seconde, provoquant le renversement de l'algorithme de l'ordinateur.

---

C'est vrai. L'algorithme central (bon)

«» "
trier les tâches par heure de fin
utilisé[1..2000] = 0 // Tableau booléen: 1 si l'ordinateur est allumé à cette seconde
pour chaque tâche [l, r, d] dans l'ordre trié:
Nombre de secondes déjà utilisées [l, r]
pour i = l .. r:
si utilisé[i] : d -= 1
si d == 0 : rupture

Annexe Ajouter les secondes restantes avidement de la droite
i = r
pendant que d > 0:
[i]:
utilisé[i] = 1
d -= 1
I -= 1

réponse = somme (utilisée)
«» "

- **Heure**:
*Worst-case* : chaque tâche scanne l'intervalle entier → `O(n * 2000)` `O(n)` parce que 2000 est une constante.
- **Espace**: `O(2000)` pour le tableau booléen → constante.

---

C'est pas vrai. Les pièges (Bad)

Symptômes Correction
C'est pas vrai.
Autres **Clause de tri des erreurs**= Mauvaise réponse ou TLE== Toujours trier par `end` (`tasks[i][1]`). Autres
**Off‐by‐one dans le tableau booléen**= Indice d'array 0 ou 2000 manquant==Allocate size `2001` (ou `2005` pour la sécurité). Autres
**Ignorer les secondes déjà utilisées** Autres
Autres **Utiliser un `Set<Integer>`**" Fonctionne mais plus lentement (`O(log n)` par insert) Autres
**Tâches de traitement dans l'ordre d'entrée** Autres

---

C'est vrai. Le "Ugly" – Quand les choses se compliquent

1. **Si `duration_i` était plus grande que la longueur de l'intervalle* *
La stratégie gourmande fonctionne encore parce que la tâche peut être divisée arbitrairement, mais vous devez vous assurer que vous ne sortez pas des limites tout en remplissant de la droite.
*Solution*: serrer la boucle à `i >= l` et arrêter une fois `durée` devient 0.

2. **Grande plage d'entrée (>2000)**
Dans une variante hypothétique avec `start_i, end_i` jusqu'à 109, le tableau booléen est impossible.
*Alternative*: utilisez un **`TreeSet` ou `HashSet`** pour stocker les secondes d'utilisation et un arbre **segment** ou **binaire indexé** pour les requêtes de portée.
L'approche de la ligne de temps n'est plus "good" mais devient "ugly" – plus de code, plus de bugs.

3. **Tâches multiples nécessitant exactement la même seconde* *
Si de nombreuses tâches ont des fenêtres identiques, l'algorithme compte encore chaque seconde, mais vous ne devez pas doubler.
*Insight*: la première boucle de l'algorithme consomme déjà toutes les secondes qui se chevauchent, de sorte que la seconde boucle ajoute seulement de nouvelles secondes uniques.

---

#### 6=" Conseils d'entrevue (Prêt à l'utilisation)

- ** Expliquez l'idée de ligne** avant de plonger dans le code.
- **Afficher la preuve principale** que le tri par « fin » est optimal : tout intervalle ultérieur ne peut pas bénéficier des secondes inutilisées antérieures.
- **Mention le tableau booléen à temps constant** – c'est une grande astuce pour éviter la structure des données dans le codage des entrevues.
- **Préparer les questions de suivi**: Que faire si l'horizon était énorme ? – être prêt à discuter des arbres de segment ou coordonner la compression.

---

- Oui. Pensée finale

Cracking LeetCode 2589 est tout sur **couverture**. Une fois que vous réalisez que le chevauchement ne coûte rien et que l'horizon temporel est minuscule, le problème se réduit à un simple balayage avide.
Le code Java, Python et C++ fourni illustre la même idée élégante, vous permettant de vous concentrer sur la perspicacité algorithmique** plutôt que de lutter contre les détails de l'implémentation.

Bonne chance sur votre parcours de codage et votre prochain entretien technique! C'est ce qu'il a dit.

---

> *Sentez libre de copier/coller les extraits de code ou le blog entier dans vos notes. Bon codage ! *

---



---
**Profitez du code "good", évitez les écueils "bad" et soyez prêt à s'attaquer aux cas de bord "ugly" si le problème change. **

---

> **TL;DR**: Trier par `end`, utilisez un tableau booléen, consommez des secondes déjà utilisées, ajoutez avec cupidité les secondes manquantes de la droite, résumez les secondes marquées. Les trois implémentations en langage fournissent la même solution d'espace "O(n)" et "O(1)".

---

Bon codage ! (en milliers de dollars)