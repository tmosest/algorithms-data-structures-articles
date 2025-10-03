---
Titre: LeetCode 1775. Assortiment de somme égal avec le nombre minimum d'opérations -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Arrayages égaux avec nombre minimal d'opérations
**Une solution d'entrevue complète (Java / Python / C++) + un billet de blog -Good-Bad-Ugly)* *

> ** Tags de référence** – Leetcode, Equal Sum Arrays, Java, Python, C++, algorithme gourmand, question d'entrevue, interview d'algorithme, structures de données, interview d'emploi, interview de codage, structures de données et algorithmes, préparation d'entrevues

---

- Oui. 1. Récapitulation des problèmes

> **Code de débit #1775 – Tableau de somme égale avec nombre minimal d'opérations* *
> **Difficulté:** Moyenne

On vous donne deux tableaux entiers `nums1` et `nums2`.
Chaque élément est dans la plage `[1, 6]`. Dans une opération, vous pouvez changer *any* element dans *any* array en n'importe quelle valeur de `1` à `6`.
Retourner le nombre **minimum** d'opérations nécessaires pour que la somme des «nums1» soit égale à la somme des «nums2».
Si cela est impossible, retourner `-1`.

Exemple Entrée Sortie Explication
C'est pas vrai.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
Il est impossible de réduire la somme de "nums1" ou d'augmenter "nums2". Autres
Réduisez deux `6`s à `2` et augmentez `1` à `4`. Autres

**Contrôles* *

- `1 ≤ nums1.longueur, nums2.longueur ≤ 105 "
- `1 ≤ nombres1[i], nombres2[i] ≤ 6'

Le problème semble trompeurment simple – il suffit de penser à *combien* de changements, pas *quel* éléments. Cette observation conduit à une solution cupide très rapide.

---

- Oui. 2. L ' idée fondamentale

1. ** Calculer les sommes courantes. **
«sum1 = ↓(nums1)», «sum2 = ↓(nums2)».
2. **Si les sommes sont déjà égales à → 0 opérations. **
3. **Si une somme maximale possible d'un tableau est encore plus petite que la somme minimale possible d'un autre tableau → impossible (`-1`). * *
(par exemple «len(nums1)*6 < len(nums2)*1» ou vice versa)
4. **Autrement, laissez le tableau avec la plus grande somme être `grand`, l'autre être `petit'.**
Nous *diminuerons* les valeurs dans `big` ** ou** *augmenterons* les valeurs dans `petit`.
La différence `diff = sumBig - sumSmall` est le montant total que nous devons fermer.

5. **Comparer la puissance de chaque élément** – combien il peut contribuer à fermer la différence en une seule opération:
- Pour un élément `x` dans `big`, nous pouvons **la réduire** à `1`, donc la diminution maximale est `x-1`.
- Pour un élément `y` dans `petit`, nous pouvons **augmenter** à `6`, de sorte que l'augmentation maximale est `6-y`.
Conservez-les dans un tableau de fréquences `freq[1..5]` où `freq[d]` = combien d'opérations peuvent fermer **exactement** `d` unités de différence.

6. **Greedy:** Utiliser les plus grands changements possibles en premier (5, 4, 3, 2, 1).
Pour chaque "d" de 5 à 1:
«» "
utilisation = min( freq[d], ceil(diff / d) )
opérations += utilisation
diff -= utilisation * d
si diff <= 0: rupture
«» "

Parce que chaque opération élimine autant de différence que possible, l'approche avide est optimale.

L'algorithme fonctionne dans **O(n)** temps (nous traversons juste les deux tableaux une fois) et utilise **O(1)** espace supplémentaire (`freq[6]`).

---

- Oui. 3. Mise en œuvre intégrale

Vous trouverez ci-dessous un code propre et bien commenté pour **Java, Python et C++**.
Tous les trois suivent le même schéma algorithmique.

#### 3.1 Solution Java (O(n))

