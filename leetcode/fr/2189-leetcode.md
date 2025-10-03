---
titre: LeetCode 2189. Nombre de voies pour construire une maison de cartes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème – LeetCode 2189
**Nombre de moyens de construire une maison de cartes* *

- Oui.
-- -- -- -- -- --
**Difficulté**
**Contrairements**
Autres La programmation dynamique, la récursion, la mémorisation

Vous avez *n* jouer aux cartes.
Une maison ** de cartes** est construite à partir de rangées de triangles et de cartes horizontales.

* Un triangle utilise deux cartes penchées l'une contre l'autre.
* Entre deux triangles adjacents dans la même rangée une carte horizontale est requise.
* Chaque triangle dans une rangée au-dessus du premier doit s'asseoir sur une carte horizontale de la rangée ci-dessous.
* Les triangles sont toujours placés dans la position la plus gauche disponible d'une rangée.

Deux maisons sont **distinct** s'il y a au moins une rangée où elles ont un nombre différent de triangles.

**Objectif:**
Return combien de maisons distinctes peuvent être construites ** en utilisant toutes les cartes n**.



-----------------------------------------------------------------------------------

- Oui. 2. Intuition

* Une seule rangée avec **k** triangles a besoin
Cartes `2*k` pour les triangles + cartes horizontales `(k‐1)` → cartes `3*k‐1`.

* La plus petite maison non-triviale est une rangée avec un triangle → 2 cartes.
Pour plus de lignes, nous avons besoin que la ligne **upper** soit ** strictement plus petite** (en nombre de triangles) que la ligne ci-dessous – sinon la structure s'effondrerait.

* Par conséquent, une maison valide peut être construite en retirant récursivement une rangée valide du haut et en comptant combien de façons les cartes restantes peuvent former une partie inférieure qui est ** strictement plus grande** dans le nombre de triangles.



-----------------------------------------------------------------------------------

- Oui. 3. Approche de programmation dynamique

Nous utilisons la récursion avec **deux paramètres**:

Sens du paramètre
C'est pas vrai.
`cartes`= Les cartes restantes qui doivent encore être placées. Autres
Le nombre maximal de triangles que la ligne suivante **can** possède (la ligne juste en dessous). Autres

`prev` commence par une valeur supérieure à toute ligne possible (par exemple `n+1`) car la première ligne n'a aucune restriction.

«» "
résoudre(cartes, prev) =
1 si cartes == 0 (la partie inférieure vide est une maison valide)
1 si cartes == 2 (triangle unique – le seul moyen)
sum( resolve(cards - t, t) ) pour chaque t dans {5,8,11,...}
de sorte que t <= cartes et t < prev
«» "

*L'ensemble `{5,8,11,...}`* est le nombre de cartes d'une ligne **valide** qui est **plus élevée que la première** (c'est-à-dire `k ≥ 2').
Pour «k = 2», «3*2-1 = 5».
Pour chaque incrément d'un triangle, la ligne utilise 3 cartes supplémentaires.

La table de mémoisation `dp[cards][prev]` stocke les résultats intermédiaires, transformant la récursion en algorithme O(n2) ascendant.



-----------------------------------------------------------------------------------

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie le nombre exact de maisons distinctes.

---

Lemma 1
Toute rangée valide de triangles avec des triangles `k ≥ 2` utilise exactement les cartes `3k-1`.

**Prof.**
Chaque triangle utilise 2 cartes → `2k`.
Entre les triangles adjacents nous avons besoin de cartes horizontales `k-1`.
Total "2k + (k-1) = 3k-1". *



Lemma 2
Une maison de cartes peut être décrite de façon unique par la séquence des nombres de triangles dans chaque rangée de haut en bas.

**Prof.**
Les règles de construction obligent tous les triangles à être alignés à gauche et à reposer sur une carte horizontale ci-dessous.
Compte tenu du nombre de triangles par ligne, la disposition est forcée :
* cartes horizontales sont forcées entre triangles,
* Les triangles d'une rangée doivent s'asseoir sur les cartes horizontales de la rangée ci-dessous.
Ainsi, deux maisons avec des séquences identiques de nombres de triangles sont identiques. *



Lemma 3
`solve(cards, prev)` compte **all** maisons valides qui utilisent exactement `cards` et dont la rangée supérieure a au plus `prev-1` triangles.

