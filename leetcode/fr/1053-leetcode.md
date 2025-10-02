---
titre: LeetCode 1053. Permutation précédente avec un échange -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1053. Permutation précédente avec un échange – Un complet Guide
C++*

> Vous voulez accepter la question *Précédente Permutation avec un échange* dans une interview de LeetCode?
> C'est un parcours ** étape par étape**, un algorithme clair, trois solutions prêtes à la production et un billet de blog optimisé pour le référencement qui fera remarquer votre CV par les recruteurs.

---

TL;DR

* **Problème** – Trouvez la permutation lexicographiquement la plus grande plus petite que le tableau donné en utilisant **exactement un swap**.
* **Idée de base** – Scanner à partir de la droite pour localiser le premier dip.
* **Échange de clés** – Choisissez l'élément le plus à droite qui est **plus petit** que le plongeon et **plus grand** parmi ces candidats (pour garder le résultat le plus grand possible).
* **Complexité** – **O(n)** temps, **O(1)** espace supplémentaire.
* **Cas d'Edge** – Déjà la plus petite permutation, les valeurs dupliquées, les tableaux à éléments uniques.

---

Déclaration de problème (Code Leet 1053)

> Compte tenu d'un éventail d'entiers positifs `arr` (pas nécessairement distinct), retourner la permutation lexicographiquement plus grande qui est plus petite que `arr`, qui peut être faite avec exactement un échange.
> Si cela ne peut pas être fait, retournez le même tableau.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
"[3,2,1]"" "[3,1,2]" "Swap "2" et "1". Autres
La plus petite permutation. Autres
"[1,9,4,6]""" `[1,7,4,6]"" Swap `9` et `7`. Autres

---

L'approche bonne, mauvaise et laid

**Beau**
- C'est quoi ?
Un seul passage de droite à gauche pour trouver le premier indice décroissant*. Une double boucle qui vérifie chaque paire – `O(n2)' – perd du temps. Génération et triage de la permutation Brute-force – impossible pour «n ≤ 104». Autres
**Duplications manuelles**=Trouver la trace du candidat le plus à droite pour éviter d'échanger des nombres égaux qui produisent le même tableau. Ignorer les duplicata peut produire le mauvais indice ou aucun échange. L'échange de la première apparition d'un nombre plus petit pourrait produire la permutation la plus faible possible, et non la plus grande. Autres
**Complexité**=Temps `O(n)`, espace `O(1)` – optimal pour l'entrevue.==Temps `O(n2)`, passe encore de petits tests, mais pas acceptable pour les grandes entrées. "O(n!)" temps – astronomiquement lent. Autres
**Code Simplicité**= Une boucle d'aide, un échange – facile à lire.= Nombreuses boucles imbriquées, intention peu claire. Suringénierie avec des fonctions d'aide inutiles. Autres

---

Algorithme de base (Pseudocode)

«» "
1. Trouver i = dernier indice tel que arr[i] < arr[i-1].
Si aucun n'existe → tableau est déjà le plus petit; retourner arr.

2. Dans le suffixe arr[i ... fin], trouvez l'élément
x qui est < arr[i-1] et le plus grand possible.
Si des duplicatas de x existent, choisissez le plus à gauche (le plus près de i-1)
pour s'assurer que le tableau final est le plus grand.

3. Swap arr[i-1] et x.

4. Retourner arr.
«» "

Pourquoi ça marche ?
La première position décroissante est l'endroit le plus droit où le tableau peut être réduit. Pour garder le résultat le plus grand possible, nous échangeons l'élément *le plus petit* du suffixe, et nous choisissons l'occurrence **le plus droit** de cet élément pour éviter les réductions inutiles causées par des duplicatas.

---

Solutions