"Java
// 1775. Répartition égale de la somme avec le nombre minimum d'opérations
// Java 17, solution O(n) – tableau de fréquence + gourmand
solution de classe {
Services d'information
int sum1 = 0, sum2 = 0;
pour (int x : nombres1) somme1 += x;
pour (int x : nombres2) sum2 += x;

// 1. sommes déjà égales
si (somme1 ==somme2) retourner 0;

// 2. Cas impossible
int len1 = nombres1.longueur, len2 = nombres2.longueur;
si (len1 * 6 < len2) len2 * 6 < len1) retour -1;

// 3. assurez-vous que sum1 > sum2, sinon swap de rôles
si (somme1 < somme2) {
retour minOpérations(nums2, nombres1);
}

int diff = sum1 - sum2; // différence positive que nous devons fermer
int[] freq = nouvelle int[6]; // freq[1..5] – taille de changement possible

// 4. recueillir la puissance de chaque élément
pour (int x : nombres1) { // grand tableau
freq[x - 1]++; // diminution x -> 1
}
pour (int y : nombres2) { // petit tableau
freq[6 - y]++; // augmenter y -> 6
}

// 5. avide du plus grand changement possible
Int ops = 0;
pour (int d = 5; d >= 1; d--) {
si (diff <= 0) pause;
int utilisable = diff / d; // combien de d‐ops complets correspondent
si (diff % d != 0) utilisable++; // +1 si restant
int take = Math.min(freq[d], utilisable);
ops += prise;
diff -= prise * d;
}
les opérations de retour;
}
}
«» "

> ** Points clefs**
> • Le tableau de fréquence n'a que 5 entrées (index 0 inutilisé).
> • Aucune structure supplémentaire de données comme les tas – cela maintient l'utilisation de la mémoire négligeable.

---

3.2 Python (Python 3.10, solution O(n))

'`python
# 1775. Tableau de la somme égale avec le nombre minimum d'opérations
# Python 3.10 – O(n) solution gourmande

def minOpérations(nums1: list[int], nums2: list[int]) -> Int:
somme1, somme2 = somme(nums1), somme(nums2)

si sum1 == sum2:
retour 0

# Contrôle impossible
si len(nums1) * 6 < len(nums2) ou len(nums2) * 6 < len(nums1):
retour -1

# s'assurer que nums1 a la plus grande somme
si somme1 < somme2:
retour minOpérations(nums2, nums1)

diff = somme1 - somme2
freq = [0] * 6 # freq[1..5] – quantité qu'une seule opération peut fermer

pour x en nombres1 : # grand tableau : diminution max x-1
freq[x - 1] += 1
pour y en nombres2: # petit tableau: augmentation max 6 ans
[6 - y] += 1

ops = 0
pour d en range(5, 0, -1): # utiliser avec cupidité les plus grands changements
si diff <= 0:
pause
utilisation = min(freq[d], (diff + d - 1) // d) # ceil(diff/d)
Utilisation
diff -= utilisation * d

retour ops
«» "

---

### 3.3 C++ (solution O(n))

'`cpp
// 1775. Répartition égale de la somme avec le nombre minimum d'opérations
// C++20, solution gourmande O(n) – tableau de fréquences
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minOpérations(vecteur<int>& nums1, vecteur<int>& nums2) {
longue somme1 = 0, somme2 = 0;
pour (int x : nombres1) somme1 += x;
pour (int x : nombres2) sum2 += x;

si (somme1 ==somme2) retourner 0;

int n1 = nombres1.size(), n2 = nombres2.size();
si (n1 * 6LL < n2) n2 * 6LL < n1) retour -1;

si (somme1 < somme2) { // swap pour faire somme1 > somme2
retour minOpérations(nums2, nombres1);
}

long diff = somme1 - somme2; // diff positif
int freq[6] = {0};

pour (int x : nums1) freq[x - 1]++; // grand tableau – peut tomber à 1
pour (int y : nums2) freq[6 - y]++; // petit tableau – peut atteindre 6

Int ops = 0;
pour (int d = 5; d >= 1 && diff > 0; --d) {
utilisation int = min(freq[d], (int)(diff + d - 1) / d)); // ceil
les opérations += utilisation;
diff -= 1LL * utiliser * d;
}
les opérations de retour;
}
};
«» "

