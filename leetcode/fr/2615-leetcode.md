---
titre: LeetCode 2615. Somme des distances -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Ci-dessous sont trois solutions complètes, prêtes à coller – **Java**, **Python** et **C++** – qui calculent le tableau décrit dans LeetCode 2615.

Tous les trois partagent la même approche spatiale **O(n)** time / **O(n)**:
* Gardez deux tables de hachage pendant la numérisation du tableau de gauche à droite –
`sumIdx` stocke la somme des indices vus jusqu'à présent pour chaque valeur,
`count` stocke combien de fois la valeur est apparue.
La contribution du côté gauche est `idx * count - sumIdx`.
* Puis scanner de droite à gauche en faisant de même avec les rôles inversés.
* Enfin, les deux montants partiels donnent la réponse pour chaque poste.

---

### Java (JDK 17)

"Java
Importer java.util. HashMap;

solution de classe publique {
***
* Renvoie un tableau où arr[i] est la somme des distances de
* index i à chaque autre index j qui contient la même valeur.
*/
public longue[] distance(int[] nombres) {
int n = longueur nums;
long[] ans = nouveau long[n];

// Passage de gauche à droite
HashMap<entier, long> sumIdx = nouveau HashMap<>();
HashMap<entier, entier> nombre = nouveau HashMap<>();
pour (int i = 0; i < n; i++) {
Int val = nombres[i];
long s = sumIdx.getOrDefault(val, 0L);
int c = count.get OrDéfaut(val, 0);
(long) i * c - s; // contribution du côté gauche
sumIdx.put(val, s + i);
count.put(val, c + 1);
}

// Passage de droite à gauche
les points suivants sont ajoutés:
count.clear();
pour (int i = n - 1; i >= 0; i--) {
Int val = nombres[i];
long s = sumIdx.getOrDefault(val, 0L);
int c = count.get OrDéfaut(val, 0);
ans[i] += s - (long) i * c; // contribution du côté droit
sumIdx.put(val, s + i);
count.put(val, c + 1);
}

le retour des an;
}

// Démo
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
nombres int[] = {1,3,1,1,2};
longue[] res = sol.distance(nums);
Système.out.println(java.util.Arrays.toString(res)); // [5, 0, 3, 4, 0]
}
}
«» "

---

### Python (3.11+)

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def distance(self, nombres: List[int]) -> Liste[int]:
n = len(nums)
ans = [0] * n

De gauche à droite
sum_idx = defaultdict(int)
count = defaultdict(int)
pour i, val dans l'énumération(nombres):
ans[i] += i * nombre[val] - sum_idx[val]
sum_idx[val] += Les
nombre[val] += 1

De droite à gauche
sum_idx.clear()
nombre.clair()
pour i dans la fourchette(n - 1, -1, -1):
val = nombres[i]
ANS[i] += sum_idx[val] - i * count[val]
sum_idx[val] += Les
nombre[val] += 1

retour et

♪ Démo
si __nom__ == "__main__" :
sol = Solution()
print(sol.distance([1, 3, 1, 1, 2,])) # [5, 0, 3, 4, 0]
«» "

---

### C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle <long> distance(vecteur<int>&nums) {
int n = nombres.size();
vecteur <long> ans(n, 0);

non ordonné_map<int, long> sumIdx; // somme des indices
non ordonné_map<int, int> cnt; // nombre d'événements

// Gauche → Droite
pour (int i = 0; i < n; ++i) {
int v = nombres[i];
ii) Le nombre d'unités de compte est égal à celui des unités de compte;
Le tableau ci-dessous indique le nombre d'heures de travail. i);
++cnt[v];
}

// Effacer les cartes pour le bon passage
les points suivants sont ajoutés:
cnt.clair();

// Droite → Gauche
pour (int i = n - 1; i >= 0; --i) {
int v = nombres[i];
as[i] += sumIdx[v] - 1LL * i * cnt[v];
Le tableau ci-dessous indique le nombre d'heures de travail. i);
++cnt[v];
}

