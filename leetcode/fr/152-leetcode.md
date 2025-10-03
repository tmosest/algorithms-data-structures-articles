---
Titre: LeetCode 152. Subarray maximal de produit -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 152 – Subarray produit maximal
implémentations C++ + billet de blog SEO-friendly*

---

Récapitulation des problèmes

> **Subarray de produits maximaux* *
> Compte tenu d'un nombre entier, trouvez un sous-réseau **contitueux** avec le produit **le plus important** et retournez ce produit.

- "1 ≤ longueur nominale ≤ 2·104 "
- 10 ≤ nombres[i] ≤ 10'
- Oui. La réponse est garantie dans un entier signé 32 bits.

> **Exemple**
> `nums = [2, 3, -2, 4] → 6` (sous-arraison `[2,3]`)

---

Pourquoi ça compte ?

- **Favoris d'interview**: La plupart des intervieweurs demandent une variation de ce problème pour évaluer votre compréhension de la programmation dynamique* et de la manipulation des cas de pointe*.
- L'algorithme de Kadane : Le problème classique de la somme sous-array maximale, mais avec *multiplication*, qui introduit une torsion.
- **Avantage de recherche d'emploi**: La présentation d'une solution propre et idiomatique en plusieurs langues démontre la polyvalence aux recruteurs.

---

L'idée : garder la trace des deux Max et Min

La multiplication se comporte différemment de l'addition :

1. Un *négatif* fois un *négatif* → *positif*.
2. Un *positif* fois un *négatif* → *négatif*.

Ainsi, lors de la numérisation du tableau, nous devons nous rappeler **deux** le produit maximum courant *fin* à l'indice courant et le produit minimum courant *fin* à l'indice courant. Le minimum est essentiel car le prochain nombre négatif pourrait le transformer en nouveau maximum.

Algorithme (style kadané)

«» "
max_so_far = nombres[0]
current_max = nombres[0]
courant_min = nombres[0]

pour chaque nombre en nombres[1:]:
temp_max = current_max
current_max = max(num, temp_max * num, current_min * num)
current_min = min(num, temp_max * num, current_min * num)
max_so_far = max(max_so_far, current_max)

retourner max_so_far
«» "

- **Heure**: `O(n)` – un laissez-passer.
- **Espace**: "O(1)" – seulement quelques variables.

---

Code – Java, Python, C++

Vous trouverez ci-dessous des extraits propres et prêts à la production pour chaque langue. Chacun contient des commentaires et est prêt à coller dans votre éditeur LeetCode.

C'est pas vrai. Java

"Java
***
* LeetCode 152 – Subarray maximal du produit
* Heure: O(n) Espace: O(1)
*/
solution de classe {
Int maxProduit(int[] nombres) {
la valeur de la valeur de référence est égale à la valeur de référence de la valeur de référence.
la valeur d'int currMax = nombres[0];
Int currMin = nombres[0];

pour (int i = 1; i < nombres de longueur; i++) {
int n = nombres[i];
// si n est négatif, currMax et currMin échangeront des rôles
Int temps Max = currMax;
currMax = Math.max(n, Math.max(tempMax * n, currMin * n));
currMin = Math.min(n, Math.min(tempMax * n, currMin * n));
maxSoFar = Math.max(maxSoFar, currMax);
}
retour max SoFar;
}
}
«» "

# # # # # #

'`python
# LeetCode 152 – Subarray maximal de produits
♪ Heure: O(n) Espace: O(1)

Solution de classe:
def maxProduit(self, nombres: list[int]) -> Int:
max_so_far = curr_max = curr_min = nombres[0]
pour n en nombres[1:]:
temp_max = curr_max
curr_max = max(n, temp_max * n, curr_min * n)
curr_min = min(n, temp_max * n, curr_min * n)
max_so_far = max(max_so_far, curr_max)
retourner max_so_far
«» "

C'est vrai. C++

'`cpp
// LeetCode 152 – Subarray maximal du produit
// Heure: O(n) Espace: O(1)

solution de classe {
public:
int maxProduct(vector<int>& nums) {
int max_so_far = nombres[0];
Int curr_max = nombres[0];
int curr_min = nombres[0];

pour (int i = 1; i < nums.size(); ++i) {
int n = nombres[i];
int temp_max = curr_max;
curr_max = max({n, temp_max * n, curr_min * n});
curr_min = min({n, temp_max * n, curr_min * n});
max_so_far = max(max_so_far, curr_max);
}
retourner max_so_far;
}
};
«» "