> Les trois codes sont identiques en logique, juste une syntaxe différente.
> Compiler avec `javac Solution.java`, `python3 solution.py`, 'g++ -std=c++20 solution.cpp -O2 -o solution`.

---

- Oui. 4. Bon – Mauvais – Analyse Ugly

#### 4.1 Bonne

Autres Pourquoi c'est bon Ce que vous vous vantez dans votre interview
C'est-à-dire...
**O(n) time** – linéaire dans le nombre total d'éléments.
**O(1) espace** – seulement un tableau de fréquences à 6 éléments.
Autres **Pas de tas / pas de tri** – l'algorithme est le comptage pur.
**Déterministe** – pas de hasard ou de bris d'attache.
**Extremement lisible** – le code n'est que quelques boucles et un tableau. Autres

Ces propriétés se traduisent par une solution *rapide et fiable* qui fonctionne sur toutes les caisses de bord, et surtout, il est **facile à expliquer**. C'est un gros plus dans les interviews.

---

4.2 Mauvais (les pièges potentiels)

Comment l'éviter
C'est-à-dire
**Check impossible incorrect** – oublier la logique *length × 6* vs. *length × 1* signifie que vous pouvez retourner une réponse erronée pour des tableaux qui ne peuvent pas atteindre la somme requise. Autres Effectuez toujours le test d'impossibilité **avant** en échangeant les tableaux. Autres
**Mixing signs** – si vous supposez toujours `sum1 > sum2` mais oubliez d'échanger, le diff devient négatif et la boucle gourmande ne fonctionne pas. Echangez les tableaux si `sum1 < sum2`, ou de façon équivalente, traitez toujours `big` comme si la somme était plus grande. Autres
**Débordement entier** – bien que les sommes soient limitées par `6 * 105`, lorsque vous additionnez de nombreux nombres, vous devriez utiliser `long`/`long`. Autres
**Zero-indexing freq** – assurez-vous de ne jamais accéder à `freq[0]` (nous avons seulement besoin de 1..5). Initialiser `int[] freq = nouveau int[6]`; ignorer l'index 0.
**Cailing division** – oublier le `+ (diff % d == 0 ? 0 : 1) Une partie peut conduire à trop d'opérations. Utiliser `(diff + d - 1) / d` pour calculer `ceil(diff/d)` en toute sécurité. Autres

---

#### 4.3 Doucement – Pourquoi le problème est plus difficile qu'il ne l'est

1. **La puissance d'un élément est non évidente. **
À première vue, vous pourriez penser que vous devez choisir quel élément changer.
Le point de vue clé est que vous ne vous souciez que * combien * d'unités vous pouvez fermer par opération, pas *quel* élément.
Rappelez-vous que chaque élément peut se réduire à `1` ou grandir à `6`.

2. **Équilibrer les deux tableaux.**
La décision d'opérer toujours sur le tableau *larger* est simple, mais vous devez vous rappeler d'échanger les rôles si nécessaire.

3. **Cailing division à l'intérieur de la boucle gourmande. **
Beaucoup de gens utilisent `diff / d` et oublier le +1 quand `diff % d != 0'.
L'astuce est "ceil(diff/d) = diff / d + (diff % d ? 1 : 0)".

4. **Edge-case : vérification impossible** – certains intervieweurs pourraient ne pas en parler.
Il est facile d'ignorer que «len(nums1)*6» pourrait encore être inférieur à «len(nums2)*1».

5. **Test sur des tableaux énormes** – la solution est linéaire, mais vous ne devez pas accidentellement utiliser une structure de données `O(n log n)` comme un tas.
Cela passera toujours sur Leetcode, mais vous coûtera beaucoup d'exécution.

---

- Oui. 5. Autres approches (priorité)

