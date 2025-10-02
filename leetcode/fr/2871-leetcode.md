---
titre: LeetCode 2871. Découper le tableau jusqu'au maximum Nombre de subarrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Aperçu de la solution

** Problème* *
Compte tenu d'un tableau «nums» (0 ≤ nums[i] ≤ 106), le diviser en sous-tribus contigus de sorte que

* chaque élément appartient exactement à un sous-réseau,
* la somme du bitwise– ET les scores de tous les concours sont **minimum possibles**,
* le nombre de sous-groupes est **maximal** parmi toutes les divisions qui atteignent cette somme minimale.

Retournez ce nombre maximal de sous-cours.

**Observation* *
Le score d'une sous-tribu est le bitwise ET de tous ses éléments.
`x & y ≤ x` et `x & y ≤ y`, donc le score de n'importe quel sous-réseau est **jamais plus grand** que le score de l'ensemble du tableau.
Si le score de l'ensemble du tableau est `> 0`, aucun sous-ensemble ne peut avoir un score `0`; le fractionnement ne peut qu'augmenter le score total.
Ainsi, le seul cas intéressant est lorsque le score global est `0`. Dans ce cas, nous pouvons diviser arbitrairement tant que chaque division a un score `0`.

**Greedy One-Pass**
Traverser le tableau en maintenant un ET (`cur`).
* Chaque fois que `cur` devient `0`, nous pouvons mettre fin à une sous-tribu ici - son score est `0`.
Nous réinitialisons `cur` à ─all‐ones=" (`-1` en deux-complement) et continuons.
* À la fin, nous aurons compté toutes les fractions zéro.
Si aucun n'a été trouvé (`ans == 0`) nous devons retourner `1` parce que tout le tableau est un sous-array.

Cette stratégie gourmande est optimale :
* Chaque fois que `cur` devient `0` nous sommes obligés d'inclure l'élément courant dans le sous-array actuel; sinon, l'élément suivant garderait toujours le ET non-zéro et nous ne pourrions pas terminer un sous-array plus tôt.
* Le fractionnement plus tôt ne peut jamais diminuer le score total (il reste `0`) et augmente toujours le nombre de sous-cours.

**Complexités* *
*Time*: `O(n)` – on passe par le tableau.
*Espace*: "O(1)" – seulement quelques variables entières.

---

Mise en oeuvre du code

Java

"Java
// LeetCode 2871: Découper le tableau jusqu'au maximum Nombre de stations
solution de classe {
Int public maxSubarrays(int[] nums) {
int cur = -1; // all-ones (complément bitwise de 0)
réponse int = 0;

pour (int val : nombres) {
cur &= val; // en cours ET
Si (curir) 0) { // terminé une sous-évaluation de zéro
réponse++;
cur = -1; // remise à l'unité
}
}
// Si aucune scission n'était possible, le tableau entier est une sous-tribution
réponse au retour == 0 ? 1 : réponse;
}
}
«» "

Python

'`python
# LeetCode 2871: Dispersion dans le maximum Nombre de stations
Solution de classe:
def maxSubarrays(self, nombres: list[int]) -> Int:
cur = -1 # masque all-ones
ans = 0

pour la valeur en chiffres:
cur &= val
Si cur == 0:
+= 1
pour = -1

retourner 1 si les années == 0 autres années
«» "

C++

'`cpp
// LeetCode 2871: Découper le tableau jusqu'au maximum Nombre de stations
solution de classe {
public:
int maxSubarrays(vecteur<int>& nums) {
Int cur = -1; // tous les
Int ans = 0;

pour (int val : nombres) {
cur &= val;
Si (curir) 0) { // sous-repère zéro trouvé
++ans;
cur = -1; //
}
}
retour des ans == 0 ? 1 : ans;
}
};
«» "

---

- Oui. Article du blog : Le bon, le mauvais, et le lamentable de diviser les tableaux par Bitwise AND

> **Titre**
> *=Le bon, le mauvais, et le lamentable de diviser les tableaux par Bitwise ET – Un guide pratique pour les développeurs de recherche d'emploi

3.1 Pourquoi ce problème compte pour votre portefeuille

- **Les opérations de type Bitwise** sont un élément essentiel des entrevues (en particulier chez FAANG). En les maîtrisant, vous comprenez la manipulation des données de bas niveau.
- **Les algorithmes de grêle** sont un thème d'interview classique. Ce problème mêle logique bitwise à une stratégie gourmande, une combinaison attrayante pour les recruteurs.
- Oui. La solution est *O(n) time* et *O(1) space*, un exemple parfait d'un algorithme efficace qui impressionnera les gestionnaires d'embauche.