---

Cas et pièges

Pourquoi ça compte Comment l'algorithme le gère
-- -- -- -- -- -- -- -- -- -- -- -- -- --
Le produit maximum peut être un seul négatif s'il y a un nombre impair, ou un positif si même. `curr_max` commence par le premier élément; la boucle se met à jour correctement. Autres
Autres 2. **Zeros dans le tableau**.Zero brise la chaîne de produits; un nouveau sous-réseau doit commencer après. `max(n, ...)` comprend `n` lui-même, qui devient 0, réinitialisant `curr_max` et `curr_min`. Autres
**L'élément doit être retourné. La boucle ne s'exécute jamais ; `max_so_far` est retournée. Autres
Autres 4= **Grand négatif * négatif**= Peut déborder si l'on utilise des entiers 32 bits. Le problème garantit le résultat dans un int signé 32 bits, de sorte que `int` est sûr. Autres

---

Les bons, les mauvais, les méchants

Les bons
- **O(n)** temps et **O(1)** espace – parfait pour les contraintes d'entrevue.
- Traite tous les cas (négatifs, zéro, positifs) en un seul passage.
- Très lisible une fois que vous comprenez l'idée *max/min paire*.

- Oui. Les mauvais
- Oui. Le code peut sembler un peu magique pour un lecteur de première fois; le *swapping des rôles* pour les nombres négatifs n'est pas immédiatement évident.
- Nécessite une utilisation prudente des variables temporaires pour éviter d'écraser accidentellement `curr_max` avant que `curr_min` ne soit mis à jour.

- Oui. L'Ugly
- Certaines solutions naïves tentent de précalculer les produits préfixés ou d'utiliser des tableaux de programmation dynamiques de taille `n`, ce qui donne **O(n)** espace et frais généraux supplémentaires.
- Un bug commun : oublier de réinitialiser le min/max après avoir rencontré un zéro, conduisant à des résultats incorrects.

---

Liste de contrôle rapide avant votre entrevue

- [ ] Expliquer pourquoi nous avons besoin de ** tous les deux** "currMax" et "curr" Min'.
- [ ] Montrez comment un nombre négatif *swaps* les.
- [ ] Passez par un exemple de signe mixte sur le tableau blanc.
- [ ] Mentionnez la mise à jour `max_so_far`.
- [ ] Discutez de la complexité du temps et de l'espace et pourquoi il est optimal.

---

## Bonus – Solution O(n) alternative (préfixe + postfixe)

Certains intervieweurs pourraient demander une approche "deux passes" :

1. Pass avant : calculez le produit maximum se terminant à chaque indice.
2. Passage en arrière : calculer le produit maximum à partir de chaque indice.
3. Prendre le maximum du produit des deux passes à chaque index.

Cela utilise également l ' espace " O(n) " mais peut être plus facile à expliquer sur le plan conceptuel.

---

Les pensées finales

Le problème Maximum Product Subarray est un exemple classique de la façon dont une simple déclaration de problème peut cacher une torsion subtile. En gardant la trace des produits **maximum** et **minimum** à chaque étape, nous traitons élégamment les nombres négatifs et les zéros en un seul passage. Maîtrisez ce modèle, et vous vous sentirez confiant en s'attaquant non seulement au LeetCode 152, mais à toute une série de problèmes d'entrevue qui impliquent *préfixer des produits* ou *scanners à deux faces*.

---

Faites-le.

- **Mise en oeuvre** les extraits dans votre langue préférée et test sur LeetCode.
- **Expliquer** l'algorithme à un ami ou enregistrer une courte vidéo; l'enseignement renforce l'apprentissage.
- **Ajouter** cette solution à votre portfolio ou GitHub repo; recruteurs aiment voir le code propre et multilingue.

Bon codage, et bonne chance d'atterrir ce travail de rêve! C'est ce qu'il a dit.

---

Référence Mots clés (pour l'article):
- Subarray maximal du produit
- LeetCode 152 solution
- Algorithme de Kadane pour le produit
- Problèmes d'entretien de programmation dynamique
- Codage d'interviews Java Python C++
- Préparation des entretiens d'embauche
- Gérer les nombres négatifs dans les tableaux
- O(n) temps O(1) problèmes de tableau d'espace

---