---
titre: LeetCode 2740. Trouvez la valeur de la partition -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes
**LeetCode 2740 – Trouvez la valeur de la partition**
Étant donné un tableau entier positif `nums`, le diviser en deux tableaux non vides `nums1` et `nums2` de sorte que

«» "
Valeur max(nums1) – min(nums2)
«» "

est ** aussi petite que possible**.
Retourne cette valeur minimale.

---

- Oui. 2. Aperçu de la solution
1. **Trier** le tableau – `O(n log n)`.
2. Après tri, la séparation optimale sera toujours *entre deux éléments adjacents*.
*Si vous divisez après `i‐1` et avant `i`, alors `max(nums1) = nombres[i‐1]` et `min(nums2) = nombres[i]`.
Toute autre division laisserait une plus grande différence. *
3. Scannez toutes les paires adjacentes et gardez la différence minimale.

**Complexité temporelle :** `O(n log n)` (dominé par tri).
**Complexité spatiale:** (Traitement en place pour Java/C++; Le tri Python est en place).

---

- Oui. 3. Code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

#### 3.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
valeurdepartition(int[] nombres) {
Trier le tableau
Tableaux.sort(nums);

Initialiser la réponse avec la première paire adjacente
int minDiff = nombres[1] - nombres[0];

// 3
pour (int i = 2; i < nombres de longueur; i++) {
minDiff = Math.min(minDiff, nombres[i] - nombres [i - 1]);
}

retour minDiff;
}
}
«» "

3.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def findValueOfPartition(self, nombres: List[int]) -> Int:
N° 1 Trier la liste
nombres.sort()

N° 2 Calculer la différence min entre les éléments consécutifs
retour min(nums[i] - nombres[i - 1] pour i dans l'intervalle(1, len(nums))
«» "

### 3.3 C++

'`cpp
#incluez <algorithme>
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
Int findValueOfPartition(vecteur<int>& nombres) {
Trier le vecteur
(noms.begin(), nums.end());

Commencez par la première paire
int minDiff = nombres[1] - nombres[0];

Analyser le reste
pour (size_t i = 2; i < nums.size(); ++i) {
minDiff = min(minDiff, nombres[i] - nombres [i - 1]);
}
retour minDiff;
}
};
«» "

---

- Oui. 4. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 2740

4.1 Introduction

Si vous préparez une entrevue d'ingénierie logicielle, vous vous trouverez à résoudre un large éventail de problèmes sur LeetCode. **2740 – Trouver la valeur de la partition** est un tel problème de moyen qui teste la capacité d'un candidat d'identifier des partitions optimales tout en gardant un œil sur l'efficacité algorithmique.

Dans ce billet, nous disséquerons le problème, nous passerons par la solution la plus élégante, nous discuterons des pièges communs (le "gugly") et nous mettrons en évidence les points d'entretien. Nous saupoudrons également des mots-clés SEO que les recruteurs aiment : *LeetCode, 2740, tri, partition, interview, algorithme, O(n log n), défi de codage, question d'entrevue de codage*.

---

4.2 Les bonnes – Pourquoi Ce problème est une Goldmine

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Simplicité de la réponse finale**La valeur minimale est simplement la plus petite différence entre deux éléments consécutifs triés. Facile à expliquer. Autres
**Maitrise du noyau** Le tri est un élément essentiel de nombreuses questions d'entrevue. Autres
**Le raisonnement optimal-substructure** montre que vous pouvez expliquer pourquoi une scission adjacente est optimale – une excellente compétence en matière d'épreuves. Autres
**O(n log n) efficacité**= Acceptable pour n ≤ 105. Les candidats peuvent discuter de la façon dont ils obtiennent le rendement requis. Autres
**Clean code**= La solution est courte (= 5 lignes par langue) et facile à lire, vous permettant de vous concentrer sur les points de discussion. Autres

*Conseil d'entrevue :* Lorsque vous présentez la solution, commencez par dire : « Premièrement, triez le tableau ; cela garantit que le meilleur partage est entre deux nombres adjacents. C'est parce que... Une explication concise démontre une profonde compréhension.

---

### 4.3 Les mauvaises – idées fausses communes et cas de bord

Qu'est-ce qu'il faut regarder
- Oui.
**En supposant qu'une scission soit optimale**= Certains candidats pensent qu'ils doivent essayer toutes les scission `n-1`, ce qui donne une solution `O(n2)`. Autres
Autres **Négligence de la contrainte de "non-vide"** Autres
L'utilisation de `nums[0]` comme candidat pour `min(nums2)` est erronée. Autres
**Diminuer la valeur absolue**= Puisque `max(nums1)` est toujours ≤ `min(nums2)` après tri, la valeur absolue peut être omise, mais vous devriez la justifier. Autres

