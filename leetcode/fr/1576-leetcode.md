---
titre: LeetCode 1576. Remplacer tous les ? pour éviter les répétitions consécutives -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1576
**Titre :** *Remplacer tous ? pour éviter les répétitions consécutives*
**Difficulté:** Facile

> **Objectif** – Remplacer chaque `?` dans la chaîne `s` (seulement les lettres minuscules et `?`) pour que la chaîne finale n'ait **pas deux caractères égaux adjacents**.
> Les caractères non-questionnaires ne peuvent pas être modifiés.
> Il est garanti que la chaîne originale ne contient pas de répétitions consécutives, sauf pour les positions `?`.
> La réponse existe toujours et toute chaîne valide est acceptée.

---

- Oui. 2. Idée de haut niveau

Traversez la ficelle de gauche à droite.
Lorsque nous avons frappé un `?`, choisissez une lettre qui diffère des caractères **précédent** et **prochain** (s'ils existent).
Parce que nous avons seulement besoin d'un remplacement valide, il suffit d'essayer les trois premières lettres `a`, `b` et `c`.
Tout au plus l'un d'eux rencontrera l'un ou l'autre voisin, donc nous trouverons toujours un choix approprié.

Cette approche gourmande est linéaire dans le temps et constante dans l'espace supplémentaire.

---

- Oui. 3. Le Code

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
Tous les trois ont une seule passe sur la chaîne, le temps O(n) et l'espace O(1).

---

#### 3.1 Java

"Java
// Code Leet 1576 – Remplacer tous ? pour éviter les répétitions consécutives
solution de classe {
public Chaîne modifierString(String s) {
char[] chars = s.toCharArray(); // vue mutable
int n = longueur des caractères;

pour (int i = 0; i < n; i++) {
si [chars[i]]]? {
char gauche = i > 0 ? Chars[i - 1] : '\0';
Char droit = i < n - 1 ? chars[i + 1] : '\0';

// essayer a, b, c – le premier qui ne se heurte pas
pour (char c = 'a'; c <= 'c'; c++) {
si (c != gauche && c!= droite) {
Chars[i] = c;
pause;
}
}
}
}
retourner la nouvelle chaîne(chars);
}
}
«» "

---

3.2 Python 3

'`python
Code Leet 1576 – Remplacer tous ? pour éviter les répétitions consécutives
Solution de classe:
def modifieString(self, s: str) -> str:
chars = liste(s)
n = len(chars)

pour i dans la plage(n):
Si Chars[i] == '?':
gauche = chars[i - 1] i > 0 autre Aucune
droite = chars[i + 1] si i < n - 1 autre Aucune

pour c dans 'abc': # seulement trois lettres
Si c != gauche et c != à droite :
Chars[i] = c
pause
retour ''.join(chars)
«» "

---

### 3.3 C++

'`cpp
// Code Leet 1576 – Remplacer tous ? pour éviter les répétitions consécutives
solution de classe {
public:
chaîne modifierString(chaîne s) {
int n = s.size();
pour (int i = 0; i < n; ++i) {
si (s[i] == '?') {
char gauche = (i > 0) ? s[i - 1] : '\0';
Char droit = (i < n - 1) ? s[i + 1] : '\0';

pour (char c = 'a'; c <= 'c'; ++c) {
si (c != gauche && c!= droite) {
s[i] = c;
pause;
}
}
}
}
retour s;
}
};
«» "

Les trois extraits compilent sur l'environnement officiel LeetCode et s'exécutent en < 1 ms pour la taille maximale d'entrée (`n <= 100`).

---

- Oui. 4. Pourquoi cela fonctionne – une plongée plus profonde

4.1 Validité de l'avidité
À la position `i` nous connaissons le voisin gauche (`s[i-1]`) parce que nous avons déjà remplacé un précédent `?`.
Le voisin droit (`s[i+1]`) est-ce une lettre originale ou une `?` que nous remplacerons plus tard.
Choisir une lettre distincte de **les deux** voisins garantit que, après cette étape, la sous-chaîne `[i-1.i]` est déjà valide.
Parce que nous traitons de gauche à droite, les décisions futures ne peuvent pas l'invalider: le seul caractère qui pourrait égaler `s[i]` plus tard est `s[i+1]`, mais nous l'évitons explicitement.

Ainsi, par induction, toute la chaîne reste valide.