- Oui. Java – `Solution.java "

"Java
Importation de java.util.*;

solution de classe {
[] prvPermOpt1(int[] arr) {
int n = longueur de l'arrond;
i = n - 1;

// 1. Trouvez la première paire décroissante de droite.
pendant que (i > 0 && arr[i - 1] <= arr[i]) i--;

si (i) 0) retour arr; // déjà minime

pivot int = i - 1;

// 2. Trouvez l'élément le plus droit < arr[pivot] et le plus grand possible.
Int cible Idx = -1;
Int cible Val = entier.MIN_VALUE;

pour (int j = pivot + 1; j < n; j++) {
si (arr[j] < arr[pivot] && arr[j] > cibleVal) {
cibleVal = arr[j];
cible Idx = j;
}
}

// 3. Échange
int tmp = arr[pivot];
arr[pivot] = arr[targetIdx];
arr[targetIdx] = tmp;

retour arr;
}

// Main optionnelle pour un test manuel rapide
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(Arrays.toString(s.prevPermOpt1(nouveau int[]{1, 9, 4, 6, 7}));
}
}
«» "

**Explication**
*La boucle `pendante (i > 0 && arr[i-1] <= arr[i]) Je...
C'est le plus droit.
*La boucle intérieure* garde le meilleur candidat (`targetVal`) qui est plus petit que le pivot.
Finalement nous effectuons l'échange.

---

### Python – `solution.py "

'`python
de taper l'importation Liste

Solution de classe:
def prevPermOpt1(self, arr: List[int]) -> Liste[int]:
n = len(arr)
i = n - 1

1. Localisez la première paire décroissante.
alors que 0 et arr[i - 1] <= arr[i]:
I -= 1

Si i == 0:
retour arr # Déjà la plus petite permutation.

pivot = i - 1

# 2. Trouvez l'élément le plus droit < arr[pivot] avec la valeur maximale.
cible_idx = -1
cible_val = -1
pour j dans la plage (pivot + 1, n):
si arr[j] < arr[pivot] et arr[j] > cible_val:
cible_val = arr[j]
cible_idx = j

3. Échange
arr[pivot], arr[target_idx] = arr[target_idx], arr[pivot]
retour arr

♪ Essai rapide facultatif
si __nom__ == "__main__" :
s = Solution()
print(s.prevPermOpt1([1, 9, 4, 6, 7])
«» "

---

### C++ – `solution.cpp "

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
std::vector<int> prevPermOpt1(std::vector<int>& arr) {
int n = arr.size();
i = n - 1;

// 1. Trouvez la première paire décroissante de droite.
pendant que (i > 0 && arr[i - 1] <= arr[i]) --i;
si (i) 0) retour arr; // déjà minime

pivot int = i - 1;

// 2. Trouvez le meilleur candidat avec lequel échanger.
Int cible Idx = -1;
Int cible Val = -1;
pour (int j = pivot + 1; j < n; ++j) {
si (arr[j] < arr[pivot] && arr[j] > cibleVal) {
cibleVal = arr[j];
cible Idx = j;
}
}

// 3. Échange
La présente directive entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
retour arr;
}
};
«» "

**Astuce:** L'algorithme fonctionne dans *O(n)* temps et utilise *O(1)* espace supplémentaire, parfait pour les contraintes d'entretien.

---

Le projet de blog

---

Titre
**LeetCode 1053: Permutation précédente avec un échange – Master the O(n) Solution (Java, Python, C++)* *

Description de la méta
Apprenez à résoudre le LeetCode 1053, la Permutation précédente avec un échange, en Java, Python et C++. Obtenez l'algorithme complet, la manipulation de cas de bord, et un blog prêt à travailler avec des mots clés SEO.

Introduction
Lorsque les intervieweurs vous donnent le code Leet. *Permutation précédente avec un échange*, ils testent votre capacité à raisonner sur les permutations, à manipuler les duplicatas et à écrire du code propre. Cet article explique le problème, passe par un algorithme gourmand, et vous donne trois implémentations prêtes à la production. Que vous soyez un développeur Java, un Pythonista ou un gourou C++, vous allez partir avec un extrait de code que vous pouvez déposer dans votre prochaine interview ou portfolio.

### Aperçu du problème
*Vous êtes donné un éventail d'entiers positifs. Vous devez produire le tableau lexicographiquement le plus grand qui est strictement plus petit que l'original, en utilisant exactement un échange. Si un tel échange n'existe pas, retournez le tableau original. *

### Insight de base – Premier indice décroissant
L'endroit le plus à droite où le tableau diminue (`arr[i] < arr[i‐1]`) est celui où vous pouvez réduire le tableau. Tout à sa gauche est déjà optimal; tout à sa droite doit être modifié pour obtenir le plus grand résultat possible.

