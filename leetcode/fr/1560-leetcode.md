---
titre: LeetCode 1560. Secteur les plus visités dans une voie circulaire -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1560. Secteur les plus visités dans une voie circulaire
### 3-Language Solution (Java-Python-C++) + SEO-Optimized Blog Post

> ** Lien de problème** – <https://leetcode.com/problèmes/most-vised-sector-in-a-circularr-track/>
> **Difficulté** – Facile
> **Tags** – Array, Math, Greedy

---

- Oui. 1. Résumé du problème

Vous organisez un marathon sur une piste circulaire avec les secteurs `n` numérotés **1 ... N**.
La course se compose de " m " rounds.
"rounds[i]" (0-based) est le secteur où commence le "i-th* round; le round se termine au secteur "rounds[i+1]".
Le coureur se déplace toujours dans l'ordre ascendant du secteur, passant de `n` à `1`.

Retourner tous les secteurs visités le nombre **maximum** de fois, trié ascendant.

> **Exemple**
> `n = 4, rondes = [1,3,1,2] → [1,2]`
> Le coureur visite les secteurs `1` et `2` deux fois, tous les autres seulement une fois.

---

- Oui. 2. Principales perspectives

Chaque cycle *plein* autour de la piste augmente chaque secteur de visite de 1, de sorte qu'il ne change jamais le maximum *relatif*.
Seule la partie **partielle** du premier secteur au dernier secteur compte.

Laissez :

- `démarrage = tours[0]`
- `end = rounds[rounds.longueur-1] "

Si `start ≤ fin`, le coureur visite les secteurs `start ... fin` inclusive.
Si `start > fin`, le chemin enveloppe:
"démarrer ... n" **alors** "1 ... fin".
Tous ces secteurs sont ceux qui reçoivent le plus de visites.

Cela donne une solution directe **O(n)** avec **O(n)** espace supplémentaire.

---

- Oui. 3. Algorithmes et complexité

Langue Heure Espace
- C'est quoi ?
**O(n)**** (liste des extrants)
Python **O(n)**
* * * * * * * *

---

- Oui. 4. Code

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<entier> la plupartVisited(int n, int[] tours) {
début int = tours[0];
int end = rondes[rounds.longueur - 1];
Liste du résultat <entier> = nouvelle liste de distribution<>();

si (démarrer <= fin) {
pour (int i = début; i <= fin; i++) résultat.add(i);
} autre {
pour (int i = 1; i <= fin; i++) résultat.add(i);
pour (int i = start; i <= n; i++) result.add(i);
}
le résultat du retour;
}
}
«» "

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def mostVisited(self, n: int, rounds: List[int]) -> Liste[int]:
début, fin = tours[0], tours[ -1)
si début <= fin:
liste de retour(fourchette(début, fin + 1))
liste de retour(intervalle(1, fin + 1)) + liste(intervalle(début, n + 1))
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>

solution de classe {
public:
mt::vector<int> mostVisited(int n, const std::vector<int>& rounds) {
début int = rounds.front();
int fin = rounds.back();
std::vector<int> res;
si (démarrer <= fin) {
pour (int i = début; i <= fin; ++i) res.push_back(i);
} autre {
pour (int i = 1; i <= fin; ++i) res.push_back(i);
pour (int i = start; i <= n; ++i) res.push_back(i);
}
retour rés;
}
};
«» "

Les trois solutions fonctionnent dans le temps **O(n)** et n'utilisent que la liste de sortie comme espace supplémentaire.

---

- Oui. 5. Article de blog – Le bon, le mauvais, et le mauvais: résoudre le leetCode 1560 (Secteur le plus visité)

> **Méta-Description**: Découvrez comment cracker LeetCode 1560 -Les plus visités Secteur dans une piste circulaire avec des solutions simples Java, Python et C++. Obtenez les parties "good", "bad" et "ugly" expliquées et boostez votre interview prep.

---

5.1 Introduction

Lorsque vous vous préparez à coder des interviews, LeetCodes Les plus visités Secteur dans une piste circulaire (Problème 1560) apparaît souvent. C'est une question **facile** qui vous apprend à penser aux boucles *partielles* versus *plein* et à la façon dont une structure circulaire peut être manipulée avec des maths simples.

Dans cet article, nous disséquerons:

1. **Le Bon** – L'idée élégante que seule la fenêtre de départ est importante.
2. **Les mauvais** – Ce que beaucoup de débutants font (simuler tout le marathon) et pourquoi il est gaspillé.
3. **L'Ugly** – Cas d'Edge qui font monter les gens (début > fin, regroupement d'un seul secteur).

Nous terminerons avec un code propre, prêt à coller pour **Java, Python et C++**.

> **Références clés**:
> Les plus visités Secteur LeetCode, Solution Java, LeetCode 1560 Python, C++ LeetCode Circular track, C++

---

5.2 La bonne – Fenêtre monopass

L'observation clé est qu'un **plein cercle** ajoute `+1` à chaque secteur de visite. Cela ne change pas quel secteur est le plus visité. Ainsi, seul le segment **partial** du premier secteur au dernier secteur compte.

- Si le premier secteur (démarrage) est le dernier secteur (démarrage), le chemin est simplement le «démarrage... fin».
- Si `démarrer > fin`, le coureur enroule autour:
"démarrer ... n" **alors** "1 ... fin".

Ces secteurs sont visités une fois de plus par rapport au reste, donc ils sont la réponse.

---

5.3 Les mauvaises – Simulation naïve

Une erreur courante est de simuler tout le marathon:
«» "
pour i dans la plage (m):
traversée de rounds[i] à rounds[i+1] # étape par étape
«» "
C'est **O(m * n)** dans le pire des cas, et pour les contraintes données (`n, m <= 100`) il passe encore, mais il est inutile et confus. L'approche de la fenêtre propre est **O(n)** et plus facile à raisonner.

---

#### 5.4 Les horribles cas de bord

Autres Décision Pourquoi ça compte ?
Il n'y a pas de lien entre les deux.
"démarrage > fin" Le chemin d'enroulement se divise en deux plages. Autres
Autres Une seule piste du secteur (`n = 2`, de nombreux tours) L'algorithme retourne automatiquement le bon jeu. Autres
Autres Tous les secteurs visités également ( 'rounds = [1, 3, 5, 7] ' avec 'n=7 ') , la fenêtre couvre tout le cercle. Autres Notre logique renvoie `[1,2,3,4,5,7]`. Autres

---

5.5 Captures de code

**Java**

"Java
liste publique<entier> la plupartVisited(int n, int[] tours) {
début int = tours[0];
l'extrémité int = rounds[rounds.longueur-1];
Liste <Integer> ans = nouvelle liste de distribution<>();

si (démarrer <= fin) {
pour (int i=start; i<=end; i++) ans.add(i);
} autre {
pour (int i=1; i<=end; i++) ans.add(i);
pour (int i=start; i<=n; i++) ans.add(i);
}
le retour des an;
}
«» "

**Python**

'`python
def mostVisited(n, rounds):
début, fin = tours[0], tours[ -1)
si début <= fin:
liste de retour(range(start, fin+1))
liste de retour(range(1, fin+1)) + liste(range(start, n+1))
«» "

