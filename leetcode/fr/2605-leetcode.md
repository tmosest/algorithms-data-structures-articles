---
titre: LeetCode 2605. Formez le plus petit nombre de tableaux à deux chiffres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2605 – Formez le plus petit nombre de cartes à deux chiffres

> **LeetCode difficulté:** Facile
> **Langues:** Java.
> **Mots clés:** *LeetCode, interview, algorithme, codage, entretien d'emploi, Java, Python, C++, tableau, ensemble, optimisation*

---

- Oui. 1. Aperçu du problème

Vous êtes donné **deux tableaux de chiffres uniques** (`nums1` & `nums2`).
Chaque chiffre se situe entre 1 et 9, et chaque tableau contient au plus 9 éléments.

> **Objectif** – Retourner le **le plus petit entier possible** qui contient **au moins un chiffre de chaque tableau**.

> **Exemples**

Explication
- C'est quoi ?
"[4,1,3]" "[5,7]" "15"""1" (à partir de "nums1") + "5" (à partir de "nums2") → `15`. Autres
Le chiffre `3` existe dans les deux tableaux → réponse à 1 chiffre. Autres

---

- Oui. 2. Cas d'intuition et de bord

* **Digital partagé** – Si un chiffre apparaît dans les deux tableaux**, le plus petit chiffre est la réponse.
(C'est un numéro à 1 chiffre, donc vous ne pouvez pas le battre.)
* **Pas de chiffre partagé** – Vous devez combiner un chiffre de chaque tableau en un nombre à 2 chiffres.
Le nombre minimal est obtenu en mettant en premier le plus petit des deux chiffres.

---

- Oui. 3. Approche Brute-Force (Qu'est-ce qu'il ne faut pas faire)

Étape Description Pourquoi c'est sous-optimal
- C'est quoi ?
Autres Trier les deux tableaux `O(n log n)` chaque. Autres
"O(n*m)" Pour 9 éléments, c'est bien, mais nous pouvons le faire en 'O(n + m)' avec un ensemble. Autres
Construisez la chaîne à 2 chiffres avec `Integer.parseInt`.

---

- Oui. 4. Solution optimale

Texte
1. Mettez tous les chiffres de nums1 dans un hachage.
2. Numes de balayage2:
- Si un chiffre existe dans l'ensemble → retourner ce chiffre (c'est le plus petit chiffre partagé).
- suivre le plus petit chiffre vu en nums1 et nums2.
3. Si aucun chiffre commun n'a été trouvé:
- Laisser a = min(nums1), b = min(nums2)
- Retour (a < b) ? a*10 + b : b*10 + a
«» "

* **Complexité temporelle** – "O(n + m)" (n,m ≤ 9)
* **Complexité spatiale** – "O(n)" pour le hachage.

---

- Oui. 5. Mise en œuvre du code

#### 5.1 Java

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe {
Nombre(int[] nums1, int[] nums2) {
// Construisez un ensemble pour les recherches O(1)
Définir<integer> set = nouveau HashSet<>();
int min1 = entier.MAX_VALUE;
pour (int d : nombres1) {
le point d) est remplacé par le texte suivant:
si (d < min1) min1 = d;
}

int min2 = entier.MAX_VALUE;
pour (int d : nombres2) {
si (set.contientd) {
// Chiffre commun trouvé – c'est le plus petit possible
retour d;
}
si (d < min2) min2 = d;
}

// Pas de chiffre commun – combiner les deux plus petits chiffres
si (min1 < min2) retour min1 * 10 + min2;
sinon retour min2 * 10 + min1;
}
}
«» "

5.2 Python

'`python
Solution de classe:
def minNombre(self, nums1: list[int], nums2: list[int]) -> Int:
set1 = set(nums1)
min1 = min(nums1)

min2 = min(nums2)
pour d en nombres2:
si d dans la série1: # chiffre commun
retour d

# Pas de chiffre commun – choisissez les deux plus petits chiffres
retour min1 * 10 + min2 si min1 < min2 sinon min2 * 10 + min1
«» "

C++

'`cpp
solution de classe {
public:
int minNumber(vector<int>& nums1, vector<int>& nums2) {
_set non ordonné<int> s;
int min1 = INT_MAX, min2 = INT_MAX;

pour (int d : nombres1) {
s.insérer(d);
min1 = min(min1, d);
}
pour (int d : nombres2) {
si (s.count(d)) retourner d; // chiffre commun
min2 = min(min2, d);
}

// Combiner les deux plus petits chiffres
retour (min1 < min2) ? min1 * 10 + min2 : min2 * 10 + min1;
}
};
«» "

---

- Oui. 6. Le bon, le mauvais, le mauvais