Si vous préférez *en fait* garder les éléments les plus prometteurs dans une file d'attente prioritaire, l'algorithme fonctionne encore, mais il est **O((n1 + n2) log(n1 + n2)** et consomme plus de mémoire.

**Étapes de haut niveau**

1. Mettre chaque élément du tableau de somme plus petite dans un potential max-heap («+5»).
2. Mettre tous les éléments du tableau de somme plus grande dans un minimum (potentiel «-5 »).
3. Alors que `diff > 0`, pop le meilleur candidat du tas approprié, le changer à l'extrême (`1` ou `6`), repousser la nouvelle valeur, mettre à jour `diff`, et compter une opération.
4. Si les sommets sont déjà à leurs extrémités (`1` dans min-heap ou `6` dans max-heap) et `diff` toujours > 0 → impossible.

Cette approche est conceptuellement facile à voir pour les intervieweurs, mais est plus lente et utilise plus de mémoire.

---

- Oui. 6. Comment se préparer à cette question

Thème Pourquoi ça compte ?
- Oui.
**Greedy Algorithmes**La solution de base est gourmande : utilisez le plus grand changement d'abord. Pratique avec la couverture de l'intervalle, le changement de pièce, la sélection d'activité. *Cracking the Coding Interview*, section sur le LeetCode
Autres **Tarifs de calcul / de fréquence** *Algorithmes sur le code de Leet* – Tri de la composition
Autres **Edge‐Case Thinking** . L'impossible vérification et la manipulation des signes sont subtiles. Pratiquez les cas d'angle sur des tableaux de longueurs variables. Section "Array Bounds" sur *Exercisme* ou *HackerRank*
**Intuition mathématique**Le tour de division "ceil" est courant dans de nombreuses questions d'entrevue. Article sur GeeksforGeeks
Autres **Maîtrise de la complexité du temps**= Comprendre quand `O(n log n)` vs `O(n)` importe. Feuille de chaleur* (Code Leet)
**Testation**LeetCode vous permet de créer d'énormes cas de test pour confirmer la linéarité.

Plan d'étude rapide (7 jours)

Journée Focus Pratique
C'est pas vrai.
Autres Lire l'énoncé du problème lentement, paraphraser dans vos propres mots. Code leet 1775
Autres 2= Écrire la solution du tableau de fréquence à partir de zéro. Solution ci-dessus
Autres Expliquez chaque étape à haute voix; apprenez-le à un canard en caoutchouc.
Autres Essayez la variante priority-queue ; comparez les runtimes. Code du leet
Autres Écrire des cas de test : aléatoires, tous les mêmes nombres, des cas impossibles. Déclarations `assert` dans Python
Autres 6= Entretien avec un ami : expliquer la solution en 5 minutes. InterviewBit simulation interview
Autres Revue Good‐Bad‐Ugly analyse, jot points clés sur une feuille de triche. Remarques personnelles

---

- Oui. 7. Conclusion

- La solution cupide **O(n)** utilisant un tableau de fréquences est la norme *or* pour 1775 sur Leetcode.
- Oui. Il présente la linéarité, la mémoire constante et une approche de comptage propre – idéal pour toute entrevue d'ingénierie logicielle.
- Souvenez-vous des quelques écueils et de la logique impossible de vérification, qui vous sépareront des candidats qui oublient les cas de bord.

Bonne chance ! Et si vous êtes coincé, n'oubliez pas : **comptez le montant que vous pouvez fermer par opération, choisissez le plus grand et répétez**. C'est la formule gagnante. C'est ce qu'il a dit.

---

**Bonus**: Voici un extrait rapide pour exécuter les trois implémentations sur les mêmes données de test, pour s'assurer qu'ils sont tous d'accord:

'`cpp
// solution.cpp – harnais d'essai pour les trois implémentations
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// (Insérer la classe de solution C++ ici)

// Solution Python comme pointeur de fonction – omis pour la brièveté

Int main() {
vecteur<int> a{3,2,3};
vecteur<int> b{3,5,3,4};
Solution s;
Cout << s.minOpérations(a, b) << endl; // attendu 2
}
«» "

Compilez et exécutez – le résultat doit correspondre à la sortie attendue de Leetcode.

Bon codage, et que votre entrevue soit *rapide, propre et antidérapante*! C'est ce qu'il a dit.

---

* Sentez-vous libre de déposer un commentaire si vous avez besoin de plus d'explication ou d'avoir une variante de ce problème que vous souhaitez discuter. *