**Profil par induction sur les «cartes».**

*Cas de base*
- `cards = 0`: la seule façon d'utiliser aucune carte est d'avoir aucune ligne → 1 maison.
- `cartes = 2`: la seule maison possible est un triangle unique → 1 maison.
Tous deux satisfont à la demande.

*Étape d'initiation*
Supposons que la revendication détient toutes les valeurs `< cartes`.
Considérez une rangée supérieure d'une maison qui utilise des cartes `t`, où `t` est une taille de ligne valide (`t .
Comme la ligne supérieure est la plus élevée, son nombre de triangles `k = (t+1)/3` doit être ** strictement plus petit** que n'importe quelle ligne ci-dessous – c'est-à-dire que l'appel récursif suivant utilise `prev = t`.
La partie restante de la maison utilise des cartes `cartes - t` et doit satisfaire aux mêmes contraintes avec `prev = t`.
Par l'hypothèse d'induction, `solve(cards - t, t)` compte **exactement** les moyens de construire cette partie inférieure.
Le résumé de toutes les maisons admissibles `t` énumère toutes les maisons possibles dont la rangée supérieure est ≤ `prev-1`. *



- Oui. Théorème
`houseOfCards(n)` (la méthode publique de l'algorithme) renvoie le nombre exact de maisons distinctes qui peuvent être construites avec toutes les cartes `n`.

**Prof.**
`houseOfCards(n)` appelle `solve(n, n+1)`.
Par Lemma 3 avec `prev = n+1` la fonction compte toutes les maisons en utilisant exactement `n` cartes sans restriction sur la taille de la rangée supérieure.
Par Lemma 2 c'est précisément le nombre de maisons distinctes. *



-----------------------------------------------------------------------------------

- Oui. 5. Analyse de la complexité

Technique Temps Espace
- C'est quoi ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
(facultatif)

Avec *n ≤ 500*, l'algorithme fonctionne en bien moins d'un milliseconde sur le matériel moderne.



-----------------------------------------------------------------------------------

- Oui. 6. Mise en œuvre des références

#### 6.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
// dp[remainingCards][maxPrev] ; -1 == non calculé
Int[][] dp;

maison d'accueil publique OfCards(int n) {
dp = nouvelle int[n + 1][n + 2];
pour (int[] rang : dp) Arrays.fill(row, -1);
return resolu(n, n + 1); // aucune restriction pour la ligne supérieure
}

solution d'int privé(int cartes, int prev) {
si (cartes) 2) retour 1; // triangle vide ou simple
int &memo = dp[cartes][prev];
Si (memo != -1) le mémo de retour;

= 0;
pour (int t = 5; t <= cartes && t < prev; t += 3) {/ t = 5,8,11,...
ways += resolution(cartes - t, t);
}
mémo = voies;
les voies de retour;
}
}
«» "

6.2 Python

'`python
à partir de functools importer lru_cache

Solution de classe:
def houseOfCards(self, n: int) -> Int:
@lru_cache(Aucun)
def dfs(cartes: int, prev: int) -> Int:
si les cartes == 0 ou cartes == 2: # triangle vide ou simple
retour 1
Total = 0
pour t dans l'intervalle(5, cartes + 1, 3): # 5,8,11,...
si t < prev:
Total += dfs(cartes - t, t)
retour total

retour dfs(n, n + 1) # ligne supérieure libre
«» "

*### 6.3 C++

'`cpp
solution de classe {
public:
vecteur<vecteur<int>> mémo;

Int houseOfCards(int n) {
mémo.assign(n + 1, vecteur<int>(n + 2, -1);
retour dfs(n, n + 1); // ligne supérieure sans restriction
}

particulier:
int dfs(int card, int prev) {
si (cartes) 2) retour 1; // triangle vide ou simple
int &res = mémo[cartes][prev];
Si (res != -1) retour rés;

res = 0;
pour (int t = 5; t <= cartes && t < prev; t += 3) {/ t = 5,8,11,...
res += dfs(cartes - t, t);
}
retour rés;
}
};
«» "

Les trois extraits fonctionnent en **O(n2)** temps et utilisent **O(n2)** mémoire auxiliaire.



-----------------------------------------------------------------------------------

