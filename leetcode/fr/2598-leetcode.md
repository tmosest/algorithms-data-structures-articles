---
titre: LeetCode 2598. Le plus petit nombre d'éléments non négatifs manquants après les opérations -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## LeetCode 2598 – *L'entier non négatif manquant le plus petit après les opérations*
### Java / Python / C++ implémentation + SEO-friendly blog post

---

- Oui. 1. Récapitulation du problème

«» "
On vous donne un nombre de tableaux et une valeur entière.
Dans une opération, vous pouvez ajouter ou soustraire la valeur de n'importe quel élément de nombres.

Objectif : Après un certain nombre d'opérations, maximiser le MEX du tableau.
Le MEX d'un tableau est le plus petit entier non négatif qui en manque**.
«» "

> **Exemple**
> `nums = [1,‐10,7,13,6,8]`, `valeur = 5`
> Le MEX maximal qui peut être atteint est **4**.

Les contraintes ('nums.longueur, valeur ≤ 10^5', ''nums[i]" ≤ 10^9') signifient qu'une solution linéaire est nécessaire.



---

- Oui. 2. Aperçu général

Pour tout nombre `x` dans le tableau, nous pouvons le modifier en
Valeur `x + k *` **ou** `x – k * valeur` pour tout entier `k`.
Donc **seulement le reste de chaque élément modulo "valeur" questions** – tous les autres
les chiffres sont équivalents.

* "x % valeur = r" (non négatif)
`x` peut être transformé en **any** entier dont le reste modulo `valeur` est `r`.

Donc nous avons seulement besoin de savoir ** combien d'éléments nous avons pour chaque reste**.

Si nous voulons construire l'entier `i` du tableau, nous avons besoin d'un élément dont
le reste est «i % valeur».
Si nous manquons de ce reste, `i` ne peut pas être formé → c'est la réponse.



---

- Oui. 3. Algorithme (O(n + réponse) temps, O(valeur) espace)

«» "
1. Compter le nombre de nombres qui ont chaque r restant [0, valeur‐1].
2. Pour i = 0,12,...
r = i % valeur
si vous comptez[r] 0 → i est manquant → retour i
autrement compter[r]-- → utiliser un élément de ce reste
«» "

Parce que chaque itération enlève un élément du compte, la boucle finira
après tout au plus les marches `n`, où `n = nums.longueur`.
La réponse elle-même peut être aussi grande que `n`, de sorte que la complexité totale est linéaire.



---

- Oui. 4. Preuve d ' exactitude

Lemma 1
Après toute séquence d'opérations autorisées, l'ensemble multiple des restes
les éléments de tableau restent inchangés.

**Prof.**
L'ajout ou la soustraction de la "valeur" ne modifie pas la "valeur" du module restant "
('(x ± valeur) % valeur = x % valeur'). *



Lemma 2
Si pour certains `i` nous avons au moins un élément avec le reste `i % valeur`, nous pouvons
construire le entier `i` du tableau.

**Prof.**
Choisissez tout élément `x` avec le reste `r = i % valeur`.
Définir `k = (i – x) / valeur` (un entier parce que `x % valeur = r = i % valeur`).
Ajouter `k * value` à `x`.
Le numéro résultant est exactement "i".



Lemma 3
Si, pour un certain `i`, le compte du reste `i % valeur` est zéro, alors `i` ne peut pas être
formé par toute séquence d'opérations.

**Prof.**
Par Lemma 1 le multiset des restes ne change jamais, donc nous n'avons aucun élément que
peut être transformé en un nombre correspondant à "i (mod value)".
Par Lemma 2, cela signifie "i" est impossible. *



- Oui. Théorème
L'algorithme renvoie le maximum de MEX possible après n'importe quel nombre d'opérations.

**Prof.**
L'algorithme vérifie les entiers `i = 0,1,2,...` en ordre croissant.

* Pour chaque i* :
- Oui. Si un reste existe (compte > 0), l'algorithme le diminue et continue.
Par Lemma 2, nous pouvons en effet créer `i`, donc `i` appartient à un tableau réalisable,
et le MEX est plus grand que "i".
- Oui. Si le reste est manquant, l'algorithme retourne `i`.
Par Lemma 3 `i` ne peut pas être formé; donc `i` est le plus petit manquant
entier non négatif, c'est-à-dire le MEX du meilleur tableau possible.

Ainsi, la valeur retournée est exactement la MEX maximale. *



---

- Oui. 5. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Dénombrement des restes Autres
Autres Recherche de réponse
Total****** Autres

Les deux limites satisfont aux contraintes du problème.



---

- Oui. 6. Cas de bord et pièges

Situation Qu'est-ce que regarder
-- -- -- -- -- -- -- -- --
Chaque nombre devient le reste 0; la réponse est `n` (tous les nombres utilisés). Autres
= Nombres négatifs dans `nums`= Java/Python modulo peut être négatif → ajouter `value` avant de prendre `% value`. Autres
Autres Très grande réponse.La boucle peut itérer jusqu'à `n` fois; assurer qu'aucun `for(int i=0; i<value; i++)` ne s'arrête trop tôt. Autres
"valeur" supérieure à "n" Le tableau de comptage peut contenir de nombreux restes inutilisés, toujours amende. Autres

---

- Oui. 7. Bonne, mauvaise, mauvaise, panne

Aspect du bien
- C'est quoi ?
**Le calcul des restes est intuitif une fois que vous pensez à la valeur d'un module. Il faut comprendre que seulement le reste de la matière, pas les valeurs réelles. Oublier la manipulation négative du modulo conduit à de mauvais comptes. Autres
**Mise en oeuvre**= Dénombrement d'un seul passage + simple boucle. Pour une très grande "valeur", l'attribution d'un énorme réseau pourrait gaspiller la mémoire (mais "valeur ≤ 10^5"). Autres
**Performance** Si vous utilisez un HashMap au lieu d'un tableau, vous obtenez toujours linéaire, mais avec une constante plus élevée. Si vous pré-calculez par erreur tous les nombres jusqu'à un certain lien, vous allez frapper `O(n^2)` et temps-out. Autres
**Testing**= Facile à écrire des tests unitaires en vérifiant les petits exemples connus. Il faut tester les cas négatifs, `value=1`, `value>n`. Autres

---

- Oui. 8. Autres approches (pourquoi nous ne les avons pas choisies)

1. ** Programmation dynamique sur toute la gamme de nombres* *
– Nécessite un énorme tableau DP (la réponse 2), bien trop lent.
2. **Désormais le tableau et la soustraction gourmande**
– Tri est `O(n log n)`; travail supplémentaire inutile et constantes plus élevées.
3. ** Utilisant un ensemble de valeurs multiples**
– Recalculer chaque "i" possible serait "O(n·answer)"; impossible.

La méthode choisie pour le compte et le scan est la solution canonique pour cette classe de
problèmes de module.



---

- Oui. 8. Prêt à emporter pour l'entrevue

* **LeetCode 2598** est un problème classique de nombre manquant le plus petit qui tourne
une fois que vous voyez les opérations comme
Les opérations modulo.
* L'idée de base est la même que dans des problèmes comme
faire un entier avec des étapes données, ou un nombre plus petit qui ne peut pas être formé
à partir d'un multiset.
* Soyez prêts à expliquer la question négative-modulo – les intervieweurs aiment voir que
vous connaissez les bizarreries de la langue que vous utilisez.
* Discutez des compromis temps/espace: tableau vs. `HashMap`. Afficher le tableau donne
meilleur accès à temps constant.

**Mots clés pour parsemer dans votre CV ou portfolio:* *
`LeetCode 2598`, `L'entier non négatif le plus petit manquant après les opérations`, `MEX`, `modulo computing`, `Algorithme de Java`, `solution de Python`, `solution de C++`, `entrevue d'algorithme`, `entrevue de structure de données`, `problème d'entrevue d'emploi', `entrevue d'ingénieur logiciel`.

---

- Oui. 8. Code final

Voici des solutions propres et prêtes à la production dans **Java**, **Python** et **C++**.

### Java

"Java
Importation de java.util.*;

solution de classe {
public int findSmallestInteger(int[] nombres, valeur int) {
int n = longueur nums;
int[] count = nouvelle int[valeur];

// 1. Compter les restes (manipuler les nombres négatifs)
pour (int num : nombres) {
int r = valeur num %;
si (r < 0) r += valeur; // Java/Python négatif modulo hack
nombre[r]++;
}

// 2. Analyse de l'entier manquant
pour (int i = 0; i++) {
valeur d'int r = i %;
si [compter] 0) {
i; // le plus petit manque -> MEX maximum
}
count[r]--; // utiliser un élément de ce reste
}
}
}
«» "

