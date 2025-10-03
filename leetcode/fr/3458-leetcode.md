---
titre: LeetCode 3458. Sélectionner K Disjoint Sous-chaînes spéciales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour qu'une sous-chaîne soit *valable* tout caractère qui se produit à l'intérieur de la sous-chaîne doit avoir **all** de sa
occurrences dans la même sous-chaîne.
Autrement dit :

«» "
pour chaque caractère x dans la sous-chaîne
premier[x] >= _démarrage de la sous-chaîne
last[x] <= fin_of_substring
«» "

Toute la chaîne elle-même n'est jamais comptée comme une sous-chaîne valide.



-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

* Le début d'une sous-chaîne valide ne peut être que la première occurrence** d'un personnage.
(Si le début était quelque part ailleurs, le même caractère apparaîtrait dans le
La sous-chaîne et son premier événement se trouveraient à l'extérieur – en violation de la règle.)

* La fin d'une sous-chaîne valide est la **dernière occurrence** d'un caractère qui
C'est à l'intérieur.
Lorsque nous essayons de construire une sous-chaîne à partir d'une position de départ "i", nous
premier regard sur la dernière occurrence de `s[i]`.
Tout en élargissant la fin actuelle à la droite, nous pourrions devoir inclure
caractères supplémentaires dont la dernière occurrence est au-delà de la fin actuelle.
Si un personnage à l'intérieur de l'intervalle a une première occurrence *avant* `i`,
alors tout cet intervalle est impossible – nous le sautons simplement.

* Après avoir connu tous les intervalles valides `[l , r]`, le problème se transforme en
sélectionner le nombre maximal d'intervalles de non-overlaping.
C'est un problème classique d'avidité: trier tous les intervalles par `r`
(finition la plus avancée en premier) et choisir à plusieurs reprises l'intervalle suivant qui commence
après la fin du dernier choisi.



-----------------------------------------------------------------------------------

C'est vrai. 2. Algorithme
«» "
Si k == 0 → vrai

1. Scanner la chaîne une fois et stocker
premier[26] – premier index de chaque caractère
dernier[26] – dernier index de chaque caractère

2. Pour chaque position i qui est la première apparition de son caractère
(i == premier[s[i]]) :

fin = dernière[s[i]] // fin du candidat
// Élargir la fin pour couvrir chaque personnage à l'intérieur
pour pos = i ... fin:
fin = max(end , last[s[pos]])

// Vérifier la validité – aucun caractère à l'intérieur ne peut commencer à l'extérieur [i , fin]
ok = vrai
pour pos = i ... fin:
si premier[s[pos]] < i : ok = faux; casser
si !ok → continuer
si i==0 et fin==n-1 → continuer // chaîne entière n'est pas autorisée

intervalle de conservation [i , fin]

3. Triez tous les intervalles stockés par leur bon point d'arrivée.

4. Sélection des intervalles de non-overlaping
dernier Fin = -1
choisi = 0
pour chaque intervalle [l, r] dans l'ordre trié
si l > dernier Fin
choisi++, dernier Fin = r
retour (choisi >= k)
«» "

-----------------------------------------------------------------------------------

C'est vrai. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie `true`
iff la chaîne contient au moins `k` des sous-chaînes valides qui ne recouvrent pas.

---

Lemma 1
Pour chaque caractère `c` toutes ses occurrences se trouvent dans un des intervalles
construit par l'algorithme.

**Prof.**

Au cours de l'étape 1, nous calculons `premier[c]` et `dernier[c]`.
Lorsque nous rencontrons une position "i" qui équivaut à "first[c]",
l'algorithme étend la fin du candidat jusqu'à ce qu'il contienne chaque
caractère dont la dernière occurrence est à l'intérieur de l'intervalle courant.
Ainsi, l'intervalle final `[i , fin]` contient toutes les occurrences de chaque
caractère apparaissant à l'intérieur.
En particulier, il contient toutes les occurrences de "c".
Par conséquent, toute la gamme `[first[c] , last[c]]] "
est entièrement couvert par un intervalle construit (éventuellement avec d'autres
caractères). *



Lemma 2
Chaque intervalle produit par l'algorithme est une sous-chaîne valide
selon la définition du problème.

**Prof.**

Prendre tout intervalle produit `[i , fin]`.
Pendant sa construction, nous avons effectué deux vérifications :

1. *Expansion* – après la première boucle nous avons élargi `end` jusqu'à chaque
caractère à l'intérieur `[i , fin]` a son dernier événement ≤ "fin".
Ainsi pour chaque caractère `x` dans l'intervalle
«premier[x] ≥ i» et «dernier[x] ≤ fin».

2. *Validité* – dans la seconde boucle nous avons vérifié qu'aucun caractère
à l'intérieur a un premier événement `< i`.
Combiné avec la propriété précédente, pour chaque caractère `x`
dans la sous-chaîne
`premier[x]` et `dernier[x]` couché à l'intérieur `[i, fin]`.

La sous-chaîne répond donc à la définition d'une sous-chaîne valide.
*



Lemma 3
La procédure gourmande à l'étape 4 sélectionne le nombre maximum possible de
les intervalles de non-overlaping entre tous les intervalles construits.

**Prof.**

Les intervalles sont triés par temps de finition.
La preuve standard de l'algorithme cupide de programmation des intervalles
montre que pour un ensemble d'intervalles triés par temps de finition,
choisir l'intervalle de finition le plus précoce qui ne se chevauche pas avec la
précédemment choisi donne une solution optimale.
L'algorithme de l'étape 4 est exactement cet algorithme gourmand. *



Lemma 4
Si l'algorithme retourne `true`, la chaîne contient au moins `k`
les sous-chaînes valides ne chevauchent pas.

**Prof.**

`true` n'est retourné que lorsque la sélection avide à l'étape 4 a choisi au moins
Intervalles "k".
Par Lemma 2 chaque intervalle choisi est une sous-chaîne valide, et par
Lemma 3 ces intervalles ne se chevauchent pas.
Par conséquent, au moins `k` valide, il existe des sous-chaînes de non-overlaping.



Lemma 5
Si la chaîne contient au moins `k` des sous-chaînes valides,
l'algorithme renvoie `true`.

**Prof.**

Que les sous-chaînes `k` soient `T1 , T2 , ... , T_k`
et les commander par leurs positions de départ.
Par Lemma 1 chaque occurrence de chaque caractère se trouve dans l'un des
intervalles produits par l'algorithme, donc chaque `T_i` apparaît
dans la liste des intervalles.
Par Lemma 2 chaque intervalle indiqué est une sous-chaîne valide.
Puisque le `T_i` ne recouvre pas,
l'ensemble des intervalles qui les contiennent est un calendrier réalisable.
Par Lemma 3 l'algorithme gourmand sélectionnera ** au moins** autant
des intervalles comme tout calendrier possible, par conséquent, il choisira au moins `k "
intervalles et l'algorithme retourne `true`.



C'est vrai. Théorème
L'algorithme renvoie `true`
iff la chaîne d'entrée contient au moins `k` non-overlaping valide
sous-chaînes.

**Prof.**

*Si partie*:
"true" par Lemma 4 la sélection avide a choisi au moins "k"
les intervalles de non-overlaping, chacun d'eux est une sous-chaîne valide
(Lemme 2).
Ainsi la chaîne contient au moins `k` ces sous-chaînes.

*Seulement en partie*:
Supposons que la chaîne contient au moins `k` des sous-chaînes valides qui ne recouvrent pas.
Tous sont parmi les intervalles construits
(Lemme 1 et Lemma 2).
L'algorithme avide (Lemma 3) trouve le nombre maximum de
les intervalles de non-overlaping entre eux,
qui est donc ≥ "k".
Par conséquent, l'algorithme retourne `true`.



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

«» "
Étape 1 : O(n)
Étape 2 : chaque position est visitée au plus une fois lors de l'élargissement de la fin
→ O(n) (total pour tous les départs)
Étape 3 : tri O(m log m) (m – nombre d'intervalles, m ≤ n)
Étape 4 : O(m)
«» "

`m` ne dépasse jamais `n`, donc le temps de fonctionnement global est **O(n)* *
et la consommation de mémoire est **O(n)**.



-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Retourne true si au moins k des sous-chaînes valides ne dépassent pas
bool maxSubstringLength(string s, int k) {
si (k <= 0) retourner true; // cas bord

n = (int)s.size();
vecteur<int> premier(26, n), dernier(26, -1);

- Oui. 1. première / dernière position --------- */
pour (int i = 0; i < n; ++i) {
c = s[i] - 'a';
si (premier[c] == n) premier[c] = i;
Last[c] = i;
}

- Oui. 2. construire tous les intervalles valides --------- */
les intervalles du vecteur<pair<int,int>>; // [l , r]
pour (int i = 0; i < n; ++i) {
i) Int ch = s[i] - 'a';
si (premier [ch] != i) continuer; // commencer seulement au premier occ.

int fin = last[ch]; // fin candidate
pour (int pos = i; pos <= fin; ++pos)
fin = max(end, last[s[pos] - 'a']); // étendre pour couvrir tous

// vérifier la validité – aucun char à l'intérieur ne commence avant i
bool ok = true;
pour (int pos = i; pos <= fin; ++pos) {
c = s[pos] - 'a';
si (premier[c] < i) { ok = faux; casse; }
}
Si (!ok) continue;
si (i == 0 && fin == n - 1) continuer; // chaîne entière n'est pas autorisée

intervals.emplace_back(i, fin);
}

- Oui. 3. trier en finissant le temps
tri(intervalles.debut(), intervals.end(),
[](const auto& a, const auto& b){ retourner a.seconde < b.seconde; });

- Oui. 4. horaire des intervalles gourmands --------- */
int choisi = 0;
int dernier Fin = -1;
pour (auto &iv : intervalles) {
si (iv.first > lastFin) {
++choisi;
dernier Fin = iv.seconde;
si (choisi >= k) retourne true; // sortie anticipée
}
}
retourner faux;
}
};
«» "

Le code suit exactement l'algorithme prouvé correct ci-dessus et
conforme à la norme C++17.