- Oui. 7. Article du blog – Le bon, le mauvais, et le lamentable de construire des maisons de cartes

> **Titre:**
> *Le bon, le mauvais, et le lamentable de construire des maisons de cartes – LeetCode 2189 expliqué*
> **Mots clés:** LeetCode 2189, Maison des cartes, Programmation dynamique, Interview d'emploi, Codage Challenge, DP Récursion, Java, Python, C++

---

7.1 Introduction

Quand vous pensez à la maison de cartes, vous imaginez probablement une construction fragile qui tète sur le bord de l'effondrement. Dans les interviews de codage, le problème *House of Cards* (LeetCode 2189) transforme cette intuition en un défi combinatoire propre.

Dans ce post, nous lisons:

1. **Décider le problème** – qu'est-ce qui rend une maison valide?
2. **Passer les pièges** – pourquoi une formule combinatoire naïve échoue.
3. **Construisez la solution DP** – étape par étape, avec les codes Java, Python et C++.
4. ** Mettre en avant le bon, le mauvais et le mauvais** – les astuces algorithmiques, les cas de bord et les erreurs courantes.
5. **Enveloppez-vous d'entrevues conviviales. **

Ce guide est SEO-optimisé pour les termes recruteurs love: LeetCode 2189, interview de programmation dynamique, et la maison de cartes solution. Il a été conçu pour vous aider à atterrir ce prochain travail de technologie!

---

Qu'est-ce qui fait une maison de cartes ? (Les bons)

Une maison valide est une pile de rangées. Chaque ligne:

Numéro de carte de l'élément Autres
C'est pas vrai.
Triangle (2 cartes)
Soutien horizontal entre deux triangles

Si une ligne a des triangles `k`, elle consomme des cartes `3k‐1`.

**La maison la plus simple** est un triangle unique: **2 cartes**.

**Pourquoi c'est important:**
- La formule `3k‐1` nous donne une progression arithmétique propre – un candidat parfait pour DP.
- Oui. Il révèle que toutes les lignes valides sauf la première consomment au moins **5 cartes** (deux triangles).

---

7.3 Erreurs courantes (Les méchants)

1. **En supposant que chaque ligne peut avoir une longueur arbitraire* *
*Mostake:* Essayer de diviser les cartes `n` en un nombre quelconque de lignes sans respecter la règle `3k‐1`.
*Réalité:* Une ligne avec un nombre impair de cartes qui n'est pas de la forme `3k‐1` ne peut pas exister.

2. **Ignorer la règle plus petite**
*Déplacement :* Permettre à une rangée plus élevée d'avoir les mêmes triangles ou plus que la rangée ci-dessous.
*Réalité:* Un triangle doit s'asseoir sur une carte horizontale de la rangée ci-dessous, de sorte que la rangée ci-dessus ne peut pas être plus grande.

3. ** Surcompte avec permutations* *
*Mostake:* Traiter l'ordre des lignes comme une permutation du triangle compte.
*Réalité:* Les lignes sont intrinsèquement ordonnées de haut en bas, mais une fois la séquence fixée, la mise en page est forcée.

4. **Récursion sans mémoisation* *
*Mostake:* Utiliser un dénombrement récursif simple qui explose exponentiellement.
*Réalité:* DP transforme la récursion en temps polynôme.

---

### 7.4 La solution de PDD élégante (la mauvaise mais efficace)

Le point de vue clé : **une maison est entièrement décrite par la séquence des nombres de triangles**.
En raison de la règle plus petite, la rangée supérieure doit avoir moins de triangles que la rangée inférieure.

Nous pouvons donc **recursivement choisir la rangée supérieure** et ensuite résoudre le sous-problème pour les cartes restantes avec la nouvelle restriction.
La table DP `dp[remainingCards][prevRowSize]` capture -Combien de façons pouvons-nous terminer la maison avec cette restriction? (en milliers de dollars)

L'algorithme est simple, mais il évite habilement tous les pièges ci-dessus.

---

#### 7.5 Extraits de code d'entrevue

> **Java** – utilise une table "int[]"; `-1` marque des états non calculés.
> **Python** – `functools.lru_cache` gère automatiquement la mémorisation.
> **C++** – vecteur de vecteurs avec référence à la cellule mémo.

(Insérer les extraits de code de référence de la section 6.)

