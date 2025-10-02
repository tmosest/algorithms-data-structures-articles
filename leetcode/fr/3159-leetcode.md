---
titre: LeetCode 3159. Trouver les événements d'un élément dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3159 – Trouver les événements d'un élément dans un tableau
**Type de problème:** Moyenne **Langues:** C++

---

- Oui. 1. Résumé du problème

On vous donne

Description de l'entrée
C'est pas vrai.
Un ensemble de entiers (taille ≤ 105) Autres
Un ensemble de entiers (taille ≤ 105) Autres
Un seul entier

Pour chaque «requêtes[i]» vous devez retourner l'index **** de l'occurrence *k‐th* de `x` dans `nums`, où `k = requêtes[i]`.
Si `x` se produit moins que `k` fois, retourner `-1` pour cette requête.

> **Exemple**
> `nums = [1,3,1,7]`, `queries = [1,3,2,4]`, `x = 1` → `[0,-1,2,-1]`

---

- Oui. 2. Approche directe vers l'avant

L'observation centrale : nous ne nous soucions que des positions de **x**.
Si nous pouvons rapidement cartographier l'occurrence de x.K. de x.K. → ..index dans les nombres, chaque requête devient une recherche O(1).

La solution typique est:

1. **Premier passage – Construire la carte* *
Numériser les "nums".
Chaque fois que nous voyons `x`, incrémentez un compteur `cnt`.
Conservez `cnt → current index` dans une carte de hachage.

2. **Deuxième laissez-passer – questions de réponse**
Pour chaque `k` dans `queries`, récupérer `map[k]`.
Si elle n'existe pas → `-1`.

Les deux passes sont linéaires, ce qui donne du temps à O(n + m) et de l'espace auxiliaire à O(n) (le pire cas où `x` se produit à chaque position).

---

- Oui. 3. Code (trois langues)

C'est vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
occurrences publiques int[] OfElement(int[] nombres, inter[] requêtes, int x) {
// Carte : nombre d'événements -> indice
Carte <entier, entier> carte = nouveau HashMap<>();
nombre int = 0;
pour (int i = 0; i < nombres de longueur; i++) {
si (nums[i] == x) {
count++;
la carte.put(compte, i);
}
}

int[] ans = nouvelle int[queries.longueur];
pour (int i = 0; i < requêtes.longueur; i++) {
ans[i] = map.getOrDefault(demandes[i], -1);
}
le retour des an;
}
}
«» "

Python

'`python
def occurrencesOfElement(nombres, requêtes, x):
occ = {}
cnt = 0
pour idx, val dans l'énumération(nombres):
si val == x:
cnt += 1
occ[cnt] = idx

retourner [occ.get(q, -1) pour q dans les requêtes]
«» "

C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>

utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> occurrencesOfElement(vecteur<int>& nombres,
le vecteur<int> et les requêtes,
Int x) {
non ordonné_map<int, int> mp; // occurrence -> indice
cnt = 0;
pour (int i = 0; i < (int)nums.size(); ++i) {
si (nums[i] == x) {
++cnt;
[cnt] = i;
}
}

vecteur <int> ans;
as.reserve(queries.size());
pour (int k : requêtes) {
auto it = mp.find(k);
-1 : it->second);
}
le retour des an;
}
};
«» "

---

- Oui. 4. Analyse de la complexité

Étape Temps Espace
C'est pas vrai.
Calculer la carte "O(n)" "O(n)"
Réponse aux questions (tableau de sortie non compté)
**Total** Autres

- `n` – taille du nombre "
- `m` – taille des requêtes "

Les deux passes sont des scans simples; aucune boucle nichée.

---

- Oui. 5. Cas de bord et pièges

