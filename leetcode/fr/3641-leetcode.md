---
titre: LeetCode 3641. Subarray semi-répétant le plus long -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3641 – Subarray semi-répétant le plus long
### Un bon-mauvais-mauvais-mauvais'Dive profonde + Guide d'entrevue optimisé SEO

> **Mots clés** – *Subarray semi-répétante la plus longue, LeetCode 3641, solution Java, solution Python, solution C++, fenêtre coulissante, deux pointeurs, interview par algorithme, entretien d'emploi, préparation d'entrevue, entretien de codage, structures de données, tableau, hashmap, complexité espace-temps. *

---

- Oui. 1. Exposé des problèmes

> **Input**
> * `nums` – un ensemble entier de longueur `n` (`1 ≤ n ≤ 105`, `1 ≤ nombres[i] ≤ 105`)
> * `k` – un entier non négatif (`0 ≤ k ≤ n`)

> **Définition** – Un subarray semi-répétant* est un subarray contigu dans lequel **au plus `k` éléments distincts apparaissent plus d'une fois** (c'est-à-dire répéter au moins deux fois).

> **Tâche** – Retourner la longueur de la plus longue sous-tribu semi-répétante.

---

- Oui. 2. Intuition et idée fondamentale

Le problème est une question classique *glissante* / *deux-pointeurs* :

1. ** Invariants du vent**
* Étendre le bon pointeur `r` en comptant les événements.
* Suivre combien d'éléments ont atteint un **seconde occurrence** – c'est le nombre d'éléments à répétition.

2. **Lorsque l'invariant se casse* *
* Si le nombre d'éléments répétitifs dépasse `k`, glissez le pointeur de gauche `l` vers la droite, dépréciation des nombres et éventuellement diminution du nombre répétitif.

3. **Enregistrez la longueur maximale de la fenêtre* *
* À chaque étape, `maxLen = max(maxLen, r - l + 1)`.

Parce que chaque élément entre et quitte la fenêtre exactement une fois, l'algorithme est **O(n)** time et **O(n)** espace auxiliaire (hash map / array for counts).

---

- Oui. 3. Coin Cases & Le Ugly

Autres Décision Pourquoi ça compte ?
Il y a un problème.
Quand la seconde occurrence de n'importe quelle valeur est vue, rétrécissez immédiatement la fenêtre. Autres
Autres Tous les éléments sont égaux.Le tableau entier est valide si `k ≥ 1` 1. Autres
`k` grand (`≥` nombre de valeurs distinctes)= Le tableau entier est toujours valide= La fenêtre ne rétrécit jamais; retourne simplement `n`. Autres
"nums" contient de grandes valeurs (jusqu'à 105) Un tableau simple de la taille `max(nums)+1` (= 105+1) est sûr et plus rapide en Java/Python; C++ peut utiliser `unordered_map`. Autres
Des nombres négatifs (pas dans les contraintes) Autres

---

- Oui. 4. Solution de référence (Java)

"Java
solution de classe {
le plus long des interets publicsSubarray(int[] nums, int k) {
int n = longueur nums;
Int maxLen = 0;
int[] cnt = nouvelle int[100_010]; // nombres, valeurs basées sur 1
nombre d'éléments qui apparaissent deux fois

pour (int l = 0, r = 0; r < n; ++r) {
valeur int = nombres[r];
cnt[val]++;
si (cnt[val]] 2) répétitions++; // nouvel élément répétitif

pendant que (répète > k) { //
Int gauche Val = nombres[l];
si (cnt[leftVal]) 2) répète--; // perdre une répétition
cnt[leftVal]--;
l++;
}

maxLen = Math.max(maxLen, r - l + 1);
}
retour maxLen;
}
}
«» "

> **Complexité** – Temps `O(n)`, Espace `O(max(nums))` (= 105).

> **Pourquoi c'est bon** – Opérations à temps constant, pass simple, frais généraux minimes.
> **Piège potentiel** – La taille du tableau codé en dur doit correspondre aux contraintes du problème ; sinon, utilisez un `HashMap`.

---

- Oui. 5. Mise en œuvre de Python

'`python
def leastSubarray(nums: list[int], k: int) -> Int:
de collections importer par défautdict
cnt = par défautdict(int)
répétitions = 0 nombre nombre de valeurs qui apparaissent >= 2
l = 0
meilleur = 0

pour r, valeur dans l'énumération(nombres):
cnt[val] += 1
si cnt[val] == 2 :
répète += 1

pendant la répétition > k:
gauche = nombres[l]
si cnt[gauche]] 2 :
répéter -= 1
cnt[gauche] -= 1
l += 1

best = max (best, r - l + 1)
le meilleur retour
«» "

> **Complexité** – Temps `O(n)`, Espace `O(min(n, distinct)`.

