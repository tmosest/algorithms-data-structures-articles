---
titre: LeetCode 795. Nombre de sous-barrages avec maximum Bounded -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 795. Nombre de sous-barrages avec maximum
## Les bons, les mauvais et les méchants – Un guide complet d'entrevues

> **Mots-clés cibles**: *LeetCode 795, Nombre de Subarrays avec Bounded Maximum, préparation d'entretien, fenêtre coulissante, deux pointeurs, solution Java, solution Python, solution C++, temps O(N)

---

Table des matières
1. [Restatement de problèmes] (#restatement de problèmes)
2. [Intuition et approche]
3. [Pourquoi la solution Sliding-Window gagne] (#Why-the-sliding-wind-solution-wins)
4. [Détails de mise en œuvre (Java, Python, C++)] (#détails de mise en œuvre)
5. [Régimes et pièges] (#cases--règles)
6. [Analyse de la complexité] (#analyse de la complexité)
7. [Qu'est-ce qui fait ce problème ?](#qu'est-ce qui fait-ce-problème-le-gros)
8. [Comment en parler dans une entrevue] (#comment parler à propos-il-dans-une-entrevue)
9. [Traitement et ressources] (#tâche -- ressources)

---

Rétablissement du problème

> **LeetCode 795** – *Nombre de sous-arrachages ayant un maximum sonore*
> Compte tenu d'un tableau entier `nums` et de deux entiers `left` et `right`, retournez le nombre de subarrays contigus et non vides de telle sorte que l'élément maximum de la subarray se trouve dans la plage `[left, droite]`.
> Toutes les réponses correspondent à un entier signé 32 bits.

Exemple
«» "
nombres = [2,1,4,3], gauche = 2, droite = 3
sortie: 3 (sous-ensembles: [2], [2,1], [3])
«» "

---

## Intuition & Approche

- Oui. 1. La vue "Deux-Pointeurs"
Une sous-audience satisfait à la condition **iff**:

* **Aucun élément > droit** – sinon le maximum serait > droit.
* **Au moins un élément ≥ gauche** – sinon le maximum serait < gauche.

Ainsi, un sous-barrage est valide lorsqu'il s'agit d'un *segment* du tableau qui ne contient ** aucun élément hors de portée** et ** contient au moins un élément de bien** (≥ gauche).

- Oui. 2. Compter efficacement les sous-tribus valides
Au lieu d'énumérer chaque sous-aire (O(n2)), nous traversons le tableau une fois tout en maintenant:

La variable signifie comment elle est mise à jour
- Oui.
"lastInvalid" de l'élément **last** qui est > droite
"lastGood" de l'élément **last** qui est ≥ gauche

À l'index `i`, chaque sous-poste se terminant par `i` qui commence **après** `lastInvalid` et **includes** `lastGood` est valide.
Nombre de ces sous-tarifs = `dernierBien -dernierInvalid` (si `dernierBien >dernierInvalid`, sinon 0).

Accumuler cela sur l'ensemble du tableau → **O(n)** temps, **O(1)** espace.

---

- Oui. Pourquoi la solution Sliding-Window gagne

CRITÈRES Sliding-Window
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Temps****** O(n)** O(n2) O(n) mais avec une constante plus élevée
**Space**= O(1)= O(1)= O(n)=
**Simplicité de mise en œuvre**
*Intuition * Facile à expliquer
Autres **Edge-Case Handling**

L'approche de la fenêtre coulissante est *la plus conviviale pour les entrevues* – concise, éprouvée et facile à tester.

---

## Détails de la mise en œuvre

Voici trois implémentations propres et prêtes à la production.
Tous sont **public**, **fil-safe** et traitent tous les cas bord.

> **Astuce:** Utilisez `long` pour l'accumulateur seulement si vous anticipez des valeurs proches de `Integer. MAX_VALUE'.
> Le problème garantit le résultat en 32 bits, donc "int" est bien.

### Java

"Java
// Java 17+ (Lombok non requis)
solution de classe publique {
***
* Compte les subarrays dont le maximum est dans [gauche, droite].
*
* @param nums le tableau d'entrée
* @param gauche limite inférieure du maximum
* @param à droite limite supérieure du maximum
* @return number of valid subarrays
*/
public int numSubarrayBoundedMax(int[] nums, int gauche, int droite) {
nombre int = 0;
int lastInvalid = -1; // dernier indice où nombres[i] > droite
int dernier Bon = -1; // dernier indice où nombres[i] >= gauche

pour (int i = 0; i < nombres de longueur; i++) {
si (nums[i] > droite) {
lastInvalid = i; // réinitialiser la fenêtre
}
si (nums[i] >= gauche) {
dernier Bon = i; // nouveau bon élément
}
// nombre de subarrays se terminant à i qui sont valides
si (dernierBien > dernierInvalide) {
nombre += dernier Bonne - dernière Non valable;
}
}
le nombre de retours;
}
}
«» "

---

Python

'`python
# Python 3.9+
Solution de classe:
def numSubarrayBounded Max (self, nums, gauche, droite):
"""
:noms de type: Liste[int]
:type gauche : int
:type droit : int
:rtype : int
"""
nombre = 0
last_invalid = -1 # index de la dernière > droite
last_good = -1 # indice du dernier >= gauche

pour i, val dans l'énumération(nombres):
si valeur > droite:
last_invalid = i
si valeur >= gauche:
last_good = i

si _bien dernière > _non valide :
count += last_good - last_invalid

Nombre de retours
«» "

---

C++

'`cpp
// C++17
solution de classe {
public:
int numSubarrayBoundedMax(vecteur<int>& nums, int gauche, int droite) {
nombre long = 0;
int last_invalid = -1; // dernier indice où nombres[i] > droite
int last_good = -1; // dernier indice où nombres[i] >= gauche

pour (int i = 0; i < nums.size(); ++i) {
si (nums[i] > droite) last_invalid = i;
si (nums[i] >= gauche) last_good = i;

si (dernier_bien > dernier_invalide)
count += last_good - last_invalid;
}
return static_cast<int>(count); // correspond à 32 bits par problème
}
};
«» "

> **Pourquoi utiliser `long` pour `count` en C++?**
> Pour se protéger contre le débordement intermédiaire lorsque la longueur du tableau est de 105 et que tous les éléments sont dans la plage – le nombre de sous-arrachages peut atteindre ~5 × 109 temporairement, mais la réponse finale est toujours dans `int`.

---

## Cas de bord et pièges

La situation Que regarder?
- C'est quoi ?
"nums` contient seulement des valeurs > right" Loop continuera à réinitialiser `last_invalid`; `last_good` jamais mis à jour → réponse C'est déjà le code qui s'en occupe – il suffit d'éviter toute division par zéro. Autres
Autres Toutes les valeurs dans `[gauche, droite]` Chaque sous-tribu est valide. Autres
Autres Très grande `gauche` & `droite` (p. ex. 109)=La comparaison est toujours bonne=Utilisez les termes 64 bits si vous écrivez des constantes. Autres
Des chiffres négatifs ? Les contraintes du problème disent "nums[i] >= Aucun changement nécessaire. Autres
Un tableau vide (non autorisé par les contraintes)

---

Analyse de complexité

Valeur métrique
C'est pas vrai.
Temps **O(n)** – un passage sur le tableau
Espace **O(1)** – seulement quelques variables entières

---

- Oui. Ce qui fait Ce problème ?

1. **Intuition de Brute-Force ignorante**
De nombreuses personnes interrogées pensent qu'elles doivent vérifier chaque sous-aire – O(n2).
La clé est de se rendre compte que les éléments de la «bad» (> droite) agissent comme des points d'arrêt**.

2. **Hidden (Deux points)
L'idée de la fenêtre coulissante n'est pas évidente tant que l'on ne voit pas la relation* entre les éléments *invalides* et *valides*.

3. **Edge-Cas Overlook**
Oublier de réinitialiser `last_invalid` ou mal calculer `last_good - last_invalid` donne des bugs subtils.

4. **Test de complexité**
Les petits cas d'essai semblent bien; les tests de contrainte (p. ex. 105 éléments dans la plage) exposent le débordement entier si vous n'êtes pas prudent.

---

Comment parler Dans une interview

1. ** Clarifier les conditions**
Nous avons besoin de subarrays où le maximum se trouve dans [gauche, droite]. Cela signifie: aucun élément > droit, et au moins un élément ≥ gauche.

2. **Exposer l'observation clé**
Les indices avec des valeurs > droite divisent le tableau en segments indépendants. À l'intérieur de chaque segment, nous avons juste besoin de savoir combien de sous-arrachages contiennent un bon élément.

3. **Dériver la solution O(n)**
*. Maintenez deux indices : `last_invalid` (le plus récent > droit) et `last_good` (le plus récent ≥ gauche). Pour chaque position i, le nombre de subarrays valides se terminant à i est `max(0, last_good - last_invalid)`.

4. **Discuses sur les cas de bord* *
*S'il n'y a pas encore de bon élément (`last_good == -1`) ou le dernier bien est avant la dernière invalide, nous ajoutons 0.

5. **Complexité des peines**
Nous visitons chaque élément une fois, donc le temps O(n) et l'espace O(1).

6. **Optionnel: fournir une deuxième approche**
*Vous pourriez aussi faire un DP préfixe, mais il est plus lourd.

---

## À emporter & Ressources

* **Idée clé:** Sliding-window avec deux indices qui suivent les dernières positions de "bad" et "good".
* **Découvreur du temps:** Un seul passe, O(n) heure.
* **Interview hack:** Expliquez le concept *breakpoint* – il montre une profonde perspicacité.

> ** Pratique :**
> 1. LeetCode 795 (Facile à moyen).
> 2. Problèmes similaires : *Nombre de sous-arrachages avec somme ≤ K*, *Sous-arrachage maximal de la taille K*.
> 3. Construisez un harnais d'essai de petite unité dans chaque langue pour vérifier les données au hasard.

---

Références

- Page de problème de LeetCode: https://leetcode.com/problèmes/nombre de subarrays-with-bounded-maximum/
- Meilleures solutions (Java, Python, C++): https://leetcode.com/problèmes/number-of-subarrays-with-bounded-maximum/solutions/
- Oui. Ma propre solution de fenêtre coulissante : (Insérer votre lien de repo GitHub si disponible)

---

La pensée finale

La beauté de ce problème réside dans le fait qu'une question de comptage subarray apparemment difficile s'effondre à deux indices simples. Maîtrisez ce modèle, et vous aurez un outil puissant pour de nombreux problèmes d'entrevue qui impliquent des contraintes **max/min** ou **=non-mauvais-éléments**. Bon codage !