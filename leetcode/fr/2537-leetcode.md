---
titre: LeetCode 2537. Compter le nombre de bons subarrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2537 – Compter le nombre de bonnes subarraies
*Code de leet*- *Java*- *Python*- *C++*- *Sliding-Window*- *Entretien d'emploi*

Ci-dessous vous trouverez une implémentation prête à la production pour **Java, Python et C++** qui résout le problème LeetCode **2537 – Comptez le nombre de bons subarrays** en *O(n)* en utilisant la technique classique de la fenêtre coulissante à deux points.

---

- Oui. 1. Récapitulation des problèmes

> **Définition** – Un sous-barrage est *bon* s'il contient **au moins des paires `k` d'éléments égaux**.
>
> Entrée: `int[] nums` (en chiffres ≤ 105, 0 ≤ nums[i] ≤ 109) et `int k` (0 ≤ k ≤ 109).
> Produit : nombre de sous-arrayes *bonnes* (type de retour "long`/`long`).

La solution de la force brute examinerait chaque sous-aire (O(n2)), ce qui est beaucoup trop lent pour les contraintes. Le tour de la fenêtre coulissante le transforme en algorithme linéaire.

---

- Oui. 2. Sliding-Window Insight

Autres Qu'est-ce que tu *track*- Pourquoi ça marche
- Oui.
Une carte de fréquence (`freq`) Autres
"pairs` – nombre de paires égales dans la fenêtre courante" Ajouter un élément de valeur `x` crée `freq[x]` nouvelles paires (depuis chacune des `freq[x]` existantes occurrences peuvent être jumelées avec le nouveau). Autres
– pointeur gauche de la fenêtre Lorsque la fenêtre est bonne (`pairs` ≥ `k`), chaque sous-barrage qui commence à un indice ≤ `gauche` et se termine à l'indice courant droit est bon. Le nombre de ces subarrays est égal à "gauche". Autres

**Invariant de boucle clé** – Après avoir rétréci la fenêtre pendant qu'elle reste bonne, la fenêtre `[gauche ... droite]` est la fenêtre *la plus petite* se terminant à "droite" qui satisfait encore à l'exigence. Ainsi, tous les subarrays se terminant à `à droite` qui commencent **avant** `gauche` sont garantis être bons, et nous ajoutons `à gauche` à la réponse.

---

- Oui. 3. Mise en œuvre des références

### Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
***
* Renvoie le nombre de bons sous-arrachages dans le temps O(n).
* @param nums le tableau des entiers
* @param k le nombre requis de paires
* @return le compte de bons subarrays (long pour éviter le débordement)
*/
compte public longGood(int[] nums, int k) {
Carte<integer, integer> freq = nouveau HashMap<>();
int gauche = 0; // limite gauche de la fenêtre actuelle
long ans = 0;
paires int = 0; // nombre de paires égales à l'intérieur de la fenêtre

pour (int droite = 0; droite < nums.longueur; droite++) {
int cur = nombres[droite];
// Ajouter cur ajoute freq[cur] de nouvelles paires
paires += freq.getOrDefault(cur, 0);
freq.put(cur, freq.getOrDefault(cur, 0) + 1);

// Réduire la fenêtre pendant que nous avons assez de paires
pendant que (paires >= k) {
ans += nums.longueur - droite; // tous les sous-arrachages qui commencent à 'gauche' sont bons
Int gauche Val = nombres[gauche];
int gaucheFreq = freq.get(leftVal);

// Suppression à gauche Val réduit le nombre de paires de (gaucheFrek - 1)
paires -= (gaucheFrek - 1);
Si (leftFreq) 1) {
freq.remove(leftVal);
} autre {
freq.put(gaucheVal, gaucheFreq - 1);
}
gauche++;
}
}
le retour des an;
}
}
«» "

---

Python

'`python
de collections importer par défautdict
de taper l'importation Liste

