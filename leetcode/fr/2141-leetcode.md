---
titre: LeetCode 2141. Durée maximale de fonctionnement des ordinateurs N -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Description de la solution – LeetCode 2141: Durée maximale de fonctionnement des ordinateurs N

** Exposé des problèmes* *
Vous avez des ordinateurs `n` et un tableau `batteries`.
`batteries[i]` est le nombre de minutes qu'une seule batterie peut alimenter un ordinateur.
A n'importe quelle minute entière, vous pouvez échanger des batteries entre les ordinateurs (swapping ne prend pas de temps).
Votre objectif est d'exécuter tous les ordinateurs `n` ** simultanément** pendant autant de minutes que possible.
Retourne ce nombre maximum de minutes.

> **Constraints**
> * `1 ≤ n ≤ batteries, longueur ≤ 10^5`
> * `1 ≤ batteries[i] ≤ 10'9'

Le point de vue clé :
Pendant n'importe quel intervalle de longueur `T`, *chaque* batterie peut contribuer au plus `T` minutes de puissance, même si elle peut fonctionner plus longtemps.
Ainsi, la contribution totale de toutes les batteries à un fonctionnement de la minute `T` est au maximum `min(batterie, T)` pour chaque batterie.

Nous présenterons deux approches populaires, avec une complexité temporelle de `O(m log m)` où `m = batteries.longueur`.
La méthode **sort‐and‐trim** est plus facile à comprendre et à mettre en œuvre, tandis que la méthode **binary search** est un peu plus -algorithmique et montre un angle différent.

Vous trouverez ci-dessous des implémentations prêtes à la copie dans **Java**, **Python** et **C++**.

---

Solution de triage (O(m log m))

L'idée est de garder toutes les batteries à l'exception de celles qui seraient "déchetées" si elles sont trop puissantes par rapport au temps d'exécution moyen actuel.

1. **Trier** le tableau de batterie.
2. Calculer la somme de l'énergie totale.
3. À partir de la plus grande batterie, continuez de la retirer de la considération alors qu'elle est plus grande que la moyenne actuelle possible `sum / (n - k)`.
*Quand une batterie est retirée, nous réduisons `sum` et `n` par une seule. *
4. Après la coupe, la réponse est simplement "sum / n" (division entière – tout s'adapte parfaitement maintenant).

Pourquoi ça marche ?

- Oui. Si la batterie la plus forte a plus de puissance que la moyenne (`somme / n`), elle serait utilisée seule pendant cette durée moyenne et le reste des batteries serait au ralenti.
L'enlever et recalculer la moyenne donne une limite plus serrée.
- Oui. Nous continuons à le faire jusqu'à ce que la batterie restante la plus forte puisse partager la charge avec le reste des batteries sans gaspiller aucune énergie.
A ce moment-là, chaque batterie peut être utilisée exactement `sum / n` minutes, ce qui est optimal.

---

Solution de recherche binaire (O(m log sum))

Approche alternative mais aussi rapide:

1. Calculer le total de l'énergie.
2. Définir `faible = 0`, `élevée = total / n`. (Aucune course ne peut dépasser cette limite supérieure.)
3. "faible ≤ élevée":
* Vérifiez si une course de mi-minutes est possible.
* Si oui, entreposez-le et recherchez plus haut; sinon, recherchez plus bas.
4. Pour **check** un candidat `mid`:
* Chaque batterie contribue `min(batterie, mi)` minutes.
* Somme toutes les contributions; si la somme est au moins `n * mi`, la course est possible.

Les deux approches sont `O(m log m)` mais la version de recherche binaire n'utilise qu'un seul passage sur la peritération du tableau.

---

Mise en œuvre du code

Voici des solutions propres et commentées en trois langues.
Tous utilisent l'arithmétique 64 bits («long» / «long long») parce que la somme totale peut dépasser 32 bits.

### Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
***
* Retourner le nombre maximum de minutes que tous les ordinateurs `n` peuvent exécuter simultanément.
* @param n nombre d'ordinateurs
* Gamme de batteries @param des temps d'exécution de la batterie
* @retour temps d'exécution maximum simultané (minutes)
*/
public long maxRunTime(int n, piles int[]) {
Tableaux.sort(batteries); // O(m log m)

somme longue = 0;
pour (int b : piles) somme += b; // énergie totale

int idx = batteries.longueur - 1; // commencer par le plus grand
pendant que (idx >= 0 && batteries[idx] > somme / n) {
sum -= piles[idx]; // supprimer une batterie trop puissante
idx--; // réduire le tableau utilisable
n--; // un ordinateur de moins
}

somme de retour / n; // réponse finale
}
}
«» "

Python

'`python
def maxRunTime(n: int, batteries: list[int]) -> Int:
"""
Retourner le nombre maximum de minutes que tous les ordinateurs `n` peuvent exécuter simultanément.
"""
batteries.sort() # O(m log m)