4.2 Pourquoi trois lettres suffisent
Si les voisins de gauche et de droite sont différents, au plus deux lettres sont interdites (`a` et `b`).
S'ils sont identiques, une seule lettre est interdite.
Par conséquent, au moins un des "{a, b, c}" fonctionnera.
Il n'est pas nécessaire de scanner l'alphabet entier.

---

- Oui. 5. Cas de bord et essais

Facteurs de production Résultats attendus Raisonnement Autres
- C'est quoi ?
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" Autres
`"a?c" `"""aba"`" `?` ne peut être `a` (gauche) ou `c` (droite). Autres
""a?b?c" """"acb""""Remplacements alternatifs. Autres
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""" Autres
""a""""a"""""""" Non `?" ; la chaîne reste inchangée. Autres

L'implémentation gère les chaînes de longueur 1 et celles qui se terminent/démarrent avec `?` gracieusement parce que les contrôles voisins utilisent des valeurs sentinelles.

---

- Oui. 6. Complexité temporelle et spatiale

Algorithme Temps Espace
- C'est quoi ?
Scan de l'avidité **O(n)**

Avec `n <= 100`, c'est trivial, mais la solution s'échelle à de très longues chaînes sans modification.

---

- Oui. 7. Ce qui fait ce problème

#### 7.1 Bon – Le problème est les forces
- **Clarité** – Les contraintes sont simples : lettres minuscules + `?`.
- **Déterministe** – Il y a toujours une solution, il suffit de la trouver.
- **Échelle** – La stratégie gourmande fonctionne pour toute longueur de corde.
- **Bonne pratique** – Démontre la gestion des voisins, les valeurs sentinelles et l'édition en place.

7.2 Mauvais – Pièges potentiels
- ** Contraintes manquantes** – Oublier que la chaîne originale ne contient jamais de duplicatas adjacents.
- **Off‐by‐One Errors** – Indices du mauvais voisin (surtout à la fin).
- **Complexité inutile** – Certains peuvent sur-enginer avec des boucles complètes de l'alphabet ou du régex.

### 7.3 Motifs de code courants
- Remplacer `?` par un balayage de l'alphabet à chaque fois (`pour c dans 'abcdefghijklmnopqrstuvwxyz').
- Utilisation de chaînes ou de listes supplémentaires pour suivre les voisins (déchet de mémoire O(n)).
- Boucles imbriquées qui revisitent le même personnage plusieurs fois.

La solution propre ci-dessus évite tous ces pièges en se concentrant sur la propriété essentielle : **Seule trois lettres sont nécessaires**.

---

- Oui. 8. Autres approches (Bonus)

Démarche
C'est quoi ?
** Programmation dynamique** – suivre le caractère précédent et essayer toutes les possibilités. Il gère des variantes plus complexes. "Overkill" pour ce simple problème; temps O(n·26). Autres
**Backtracking** – Essayez chaque lettre pour chaque `?` jusqu'au succès. Temps expanentiel pour les grandes cordes. Autres
**Remplacement Regex** – `s.replaceAll("\\?","a")` puis post-processus. Rapide pour les petites cordes. Autres

S'en tenir à la méthode gourmande pour LeetCode 1576.

---

- Oui. 9. Comment cela vous aide à obtenir un emploi

- **Showcase**: La solution démontre votre capacité à lire les contraintes, à repérer les possibilités d'optimisation et à implémenter un algorithme O(n).
- **Préparation à l'entrevue**: De nombreux gestionnaires d'embauche posent des questions similaires sur le remplacement du titulaire du poste. Votre code est court, lisible et couvre les cas de bord.
- **Portfolio**: Inclure la mise en œuvre en trois langues sur GitHub avec des commentaires et un README qui explique la logique.
- **SEO-Friendly Portfolio**: Ajouter des tags comme *Code de leet 1576*, *Remplacer tous ?'s*, *Éviter les répétitions consécutives*, *Java/Python/C++ question d'entrevue*, *pratique d'entrevue de codage*, *algorithme facile*.

---

10. Enveloppe

- **Insight clé** – À chaque `?`, il suffit d'éviter les deux voisins; `a`, `b`, ou `c` fonctionneront toujours.
- **Complexité** – temps O(n), espace supplémentaire O(1).
- **Robustness** – Manipulation de tous les cas de bord, y compris les chaînes qui commencent ou se terminent par `?`.
- **Job‐Ready** – Code propre et concis en trois langues populaires, parfait pour votre trousse d'entrevue technique.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit