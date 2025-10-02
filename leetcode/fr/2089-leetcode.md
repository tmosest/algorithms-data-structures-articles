---
titre: LeetCode 2089. Trouver les indices cibles après triage -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trouver des indices de la cible après triage (LeetCode 2089)

Code de la langue
C'est quoi, ça ?
**Java**= <details><sommaire>Cliquer pour agrandir</sommaire><pre>import java.util.*;<br><br>Solution de classe publique {<br> Liste publique<Intégrer>cibleIndices(int[] nums, int cible) {<br> // Trier le tableau – O(n log n)<br> Arrays.sort(nums);<br> Liste <entier> ans = nouvelle liste d'array<>();<br> // 2 Analyse linéaire pour recueillir tous les indices de «cible» – O(n)<br> pour (int i = 0; i < nums.longueur; i++) {<br> si (nums[i] == cible) ans.add(i);<br> }<br> retourner ans;<br> }<br>}<br><br></pre></details> Autres
**Python**= <details><sommaire>Cliquez pour agrandir</sommaire><pre>class Solution:<br>def cibleIndices(self, nums: List[int], cible: int) -> List[int]:<br> #1= Trier la liste – O(n log n)<br> nums.sort()<br> # 2 Recueillir tous les indices où l'élément est égal à `cible` – O(n)<br> retourner [i pour i, x dans énumérate(nums) si x == cible]<br></pre></details> Autres
**C++**=details><sommaire>Cliquer pour agrandir</sommaire><pre>#includer <bits/stdc++.h><br>utiliser l'espace de noms std;<br><br>class Solution {<br>public:<br>vector<int>cibleIndices(vector<int>& nums, int cible) {<br> // 1/ 1/ 1/ 1/> Trier – O(n log n)<br> tri(nums.begin(), nums.end());<br>vector<int> ans;<br> // 1/ 1/ 1/ 1/ 1/ 1/ 1/> Pass linéaire – O(n)<br> pour (int i = 0; i < (int)numsize(); ++i) {<br> si (nums[i] == cible) ans.push_back(i);<br> }\n retourner ans;<br> }<br>};<br></pre></details> Autres

> **Pourquoi cette solution? * *
> *Le tri garantit que les indices de la cible dans le tableau trié sont déjà en ordre ascendant. *
> *Complexité temporelle:* `O(n log n)` en raison du tri.
> *Complexité spatiale:* `O(m)` où `m` est le nombre d'occurrences de `cible` (liste de réponses).
> *Les contraintes (`n ≤ 100`) rendent cette approche parfaitement bien, mais vous pouvez également la résoudre dans `O(n)` temps en utilisant le tri de comptage si vous voulez présenter l'optimisation avancée. *

---

- Oui. 2. Article de blog – Code de leet 2089: Trouver des indices de cible après trier l'array – bon, mauvais et lugubre

> **Mots-clés du référencement**: LeetCode 2089, Trouver des indices cibles après triage Array, entretien de codage, solution Java, solution Python, solution C++, complexité temporelle, algorithme de tri, conseils d'entretien, entretien d'emploi, entretien d'algorithme.

---

2.1 Introduction

Dans le monde des entrevues d'ingénierie logicielle, les problèmes de LeetCode sont les *show-stopper* que les recruteurs aiment lancer aux candidats. L'un des ajouts récents est **LeetCode 2089 – -Découvrez les indices cibles après avoir trié le tableau. Bien qu'elle soit étiquetée "Easy", elle a une torsion qui en fait un moment d'enseignement parfait pour * tri*, * scan linéaire* et * pensée algorithmique*.

Si vous vous préparez à une entrevue sur la structure des données ou que vous voulez simplement perfectionner vos compétences en Java/Python/C++, ce billet vous fait découvrir le problème, vous montre un code propre dans trois langues principales, vous plonge dans les compromis (le bon, le mauvais et le mauvais), et se termine par des conseils prêts pour l'entrevue.

---

2.2 Énoncé du problème (simplifié)

> Compte tenu d'un nombre entier et d'un nombre entier,
> **Retourner une liste de tous les indices où `target` apparaît dans `nums` après que le tableau soit trié dans un ordre non décroissant. **
> La liste des réponses doit être triée par ordre croissant.
> Si la cible n'apparaît jamais, retournez une liste vide.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Les indices de "2" sont 1 & 2
"[1,2,5,2,3]", `3`=" `[3]`=" Trié → `[1,2,2,3]`; l'index de `3` est 3="
"[1,2,5,2,3]", `5`=" `[4]`=" Trié → `[1,2,2,3]`; l'index de `5` est 4="

**Contrôles* *

* `1 ≤ longueur nominale ≤ 100`
* `1 ≤ nombres[i], cible ≤ 100`

Comme le tableau est minuscule, tout algorithme qui fonctionne dans `O(n log n)` ou même `O(n)` passera. La solution canonique utilise **sort + scan linéaire**, qui est à la fois intuitif et facile à expliquer dans une interview.

---

2.3 Le bien – ce qui fait Ce problème est classique

1. **Simplicité et clarté**
*Trier un tableau puis scanner une valeur est un modèle de manuel.* Les intervieweurs aiment les questions où il existe une approche claire et canonique – elle vous permet de présenter un style de codage propre.

2. ** Support linguistique multiple**
*Les solutions Java, Python et C++ sont presque identiques.* Cela démontre la pensée linguistique – une valeur des recruteurs de compétences lorsque votre équipe utilise des piles de polyglotte.

3. ** Sensibilisation à la complexité du temps**
*Vous êtes forcé de parler de `O(n log n)` pour trier contre `O(n)` si vous utilisez le tri de comptage.* Les intervieweurs recherchent souvent cette sensibilisation.

4. **Traitement des affaires**
*Exemple de résultat, valeurs dupliquées, cible hors de portée.* Ce problème vous oblige à penser aux cas de bord et à écrire un code défensif.

---

2.4 Les mauvais – où vous pouvez perdre des points

Pourquoi ça va mal
- C'est quoi ?
** Supposons que `cible` est toujours présent** Après le tri, il suffit de retourner la liste `ans` vide si rien n'est trouvé. Autres
**Pas de tri**=Le saut de l'étape de tri donne de mauvais indices parce que le tableau n'est pas trié. "Traitement explicite ("Arrays.sort(nums)", "nums.sort()" ou "std::sort"). Autres
**Utiliser la force brute d'O(n2)** Collez à l'approche canonique + scan. Autres
**Ignorer l'exigence de l'ordre trié**= Si vous retournez des indices de l'ordre initial du tableau, vous échouerez les tests cachés. Autres Assurez-vous d'être itératif sur le tableau *trié*. Autres

---

2.5 L'Ugly – Optimisation pour la vitesse et l'espace

Bien que `O(n log n)` soit acceptable, vous pouvez raser entièrement l'étape de tri:

1. **Traitement de la composition** –
Depuis `nums[i] ≤ 100`, vous pouvez créer un tableau de fréquence de taille 101.
Puis, tout en traversant les comptes, gardez un pointeur d'index courant pour savoir où la cible atterrira après le tri.

2. **Désistement précoce** –
Si le tableau trié commence par des nombres plus grands que `cible`, vous pouvez casser tôt.

3. **Réponse de mémoire efficace** –
Au lieu de construire l'ensemble du tableau trié, vous pouvez calculer les indices de début et de fin de `cible` directement à partir du tableau de fréquence.

> *Pourquoi faire ça dans une interview? *
> Il montre que vous pensez à *l'optimisation algorithmique* et *les contraintes problématiques*. Mais si l'intervieweur n'est pas à la recherche de micro-optimisations, s'en tenir à l'approche propre – la clarté gagne.

---

#### 2.6 Passage du code (Python)

'`python
Solution de classe:
def cibleIndices(self, nombres: List[int], cible: int) -> Liste[int]:
N° 1 Trier le tableau (O(n log n))
nombres.sort()
N° 2 Recueillir les indices de la cible (O(n))
retour [i pour i, x dans l'énumération(nums) si x == cible]
«» "

* Ligne 3: * Le tri est fait.
* Ligne 5 : * La compréhension de la liste donne une réponse concise.

---

2.7 Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Trier "O(n log n)" "O(1)" (en place pour Python/C++/Java)
(liste des réponses; `m` ≤ `n`) Autres
**Total** Autres

Avec `n ≤ 100`, le temps d'exécution est négligeable, mais la complexité est le *droit* à mentionner dans une interview.

---

2.8 Conseils d'entrevue

Scénario Pourquoi ça compte ?
- C'est quoi ?
**Démarrer**=I=ll trie d'abord le tableau, puis scanne la cible.= Affiche que vous utilisez un modèle standard. Autres
**Complexité** Démontre la conscience algorithmique. Autres
**Edge Cases**=Si la cible n'est pas présente, je retourne une liste vide. Couvre les tests cachés. Autres
Parce que tous les nombres sont ≤ 100, nous pourrions utiliser le tri de comptage pour obtenir "O(n)". Autres
**Tests**=1 test avec des cibles dupliquées, des tableaux à éléments uniques et des tableaux tous différents.= Ça montre la rigueur. Autres

---

2.9 Conclusion

LeetCode 2089 est trompeurment simple, mais il offre une excellente leçon dans les cas *de tri*, *de traversée linéaire* et *de bord de manipulation*. La solution canonique est un motif de type «sort‐and‐scan» qui est facile à coder et à expliquer. Pour une entrevue d'emploi, le **good** affiche un code propre et lisible; le **bad** ignore la nécessité de trier; le **ugly** est sur-ingénierie la solution quand une approche simple est suffisante.

> **Vous êtes prêt à poser cette entrevue sur la structure des données? * *
> Pratiquez ce problème en Java, Python, et C++, écrivez votre propre suite de test, et répétez le "Why" derrière chaque étape. Les employeurs aiment les candidats qui peuvent *expliquer* leur solution aussi clairement qu'ils la codent.

Joyeux codage, et que les dieux d'interview soient toujours en votre faveur!