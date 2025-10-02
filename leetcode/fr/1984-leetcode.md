---
titre: LeetCode 1984. Différence minimum entre le plus haut et le plus bas des scores K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Ci-dessous sont trois implémentations propres et prêtes à la production de la différence minimale entre le plus haut et le plus bas des scores K (LeetCode 1984).
Les trois utilisent la même stratégie optimale – **sortez le tableau et glissez une fenêtre de taille k** – mais sont écrits en Java, Python et C++.

---

#### 1.1 Java 17

"Java
Importer java.util. Les tableaux;

solution de classe publique {
***
* Renvoie la différence minimale possible entre le plus haut
* et les scores les plus bas de tous les étudiants choisis.
*
* @param nombres de scores étudiants
* @param k nombre d'élèves à choisir
* @retour différence minimale
*/
Inf. public int minimumDifférence(int[] nombres, int k) {
si (k) 1) retour 0; // cas trivial
Tableaux.sort(nums); // O(n log n)

int best = entier.MAX_VALUE;
pour (int i = 0; i <= nombres.longueur - k; i++) {
Int diff = nombres[i + k - 1] - nombres[i];
si (diff < best) best = diff;
}
le meilleur retour; // O(n)
}

public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.minimumDifférence(nouvelle int[]{9,4,1,7}, 2)); // 2
}
}
«» "

---

#### 1.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minimumDifference(self, nombres: List[int], k: int) -> Int:
"""Retourne la différence minimale entre max et min de tous les scores k."""
Si k == 1:
retour 0

nombres.sort() # O(n log n)
meilleure = flotteur('inf')
pour i dans la plage (len(nums) - k + 1):
diff = nombres[i + k - 1] - nombres[i]
best = min(best, diff)
le meilleur retour # O(n)

♪ Démo
si __nom__ == "__main__" :
sol = Solution()
print(sol.minimumDifférence([9,4,1,7), 2) # 2
«» "

---

*## 1.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nt minimumDifférence(vecteur<int>& nombres, int k) {
si (k) 1) retourner 0;
(noms.begin(), nums.end()); // O(n log n)

int best = INT_MAX;
pour (int i = 0; i <= nums.size() - k; ++i) {
Int diff = nombres[i + k - 1] - nombres[i];
best = min (best, diff);
}
le meilleur retour; // O(n)
}
};

Int main() {
Solution s;
vecteur<int> v = {9,4,1,7};
<< s.minimumDifférence(v, 2) << '\n'; // 2
retour 0;
}
«» "

---

- Oui. 2. Article du blog – Différence minimale entre le plus haut et le plus bas des scores K : Le bon, le mauvais, le mauvais

2.1 Titre (optimisé par le référencement)

> **Différence minimale entre le plus haut et le plus bas des scores K – Solutions Easy Java, Python, C++ (LeetCode 1984)**

---

Introduction

Lors d'une entrevue pour des rôles d'ingénierie logicielle, les intervieweurs aiment les problèmes qui testent la capacité d'un candidat à raisonner sur les structures de données et la complexité algorithmique.
Code du leet 1984 – *Différence minimale entre le plus haut et le plus bas des scores de K* – est un tel problème de "easy" qui montre néanmoins la clarté, l'efficacité et la qualité du code.

Dans cet article, nous allons:

1. ** Expliquez le problème** en anglais.
2. Discutez des contraintes** qui façonnent notre approche.
3. Marchez à travers la solution **optimale** – tri + fenêtre coulissante – et pourquoi il gagne.
4. Afficher trois **implémentations idiomatiques complètes**: Java, Python, C++.
5. Mettre en avant le **bon, le mauvais, et le laid** des pièges communs.
6. Fournir **Balises de référence** afin que les recruteurs qui cherchent ce problème puissent trouver ce guide.

---

2.3 Réévaluation des problèmes

> **Input**: un tableau entier `nums` (`1 ≤ longueur nums ≤ 1000`, chaque élément `0 ... 105`) et un entier `k` (`1 ≤ k ≤ longueur nums`).
> **Tâche**: Choisissez les points `k` parmi `nums`. Parmi ces résultats `k`, calculez la différence entre le plus haut et le plus bas. Retourner la différence *minimum possible* réalisable par tout choix de scores `k`.

> **Exemples**
> * `nums = [90]`, `k = 1` → réponse `0`.
> * `nums = [9,4,1,7]`, `k = 2` → réponse `2` (pick `7` et `9`).

---

#### 2.4 Pourquoi la force brute droite s'affaiblit

Une solution naïve énumérerait chaque combinaison d'éléments `k` (`O(n choisissez k)`), calculerait le max/min pour chaque, et traquerait la meilleure différence.
Pour `n = 1000` et même modéré `k`, le nombre de combinaisons explose combinatoirement – clairement impossible pour l'interview ou le code de production.

Nous avons donc besoin d'un algorithme **polynomial-time**.

---

2.5 La stratégie optimale – Tri + Fenêtre coulissante

2.5.1 Intuition