> **Pourquoi c'est bon** – Pytonic `defaultdict`, des noms de variables clairs, et fonctionne avec de grandes entrées.
> **Piège potentiel** – "defaultdict" en tête; si la vitesse est critique, considérez `Counter` ou un dict simple avec `get`.

---

- Oui. 6. Mise en œuvre C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int le plus long Subarray(vecteur <int>& nums, int k) {
unordered_map<int,int> cnt;
les répétitions int = 0, le meilleur = 0;
Int l = 0;
pour (int r = 0; r < (int)nums.size(); ++r) {
valeur int = nombres[r];
si (++cnt[val]] 2) répétitions++; // nouvelle répétition

pendant la période (répètes > k) {
int gauche = nombres[l];
si (cnt[gauche]] 2) répète--; // perdre une répétition
si (--cnt[gauche]] 0) cnt.erase (à gauche);
++l;
}
best = max (best, r - l + 1);
}
le meilleur retour;
}
«» "

> **Complexité** – Temps `O(n)` en moyenne, Espace `O(min(n, distinct)`.

> **Pourquoi c'est bon** – `unordered_map` gère les valeurs arbitraires, la mémoire minimale au-dessus.
> **Piège potentiel** – Dans le pire des cas «O(n^2)» si les collisions de hachage sont terribles; peut atténuer en réservant le nombre de seau ou en utilisant un hachage personnalisé.

---

- Oui. 7. Essais & Edge‐ Validation des cas

'`python
# Vérification rapide de la santé mentale
affirmer le plus longSubarray([1,2,3,1,2,3,4], 2) 6
affirmer la plus longue Subarray([1,1,1,1], 4) 5
affirmer la plus longue Subarray([1,1,1,1], 0) 1
affirmer la plus longue Subarray([1,2,3,4,5], 0) == 5
affirmer la plus longue Subarray([1,1,2,2,3,3,4], 1) == 5 # [2,2,3,4]
«» "

Exécutez ça sur les trois implémentations. Considérer de grands tests aléatoires (`n = 105`) pour assurer un comportement linéaire.

---

- Oui. 8. SEO-optimized Blog Wrap‐ En haut

Titre
**LeetCode 3641: Subarray semi-répétant le plus long – Java, Python & C++ Solutions + Conseils d'entrevue

Description de la méta
Apprenez à résoudre le LeetCode 3641 (le plus long des Subarray semi-répétant) avec des algorithmes de fenêtre coulissante optimaux. Obtenez le code Java, Python et C++, l'analyse des cas de bord et des informations prêtes à l'entrevue.

Sous-chefs

- **Récapitulation des problèmes et contraintes** – Rafraîchissement rapide.
- **Stratégie de la fenêtre coulissante** – Le modèle algorithmique de "good".
- **Java / Python / C++ Échantillons de code** – Copier-coller prêt.
- **Cas d'Edge & Conseils de débogage** – Les écueils de Ugly pour éviter.
- **Analyse du temps et de l'espace** – Pourquoi cette solution bat la force brute O(n2).
- **Interview Prep** – Comment en discuter lors des entrevues de codage.

#### Mots clés Placement
- *Sous-séparation la plus longue* (en tête, introduction, conclusion)
- *LeetCode 3641* (numéro du problème)
- * Solution Java*, * Solution Python*, * Solution C++* (sections de code)
- *Fenêtre coulissante*, *deux pointeurs*, *hashmap* (algorithme)
- *Question d'entrevue*, *entrevue de codage*, *entrevue d'emploi* (contexte de carrière)

#### Appel à l'action
> Vous voulez plus de LeetCode ? Abonnez-vous aux publications hebdomadaires et interviews réussies.

---

- Oui. 9. Pensées finales – bonnes, mauvaises, Méchant

Aspect du bien
- C'est quoi ?
**Algorithme**= O(n) fenêtre coulissante – optimale== Aucune si implémentée correctement===
**Code Simplicité**= Pointeurs rectilignes, pass simple=Il faut gérer soigneusement les nombres et les répétitions==Les répétitions décomptables conduisent à une mauvaise réponse==
**Performance**
**Readability** L'index d'array et le choix de la carte peuvent confondre.
**Scalabilité**= Fonctionne avec de grands nombres== Grand `max(nums)` peut pousser la mémoire=== Dans les langues sans carte de hachage intégrée, le hachage personnalisé requis===

---

C'est vrai. Prêt pour l'entretien ?
Déposez le code dans votre IDE, testez avec des cases de bord, et soyez prêt à expliquer la logique de la fenêtre coulissante à la volée. Avec la bonne narration et la confiance, vous présenterez à la fois la compétence technique et la clarté de résolution de problèmes, exactement ce que les recruteurs recherchent. C'est ce qu'il a dit.

---