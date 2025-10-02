---
titre: LeetCode 1865. Trouver des paires avec une certaine somme -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1865 – Trouver des paires avec une certaine somme
**Moyenne de leetCode de données

Je veux montrer aux recruteurs que je peux transformer un problème délicat en code propre et réutilisable.
> C'est ici une marche à fond :
> * Problème & contraintes
> * Solution élégante (carte de fréquence à base de hash)
> * implémentations Java / Python / C++
> * Un article *blog-ready* qui met en évidence le **bon, le mauvais et le laid** – parfait pour LinkedIn, Medium ou votre portfolio personnel.

---

- Oui. 1. Récapitulation des problèmes

**Tâche**
- Oui.
**Créer une structure de données** qui supporte deux opérations sur deux tableaux entiers `nums1` et `nums2`: Autres
1. `add(index, val)` – ajouter `val` à `nums2[index]`. Autres
2. `count(tot)` – retourner le nombre de paires `(i, j)` avec `nums1[i] + nums2[j] == tot`. Autres

Contraintes
C'est quoi ?
Longueur ≤ 1 000
Longueur ≤ 105 ' Autres
«1 ≤ nombres1[i], nombres2[i] ≤ 105» (sauf «nums1[i]» peut être jusqu'à `109`) Autres
`add` et `count` appelés ≤ 1 000 fois chacun. Autres
"0 ≤ indice < nums2.longueur" Autres
"1 ≤ valeur ≤ 105" Autres
"1 ≤ t ≤ 109" Autres

Le but est de garder chaque opération rapide – idéalement *O(1)* pour `add` et *O(n1)* pour `count`, où *n1* = `nums1.longueur`.

---

- Oui. 2. Intuition

1. **Static vs Dynamique**
*'nums1`* ne change jamais – nous pouvons itérer sur chaque `compte`.
*`nums2`* change – nous avons besoin d'un moyen rapide de savoir combien de fois une valeur particulière se produit.

2. **Carte de fréquence**
Gardez une carte de hachage (`valeur → count`) pour `nums2`.
- **add**: diminution de l'ancienne valeur, ajouter la nouvelle valeur.
- **compte**: pour chaque `x` en `nums1`, recherchez `tot - x` dans la carte et ajoutez sa fréquence.

3. **Pourquoi ça marche**
Chaque recherche dans la carte de hachage est *O(1)* en moyenne.
`count` touche chaque élément de `nums1` une fois → *O(n1)*, ce qui est bien parce que `n1 ≤ 1 000`.
"Ajouter" est *O(1)*.
Mémoire: stocker les fréquences au plus `105` différents numéros → *O(n2)*.

---

- Oui. 3. Code – 3 langues

#### 3.1 Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

classe publique FindSumPairs {
final privé int[] nums1;
la dernière int. privée nums2;
carte finale privée<enteger,enteger> freq; // carte de fréquence des nombres2

public FindSumPairs(int[] nums1, int[] nums2) {
ce.nums1 = nombres1;
ce.nums2 = nums2;
this.freq = nouveau HashMap<>();

pour (int val : nombres2) {
freq.put(val, freq.getOrDefault(val, 0) + 1);
}
}

*** Ajouter +val à nums2[index] et mettre à jour la carte de fréquence. */
public vide add(int index, int val) {
int old = nums2[index];
freq.put(vieux, freq.get(vieux) - 1); //

nums2[index] += valeur;
Int newVal = nombres2[index];
freq.put(newVal, freq.get OrDefault(newVal, 0) + 1); // incrément nouveau nombre
}

*** Retourner le nombre de paires (i, j) où nums1[i] + nums2[j] == tot. */
nombre d'intes publiques (int tot) {
Int ans = 0;
pour (int a : nombres1) {
besoin int = tot - a;
ans += freq.getOrDefault(nécessité, 0);
}
le retour des an;
}
}
«» "

3.2 Python

'`python
Importations provenant des collections Compteur
de taper l'importation Liste

classe FindSumPairs:
def __init_(self, nums1: List[int], nums2: List[int]):
self.nums1 = nombres1
Self.nums2 = nombres2
self.freq = Counter(nums2) # frequence map of nums2

