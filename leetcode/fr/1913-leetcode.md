---
titre: LeetCode 1913. Différence maximale de produit entre deux paires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 1913 – Différence de produit maximale entre deux paires

** Exposé des problèmes* *
> Étant donné un tableau entier `nums`, choisissez quatre indices distincts `w, x, y, z` de sorte que la différence de produit
> \[(nums[w] * nums[x]) - (nums[y] * nums[z]\]
> est optimisé.
> Retourne cette différence de produit maximale.

> **Constraints**
> * < 4 ≤ longueur maximale ≤ 104 "
> * `1 ≤ nombres[i] ≤ 104`

Le but est de choisir **les deux plus grands nombres** pour une paire et **les deux plus petits nombres** pour l'autre paire – ce qui donne toujours la différence maximale.

---

- Oui. 2. Algorithme (temps O(N), espace O(1))

1. **Trouver les deux plus grands nombres** `max1 ≥ max2`.
2. **Trouver les deux plus petits nombres** "min1 ≤ min2".
3. Retour `max1 * max2 - min1 * min2`.

Parce que le tableau peut contenir des duplicatas, nous choisissons toujours des indices distincts – l'algorithme fonctionne aussi pour cela.

---

- Oui. 3. Mise en œuvre des références

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.
N'hésitez pas à copier-coller dans votre environnement IDE ou interview.

---

#### 3.1 Java

"Java
***
* 1913. Différence maximale de produit entre deux paires
* Heure O(N), espace O(1)
*/
solution de classe publique {
Int public maxProductDifference(int[] nums) {
// Deux valeurs les plus importantes
int max1 = entier.MIN_VALUE, max2 = entier.MIN_VALUE;
// Deux valeurs les plus faibles
int min1 = entier.MAX_VALUE, min2 = entier.MAX_VALUE;

pour (int n : nombres) {
// Mettre à jour les deux plus importants
si (n > max1) {
max2 = max1;
max1 = n;
} sinon si (n > max2) {
max2 = n;
}

// Mettre à jour les deux plus petits
si (n < min1) {
min2 = min1;
min1 = n;
} sinon si (n < min2) {
min2 = n;
}
}

retour max1 * max2 - min1 * min2;
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def maxProduit Différence(même, nombres: Liste[int]) -> Int:
# Initialiser les extrêmes
max1 = max2 = -1 # plus grand deux
min1 = min2 = 10 ** 5 + 1 # plus petit deux

pour n en nombres:
# Deux plus grands
si n > max1:
max2, max1 = max1, n
elif n > max2:
max2 = n

# Deux plus petits
si n < min1:
min2, min1 = min1, n
elif n < min2:
min2 = n

retour max1 * max2 - min1 * min2
«» "

---

### 3.3 C++

'`cpp
***
* 1913. Différence maximale de produit entre deux paires
* Heure O(N), espace O(1)
*/
solution de classe {
public:
Int maxProductDifférence(vecteur<int>& nombres) {
int max1 = INT_MIN, max2 = INT_MIN;
int min1 = INT_MAX, min2 = INT_MAX;

pour (int n : nombres) {
// plus grand deux
si (n > max1) {
max2 = max1;
max1 = n;
} sinon si (n > max2) {
max2 = n;
}

// Deux
si (n < min1) {
min2 = min1;
min1 = n;
} sinon si (n < min2) {
min2 = n;
}
}

retour max1 * max2 - min1 * min2;
}
};
«» "

---

- Oui. 4. Article de blog: -Le bon, le mauvais, et l'indulgence de LeetCode 1913

> **Titre:** *Cracking LeetCode 1913: Le Bon, le Mauvais et le Ugly – Un guide convivial pour l'entrevue*
> **Meta Description:** Master LeetCode 1913 en quelques minutes. Apprenez la solution O(N), les pièges, et comment l'accrocher dans votre prochaine entrevue de codage.

4.1 Introduction
Les problèmes de LeetCode sont le rite de passage pour quiconque chasse un rôle d'ingénierie logicielle.
Problème **1913 – Différence maximale de produit entre deux paires** est étiqueté **Facile**, mais c'est un grand moment d'enseignement pour:

* **O(N) conception d'algorithme** – pas de tri, juste un seul passage.
* **Manipulation soignée des boîtiers de bord** – duplicatas, petits tableaux, grands nombres.
* **Lisibilité du code** – variables qui disent ce qu'elles sont.

Si vous pouvez articuler clairement la solution dans une entrevue, vous impressionnerez les gestionnaires d'embauche.

---

4.2 Les bonnes: Pourquoi Ce problème est un gagnant

Caractéristiques Pourquoi ça compte
C'est-à-dire
**Straightforward O(N) solution** Autres
Autres **Aucun espace supplémentaire n'est nécessaire** Autres
**Intution mathématique claire**=Le choix des plus grands deux et des plus petits deux se sent évident== une fois que vous l'avez expliqué. Autres
**L'assistance linguistique multiple** Autres
**Bonne testabilité**= Petite entrée, sortie déterministe – facile à tester. Autres

Si vous réussissez ce problème, vous pouvez en toute confiance passer au niveau suivant (Moyen/Hard) sachant que vous avez maîtrisé les fondamentaux.

---

### 4.3 Les mauvaises: pièges communs

Piège
- Oui.
**Le tri est O(N log N); inutile lorsqu'un seul balayage suffit. Autres
**Utiliser seulement deux variables pour les extrêmes** L'oubli mène à une mauvaise réponse. Autres
**En supposant que les indices soient uniques**. Notre logique de passage unique respecte cela. Autres
**Overflow in languages with fixed int size**.Dans C++/Java, `int` est 32-bit; produit de deux 104 nombres correspond (108), si sûr. Autres
**Caisse Edge : la longueur du tableau exactement 4** uvre encore – les deux plus grands et les deux plus petits sont les quatre nombres eux-mêmes. Autres

---

#### 4.4 L'Ugly: Un Tricky

Certains intervieweurs aiment tordre légèrement le problème:

> *Et si nous voulions la différence de produit **minimum**? *

La réponse serait simplement inverser les rôles : choisir les deux plus grands pour le produit *plus petit* et les deux plus petits pour le produit *plus grand*. C'est un exercice mental rapide pour tester à quel point vous comprenez la logique de base.

---

4.5 Écrire un entretien-emploi Explication prête

1. **Énoncer clairement le problème** – *=Avec un tableau, choisir quatre indices distincts pour maximiser `(a*b)-(c*d)`.
2. ** Expliquer l'intuition** – Le produit de deux nombres est maximisé par les deux plus grands, minimisé par les deux plus petits.
3. **Ouvrez l'algorithme** – *=Single pass, gardez quatre extrêmes.
4. **Discuse la complexité** – *(O(N) temps, O(1) espace.
5. **Voir le code** – Choisissez la langue avec laquelle vous êtes le plus à l'aise. (Java, Python, code C++ ci-dessus.)
6. **Parler des cas de bord** – **Dupliquer, taille minimale du tableau, grandes valeurs.
7. **Tronde facultative** – **Et si nous avions besoin de la différence minimale?

Gardez votre explication courte (1 minute) mais pleine de profondeur technique. C'est l'endroit idéal pour la plupart des gestionnaires d'embauche.

---

4.6 SEO et conseils de carrière

Pourquoi ça marche ?
C'est pas vrai.
Les personnes qui cherchent cette phrase exacte veulent la réponse. Autres
*= Entrevue sur la différence de produit maximale*= Ajoute le contexte de l'entrevue, augmente la pertinence pour les recruteurs. Autres
L'algorithme O(N) LeetCode*L'efficacité est une qualité d'entretien clé. Autres
Java/Python/C++ Solutions de LeetCode Autres

**Conseil de carrière:**
- Publiez un billet **blog** (comme celui-ci) et partagez sur LinkedIn, Twitter ou dev blogs.
- Marquez-le avec `#LeetCode`, `#CodingInterview`, `#LogicielEngineering`.
- Relier à votre dépôt GitHub contenant les solutions propres.

Les recruteurs aiment voir des candidats qui *enseignent* – cela prouve une compréhension et une communication profondes.

---

4.7 Liste de contrôle finale avant votre prochaine entrevue

1. Mettre en œuvre la solution O(N) dans votre langue préférée.
2. Écrire les tests unitaires pour les cas de bord (`[1,1,1,1]`, `[10000,1,19999]`).
3. Soyez capable d'expliquer l'algorithme en 60 secondes.
4. Connaître le *pourquoi* – pas seulement le *quoi*.
5. Préparez un extrait de code de démonstration sur un tableau blanc ou un ordinateur portable.

Bonne chance ! C'est ce qu'il a dit.

---

**Mots clés:** LeetCode, différence maximale de produit, solution O(N), entretien de codage, solution Java, solution Python, solution C++, entretien d'ingénierie logicielle, entretien d'algorithme, entretien d'emploi, préparation d'entrevue.