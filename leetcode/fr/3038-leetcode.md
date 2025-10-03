---
titre: LeetCode 3038. Nombre maximal d'opérations avec le même score I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Résumé du problème – Nombre maximal d'opérations avec le même score I (Code Leet 3038)

**Objectif**
Avec un tableau "nums", retirez à plusieurs reprises les deux premiers éléments.
Le point de chaque enlèvement est la somme de ces deux éléments.
Tous les retraits doivent produire le score *même*.
Retournez le nombre **maximum** de ces suppressions qui peuvent être effectuées.

«» "
Entrée : nombres = [3,2,1,4,5]
Produit : 2
Explication :
1ère suppression : 3 + 2 = 5 → nombres = [1,4,5]
2ème enlèvement : 4 + 1 = 5 → nombres = [5]
Plus d'enlèvements possibles
«» "

**Contrôles* *

- Oui.
-- -- -- -- -- --
2 ≤ "longueur en nombre" ≤ 100 1 ≤ "nums[i]" ≤ 1000

---

Une perspective de haut niveau

Lorsque nous commençons à enlever des éléments du *front*, la seule décision que nous devons faire est le **score** du premier retrait.
Toutes les suppressions ultérieures sont forcées : chaque paire suivante doit correspondre au même score, sinon le processus s'arrête.

Par conséquent:

1. Choisissez la somme des deux premiers éléments comme score cible (`cible = nombres[0] + nombres[1]`).
2. Scanner le tableau par étapes de deux : si `nums[i] + nums[i+1] == cible`, incrémenter le compteur ; sinon arrêter.

Cela donne une solution optimale en **O(n)** temps et **O(1)** espace.

---

Code de solution (Java, Python, C++)

### Java

"Java
solution de classe publique {
int maxOpérations(int[] nombres) {
cible int = nombres[0] + nombres[1]; // score de la première opération
int count = 1; // nous pouvons toujours effectuer la première opération

pour (int i = 2; i < nombres.longueur - 1; i += 2) {
si (nums[i] + nombres[i + 1] == cible) {
count++;
} autre {
break; // score incorrect → stop
}
}
le nombre de retours;
}
}
«» "

Python

'`python
Solution de classe:
def maxOperations(self, nombres: List[int]) -> Int:
cible = nombres[0] + nombres[1] # score de la première opération
count = 1 # la première opération est toujours valide

pour i dans la plage(2, len(nums) - 1, 2):
si nombres[i] + nombres[i + 1] == cible:
nombre += 1
Sinon:
pause
Nombre de retours
«» "

C++

'`cpp
solution de classe {
public:
int maxOpérations(vecteur<int>& nums) {
cible int = nombres[0] + nombres[1]; // score de la première opération
= 1; // la première opération est toujours possible

pour (int i = 2; i < nums.size() - 1; i += 2) {
si (nums[i] + nombres[i + 1] == cible) {
+ nombre;
} autre {
break; // score d'inadéquation – arrêter tôt
}
}
le nombre de retours;
}
};
«» "

---

Analyse de complexité

- Oui.
-- -- -- -- -- --
**Temps**="O(n)"– nous itérer sur le tableau une fois, étape-size 2="
**Espace** – seules quelques variables entières sont utilisées

---

Le bon, le mauvais, le mauvais de ce problème

Aspect du bien
- C'est quoi ?
*Déclaration de problème** , des contraintes claires et concrètes , seulement 100 éléments – trivial pour la plupart des interviews de codage , très petite taille d'entrée → trivial solution , mais teste toujours mindset ,
**Insight algorithmique**
**Cas d'Edge**= Les tableaux de longueurs even/odd manipulés naturellement== Doit gérer le cas où seuls les deux premiers éléments existent==Aucun cas particulier pour `nums.length=============================================================================================================================================================================================================== 2' – mais l'algorithme fonctionne toujours
**Pratiques de codage**= Bon pour la pratique des pointeurs/indices et des sorties précoces==Taxe variable minimale==La suringénierie (cartes deash, sous-algorithmes gourmands) est inutile==

---

Article du blog – Mastering LeetCode 3038 : une solution rapide et propre pour réussir l'entrevue

> ** Keyword Focus**: LeetCode 3038, Nombre maximal d'opérations, codage d'entretien, algorithme, Java, Python, solution C++

---

- Oui. 1. Présentation

Lorsque les recruteurs vous demandent de résoudre **LeetCode 3038 – Nombre maximum d'opérations Avec le même score I**, ils sont vraiment tester votre capacité à:

- Comprendre un problème en une seule ligne
- Trouvez une solution avide linéaire
- Ecrire le code propre dans votre langue préférée

Cet article vous explique le problème, vous montre la meilleure solution en Java, Python et C++, et explique pourquoi cette approche fonctionne. À la fin, vous vous sentirez assez confiant pour casser des questions d'entrevue similaires sur place.

---

- Oui. 2. Récapitulation des problèmes