def countGood(nums: List[int], k: int) -> Int:
"""
Compter de bons sous-arrachages en temps O(n).
:param nombres: List[int] – tableau d'entrée
Param k: int – nombre requis de paires égales
:retour: int – nombre de bons subarrays
"""
freq = defaultdict(int) # element → fréquence dans la fenêtre actuelle
gauche = 0 # limite gauche de la fenêtre
paires = 0 nombre de paires égales dans la fenêtre
ans = 0

pour droite, val in énumérate(nums):
# Ajouter un nouvel élément crée `freq[val]` nouvelles paires
paires += freq[val]
freq[val] += 1

Alors que la fenêtre est encore bonne, rétrécissez-la de la gauche
alors que les paires >= k:
Tous les subarrays qui partent du moment 'gauche' à 'droite' sont bons
ans += droite - gauche + 1
gauche_val = nombres[gauche]
gauche_freq = freq[left_val]

# Supprimer le_val gauche réduit les paires par (left_freq - 1)
paires -= (gauche_freq - 1)
freq[left_val] = gauche_freq - 1
gauche += 1

retour et
«» "

> **Pourquoi `ans += droite - gauche + 1`?**
> Une fois que nous trouvons la gauche minimale qui garde encore la fenêtre bonne, chaque sous-barrage qui commence à `gauche` ** ou plus tard** et se termine à `droite` contiendra également au moins des paires `k`. Le nombre de ces subarrays est exactement "à droite - à gauche + 1".

---

C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
utilisant l'espace de noms std;

solution de classe {
public:
***
* @param nums le tableau des entiers
* @param k le nombre requis de paires
* @return le nombre de bons subarrays (long pour éviter le débordement)
*/
long compteGood(vector<int>& nums, int k) {
unordered_map<int, int> freq;
long an = 0;
int gauche = 0; // limite gauche de la fenêtre
longues paires longues = 0; // nombre de paires égales à l'intérieur de la fenêtre

pour (int right = 0; right < (int)nums.size(); ++right) {
int cur = nombres[droite];
// Ajouter cur crée freq[cur] de nouvelles paires
paires += freq[cur];
++freq[cur];

// Réduire la fenêtre pendant que nous avons assez de paires
pendant que (paires >= k) {
ans += nums.size() - droite; // toutes les sous-couches commençant à 'gauche' sont bonnes
Int gauche Val = nombres[gauche];
int gaucheFreq = freq[leftVal];

// Suppression à gauche Val réduit les paires par (gaucheFreq - 1)
paires -= (gaucheFrek - 1);
Si (leftFreq) 1) freq.erase (leftVal);
sinon freq[leftVal] = gaucheFreq - 1;
+ + gauche;
}
}
le retour des an;
}
};
«» "

> **Astuce:** Dans de nombreuses solutions acceptées, vous verrez la variable `k` être décrémentée/incrémentée pour suivre le quota de paire restant. La logique est équivalente à ce que nous avons décrit ci-dessus – juste un style de comptabilité légèrement différent.

---

- Oui. 4. La bonne, mauvaise et laborieuse de cette solution

Qu'est-ce qui le rend bon ? Qu'est-ce qui pourrait mal tourner ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bon**=Temps linéaire, facile à comprendre une fois que l'astuce du nombre de paires est saisi.
Vous devez garder `k` *mutable* ou maintenir un compteur `pairs` séparé; mélanger les deux peut conduire à des bogues. Autres
La logique selon laquelle l'ajout d'un élément augmente les paires par sa fréquence actuelle n'est pas évidente à première vue. Autres

---

- Oui. 5. SEO-Optimized Blog Post

Maître LeetCode 2537: Comptez le nombre de bonnes sous-tribus

Si vous êtes en train de vous préparer à un **entretien d'ingénierie logiciel** ou un **codage bootcamp** et voulez ace **LeetCode 2537 – Comptez le nombre de bons subarrays**, vous êtes au bon endroit.
Dans cet article, nous allons:

1. Divisez l'algorithme **sliding-window** qui amène la complexité temporelle de **O(n2)** à **O(n)**.
2. Fournir un code propre et prêt à la production en **Java**, **Python** et **C++**.
3. Expliquez les points délicats, les pièges et comment parler de cette solution dans une interview.

