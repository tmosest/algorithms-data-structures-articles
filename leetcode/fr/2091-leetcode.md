---
titre: LeetCode 2091. Éliminer le minimum et le maximum des rayons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2091 – Enlever le minimum et le maximum de la représentation
**Une solution rapide, propre et prête à l'interview (Java / Python / C++) + un billet de blog SEO complet* *

---

TL;DR

L'espace
- C'est quoi ?
Un passage pour trouver des indices de min & max; prendre le minimum de quatre façons de supprimer Autres
La même logique, les méthodes de liste la gardent courte Autres
*C++** .std::min_element` et `std::max_element` ou une seule boucle Autres

> **Résultat** – Pour tout tableau d'entrée, vous pouvez supprimer le min & max au maximum
> `min( max(i+1, j+1), max(n-i, n-j), i+1 + n-j, j+1 + n-i)`
> où `i` est l'indice du minimum, `j` est l'indice du maximum et `n` est la longueur.

---

- Oui. Pourquoi ce problème est une grande question d'interview

* **Clarité** – Tous les nombres sont distincts → pas de rupture d'égalité.
* **Constraints** – `n` jusqu'à `105` → solutions linéaires seulement.
* **Intuition** – Vous ne pouvez couper que des extrémités, de sorte que vous êtes effectivement ..
* **Plusieurs voies optimales** – Montre que vous devez examiner les quatre stratégies de suppression, pas seulement une cupidité.

---

- Oui. 1. La solution "Good" – Une solution propre et unique

### Java

"Java
solution de classe {
valeur minimale des actifs publics
int n = longueur nums;
la valeur de la valeur de référence est égale ou supérieure à 10 %;

// Trouver des indices de min et max
pour (int i = 0; i < n; i++) {
si (nums[i] < nums[minIdx]) minIdx = i;
si (nums[i] > nombres[maxIdx]) maxIdx = i;
}

// Quatre façons de supprimer les deux éléments
int delFromFront = Math.max(minIdx, maxIdx) + 1; // les deux de l'avant
int delFromBack = n - Math.min(minIdx, maxIdx); // les deux depuis l'arrière
int delFrontBack = (Math.min(minIdx, maxIdx) + 1) + // min avant, max dos
(n - Math.max(minIdx, maxIdx)); // ou vice-versa
int delBackFront = (Math.max(minIdx, maxIdx) + 1) + // max avant, min dos
(n - Math.min (minIdx, maxIdx));

Retour Math.min(Math.min(delFromFront, delFromBack),
Math.min(delFrontBack, delBackFront));
}
}
«» "

Python

'`python
Solution de classe:
def minimumDeletions(self, nombres: List[int]) -> Int:
n = len(nums)
min_idx, max_idx = nombres.index(min(nums)), nombres.index(max(nums))

avant = max(min_idx, max_idx) + 1
dos = n - min(min_idx, max_idx)
front_back = (min(min_idx, max_idx) + 1) + (n - max(min_idx, max_idx))
avant = (max(min_idx, max_idx) + 1) + (n - min(min_idx, max_idx))

retour min(avant, arrière, avant, arrière)
«» "

C++

'`cpp
solution de classe {
public:
au minimumDélétions(vecteur<int> et nombres) {
int n = nombres.size();
la valeur de la valeur de référence est égale ou supérieure à 10 %;

pour (int i = 0; i < n; ++i) {
si (nums[i] < nums[minIdx]) minIdx = i;
si (nums[i] > nombres[maxIdx]) maxIdx = i;
}

int front = max(minIdx, maxIdx) + 1;
Int back = n - min(minIdx, maxIdx);
l'entrée avantBack = (min(minIdx, maxIdx) + 1) + (n - max(minIdx, maxIdx));
int backFront = (max(minIdx, maxIdx) + 1) + (n - min(minIdx, maxIdx));

retour min({avant, arrière, arrière, arrière, arrièreFront});
}
};
«» "

Les trois codes fonctionnent dans **O(n)** temps et utiliser **O(1)** mémoire supplémentaire – parfaitement adapté aux contraintes.

---

- Oui. 2. L'approche rapide, mais toujours correcte

> *Pourquoi il est encore pratique* – parfois vous êtes pressé, voulez écrire quelque chose de super court, ou sont juste prototypage.

- Oui. Java (en utilisant des flux, mais plus lentement)

"Java
valeur minimale des actifs publics
int min = entier.MAX_VALUE, max = entier.MIN_VALUE;
-1, maxIdx = -1;
pour (int i = 0; i < nombres de longueur; i++) {
si (nums[i] < min) { min = nombres[i]; minIdx = i; }
si (nums[i] > max) { max = nombres[i]; maxIdx = i; }
}
// mêmes quatre options qu'avant...
}
«» "

> **Cons** – Vous pouvez écrire la même logique deux fois ou oublier de considérer l'une des quatre stratégies de suppression.
> **Pros** – Facile à lire et à comprendre pour les débutants.

---

- Oui. 3. L'Essayez de sur-optimisation

Une tentative courante est d'écrire une boucle imbriquée, en vérifiant toutes les façons de supprimer min & max, qui finit par **O(n2)** et est un **poids mort** pour ce problème.

