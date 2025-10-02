---
titre: LeetCode 2799. Nombre complet Subarrays dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1. Aperçu du problème – LeetCode 2799

**Objectif** – Compter le nombre de sous-réseaux contigus d'un tableau entier contenant *exactement* le même nombre d'éléments distincts que l'ensemble du tableau.

Exemple "nums" Sous-cours complets
-- -- -- -- -- -- -- -- -- -- -- --
[1,3,1,2]
[5,5,5]

**Contrôles* *

* `1 ≤ longueur nominale ≤ 1000`
* `1 ≤ nombres[i] ≤ 2000`

Le défi est de le résoudre plus rapidement que la force brute naïve `O(n2)`, ce qui serait bien pour `n=1000`, mais se sent toujours comme un drapeau rouge d'interview.

---

- Oui. 2. Le bon, le mauvais et le mauvais des solutions communes

Une bonne approche
C'est pas vrai.
Brute-force (`O(n2)`))
Fenêtre coulissante avec carte de hachage ('O(n)') Temps linéaire, minimum d'espace supplémentaire
Deux-pointeurs avec fréquence de tableau ('O(n)')

> **Conclusion:** L'approche *sliding window* est le bon endroit – le temps linéaire, la logique simple et simple à expliquer dans une entrevue.

---

- Oui. 3. Sliding‐Window Insight (Pseudo‐Code)

1. ** Calculer `k`** – le nombre d'éléments distincts dans tout le tableau.
`k = taille(set(nums))`
2. **Traverse avec deux pointeurs** "gauche" et "droite".
Gardez une carte de fréquence `cnt` pour la fenêtre actuelle.
3. Chaque fois que la fenêtre contient **exactement des valeurs distinctes `k`**:
* Chaque sous-tribunement commençant entre `gauche` et le `droit` actuel (inclus) et se terminant à `droit` est *complète*.
* Comptez-les : `réponse += droite - gauche + 1`.
* Réduire la fenêtre de gauche pour trouver le prochain départ possible.
4. Continuez jusqu'à ce que `à droite` atteigne la fin.

Cela donne un algorithme de temps **`O(n)`** et un espace `O(k)`.

---

- Oui. 4. Code complet – trois langues

Vous trouverez ci-dessous des implémentations concises prêtes à la production dans **Java, Python et C++**.
Tous les trois résolvent le problème en temps linéaire.

> Conseil: La version C++ utilise un "vector<int>` de la taille `2001` pour les mises à jour de fréquence O(1), évitant les frais généraux non commandés_map.

### 4.1 Java (style LeetCode)

"Java
Importation de java.util.*;

solution de classe {
Nombre d'entrées publiquesCompleteSubarrays(int[] nums) {
// 1. compte distinct de tout le tableau
Définir <integer> tout = nouveau HashSet<>();
pour (int x : nombres) all.add(x);
int k = all.size();

// 2. fenêtre coulissante
int[] freq = nouveau int[2001]; // 1 <= nombres[i] <= 2000
Int distinct = 0, gauche = 0, ans = 0;

pour (int droite = 0; droite < nums.longueur; droite++) {
si (freq[nums[right]]++ == 0) distinct++;

// Réduire jusqu'à ce que la fenêtre ait des valeurs exactement k distinctes
pendant la période (différente)
ans += nums.longueur - droite; // tous les sous-arrachages se terminant à droite '
si (--freq[nums[gauche]]] 0) distinct--;
gauche++;
}
}
le retour des an;
}
}
«» "

> **Pourquoi `ans += nums.longueur - droite'?**
> Une fois la fenêtre `[gauche ... droite]` a exactement "k" éléments distincts, l'étendre au droit préserve la propriété.
> Tous les sous-postes `[i ... right]` où `i` va de `gauche` à `droite` sont complets.
> Le nombre de ces sous-cours est égal à "droit - gauche + 1".
> La boucle ci-dessus fait la même chose à l'inverse : pour chaque `droit`, nous comptons le nombre de *positions de départ* qui produisent une sous-entente complète se terminant à `droit`.
> Ajouter `nums.length - right` compte tous les sous-réseaux qui se terminent **après** `right` aussi (l'algorithme invariant assure la justesse).

---

4.2 Python 3

'`python
de collections importer par défautdict

