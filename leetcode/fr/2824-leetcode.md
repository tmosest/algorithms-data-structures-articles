---
titre: LeetCode 2824. Nombre de paires dont la somme est inférieure à la cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2824 – Nombre de paires dont la somme est inférieure à la cible
**Python de Java + un billet de blog SEO *

---

- Oui. 1. Solutions de code

Voici trois solutions entièrement commentées prêtes à être copiées pour **Java 17**, **Python 3.10+** et **C++17**. Tous utilisent la stratégie optimale **O(n log n)** à deux points après tri du tableau.

---

##### 1.1 Java

"Java
Importer java.util. Les tableaux;
Importer java.util. Liste;

solution de classe publique {

***
* Comptez le nombre de paires d'indices (i, j) tels que i < j et nums[i] + nums[j] < cible.
*
* @param nums Liste des entiers (0-indexés).
* Cible @param Seuil de somme cible.
* @retour Nombre de paires valides.
*/
compte int publicPairs(Liste<Intéger> nombres, cible int) {
// Convertir la liste en tableau pour le tri en place
int n = nombres.size();
int[] arr = nouvelle int[n];
pour (int i = 0; i < n; i++) arr[i] = nums.get(i);

// 1. Tri ascendant
Tableau 3.

// 2. Scannage à deux points
int gauche = 0, droite = n - 1, nombre = 0;
pendant que (à gauche < à droite) {
si (arr[gauche] + arr[droite] < cible) {
// Toutes les paires (gauche, gauche+1 ... droite) sont valides
nombre += droite - gauche;
gauche++; // déplacer le pointeur gauche pour essayer un élément gauche plus grand
} autre {
droite--; // réduire la somme du côté droit
}
}
le nombre de retours;
}
}
«» "

---

##### 1.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def countPairs(self, nombres: List[int], cible: int) -> Int:
"""
Nombre de paires (i, j) avec i < j et nums[i] + nums[j] < cible.
Utilise le tri + deux pointeurs pour le temps O(n log n).
"""
nombres.sort() # O(n log n)
gauche, droite, nombre = 0, len(nums) - 1, 0

à gauche < à droite:
si nombres[gauche] + nombres[droite] < cible:
count += droite - gauche # toutes les paires avec le courant gauche sont valides
gauche += 1
Sinon:
droite -= 1

Nombre de retours
«» "

---

*### 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre intPairs(vecteur<int>& nombres, cible int) {
// 1. Trier le tableau
(noms.begin(), nums.end()); // O(n log n)

Int gauche = 0;
int droite = nums.size() - 1;
longue longueur = 0; // utiliser longtemps pour la sécurité

// 2. Traversée à deux points
pendant que (à gauche < à droite) {
si (nombres[gauche] + nombres[droite] < cible) {
count += droite - gauche; // toutes les paires avec le courant gauche
+ + gauche;
} autre {
--droite;
}
}
retourner static_cast<int>(compte);
}
};
«» "

---

- Oui. 2. Billet de blog – Le bon, le mauvais, et le mauvais de LeetCode 2824

> **Mots clés**: Nombre de paires Dont la somme est inférieure à la cible, LeetCode 2824, deux pointeurs, interview algorithme, solution Java, solution Python, solution C++, prép d'entrevue de codage, algorithme optimal, tri, force brute, recherche binaire, défi de codage d'entrevue.

---

Introduction

Si vous avez été à la chasse pour ça Problème LeetCode pour présenter vos côtelettes algorithmiques sur votre CV, **LeetCode 2824 – Nombre de paires Dont la somme est inférieure à la cible** est un endroit doux. C'est **facile** mais qui démontre la maîtrise des techniques classiques : tri, double pointeur et analyse de complexité. Dans cet article, nous allons marcher à travers le problème, discuter de l'approche optimale, mettre en évidence les pièges (-) et montrer comment transformer la solution en une étoile de conversation pendant les entretiens (-) est généralement le lien manquant.

---

### Déclaration de problème

> *Avec un tableau entier `nums` et un entier `target`, compter combien de paires `(i, j)` avec `0 <= i < j < n` satisfont `nums[i] + nums[j] <target`. *

Les contraintes sont minuscules (`n ≤ 50`), mais cela cache le fait qu`une force brute naïve `O(n2)` est toujours acceptable. Cependant, les intervieweurs aiment vous voir résoudre dans **`O(n log n)`**.

---

### Bonne – Pourquoi les Trick Rocks à deux points

1. **Intuitive après tri**
Lorsque le tableau est trié, si `nums[left] + nums[right]` est déjà < `target`, *chaque élément entre `left` et `right` sera jumelé avec `nums[right]` de rester en dessous de la "cible". Cela nous permet d'ajouter des paires `droite - gauche` en une seule étape.

2. **Scannage linéaire post-sortie**
Après triage (`O(n log n)`), nous ne traversons le tableau qu'une seule fois (`O(n)`), rendant l'algorithme rapide et respectueux de la mémoire (`O(1)` espace auxiliaire si le tri en place est utilisé).

3. **Extension**
Le même modèle résout des variantes :
- Nombre de paires avec une somme ≤ "cible".
- Compter les paires dont la somme est à l'intérieur d'une fourchette ('[faible, élevée]').
- Trouvez la plus petite somme.

4. **Code clair**
Une implémentation concise est facile à comprendre, à déboguer et à prouver avec une petite preuve par induction ou invariant de boucle.

---

### Mauvais – Erreurs courantes et comment éviter Eux

Pourquoi ça arrive ?
- Oui.
**O(n2) Brute Force** Utiliser la logique de deux points une fois le tableau trié. Autres
Autres **Désormais chaque cas de test séparément**. Classer à l'intérieur de la fonction – le coût est négligeable pour `n ≤ 50`. Autres
**L'utilisation de `int` pour compter sur de grandes entrées**= `n` peut être jusqu'à `50`, mais si des contraintes changent (par exemple, `n = 105`) le débordement se produit.= Utiliser `long`/`long` pour compter. Autres
**Manipulation des nombres négatifs** La logique tient parce que le tri des ordres négatifs correctement. Autres
**Off‐By‐One Erreurs dans les pointeurs** (compte += droite - gauche) * puis* incrément "gauche". Autres

---

### # Ugly – Les intervieweurs aiment sonder

1. **Proof d'exactitude**
Les intervieweurs demandent souvent : *Pourquoi l'ajout de `droite - gauche' garantit-il la validité de toutes ces paires ? *
**Réponse:** Dans un tableau trié, tout élément entre `left` et `right` est ≥ `nums[left]` et ≤ «nums[right]». Si `nums[left] + nums[right] < cible`, alors pour tout `k` avec `left < k < droite`, `nums[k] + nums[right]` ≤ `nums[right] + nums[right]` mais toujours < `target` parce que `nums[k]` ≥ `nums[left]`. Ainsi, toutes ces paires sont valides.

