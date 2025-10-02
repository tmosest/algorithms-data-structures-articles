---
titre: LeetCode 3216. Lexicographiquement plus petite corde après un échange -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

3216 – Lexicographiquement Plus petite corde après un échange
** Facile**

> **Problème**
> Étant donné une chaîne `s` qui ne contient que des chiffres, vous pouvez effectuer ** au plus un** échange de * chiffres adjacents* qui ont la même parité (à la fois impair ou les deux même).
> Retourner la plus petite corde lexicographiquement qui peut être obtenue.

---

- Oui. Pourquoi ce problème est important
- **Signal d'interview :** Leetcode -Easy, mais nécessite une compréhension claire de *parité* et d'ordre lexicographique*.
- ** Compétence de codage :** Démontre un raisonnement avide, un passage linéaire et un design algorithmique à changement minimal.
- **Career Boost:** Résoudre le problème met en évidence votre capacité de lire un problème, de raisonner rapidement et de fournir une solution O(n) optimale – un trait caractéristique que les recruteurs aiment.

---

Aperçu de la solution (Greedy)

1. **Traversez la corde de gauche à droite. **
2. À la position `i`, comparez le chiffre `s[i]` et le chiffre suivant `s[i+1]`.
3. Si:
* ils ont la même parité** ('(s[i]-'0') % 2 == (s[i+1]-'0') % 2') **et**
* `s[i] > s[i+1]` (c'est-à-dire que le chiffre de gauche est plus grand que le chiffre de droite)

puis **swap** et **stop** – nous n'avons permis qu'un seul échange.
4. Si la boucle se termine sans swap, retournez la chaîne d'origine.

Parce que nous effectuons toujours l'échange *premier* possible bénéfique, la chaîne résultante est garantie d'être la plus petite lexicographiquement obtenue avec une seule paire adjacente. Ce choix avide est optimal : tout échange ultérieur n'améliorerait pas le préfixe ou nécessiterait plus d'un échange.

---

Mise en œuvre (toutes langues)

### Java

"Java
// 3216. Chaîne lexicographiquement la plus petite après un échange
solution de classe publique {
chaîne publique getSmallestString(String s) {
int n = s.longueur();
char[] arr = s.toCharArray();

pour (int i = 0; i < n - 1; i++) {
int a = arr[i] - '0';
int b = arr[i + 1] - '0';

si ((a % 2 == b % 2) && (a > b)) {
// échange une fois et sortie
la température du char = arr[i];
arr[i] = arr[i + 1];
arr[i + 1] = température;
pause;
}
}
retourner la nouvelle chaîne(arr);
}
}
«» "

---

Python

'`python
# 3216. Lexicographiquement plus petite corde après un échange
Solution de classe:
def getSmallestString(self, s: str) -> str:
arr = liste(s)
n = len(arr)

pour i dans la plage (n - 1):
a = int(arr[i])
b = int(arr[i + 1])

si a % 2 == b % 2 et a > b:
arr[i], arr[i + 1] = arr[i + 1], arr[i]
pause

retour ''.join(arr)
«» "

---

C++

'`cpp
// 3216. Chaîne lexicographiquement la plus petite après un échange
solution de classe {
public:
chaîne getSmallestString(chaîne s) {
int n = s.size();

pour (int i = 0; i < n - 1; ++i) {
int a = s[i] - '0';
Int b = s[i + 1] - '0';

Si (a % 2 == b % 2) && a > b) {
échange(s)[i], s[i + 1];
rupture; // un seul échange autorisé
}
}
retour s;
}
};
«» "

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Traversal (une seule boucle)
Conversion des chaînes (Java)

`n ≤ 100`, donc toutes les solutions fonctionnent dans un temps négligeable.

---

Les bons, les mauvais et les méchants

Catégorie: Ce qui fonctionne: Pièges potentiels: Meilleures pratiques:
- C'est quoi ?
**Bon** • Un seul passage cupide donne du temps linéaire. <br>• Pas besoin de structures de données supplémentaires. <br>• Fonctionne pour tous les cas de bord (`s` déjà minime, aucun échange valide, échange à la fin).
**Bad** <br>• L'oubli de rompre après le premier swap viole la règle de "au plus une". <br>• Une suroptimisation avec deux pointeurs peut ajouter une complexité inutile.
**Ugly**) • L'utilisation de la concaténation des cordes dans la boucle en Python (`s = s[:i] + s[i+1] + s[i] + s[i+2:]`) peut produire un comportement O(n2). <br>• En Java, recréer une nouvelle chaîne dans chaque itération serait un gaspillage. Éviter la création répétée de chaînes; utiliser des tableaux de caractères ou des chaînes de caractères.

