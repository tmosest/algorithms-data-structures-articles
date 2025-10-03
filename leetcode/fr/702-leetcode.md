---
titre: LeetCode 702. Recherche dans un tableau trié de taille inconnue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code 702 : Recherche dans un tableau trié de taille inconnue
### Les bons, les mauvais et les méchants – Un guide complet d'entrevues et de préparation

> **Mots clés:** *LeetCode 702*, *recherche triée tableau taille inconnue*, *ArrayReader*, *recherche exponentielle*, *recherche binaire*, *question d'entrevue*, *solution de Java*, *solution de Python*, *solution de C++*, *entrevue d'algorithme*, *entrevue d'ingénieur logiciel*, *codage d'entrevue d'emploi*

---

Récapitulation des problèmes

> **LeetCode 702 – Recherche dans un tableau trié de taille inconnue* *
> On vous donne un tableau trié `secret` avec des éléments uniques, strictement croissants.
> La taille du tableau est inconnue et vous ne pouvez pas y accéder directement. Au lieu de cela, vous interagissez avec l'interface `ArrayReader` fournie:

Texte
int get(index de l'int)
«» "

* Si `index` est dans les limites, il retourne `secret[index]`.
* Si `index` est hors limites, il retourne `entier. MAX_VALUE` (ou `2^31-1`).

Vous devez écrire `search(ArrayReader reader, int target)` qui retourne l'index de `target` ou `-1` s'il n'existe pas, en utilisant **O(log n)** time et **O(1)** espace supplémentaire.

---

C'est vrai. Le Bon : Un Deux Propre et Élégant Solution de phase

1. **Agrandir la fenêtre de recherche (Recherche exploratoire)* *
* Commencez par `[gauche = 0, droite = 1]`.
* Alors que `get(right)` n'est pas en dehors des limites ** et** inférieure à la cible, double "droit".
* Cela nous garantit de finir par entrecroiser la cible entre `gauche` et `droite`.

2. **Binary Search Inside the Bracket**
* Recherche binaire classique avec `mid = gauche + (droite-gauche)/2`.
* Comparer `get(mid)` à la cible; ajuster `left`/`right` en conséquence.
* Arrêtez lorsque la valeur correspond ou que la fenêtre s'effondre.

Les deux phases s'exécutent ensemble dans `O(log T)` où `T` est le plus petit indice qui est soit la cible, soit le premier indice hors des limites – exactement le lien logarithmique requis.

C'est vrai. Pourquoi c'est génial

* **Simplicité :** Seulement deux boucles, aucune récursion.
* **Déterministe :** Pas de dépendance à la taille du tableau – il s'élève à 104 ou plus.
* **Efficacité de la mémoire:** Espace supplémentaire constant.
* ** Prêt pour l'industrie:** Fonctionne avec la véritable API de LeetCode `ArrayReader` (ou tout emballage qui se comporte de la même manière).

---

C'est vrai. Les mauvaises: les pièges communs à éviter

Pourquoi ça se brise
C'est pas vrai.
**L'accès à des indices hors frontières sans vérification**. Toujours tester `value == Integer.MAX_VALUE` avant de comparer à la cible. Autres
**Utiliser `When (get(right) < cible)` sans un contrôle lié. Arrête quand `get(right) == Integer.MAX_VALUE` ou lorsque le doublement déborderait `Integer. MAX_VALUE'. Autres
**Binary search `mid = (gauche + droite) / 2`**= Peut déborder pour de grands indices. Utiliser `mid = gauche + (droite - gauche) / 2`. Autres
**Returning `right` after loop**.Si la cible n'est pas trouvée, vous pouvez par erreur retourner un index valide. Autres
**Ignorer la propriété unique, augmenter strictement** Aucune action nécessaire; l'algorithme repose sur la monotonicité. Autres

---

C'est pas vrai. L'Ugly: Sur-Ingénierie & Tricks cachés

* **Recursive Binary Search** – Ajoute les frais généraux et le risque de débordement de la pile pour de très grandes gammes.
* **Pre-fetching the array size** – Impossible sous les contraintes du problème; essayer de le faire va à l'encontre du but.
* **Binary Search sur `Integer.MAX_VALUE`** – Traiter le sentinelle comme une valeur régulière peut conduire à des boucles infinies si elles ne sont pas manipulées avec soin.
* ** Utilisation `Math.min` pour `mid`** – inutile et plus lent que la formule sûre.

> **Ligne de bottom:** Gardez-le *simple* et *robust*. Toute astuce qui complique le code ne fera que blesser votre score d'entrevue.

---

Code complet – Java, Python et C++

> **Note:** Toutes les implémentations utilisent la même stratégie en deux phases. Les extraits de code ci-dessous sont prêts à être collés dans votre boîte de soumission IDE ou LeetCode.

---

#### 5.1 Java (Présentation de code à gauche)

"Java
***
* Ceci est l'interface API de ArrayReader.
* Vous ne devriez pas l'implémenter, ni spéculer sur sa mise en œuvre.
*/
interface ArrayReader {
public int get(index d'int);
}

solution de classe {
recherche publique d'int (lecteur d'ArrayReader, cible int) {
// 1/ 1/ Recherche exponentielle pour trouver une liaison qui contient définitivement la cible
int gauche = 0, droite = 1;
alors que (vrai) {
int val = reader.get(à droite);
si (val) l'entier.MAX_VALUE.
gauche = droite;
droite <<= 1; // double la fenêtre
si (droite < 0) { //
droite = entier.MAX_VALUE;
pause;
}
}

La recherche binaire classique dans [gauche, droite]
pendant que (gauche <= droite) {
int milieu = gauche + (droite - gauche) / 2;
int midVal = reader.get(mid);

si (midVal) la cible revient au milieu;
i (midVal == Integer.MAX_VALUE=" milieu de Val > cible) {
droite = milieu - 1;
} autre {
gauche = milieu + 1;
}
}
retour -1; // non trouvé
}
}
«» "

---

5.2 Python

'`python
♪ L'interface ArrayReader est fournie par LeetCode
# classe ArrayReader:
# def get(self, index: int) -> Int: ...

Solution de classe:
def search(self, reader: 'ArrayReader', cible: int) -> Int:
gauche, droite = 0, 1

# Expansion exponentielle du lien droit
alors que Vrai:
val = reader.get(à droite)
Si la valeur est >= cible:
pause
gauche = droite
droite <<= 1 # double la fenêtre
si droite >= 2**31 - 1: # éviter le débordement
droite = 2**31 - 1
pause

# Recherche binaire à portée limitée
alors que gauche <= droite:
milieu = gauche + (droite - gauche) // 2
mid_val = reader.get(mid)

if mi_val == cible & #160;:
retour
si mi_val == 2**31 - 1 ou mi_val > cible:
droite = milieu - 1
Sinon:
gauche = milieu + 1

retour -1
«» "

---

C++

'`cpp
// Assumer ArrayReader est défini comme suit:
// classe ArrayReader {
// public:
// Int get(index d'int);
// };

solution de classe {
public:
recherche int(ArrayReader &reader, cible int) {
int gauche = 0, droite = 1;

// Recherche exponentielle pour trouver une limite supérieure
alors que (vrai) {
int val = reader.get(à droite);
si (val) la val >= cible est cassée;
gauche = droite;
droite <<= 1; // double la fenêtre
si (droite < 0) { //
droite = INT_MAX;
pause;
}
}

// Recherche binaire dans [gauche, droite]
pendant que (gauche <= droite) {
int milieu = gauche + (droite - gauche) / 2;
int midVal = reader.get(mid);

si (midVal) la cible revient au milieu;
si (midVal == INT_MAX=" milieu de Val > cible) {
droite = milieu - 1;
} autre {
gauche = milieu + 1;
}
}

retour -1; // cible non trouvée
}
};
«» "

---

Analyse de complexité

Étapes Complexité temporelle Complexité spatiale Autres
-- -- -- -- -- -- -- -- -- -- -- --
Recherche exponentielle **O(log k)** (k = indice de la cible ou de la première destination)
Recherche binaire
**O(log k)**

*L'algorithme répond au temps d'exécution `O(log n)` et à l'espace supplémentaire constant requis. *

---

### 7--Des conseils d'entrevue

Conseil Explication
C'est pas vrai.
**Expliquez les deux phases en amont** Autres
**Mention la sentinelle ('Intégrée. MAX_VALUE')**=Clarifie la manipulation des liaisons extérieures. Autres
**Discuss ledge cases**= Tableau vide (non autorisé par les contraintes), cible inférieure au premier élément, cible supérieure au dernier élément. Autres
Autres Pourquoi `mid = gauche + (droite - gauche)/2` est plus sûr que `(gauche + droite)/2`. Autres
Autres **Afficher le code dans votre langue préférée**= Si les intervieweurs préfèrent Java, Python ou C++, soyez prêts à l'écrire en direct. Autres

---

- Oui. Comment cela va-t-il vous mettre à la recherche d'un emploi

* **LeetCode Mastery:** Problème 702 est un favori classique d'interview de -qui montre votre compréhension de la recherche binaire, la recherche exponentielle et la manipulation sentinelle.
* ** Confiance algorithmique :** L'approche en deux phases démontre une façon systématique de traiter les tailles inconnues – un modèle qui apparaît dans de nombreux systèmes du monde réel.
* **Multi-Language Proficiency:** Fournir des solutions Java, Python et C++ prouve que vous êtes polyvalent et prêt pour diverses bases de code.
* **Blogue optimisé sur le référencement:** En publiant un article détaillé, vous augmentez votre visibilité sur les moteurs de recherche – les recruteurs cherchent souvent des solutions de type LeetCode 702 ou de type Recherche de taille inconnue.
* ** Portfolio Boost :** Ajoutez le code et le billet de blog à votre GitHub et LinkedIn. Étiquetez le dépôt avec `leetcode`, `array-search`, `binary-search`, `algorithm-interview`.

---

C'est pas vrai. Dernier départ

Le problème 702 est soluble avec une solution ** courte, robuste et logarithmique. Évitez la suringénierie, gardez à l'esprit les débordements et traitez toujours `Integer. MAX_VALUE` comme sentinelle. Avec le code ci-dessus et la stratégie d'entrevue décrite, vous êtes parfaitement équipé pour répondre à cette question – et pour vous faire remarquer par les gestionnaires d'embauche.

Bon codage – et que vos entrevues soient aussi propres et efficaces que cette solution! C'est ce qu'il a dit.

---