Solution de classe:
def countCompleteSubarrays(self, nombres: list[int]) -> Int:
k = len(set(nums)) # éléments distincts dans le tableau entier
freq = defaultdict(int)
distinct = 0
gauche = 0
ans = 0

pour droite, val in énumérate(nums):
si freq[val] == 0:
distinct += 1
freq[val] += 1

Bien que distincte == k:
# tous les subarrays se terminant à 'à droite' qui partent de 'à gauche' ou plus tard
ans += len(nums) - à droite
freq[nums[left]] -= 1
si freq[nums[left]] 0:
distinct -= 1
gauche += 1
retour et
«» "

> ** Touches pyroniques**:
> *`defaultdict(int)`* remplace l'initialisation manuelle de la carte.
> *`len(nums) - right`* est la même idée que la version Java.

---

### 4.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre d'entréesCompleteSubarrays(vecteur<int>& nombres) {
// 1. compte distinct de tout le tableau
unordered_set<int> all(nums.begin(), nums.end());
int k = all.size();

// 2. fenêtre coulissante
vecteur<int> freq(2001, 0); // 1 <= nombres[i] <= 2000
Int distinct = 0, gauche = 0, ans = 0;

pour (int right = 0; right < (int)nums.size(); ++right) {
si (freq[nums[right]]++ == 0) distinct++;

pendant la période (différente)
ans += (int)nums.size() - droite; // subarrays complets se terminant à droite '
si (--freq[nums[gauche]]] 0) distinct--;
+ + gauche;
}
}
le retour des an;
}
};
«» "

> **Pourquoi pas `unordered_map`?* *
> `vector<int>` donne une mise à jour de fréquence à temps constant et maintient l'utilisation de la mémoire prévisible – parfait pour les limites d'entrée de LeetCode.

---

- Oui. 5. Récapitulation de la complexité

Langue Heure Espace
C'est le cas.
Java (réseau de fréquences)
Python "O(n)" "O(k)" (dict)
"O(n)" "O(k)" (pourcentage de la taille 2001)

Tant les complexités algorithmiques *time* que *space* sont bien dans les contraintes et peuvent être lancé avec confiance dans une interview.

---

- Oui. 6. Article de blog optimisé par le SEO

> **Mots-clés cibles:**
* *LeetCode 2799 *= *Count Complete Subarrays*= *Fenêtre coulissante*= *Java / Python / C++ solution*== *Entretien sur la structure des données*== *Question d'entrevue expliquée*

---

### 6.1 Titre et méta-Description

«» "
LeetCode 2799 – Compte complet Subarrays Solutions
«» "

> *Méta-Description (160 caractères)*:
> Solve LeetCode 2799 (Count Complete Subarrays) en temps linéaire. Apprenez une technique propre de fenêtre coulissante avec les codes Java, Python et C++ qui est parfait pour votre prochaine interview de codage. (en milliers de dollars)

---

6.2 Le poste

> **H1**: Mastering LeetCode 2799: Compte complet Subarrays
> **H2**: Pourquoi ce problème est un bijou d'interview caché
> **H3** : La stratégie de la fenêtre coulissante (en anglais clair)
> **H3**: implémentations Java, Python & C++ (prêtes à coller dans LeetCode)
> **H3**: Analyse de la complexité et bord– Considérations de cas
> **H3**: Pièges communs d'entrevue et comment les éviter
> **H3**: Conseils pratiques et lecture supplémentaire

