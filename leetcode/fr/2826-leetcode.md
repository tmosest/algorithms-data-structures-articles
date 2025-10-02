---
Titre: LeetCode 2826. Tri de trois groupes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 2826 – **Trois groupes de triés**
**Un guide complet et optimisé pour les intervieweurs et les candidats* *

Langage Complexe Durée Espace
- C'est quoi ?
**Java******O(n)**
**Python******O(n)**
*C++******O(n)**

> **Pourquoi ce problème est important* *
> Trier un petit alphabet fixe (1, 2, 3) est un motif DP classique. C'est une question d'entrevue courante sur *LeetCode*, *InterviewBit*, *HackerRank*, et de nombreuses entrevues de niveau supérieur.
> La maîtrise de ce problème montre que vous comprenez :
> * Programmation dynamique sur les petits espaces d'état
> * Préfixe / suffixes astuces
> * Comment réduire une solution "O(n3)" de force brute au temps linéaire

---

- Oui. 1. Exposé des problèmes

> **On vous donne un tableau entier `nums`. Chaque élément est soit `1`, `2`, ou `3`**.
> En une seule opération, vous pouvez **supprimer** n'importe quel élément.
> Retourner le nombre minimum d'opérations nécessaires pour faire des "nums" **non-diminution** (c'est-à-dire toutes les "1", puis toutes les "2", puis toutes les "3").

**Exemples**

Nombres d'opérations minimales Raison
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Enlever "2,3,2" ou tout triple optimum
Supprimer `3` et `2` (les deux moyennes)
"[2,2,2,3,3]"" "0"" Déjà triés

**Contrôles* *

* `1 ≤ longueur nominale ≤ 100`
* "nums[i] " {1, 2, 3} "

> **Suivi :** Atteindre le temps O(n) et l'espace O(1).

---

- Oui. 2. Intuition Brute-Force

Si nous choisissons un point de division `i` pour la fin du bloc `1`s et un point de division `j` pour la fin du bloc `2`s, nous pouvons compter combien d'éléments se trompent dans chaque bloc.
Itération sur toutes les boucles `i, j` donne `O(n2)`, chaque erreur de comptage dans `O(n)` temps → `O(n3)`.
Avec des sommes préfixées, nous pouvons apporter cette boucle intérieure à `O(1)`, en donnant `O(n2)`.