Situation Pourquoi ça compte Comment éviter
- C'est quoi ?
`x` n`apparaît jamais=Toutes les requêtes retournent `-1`=La carte restera vide – la recherche fonctionne très bien=
Les requêtes contiennent des valeurs > nombre d'occurrences.
Importante entrée (105) : Risque de TLE ou de MLE si l'on utilise la récursion ou l'O(n2) :
"requêtes" non triées

---

- Oui. 6. Bonne, mauvaise, mauvaise de cette solution

Aspect du bien
- C'est quoi ?
**Readability**
**Performance**= O(n+m) temps optimal pour 105= Utiliser une carte de hachage → O(n) espace= Si `x` se produit dans chaque position, mémoire = O(n) mais toujours acceptable==
**Scalabilité**
* Maintenabilité * Facile à étendre (par exemple, indices de retour pour des valeurs multiples)
**Bogue potentiel**
**Pièce dure**

> **Ligne de bottom:** L'approche hash-map est *la manière la plus propre et la plus rapide de résoudre ce problème. Éviter les structures de données supplémentaires (p. ex., les listes liées) maintient le code souple et convivial pour les entrevues.

---

- Oui. 7. SEO-Optimized Blog Post

---

Titre
**Crack LeetCode 3159 – Trouver les événements d'un élément dans un tableau (Java, Python, C++)* *

Description de la méta
Master LeetCode 3159 en quelques secondes. Apprenez la solution de hash‐map, consultez le code Java/Python/C++, comprenez les compromis entre l'espace temporel et obtenez l'entrevue. Parfait pour les ingénieurs logiciels se préparant pour les entrevues de codage.

---

Introduction

Si vous chassez pour un *niveau moyen* Problème LeetCode qui est parfait pour aiguiser vos compétences de hash-map, ne cherchez pas plus loin que **3159. Trouvez les événements d'un élément dans un tableau**. Ce problème teste votre capacité à cartographier les événements pour les indexer et répondre aux requêtes en temps linéaire – un scénario d'entrevue classique.

Dans cet article, nous allons:
- Divisez le problème en anglais.
- Présentez une solution O(n+m) propre avec le code Java, Python et C++.
- Discutez de cette approche.
- Soulignez pourquoi cette solution brille dans les interviews de codage du monde réel.

---

Récapitulation du problème

Étant donné:
- `nums` – un ensemble de entiers (jusqu'à 100 000 éléments).
- `queries` – un tableau d'entiers où chaque valeur est un rang (occurrence k-th).
- `x` – la valeur cible.

Retourner un tableau où chaque élément est l'index de l'occurrence k de `x` dans `nums`, ou `-1` s'il n'existe pas.

---

C'est vrai. Pourquoi une carte Hash est la clé

L'idée simple est de passer par `nums` une fois et de se rappeler chaque position où `x` apparaît.
Une fois que nous avons que la mappage de l'index -occurrence →, chaque requête est une recherche de dictionnaire à temps constant.

Cette stratégie donne:
- **Heure linéaire** – seulement deux scans ('O(n+m)').
- **Requêtes à temps constant** – aucune boucle ni aucune recherche binaire sur une liste de positions.
- **Utilisation évolutive de l'espace** – au plus une entrée par occurrence de « x ».

---

#### Étape par étape

1. **Construire la carte**
Texte
nombre = 0
pour i en 0 ... longueur maximale-1:
si nombres[i] == x:
nombre += 1
carte[compte] = i
«» "

2. **Réponse à chaque requête**
Texte
ans[i] = map.getOrDefault(demandes[i], -1)
«» "

C'est tout. Pas de tableaux supplémentaires, pas de structures de données complexes.

---

Code des échantillons

> Voir les implémentations *Java*, *Python* et *C++* dans la section "Code" ci-dessus. Chaque extrait n'est que de quelques lignes, ce qui le rend convivial et facile à retenir.

---

C'est vrai. Tant mieux. Méchant

Caractéristiques Bonnes mauvaises
-- -- -- -- -- -- -- -- -- -- -- --
Une logique claire et concise
**Speed**= O(n+m) – optimum pour 105== Aucune –=
**L'espace**=O(n) dans le pire des cas – toujours d'amende pour 105=Hash carte au-dessus
**Maintenabilité**
**Interview-fit**. Pas de plaque de chaudière, commentaires propres.

> **Conseil d'entrevue :** Parlez à travers l'idée de cartographie avant d'écrire du code. Il montre à l'intervieweur que vous comprenez la structure des données sous-jacentes, et pas seulement l'astuce "code-it-up".

---

#### # Les gouts communs à éviter

- **Missing `x` en `nums`** – la carte reste vide, mais les recherches retournent `-1`.
- **Quêtes plus grandes que le nombre réel d'événements** – utilisez `getOrDefault` / `unordered_map::find` pour garder.
- **Bondage de mémoire** – si `x` apparaît dans chaque élément, la carte a 100 000 entrées; toujours bien dans les contraintes d'entrevue typiques.

---

À emporter

La solution de hash-map est la réponse *canonique* au LeetCode 3159. Il est concis, rapide et démontre la maîtrise des recherches de dictionnaire – exactement ce que les intervieweurs veulent voir.
Pratiquez-le jusqu'à ce que vous puissiez l'écrire en une seule ligne (Java/Python) ou en deux boucles (C++), puis vous serez prêt à répondre à cette question et à de nombreuses autres questions de plan de hachage de niveau moyen.

---

Vous voulez améliorer vos compétences en entrevue?

- Construire une aire de jeux **LeetCode** et pratiquer 5-10 problèmes par jour.
- Paire-programme avec un ami ou utilise une plateforme comme **InterviewBit** pour des entrevues simulées.
- Partagez cette solution sur LinkedIn – la communauté aime le code propre!

Bon codage, et que vos indices indiquent toujours le succès! C'est ce qu'il a dit.

---

*Sentez-vous libre de déposer un commentaire si vous avez des questions ou voulez discuter d'autres stratégies LeetCode! *