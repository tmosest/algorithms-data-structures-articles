---
titre: LeetCode 2730. Trouver la sous-chaîne semi-répétition la plus longue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> **2730. Trouvez la sous-chaîne semi-répetite la plus longue* *
> **Difficulté:** Moyenne
> **Input:** une chaîne à chiffres `s` (`1 ≤=1 ≤=50`, chaque char est `'0'...'9'`)
> ** Sortie :** la longueur de la plus longue sous-chaîne contiguë qui contient ** au plus une paire** adjacente de chiffres identiques.

Une sous-chaîne est *semi-répetitive* s'il y a **zéro ou un** indices "i" de sorte que
"substr[i] ==substr[i+1]".
Exemples:
- `"0010"` – une paire (`00`) → valide
- `"00101022"` – deux paires (`00`, `22`) → invalide

Nous avons besoin de la longueur maximale d'une telle sous-chaîne.



-----------------------------------------------------------------------------------

- Oui. 2. Algorithme – Fenêtre coulissante (Two-Pointer)

Le problème classique de la violation peut être résolu avec un **pass unique** en utilisant une fenêtre coulissante:

Étape
- C'est quoi ?
Autres 1) Conserver deux indices `gauche` et `droite` – la fenêtre actuelle `[gauche, droite]`. Autres
Autres 2) Gardez un compteur `repeats` – combien de paires égales adjacentes sont à l'intérieur de la fenêtre. Autres
Autres 3) Déplacer `droit` de `0` à `n‐1`. Après avoir déménagé, vérifiez si `s[right] == s[right‐1]`. Si c'est le cas, incrémentez les "répètes". Autres
Autres 4.- Alors que les "répètes > 1", avancer "gauche" un pas. Si vous passez au-delà d'une paire (`s[left] == s[left‐1]`) decrement `repeats`. Autres
Autres 5) Mettre à jour la réponse avec `droite - gauche + 1`. Autres

Parce que chaque index est déplacé au plus une fois, l'algorithme fonctionne dans **O(n)** temps et utilise **O(1)** espace supplémentaire.



-----------------------------------------------------------------------------------

- Oui. 3. Mise en œuvre des références

Voici des solutions propres et idiomatiques dans **Java, Python et C++**.
Tous suivent la même logique de fenêtre coulissante décrite ci-dessus.

> **Conseil:**
> Utilisez `charAt` (Java), l'indexation directe (Python, C++) et faites attention avec les erreurs hors-par-un lors de la vérification de la paire qui se termine à la nouvelle ` droite` ou commence à la nouvelle `gauche`.

---

#### 3.1 Java

"Java
***
* LeetCode 2730 – Subchaîne semi-répetite la plus longue
*
* Complexité temporelle : O(n)
* Complexité spatiale: O(1)
*/
solution de classe {
public int le plus longSemiRepetitive Sous-chaîne(String s) {
int n = s.longueur();
int gauche = 0; // limite gauche de la fenêtre
int répète = 0; // nombre de paires égales adjacentes dans la fenêtre

pour (int right = 1; right < n; right++) {
// Avons-nous créé une nouvelle paire adjacente en ajoutant s[right] ?
si (s.charAt(à droite) == s.charAt(à droite - 1)) {
répéter ++;
}

// Réduire la fenêtre jusqu'à ce que nous ayons au plus une paire
pendant la période (répètes > 1) {
// Déplacement gauche après une paire l'enlève de la fenêtre
si (s.charAt(à gauche) == s.charAt(à gauche + 1)) {
répète...
}
gauche++;
}
}
// La longueur la plus longue de la fenêtre est n - gauche (extrémité droite à n-1)
retour n - gauche;
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def leastSemiRepetitiveSubstring(self, s: str) -> Int:
n = len(s)
gauche = 0 # limite gauche
répétitions = 0 nombre nombre de paires égales adjacentes

pour droite dans la plage(1, n):
si s[droite]] [droite - 1]:
répète += 1

pendant la répétition > 1 :
si s[gauche]] s[gauche + 1]:
répéter -= 1
gauche += 1

