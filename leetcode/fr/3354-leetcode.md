---
titre: LeetCode 3354. Faire des éléments d'array égaux à zéro -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le Code – 3 langues en une

Ci-dessous vous trouverez trois implémentations **ready‐to-copy** qui résolvent LeetCode 3354 – Faire des éléments d'array égaux à zéro – dans **Java, Python et C++**.
Les trois solutions fonctionnent dans *O(n)* temps et utilisent seulement *O(1)* mémoire supplémentaire.

> **Pourquoi cela compte pour votre entrevue* *
> • La solution est un algorithme monopass, espace constant – un favori d'interview.
> • Il présente une compréhension claire de **préfixe des sommes** et de la manipulation des cas de bord.
> • Le code est propre, bien commenté et suit les directives de codage que la plupart des intervieweurs recherchent.

---

#### 1.1 Java (classe de LeetCode de Solution)

"Java
***
* 3354. Faire des éléments de tableau égaux à zéro
* https://leetcode.com/problèmes/make-array-elements-egal-to-zero
*/
solution de classe {
nombre d'entrées publiquesValidSelections(int[] nombres) {
int n = longueur nums;
= 0;
pour (int v : nombres) total += v; // somme totale du tableau

int leftSum = 0; // somme des éléments restant de l'indice courant (exclusif)
Int droite Somme = total; // somme des éléments de l'indice actuel à la fin (inclus)

réponse int = 0;
pour (int i = 0; i < n; ++i) {
rightSum -= nombres[i]; // maintenant à droite La somme est la somme des éléments strictement droits de i

si (nums[i] != 0) { // Les éléments non nuls ne sont pas pertinents pour les positions de départ
gauche Somme += nombres[i];
poursuivre;
}

/*
* En position zéro, nous devons vérifier la différence
* entre la somme des éléments à gauche et la somme à droite.
*
* Condition 1: gauche Somme == droiteSum -> les deux directions sont valables
* État 2 : Une seule direction fonctionne
*/
si (leftSum == droiteSum) {
réponse += 2;
} sinon si (Math.abs(leftSum - droiteSum) == 1) {
réponse += 1;
}

leftSum += nums[i]; // inclure le zéro lui-même pour les étapes suivantes
}

réponse de retour;
}
}
«» "

---

#### 1.2 Python (Python 3)

'`python
Solution de classe:
def countValidSelections(self, nombres: list[int]) -> Int:
total = somme(s)
gauche_sum = 0 # éléments restants de i
right_sum = total des éléments # de i à fin

ans = 0
pour v en chiffres:
right_sum -= v # now `right_sum` est strictement à droite

si v: # sauter les entrées non nulles – elles ne peuvent pas être un point de départ
gauche_sum += v
poursuivre

if left_sum == right_sum :
+= 2
elif abs(left_sum - right_sum) == 1 :
+= 1

left_sum += v # inclut le zéro lui-même

retour et
«» "

---

*## 1.3 C++ (fonction unique)

'`cpp
***
* 3354. Faire des éléments de tableau égaux à zéro
* https://leetcode.com/problèmes/make-array-elements-egal-to-zero
*/
nombre d'entréesValidSelections(vecteur<int>& nombres) {
long total = 0;
pour (int v : nombres) total += v; // utiliser longtemps pour éviter le débordement

longue gauche = 0; // somme des éléments restant de l'indice actuel
long droit = total; // somme des éléments de l'indice actuel à la fin

int res = 0;
pour (int i = 0; i < nums.size(); ++i) {
right -= nums[i]; // supprimer l'élément courant – right est maintenant strictement à droite

si (nums[i] != 0) {
à gauche += nombres[i];
poursuivre;
}

si (gauche == droite) res += 2;
Sinon, si (lambs(gauche - droite)) 1) res += 1;

gauche += nombres[i]; // inclure le zéro pour la prochaine itération
}
retour rés;
}
«» "