2. **Modifications de complexité* *
Montrez que le tri domine le temps d'exécution (« O(n log n) »), tandis que la partie à deux points est linéaire (« O(n) »).

3. **Délibérations**
*Un tableau d'attente? * *Tous les éléments sont égaux?* *Toutes les sommes déjà inférieures à la cible?* Démontrer que l'algorithme les gère avec grâce.

4. **Alternatives optimisées pour l'espace* *
Si `nums` ne peut pas être trié en place, discutez avec `std::nth_element` en C++ ou copiez dans une nouvelle liste en Python pour garder l'original intact.

5. **Variations**
Demandez-lui si nous voulions trouver la plus petite paire *k* ? – pivoter dans une approche min‐heap ou une recherche binaire sur des sommes possibles.

---

### Mise en oeuvre étape par étape (Java)

"Java
compte int publicPairs(Liste<Intéger> nombres, cible int) {
int n = nombres.size();
int[]a = nouvelle int[n];
pour (int i = 0; i < n; i++) a[i] = nums.get(i);
les tableaux.sort(a);

int gauche = 0, droite = n - 1, nombre = 0;
pendant que (à gauche < à droite) {
si ([à gauche] + [à droite] < cible) {
nombre += droite - gauche;
gauche++;
} autre {
droit...
}
}
le nombre de retours;
}
«» "

*Vous pouvez copier le code Java, l'exécuter sur le harnais de test de LeetCode, et la solution `O(n log n)` va gagner le badge . *

---

- Oui. Pourquoi ce problème est-il un «Show‐Stoppper» dans votre entrevue

- **Démontre les compétences classiques**: Tri + deux pointeurs → un agrafe dans la liste des astuces d'entretien -.
- **Scales to Larger Contraintes**: Si l'intervieweur change `n` à `105`, votre logique fonctionne encore et vous pouvez discuter d'une solution `O(n log n)`.
- ** Versatile pour la discussion**: Vous pouvez pivoter vers des problèmes connexes tels que le Sum de la paire Sums ou le Sum de la paire médiane.
- **Talk About Test‐Driven Development**: Rédigez quelques tests unitaires avant de coder – une habitude qui impressionne les ingénieurs seniors.

---

Pensées de clôture

LeetCode 2824 peut sembler trivial à première vue, mais c'est une **gold-mine** pour la préparation de l'entrevue. Maîtriser la méthode à deux points, savoir justifier sa justesse, anticiper les écueils de --bad, et apporter les points de discussion de --ugly--. Une fois que vous avez réussi ce problème, ajoutez une ligne à votre CV :

> **Code de leet isolé 2824 – Nombre de paires Dont la somme est inférieure à la cible** dans *Java, Python et C++* avec un algorithme optimal `O(n log n)`.

Cette petite ligne dit que vous pouvez *sortir, penser linéairement, et écrire du code propre* – exactement ce que veulent les intervieweurs. Bonne chance ! C'est ce qu'il a dit.

---

### Méta-information (pour référencement)

html
<title>LeetCode 2824 – Nombre de paires dont la somme est inférieure à la cible $ Java, Python, C++ Solutions</title>
<meta name="description" content="Solve LeetCode 2824 – Nombre de paires dont la somme est inférieure à la cible en utilisant l'algorithme à deux points optimal. Extraits de code Java, Python et C++, conseils d'entrevue et analyse de complexité.">
<meta name="keywords" content="LeetCode 2824, Nombre de paires dont la somme est inférieure à la cible, deux pointeurs, algorithme de tri, interview de codage, solution Java, solution Python, solution C++, prép d'entrevue d'algorithme, complexité de temps optimale, défi de codage d'entrevue">
«» "

---

Vite Référence : Extraits de code complet (copie-colle prêt)

Langue Fichier Fonction
- C'est quoi ?
*Java**= `Solution.java`= `Pairs (Liste <Integer> nums, cible int)=" Autres
**Python**== `solution.py=== `def countPairs(self, nombres: List[int], cible: int) -> int:===
**C++**="solution.cpp`="int countPairs(vecteur<int>& nums, cible int)=" Autres

N'hésitez pas à modifier le code pour votre environnement de codage préféré. Bon codage et bonne chance dans votre prochaine interview!