'`python
♪ Cette force brute est *wrong* en termes de performance pour n=100k
def minimumDélétions(nums):
n = len(nums)
meilleure = n
pour i dans la plage(n):
pour j dans la plage(n):
Si i==j: continuer
# Essayez de supprimer i et j des deux extrémités
«» "

> **Takeaway** – LeetCode est un environnement d'entrevue limité dans le temps; toujours viser des solutions linéaires à moins qu'un meilleur algorithme ne soit explicitement demandé.

---

- Oui. 4. Essai de la solution

Entrée Sortie Explication
C'est pas vrai.
"[2,10,7,5,4,1,8,6] "" "5" "minIdx=5", "maxIdx=1"; le meilleur est "2" de l'avant + "3" de l'arrière. Autres
`[0,-4,19,1,8,-2,-3.5]`=" `3`=" `minIdx=1`, `maxIdx=2`; supprimer les 3 de l'avant. Autres
Un seul élément → une suppression. Autres

Exécutez le code dans tout compilateur en ligne ou IDE local. Les trois langues passent le LeetCode.

---

- Oui. 5. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 2091

> **Mots-clés de référence:** Leetcode 2091, Suppression minimum et maximum de Array, défi de codage d'entretien, solution Java, solution Python, solution C++, analyse d'algorithme, temps O(n), conseils d'entretien de codage

---

Titre
**Supprimer le minimum et le maximum de l'array (LeetCode 2091) : le bon, le mauvais et le mauvais* *

Description de la méta
Solve LeetCode 2091 en Java, Python ou C++ avec un algorithme O(n). Apprenez la stratégie optimale, les pièges à éviter et les idées d'entrevue qui impressionneront les recruteurs.

---

- Oui. 1. Récapitulation des problèmes

LeetCode 2091 vous demande de supprimer les plus petits et les plus grands nombres dans un tableau, où vous pouvez seulement supprimer des éléments du **front ou arrière**. L'objectif est de minimiser le nombre total de suppressions.

- **Input** – "nums" (entiers distincts, longueur 1 ≤ n ≤ 105)
- ** Sortie** – Suppressions minimales nécessaires

---

- Oui. 2. Le bon – Une solution propre et linéaire

Expliquez les quatre scénarios de suppression (avant, avant, arrière, avant, arrière) et pourquoi nous en prenons le minimum. Insistez sur la recherche d'index à un passage, qui maintient le temps à **O(n)** et la mémoire à **O(1)**.

Inclure des extraits de code pour Java, Python et C++ – chaque court et prêt à la production.

---

- Oui. 3. Le mauvais – rapide et lisible mais moins élégant

Afficher une implémentation Java plus verbeuse qui fonctionne encore mais qui duplique la logique. Soulignez que bien que la lisibilité soit la clé, il est facile d'oublier un scénario de suppression ou un mauvais indice.

---

- Oui. 4. Le mauvais – sur-optimisation ou mauvaise mise en œuvre

Illustrez une tentative de force brute O(n2) et pourquoi elle est inacceptable. Stress que les intervieweurs cherchent *correctitude* et *efficacité* simultanément; une solution intelligente mais lente est une impasse.

---

- Oui. 5. Pourquoi ce problème compte dans les entrevues

* **Les valeurs distinctes** suppriment l'ambiguïté.
* ** Contraintes linéaires** vous forcez à penser à des stratégies de suppression optimales.
* ** Quatre scénarios** forcent une vision combinatoire plus profonde.
* Il s'agit d'un modèle **classique, qui sort des extrémités** et qui apparaît dans de nombreux énigmes d'entrevue.

---

- Oui. 6. Conseils pour réussir

1. **Trouver des indices min/max en un seul balayage. **
"Java
si (nums[i] < nums[minIdx]) minIdx = i;
«» "
2. **Énumérer les quatre chemins de suppression** – ne manquez aucun.
3. **Utilisez des méthodes intégrées** (`index`, `min_element`) pour la brièveté si le temps est serré.
4. **Test avec cas de bord**: élément unique, min avant max, max avant min.
5. ** Expliquez votre processus de pensée** à l'intervieweur; la clarté de votre raisonnement est souvent plus importante que le code final.

---

- Oui. 6. Résumé

La meilleure façon de résoudre le LeetCode 2091 est une seule boucle** + **quatre options arithmétiques**. Évitez le code redondant et les boucles quadratiques. Apportez cette solution à votre prochaine entrevue de codage et regardez les recruteurs saluer en approbation.

---

- Oui. 7. Appel à l ' action

> Vous voulez plus de LeetCode interview prep? Abonnez-vous aux solutions de morsure, aux stratégies d'entrevue et aux défis de codage hebdomadaires.
> Téléchargez notre *Coding Interview Cheat Sheet* gratuit dès aujourd'hui!

---

- Oui. 8. Auteur Bio

* Ingénieur logiciel principal, coach d'entretien de codage, auteur des mises à jour de l'interview de codage. *

---

- Oui. 6. Pensées finales

* Gardez le code maigre, l'explication concise et l'état d'esprit de l'entrevue. *

Avec les implémentations Java / Python / C++ fournies, vous êtes prêt à aborder LeetCode 2091 dans n'importe quel entretien de codage, impressionnant les recruteurs avec élégance et efficacité.

Bon codage ! C'est ce qu'il a dit.

---


---

**Fin de TL;DR & Blog Post**