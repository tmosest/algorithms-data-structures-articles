---
titre: LeetCode 1921. Éliminer le nombre maximal de monstres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Éliminer le nombre maximum de monstres
> **Une plongée profonde sur un problème classique de LeetCode (Time-O(n), Space-O(n)* *

---

Rétablissement du problème

- Oui.
-- -- -- -- -- --
**Dist[i]» – distance du monstre *i* par rapport à la cible. <br> `speed[i]` – vitesse constante du monstre *i*. Autres
À chaque tour nous pouvons éliminer ** exactement un** monstre. <br> Un monstre qui arrive à temps `t` (nombre entier de tours) avant que nous ayons une chance de tirer à elle va gagner. Autres
**But**= Trouvez le nombre maximum de monstres que nous pouvons éliminer avant que n'importe quel monstre n'atteigne la cible. Autres

> **Output** – le nombre de monstres que nous pouvons éliminer.

---

- Oui. 1. Intuition – Quand un monstre arrive-t-il? (en milliers de dollars)

Un monstre a besoin de «ceil(dist/vitesse)» tourne pour atteindre la cible.
Pourquoi ?

* `dist = 4`, `speed = 3` → il faut 1,33 tours, donc il arrive au tour **2**.
* `dist = 2`, `speed = 2` → il atteint au tour **1**.

Ainsi **temps d'arrivée** est:

Texte
arrivée = ceil( dist / vitesse )
«» "

Si `arrivée` est plus grand que le nombre de monstres que nous avons, cela signifie simplement que le monstre arrivera *après* nous avons déjà fini d'éliminer tout le monde – nous pouvons l'ignorer en toute sécurité.

---

- Oui. 2. Solution classique – Demande prioritaire

La solution la plus courante (et celle que vous voyez le plus souvent sur LeetCode) est :

1. ** Calculez l'heure d'arrivée** de chaque monstre.
2. **Trier** toutes les heures d'arrivée.
3. Marchez à travers eux: dès que nous avons frappé un monstre dont l'heure d'arrivée `= tour courant` nous arrêtons – ce tour est la réponse.

«» "
Tri(arrivée)
pour (tour = 0; tour < n; ++tour) {
si (arrivéeTimes[tour] <= tour) retourne le tour;
}
retour n;
«» "

* Heure*: `O(n log n)` (à cause du tri)
*Espace*: `O(n)` (pour le tableau des heures d'arrivée)

Bien que cela soit assez rapide pour la plupart des cas de test, nous pouvons faire mieux – **O(n) time**.

---

- Oui. 3. Le seau / Tri de la composition Heure

L'observation clé :
*Pour qu'un monstre survive jusqu'à ce qu'il devienne `t`, son heure d'arrivée doit être ≤ `t`. *

Au lieu de trier, nous **bucket** monstres à leur heure d'arrivée.

«» "
n = longueur dist.
seau[i] = nombre de monstres qui arrivent au tour i (0-indexé)
«» "

Nous n'avons besoin que de seaux jusqu'à «n‐1». Si le temps d'arrivée d'un monstre est ≥ `n`, il arrivera après que nous ayons déjà fini d'éliminer tout le monde – cela ne cause jamais de problèmes.

**Étape 1 – Construire les seaux**

Texte
pour chaque monstre i
arrivée = ceil(dist[i] / speed[i])
en cas d ' arrivée < n
seau[arrivée]++
«» "

**Étape 2 – Scanner les seaux**

Nous marchons dans l'ordre des virages.
Au tour `i` nous avons déjà éliminé les monstres `éliminés`.
Si **plus de monstres attendent à ce tour que les tours que nous avons survécu**, c'est-à-dire

«» "
éliminée + seau[i] > i
«» "

alors un monstre atteindra la cible avant que nous puissions tirer – nous nous arrêtons et retournons 'i'.
Sinon nous ajoutons les monstres de ce tour à `éliminé` et continuons.

Si nous terminons le scan sans revenir, nous pouvons éliminer tous les monstres – la réponse est `n`.

**Algorithme complet (style python)* *

'`python
def eliminerMaximum(dist, vitesse):
n = len(dist)
seau = [0] * n

pour d, s dans le zip(dist, vitesse):
arrivée = math.ceil(d / s)
en cas d ' arrivée < n:
Seau[arrivée] += 1

éliminé = 0
pour i dans la plage(n):
si éliminé + seau[i] > i:
retour
éliminé += seau[i]

retour n
«» "

**Pourquoi ça marche* *

* Au tour `i` nous avons exactement `i+1` possibilités de tirer (tourner 0, tourner 1, ..., tourner i).
* Si à n'importe quel tour `i` le nombre de monstres qui sont déjà arrivés (`eliminated + seau[i]`) dépasse le nombre d'opportunités (`i+1`), certains monstres gagnent - nous ne pouvons pas aller plus loin.
* Si nous atteignons la fin des seaux, nous avons eu assez de tours pour tirer une fois à chaque heure d'arrivée de monstre, donc tous les monstres sont éliminés.

**Complexité* *

- Oui.
-- -- -- -- -- --
**Heure**="O(n)" – un passage à seau, un passage à balayage. Autres
**L'espace**="O(n)" – le tableau de godets. Autres

---

- Oui. 4. Mise en œuvre des références

Vous trouverez ci-dessous le même algorithme écrit en **Java 17**, **C++17** et **Python 3**.
Les trois sont des traductions 1 à 1 de la logique décrite ci-dessus et sont prêtes à être collées dans votre éditeur.

---

#### 4.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
publique Maximum(int[] dist, vitesse int[] {
int n = longueur dist.;
int[] seau = nouveau int[n];

// Construire des seaux
pour (int i = 0; i < n; i++) {
arrivée int = (int) Math.ceil((double) dist[i] / speed[i]);
si (arrivée < n) {
seau[arrivée]++;
}
}

// Seaux de balayage
int éliminé = 0;
pour (int i = 0; i < n; i++) {
si (éliminé + seau[i] > i) {
retour i;
}
Éliminé += seau[i];
}
retour n;
}
}
«» "

---

Numéro 4.2 C++17

'`cpp
#incluez <vecteur>
#incluez <cmath>

solution de classe {
public:
élimination Maximum(std::vector<int>& dist, std::vector<int>& speed) {
int n = dist.size();
md::vecteur<int> seau(n, 0);

// Construire des seaux
pour (int i = 0; i < n; ++i) {
l'arrivée int = static_cast<int>(std::ceil(static_cast<double>(dist[i]) / speed[i]);
si (arrivée < n) {
++bucket[arrivée];
}
}

// Seaux de balayage
int éliminé = 0;
pour (int i = 0; i < n; ++i) {
si (éliminé + seau[i] > i) {
retour i;
}
Éliminé += seau[i];
}
retour n;
}
};
«» "

---

4.3 Python 3

'`python
importer des maths
de taper l'importation Liste

Solution de classe:
éliminer Maximum(self, dist: List[int], vitesse: List[int]) -> Int:
n = len(dist)
seau = [0] * n

# Construire des seaux
pour d, s dans le zip(dist, vitesse):
arrivée = math.ceil(d / s)
en cas d ' arrivée < n:
Seau[arrivée] += 1

# Seaux de balayage
éliminé = 0
pour i dans la plage(n):
si éliminé + seau[i] > i:
retour
éliminé += seau[i]

retour n
«» "

---

- Oui. 5. Bonne – mauvaise – mauvaise perspective

- Oui.
-- -- -- -- -- --
**Bien**. *O(n)* temps, *O(n)* espace. Il gère toutes les caisses de bord. Logique très claire (bucket & scan). Autres
Autres **Le tableau de godets peut être grand ('n` jusqu`à 200 000). Si de nombreux monstres arrivent après les virages `n`, ils sont simplement ignorés – mais nous allouons toujours le tableau complet. Autres
Une solution naïve de file d'attente est simple mais « O(n log n) ». Si vous n'avez besoin que de la réponse pour une seule requête, l'astuce de seau peut se sentir un peu magique et plus difficile à justifier à un intervieweur sceptique. Autres

---

- Oui. 6. Ce que les intervieweurs aiment

1. ** Expliquez votre pensée** – commencez avec -I-ll calculez les temps d'arrivée et montrez-les trier.
2. **Afficher que vous pouvez optimiser** – demander si nous pouvons faire mieux que `O(n log n)`. Apportez l'idée de seau, et expliquez l'invariant de tour de tour.
3. **Boîtes de bord à la main** – par exemple, `dist[i]=0`, `speed[i]=1`, ou tous les monstres arrivent après `n`.
4. **Temps-Espace compromis** – vous pouvez mentionner que si la mémoire est à une prime, vous pouvez conserver la liste triée au lieu de seaux.

---

- Oui. 6. Décollage final

La solution «bucket & scan» est un exemple classique de *triage par comptage* lorsque les touches (temps d'arrivée) sont limitées par «n».
Il bat l'approche standard de la file d'attente par un facteur clair de *log n* et garde le code lisible.

Quand vous êtes demandé de résoudre ce problème dans une interview:

1. **Afficher la solution simple de file d'attente de priorité** (qui permet de bien comprendre la mécanique de base).
2. **Demandez** s'il y a une approche plus efficace.
3. **Présentez l'astuce du seau** – expliquez l'invariant clé (`éliminé + seau[i] > i`) et pourquoi ignorer les temps d'arrivée ≥ `n` est sûr.
4. **Remplissez la complexité** et vérifiez rapidement les contraintes.

Bonne chance, et que vos tirs atteignent toujours la bonne cible! C'est ce qu'il a dit