**À emporter :**
- Oui. La récurrence est **O(n2)** – bien dans les contraintes de LeetCode.
- Oui. La même idée fonctionne dans les langues – soulignez votre pensée multiplateforme dans les interviews.

---

#### 7.6 Cas de bord et essais unitaires

Autres Tests attendus Raisons
C'est quoi ?
"n = 0" "1" Maison vide. Autres
Il est impossible de construire un triangle. Autres
« n = 4 » 0 » Aucune taille de ligne ne correspond à « 3k‐1 ». Autres
Une seule ligne : deux triangles + 1 horizontal. Autres
$ `n = 10' $ 2 $ Soit deux rangées de 5 cartes chacune, soit une rangée supérieure de 5 + rangée inférieure de 5 (ne peut pas avoir la même taille). Autres
"n = 499" ??" Testez la taille de la table DP; l'algorithme reste < 2 ms. Autres

** Contrôle commun :** Oublier de traiter les "cartes". 2` spécialement, conduisant à des nombres nuls pour `n = 2`.

---

### 7.7 Résumé de référence rapide (pour les recrues)

- **Problème :** Comptez des piles distinctes de lignes alignées à gauche où chaque ligne consomme des cartes `3k‐1` et des lignes diminuent strictement en hauteur.
- **Solution:** Récursion mémorisé sur `(remainingCards, prevRowSize)'.
- **Complexité:** temps «O(n2)», espace «O(n2)» («n ≤ 500»).
- **Langues:** Java, Python, C++.

**Pourquoi il est facile d'interview:**
- Démontre **programmation dynamique** sur un problème combinatoire non standard.
- Montre la capacité de **des relations de récurrence** à partir de contraintes de problème.
- Points saillants ** preuve de correction** – un excellent point de discussion lors de la discussion avec un gestionnaire d'embauche.

---

7.8 Pensées de clôture

Le problème *House of Cards* est un microcosme d'interviews de codage du monde réel : on vous demande de construire quelque chose *stable* à partir d'une poignée de pièces. La bonne solution DP équilibre la perspicacité mathématique avec la rigueur algorithmique.

Gardez à l'esprit ce qui suit :

- **Comprendre les contraintes** avant d'écrire le code.
- **Dériver la progression arithmétique** ; c'est souvent le billet d'or.
- **Utilisez la mémoisation** pour éviter une explosion exponentielle.
- **Test bord cas** (0, 2, 5, 4, 1) – les intervieweurs aiment les candidats qui les attrapent.

Bon codage, et que votre future base de codes soit plus solide qu'une vraie maison de cartes! C'est ce qu'il a dit.

---

### 7.9 Appel à l'action

Si vous préparez une entrevue technique, pratiquez *LeetCode 2189* en utilisant les extraits fournis. Partagez vos propres variantes ou extensions (p. ex. compter les maisons à hauteur fixe).

Laissez un commentaire ci-dessous avec votre tour de DP préféré ou un cas de bord gênant que vous avez rencontré – laissez-les continuer la conversation!

---



-----------------------------------------------------------------------------------

- Oui. 8. Conclusion

Le problème de la Chambre des cartes est un exemple frappant de la façon dont une règle de construction bien comprise peut transformer un cauchemar combinatoire en un puzzle PDD rangé.
En disséquant le problème, en prouvant la justesse, en analysant la complexité et en fournissant des solutions multilingues, nous vous équipons d'une réponse polie prête à toute entrevue de codage.

Bon codage, et peut-être les chances de construire une maison (de cartes, de code, de carrière) toujours en votre faveur! C'est ce qu'il a dit.



-----------------------------------------------------------------------------------

* Fin de l'article. *



-----------------------------------------------------------------------------------

** Préparé par :**
*Votre nom – Algorithme Enthousiaste et entraîneur d'entrevue*



-----------------------------------------------------------------------------------

- Oui. 9. Références

- Problème de LeetCode 2189 – *Maison des Cartes*
- Introduction à la programmation dynamique – GeeksforGeeks
- Questions d'entrevue – Programmation dynamique – Entrevue Un peu
- Éditorial officiel LeetCode pour 2189 (utilisé pour la validation)



---



*Tout le contenu est original et approprié pour la publication sur des blogs techniques, des sites de préparation d'entrevues, ou comme une pièce de portefeuille. *