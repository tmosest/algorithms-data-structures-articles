---
titre: LeetCode 3209. Nombre de sous-barrages avec et valeur de K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3209 – Nombre de sous-barrages avec et valeur de K
> **Objectif:** Compter tous les sous-tribus contigus dont le bitwise ET est égal à *k*
> **Langues:** Java.
> **Cible auprès du public:** Ingénieurs, intervieweurs, recruteurs

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Pourquoi ce problème rocks] (# pourquoi ce problème rocks)
3. [solution de haut niveau] (#solution de haut niveau)
4. [Analyse de la complexité] (#analyse de la complexité)
5. [Mise en œuvre – HashMap-Based](#mise en oeuvre---hashmap-based)
* Java
* Python
* C++
6. [Approches alternatives] (#approches alternatives)
7. [Pièges communs et cas de bord] (#pierres communes -- cas de bord)
8. [Blog-Style -Le bon, le mauvais, le mauvais] (#blog-style-le-bon-le-mauvais)
9. [SEO Tips for Your Resume & Blog](#seo-tips-for-votre-résume--blog)
10. [Enveloppe](#Enveloppe)

---

- Oui. 1. Énoncé du problème <un nom="problème-statement"></a>

> **Donné** d'un nombre entier et d'un k entier,
> **Retour** le nombre de sous-groupes ** (sous-groupes contigus) de telle sorte que le bitwise ET de tous les éléments du sous-groupe égal `k`.
> **Constraints**
> - `1 <= nombres.longueur <= 10^5`
> - `0 <= nombres[i], k <= 10^9`

La solution de la force brute `O(n^2)` échoue lorsque `n = 10^5`. Nous avons besoin d'un algorithme linéaire.

---

- Oui. 2. Pourquoi ce problème fait-il des rocs <un nom>

Raison
- Oui.
**Bitwise mastery** – présente une compréhension profonde des opérations bitwise. Autres
Autres **Fenêtre coulissante + hashmap** – combo d'interview populaire. Autres
**Cas lourd** – difficile `k = 0`, grand nombre, valeurs répétées. Autres
Autres La pertinence du monde réel** apparaît souvent dans les problèmes de diffusion et d'analyse des données. Autres

Une solution solide démontre la pensée algorithmique, la qualité du code et les astuces spécifiques que les recruteurs aiment.

---

- Oui. 3. Solution de haut niveau <un nom="solution de haut niveau"></a>

Observation

Le bitwise ET d'une sous-tribu est toujours **non-croissant** alors que nous étendons la sous-tribu à droite :

«» "
a & b & c <= a & b <= a
«» "

Par conséquent, **pour une fin droite fixe `i`, les valeurs ET des sous-ensembles se terminant par `i` ne peuvent prendre que 31 valeurs distinctes** (une position par bit).

Idée

Traverser le tableau une fois tout en maintenant une carte :

- **Key** – possible ET valeur d'un sous-réseau qui se termine à l'indice actuel.
- **Valeur** – combien de sous-cours se terminant à l'indice actuel produisent que ET.

Pour chaque nouvel élément `x = nombres[i]`:

1. Démarrer une nouvelle carte "curr".
2. Pour chaque précédente ET `prev` dans la carte:
- "nouveau Et = prev & x "
- Si `newAnd= k`, ajouter `cnt(prev)` à la réponse.
- Ajouter `cnt(prev)` à `curr[newAnd]`.
3. Comptabilisez également la sous-entente constituée uniquement de «x»:
- Si `x == k`, réponse par incrément.
- Incrément "curr[x]".

Définir `prev = curr` et répéter.

Parce que chaque carte contient ≤ 31 clés, l'algorithme entier fonctionne dans **O(n · 31)** temps et **O(31)** espace supplémentaire.

---

- Oui. 4. Analyse de complexité <un nom="analyse de complexité"></a>

Valeur métrique
C'est pas vrai.
**Heure**="O(n · B)" où `B = 31` (bits en int 32-bit). Pour `n = 10^5`, environ 3 × 10^6 opérations – facilement sous 1 s.
**L'espace**="O(B)" – au plus 31 paires de clés/valeurs à tout moment. Autres
**Type de réponse**= 64 bits entier (`long` en Java, `int64`/`long` en C++, `int` en Python). Autres

---

- Oui. 5. Mise en oeuvre – HashMap-Based <a name ---hashmap-based"></a>

#### 5.1 Java

"Java
Importer java.util. HashMap;

solution de classe publique {
compte long publicSubarrays(int[] nums, int k) {
réponse longue = 0;
HashMap<entier, entier> prev = nouveau HashMap<>();

pour (int x : nombres) {
HashMap<entier, entier> curr = nouveau HashMap<>();

// Sous-recours composé de seulement x
si (x == k) réponse++;
curr.merge(x, 1, entier::sum);

// Prolonger tous les sous-cours précédents
pour (entrée var : prev.entrySet()) {
int prevAnd = entry.getKey();
int cnt = entrée.getValue();
Int nouveau Et = prevAnd & x;
si (newAnd) k) réponse += cnt;
curr.merge(nouveau) Et, cnt, entier::sum);
}
prev = curr;
}
réponse de retour;
}
}
«» "

5.2 Python

'`python
de collections importer par défautdict

Solution de classe:
def countSubarrays(self, nombres: list[int], k: int) -> Int:
ans = 0
prev = defaultdict(int)

pour x en nombres:
curr = defaultdict(int)

# Sous-tribution d'éléments uniques
Si x == k:
+= 1
pour [x] += 1

# Prolonger les sous-cours précédents
pour prev_and, cnt dans prev.items():
new_and = prev_and & x
if new_and == k:
ans += cnt
[nouveau_et] += Cnt

prev = curr
retour et
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre longSubarrays(vector<int>& nums, int k) {
long an = 0;
unordered_map<int, int> prev, curr;
pour (int x : nombres) {
clar.clair();
// Sous-délai de longueur 1
si (x == k) ans++;
pour [x] += 1;
pour (auto &p : prev) {
int prevAnd = p.first, cnt = p.seconde;
Int nouveau Et = prevAnd & x;
si (newAnd) k) ans += cnt;
[nouveau] += cnt;
}
prev.swap(curr);
}
le retour des an;
}
};
«» "

> **Astuce:** En C++, vous pouvez remplacer `unordered_map` par `std::map` si vous préférez les clés commandées; la différence de performance est négligeable pour ≤ 31 entrées.

---

- Oui. 6. Approches alternatives <un nom="approches alternatives"></a>

Méthode de fonctionnement
- C'est quoi ?
**Fenêtre coulissante** (deux pointeurs)* Garder une fenêtre où ET == k; réduire de gauche jusqu'à ET > k. Autres
**Bit DP** Complexe, difficile à mettre en œuvre; risque de débordement. Autres
Autres **Segment Tree / Sparse Table** ► Pré-calculer ET sur les plages; itérer tous les démarrages, fin de recherche binaire. Peut répondre aux requêtes rapidement.(O(n log n) espace/temps, trop de compétences pour ce problème. Autres

La solution à base de hashmap est la plus *propre*, * bien documentée* et *rapide* pour les contraintes données.

---

- Oui. 7. Pièges communs et cas de bordure <un nom="pièges communs--cas de bordure"></a>

Piège
- Oui.
**Utiliser `int` pour la réponse** Pour `n=10^5`, la réponse peut être jusqu'à ~5 × 10^9. Autres
**Overflow dans Java `int` touches de carte**. Les valeurs peuvent être des nombres `int` parce que chaque entrée de carte est ≤ n. Autres
**Négligence de la sous-période de longueur Vérifiez toujours `x == k` avant de traiter les AND précédents.
**Utiliser `pour (clé int : prevMap.keySet())` En Java** , la modification de la carte pendant que l'itération conduit à `ConcurrentModificationException`. Utilisez une liste séparée de clés ou itérer sur l'ensemble d'entrée. Autres
**Ne pas réinitialiser la carte "curr" à chaque itération**. Autres
**Large `k` (p. ex., 10^9)** Autres
**Tous les zéros** Le nombre sera `n*(n+1)/2`. Autres

---

- Oui. 8. Le bon, le mauvais, le mauvais nom, le style blog, le bon, le mauvais...

> *Titre: Le bon, le mauvais, et le lamentable de compter les sous-images avec et la valeur de K.*

> **SEO Mots-clés** – Leetcode 3209, bitwise ET subarray, problème de codage d'entretien, solution Java Python C++, approche de hashmap, interview d'algorithme, entretien d'ingénieur logiciel, obtenir un emploi.

Introduction

Dans les interviews de codage, le *Nombre de Subarrays Avec ET Valeur de K* est un test classique de prouesses de manipulation de bits et d'efficacité algorithmique. Alors que l'énoncé est trompeurment simple, concevoir une solution optimale implique une poignée d'idées subtiles. Dans ce post, nous allons décomposer le **bon** (ce que vous devriez faire), le **mauvais** (ce que vous devriez éviter), et le **ugly** (les pièges qui guettent quand vous êtes pas prudent).

---

C'est vrai. Le Bon – Maîtriser le Trick HashMap

1. ** Tirer parti de la propriété non croissante de ET** – alors que vous étendez une sous-tribu à droite, son ET ne peut que perdre des bits, jamais les gagner.
2. **Conservez seulement des valeurs ET uniques** – pour toute extrémité droite, il y a au plus 31 résultats ET distincts (un par bit).
3. **Mise à jour des comptes incrémentalement** – utilisez une carte `prev` qui contient les comptes de toutes les valeurs ET se terminant à l'index précédent. Pour chaque nouvel élément, calculez de nouveaux ET et accumulez la réponse quand ils sont égaux à "k".
4. **Comptabilisent toujours les sous-tribus à éléments uniques** – ils sont le cas de base.

Résultat: **O(n · 31)** temps, **O(31)** espace, entièrement déterministe, et très facile à traduire en Java, Python ou C++.

---

C'est vrai. Les mauvais – Des erreurs communes

Pourquoi ça casse
C'est pas vrai.
**Fils pour `n=10^5'. Autres
Autres **Mise à jour de la même carte pendant l' itération**. Autres
**Utiliser `int` pour la réponse** Autres
Autres 4= **Skipping single-element case**= Sous-dénombrements lorsque `k=nums[i]'. Autres
*En supposant que la fenêtre coulissante fonctionne**** ET ne se déplace pas lorsque vous déplacez le pointeur droit; la taille de la fenêtre peut devenir exponentielle. Autres

---

C'est vrai. Les cas d'indulgence – Bord de Tricky

1. **Tous les zéros** – Alors que l'algorithme s'en occupe, de nombreuses solutions naïves oublient que chaque sous-cours ET est 0, causant un sous-compte massif.
2. **Très grandes valeurs `k`** – Pas de problème pour les ints 32 bits, mais il peut vous induire en erreur dans la réflexion des optimisations spécifiques aux bits sont nécessaires.
3. ** Tailles entières non standard** (p. ex. 64-bit)= Vous devez vous assurer que votre carte utilise la bonne largeur; sinon vous vous tromperez ET les résultats. Autres
4. **Les plus grandes entrées de test**= La carte pourrait croître si vous utilisez une structure de données qui ne prune pas les touches, conduisant à un agrandissement de la mémoire. Autres

---

C'est vrai. L'horrible – Comment l'éviter

- **Toujours tester avec les entrées de bord** – `n=1`, tous les zéros, tous ceux, les bits alternés, etc.
- **Utilisez une copie des touches** lors de l' itération (`Liste<Integer> touches = nouvelle ArrayList<>(prev.keySet());`).
- **Swap maps** au lieu de ré-allouer – `prev.swap(curr)` en C++ ou `prev = curr` après `clear()`.
- **Validez avec la force brute pour les petits cas** – assure la justesse avant l'échelle.

---

À emporter

Lorsque vous entrez dans une salle d'entrevue, l'intervieweur s'attend à ce que vous pensiez *en bits*. En utilisant l'approche du hashmap, vous démontrez :

- **Perspective algorithmique** – reconnaître que l'opération ET réduit la complexité.
- **Codage discipline** – manipulation soigneuse des cartes, des gros entiers et des cas de base.
- **Adaptabilité** – la solution est language-agnostique, vous pouvez en discuter en Java, puis passer rapidement en Python ou C++.

Ce mélange de *profondeur technique* et *Simplicité de mise en oeuvre* est exactement ce que les gestionnaires d'embauche recherchent quand ils demandent, "Pouvez-vous résoudre Leetcode 3209?

---

- Oui. 9. Conclusion <un nom="conclusion"></a>

La solution à base de hashmap est **robuste, rapide et linguistique**. En suivant les lignes directrices de la présente mise à jour de la carte, en corrigeant les types de données et en manipulant des sous-réseaux à éléments uniques, vous éviterez les pièges les plus courants. Que vous soyez en train de vous préparer à une entrevue de codage ou de résoudre un problème de concours, maîtriser cette astuce vous donnera un avantage concurrentiel.

> *Le bien de ce problème est l'élégance de l'astuce de hashmap; le mal est la tentation de la force brute ou de la manipulation de cartes sans souci; le laid est le débordement subtil et les bugs qui sabotent des solutions par ailleurs correctes.

Bon codage, et bonne chance d'obtenir ce travail de rêve!

---

- Oui. 9. Pensées finales <un nom="conclusion"></a>

> *Titre: De Code à Carrière: Résoudre le Leetcode 3209 avec HashMaps

> **SEO** – solution Leetcode 3209, algorithme d'entretien, bitwise AND, Java Python C++.

**Si vous venez de terminer le codage de la solution, vous pouvez déjà l'utiliser comme point de discussion dans les interviews.** Discutez de l'observation sur le ET non-augmentation, la limite de 31 clés, et comment l'algorithme reste linéaire. La plupart des recruteurs seront impressionnés par ce niveau de perspicacité.

---

> **Télécharger l'implémentation complète** dans la langue de votre choix à partir de la repo GitHub (lien).
> **Essayez-le** sur Leetcode ou votre IDE local, et gardez une minuterie pour voir la performance.

Joyeux entretien, et que les morceaux soient toujours en votre faveur !*

---

- Oui. 9. Pensées finales <un nom="pensées finales"></a>

L'approche haschmap est une solution *no-frills* qui s'écaille avec grâce. Une fois que vous comprenez l'observation clé — ET les valeurs se rétrécissent et sont limitées par le nombre de bits — vous pouvez écrire du code propre et prêt à produire dans n'importe quelle langue.

> ** À emporter pour les recruteurs :**
> - *Montrer l'observation. *
> - *Mention liée à 31 clés. *
> - *Produire la solution O(n · 31). *

C'est une réponse solide qui dit, Je connais l'astuce, Je connais les limites, et je peux l'appliquer correctement. Parfait pour décrocher un rôle d'ingénierie logicielle!