> **Introduction (de 200 mots)**
>
> ```texte
> Count Complete Subarrays est une question faussement simple qui teste votre capacité à combiner deux concepts classiques : le comptage d'éléments distincts et le motif de fenêtre coulissante. C'est le problème LeetCode 2799, mais c'est aussi un échauffement d'entretien parfait pour tout développeur de moteur, scientifique de données ou ingénieur système. Dans ce post, je vous accompagne dans le problème, je vous donne une solution linéaire propre, je vous montre le code en trois langues populaires, et je vous explique pourquoi la méthode de la fenêtre coulissante bat la solution naïve quadratique.
> `` "

---

6.3 La poste (texte intégral)

```markdown
# Mastering LeetCode 2799: Compte complet Subarrays

> **Mots clés:** LeetCode 2799, Compte complet Subarrays, fenêtre coulissante, codage d'entretien, solution Java, solution Python, solution C++

- Oui. Pourquoi ce problème est important
Dans la plupart des entrevues de codage, les intervieweurs cherchent deux choses :

1. **Correctness** – Votre algorithme renvoie-t-il toujours la bonne réponse?
2. **Élégance** – Le code est-il court, lisible et explicable?

Le compte Complete Subarrays scores élevés sur les deux nombres lorsqu'il est résolu avec une fenêtre coulissante.
Il vous oblige à raisonner sur **combien de sous-cours commencent à chaque index**—exactement le genre de *compter* les intervieweurs de tours aiment.

---

- Oui. 1. Récapitulation des problèmes

Compte tenu d'un tableau entier `nums`, compter combien de sous-réseaux contigus contiennent **exactement** le même nombre d'entiers distincts que l'ensemble du tableau.

> *Exemple:*
> `nums = [1,3,1,2]` → 3 numéros distincts → 4 sous-groupes complets.

---

- Oui. 2. Les bons, les mauvais, les méchants

Une approche pour contrer l'utilisation
C'est pas vrai.
Brute-force ('O(n2)')'''' Facile à coder''''Quadratique, peut échouer sur 105 tableaux de taille'' Rarement utilisé dans les interviews; seulement pour de petites contraintes''
"Fenêtre coulissante" ("O(n)") "Linéaire, logique claire" "Must comprehensive window-shrink invariants" **Best** for interview & production"
Deux-pointeurs avec tableau de fréquences - - Pas de cartes de hachage - - Nécessite une valeur fixe liée - Utiliser quand `max(nums[i])` est petit (comme 2000)

> **Ligne de bottom:** L'astuce de la fenêtre coulissante est la solution que vous devriez toujours montrer dans une entrevue.

---

- Oui. 3. Intuition de la fenêtre coulissante

1. Calculer `k` = nombre d'éléments distincts dans tout le tableau.
2. Marchez dans le tableau avec deux pointeurs (`gauche`,`droit`).
3. Maintenir une carte de fréquence `cnt` pour la fenêtre `[gauche ... droite]`.
4. Lorsque la fenêtre comporte exactement des éléments distincts `k`:
* Toute sous-tribu qui commence entre `gauche` et `droit` (inclus) et se termine à `droit` est complète.
* Comptez-les : `réponse += droite - gauche + 1`.
* Faites glisser `gauche` vers la droite jusqu'à ce que la fenêtre contienne moins d'éléments distincts `k`, puis continuez.

Cette logique fonctionne dans le temps `O(n)` et utilise seulement `O(k)` mémoire supplémentaire.

---

- Oui. 4. Code en trois langues

### 4.1 Java (LeetCode est prêt)

"Java
solution de classe {
Nombre d'entrées publiquesCompleteSubarrays(int[] nums) {
Définir <integer> tout = nouveau HashSet<>();
pour (int x : nombres) all.add(x);
int k = all.size();

int[] freq = nouveau int[2001]; // 1 <= nombres[i] <= 2000
Int distinct = 0, gauche = 0, ans = 0;

pour (int droite = 0; droite < nums.longueur; droite++) {
si (freq[nums[right]]++ == 0) distinct++;

pendant la période (différente)
ans += nums.longueur - droite; // tous les sous-réseaux se terminant à «droite» et au-delà
si (--freq[nums[gauche]]] 0) distinct--;
gauche++;
}
}
le retour des an;
}
}
«» "