3.2 Les bons – Ce que vous apprendrez

Concept Pourquoi il est bon Comment il vous aide
- C'est quoi ?
**Bitwise ET Properties** Vous saurez quand ET ne peut que réduire les valeurs, un aperçu clé pour beaucoup de problèmes de niveau bit. Autres
Autres **Greedy One-Pass**.Vous pouvez décider en un seul passage si vous devez diviser. Démontre la capacité de convertir un problème apparemment complexe en un balayage linéaire. Autres
Autres **Traitement des cas**= Retour `1` si aucune scission n'est possible. Autres Montre l'attention au détail, un trait très apprécié dans le code de production. Autres
Autres **Optimisation de l'espace** Points saillants du codage propre et efficace en mémoire – quelque chose que les recruteurs aiment voir. Autres

3.3 Les mauvaises – Pièges communs

Exemple d'erreur
- Oui.
**En supposant que vous pouvez diviser à tous les zéros ET**. Rappelez-vous à **reset** la course ET à tous les (`-1`) après avoir compté une fraction. Autres
**Ignorer l'affaire « no-split »**= Retourner « 0 » lorsque le tableau ne peut pas être divisé en un sous-array de zéro. Retourner `1` comme le nombre minimum de sous-tarifs. Autres
Autres **Utiliser une opération non-bitwise-AND**= Utiliser `+` ou `*` au lieu de `&` dans la boucle. Toujours utiliser `&=` pour une course ET. Autres
**Signature entière mal comprise** En deux, `-1` est `111...111`, qui est l'identité pour bitwise ET. Autres

3.4 La suringénierie et ce qu'il faut éviter

Pourquoi c'est une meilleure approche
- Oui.
**Pre-computing prefix AND arrays**= Nécessite une mémoire supplémentaire `O(n)`, inutile pour cette solution gourmande. Gardez une seule variable AND. Autres
**Recursive backtracking**= Temps exponentiel, pas évolutive pour `n = 105'.=Utilisez la stratégie avide d'un passage unique. Autres
**Utiliser BigInteger pour le bitwise ET**= Ajouter les frais généraux, perd l'avantage de performance. Stick aux types primitifs ('int'). Autres
**Ignorer l'astuce "all-ones"**.Réinitialiser en `0` au lieu de `-1` peut causer des erreurs logiques. Autres

3.5 Réflexions finales

Ce problème est un micro-écosystème de concepts algorithmiques:

1. **Algèbre bitwise** – comprendre comment ET se comporte.
2. **Greedy raisonnement** – peut-on se séparer immédiatement quand le ET frappe zéro?
3. **Edge-case mindfulness** – et si l'ensemble du tableau est déjà minimal?

En maîtrisant cela, vous ne vous contentez pas d'avoir une question LeetCode, mais aussi de démontrer un état d'esprit polyvalent qui valorise les recruteurs.

**Pourboire professionnel pour les candidatures**:
- Inclure cette solution dans votre repo GitHub dans un dossier clair (par exemple `Algorithms/LeetCode/2871`).
- Oui. Ajouter un README expliquant l'approche avide, la complexité et les extensions potentielles (p. ex. pour d'autres opérations bitwise).
- Mentionnez que la même technique peut être adaptée à des problèmes tels que la somme subarray maximale avec OU ou le nombre minimum de segments avec XOR = 0.

---

- Oui. Feuille de Cheat de référence rapide

Étapes Actions Code Extrait
- C'est quoi ?
Autres 1) Initialiser la course ET vers tous les éléments
Autres 2.Iterate over array. Autres
Autres Mise à jour en cours d'exécution et `cur &= val;`
Autres Contrôlez la valeur zéro et si (curir) 0) { ...}
Autres Réinitialiser après scission Autres
Autres Nombre de scissions
Autres Réponse finale

---

À emporter pour l'intervieweur

> Lorsque le score de l'ensemble du tableau est zéro, nous pouvons couper avec cupidité chaque fois que la course ET devient zéro; si le score est positif, le seul partage possible est l'ensemble du tableau. L'algorithme est linéaire et constant. *

N'hésitez pas à expliquer cette logique, et vous démontrerez votre capacité à mélanger la théorie avec le code propre et prêt à la production, exactement ce que les gestionnaires d'embauche recherchent. Bon codage 