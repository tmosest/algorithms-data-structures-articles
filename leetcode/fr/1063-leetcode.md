---
titre: LeetCode 1063. Nombre de subarrays valides -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1063 – Nombre de substituts valides
**Hard** – LeetCode

> **Objectif**
> Pour un tableau «nums», compter chaque sous-aire contiguë dont l'élément *leftmost* est **pas plus grand** que tout autre élément de ce sous-aire.
> (En d'autres termes, l'élément le plus à gauche est le minimum de cette sous-entente.)

Les contraintes (`n ≤ 5·104`) forcent une solution O(n) – un boîtier classique pour une pile *monotonique*.

Ci-dessous vous trouverez une implémentation propre et prête à la production dans **Java, Python et C++**.
Après le code, un Le blog SEO-optimisé explique l'algorithme, les pièges et pourquoi il impressionnera les recruteurs.

---

Code – Trois langues

> Les trois extraits résolvent le même problème dans l'espace auxiliaire **O(n)** et **O(n)**.
> Ils suivent tous la même logique : maintenir une pile croissante d'indices ; quand un nombre plus petit apparaît, pop et calculent les contributions.

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Compte le nombre de subarrays valides.
*
* @param nums le tableau d'entrée
* @retourner le nombre de sous-tribus valides
*/
public int valideSubarrays(int[] nums) {
int n = longueur nums;
Deque<Integer> pile = nouveau ArrayDeque<>(); // stocke des indices en ordre croissant
long total = 0; // utiliser longtemps pour éviter le débordement

pour (int i = 0; i < n; i++) {
// Alors que l'élément courant est plus petit, le haut de la pile
// ne peut pas dépasser i-1.
alors que (!stack.isEmpty() && nums[i] < nums[stack.peek()]) {
int idx = pile.pop();
total += i - idx; // subarrays où nums[idx] est le plus à gauche
}
Le point i) est remplacé par le texte suivant:
}

// Les indices restants peuvent s'étendre jusqu'à la fin du tableau.
pendant que (!stack.isEmpty()) {
int idx = pile.pop();
total += n - idx;
}

retour (int) total; // résultat correspond à l'ent.
}
}
«» "

---

- Oui. 2. Python

'`python
de taper l'importation Liste

Solution de classe:
def valide Subarrays(self, nombres: Liste[int]) -> Int:
pile : Liste[int] = [] # indices d'éléments dans l'ordre croissant
total: int = 0
n: int = len(nums)

pour i, val dans l'énumération(nombres):
# pop tous les indices dont les valeurs sont supérieures à la valeur actuelle
pendant la pile et les nombres[stack[-1]] > Valeur
idx = pile.pop()
Total += i - idx # nombre de subarrays avec nums[idx] comme le plus à gauche
pile.annexe(i)

# Les indices restants atteignent la fin du tableau
pendant la pile:
idx = pile.pop()
Total += n - idx

retour total
«» "

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int valideSubarrays(vector<int>& nums) {
int n = nombres.size();
vectorielle<int> st; // pile d'indices
long total = 0; // utiliser long pour être sûr

pour (int i = 0; i < n; ++i) {
pendant que (!st.vide() && nums[st.back()] > nums[i]) {
int idx = st.back(); st.pop_back();
Total += i - idx; // contribution des nombres[idx]
}
st.push_back(i);
}

// Les indices restants peuvent s'étendre jusqu'à la fin
pendant que (!st.vide()) {
int idx = st.back(); st.pop_back();
total += n - idx;
}

retourner static_cast<int>(total);
}
};
«» "

> **Pourquoi `long`/`long`?**
> Pour `n = 5·104`, le nombre maximal de sous-barrages est `n*(n+1)/2 ↓ 1,25·109`, qui correspond à un int signé 32 bits. Cependant, les ajouts intermédiaires peuvent dépasser cette limite dans une mise en œuvre naïve. L'utilisation d'un accumulateur 64 bits garantit la sécurité.

---

Le bon, le mauvais et le mauvais de LeetCode 1063

> **Audience cible** – étudiants CS, personnes interrogées en génie logiciel et recruteurs
> **Mots clés** – *Nombre de Subarrays valides*, *LeetCode 1063*, *monotonic stack*, *entrevue d'ingénierie de logiciels*, *entrevue d'algorithme*, *algorithme d'entrevue d'emploi*, *ingénieur de logiciels*