> *Astuce – pour la solution C++, vous pouvez aussi laisser tomber les `labs` en utilisant `abs(gauche - droite)`; le compilateur va promouvoir `int`.
> Le "long long" garde le code en toute sécurité pour la somme la plus défavorable (n ≤ 200 000, a[i] ≤ 109). *

---

- Oui. 2. Le fonctionnement de l'algorithme – Le 3-minute

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
Autres **1**= Calculer la somme *total* du tableau (`total`). Autres Les règles garantissent que le nombre total de diminutions correspond au nombre total d'augmentations, donc la somme totale est une constante utile. Autres
Autres **2**= Marchez une fois dans le tableau, en maintenant deux sommes courantes : `leftSum` (à gauche de l'indice actuel) et `rightSum` (à droite de l'indice actuel). Ces deux valeurs sont les *efficaces* charge de chaque côté d'un zéro ; elles décident quelle direction(s) peut(nt) effacer le tableau. Autres
Autres À une position zéro: *si* `leftSum == droiteSum` → **les deux** mouvements gauche et droite sont valides → «+2». *Sommeil de gauche - droite 1` → **on** direction fonctionne → Les règles de mouvement forcent le pointeur à franchir un premier pas sur le côté plus large; une différence de 1 garantit que exactement une direction peut compenser la valeur supplémentaire. Autres
Autres Mise à jour des montants d'exécution pour l'élément suivant (`leftSum += nums[i]`). Autres

> **Complexités**
> • *Time*: **O(n)** – chaque élément est traité une seule fois.
> • *Espace* : **O(1)** – seulement une poignée de variables entières sont utilisées.

---

- Oui. 3. L'article du blog – --Bon, mauvais, lugubre avec Job‐Search‐ Prêt SEO

> **Titre (SEO)* *
> **Cracking LeetCode 3354 – Les éléments d'interprétation de l'image égale à zéro (Java, Python, C++)* *

> **Méta—Description* *
> Découvrez comment résoudre le LeetCode 3354 en Java, Python et C++ en un seul passage avec l'espace O(n) et O(1). Comprendre les montants préfixés, la manipulation des cas de bord, et comment ce problème peut stimuler votre CV d'entrevue. (en milliers de dollars)

3.1 Introduction

Les entrevues dépendent souvent de votre capacité à *penser clairement, coder proprement et expliquer votre raisonnement. *
LeetCode 3354 est une vitrine parfaite des trois compétences. La tâche est fallacieusement simple : étant donné un tableau d'entiers qui contient au moins une `0`, compter **tous** positions de départ possibles **et** la direction de première étape (`+1` ou `-1`) qui, en suivant les règles prescrites par le décret, réduira l'ensemble du tableau à zéro.

**Takeaway clé pour les recruteurs** – la solution est un scan linéaire unique avec stockage auxiliaire constant – un modèle d'entrevue classique.

---

### 3.2 Le "Bien" – Ce que vous aimez à propos de ce problème

1. **Temps linéaire, espace constant* *
L'algorithme à un passage est un élément essentiel des entrevues de codage. Il indique que vous pouvez optimiser pour la vitesse et la mémoire – les deux traits précieux dans l'ingénierie logicielle.

2. **Sommes préfixes, pas de tableaux supplémentaires**
La solution utilise des totaux d'exécution (`leftSum` et `rightSum`) au lieu de construire des tableaux préfixes complets. Cela démontre une compréhension profonde de *préfixe sum* tours que les intervieweurs demandent souvent.

3. ** Logique de décision claire**
Les deux conditions simples - "gauche == droite" (deux directions) et "gauche - droite" == 1` (une direction) – sont faciles à raisonner et peuvent être expliqués en moins d'une minute. Les intervieweurs aiment les solutions qui peuvent être verbalisées succinctement.

4. **Language-agnostique**
La même logique peut être exprimée en Java, Python ou C++. En mettant en avant cette polyvalence, vous êtes à l'aise avec plusieurs piles – un avantage dans une équipe polyglotte moderne.

---

### 3.3 Le "Bad" – Pièges communs que vous devriez éviter

