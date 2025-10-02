---
titre: LeetCode 2390. Supprimer les étoiles d'une chaîne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation du problème – -Enlèvement des étoiles d'une chaîne

Numéro de code:** 2390
**Difficulté:** Moyenne

> Vous êtes donné une chaîne `s` qui contient des lettres minuscules et le caractère `'*'`.
> Dans une opération, vous pouvez:
> 1. Choisissez un `'*'` dans `s`.
> 2. Retirez le caractère *close* non-star à son **left**.
> 3. Supprimer le `'*' lui-même.
>
> Effectuez l'opération jusqu'à ce qu'aucun `'*'' ne reste.
> Retourne la dernière corde.

L'entrée garantit que l'opération peut toujours être exécutée, et la chaîne résultante est unique.

> **Exemple**
> `s = "leet**cod*e"` → `lecoe`

L'observation clé est que chaque `'*'` supprime le caractère juste avant lui.
Donc nous pouvons scanner la chaîne une fois, en gardant seulement les caractères qui survivent aux suppressions.

---

- Oui. 2. Aperçu de la solution

Le modèle le plus courant pour ce problème est de traiter la chaîne comme un *stack*:

* Poussez une lettre sur la pile.
* Quand un `'*'` est rencontré, pop l'élément supérieur de la pile (le personnage non-star le plus proche) et ignorer l'étoile.

La pile peut être simulée avec un tableau et un pointeur entier (`top`) pour **O(1)** opérations push/pop.

