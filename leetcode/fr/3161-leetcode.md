---
titre: LeetCode 3161. Demandes de renseignements sur le placement des blocs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour l'escalier nous connaissons les limites

«» "
1 , 2 , ..., MAX
«» "

Pendant le jeu certaines de ces positions deviennent * obstacles*.
Si vous êtes debout sur une marche `a`, vous pouvez marcher seulement à droite.
Dès que vous marchez sur un obstacle, la marche s'arrête.
La requête `P a` demande le nombre maximal de mesures qui peuvent être prises
à partir de l'étape `a`.

-----------------------------------------------------------------------------------

C'est vrai. 1. Observation

Un obstacle ne disparaît jamais – il s'ajoute seulement.
Tous les obstacles divisent l'ensemble de la gamme en disjoints
intervalles

«» "
D'abord Obstacle,
(premier obstacle, deuxième obstacle),
(deuxième obstacle, troisième obstacle), ...,
(dernier obstacle, +)
«» "

La marche commençant à `a` ne peut utiliser que l'intervalle qui contient `a`
et il doit s'arrêter **avant** le prochain obstacle à droite.
Par conséquent, la réponse pour une requête `P a` est

«» "
suivantObstacleOnRight – a – 1
«» "

`nextObstacleOnRight` est le premier obstacle dont la position est plus grande
que «a».
Si `a` est un obstacle, la marche est déjà bloquée – la réponse
est "0".

-----------------------------------------------------------------------------------

C'est vrai. 2. Structure des données

L'ensemble des positions d'obstacles doit soutenir

* insérer un nouvel obstacle,
* demander si une position est un obstacle,
* trouver le premier obstacle plus grand qu'une position donnée.

Toutes les opérations sont nécessaires en temps logarithmique.
Un arbre de recherche binaire équilibré (`TreeSet` en Java) est parfait pour cela.
Deux obstacles fictifs sont insérés une fois par cas d'essai:

«» "
-1 – juste avant la première étape réelle
MAX + 1 – juste après la dernière étape réelle
«» "

Avec ces deux sentinelles "haut(a)" (le premier élément est supérieur à
`a`) est toujours défini pour chaque `a` entre `1` et `MAX`.

-----------------------------------------------------------------------------------

C'est vrai. 3. Algorithme

Pour chaque essai

«» "
lire MAX et Q
Obs ← TreeSet contenant -1 et MAX+ 1

répéter Q fois
lire type (C ou P) et valeur v
si type = 'C' // créer un obstacle
(v)
sinon // type = 'P', requête
si obs.contient(v)
sortie 0
Autre
suivant ← obs.higher(v)
sortie (suivant - v - 1)
«» "

-----------------------------------------------------------------------------------

C'est vrai. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme imprime la bonne réponse pour chaque requête.

---

Lemma 1
Laissez `O` être le premier obstacle strictement plus grand que `a`.
Toute marche qui commence à l'étape `a` et ne marche pas sur un obstacle
contient exactement "O - a - 1".

**Prof.**

Toutes les étapes entre `a` et `O-1` sont exemptes d'obstacles, car
'O' est le premier obstacle à droite.
La marche peut se déplacer à `O-1`, qui est la dernière étape libre.
Après cela, la prochaine étape serait sur "O", un obstacle, qui est
Non autorisé.
Ainsi la marche se compose des marches

«» "
a, a+1, ..., O-1
«» "

dont la longueur est "O-1 - a + 1 = O - a - 1".



Lemma 2
Si l'étape `a` est elle-même un obstacle, le nombre maximum d'étapes
peut être pris de `a` égale `0`.

**Prof.**

Vous commencez sur un obstacle, donc vous êtes déjà bloqué et
ne peut faire aucun pas. *



Lemma 3
Pour chaque étape `a` entre `1` et `MAX` l'algorithme retourne
`0` si `a` est un obstacle et renvoie `O - a - 1`,
où `O` est le premier obstacle à la droite de `a`.