---

Titre
Nombre de sous-barrages valides (Code de débit 1063): Le bon, le mauvais et le mauvais – Un guide monotonique pour les codeurs prêts à travailler**

---

C'est vrai. 1. Introduction – Pourquoi ce problème compte

- **LeetCode Hard** – apparaît dans de nombreux pipelines de location (Google, Amazon, Microsoft).
- **Exemple du monde réel** – trouver un lien le plus faible dans une chaîne de contraintes (p. ex., la première fois qu'un emploi peut commencer avec des échéances).
- **Signal d'entrevue** – testez votre compréhension du comptage des subarraies*, des astuces* et de l'analyse amortie*.

---

C'est vrai. 2. Récapitulation des problèmes

Compter le nombre de sous-aires contiguës non vides où l'élément **leftmest** est le plus petit de ce sous-aire.
Formellement: pour une sous-tribu `nums[l...r]`, nous avons besoin `nums[l] ≤ nums[i]` pour tous `l < i ≤ r`.

> **Insight clé** – L'élément le plus à gauche est le **minimum** du sous-appel.

---

C'est vrai. 3. La solution Bon – Élégant O(n)

- **Monotonique Augmentation de la pile* *
* Indices de valeurs croissantes. *
Lorsqu'un élément plus petit apparaît, tous les indices de la pile sont « gelés » – ils ne peuvent plus dépasser la position actuelle.

- ** Compte des contributions**
Pour un indice `idx` affiché à la position `i`, le nombre de sous-groupes valides où `nums[idx]` est l'élément le plus à gauche égal `i - idx`.
Pourquoi ? Tous les sous-réseaux `[idx, k]` avec `k` allant de `idx` à `i-1` ont `nums[idx]` comme leur minimum (car aucun élément plus petit n'a encore été vu).

- **Deuxième col**
Les indices restants après la boucle principale peuvent s'étendre jusqu'à la fin du tableau, contribuant `n - idx` sous-ensembles chacun.

**Code Pseudo (style Java)* *

"Java
pour (i = 0; i < n; i++) {
alors que (!stack.isEmpty() && nums[i] < nums[stack.peek()]) {
idx = pile.pop();
total += i - idx;
}
Le point i) est remplacé par le texte suivant:
}
pendant que (!stack.isEmpty()) {
idx = pile.pop();
total += n - idx;
}
«» "

**Complexité** – Chaque index est poussé et affiché au plus une fois → **O(n)** temps, **O(n)** espace.

> **Pourquoi c'est le "Bien"** –
> *Simplicité* : Une passe linéaire, une pile, une logique mathématique claire.
> *Robustness*: Poigne des valeurs égales, en augmentation stricte, en diminution stricte, et des données aléatoires sans cas particuliers.

---

C'est vrai. 4. Les mauvaises – Pièges communs

Pourquoi il casse
- Oui.
Autres **L'utilisation d'une pile de valeurs au lieu d'indices **Vous perdez l'information de distance (`i - idx`). Conservez des indices; recherchez des valeurs via `nums[idx]`. Autres
**Utiliser une pile décroissante** Utilisez une pile croissante (`nums[stack[top]] < nums[i]`). Autres
**Comptant après chaque pop avec `i - idx`**=Fails quand des valeurs dupliquées apparaissent; la condition `nums[i] < nums[stack[top]]` doit être *strictement* plus petite. Conserver `>` pour les duplicata ou gérer les duplicata dans la deuxième passe. Autres
**Ne pas manipuler le reste de la pile après la boucle** Dernière boucle: `total += n - idx`.
**Utiliser le trop-plein d'inte**= Pour les grands réseaux, les sommes intermédiaires dépassent 32 bits.= Utiliser `long`/`long` pour l'accumulateur. Autres

> **Pourquoi c'est "Bad"** – Ces bugs sont subtils, mais ils font une solution échoue rapidement sur les tests cachés. Ils sont également faciles à repérer si vous pensez soigneusement aux invariants.

---

C'est vrai. 5. Les solutions Ugly – Overkill et inefficaces

1. ** Force brute** – Triple boucles imbriquées → **O(n3)**, impossible pour `n = 50k`.
2. **Prefix‐Min + Binary Search** – Toujours **O(n2)** dans le pire des cas.
3. **Segment Tree / RMQ** – Sur-ingénierie : construction d'un arbre O(n) et requête O(log n) pour chaque sous-réseau → **O(n2 log n)**.
4. **Two-Pointer Sliding Window** – Fonctionne pour les contraintes *sum* ou *product* mais pas pour les contraintes basées sur le minimum ; vous auriez besoin d'une deque pour maintenir les minutes → encore **O(n2)** si pas prudent.

> Les solutions "gugly" sont souvent les premières auxquelles les candidats pensent, mais elles ne sont pas "compétitives". Un panel d'entretien s'attendra à une solution de pile O(n) propre. Démontrer la conscience de ces pièges montre de la profondeur.

---

C'est vrai. 6. À emporter dans le monde réel

- **Les piles à moteur** apparaissent dans de nombreux contextes : prochain élément plus grand, minima de fenêtre coulissante, entretien de coque convexe, etc.
- Maîtrisez le modèle → vous le reconnaîtrez instantanément lors des entretiens.
- Pensez toujours en termes de *=quand un élément cesse-t-il d'être pertinent ?===* – c'est le noyau des tours de pile d'O(n) amortis.

---

C'est vrai. 7. Exemple de dialogue d ' entretien

> **Interrogateur:** Pourquoi O(n) suffit-il? Pourriez-vous expliquer l'analyse amortie en anglais clair ? (en milliers de dollars)
> **Candidat :**
> Chaque élément peut être poussé sur la pile une fois. Après qu'il ait sauté, il n'a jamais revu. Ainsi, le nombre total d'opérations push/pop est limité par "2n", ce qui donne du temps linéaire. (en milliers de dollars)

> Cette réponse précise montre à la fois la justesse et la compréhension du rendement.

---

7.1 Liste de contrôle pour votre soumission

- [ ] Stocker **indices**, pas des valeurs.
- [ ] Utiliser ** strictement** une comparaison plus petite pour le popping.
Le comte 'i - idx' sur pop.
- [ ] Processus restant pile après boucle.
- [ ] Accumuler avec `long`/`long`.
- [ ] Écrire un code propre et bien commenté.

> Soumettez l'extrait de Java, mais apportez la version Python ou C++ le jour – de nombreux gestionnaires d'embauche lancent votre solution dans plusieurs runtimes.

---

C'est vrai. 7. Bonus – Visualisation de la dynamique des piles

«» "
Indice: 0 1 2 3 4 5
Valeur: 3 2 1 1 4 2

Évolution de la pile (en haut = gauche):

i=0: pile=[0]
i=1: pop 0 (3>2) → contrib 1, pile=[1]
i=2: pop 1 (2>1) → contrib 1, pile=[2]
i=3: pas de pop (1==1), pile=[3,2]
i=4: pas de pop (4>1), pile=[4,3]
i=5: pop 4 (4>2) → contrib 1, pop 3 (1>2? non), pop 2 (1>2? non), pile=[5,2]
Finale: pop 5→ 1, pop 2→ 4
Total = 1+1+1+4 = 8
«» "

> Voir la pile aide visuellement à solidifier le raisonnement et est idéal pour une entrevue de tableau blanc.

---

C'est vrai. 8. Fermeture – recruteurs d'impression

- **Parlez de l'amortissement O(n)** – les recruteurs aiment pourquoi c'est rapide.
- **Afficher le deuxième laissez-passer** – beaucoup de candidats l'oublient ; il montre l'attention au détail.
- **Manipulation explicite du débordement** – indique l'état d'esprit du code de production.
- **Mention le modèle** – Il s'agit d'un problème classique de pile monotonique, qui sous-tend également le prochain élément, les minima de la fenêtre coulissante, etc. (en milliers de dollars)
Ils vont voir instantanément que vous pouvez transférer cette connaissance à d'autres problèmes.

---

La pensée finale

LeetCode 1063 est plus qu'un simple problème de comptage – c'est une passerelle vers la maîtrise des techniques de pile monotonique qui dominent les entretiens techniques.
Avec le code ci-dessus et la plongée profonde dans cet article, vous êtes entièrement équipé pour convertir ... ..la mauvaise et laid... en une solution propre, **prêt à travailler** qui se démarquera aux recruteurs.

Bon codage, et bonne chance pour la prochaine interview!

---

* Se sentir libre de copier, adapter et partager. *