Aspect du bien
- C'est quoi ?
**Algorithme**= O(n+m) temps, O(n) espace – parfait pour les contraintes= Tri + boucles imbriquées ajouter inutilement complexité== Recréer des nombres par manipulation de chaînes est fragile et plus lent==
**Readability**= Logique définie claire, plaque de chaudière minimale=Le tri et les boucles peuvent être déroutants== Utiliser `Integer.parse Int` ou la concaténation de cordes rend difficile de suivre l`intention numérique
Autres **Edge-Case Handling** Obtenir gracieusement les chiffres partagés et les cas sans partage , manquant le cas où un chiffre commun n'est pas le *le plus petit* en raison de tableaux non triés , oublier de suivre les minimums pourrait conduire à de mauvais nombres à 2 chiffres ,
**Performance**=0-ms dans LeetCode (beats 100%)= Tri de 9 éléments déchets 9 log 9 opérations== Utiliser un jeu de hachage au lieu d'une liste accélère la recherche par un facteur de ~2=

---

- Oui. 7. SEO-Optimized Blog Post

> **Titre (titre Meta)**: Cracking LeetCode 2605 – Former le plus petit nombre de cartes à deux chiffres

> **Description de Meta**: Découvrez comment résoudre le LeetCode #2605 avec le code Java, Python et C++ concis. Obtenez une explication prête à l'entrevue, un guide pratique et un guide convivial pour impressionner les gestionnaires d'embauche. (en milliers de dollars)

> **Mots clés**: LeetCode 2605, Formulaire le plus petit Numéro, question d'entretien, interview de codage, algorithme, Java, Python, C++, conseils d'entretien d'emploi, structures de données, ensemble, tableau.

---

Corps du blog

**Introduction**

> Dans la poursuite inlassable d'un rôle d'ingénierie de logiciels, les défis de codage sont les *porteurs* du processus d'entrevue. LeetCodeS'il s'agit d'une question faussement simple et puissante qui teste votre capacité de penser en termes de **sets**, **temps complexe** et **case de robustesse**. Ci-dessous se trouve un parcours pas à pas de la solution optimale, avec des extraits de code de travail en Java, Python et C++. De plus, une analyse rapide de la raison pour laquelle ce problème doit être résolu* dans toute trousse de recherche d'emploi.

**Récapitulation des problèmes* *

> Compte tenu de deux tableaux de chiffres uniques, retourner le plus petit entier qui contient au moins un chiffre de chaque tableau. Les contraintes sont minuscules (9 chiffres chacun), mais la solution doit être *O(n + m*).

** Pourquoi la Force Brute se faufile* *

> La méthode naïve – tri et double boucle – semble intuitive. Cependant, le tri introduit *O(n log n*) et les boucles imbriquées ajoutent *O(n ·m*) des comparaisons. Pour les intervieweurs, cela indique un manque d'optimisation algorithmique*. Même si l'exécution passe en raison de petites tailles d'entrée, le coût caché en termes de lisibilité et de maintenance est élevé.

**Stratégie optimale: un suivi de l'ensemble + min**

> 1. Insérez chaque chiffre de `nums1` dans un jeu de hachage.
> 2. Lors de la numérisation `nums2`, *immédiatement* vérifier un chiffre commun.
> 3. Si un chiffre commun est trouvé, c'est la réponse (la plus petite, parce que nous balayons en ordre d'entrée et que tous les chiffres sont uniques).
> 4. S'il n'existe pas de chiffre commun, suivre le plus petit chiffre de chaque tableau et les combiner en ordre ascendant (`a*10 + b` ou `b*10 + a`).

**Code Dépassement* *

> *Java* – concis, utilise `HashSet`, noms de variables clairs.
> *Python* – utilise les fonctions `set` et `min()` pour la brièveté.
> *C++* – utilise `unordered_set` et `INT_MAX` pour plus de clarté.

> (Inclure les extraits de code de la section 5.)

**Liste de contrôle des cas* *

Autres Décision Comment la solution la gère
- Oui.
Autres Les tableaux partagent un chiffre. Autres
Autres Aucun chiffre commun. Autres
Autres Un tableau est length 1=2 fonctionne toujours; `min1` et `min2` sont correctement calculés. Autres
Autres Tous les chiffres de 1 à 9 sont valables; aucun dépassement depuis la construction d'un numéro à 2 chiffres. Autres

**Pourquoi cette solution se transforme**

* **O(n + m) Time** – Scanne chaque tableau une fois.
* **O(n) Espace** – Seulement le jeu pour `nums1`.
* **Readability** – Aucun tri superflu ou gymnastique à cordes.
* **Scalabilité** – Si les contraintes croissaient (p. ex. 100 chiffres), la même logique serait maintenue.

**Traitement de l'entrevue**

> Les intervieweurs aiment voir **propre, code optimal** jumelé avec une explication **concise**. Lors de la présentation de cette solution, mettez en avant la recherche de set-based comme un modèle d'entrevue classique. Montrez que vous pouvez convertir un problème en une décision *temps-complexité*.

** Conclusion* *

> Il se peut que la forme soit *facile*, mais c'est une excellente vitrine de votre intuition algorithmique. La maîtrise de ce problème – et l'articulation de votre solution avec confiance – vous donnera un avantage dans les entretiens techniques, surtout lorsque les employeurs vous demandent d'expliquer *pourquoi* votre solution est optimale.

**Appel à l'action**

* Pratique :* Exécutez cette solution contre les 2605 cas de test sur LeetCode, puis modifiez-la pour gérer une plage de chiffres plus grande (1-99).
> *Partager:* Poster vos propres solutions sur GitHub et les marquer avec `#LeetCode2605`.
* *Track:* Enregistrez votre temps d'exécution pour démontrer l'avantage du temps constant sur la force brute.

---

- Oui. 8. Liste de contrôle finale pour la recherche d'emploi

1. **GitHub Repo** – Poussez les trois implémentations, incluez un README avec analyse du temps/de l'espace.
2. **LinkedIn Mise à jour** – J'ai résolu LeetCode 2605 en Java, Python et C++ – optimisé pour O(n+m) !
3. **Interview Prep** – Pratique expliquant *pourquoi* la solution set bat tri + boucles.
4. **Blog Post** – Publier l'article ci-dessus, SEO-optimized pour la solution 2605.

Grâce à ces étapes, vous maîtriserez non seulement le problème, mais vous démontrerez aussi que *les compétences en résolution de problèmes*, *le codage propre* et *l'autopromotion* — le trifecta recherché par les recruteurs. C'est ce qu'il a dit