Langage de l'espace Complexité du temps Complexité de l'espace Détail
-- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Java (n) (n) O(n) (n) (n) (n) (n) (n) (n) (n) (n) (n) (n) (n)) (n) (n) (n) (n)) (n) (n) (n) (n) (n)) (n) (n) (n)) (n) (n)) (n) (n) (n) (n) (n)) (n) (n) (n)) (n)) (n) (n)) (n) (n) (n)) (n)) (n) (n)) (n) (n) (n)) (n) (n) (n) (n) (n)) (n) (n) (n)) (n) (n) (n) (n)) (n) (n)) (n) (n)) (n)) (n) (n) (n)) (n) (n) (n) (n) (n)) (n) (n) (n) (n) (n
"list" comme pile
* C++ * O(n) * O(n) * "vecteur <char> " ou "chaîne" + "top"

Parce que chaque caractère est traité exactement une fois, l'algorithme fonctionne en temps linéaire, ce qui est optimal.

---

- Oui. 3. Code de référence

Voici des solutions idiomatiques propres pour **Java**, **Python** et **C++**.
Chaque implémentation suit la même logique : simuler une pile avec un tableau/liste et utiliser un pointeur d'index.

#### 3.1 Java

"Java
solution de classe publique {
Chaîne publique supprimerStars(String s) {
// Utilisez un tableau de caractères pour éviter les frais généraux d'un vrai Stack
tampon char[] = nouveau char[s.longueur()];
int top = 0; // points à la prochaine fente libre

pour (int i = 0; i < s.longueur(); i++) {
c = s.charAt(i);
Si (c) {
// Supprimer la non-étoile la plus proche à gauche
haut--; // jeter le caractère précédent
} autre {
tampon[top++] = c; //
}
}

// Convertir la partie conservée du tampon en une chaîne
retourner la nouvelle chaîne(buffer, 0, top);
}
}
«» "

**Pourquoi ça marche:**
Lorsque l'on frappe `'*'', la non-étoile la plus proche est déjà au-dessus du tampon.
Décrementer `top` Pops de ce personnage.
Tous les autres personnages restent dans le tampon.

---

3.2 Python

'`python
Solution de classe:
def supprimer Stars(self, s: str) -> str:
pile = [] # La liste Python est un tableau dynamique

pour ch en s:
Si ch == '*':
Pile.pop() # supprimer le caractère précédent
Sinon:
pile.append(ch) # conserver la lettre

retour ''.join(stack)
«» "

**Astuce:** `list.pop()` supprime le dernier élément dans l'heure O(1).

---

### 3.3 C++

'`cpp
solution de classe {
public:
chaîne supprimer Étoiles(chaîne s) {
res; // tiendra la chaîne finale
res.reserve(s.size()); // mémoire de réserve pour éviter les réaffectations

pour (charc : s) {
Si (c) {
if (!res.vide()) res.pop_back(); // supprimer le plus proche char gauche
} autre {
res.push_back(c); // conserver le caractère
}
}
retour rés;
}
};
«» "

** Pourquoi réserver? **
"réserve" empêche plusieurs réaffectations de mémoire, en maintenant l'algorithme vraiment linéaire.

---

- Oui. 4. Article de blog – Le bon, le mauvais, et le lamentable de retirer les étoiles d'une corde

### 4.1 Crochet – Attrapez votre intervieweur

Si vous êtes eye-balling un **software ingénierie interview** et une LeetCode-style question apparaît, vous êtes en bonne forme.
L'enlèvement d'étoiles d'une corde (LeetCode 2390) est trompeurment simple mais une grande vitrine pour :

* **La pensée basée sur les piles* *
* **Manipulation de chaînes linéaires**
* **Code optimal de l'espace**

Laissez tomber ce qui fait de ce problème une question d'interview *stellaire*, pourquoi vous allez l'adorer (le Bon), les pièges à éviter (le Mauvais), et les cas de bord sournois qui peuvent vous faire monter (l'Ugly).

---

4.2 Les bonnes – Pourquoi Ce problème est un gagnant

Pourquoi ça aide ?
C'est quoi ?
**O(n) Temps**Démontre que vous pouvez résoudre le problème en temps linéaire – critique pour les intervieweurs. Autres
**O(n) Espace**La simulation simple de la pile montre que vous comprenez les compromis entre l'espace auxiliaire. Autres
**Effacer l'entrée/l'entrée**= Pas de structures de données compliquées, juste des chaînes et des étoiles. Autres
**Single-Pass Solution**= Affiche que vous pouvez traiter l'entrée en un seul balayage—valable pour les problèmes de diffusion des données. Autres
**Évoluable**= Fonctionne pour `n = 10^5` confortablement, répondant aux contraintes de LeetCode. Autres

Une solution concise de simulation de pile gagne des points pour l'élégance et la lisibilité, exactement ce que les recruteurs recherchent.

---

#### 4.3 Les mauvaises – Pièges communs à surveiller

1. ** Utilisation d'une vraie pile (`Stack` en Java, `std::stack` en C++*) *
*Ces emballages ajoutent des frais généraux inutiles. *
Utilisez un tableau ou un vecteur et un pointeur pour O(1) push/pop.

2. **Sans traitement des cas de bord* *
*Une chaîne vide après toutes les suppressions. *
Votre code devrait renvoyer une chaîne vide (`""`) avec grâce.

3. **Musicipation *
*Confuser gauche/droite ou étoile suivante. *
Rappelez-vous : l'étoile supprime toujours le personnage **immédiatement à sa gauche** (pas l'étoile la plus proche).

4. **Négligence de l'optimisation de l'espace**
*Construire une nouvelle chaîne avec `+` ou `StringBuilder` dans une boucle peut créer du temps quadratique. *
Pré-allouer ou utiliser un tableau de caractères.

---

4.4 Les pièges subtils

Pourquoi ça a l'air bizarre
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Plusieurs étoiles consécutives** ('erase*****`)= Chaque `'*'` supprime le caractère précédent, mais vous pourriez penser que seul le premier compte. Simuler une pile; chaque `'*' pop est un élément. Autres
Autres **Etoiles au début**.Les opérations d'entrée sont possibles, mais vous pouvez encore rencontrer une étoile comme premier personnage dans un test mal formé. Sauter les étoiles qui décrémenteraient "top" en dessous de 0 (ou s'appuyer sur la garantie). Autres
Une naïve `StringBuilder.append()` dans une boucle avec `.toString()` répété peut faire exploser la mémoire. Ajouter une fois à la fin ou utiliser un tableau pré-alloué. Autres
**Caractéristiques**Le problème se limite aux lettres minuscules, mais une solution générique peut accidentellement gérer les majuscules ou les chiffres. Vérifier explicitement `c == '*' uniquement. Autres

La reconnaissance de ces détails démontre la profondeur de votre compréhension, une compétence inestimable dans les entrevues techniques.

---

4.5 Référencement Résumé optimisé

Si vous vous préparez à une interview technique ou cherchez à stimuler votre portefeuille en ligne, maîtriser *=Enlèvement des étoiles d'une chaîne* montre les recruteurs que vous pouvez:

* Mettre en œuvre des algorithmes **O(n)**
* Utiliser efficacement la simulation **stack** ou **array**
* Écrire **clean Java/Python/C++ code** qui passe de grands cas de test

Ajouter les tags de probleme à votre CV ou Linked Dans peut augmenter la visibilité:
`#LeetCode #Algorithme #Stack #Java #Python #C++ #Engineer logiciel #EntretienPréparer

---

4.6 A emporter

- **Bonne**: Temps linéaire, simulation de la pile, seul passage.
- **Bad**: Éviter les enveloppes lourdes, les caisses de bord de poignée, pré-alloter.
- **Ugly**: étoiles consécutives, conditions limites, grandes entrées.

Armé de cette connaissance, vous pouvez aborder le problème avec confiance, impressionner les intervieweurs, et même transformer la solution en un point de discussion lors de votre prochain entretien d'emploi. Bon codage !

---

*Sentez libre de copier les extraits de code dans votre IDE préféré, exécutez les tests d'échantillon, puis expliquez la logique dans votre prochaine simulation d'entrevue. *