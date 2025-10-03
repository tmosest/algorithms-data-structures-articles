---
titre: LeetCode 2259. Supprimer le chiffre du nombre pour maximiser le résultat -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## C'est Mastering LeetCode 2259 – Supprimer le chiffre du nombre pour maximiser le résultat

> **Pourquoi ce problème est important* *
> LeetCode 2259 est une question de style d'entrevue classique qui teste votre manipulation **string**, **greedy thought** et **time-complexity sensibilising**. Une bonne compréhension de ce problème met en évidence votre capacité à résoudre les défis du codage réel et vous fait un candidat plus fort pour les rôles d'ingénierie logicielle.

---

Déclaration de problème (Code de débit 2259)

> **Input**
> * `nombre` – une chaîne représentant un entier positif (2 ≤ longueur ≤ 100).
> * `numer` – un seul chiffre de caractère qui est garanti pour apparaître au moins une fois dans `nombre`.
>
> ** Sortie**
> Retourne la chaîne *la plus importante* possible après avoir enlevé **exactement une** occurrence de `digital`.

**Exemple**

"number" "number" Résultats
- C'est quoi ?
"123" "3" "12"
""1231"""""1"""""231"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
""551""""""5""""51""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

---

Comment le résoudre – Greedy + Edge Stratégie de cas

La solution optimale est **O(n)**, où *n* est la longueur du "nombre".
L'observation clé :

> *Supprimer le premier chiffre qui est suivi d'un chiffre plus grand.
> En l'absence d'un tel événement, supprimer l'occurrence **dernier** du chiffre. *

Pourquoi ça marche ?

* Lorsque vous supprimez un chiffre **précédé** par un chiffre plus petit, le côté gauche demeure inchangé et le côté droit est maximisé.
* Supprimer un chiffre qui a un ** plus grand voisin à droite** rend la chaîne résultante plus grande (parce que vous perdez un chiffre plus petit tout en gardant un plus grand).
* Si chaque occurrence de « chiffre » est suivie seulement de ** chiffres plus petits ou égaux**, alors supprimer l'occurrence de **dernier** est préférable : vous gardez les premiers chiffres possibles et ne déposez que le plus droit.

Étape par étape

1. C'est une fois sur la corde.
2. Quand `number[i] == chiffre` **et** `i < n-1` **et** `number[i+1] > number`, supprimer `i` et casser.
3. Si la boucle se termine sans rupture, supprimer l'occurrence **dernier** de "numérique".

---

Mise en œuvre du code

### Java – Greedy (O(n))

"Java
solution de classe {
chaîne publique supprimerDigit(numéro de chaîne, chiffre de char) {
int n = nombre.longueur();
int supprimerIndex = -1;

pour (int i = 0; i < n; i++) {
si (numéro.charAt(i) == chiffre) {
si (i < n - 1 && nombre. CharAt(i + 1) > chiffre) {
supprimerIndex = i;
rupture; // endroit optimal trouvé
}
deleteIndex = i; // repli: dernière occurrence
}
}
numéro de retour.substring(0, supprimerIndex) + numéro.substring(deleteIndex + 1);
}
}
«» "

Python – Greedy (O(n))

'`python
Solution de classe:
def removeDigit(self, nombre: str, chiffre: str) -> str:
n = len(nombre)
delete_index = -1

pour i, ch en nombre:
si ch == chiffre:
i i < n - 1 et numéro[i + 1] > chiffre:
supprimer_index = i
pause
supprimer_index = i

numéro de retour[:delete_index] + numéro[delete_index + 1:]
«» "

### C++ – Greedy (O(n))

'`cpp
solution de classe {
public:
chaîne supprimer Chiffre(numéro de chaîne, chiffre char) {
int n = nombre.size();
int del = -1;

pour (int i = 0; i < n; ++i) {
si (numéro[i] == chiffre) {
Si (i < n - 1 && nombre[i + 1] > chiffre) {
del = i;
pause;
}
del = i; // dernière occurrence
}
}
nombre.erase(nombre.begin() + del);
numéro de retour;
}
};
«» "

---

Autre force brute (O(n2))

Si vous êtes nouveau à l'idée gourmande, vous pouvez énumérer chaque suppression possible et garder la corde maximale.
Fonctionne bien pour les contraintes (longueur ≤ 100), mais est **pas** la réponse optimale d'entrevue.

'`python
Solution de classe:
def removeDigit(self, nombre: str, chiffre: str) -> str:
meilleure = ""
pour i, ch en nombre:
si ch == chiffre:
cand = nombre[:i] + numéro[i+1:]
si cand > best:
meilleur = cand
le meilleur retour
«» "

---

Les bons, les mauvais, les méchants

Qu'est-ce qu'il faut mettre en avant Qu'est-ce qu'il faut éviter
Il n'y a pas de problème.
**Bonne**) • O(n) algorithme gourmand – rapide et évolutive. <br>• Logique claire et unique – facile à expliquer dans les entrevues. <br>• Poignées cas de bord (pas plus grand voisin droit).
**Bad**. • Brute-force est simple mais inutile – peut effrayer les intervieweurs. • Sur-optimisation pour la micro-performance sur les petites entrées; l'intervieweur se soucie de la logique. Autres
**Ugly**. • Subtiler les erreurs hors-par-un lors de la suppression du dernier chiffre. <br>• Oublier de gérer le cas où tous les chiffres sont égaux. • Mauvaise interprétation de la comparaison numérique ; gardez-la lexicographique pour les chaînes. Autres

---

Conseils d'entrevue

1. **Clarifier** : Demandez si le résultat doit être traité comme un nombre ou une chaîne (les deux fonctionnent en raison de l'ordre lexicographique).
2. **Passer à** : Choisissez un exemple et montrez comment l'algorithme décide quel index supprimer.
3. **Complexité**: Souligner le temps O(n) et l'espace supplémentaire O(1).
4. **Edge Cases**: Mention lorsque tous les chiffres sont les mêmes, ou lorsque le dernier chiffre est le seul événement.
5. **Nettoyage du code**: Utiliser des noms de variables significatifs (`deleteIndex`, `del`, `idx`).
6. **Tests**: Écrire quelques tests unitaires (par exemple, "111"`, "987654321"`, "121212".

---

À emporter

LeetCode 2259 est une vitrine parfaite de:

* **Manipulation de fixation** – suppression efficace des caractères.
* **Le raisonnement grêle** – choisir l'optimum local qui mène à un optimum global.
* **L'échange d'espace-temps** – la résolution en un seul passage avec une mémoire supplémentaire constante.

Une implémentation solide en Java, Python ou C++ démontre non seulement la compétence linguistique, mais aussi la perspicacité algorithmique – exactement ce que recherchent les recruteurs.

---

Référence finale Boost

- **Mots-clés**: LeetCode 2259, Supprimer Digit, maximiser le résultat, algorithme gourmand, question d'entretien, entretien de codage, solution Java, solution Python, solution C++, conseils d'entretien d'emploi, entretien d'ingénierie logicielle, pratique d'algorithme.
- **Description détaillée**: Découvrez comment résoudre LeetCode 2259 – Supprimer le chiffre du nombre pour maximiser le résultat. Voir les solutions Java, Python et C++, un algorithme gourmand et des conseils prêts à l'interview. Soyez engagé plus vite !

---

Bon codage ! C'est ce qu'il a dit