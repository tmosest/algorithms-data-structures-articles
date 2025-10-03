---
titre: LeetCode 2038. Supprimer les pièces colorées si les deux voisins sont de la même couleur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2038 – Supprimer les pièces colorées si les deux voisins sont de la même couleur
> **LeetCode 2038 – Théorie du jeu + Greedy**
> *Solved en Java, Python et C++ – couverture 100 % des cas de test*

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Game-Theory Insight](#game-theory-insight)
3. [La formule « Bonne » – Une seule ligne] (# la bonne)
4. [Le "Bad" – Cas de bord et pièges communs] (#the-bad)
5. [Le "Ugly" – Quand l'avidité s'affole (pourquoi il n'y a pas ici)]
6. [Solution passante](#solution passante)
7. [Analyse de la complexité] (#analyse de la complexité)
8. [Code complet (Java / Python / C++)](#code complet)
9. [Références géographiques et perspectives de carrière](#seo-takeaways)
10. [Autres lectures et ressources](#ressources)

---

- Oui. 1. Aperçu du problème<un nom="problème-overview"></a>
Avec une chaîne `colors` composée uniquement de `'A'` et `'B'`, deux joueurs jouent à un jeu à tour de rôle:

Déplacement du joueur Restrictions Autres
- C'est quoi ?
**Alice** (premier)=Enlever un morceau de couleur **A**=Le morceau **doit** avoir *deux* voisins de couleur **A** (ne peut pas être sur un bord). Autres
**Bob** Autres

Si un joueur ne peut pas bouger à son tour, il perd.
Retourner `true` si Alice gagne, sinon `faux`.

*Contrôles*
"1 ≤ couleurs. longueur ≤ 105 "
- `couleurs[i] -- { 'A', 'B' }'

---

- Oui. 2. Game-Theory Insight<a name="game-theory-insight"></a>
À première vue, le jeu se sent comme un jeu combinatoire impartial typique.
Cependant, les *seulement* pièces qui peuvent jamais être retirées sont ceux qui sont ** strictement à l'intérieur** un bloc de la même couleur.
Les conséquences :

1. **Enlever une pièce d'un bloc ne crée jamais une nouvelle pièce amovible de la couleur *autre*. **
La seule chose qui peut arriver est que le bloc *même* rétrécit par un, peut-être détruire une pièce amovible à l'intérieur.

2. ** Les deux joueurs jouent de manière optimale et alternative. **
Par conséquent, le gagnant est décidé par le *compte* des déplacements possibles de chaque joueur au départ.
Si Alice peut faire plus de mouvements que Bob, elle épuisera ses mouvements d'abord et forcera Bob à n'en avoir aucun, garantissant une victoire.
Inversement, si les mouvements de Bob sont ≥ Alice, Bob peut survivre plus longtemps et gagner.

Ainsi, le problème s'effondre à un problème de comptage *simple*.

---

- Oui. 3. La formule « Bonne » – Une seule ligne<un nom « bonne »></a>
Pour chaque bloc maximal de caractères égaux consécutifs (par exemple, "AAA" ou "BBBB""), le nombre de pièces amovibles à l'intérieur de ce bloc est "max(blockLength − 2, 0)".
Pourquoi ?

- Oui. Il faut au moins trois pièces identiques (AAA) pour que le milieu ait deux voisins identiques.
- Oui. Les premiers et derniers morceaux du bloc sont sur le bord de ce bloc, de sorte qu'ils ne peuvent pas être enlevés.
- Enlever le milieu réduit la taille du bloc de 1, potentiellement détruire un mouvement futur, mais **ceci est déjà capturé par le décompte initial**.

Donc l'algorithme est :

«» "
nombreA = nombre de pièces amovibles 'A'
nombreB = nombre de pièces amovibles 'B'
Compte de retourA > compteB
«» "

Pas de simulation, pas de récursion, pas de DP – temps O(n), mémoire O(1).

---

- Oui. 4. Le "Bad" – Cas de bord et pièges communs <un nom "the-bad"></a>

Ce qui arrive
- C'est quoi ?
**Tranche d`empattement**= Aucun mouvement pour personne → Bob gagne== Retour `faux` si longueur < 3 (pas de pièces d`intérieur)=
Autres **Tous les mêmes caractères**= Un seul bloc → count = len−2=1 Assurez `max(len−2, 0)` Autres
**D'autres caractères** ("ABAB" etc.)
**Leading / pièces du bord de la piste** Notre logique de bloc les exclut automatiquement (la longueur du bloc est entièrement exécutée). Autres
** Longue durée de 3** ("AAA"" ou "BBB"") Exactement une pièce amovible
Autres **Très long terme de 100000**

---

- Oui. 5. Le "Ugly" – Quand l'avidité s'affole (Pourquoi il n'y a pas ici)<un nom "le-gros"></a>
Dans de nombreux jeux à tour de rôle, une approche gourmande (toujours choisir le meilleur mouvement immédiat) est *incorrecte*.
On pourrait penser qu'Alice pourrait stratégiquement enlever une pièce qui crée une nouvelle pièce amovible pour Bob, etc.
Mais ici, **Toute** suppression seulement *réduit* le bloc de la même couleur et ne crée jamais de nouvelles opportunités pour l'adversaire.
Par conséquent, le jeu est «Greedy‐safe» : vous comptez simplement les mouvements disponibles.
C'est la laid simplicité qui transforme un jeu complexe en un seul liner.

---

- Oui. 6. Démarche de solution<un nom="solution-démarche"></a>

1. Itérer sur la chaîne, en regroupant des caractères identiques consécutifs.
2. Pour chaque groupe, si le caractère est `'A'`, ajouter `max(len−2, 0)` à `countA`.
Si `'B'`, ajouter `countB`.
3. Après la boucle, comparez les deux compteurs.
4. Retour `true` si `countA > countB`, sinon `faux`.

---

- Oui. 7. Analyse de complexité<un nom="analyse de complexité"></a>

Valeur métrique
C'est pas vrai.
Temps `O(n)` – passage unique sur la chaîne
Espace – seulement quelques compteurs entiers

Les deux respectent les limites de LeetCodes confortablement même pour `n = 105`.

---

- Oui. 8. Code complet (Java / Python / C++)<a name="full-code"></a>

### Java (style LeetCode)

"Java
// 2038. Supprimer les pièces colorées si les deux voisins sont de la même couleur
// Heure: O(n) Espace: O(1)

solution de classe {
public booléen gagnant OfGame (couleurs de la chaîne) {
nombre intA = 0, nombreB = 0;
i = 0, n = couleurs.longueur();

pendant que (i < n) {
char cur = couleurs.charAt(i);
j = i;
pendant que (j < n& colors.charAt(j) == cur) j++;
int len = j - i;
i (curir)
countA += Math.max(len - 2, 0);
Autre
countB += Math.max(len - 2, 0);
i = j;
}
le compte de retourA > compteB;
}
}
«» "

### Python (style LeetCode)

'`python
# 2038. Supprimer les pièces colorées si les deux voisins sont de la même couleur
♪ Heure: O(n) Espace: O(1)

Solution de classe:
def winnerOfGame(self, couleurs: str) -> C'est vrai.
count_a = count_b = 0
i = 0
n = len(couleurs)

alors que i < n:
cur = couleurs[i]
j = i
alors que j < n et couleurs[j] == cur:
j += 1
longueur = j - i
Si cur == 'A':
count_a += max(longueur - 2, 0)
Sinon:
count_b += max(longueur - 2, 0)
i = j

retourner count_a > count_b
«» "

> **Pythonic one-liner (pour des interviews qui aiment la brièveté)* *

'`python
de itertools importer groupeby
Solution de classe:
def winnerOfGame(self, couleurs: str) -> C'est vrai.
c = {ch: max(0, somme(1 pour _ en grp) - 2)
pour ch, grp dans groupby(colores)}
retour c.get('A', 0) > c.get('B', 0)
«» "

C++ (style LeetCode)

'`cpp
// 2038. Supprimer les pièces colorées si les deux voisins sont de la même couleur
// Heure: O(n) Espace: O(1)

solution de classe {
public:
bool gagnantOfGame(couleurs de chaîne) {
nombre intA = 0, nombreB = 0;
int n = colors.size(), i = 0;

pendant que (i < n) {
char cur = couleurs[i];
j = i;
pendant que (j < n& colors[j] == cur) ++j;
int len = j - i;
i (curir)
countA += max(len - 2, 0);
Autre
countB += max(len - 2, 0);
i = j;
}
le compte de retourA > compteB;
}
};
«» "

> Compilez avec `-std=c++17` ou `-std=c++14` – LeetCode utilise C++17 par défaut.

---

- Oui. 9. SEO & Career‐Boosting Takeaways<a name="seo-takeaways"></a>

SEO Mots-clés Pourquoi ça compte Comment ça booste votre CV
Ce n'est pas le cas.
LeetCode 2038 est un brag
Autres ** Théorie de l'image**
**Manipulation d'un support**
**O(n) solution**
**Programmation compétitive**= Compétence souhaitée pour les entreprises de pointe
**Interrogatoire sur l'algorithme**

> **Astuce**: Ajoutez une courte section à votre logiciel GitHub README intitulé -LeetCode 2038 – Game Theory + Greedy et un lien vers les solutions. Les recruteurs cherchent souvent GitHub pour le code 2038.

> **Si vous préparez une entrevue de codage* *
> 1. Commencez par une simulation *brute-force* pour comprendre les règles.
> 2. Demandez si les mouvements peuvent créer de nouveaux mouvements pour l'adversaire.
> 3. Réalisez que la réponse est un *compte* → vous êtes déjà fait.
> 4. Préparez le liner unique comme le pitch de l'ascenseur dans une entrevue.

---

- Oui. 10. Lecture et ressources supplémentaires<a name="resources"></a>

- **LeetCode Problème 2038** – [lien](https://leetcode.com/problèmes/remove-colored-pieces-if-oth-voix-are-the-meme-color/)
- **GroupBy / itertools** – Livre de cuisine Python sur les chaînes *chunking*
- ** Théorie du jeu de base** – Théorie du jeu mixte de Berlekamp, Conway & Guy (PDF gratuit en ligne)
- ** Programmation compétitive 3** – Chapitre sur la manipulation des chaînes* et les scans linéaires*
- **Dépassement de la pile** – Discussion sur Pourquoi O(n) compter fonctionne pour ce jeu impartial

---

La pensée finale

*Qu'est-ce que cette solution vous donne? *
- **Un extrait concret, prêt à l'essai** vous pouvez coller dans une entrevue de codage ou une discussion LeetCode.
- Un exemple clair** de la façon dont la théorie du jeu peut réduire un problème apparemment complexe à une seule ligne.
- Une entrée **portfolio** qui montre aux recruteurs que vous pouvez repérer des modèles, raisonner sur un jeu optimal, et fournir une solution efficace dans toute langue que vous aimez.

Bon codage – et que vos points LeetCode s'accumulent !