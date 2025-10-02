---
titre: LeetCode 3452. Somme des bons nombres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Code de Leet 3452 – Nombre de bons numéros
**Java-Python C++** – Solutions One-pass, O(n)
**Article de blog** – Le bon, le mauvais, et la laid de ce problème (SEO-optimisé pour l'embauche)

---

- Oui. 1. Récapitulation des problèmes

> **Don** un tableau entier `nums` et un entier `k`, un élément `nums[i]` est **bon** s'il est strictement supérieur aux éléments des indices `i‐k` et `i+k` (si ces indices existent).
> **Retour** la somme de tous les bons éléments.

**Contrôles* *
* 2 ≤ longueur nominale ≤ 100
* 1 ≤ nombres[i] ≤ 1000
* 1 ≤ k ≤ 2

---

- Oui. 2. Pourquoi ce problème est un tour d'interview de Must-Know

C'est bien, c'est mal.
C'est pas vrai.
**Bien** – Très court, temps O(n), espace O(1), pas de structures de données supplémentaires. **Bad** – L'état de la distance peut être mal compris; les gens vérifient parfois `i‐1` ou `i+1` au lieu de `i‐k`. Autres

---

- Oui. 3. Solution à passe unique (Les trois langues)

#### 3.1 Java

"Java
// Java 17
solution de classe publique {
la somme d'intérêt public de GoodNumbers(int[] nums, int k) {
int n = longueur nums;
= 0;

pour (int i = 0; i < n; i++) {
booléen bon = vrai;

si (i - k >= 0 && nums[i] <= nums[i - k]) bon = faux;
si (i + k < n && nums[i] <= nums[i + k]) bon = faux;

si (bonne) somme += nombres[i];
}
la somme de retour;
}
}
«» "

3.2 Python

'`python
# Python 3
def sum_of_good_numbers(nums: list[int], k: int) -> Int:
n = len(nums)
Total = 0

pour i dans la plage(n):
Bien = Vrai
i - k >= 0 et nombres[i] <= nombres[i - k]:
bonne = Faux
i + k < n et nombres[i] <= nombres[i + k]:
bonne = Faux
si bon:
Total += nombres[i]
retour total
«» "

#### 3.3 C++

'`cpp
// C++17
nt sumOfGoodNumbers(vector<int>& nums, int k) {
int n = nombres.size(), somme = 0;
pour (int i = 0; i < n; ++i) {
bool good = true;
si (i - k >= 0 && nums[i] <= nums[i - k]) bon = faux;
si (i + k < n && nums[i] <= nums[i + k]) bon = faux;
si (bonne) somme += nombres[i];
}
la somme de retour;
}
«» "

Les trois extraits partagent le même **O(n)** temps, **O(1)** complexité spatiale.

---

- Oui. 4. Explication étape par étape

1. **Initialiser l'accumulateur** `sum` (ou `total` en Python).
2. **Loop à travers chaque index** `i` dans le tableau.
3. **Somme** l'élément courant est bon (`bon = vrai`).
4. **Vérifier le voisin gauche**:
* Si 'i-k >= 0` et `nums[i] <= nums[i-k]`, l'élément est **not** bon.
5. **Vérifier le bon voisin**:
* Si `i+k < n` et `nums[i] <= nums[i+k]`, l'élément est **not** bon.
6. **Si toujours bon**, ajouter `nums[i]` à l'accumulateur.
7. Après la boucle, **return** la somme finale.

Les deux contrôles de la frontière (`i-k >= 0` et `i+k < n`) traitent automatiquement les cas de bord d'un seul voisin ou aucun.

---

- Oui. 5. Cas de bord et pièges communs

Pourquoi ça arrive ?
- Oui.
**En utilisant `i-1` et `i+1` au lieu de `i-k` / `i+k`** Double-vérifiez le paramètre de distance `k`.
**Ignorer les indices hors frontières** déclenche une erreur d'exécution. Toujours garder la vérification avec `>= 0` et `< n`. Autres
L'utilisation de `>=` au lieu de `>` permet de considérer des valeurs égales comme bonnes. Autres Gardez la comparaison comme `<=`. Autres
**Confuser `sum` vs `count`**= Certaines solutions comptent à tort le nombre d'éléments bons au lieu de les résumer. Autres Utiliser une variable qui représente clairement la valeur totale (par exemple, `total` ou `sum`). Autres

---

- Oui. 6. Analyse du rendement

Métrique
- C'est quoi ?
Complexité temporelle
Complexité spatiale
Facteur constant Très faible (seulement quelques opérations entières par itération) Très faible

Étant donné que la taille du tableau est au plus 100, le temps d'exécution est négligeable sur les machines modernes, mais le modèle s'échelle à des entrées plus grandes (la logique fonctionne pour `n` jusqu'à des millions).

---

- Oui. 7. Conseils d'entrevue

1. **Lisez attentivement la déclaration** – `k` peut être jusqu'à `floor(n/2)`; il peut y avoir deux voisins, un voisin, ou aucun.
2. **Exposer votre raisonnement** – Mentionnez que nous itérer une fois, vérifiez deux conditions, et accumulez.
3. **Parlez des cas de bord** – Discutez des indices qui pourraient sortir des limites et de la façon dont vous les protégez.
4. **Afficher la complexité du temps/de l'espace** – Un temps succinct de O(n), O(1) espace est généralement suffisant.
5. **Demander des éclaircissements** – Et si `k` est égal `n/2`? Et les chiffres négatifs ? (les contraintes garantissent des valeurs positives, mais c'est une bonne habitude).

---

- Oui. 8. Aperçu du blog SEO optimisé

Section du référencement Mots clés Autres
C'est quoi ?
TitreSum of Good Numbers LeetCode 3452 – Java, Python, C++ Solutions
Description de la Meta de LeetCode 3452 'Sum of Good Numbers' avec le code clair Java, Python et C++. Comprendre l'algorithme, les cas de bord et les conseils d'entrevue. Autres
H1=Somme des bons nombres – LeetCode 3452=
Déclaration du problème
Un seul passage Algorithme
Mise en œuvre de Java Autres
Mise en œuvre de Python
Mise en œuvre C++ Autres
Cas et pièges des bords Autres
Heure et complexité de l'espace
Conseils d'entrevue et meilleures pratiques
Conclusion – Pourquoi ce problème est important

Ajouter des liens internes à des sujets liés au LeetCode (p. ex., Manipulation d'Array, Deux Pointeurs) et des liens externes à la page de problème officiel LeetCode et des solutions de discussion pour la crédibilité.

---

- Oui. 9. Réflexions finales

Le problème "Sum of Good Numbers" est un exemple de manuel d'une question d'interview **simple mais subtile**. La maîtrise démontre :

* Capacité de traduire les énoncés de problèmes dans des conditions précises.
* Confort avec la vérification des limites.
* Clarté dans la communication de la complexité et les cas de bord.

Avec les solutions Java, Python et C++ ci-dessus, vous êtes prêt à impressionner à la fois les plateformes de codage et les gestionnaires d'embauche. Bon codage 