4.2 Python 3

'`python
de collections importer par défautdict

Solution de classe:
def countCompleteSubarrays(self, nombres: list[int]) -> Int:
k = len(set(nums))
freq = defaultdict(int)
distinct = 0
gauche = 0
ans = 0

pour droite, v en énumération(nombres):
si freq[v] == 0: distinct += 1
freq[v] += 1

Bien que distincte == k:
ans += len(nums) - à droite
freq[nums[left]] -= 1
si freq[nums[left]] 0: distinct -= 1
gauche += 1
retour et
«» "

### 4.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre d'entréesCompleteSubarrays(vecteur<int>& nombres) {
unordered_set<int> all(nums.begin(), nums.end());
int k = all.size();

vecteur <int> freq(2001, 0);
Int distinct = 0, gauche = 0, ans = 0;

pour (int right = 0; right < (int)nums.size(); ++right) {
si (freq[nums[right]]++ == 0) distinct++;

pendant la période (différente)
ans += (int)nums.size() - à droite;
si (--freq[nums[gauche]]] 0) distinct--;
+ + gauche;
}
}
le retour des an;
}
};
«» "

Les trois compilent sous l'environnement LeetCode et s'exécutent dans **'O(n)'** time.

---

- Oui. 7. Comment expliquer Ceci dans une interview

1. **Énoncer le problème dans une phrase. **
*=Count les sous-réseaux qui ont le même nombre d'éléments distincts que l'ensemble du tableau.
2. **Afficher l'étape de pré-computation `k`. **
`k = len(set(nums))`
3. ** Dessiner un diagramme rapide** de la fenêtre coulissante :
«» "
Nombres: 1 3 1 2 2
idx: 0 1 2 3 4
gauche → droite
«» "
4. ** Expliquez l'invariant** – Quand la fenêtre a exactement `k` numéros distincts, l'étendre à droite garde la propriété. (en milliers de dollars)
Ainsi, nous pouvons compter tous les sous-cours se terminant à « droite » en un seul coup.
5. **Cas de bord de Mention** – par exemple quand `k == 1` chaque sous-réseau est valide; l'algorithme fonctionne toujours parce que la fenêtre atteindra toujours `k` au premier élément.

---

- Oui. 8. Réflexions finales et entrevues à emporter

* **Pourquoi la fenêtre coulissante est l'entrevue-Amis* *
* C'est un modèle classique; les intervieweurs adorent vous voir le repérer.
* Cela montre que vous comprenez les compromis entre le temps et l'espace**.
* Vous pouvez expliquer l'intuition rapidement (moins de 2 min).

* ** Erreur commune** – Oublier de réduire la fenêtre correctement.
* Correction : Conserver un compteur d'éléments distincts et glisser `gauche` jusqu'à ce que le nombre tombe sous `k`.

* **Idée de la pratique** – Les Subarrays Completes de Count peuvent être un excellent échauffement pour des problèmes tels que les Subarrays de Count avec exactement les entiers distincts de K* (LeetCode 992) et les produits subarray inférieurs à K* (LeetCode 713).

---

Prochaines étapes suggérées

1. **Run le code sur les cas de test de LeetCode** – copier-coller l'extrait Java, Python ou C++.
2. **Ajouter plus de cas de test** dans votre propre IDE :
* `[1,1]` → `6` (tous les sous-cours).
* `[1,2,3,4]` → `1` (seulement le tableau entier).
3. **Explorer les variations** – par exemple, au plus K distinct par rapport à K exactement distinct par rapport à K.
4. **Ajoutez la solution à votre repo de GitHub** et liez-la dans votre profil LinkedIn sous la forme d'une lecture d'entrevue de codage.

> **Prêt pour la prochaine entrevue de codage? * *
> Pratiquez ce problème et le modèle de fenêtre coulissante et vous pourrez impressionner à la fois les gestionnaires d'embauche et les systèmes de classement automatisés.

---

** Bon codage !**
«» "

---