Si le tableau est trié, tout groupe d'éléments consécutifs `k` aura une diffusion **minimale** parmi ce sous-ensemble : le premier élément est le plus petit, le dernier est le plus grand.
À l'inverse, tout groupe d'éléments "k" qui est **non consécutif** peut être "resserré" en échangeant un élément extrême contre un élément plus proche, n'augmentant donc jamais l'écart.

Donc :

1. **Trier** «nums» – «O(n log n)».
2. Faites glisser une fenêtre de taille `k` sur le tableau trié – `O(n)`.
Pour chaque fenêtre `i...i+k-1`, la différence est `nums[i+k-1] - nums[i]`.
3. Gardez la différence minimale rencontrée.

Cela donne une complexité globale **temps de `O(n log n)`** et **`O(1)` espace auxiliaire** (en ignorant les frais généraux de la bibliothèque de tri).

2.5.2 Cas de bord

Motifs
C'est pas vrai.
- Oui. 1 ''. Tout élément donne diff = 0.
Il faut prendre tous les éléments
Le tri les maintient ensemble ; les poignées de fenêtre duplicate automatiquement.

---

#### 2.6 Mise en oeuvre intégrale

##### 2.6.1 Java

*Utilise `Arrays.sort()` pour le tri en place et une simple boucle `pour` pour la fenêtre coulissante. *

"Java
nt minimumDifférence(int[] nombres, int k) {
si (k) 1) retourner 0;
Tableaux.sort(nums);
int best = entier.MAX_VALUE;
pour (int i = 0; i <= nombres.longueur - k; i++) {
best = Math.min(meilleur, nombres[i + k - 1] - nombres[i]);
}
le meilleur retour;
}
«» "

##### 2.6.2 Python

*Traitement de la liste des leviers et d'une boucle de portée `pour`. *

'`python
def minimumDifférence(nombres: List[int], k: int) -> Int:
Si k == 1:
retour 0
nombres.sort()
meilleure = flotteur('inf')
pour i dans la plage (len(nums) - k + 1):
best = min(meilleur, nombres[i + k - 1] - nombres[i])
le meilleur retour
«» "

2.6.3 C++

*Utilise `std::sort` et une boucle `pour` classique. *

'`cpp
nt minimumDifférence(vecteur<int>& nombres, int k) {
si (k) 1) retourner 0;
(noms.begin(), nums.end());
int best = INT_MAX;
pour (size_t i = 0; i + k <= nums.size(); ++i) {
best = min(meilleur, nombres[i + k - 1] - nombres[i]);
}
le meilleur retour;
}
«» "

Les trois implémentations s'exécutent dans l'espace supplémentaire "O(n log n)" et "O(1)".

---

2.7 Bien, mal, Méchant

Aspect du bien
- C'est quoi ?
**Complexité temporelle**= Tri + fenêtre = `O(n log n)` (optimal)== Brute-force `O(n choose k)` – impraticable=== Aucun – algorithme est simple===
**Readability**
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**L'espace**= Tri en place, `O(1)` auxiliaire==Construire toutes les combinaisons → `O(nCk)` mémoire=== Aucune=
**Maintenabilité**= Commentaires, style cohérent== Conventions de noms mixtes==Notes surcommentées ou redondantes==

Pièges communs

- **Off‐by‐one** dans la boucle coulissante de la fenêtre ('i <= nums.longueur - k').
- **Débordement entier**: Utilisez `int` pour les scores jusqu'à `10^5` mais gardez à l'esprit `nums[i+k-1] - nums[i]` correspond toujours à `int`.
- **Ignorer les cas triviaux**: `k==1` donne toujours `0`; le retour anticipé permet d'économiser du temps.

---

#### 2.8 Métadonnées de référence (pour les recruteurs)

Autres Valeur de Meta Tag
C'est quoi ?
**Titre**= Différence minimale entre les scores K les plus élevés et les plus bas – Solutions Easy Java, Python, C++ (LeetCode 1984)=
**Description**= Apprenez à résoudre le LeetCode 1984 en Java, Python et C++. Comprendre la stratégie de tri + fenêtre coulissante, la complexité du temps, les cas de bord et les conseils d'entrevue. Autres
LeetCode 1984, différence minimale entre le plus haut et le plus bas des scores K, solution Java, solution Python, solution C++, fenêtre coulissante, tri, interview par algorithme, structures de données, entretien d'emploi, défi de codage

---

2.9 Conclusion

LeetCode 1984 est un test d'entrevue classique** de :

1. **Compréhension des problèmes** – choix de la sous-tribu.
2. **La pensée algorithmique** – reconnaître le tri + fenêtre comme le modèle optimal.
3. **Codage propre** – mise en œuvre avec clarté et manipulation des cas bord gracieusement.

Les trois implémentations ci-dessus devraient bien vous servir dans les entrevues de codage et les bases de code du monde réel.
Ajoutez l'article à votre portfolio, partagez-le sur LinkedIn et étiquetez-le avec les métadonnées SEO afin que les recruteurs qui cherchent ce problème exact le voient.

> Codage heureux !

---

*Vous pouvez télécharger gratuitement les extraits de code source complets ou les adapter à votre langue préférée. *