retour n - gauche
«» "

---

### 3.3 C++

'`cpp
solution de classe {
public:
int le plus longSemiRepetitive Sous-chaîne(chaîne s) {
int n = s.size();
int gauche = 0; // limite gauche de la fenêtre
nombre de paires égales adjacentes

pour (int droite = 1; droite < n; + + droite) {
si (s[droit]] s[right - 1]) répète++;

pendant la période (répètes > 1) {
Si (à gauche) s[gauche + 1]) répète--;
gauche++;
}
}
retour n - gauche; // longueur de la fenêtre
}
};
«» "

Les trois codes fonctionnent dans le temps linéaire, utilisent une mémoire auxiliaire constante et sont prêts à être soumis.



-----------------------------------------------------------------------------------

- Oui. 4. Article du blog – Le bon, le mauvais et le mauvais des sous-chaînes semi-répétitions

> **Mot-clé – Titre :**
> *Les sous-chaînes semi-répétitions: le bon, le mauvais, le mauvais – un LeetCode 2730 Deep Plongée (Java, Python, C++)*
>
> *Pourquoi cela importe:* Ce problème est un défi de fenêtre coulissante que les intervieweurs aiment parce qu'il teste :
> 1. **Array/chaîne traversant** – pouvez-vous garder un œil sur les paires adjacentes?
> 2. **Two-pointer technique** – pouvez-vous réduire / agrandir une fenêtre efficacement?
> 3. **Manipulation de cas d'Edge** – qu'en est-il des chaînes de chiffres identiques ou de longueur‐1?
>
> Débarquer ceci sur votre CV démontre la maîtrise des algorithmes *O(n*), une compétence incontournable pour les ingénieurs logiciels dans les systèmes de production.

---

4.1 Les bonnes

1. **Complexité linéaire* *
La solution ne visite chaque personnage qu'une seule fois. Dans les entrevues, les candidats tombent souvent dans des pièges quadratiques. Une approche **O(n)** indique instantanément la maturité algorithmique.

2. **Efficacité de l'espace* *
Seules quelques variables entières sont utilisées – une quantité constante de mémoire supplémentaire. Les recruteurs apprécient les solutions qui peuvent s'étendre à de très grandes entrées.

3. ** Clarté conceptuelle**
La fenêtre coulissante est une *unique, idée propre*: Déplacer à droite, compter les violations, réduire à gauche pendant les violations>1. Pas de boucles imbriquées, pas de structures de données auxiliaires, facile à expliquer et à déboguer.

4. **Indépendant de la langue* *
La même logique fonctionne en Java, Python, C++, Allez, etc. Cette portabilité démontre une compréhension profonde des modèles algorithmiques au-delà du sucre syntaxique.

---

4.2 Les mauvais

1. **Misscompréhension du comte de Paire**
Une erreur courante de débutant est de compter ** caractères dupliqués** au lieu de * paires égales adjacentes*.
- **Dupliquer le nombre** permettrait incorrectement des chaînes comme `"121212"` (pas de duplicata) mais rejeter `"123444"` (duplicata, mais seulement une paire adjacente).
- La clé est d'examiner *indices adjacents*: `s[i] == s[i+1]`.

2. ** Erreurs hors pair**
Les limites de la fenêtre sont une source fréquente de bogues:
- Oublier de régler `gauche` après le retrait de la paire.
- Utiliser `s[left] == s[left-1]` au lieu de `s[left] == s[left+1]` lors du déplacement du pointeur gauche.