### Python (3.8+)

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def findSmallestInteger(self, nombres: List[int], valeur: int) -> Int:
# Normaliser le reste pour les nombres négatifs
cnt = contre(((x % valeur) + valeur) % valeur pour x en chiffres)

i = 0
alors que Vrai:
r = i % valeur
si cnt[r] 0:
retour
[r] 1
i += 1
«» "

C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#incluez <numérique>

solution de classe {
public:
Int findSmallestInteger(std:vector<int>& nums, valeur int) {
(valeur, 0);

// Compter les restes, normaliser les nombres négatifs
pour (int x : nombres) {
int r = ((x % valeur) + valeur) % valeur;
cnt[r]++;
}

// Analyser la réponse
pour (int i = 0; ++i) {
valeur d'int r = i %;
si (cnt[r]) 0) retour i;
cnt[r]--;
}
}
};
«» "

Les trois extraits suivent la même logique linéaire et traitent les valeurs négatives
correctement.



---

- Oui. 9. À emporter pour les recruteurs et les intervieweurs

* LeetCode 2598 est un problème de comptage basé sur le module canonique**.
Comprendre que la valeur est juste un module est la clé de la solution.
* La solution est **robuste, rapide et facile à expliquer** – parfaite pour les cycles de codage.
* Mettez en évidence votre connaissance de :
* Modulo arithmétique (y compris les nombres négatifs)
* Techniques de comptage linéaire
* Raisonner au sujet du MEX
* Apportez la discussion "bonne, mauvaise, laid" : il montre que vous pouvez penser critiquement à
décisions de conception et pièges, une compétence très précieuse dans le logiciel réel
l'ingénierie.



---

### TL;DR

* **Problème** – Maximiser le MEX après avoir ajouté/soustrayant à plusieurs reprises la "valeur".
* **Insight** – Seulement les restes de la matière "valeur".
* **Solution** – Compter les restes → itérer `i = 0,1...`, consommer une correspondance
jusqu'à ce qu'il en manque un.
* **Complexité** – temps « O(n) », espace « O(value) ».
* **Code** – Fourni en Java, Python et C++.

Codage heureux et bonne chance de casser cette interview!