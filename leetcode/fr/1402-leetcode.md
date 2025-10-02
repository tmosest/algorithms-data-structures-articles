---
titre: LeetCode 1402. Réduction des plats -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Résumé des solutions**

Le problème est un problème classique du calendrier-le-préfixe-positif.

* Si vous faites cuire des plats dans un ordre *décroissant* de leur satisfaction,
vous pouvez continuer à ajouter un plat aussi longtemps que la somme de préfixe en cours reste
non négatif.
* Chaque fois que vous ajoutez un nouveau plat le *bénéfice* du plat est multiplié
par sa position (1‐fondée).
Le bénéfice total d'un préfixe de plats est exactement la somme de préfixe
lui-même.
* Par conséquent, pendant que nous traversons la liste triée, nous maintenons une course
Préfixe la somme.
Dès que cette somme de préfixe devient négative, ajouter plus de plats peut
seulement blessé le total; nous arrêtons.

La réponse finale est la somme de tous les préfixes positifs.

---

Algorithme
1. **Trier** le tableau `satisfaction` dans l'ordre **decreasing**.
2. Initialiser «prefSum = 0», «réponse = 0».
3. Pour chaque `s` dans le tableau trié
* `prefSum += s`
* Si `prefSum < 0` → **break**
* `réponse += prefSum`
4. Retour "réponse".

---

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie la satisfaction maximale possible.

**Lemme 1**
Laissez `S` être un ensemble de plats choisis dans un certain ordre.
Si nous commandons les plats de `S` dans un ordre décroissant de satisfaction,
la satisfaction totale de «S» ne diminue pas.

*Proof. *
La satisfaction totale de `S` est
\[
\sum_{i=1}^{k} s_{\pi(i)} \times i ,
\]
où `π` est l'ordre de cuisson et `k ====2'.
Réorganiser les plats de sorte que `s_{π(i)} \ge s_{π(j)}` pour `i < j` ne puisse que
augmenter chaque terme parce que le multiplicateur `i` augmente avec le
position. *



**Lemme 2**
Laissez `T` être la liste triée en ordre décroissant.
Laisser préfSum(i) La valeur de la valeur de référence est la valeur de référence. T[j]».
Si "prefSum(i) < 0", alors pour chaque "j ≥ i" la satisfaction totale de
tout horaire qui utilise les premiers plats `j` de `T` est **pas plus grand** que
le calendrier qui utilise uniquement les premiers plats `i-1`.

*Proof. *
Ajouter le plat `i` augmente le total de `prefSum(i)`.
Si «prefSum(i) < 0», cette contribution est négative, donc tout calendrier
ne peut être pire que le calendrier qui le saute. *



* Théorème *
L'algorithme produit la satisfaction totale maximale possible.

*Proof. *
Par Lemma 1 nous pouvons supposer que les plats sont transformés en baisse
ordre.
L'algorithme continue d'ajouter un plat aussi longtemps que la somme du préfixe courant
reste non négatif; une fois qu'il devient négatif, par Lemma 2
L'ajout ne ferait que diminuer le total.
D'où l'algorithme considère exactement l'ensemble optimal de plats et
accumule leurs contributions correctes, ce qui donne le total maximal
satisfaction. *



---

Analyse de complexité

*Trier* domine l'exécution : **O(n log n)** temps.
L'algorithme utilise **O(1)** espace supplémentaire (à l'exception du tableau d'entrée).

---

### Mise en oeuvre de la référence (Python)

'`python
de taper l'importation Liste

Solution de classe:
def maxSatisfaction(self, satisfaction: List[int]) -> Int:
# Étape 1: trier dans l'ordre décroissant
satisfaction.sort(inverse=vérité)

pref_sum = 0 # nombre actuel de préfixes pour les plats choisis
réponse = 0

# Étape 2: itérer tandis que la somme préfixe reste non négative
pour s en satisfaction:
pref_sum += s
si pref_sum < 0:
Break # ajouter plus ne fera que mal
réponse += pref_sum

réponse de retour
«» "

---

### Mise en œuvre de la référence (C++)

'`cpp
solution de classe {
public:
int maxSatisfaction(vecteur<int> et satisfaction) {
tri(satisfaction.begin(), satisfaction.end(), plus<int>();
long prefSum = 0, res = 0;
pour (int s : satisfaction) {
le nombre d'heures de travail est égal à celui des heures de travail.
Si (préfSum < 0) rupture; // arrêt lorsque la somme du préfixe devient négative
rés += prefSum; // accumuler le bénéfice
}
retourner static_cast<int>(res);
}
};
«» "

---

### Mise en oeuvre des références (Java)

"Java
solution de classe {
Int public maxSatisfaction(int[] satisfaction) {
Arrays.sort(satisfaction);
// Trier en ordre décroissant
pour (int i = 0; i < satisfaction. longueur / 2; i++) {
int tmp = satisfaction[i];
satisfaction[i] = satisfaction[satisfaction.longueur - 1 - i];
satisfaction[satisfaction.longueur - 1 - i] = tmp;
}

long prefSum = 0, res = 0;
pour (int s : satisfaction) {
le nombre d'heures de travail est égal à celui des heures de travail.
si (préfSum < 0) rupture;
res += prefSum;
}
retour (int) rés;
}
}
«» "

---

Cet algorithme gourmand est optimal et beaucoup plus rapide que les solutions DP,
tout en étant très simple à comprendre et à mettre en œuvre.