le retour des an;
}
};

Int main() {
Solution s;
vecteur<int> nums{1,3,1,1,2};
auto res = s.distance(nums);
pour (auto x : res) cout << x << ' ';
Cout << '\n'; // 5 0 3 4 0
}
«» "

Les trois codes fonctionnent dans **O(n)** temps et utilisation **O(n)** espace auxiliaire – parfait pour les contraintes (`n ≤ 10^5').

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 2615

Titre
**Sum of Distances (LeetCode 2615) – Le Bon, le Mauvais et l'Ugly (Java, Python, C++)* *

> *Mots-clés de recherche*: LeetCode 2615 solution, LetPython solution de dictionnaire de distance, LetPython solution

---

Introduction

Dans une entrevue de codage, on vous demande souvent de calculer une métrique basée sur la distance sur un tableau.
LeetCode 2615 – **Sum of Distances** – est un exemple classique qui teste deux compétences de base:

1. **Utilisation efficace de la structure des données** (cartes deash, préfixe des sommes).
2. ** Logique de balayage à deux passages** – un modèle qui apparaît dans de nombreuses questions d'entrevue.

Ci-dessous, nous marchons à travers le problème, une solution O(n) propre, des pièges communs, et les cas de bord d'Eugly, qui peuvent voyager même les ingénieurs chevronnés.

---

### Énoncé du problème (simplifié)

> On vous donne un nombre entier.
> Pour chaque indice `i`, calculez la somme de `=i - j=` sur tous les autres indices `j` où `nums[j] == nums[i]`.
> S ' il n ' existe pas de " j " de ce type, la réponse est " 0 " .

---

### Le bon – Pourquoi la solution O(n) est élégante

Autres Pourquoi il est grand Ce qu'il enseigne
(En milliers de dollars des États-Unis)
**Heure linéaire** – seulement deux scans, chacun `O(n)` La plupart des personnes interrogées reviennent à la force brute quadratique `O(n2)`. Autres
Autres **Aucune lourde structure de données** – seulement quelques cartes de hachage. Autres
** Logique claire en deux phases** – côté gauche + côté droit. Autres
**Travaille pour 105 éléments** Obtenir des contraintes de production; aucune constante cachée. Autres

#### Aperçu du Pseudocode

«» "
ans = tableau(n)
sumIdx, cnt = cartes vides

// De gauche à droite
pour i = 0 .. n-1:
[i] += i * cnt[nums[i]] - sumIdx[nums[i]]
[nums[i]] += Les
cnt[nums[i]] += 1

des cartes claires

// De droite à gauche
pour i = n-1 .. 0:
[i] += sumIdx[nums[i]] - i * cnt[nums[i]]
[nums[i]] += Les
cnt[nums[i]] += 1
«» "

Chaque étape suit :
* `cnt[valeur]` – combien de fois une valeur est apparue jusqu'à présent.
* `sumIdx[value]` – la somme de tous les indices où cette valeur est apparue.

La passe gauche contribue aux distances des indices à gauche; la passe droite complète le calcul symétrique.

---

- Oui. Les mauvaises – pièges communs

1. **En utilisant des entiers 32 bits pour la réponse* *
*Le nombre de distances* peut atteindre `n * n` (=1010).
**Fix:** Utiliser `long` (Java, C++) ou `int64`/`long` (Python®s int est une précision arbitraire, mais être explicite).

2. **Obligation d'effacer les cartes de hachage** entre les passages
*Résultat:* La passe droite utilise les données de la passe gauche, conduisant à de mauvaises réponses.

3. ** Négligence de l ' état < < j i > > *
Dans certaines solutions naïves, les gens doublent le même indice; la formule ci-dessus exclut naturellement `i` parce que `cnt` et `sumIdx` ne contiennent que les indices *précédents* dans la passe de gauche, et *futur* dans la passe de droite.

4. **Utiliser la récursion ou DFS** – une surcompétence ; le problème est purement linéaire et itératif.

---

### Les mauvais – les cas de bord et les conseils de débogage

Qu'est-ce qu'il faut faire attention
C'est ce que j'ai dit.
**Tous les éléments sont égaux** (`[1,1,...]`) La réponse pour chaque poste est "i*(i-1)/2 + (n-1-i)*(n-i)/2". Votre algorithme le gère automatiquement. Autres
**Tableau de longueur Retour `[0]`. Les deux passes fonctionnent toujours parce que les boucles sautent simplement les mises à jour. Autres
Autres **Très grands nombres (`109`)** . Ce ne sont que des clés dans la carte de hachage, donc l'utilisation de la mémoire reste `O(n)`. Autres
**Indices negatifs?**= Non permis par les contraintes, mais si le problème change, la logique de valeur absolue resterait. Autres
**Données entières en langues 32 bits** Autres

** Liste de contrôle du débogage**

1. Exécutez un petit essai (`[1,3,1,2]`) et comparez manuellement.
2. Imprimer l'intermédiaire `sumIdx` et `cnt` pour quelques indices.
3. Vérifiez que la passe de gauche entraîne des contributions *négatives* avant la passe de droite.
4. Recoupez les sorties Python et Java – elles doivent correspondre exactement.

---

Variations et suivi Hauts

1. **Sum de différences absolues entre *toutes* paires** (LeetCode 2121) – c'est le même problème.
2. **Arithmétique modulaire** – si vous demandez de retourner la réponse modulo `109+7`, appliquez simplement `%` après chaque ajout.
3. **Range requests** – pourrait être étendu aux requêtes dynamiques où vous changez un élément et recalculez. Cela nécessiterait un arbre de segment ou un arbre indexé binaire.

---

### Entretien à emporter

Compétence Comment ça s'est montré
-- -- -- -- -- -- -- -- -- -- -- --
Analyse de la complexité du temps
Autres ** Optimisation de l ' espace** Cartes de hachage
**Deux-passe préfixe/suffixe logique**
**Attention aux limites entières**

> **Astuce:** Lorsque vous expliquez, mentionnez que la contribution *left* est `i * cnt - sumIdx` parce que vous êtes en train de résumer `i - j` sur tous les `j` précédents. La contribution *right* est symétrique. Ce modèle mental clair impressionne souvent les intervieweurs.

---

Les pensées finales

LeetCode 2615 est trompeurment simple mais une question *rich* d'entrevue qui touche aux concepts CS de base.
La solution O(n) ci-dessus fonctionne à travers Java, Python et C++.
Maîtrisez ce modèle, et vous serez prêt pour de nombreux problèmes de réseau orientés vers la distance dans les interviews du monde réel et sur des plateformes comme LeetCode.

Bon codage, et bonne chance pour ce prochain travail !

---

- Oui. À propos de l'auteur

> *Votre nom*, un ingénieur logiciel avec 5 ans et plus de développement en backend, a distillé des dizaines de problèmes de LeetCode en solutions propres et inter-langues.
> Suivez-moi sur LinkedIn et GitHub pour plus de préparation d'entrevues, de pannes d'algorithmes et de contenu de croissance de carrière.

---

### Appel à l'action

> Si vous avez trouvé cet article utile, **partager** sur LinkedIn ou Twitter avec le hashtag #CodingInterview.
> Vous avez une solution différente ou une variation unique ? Laissez un commentaire ci-dessous – laissez passer la conversation!

---

> **Disclaimer**: Les extraits de code sont fournis à des fins éducatives. Pour l'utilisation de la production, n'oubliez pas de gérer les entrées nulles, les indices invalides et d'autres contrôles défensifs.

---

**Fin de l'article du blog**

---

> *Note intermédiaire*: L'article comprend des sections structurées, un résumé clair du problème, un algorithme O(n) élégant, des pièges, des stratégies de débogage et des idées axées sur l'entrevue. En étiquetant l'article avec des termes de recherche à volume élevé (=LeetCode 2615 solution Java=), il se classera dans les résultats de recherche Google pour les demandeurs d'emploi se préparant à des entrevues par algorithme.