Algorithme pas à pas
1. **Scan à partir de la fin** pour trouver le premier indice `i` où `arr[i-1] > arr[i]`.
2. Si aucun tel `i` n'existe, le tableau est déjà la plus petite permutation - le retourner.
3. Dans le suffixe `arr[i ... fin]`, trouver l'élément qui est
* inférieure à `arr[i-1]` **et** le plus important parmi ces éléments.
4. **Swap** `arr[i-1]` avec cet élément.

- Oui. Pourquoi cela fonctionne
La première paire décroissante garantit que le tableau devient plus petit. En sélectionnant l'élément *plus grand* dans le suffixe, nous conservons le préfixe (qui détermine l'ordre lexicographique) le plus grand possible. Le choix de l'événement le plus à droite s'effectue en toute sécurité : si le même nombre apparaît plusieurs fois, l'échange avec l'événement le plus à gauche laisserait un plus grand nombre plus tard dans le tableau, ce qui n'est jamais souhaitable.

Traitement des cas de bord
Autres Décision Que faire? Pourquoi?
- C'est quoi ?
**Jusqu'à présent, le tableau original de retour n'existe pas
**Duplicats**=Choisir le candidat le plus à droite=Éviter les réductions inutiles=
**Élément unique**

Analyse de complexité
* **Heure** – `O(n)` (un passe pour trouver le plongeon, un autre passe pour trouver le candidat).
* **Espace** – "O(1)" (modification en place).

### Code Passage – Java

*(Inclure l'extrait de Java de plus tôt avec les commentaires line-by-line.) *

### Code Passage – Python

*(Inclure l'extrait de Python de plus tôt avec des commentaires concis.) *

### Code Passage – C++

*(Inclure l'extrait de C++ de plus tôt avec des commentaires.) *

Ce que les intervieweurs recherchent
*Reconnaissance du motif gourmand, manipulation correcte des duplicatas, et code propre et testable. *

Cas d'essai rapide

Produit escompté
-- -- -- -- -- -- -- --
[3,2,1] Autres
[1,1,5]
"[1,9,4,6,7]" "[1,7,4,6,9]" Autres
"[1]"
[2,2,1,2]

Exécutez les extraits de "main`/`_main__` fournis pour les voir en action.

### SEO & Job‐Search Conseils utiles
- Utilisez des mots-clés : *LeetCode 1053,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,. *
- Ajouter un lien vers votre repo GitHub (par exemple, `https://github.com/votrenom/leetcode-solutions`).
- Offrez un PDF téléchargeable de la solution pour les recruteurs qui préfèrent des références rapides.
- Mentionnez votre solution optimale (O(n) et les duplicatas (handles duplicatas) – les recruteurs de caractères aiment.

Mot final
Vous avez disséqué LeetCode dans sa forme la plus simple. Tirez n'importe lequel des trois extraits dans votre portfolio, incluez l'explication de l'algorithme dans votre CV, et sentez-vous confiant à résoudre ce problème de permutation dans votre prochaine entrevue de codage.

---

Conclusion
*Avec l'algorithme et trois implémentations propres à portée de main, vous pouvez revendiquer avec confiance la victoire sur LeetCode 1053. Bon codage, et bonne chance pour votre prochaine interview! *

---

Cette ébauche combine une explication algorithmique détaillée avec des commentaires axés sur l'entrevue et un contenu optimisé par le SEO. N'hésitez pas à ajuster le ton ou à ajouter des diagrammes visuels pour correspondre à votre style de blog personnel.

---

À emporter

- **Problème**: La plus grande permutation est strictement plus petite que l'originale avec un seul échange.
- **Solution**: Trouvez le plus droit, échangez avec le plus petit élément suffixe.
- **Complexité**: Temps optimal "O(n)", espace "O(1)".
- **Code**: Java, Python, extraits C++ prêts pour des interviews ou des portfolios.
- **Blog**: Un brouillon prêt à être publié avec des mots-clés SEO et une couverture de cas de bord.

Bonne chance, et que vos intervieweurs soient impressionnés par votre code et le billet de blog que vous allez fièrement présenter! C'est ce qu'il a dit