> *=On vous donne un tableau de nombres entiers. Supprimer les deux premiers éléments et définir le score de l'opération comme la somme de ces deux éléments. Vous pouvez effectuer cette opération jusqu'à ce que le tableau contienne moins de deux éléments. Toutes les opérations doivent avoir le même score. Retournez le nombre maximum d'opérations que vous pouvez effectuer.

---

- Oui. 3. Pourquoi la solution est si simple

1. **La première opération corrige le score** – `cible = nombres[0] + nombres[1]'.
Toutes les opérations subséquentes doivent correspondre à cette somme.
2. **Les opérations subséquentes sont forcées** – vous ne pouvez pas sauter ou réorganiser des éléments.
Le seul point de décision est de savoir si la paire suivante correspond à "cible".
3. **Suffisances de balayage linéaire** – nous ne faisons qu'itérer paire par paire.

Ce raisonnement élimine tout besoin de structures de données fantaisistes ou de rétrosuivi. L'idée clé est de reconnaître que la somme de **première paire** est une contrainte globale.

---

- Oui. 4. Passage du code

C'est vrai. Java

"Java
solution de classe publique {
int maxOpérations(int[] nombres) {
cible int = nombres[0] + nombres[1];
= 1; // au moins la première opération

pour (int i = 2; i < nombres.longueur - 1; i += 2) {
si (nums[i] + nombres[i + 1] == cible) {
count++;
} autre {
pause;
}
}
le nombre de retours;
}
}
«» "

**Pourquoi ça marche* *
- "cible" est la somme requise pour chaque opération.
- `compte` commence à 1 parce que la première opération réussit toujours.
- Oui. La boucle vérifie chaque paire consécutive; en cas d'erreur de couple, le processus s'arrête (`break`).
- 'i < nums.longueur - 1' garantit que nous ne lisons jamais hors limites.

Python

'`python
Solution de classe:
def maxOperations(self, nombres: List[int]) -> Int:
cible = nombres[0] + nombres[1]
nombre = 1

pour i dans la plage(2, len(nums) - 1, 2):
si nombres[i] + nombres[i + 1] == cible:
nombre += 1
Sinon:
pause
Nombre de retours
«» "

Python suit la même logique ; l'étape `range` de 2 sauts sur les éléments traités.

C++

'`cpp
solution de classe {
public:
int maxOpérations(vecteur<int>& nums) {
cible int = nombres[0] + nombres[1];
nombre int = 1;

pour (int i = 2; i < nums.size() - 1; i += 2) {
si (nums[i] + nombres[i + 1] == cible) {
+ nombre;
} autre {
pause;
}
}
le nombre de retours;
}
};
«» "

Le code C++ reflète la logique Java en utilisant l'indexation 0 et le «vecteur».

---

- Oui. 5. Analyse de la complexité

Complexité
C'est pas vrai.
**Heure** "O(n)" Une seule passe sur le tableau, taille de l'étape 2
**Space** `O(1)`

Parce que `n ≤ 100`, cette solution est instantanée dans la pratique, mais la même échelle logique aux entrées plus grandes.

---

- Oui. 6. Cas de bord couverts

Autres Essai
- C'est quoi ?
Une seule opération possible
Des sommes mixtes – l'algorithme s'arrête à la première inadéquation
"[10, 10, 10, 10]"" Toutes les paires égales → retournent 2
"[2, 8, 4, 6, 5, 5]" "Cible 10 → les deux premières paires match, troisième doest"

L'algorithme gère gracieusement tout sans logique supplémentaire.

---

- Oui. 7. Pourquoi cela compte pour les entrevues

- **Shows pensée algorithmique**: Vous identifiez que la première opération verrouille le score et qu'un balayage linéaire est suffisant.
- ** Démontre un codage propre**: Utilisation de noms de variables significatifs, sortie précoce et boucles concises.
- **Évite les pièges**: Pas besoin de sur-enginer avec des cartes de hachage ou une programmation dynamique, qui peut distraire les intervieweurs.

---

- Oui. 8. Pensée finale

LeetCode 3038 est un exemple de manuel d'un problème d'avidité. La solution optimale est une seule passe après avoir déterminé la somme cible. En maîtrisant ce modèle, vous serez prêt à aborder toute une famille de problèmes où une décision initiale détermine le reste du processus.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

- Oui. 9. Liste de contrôle de l ' OEA

- **Titre**: Code Leet 3038: Opérations Max Même score – Java, Python, C++ Solution & Conseils d'entrevue
- **Mêta Description**: Solve LeetCode 3038 en temps O(n). Apprenez les solutions Java, Python et C++, l'analyse de complexité et les idées d'entrevue. Préparez-vous à travailler !
- **Mots clés**: LeetCode 3038, Opérations Max Même score, algorithme d'entretien, solution Java, solution Python, solution C++, algorithme O(n), conseils d'entretien de codage.

---