total = somme (batteries)
i = len(batteries) - 1 # indice de la plus grande batterie

# Couper des batteries qui seraient gaspillées
alors que i >= 0 et batteries[i] > total // n:
Total -= piles[i]
I -= 1
n -= 1

total de retour // n
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long maxRunTime(int n, vector<int>& batteries) {
tri(batteries.begin(), batteries.end()); // O(m log m)

somme longue = 0;
pour (int b : piles) somme += b; // énergie totale

int idx = batteries.size() - 1;
pendant que (idx >= 0 && batteries[idx] > somme / n) {
sum -= piles[idx]; // supprimer trop puissant
idx--;
n--;
}
la somme de retour / n;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 2141

> **Titre**: *Mastering LeetCode 2141 – Durée maximale de fonctionnement des ordinateurs N*
> **Méta-Description**: Découvrez la solution optimale, les pièges et les perspectives d'entrevue pour LeetCode 2141. Lisez le guide complet en Java, Python et C++.

---

- Oui. 1. Présentation

LeetCode 2141 vous demande de maximiser le temps de fonctionnement simultané d'un ensemble d'ordinateurs utilisant un pool de batteries.
C'est un problème classique d'allocation des ressources* qui apparaît fréquemment dans les entrevues techniques.
Pourquoi ? Parce qu'il vous force à penser à **planification de la capacité**, **morcelage en forme** et **recherche binaire** – toutes les compétences qui sont très précieuses pour l'ingénierie des données et les rôles de moteur.

- Oui. 2. Récapitulation des problèmes

Vous avez :
- Les ordinateurs.
- "m = batteries.longueur".
- `batteries[i]` = durée d'exécution de la batterie `i` (minutes).

Vous pouvez échanger des batteries entre les ordinateurs à tout moment (swapping est instantané).
Objectif : trouver le nombre maximum de minutes que tous les ordinateurs `n` peuvent exécuter ** simultanément**.

- Oui. 3. Intuition et observations clés

Observation Pourquoi ça compte
C'est-à-dire
**O(1) Swap**= Permet de rééquilibrer instantanément; la seule contrainte réelle est la capacité de la batterie. Autres
**La batterie ne peut pas dépasser T**= Au cours d'un intervalle de « T » minutes, une batterie contribue au maximum à « T » minutes. Autres
**Faisable Total**= Une longueur `T` est réalisable sif `=min(batterie, T) ≥ n *T`.

La dernière observation nous donne une fonction **decision** – un candidat parfait pour la recherche binaire.

- Oui. 4. Les bons – Tri et tri

C'est vrai. Ce qu'il fait

1. Trie les batteries ascendantes.
2. Continuez à tailler la batterie la plus forte s'il était autrement "idle".
3. Les batteries restantes peuvent toutes être utilisées pendant exactement `sum / n` minutes.

Pourquoi c'est bon

- **Simple à expliquer** – parfait pour une entrevue.
- **Fast** – un "O(m log m)" tri + un seul balayage linéaire.
- **Déterministe** – aucun facteur aléatoire ; toujours la même réponse pour la même entrée.

Code – Extrait (Java)

"Java
Arrays.sort(batteries);
pendant que (batteries[idx] > somme / n) { ... }
«» "

- Oui. 5. Les mauvaises – Pièges de recherche binaire

La recherche binaire est élégante mais subtile :

- **Bride supérieure Wong** → boucle infinie.
Utilisez toujours `haut = total / n`, pas `total` lui-même.
- **Département entier** – "mid = (faible + élevé) / 2` peut déborder; utiliser "faible + (faible - faible) / 2`.
- **Fonction de faisabilité** – vous devez résumer `min(batterie, milieu)`; oublier de cap à `mid` donnera de mauvais résultats.

#### Conseil d'entrevue
Si on vous demande de justifier la recherche binaire, soulignez que `mid` est un **guess** pour l'exécution de la cible, et le test de faisabilité est essentiellement un *knapsack* avec des poids limités.

- Oui. 6. Les cas de pièges et de bords communs

Exemple de piège
C'est pas vrai.
**32-bit de trop-plein**="somme" de 10^5 piles chacune 10^9 = 10^14="Utilisez `long`/`long'. Autres
**Liste des piles d'Empty**= `m < n'=" Le problème garantit `m ≥ n'; toujours, gardez-vous contre la division par zéro. Autres
Après tri, la boucle de triage ne s'exécute pas; la réponse est `15/3 = 5`. Autres
Autres **Batterie très forte**"[1000,1,1]", "n=2" Trim 1000 → `sum=2`, "n=2`, réponse `1`. Autres

- Oui. 7. Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Tri Tableau 1 supplémentaire
Recherche binaire $ `O(m log (total / n)) $ `O(1) ́ supplémentaire

Avec `m ≤ 10^5`, les deux sont bien dans les limites de LeetCode.

- Oui. 8. Conseils d'entrevue

- **Expliquez la fonction de décision** avant de coder; les intervieweurs aiment voir votre processus de pensée.
- **Montrer la manipulation du boîtier** – par exemple, lorsque toutes les piles sont égales, ou qu'une batterie est astronomiquement plus grande.
- **Options de compromis** – par exemple, file d'attente prioritaire, PDD – pour démontrer l'étendue des connaissances, même si vous vous installez sur tri-trim pour la brièveté.
- **Temps de votre solution** sur un tableau blanc – assurez-vous de ne pas dépasser la fenêtre de 30 minutes allouée.

- Oui. 9. Conclusion

LeetCode 2141 est une illustration soignée de ** gredy triming + calcul arithmétique**.
En maîtrisant ce problème, vous présenterez une pensée algorithmique forte, une bonne compréhension de l'arithmétique entière et la capacité d'optimiser à la fois pour *temps* et *espace* – exactement les recruteurs de compétences recherchent dans les rôles backend, data-engineering et full-stack.

---

- Oui. Pourquoi ce blog vous aide à décrocher votre prochain emploi

- **Entretien prêt**: L'article traverse le pipeline de raisonnement complet.
- **Multi-langue**: Les extraits de Java, Python, C++ démontrent une compétence multiplateforme.
- **Adapté au référencement** : Mots-clés tels que *Temps maximal de fonctionnement des ordinateurs N*, *Codelet 2141*, *recherche binaire*, *entrevue de codage*, *Java*, *Python*, *C++* assurent la visibilité sur les moteurs de recherche d'emploi.
- **Structure claire**: Les en-têtes, les tables et les blocs de code facilitent la lecture de l'article.

---

À emporter

> **Sort‐et‐Trim** vous offre une solution propre et optimale qui est facile à expliquer dans une entrevue.
> **Binary Search** offre une perspective plus algorithmique et prouve le même résultat avec un objectif différent.
> Peu importe ce que vous présentez, soyez prêt à discuter des cas de bord et justifier la vérification de faisabilité, ce sont les moments d'interview ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Bonne chance, et le codage heureux!