---

Article du blog SEO-Optimized: Le code 3216 – Lexicographiquement La plus petite corde après un échange

> *Titre:** *Solve Leetcode 3216 en 5 minutes: Lexicographiquement la plus petite chaîne après un échange (Java, Python, C++)

> **Meta Description:** Apprendre à fissurer le Leetcode 3216 en moins de 5 minutes. Prenez la solution cupide complète, des extraits de code en Java, Python et C++, ainsi que des conseils d'entrevue. Obtenez le travail que vous voulez !

> **Mots-clés cibles:** *Leetcode 3216, Lexicographically Smallest String, swap chiffres adjacents, swap parité, problème de codage d'entretien, solution Java, solution Python, solution C++, conseils d'entretien d'algorithme*

- Oui. 1. Crochet – Pourquoi Ce problème est

- ** Note facile, difficile dans les interviews** – Les gens l'ignorent parce qu'il semble trivial, mais les recruteurs l'adorent comme un rapide bilan de santé mentale.
- **Application dans le monde réel** – L'échange de parités est similaire à l'optimisation des bulles dans les systèmes embarqués.

- Oui. 2. Énoncé du problème (condensé)

> Compte tenu d'une chaîne de chiffres, effectuer *au plus un* swap adjacent entre deux chiffres de même parité pour produire la plus petite chaîne possible.

- Oui. 3. Points de vue clés – Greedy Premier bon échange

- Oui. La plus petite chaîne est déterminée par la première position où un swap peut réduire le chiffre gauche.
- L'échange de la première paire admissible est toujours optimal.
- Oui. Cela réduit le problème à un seul balayage linéaire.

- Oui. 4. Code étape par étape (Java)

"Java
pour (int i = 0; i < n - 1; i++) {
si (mêmepriorité(s[i], s[i+1]) && s[i] > s[i+1]) {
échange(s), i, i+1;
pause;
}
}
«» "

Expliquez les aides `sameParity` et `swap`.

- Oui. 5. Code complet (Java, Python, C++)

Afficher les blocs de code (ci-dessus) avec de brèves notes sur les spécificités linguistiques.

- Oui. 6. Liste de contrôle des cas de bord

Motif Résultat
C'est pas vrai.
Autres Pas d'échange valide.Tous les chiffres adjacents diffèrent en parité ou déjà minimal.
Swap à la dernière paire
La comparaison lexicographique s'applique toujours

- Oui. 7. Complexité temporelle et spatiale

- **O(n)** temps, **O(1)** espace (à l'exception de la chaîne de sortie).

- Oui. 8. Conseils d'entrevue

- ** Expliquez votre raisonnement avide.** Les recruteurs cherchent *pourquoi* pas seulement *quoi*.
- **Mention de la contrainte au plus un échange** explicitement lors de la discussion de votre boucle.
- **Afficher les optimisations spécifiques au langage** (par exemple, en utilisant `StringBuilder` en Java, `char[]` en C++).

- Oui. 9. Enveloppage

- Résumez l'élégante solution à passe unique.
- Encourager les lecteurs à pratiquer les variations (swaps non adjacents, swaps multiples).
- Lien vers d'autres ressources et appel à l'action : Essaie sur Leetcode, upvote, partage. (en milliers de dollars)

10 ans. Appel à Action & SEO

- **Partager** sur LinkedIn avec #Leetcode #CodingInterview.
- **S'abonner** à votre chaîne YouTube pour des solutions plus rapides.
- Inclure un lien vers le dépôt GitHub contenant les trois solutions.

---

À emporter

- Oui. Le problème est un exercice d'avidité classique**.
- Oui. La solution est **O(n)** et trivialement implémentable dans n'importe quel langage majeur.
- Oui. En maîtrisant cela, vous mettez en évidence la capacité de **lire les contraintes de problèmes, d'élaborer une stratégie de changement minimal et de mettre en œuvre de façon propre** – exactement ce que les recruteurs recherchent.

Bon codage, et que cette interview soit une brise!