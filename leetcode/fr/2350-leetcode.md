---
titre: LeetCode 2350. Séquence la plus courte possible des rouleaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Ci-dessous vous trouverez **one-pass, O(k) space** solutions pour le problème LeetCode
2350. La séquence la plus courte possible de Rolls'.
Les trois extraits suivent la même idée :

1. Scanner le tableau `rolls` une fois.
2. Garder un ensemble (ou un petit tableau de drapeaux) qui se souvient des visages de dés
déjà apparu dans l'actuel segment.
3. Lorsque le jeu contient tous les visages `k`, nous avons trouvé un segment complet – nous
incrémenter le compteur de réponse et effacer le jeu pour démarrer un nouveau segment.
4. La réponse est "complèteSegments + 1" parce que la première longueur qui ne peut
être formé est un de plus que le nombre de segments complets que nous pouvons construire.

Langue Complexité Code
- C'est quoi ?
**Java**="O(n)" temps, "O(k)" espace=" [Code]="
**Python**
Temps "O(n)", espace "O(k)"

---

### Java

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe {
public int le plus courtSéquence(int[] rouleaux, int k) {
segments int = 0; // nombre d'ensembles complets trouvés
Définir<integer> vu = nouveau HashSet<>();

pour (int r : rouleaux) {
Voir.add(r);
si (seen.size() == k) { // nous avons vu tous les visages
segments++; // un segment complet terminé
voir.clear(); // démarrer un nouveau segment
}
}
segments de retour + 1; // la première longueur impossible
}
}
«» "

---

Python

'`python
Solution de classe:
def leastSéquence(self, rouleaux: List[int], k: int) -> Int:
segments = 0
vu = set()

pour r en rouleaux:
Voir.add(r)
si len(seen) == k: # segment complet
segments += 1
voir.clear()
segments de retour + 1
«» "

---

C++

'`cpp
#incluez <vecteur>
#inclut <unordered_set>
utilisant l'espace de noms std;

solution de classe {
public:
dans la plus courte Séquence(vecteur<int>& rouleaux, int k) {
segments int = 0;
non ordonné_set<int> vu;

pour (int r : rouleaux) {
voir.insérer(r);
si ((int)seen.size() == k) { // tous les visages vus
++segments; // terminé un segment
voir.clear(); // réinitialiser pour le segment suivant
}
}
segments de retour + 1; // première longueur impossible
}
};
«» "

> **Astuce** – Si vous voulez éviter un jeu de hachage en C++, vous pouvez utiliser une taille fixe
> tableau des booléens ('vecteur<bool> vu(k+1,false)') Ce qui est encore moins cher.

---

- Oui. 2. Billet de blog – Séries de dés impossibles à distribuer

> **SEO Mots-clés** – *Séquence la plus courte impossible de Rolls, Leetcode 2350, problème de codage d'interview, Java, Python, solution C++, analyse d'algorithme, temps O(n), espace O(k). *

---

♪ Séquences de dés impossibles à distribuer – Un code de leet Plongée profonde

> Pouvez-vous prédire le prochain rouleau ? (en milliers de dollars)
> Non – mais vous * pouvez * prédire * quelle séquence vous ne pourrez jamais
> formulaire. *
> C'est le coeur de LeetCode 2350: **Séquence la plus courte possible des rouleaux**.

### TL;DR

- **Ce que nous avons demandé**: Avec un tableau `rolls[i]` (résultats de dés) et un die avec
`k` faces (`1...k`), trouver la longueur `L` de la séquence *la plus courte* de longueur
`L` que **ne peut pas** être produit en tant que subséquence de `rolls`.
- **Idée de la solution**: Numériser une fois, compter combien de blocs contigus contiennent *tous*
"k" visages.
- **Réponse** : "blocs + 1".

---

- Oui. Pourquoi est-ce un problème ?

Raison
- Oui.
*Intuitive * Pensez à chaque ensemble complet de "k" visages distincts comme une couche
On peut contribuer à n'importe quelle séquence. Autres
**One-pass**= O(n) time – parfait pour les tests de stress d'entrevue. Autres
Un espace O(k) – seulement une poignée de drapeaux sont jamais nécessaires. Autres
**LeetCode-ready**
Python, C++. Autres

---

L'algorithme, étape par étape