Trouver ce qui arrive Comment réparer
- C'est quoi ?
En supposant que le premier zéro est important. Il faut passer du premier zéro à la fin, mettre à jour « leftSum » et «rightSum» pour *chaque* zéro. Autres
**Mettre à jour les montants de l'ordre incorrect**Le "rightSum" devrait exclure l'élément courant avant la vérification. Soustraire "nums[i]` *avant* l'évaluation de la condition zéro. Autres
**L'utilisation de l'eau longue par rapport à l'eau intérieure**L'utilisation de l'eau est excessive pour les gros intrants (`n ≤ 200 000`, `a[i] ≤ 109`). Autres
**L'ajout de 2 pour chaque somme égale peut faire double compte lorsque `gauche == droite` et `=diff=] 1' simultanément. Les conditions sont exclusives; utiliser "si/d'autres si". Autres
**Mis-reading , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , , Autres

---

### 3.4 L'Ugly - L'approche de la force brute (Pourquoi c'est un non-aller)

Une approche tentante mais désastreuse est de:

1. **Simulez le processus** pour chaque zéro et pour les deux directions.
2. **Appliquez la règle de décrément/ incrément** étape par étape jusqu'à ce que le tableau se stabilise ou que la simulation décroisse.

Cette méthode naïve est **O(n2)** dans le pire des cas (chaque élément pourrait être visité plusieurs fois). Il sera *time-out* sur les limites de LeetCode.

> **Leçon** – toujours chercher un raccourci mathématique (préfixer les sommes, les soldes, les invariants) avant d'écrire une simulation.

---

3.5 Quoi mettre en évidence dans votre entrevue

* **Énoncer l'invariant** – À tout zéro, la différence entre la somme des éléments de gauche et les éléments de droite détermine les directions valables. (en milliers de dollars)
* ** Expliquer la complexité temporelle** – une seule boucle, aucune opération imbriquée.
* **Mention l'optimisation de l'espace** – pas de tableaux supplémentaires, juste quelques entiers.
* **Afficher le code propre** – utiliser des noms de variables descriptives (`leftSum`, `rightSum`) et des commentaires concis.

Vous pouvez même mettre en avant le "first-zero trick"* si vous voulez impressionner un recruteur qui aime les astuces intelligentes : calculer `leftSum` jusqu'au premier zéro, `rightSum` de ce zéro à la fin, et glisser la fenêtre vers l'avant.

---

3.6 Pensée finale

LeetCode 3354 est un problème *tiny* avec *big* valeur d'enseignement:

* Il montre comment transformer une règle de type jeu en une simple condition arithmétique.
* Il montre la maîtrise des sommes de préfixe, un agrafe de nombreux problèmes d'entrevue (par exemple, Subarray Maximum, Recherche de somme de préfixe).
* Il souligne l'importance de gérer les cas de bord – zéros au début, à la fin ou au milieu du tableau.

Lorsque vous touchez ce problème dans une entrevue, passez par la logique sur papier d'abord, puis traduisez-le en code propre. De cette façon, vous démontrerez *la clarté de la pensée*, *la perspicacité algorithmique* et *la discipline de codage* – qui sont toutes la sainte trinité d'une forte performance d'entretien d'ingénierie logicielle.

Bonne chance ! C'est ce qu'il a dit.

---

- Oui. 4. Comment utiliser cet article dans votre recherche d'emploi

* **Ajoutez les extraits de code à votre portfolio** – nommez le dépôt.
* **Écrire une courte entrée de blog sur votre site personnel** – utilisez l'article ci-dessus et donnez-lui un titre convaincant.
* **Mention sur LinkedIn** – poster un court carrousel: Code du leet 3354 – La solution One-Pass en Java, Python et C++. (en milliers de dollars)
* ** Leverage the SEO tags** – ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

En vous positionnant comme un candidat qui connaît à la fois le *math* derrière les algorithmes et le *craft* du code, vous vous démarquerez dans la mer des candidats.

---

*Sentez libre de modifier le libellé ou les noms variables pour correspondre à votre style personnel ; la preuve de la logique et de la complexité de base brillera encore à travers. *