**C++**

'`cpp
vector<int> mostVisited(int n, const vector<int>& rounds) {
début int = rounds.front();
int fin = rounds.back();
vecteur<int> rés;
si (démarrer <= fin) {
pour (int i=start; i<=end; ++i) res.push_back(i);
} autre {
pour (int i=1; i<=end; ++i) res.push_back(i);
pour (int i=start; i<=n; ++i) res.push_back(i);
}
retour rés;
}
«» "

Tous les trois fonctionnent dans **O(n)** temps, **O(n)** espace, et n'utilisent aucune structure de données supplémentaires au-delà de la liste de résultats.

---

#### 5.6 Pourquoi ce selfs entrevues

1. ** Pensée claire** – Vous isolez le chemin *partial*, une technique d'entrevue commune pour réduire la complexité.
2. **Efficacité du temps** – O(n) est optimal; les intervieweurs aiment les solutions qui raisonnent sur les contraintes.
3. **Agnostisme linguistique** – La même idée de cartes à Java, Python, C++ – un bon point de discussion.

---

5.7 Pensées finales

- **Bonne**: L'élégant "start‐to‐end window" réduit le problème à deux gammes simples.
- **Bad**: Simuler chaque étape est exagéré et obscurcit la perspicacité.
- **Ugly**: Les cas de bord (enveloppés, plein circle) sont faciles à rater; l'approche de la fenêtre les gère automatiquement.

Implémentez cette solution, comprenez l'intuition sous-jacente, et vous aurez non seulement LeetCode 1560 mais toute question d'entrevue qui implique des tableaux circulaires ou le comptage du chemin.

---

#### Joyeux Codage – et bonne chance pour votre prochain entretien!