3. **Délibérations**
- Cordes à caractères simples (‘'S'=1') – la réponse est 1.
- Chaînes tout-identiques (`"111111"`) – la plus longue sous-chaîne valide est `2`.
- Cordes à chiffres multiples (`"1010101"`) – l'algorithme ne doit pas se réduire inutilement.

---

#### 4.3 L'horrible

1. **Suringénierie**
Certaines solutions introduisent des tableaux supplémentaires, des piles ou des cartes de hachage pour suivre les événements.
- Bien qu'intelligents, ils ajoutent de la complexité et des bogues potentiels.
- La fenêtre coulissante est **la solution minimale**; les structures de données supplémentaires augmentent seulement le temps/l'espace.

2. **Approche récursive ou divisatrice**
- La récursion du cloisonnement sous-chaîne peut entraîner un débordement de la pile sur de longues entrées.
- Une méthode de partage et de conquête qui fusionne les résultats de deux moitiés doit toujours gérer les paires de limites, ce qui entraîne souvent des maux de tête de coin.

3. **Blind Brute Force* *
- Essayer chaque sous-chaîne ('O(n2)'), compter les paires à l'intérieur de chaque, est **slow** et TLE sur les tests cachés de LeetCode.
- Pire, cela donne aux intervieweurs l'impression de ne pas connaître le modèle à deux points.

---

#### 4.4 Étape par étape (Java)

"Java
pour (int right = 1; right < n; right++) {
// 1. Le nouveau char a-t-il créé une nouvelle paire adjacente?
si (s.charAt(à droite) == s.charAt(à droite - 1)) {
répéte++; // nous avons maintenant une autre violation
}

// 2. Réduire jusqu'à ce que nous ayons au plus une violation
pendant la période (répètes > 1) {
si (s.charAt(à gauche) == s.charAt(à gauche + 1)) {
répéte--; // nous avons retiré une paire de la fenêtre
}
gauche++; // déplacer la limite gauche vers l'avant
}
}
retour n - gauche; // longueur de la fenêtre plus longue
«» "

*Pourquoi cela fonctionne: *
- Lorsque `right` bouge, la seule nouvelle violation qui peut apparaître est entre `right-1` et `right`.
- Lorsque `repeats` dépasse `1`, nous devons contracter la fenêtre de gauche.
- La suppression du caractère le plus à gauche peut également supprimer une paire (`gauche` et `gauche+1`).
- Chaque index est traité un nombre constant de fois → temps linéaire.

---

4.5 Stratégie d'essai

Autres Test d'entrée prévu Pourquoi
C'est pas vrai.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
""5494"""""4"" chaîne entière"
""11111"""""2""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
Aucun couple adjacent
""00101022""""5""""5"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
"""""""""""0"" chaîne vide (LeetCode ne fournira jamais)"

Utiliser un harnais d'essai de petite unité pour chaque langue (JUnit, pytest, ou `assert`).

---

4.6 À emporter pour les recruteurs

- **Afficher votre raisonnement**: Expliquez que vous comptez *des paires adjacentes*, pas des duplicatas.
- ** Mettre en évidence la fenêtre coulissante** : Deux pointeurs, un compteur de violation. (en milliers de dollars)
- **Manipulation des bords de mention**: `"1111"` → réponse `2`.
- ** Ajouter une courte preuve de linéarité** : Chaque personnage est visité au plus deux fois. (en milliers de dollars)

Ces points vous rendent mémorable dans une interview technique et mettent en valeur un état d'esprit propre et prêt à la production.



-----------------------------------------------------------------------------------

- Oui. 5. Pensées finales

Les problèmes de sous-chaînes semi-répetites, bien qu'apparemment de niche, sont un **grand objectif** pour évaluer vos côtelettes de résolution de problèmes. La technique de la fenêtre coulissante est l'un des modèles d'entrevue les plus fréquemment demandés; maîtriser avec des problèmes comme LeetCode 2730 vous donne un bord.

Si vous codez en Java, Python ou C++, rappelez-vous :

1. **Paire adjacente, non dupliquée* *
2. **Fenêtre à deux points**
3. **Espace continu**
4. **Couverture des dossiers**

Déposez cela dans votre portefeuille, partagez-le sur GitHub, et vous serez bien placé pour impressionner les gestionnaires d'embauche et les pairs. Bon codage !