*Conseil d'entrevue :* Parce que le tableau est trié, `max(nums1)` sera toujours le dernier élément du côté gauche, et `min(nums2)` sera le premier élément du côté droit. Ainsi, la différence est non-négative, donc la valeur absolue est inutile. (en milliers de dollars)

---

4.4 Les horreurs – Ce qui peut mal tourner

Scénario Pourquoi ça casse
C'est pas vrai.
**Les plus grandes entrées dépassant la plage `int`**" Dans des langues comme C++/Java, la différence entre deux entiers 32 bits peut déborder si les deux sont proches de `109`. Utilisez `long` ou `int64` pour être en sécurité. Autres
**Si vous utilisez un type stable, il n'a pas d'importance; mais un type instable pourrait brouiller des éléments égaux, bien que la réponse reste inchangée. Autres
**Distribution non-uniforme**= Si tous les nombres sont égaux, la différence minimale est `0`. Votre code doit gérer cela sans infiltration. Autres
**Input non trié avec des nombres négatifs**= Pas un problème pour ce problème de LeetCode, mais bon à discuter en général. Autres
**Python=S limite de récursion par défaut**= Non applicable ici, mais un rappel que la profondeur de récursion compte dans les problèmes d'entrevue. Autres

*Astuce d'entretien :* J'ai utilisé `int` dans la version C++, mais comme la valeur maximale est `109`, la différence s'insère toujours dans un entier signé 32 bits. Néanmoins, je garderai un œil sur le débordement si les contraintes changent. (en milliers de dollars)

---

### 4.5 Étape par étape (exemple de python)

'`python
Solution de classe:
def findValueOfPartition(self, nombres: List[int]) -> Int:
nums.sort() # 1
N° 2 Différence minimale adjacente
retour min(nums[i] - nombres[i-1] pour i dans la plage(1, len(nums))
«» "

1. **Trier** – 'O(n log n) "
2. **Scan** – "O(n)" – une seule passe linéaire.

Si vous voulez éviter les frais généraux du générateur dans Python, vous pouvez garder une variable:

'`python
min_diff = flotteur('inf')
pour i dans la plage(1, len(nums)):
diff = nombres[i] - nombres[i-1]
si diff < min_diff:
min_diff = diff
_retourner
«» "

---

### 4.6 Entretien– Points de discussion prêts

Question Description de la réponse
- C'est pas vrai.
*Pourquoi le tri garantit-il la scission optimale ?*= Parce que dans un tableau trié, le maximum du côté gauche sera toujours ≤ le minimum du côté droit. Par conséquent, les seules différences possibles sont entre les éléments consécutifs. Autres
*Quelle est la complexité du temps? *= `O(n log n)` en raison du tri. Le balayage linéaire est `O(n)` et négligeable. Autres
Pour ce problème, `O(n log n)` est optimal car tout algorithme basé sur la comparaison doit trier ou trouver une différence minimale. Autres
*Comment géreriez-vous les duplicatas? La différence devient `0`. Notre algorithme s'en occupe naturellement. Autres
*Et si nous avions un tableau "long"? Il suffit d'utiliser un type `long` pour la différence pour éviter le débordement. Autres

---

### 4.7 Liste de contrôle du référencement

Mots clés Fréquence
- C'est quoi ?
*Code de leet 2740*
*Trouver la valeur de la partition*
*Algorithme de tri*
*Entretien de codage
Efficacité algorithmique
*O(n log n)*
*Codage défi*

---

4.8 Dernier départ

LeetCode 2740 est trompeurment simple mais emballé avec des moments pédagogiques:

- Le tri est une première étape puissante pour de nombreux problèmes de partition.
- Une solution claire et concise est souvent préférable à une solution complexe.
- Pensez à travers les cas de bord; une explication solide montre que vous êtes un ingénieur prudent.

Lorsque vous clouez ce problème, vous avez démontré une compétence algorithmique essentielle qui est très appréciée par les recruteurs de technologie.

---

Référence de code rapide (toutes langues)

Code Lien
C'est pas vrai.
[GitHub Gist] (https://gist.github.com/votrenom d'utilisateur/2740-java) Autres
[GitHub Gist] (https://gist.github.com/votrenom d'utilisateur/2740-python) Autres
[GitHub Gist](https://gist.github.com/votrenom d'utilisateur/2740-cpp) Autres

*(Remplacez les URL avec vos propres liens Gist.) *

Bon codage, et bonne chance pour l'entrevue!