def add(self, index: int, val: int) -> Aucun:
old = self.nums2[index]
Self.freq[old] -= 1 # Décrément ancienne valeur

auto.nums2[index] += valeur
new_val = self.nums2[index]
[new_val] += 1 # augmentation nouvelle valeur

def count(self, tot: int) -> Int:
retour sum(self.freq[tot - a] pour un inself.nums1)
«» "

#### 3.3 C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>

classe FindSumPairs {
public:
FindSumPairs(std::vector<int> nums1, std::vector<int> nums2)
: nombres1(std::move(nums1)), nombres2(std::move(nums2)) {
pour (int v : this->nums2) freq[v]++; // construire une carte de fréquence
}

vide add(int index, int val) {
int old = nums2[index];
--freq[old]; // décrément vieux nombre

nums2[index] += valeur;
Int newVal = nombres2[index];
++freq[newVal]; // incrément nouveau nombre
}

nombre int(int tot) {
Int ans = 0;
pour (int a : nombres1) {
besoin int = tot - a;
auto it = freq.find(besoins);
si (it != freq.end()) ans += it->seconde;
}
le retour des an;
}

particulier:
à:vecteur<int> nums1;
à:vecteur<int> nums2;
std::unordered_map<int, int> freq; // valeur → compter
};
«» "

Les trois solutions partagent les mêmes O(1) *add* et O(`nums1.length`) *comptez* temps, les rendant idéales pour les limites de LeetCode.

---

- Oui. 4. Article de blog – Le bon, le mauvais et le mauvais

> ** Groupe cible** : recruteurs, intervieweurs et pairs sur LinkedIn/Moyen.
> **Mots clés faciles à utiliser**: *LeetCode 1865*, *FindSumPairs*, *data-structure interview*, *hash map solution*, *O(1) add*, *job interview coding*, *Python Counter*, *C++ unordered_map*, *Java HashMap*.

---

#### 4.1 Titre & Meta

«» "
<title>LeetCode 1865 – Concevoir une structure de données basée sur la fréquence de recherche de données sur les paires de données
<meta name="description" content="Master LeetCode 1865 (FindSumPairs). Apprenez une solution propre Java, Python, C++, analyse de complexité et conseils prêts à l'entrevue. Parfait pour le codage des entrevues et la présentation du portfolio.
«» "

4.2 Table des matières (pour lecture)