1. **Initialize** `segments = 0` et un tableau vide set/flag.
2. **Itérer** par "rolls" :
- Ajoutez le rouleau actuel au jeu.
- Si la taille de l'ensemble devient "k", nous avons vu *chaque* visage.
- Augmentation des segments.
- Effacez le jeu pour commencer le prochain segment.
3. **Retour** "segments + 1".
La première longueur impossible est toujours une plus que le nombre de pleine
les segments que vous pouvez construire.

> **Analyse d'urgence** – Si un visage de `1...k` n'apparaît jamais, l'algorithme ne sera jamais
> appuyez sur `size == k` pour la première fois, `segments` reste `0` et la réponse
> devient correctement `1`.

---

Analyse de complexité

Valeur métrique
C'est pas vrai.
**Heure**="O(n)" – un passage au-dessus des "rolls". Autres
**L'espace**="O(k)" – un jeu/array qui suit le segment actuel des faces distinctes. Autres

---

- Oui. L'Ugly – Ce qui pourrait mal tourner

Question Comment l'éviter
-- -- -- -- -- -- -- --
Autres **Très grand `k`** (jusqu'à 100 000)
"k". Utilisez un `boolean[] vu` au lieu d'un hasch-set pour garder la mémoire
Oui. Autres
Chaque "ajout"/"clair" coûte un petit facteur constant. Pour
L'entretien, un `int[]` de taille `k+1` est plus rapide et plus prévisible. Autres
**Validation d'input**
Bibliothèque, vérifiez que `k >= 1` et `rolls` n'est pas nul. Autres

---

- Oui. Le bien – Pourquoi le Trick One-Pass Set gagne

1. **Clarité** – La logique est littéralement « collectionner des visages distincts ; quand
Compléter, compter une couche.
2. **Évolutabilité** – Travaux pour `n = 10^6`, `k = 10^5` en moins d'une seconde
les trois langues.
3. **Robustness** – Poignée tous les cas d'angle : faces manquantes, dupliquées
rouleaux, longs runs, etc. L'algorithme se soucie seulement de savoir si un ensemble complet
a été vu, pas environ *où* il se produit.

---

- Oui. Les mauvais – compromis

- **L'usage de la mémoire** grandit avec "k". Si `k` est énorme (-105) le jeu ou le tableau de drapeaux
occupera autant d'octets.
- **Hash-set vs. array** – En Java ou Python le jeu intégré est pratique mais
peut être plus lent qu'un petit tableau booléen.
- **Opération claire** – Effacer un jeu à plusieurs reprises est O(1) en moyenne, mais
alloue toujours un nouveau hash‐table en Java. Utilisation d'un tableau de drapeaux
le compteur évite une réaffectation.

---

- Oui. L'Ugly - Subtle Gotchas

Scénario Ce qui s'est mal passé
C'est ce qu'on dit.
"rolls" vide La boucle ne tourne jamais; `segments = 0` → répond `1` (correcte). Autres
- Oui. 1 ''Le jeu atteint toujours la taille 1 après le premier rouleau → `segments = 1 ',
La réponse `2` – qui est correcte parce que les séquences length‐1 sont toutes
C'est possible. Autres
`k` > nombre de valeurs distinctes dans `rolls`. Cette
Il identifie correctement qu'un seul rouleau est impossible. Autres

---

- Oui. 3. Comment utiliser le code

1. **Copier** l'extrait de la langue de votre choix dans le LeetCode
éditeur.
2. **Vérifier les échantillons fournis:

Texte
Entrée: rouleaux = [4,2,1,2,3,3,2,4,1], k = 4
Produit : 3
«» "

3. **Extendez** la solution si vous avez besoin de gérer plusieurs dés ou autre
contraintes – l'idée centrale reste la même.

---

- Oui. 4. A emporter pour votre prochaine entrevue

- ** Expliquez l'intuition** d'abord :
Nous ne pouvons pas former; chaque fois que nous voyons tous les visages `k` nous pouvons dire en toute sécurité n'importe quel
séquence de cette longueur est possible. (en milliers de dollars)
- **Afficher la solution à passe unique** – les intervieweurs aiment le temps linéaire, l'espace constant
Des tours.
- **Mention le cas de bord** où un visage n'apparaît jamais → répondre `1`.

Bon codage ! C'est ce qu'il a dit