C'est *bon* pour enseigner l'idée d'une partition à trois segments, mais c'est trop lent pour les grands `n` (les contraintes officielles ne permettent que 100, donc il passe, mais il est toujours un mauvais modèle pour la préparation d'entrevues).

---

- Oui. 3. L ' optimum " O(n) " Solution DP

3.1 Aperçu

Lorsque nous balayons le tableau de gauche à droite, nous pouvons maintenir trois valeurs :

Sens de la variable
C'est pas vrai.
Suppressions minimales pour rendre tous les éléments visibles **seulement 1**
"b" : suppressions minimales pour rendre les éléments visibles **non-diminution 1 → 2**
Autres `c`= Suppressions minimales pour rendre les éléments visibles **non-diminution 1 → 2 → 3**=

Lorsque nous voyons un nouvel élément `x` (`1`, `2` ou `3`), nous mettons à jour les variables:

1. **Toutes les années**
«a += (x != 1) – nous le supprimons si ce n'est pas un 1.
2. **1 → 2**
`b = min(a, b + (x != 2))»
*Either* nous le conservons dans le bloc `2` (`b + (x != 2)»,
*ou * nous décidons de la laisser tomber de tout le préfixe ('a').
3. **1 → 2 → 3**
`c = min(b, c + (x != 3))»
De même, gardez-le dans le bloc `3` ou laissez tout tomber jusqu'ici.

Après traitement de tous les éléments `c` contient les suppressions minimales pour obtenir l'ordre trié.

3.2 Pourquoi ça marche

* Chaque variable représente une solution optimale pour un préfixe du tableau.
* La répétition pour `b` et `c` examine deux possibilités:
* l'élément courant appartient au groupe suivant, ou
* nous commençons le groupe suivant plus tard (donc nous revenons à la valeur optimale précédente).
* Parce que nous gardons toujours le meilleur de ces deux options, nous conservons l'optimalité.

3.3 Complexité

* **Time** – Une passe sur le tableau: `O(n)`.
* **Espace** – Trois entiers: "O(1)".

---

- Oui. 4. Code – Trois langues

Voici des implémentations propres et prêtes à la production pour **Java**, **Python** et **C++**.
Tous utilisent la même logique de PDD, commentée pour plus de clarté.

#### 4.1 Java

"Java
Importer java.util. Liste;

solution de classe publique {
Opérations publiques (liste <entier> nombres) {
int a = 0, b = 0, c = 0; // États DP décrits ci-dessus

pour (int x : nombres) {
a += (x == 1) ? 0 : 1; // garder 1's
b = Math.min(a, b + ((x == 2) ? 0 : 1)); // garder 2's
c = Math.min(b, c + ((x == 3) ? 0 : 1)); // garder 3's
}
retour c;
}
}
«» "

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def minimumOperations(self, nombres: List[int]) -> Int:
a = b = c = 0 # États DP

pour x en nombres:
a = 0 si x == 1 autre 1
b = min(a, b + (0 si x == 2 autres 1))
c = min(b, c + (0 si x == 3 autres 1))
retour c
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int minimumOpérations(std:vector<int>& nums) {
int a = 0, b = 0, c = 0; // États DP

pour (int x : nombres) {
a += (x == 1) ? 0 : 1;
b = md::min(a, b + ((x == 2) ? 0 : 1));
c = md::min(b, c + (x ==3) ? 0: 1));
}
retour c;
}
};
«» "

---

- Oui. 5. Une marche pas à pas (Démonstration de Java)

"Java
Liste<entier> arr = Liste de(2, 1, 3, 2, 1);
int ops = nouvelle solution().minimumOpérations(arr);
Système.out.println(ops); // impressions 3
«» "

Étape
C'est pas vrai.
Début
Lire
Lire comme suit :
Lire 3
Lire 2
Lire la réponse Deux ? Contrôle d'attente – Le tableau `[2,1,3,2,1]` rendements 3.

> **Note:** La démo montre l'algorithme en action – une ligne de code unique pour chaque mise à jour DP le rend convivial pour les entrevues.

---

- Oui. 5. Un bon, mauvais, mauvais débat

Aspect du bien
- C'est quoi ?
**Space d'Etat**= Petit DP fixe (3 entiers) – très élégant== Aucune=
**Les mises à jour DP sont un liner, mais utilisent des expressions ternaires pour la clarté.
**Échelle**= Temps linéaire et espace constant – l'épreuve future pour les plus grands `n`= Brute-force `O(n2)` peut obtenir TLE sur 105 tests de taille.
Autres **Test Coverage**= Fonctionne pour tous les cas de bord (tous les 1's, tous les 2's, tous les 3's, motifs alternés)== Brute-force peut manquer le cas où vous devez supprimer *tous* éléments d'un groupe==
**Pièges potentiels**= Oublier de mettre à jour `a` d'abord (doit utiliser l'optimum précédent lors du calcul `b`) Aucun
Aucun – seulement des ints primitifs Aucun

> **Dans une interview** vous devez d'abord expliquer la récurrence du DP, écrire le pseudocode, puis le convertir en code.
> **Pourquoi les candidats l'adorent :** il démontre que vous pouvez penser *bottom-up* et gérer une commande multi-étapes avec seulement trois états.

---

- Oui. 6. Bonus – Sous-séquence de non-décroissement la plus longue (PDL) Affichage

> **Alterner le point de vue :**
> Le problème équivaut à trouver la longueur de la plus longue sous-séquence non décroissante (LNDS) et à la soustraire de «n».
> Parce que l'alphabet est seulement `12,3`, le LNDS est exactement le nombre d'éléments qui peuvent rester.
> Le PDD décrit ci-dessus calcule essentiellement la longueur du PNDS* à la volée.

**Pourquoi nous n'utilisons pas un 'O(n2)' Algorithme LIS**
Le «O(n2)» La solution LIS fonctionne pour n'importe quel alphabet mais est *overkill* ici – le DP ci-dessus est à la fois plus rapide et plus élégant.
Cependant, montrer que vous pouvez déduire les deux montre une compréhension profonde.

---

- Oui. 7. Liste de contrôle pour la préparation des entrevues

Thème Comment trier trois groupes teste-t-il
-- -- -- -- -- -- ----------------------------------
**La programmation dynamique**
**Préfixe/Suffixe Pensée**
**Greedy / Two-Pointer**.Ce n'est pas directement applicable, mais vous pouvez expliquer pourquoi une cupidité.
**Complexité temps/espace**
Autres **Codage Style** Autres

**Conseils pour le succès**

1. ** Expliquez les variables PD en amont.**
Nous avons trois comptoirs – tous les compteurs, 1→2, 1→2→3.
Les intervieweurs aiment les candidats qui articulent l'état.
2. **Afficher la récurrence explicitement. **
Écrire `b = min(a, b + (x != 2))` sur le tableau blanc.
Cela démontre la pensée *branche et liée*.
3. ** Audit de complexité. **
Après le code, passez rapidement à travers `O(n)` et `O(1)` pour satisfaire pourquoi c'est optimal.

---

- Oui. 8. SEO-Optimized Blog Tips

1. ** Mots-clés principaux** – *LeetCode 2826 Tri de trois groupes*, * Solution linéaire PD*, *Problèmes d'entrevue PD*.
2. ** Mots-clés secondaires** – *Trier un petit alphabet*, *préfixer les montants DP*, *supprimer les éléments triés tableau*, *coder les modèles d'entrevue*.
3. **Meta Description** – ♫Solve LeetCode 2826 Tri de trois groupes en Java, Python et C++ avec un algorithme O(n) DP. Étape par étape, code et stratégie d'entrevue. (en milliers de dollars)
4. **En-têtes** – Utiliser `H1`, `H2`, `H3` à la structure. Les moteurs de recherche se classent bien avec des titres descriptifs clairs.
5. **Images / Code Snippets** – Intégrer les extraits de code comme blocs de code clôturés (comme indiqué).
6. **La section FAQ** – Puis-je résoudre cela avec 2 points? – Réponse: non, parce que nous supprimons les éléments, pas l'échange.
7. **Lien avec le problème de LeetCode** – Fournir une URL directe: `https://leetcode.com/problèmes/sorting-trois-groups/`.
8. **Appel à l'action** – Essayez-le sur LeetCode, soumettez votre solution et partagez sur LinkedIn.

---

- Oui. 9. Dernier départ

Trier un alphabet fixe de taille trois est un *micro‐ Un problème de DP* qui s'applique aux alphabets plus grands.
L'"O(n)" La solution DP est la norme d'entretien : un passage, trois compteurs, un espace constant.

> **Si vous pouvez expliquer cela dans une interview, vous allez montrer que vous pouvez:**
> * Reconnaître les modèles de PDD
> * Optimisez la force brute jusqu'au temps linéaire
> * Ecrivez un code propre et durable en Java/Python/C++

Bonne chance pour votre prochain entretien technique! C'est ce qu'il a dit.

---

* Prêt à plonger plus profondément ? Consultez le harnais d'essai complet ci-dessous. *

"""
# Test rapide (Python)
Python - <<'PY'
de taper l'importation Liste
Solution de classe:
def minimumOperations(self, nombres: List[int]) -> Int:
a = b = c = 0
pour x en nombres:
a = 0 si x == 1 autre 1
b = min(a, b + (0 si x == 2 autres 1))
c = min(b, c + (0 si x == 3 autres 1))
retour c

print(Solution().minimumOpérations([2,1,3,2,1]))
print(Solution().minimumOpérations([1,3,2,1,3,3)]
print(Solution().minimumOpérations([2,2,2,3,3])
PY
«» "

---

**Partager cet article** sur LinkedIn, Twitter ou Medium, et faire savoir aux recruteurs que vous avez maîtrisé un problème de LeetCode DP classique!