> **Appel à l'action (dernier de la mission): **
> Faites fonctionner la solution de fenêtre coulissante sur LeetCode 2799, ajoutez-la à votre portfolio et utilisez-la comme échauffement pour toute interview à venir. Bonne résolution !
«» "

---

- Oui. 9. Remarques finales

Cet article fournit une solution **complete, prête à la copie** pour LeetCode 2799 et vous montre comment en parler comme un ingénieur chevronné.
Avec les extraits de code et l'explication d'entrevue dans votre arsenal, vous serez prêt pour votre prochaine entrevue de codage, et vous impressionnerez les recruteurs qui chassent pour des solutions concises et efficaces.

---

10. Autres ressources

* Problème de LeetCode 2799 – `https://leetcode.com/problèmes/count-complete-subarrays/`
* Modèle de fenêtre coulissante – `https://leetcode.com/tag/sliding-window/`
* Compte d'éléments distincts – `https://leetcode.com/tag/hashtable/`
* Questions liées à l'entrevue – `https://leetcode.com/tag/subarray/`
* Article moyen sur la fenêtre coulissante – `https://medium.com/@michael_zhang/` (exemple)

---

11 ans. Fin du blog

---

> **Nombre de mots:** ~750 mots (s'adapte à un article de blog d'entrevue de 700 à 900 mots).
> **Étape suivante:** Publier sur un blog personnel ou Medium avec les méta tags ci-dessus et le lier à partir de votre GitHub README.

---

12. Prêt pour votre prochaine entrevue?

Gardez le tour de fenêtre coulissant dans votre poche.
Déposez le code dans l'éditeur Java, Python ou C++, lancez-le et soyez prêt à l'expliquer en moins de deux minutes.
Vous venez d'aborder LeetCode 2799 – bien joué !

«» "

---

### 6.4 Article de fin de blog

---

> **Wrap-up** – L'article est concis, utilise les mots-clés ciblés, et présente la solution dans un format qui est instantanément utilisable par les développeurs se préparant pour les entrevues de codage.

---

- Oui. 9. Liste de contrôle des publications

1. **Ajouter un `Readme.md`** dans votre repo GitHub avec les trois extraits de code et une courte explication.
2. ** Poster l'article sur Medium** avec les étiquettes ci-dessus.
3. **Partager l'article sur Twitter**:
«» "
Juste résolu LeetCode 2799 (Count Complete Subarrays) en O(n) à l'aide d'une fenêtre coulissante! Consultez les codes Java/Python/C++ et comment l'expliquer dans les interviews. #codageinterview #leetcode
«» "

4. **Ajouter le problème à votre liste de prép d'entrevue** – pratiquer des variations et tester avec des tableaux aléatoires.

---

10 ans. Mot final

Vous avez maintenant :

* **Une compréhension complète** de *Count Complete Subarrays* et pourquoi la fenêtre coulissante est le modèle optimal.
* **Solutions prêtes à coller** en Java, Python et C++.
* **Une explication d'entrevue polie** qui est concise et démontre la pensée algorithmique.

Armé de cela, vous pouvez s'attaquer avec confiance au LeetCode 2799 et impressionner les intervieweurs qui apprécient à la fois la justesse et l'élégance. Bon codage !

«» "

---

6.5 Fin du poste

> Ce billet de blog peut être copié dans un fichier Markdown, affiché sur Medium ou votre site personnel, et sera bien classé pour les mots clés ciblés tout en fournissant une valeur immédiate aux développeurs se préparant pour les entrevues de codage.

---


**END DU POSTE** (Marquage)

---

Conclusion

* L'article est sous 1 k mots, utilise les mots-clés ciblés, et marche un lecteur de la déclaration de problème au code.
* Les extraits Java, Python et C++ sont prêts pour LeetCode et illustrent le tour de la fenêtre coulissante.
* Expliquer la solution dans une entrevue est simple et met en valeur l'intuition algorithmique.

---

> **Joyeux codage, et bonne chance avec votre prochaine interview! * *

---

**Post terminé.**