**Prof.**

Le jeu `obs` contient toujours tous les obstacles actuels.
Si `a` est dans `obs`, les sorties de l'algorithme «0» – par Lemma 2
C'est la bonne réponse.

Sinon, l'algorithme obtient "next = obs.higher(a)".
Parce que le jeu contient également les sentinelles `-1` et `MAX+1`,
`next` est précisément le premier obstacle strictement plus grand que `a`.
L'algorithme produit `prochain - a - 1`.
Par Lemma 1 cela équivaut à la longueur de la plus longue marche admissible
à partir de "a".



C'est vrai. Théorème
Pour chaque requête de type `P a`, l'algorithme imprime le maximum
nombre possible d'étapes à suivre depuis l'étape «a».

**Prof.**

Par Lemma 3 la valeur imprimée par l'algorithme égale la longueur
de la plus longue marche qui ne traverse pas un obstacle.
Toute marche admissible doit se terminer avant le premier obstacle à droite,
donc ne plus marcher existe.
Par conséquent, la valeur imprimée est exactement le maximum requis. *



-----------------------------------------------------------------------------------

C'est vrai. 5. Analyse de la complexité

Que `N` soit le nombre d'obstacles qui ont été ajoutés
(y compris les deux sentinelles).

*Chaque insertion* ou *lookup* dans `TreeSet` coûte `O(log N)` temps.
Toutes les requêtes `Q` sont traitées dans
"O(Q · log N)".
Le set stocke au plus des valeurs `N`, donc la consommation de mémoire est
«O(N)».

-----------------------------------------------------------------------------------

C'est vrai. 6. Mise en œuvre des références (Java 17)

"Java
importation java.io.*;
Importation de java.util.*;

classe publique {

/* --------- scanner rapide ---------- */
classe statique privée FastScanner {
Finale privée BufferedInputStream in;
octet final privé[] tampon = nouvel octet[1 << 16];
Int privé ptr = 0, len = 0;

FastScanner(InputStream is) { in = nouveau BufferedInputStream(is); }

int private readByte() lance IOException {
si (ptr >= len) {
len = in.read(buffer);
ptr = 0;
si (len <= 0) retour -1;
}
retour du tampon[ptr++];
}

chaîne privée next() lance IOException {
StringBuilder sb = nouveau StringBuilder();
Int c;
Faites {
c = readByte();
si (c) -1) retour nul;
} tandis que [Character.isWhitespace(c)];

Faites {
sb.annexe(char) c);
c = readByte();
} pendant que (c != -1 &&!Caracter.isWhitespace(c);

retour sb.toString();
}

long nextLong() lance IOException {
Chaîne s = suivante();
si (s == null) lancer une nouvelle IOException("EOF");
retour Long.parseLong(s);
}
}
/* ---------------------------------- */

public statique vide main(String[] args) lance Exception {
FastScanner fs = nouveau FastScanner (System.in);
StringBuilder out = nouveau StringBuilder();

Jeton à cordes;
pendant que ((token = fs.next()) != null) { // lire MAX
longue MAX = Long.parseLong(token);
long Q = fs.nextLong(); // nombre de requêtes

TreeSet<Long> obs = nouveau TreeSet<>();
obs.add(-1L); // sentinelle avant l'escalier
obs.add(MAX + 1); // sentinelle après l'escalier

pour (long i = 0; i < Q; i++) {
Type de chaîne = fs.next(); // "C" ou "P"
long v = fs.nextLong();

si (type.charAt(0) == 'C') { // ajouter un obstacle
(v)
} autre { // requête
si (obs.contient(v)) {
out.append('0').append('\n');
} autre {
long suivant = obs.higher(v); // premier obstacle > v
out.append(next - v - 1).append('\n');
}
}
}
}

Système.out.print(out.toString());
}
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et
conforme à la norme Java 17.