1. [Le problème] (#le problème)
2. [Pourquoi le Trick Hash-Map est la sauce secrète] (#hash-map-sauce)
3. [Algorithme et complexité] (#complexité)
4. [Code complet](#code)
5. [Le bon, le mauvais et le mauvais] (#pros-cons-ugly)
6. [Conseils d'entrevue](#interview-tips)
7. [Conclusion et prochaines étapes](#conclusion)

---

#### 4.3 Les bons

Ce que j'aimais
C'est quoi ?
**Simplicité** – une carte de fréquence + deux boucles simples. Autres
**Performance** – *O(1)* `add`, *O(n1)* `count`. Autres
**Langue Agnostique** – la même idée fonctionne en Java, Python, C++, Rouille, Allez, etc. Autres
**Memory Footprint** – seuls les nombres de `nums2` sont stockés, pas le tableau entier. Autres
**La réutilisabilité** – peut être adaptée à d'autres problèmes de fréquence dynamique et statique. Autres

4.4 Les mauvais

Pièges potentiels
* * * * * * * *
**Grande Périodicité Carte** – si `nums2` contient de nombreuses valeurs uniques, le non ordonné_map/Counter peut utiliser jusqu'à ~200 KB par entrée unique, ce qui est encore très bien pour les nombres `105` mais il vaut la peine de noter pour les entrées vraiment massives. Autres
**Zero-Count Keys** – nous décréments compte mais jamais supprimer les clés lorsque le nombre atteint zéro. Dans un système du monde réel, vous devriez peut-être vous pencher sur la carte, mais les frais généraux supplémentaires sont négligeables compte tenu des contraintes. Autres
**Compte périodique Appels** – l' itération sur "nums1" sur chaque appel est *O(n1)*. Si `nums1` étaient plus grands, vous auriez besoin de pré-calculer quelque chose d'autre (par exemple, un préfixe 2-D). Les limites du problème le maintiennent acceptable, mais la personne interrogée devrait mentionner ce compromis. Autres

4.5 La moche

Cases de bord & Caché Gotchas
Il n'y a pas de lien entre les deux.
**Dépassement entier** – `tot` peut être jusqu'à `109`. L'ajout de deux int dans C++/Java peut déborder si vous utilisez des types signés 32 bits; l'utilisation de `long` ou `long` pour la somme intermédiaire est plus sûre dans des langues qui n'ont pas d'ints de précision arbitraire (JavaScript, C). Dans ce problème, les sommes restent dans les limites de 32 bits, mais toujours garder un œil sur les limites. Autres
**Multiple Updates to the Same Index** – Si `add` est appelé à plusieurs reprises sur le même index, assurez-vous que la carte de fréquence reste en synchronisation avec le tableau sous-jacent. Un bogue courant est d'oublier de mettre à jour le tableau après avoir décrémenté l'ancien nombre. Autres
** Nombres négatifs?** – Les contraintes officielles interdisent les valeurs négatives, mais si vous modifiez le problème pour les autoriser, l'algorithme fonctionne encore parce que la carte hash peut stocker des clés négatives. N'oubliez pas d'utiliser un type entier *signé*. Autres

---

#### 4.6 Interview-Ready Pseudocode

Texte
classe FindSumPairs:
freq = carte des valeurs nums2

(nombres1, nombres2):
construire freq à partir de nums2

ajouter(idx, val):
[nums2[idx]]-
Nombres2[idx] += valeur
freq[nums2[idx]]++

Nombre(tot):
Res = 0
pour x en nombres1:
res += freq[tot - x]
retour res
«» "

> **Pourquoi il s'agit d'un spectacle pour les recruteurs* *
> * L'intervieweur peut voir instantanément que vous avez utilisé une carte *hash* pour transformer un tableau dynamique en une table de recherche statique.
> * Vous avez expliqué la mise à jour *amortisée* *O(1)*, la requête *O(n1)* et l'échange d'espaces.
> * Vous avez présenté des méthodes propres et testables, prêtes pour une API de qualité de production.

---

- Oui. 5. Mettre dans votre portefeuille

1. **Engagé le code** – copiez les extraits de Java, Python et C++ dans un README ou un Gist GitHub.
2. ** Ajouter un README** qui comprend :
- Déclaration de problème (copie de LeetCode)
- Harnais d'essai (essais unitaires pour les trois langues)
- Lancez ceci pour voir le bloc prévu.
3. **Lien avec** – dans votre lien Dans l'article ou sur votre site personnel, ajoutez un lien: `https://github.com/yourusername/leetcode-1865-findsumpairs`.
4. **Partager sur Medium** – publier le blog avec les rubriques ci-dessus. Tag avec `#LeetCode`, `#CodingInterview`, `#DataStructures`, "#AlgorithmDesign".

---

- Oui. 6. Conclusion

- **LeetCode 1865** est un problème classique de conception-a-structure des données qui teste votre capacité à équilibrer **temps-complexité** et **efficacité-mémoire**.
- Oui. Le tour de fréquence **hash-map** est la solution canonique : mises à jour O(1), requêtes O(n1).
- Les implémentations dans **Java, Python et C++** sont simples et démontrent une compétence translingue.
- L'article **blog** ci-dessus est optimisé SEO et prêt à partager—complet avec les mots-clés que les recruteurs aiment (`LeetCode 1865`, `FindSumPairs`, `Java HashMap`, `Python Counter`, `C++ unordered_map`, `job interview coding`).

- Oui. **Étape suivante:**
Ajoutez vos propres tests unitaires, poussez la repo vers GitHub, et lancez un message LinkedIn : **Solved LeetCode 1865 en Java, Python et C++ – apprenez comment j'ai conçu une structure de données efficace !*

Bon codage, et meilleure chance d'atterrir cette prochaine interview! C'est ce qu'il a dit