C'est vrai. Mots clés :
- LeetCode 2537
- Compter le nombre de bons subarrays
- Fenêtre coulissante
- Entretien avec un algorithme Java
- Défi de codage Python
- Explication de l'algorithme C++
- Algorithme d'entretien d'emploi

---

Qu'est-ce qu'une Subarray ?

> Un sous-barrage est **bon** s'il contient au moins des paires `k` d'éléments égaux.
> Une paire est une paire d'indices `(i, j)` avec `i < j` et `nums[i] == nums[j]`.

La solution naïve vérifierait chaque sous-aire et compterait ses paires, donnant **O(n2)** temps. Ce n'est pas faisable pour "n ≤ 100 000".

---

### ♫ Glissement de la fenêtre vers le sauvetage

Le cœur de la solution est une approche **deux-pointeurs**:

- **Pointeur droit** élargit la fenêtre un élément à la fois.
- **Le pointeur gauche** rétrécit la fenêtre alors que la fenêtre satisfait encore aux exigences de la paire.

Astuce clé :
*Lorsque vous ajoutez un nouvel élément de valeur `x`, le nombre de nouvelles paires correspond à la fréquence courante de `x` dans la fenêtre. *
Ainsi, nous conservons une carte **fréquence** et un compteur "paires".

L'invariant après rétrécissement de la fenêtre est :
*'[à gauche ... à droite]' est la plus petite fenêtre qui contient encore au moins des paires `k`. *
Tous les subarrays qui se terminent à droite et commencent ** avant** `gauche` sont automatiquement bons.

---

Code de référence – Java, Python, C++

Nous avons déjà fourni les implémentations complètes ci-dessus. Dans les interviews, vous pouvez choisir la langue avec laquelle vous êtes le plus à l'aise, mais la logique est identique :

"Java
// Java
compte public longGood(int[] nums, int k) { ... }
«» "

'`python
# Python
def countGood(nums: List[int], k: int) -> Int: ...
«» "

'`cpp
// C++
long compteGood(vector<int>& nums, int k) { ... }
«» "

> **Pourquoi utilisons-nous `long' (ou `long' en Java)? * *
> La réponse peut être aussi grande que `n * (n+1) / 2`, ce qui dépasse la gamme entière 32 bits pour les grandes entrées.

---

Parler de la solution dans une entrevue

> **Question:** - Expliquez comment vous approcheriez LeetCode 2537. (en milliers de dollars)
> **Réponse (TL;DR):* *
> Utilisez une fenêtre coulissante. Je tiens une carte de fréquence et un compteur de paires. Alors que je glisse le pointeur de droite, j'ajoute la nouvelle fréquence courante d'élément à "paires". Puis je continue à déplacer le pointeur gauche jusqu'à ce que `pairs` tombe sous `k`. Chaque fois que la fenêtre est bonne, j'ajoute le nombre de sous-arrachés qui commencent avant le pointeur de gauche à ma réponse. (en milliers de dollars)

Si l'intervieweur demande **pourquoi c'est linéaire**:
- Le bon pointeur bouge **n** fois.
- Chaque mouvement de pointeur gauche se déplace également au plus **n** fois.
- Toutes les opérations sur la carte de hachage sont * amorties* O(1).
- Le temps total est **O(n)**, mémoire **O(min(n, valeurs distinctes)**.

---

À emporter

- Fenêtre coulissante + carte de fréquence = la solution standard pour LeetCode 2537.
- Oui. L'astuce du compte de paires est le moment "Eureka" : *ajouter `freq[x]` lorsque vous insérez `x`*.
- Avoir un code propre dans **Java, Python, C++** montre que vous comprenez les idiomes spécifiques au langage tout en maintenant l'idée centrale inchangée.

Bonne chance ! » Souvenez-vous, la clé de l'atterrissage que le rôle d'ingénierie logicielle n'est pas seulement d'avoir une solution correcte, mais de pouvoir expliquer *pourquoi* cela fonctionne. Bon codage !