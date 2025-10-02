---
titre: LeetCode 1133. Le plus grand numéro unique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1133. Numéro unique le plus grand
Solutions C++ + SEO-Optimized Blog Post

---

- Oui. 1. Référence de code rapide (trois langues)

"Java
// - Oui. Java - Oui.
Importation de java.util.*;

solution de classe {
Nombre(int[] nombres) {
Carte<integer,integer> freq = nouveau HashMap<>();
pour (int n : nombres) freq.merge(n, 1, entier::sum);

int ans = -1;
pour (Map.Entry<Integer,Integer> e : freq.entrySet() {
i (e.getValue() == 1 && e.getKey() > ans) ans = e.getKey();
}
le retour des an;
}
}
«» "

'`python
♪ - Oui. Python...
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
plus UniqueNumber(self, nombres: List[int]) -> Int:
freq = compteur(s)
as = -1
pour num, cnt en fréq.item():
i cnt == 1 et num > ans:
ans = nombre
retour et
«» "

'`cpp
// C++ - Oui.
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
la plus grande Numéro Unique(vecteur<int>& nums) {
unordered_map<int,int> freq;
pour (int n : nombres) ++freq[n];

int ans = -1;
pour (auto &p : freq)
si (p.second == 1 && p.first > ans) ans = p.first;
le retour des an;
}
};
«» "

> **Complexité temporelle**: `O(n)` – un passage pour compter, un passage sur la carte.
> **Complexité spatiale**: `O(n)` – au plus une entrée par élément unique.

---

- Oui. 2. Article de blog optimisé SEO

Titre
Code de sortie 1133 – Numéro unique le plus grand: Solutions Java, Python & C++, Analyse de l'espace temporel et Conseils d'entrevue *

---

Description de la méta
Découvrez le moyen le plus rapide de résoudre le LeetCode 1133 en Java, Python et C++. Comprendre l'algorithme, explorer d'autres solutions et apprendre des astuces pour impressionner les gestionnaires d'embauche.

---

Table des matières
1. Déclaration de problème
2. Contraintes et cas de bord
3. L'approche directe de la carte Hash
4. Variante: Tri de comptage (Lorsque 0 ≤ nums[i] ≤ 1000)
5. Analyse des performances (temps et espace)
6. Pièges communs & Le Ugly
7. Conseils d'entrevue et points de discussion
8. Autres lectures et ressources

---

2.1 Énoncé du problème

**LeetCode 1133 – Le plus grand nombre unique**

> Compte tenu d'un nombre entier, retourner le nombre ** le plus grand entier qui ne se produit qu'une seule fois**.
> Si aucun entier ne se produit qu'une seule fois, retourner `-1`.

Exemples
Entrée Sortie Explication
C'est pas vrai.
`[5,7,3,4,9,8,3,1]`" `8`" `9` répète, `8` est le plus grand nombre unique. Autres
Tous les nombres se répètent. Autres

---

2.2 Contraintes et causes de bord

Pourquoi ça compte ?
- C'est quoi ?
"1 <= nums.longueur <= 2000"" Petite" Brute-force toujours viable, mais la carte de hachage est propre. Autres
`0 <= nums[i] <= 1000`-Limité= Autorise l'optimisation de la composition. Autres
Nombres négatifs? Non, simplifie le comptage par tableau. Autres
Autres Tous les doublons ? Il faut retourner `-1`. Autres
Autres Tout est unique ? Revenir à l'élément max. Autres

---

2.3 L'approche directe de la carte Hash

Pourquoi ça marche ?

1. **Compte de fréquence** – Cartez chaque valeur à combien de fois elle apparaît.
2. **Scan pour le plus grand Unique** – Itérer à travers la carte; garder la clé maximale dont le nombre est `1`.

Code Pseudo étape par étape

«» "
fonction la plus grande Numéro(s) unique(s) :
freq = carte de hachage vide
pour num in nums:
freq[num] = freq.get(num, 0) + 1

as = -1
pour (num, nombre) en freq:
1 et num > ans:
ans = nombre
retour et
«» "

Faits saillants de la mise en oeuvre

Mots clés Autres
- C'est quoi ?
**Java**"merge()" simplifie le comptage" `freq.merge(n, 1, entier::sum);"
**Python**="Counter" de `collections`= `freq = Counter(nums)` Autres
*C++**= `unordered_map`= `++freq[n];` Autres

---

2.4 Alternative : Tri de comptage (Lorsque 0 ≤ nums[i] ≤ 1000)

Parce que chaque élément est limité par `1000`, nous pouvons utiliser un tableau de taille `1001` pour compter les fréquences dans **O(n)** temps **et** **O(1)** espace supplémentaire.

'`python
Numéro(s) unique(s):
Nombre = [0] * 1001
pour n en nombres:
Nombre[n] += 1
pour i dans la fourchette(1000, -1, -1):
si vous comptez[i] 1 :
retour
retour -1
«» "

**Pour**
- Accès au réseau à temps constant.
- Pas de plan.

**Cons**
- Nécessite une connaissance des limites de valeur.
- La mémoire gâchée si les limites sont énormes.

---

2.5 Analyse du rendement

L'approche Temps Espace Qualité
- C'est quoi ?
Hash-Map () "O(n)" "O(u)" ("u" = valeurs uniques)" Cas général, gère les valeurs négatives. Autres
Calcul de la répartition "O(n)" "O(1)" (fixé 1001)" Optimisé lorsque les limites sont serrées et connues. Autres
Brute-Force Acceptable pour `n <= 2000`, mais plus lentement. Autres

---

## 2.6 Pièges communs & #=L'Ugly

Erreurs dans les résultats
- C'est quoi ?
**En utilisant `HashMap` mais en oubliant de gérer les duplicatas** 1» avant la mise à jour «ans». Autres
**Returning `0` when all numbers are duplicata**= Mauvaise réponse== Initialiser `ans = -1` (par spec). Autres
**Itération dans l'ordre arbitraire (par exemple, `pour (clé int : freq.keySet()') et ne pas comparer avec `ans`**. lorsque "compte " 1'. Autres
**Utiliser `ArrayList` de `Integer` pour compter au lieu de `int[]`**. Autres
** Supposons que l'entrée s'inscrit dans `int` lors de l'utilisation de `long`**. Autres

---

2.7 Conseils et points d'entrevue

1. **Clarifier les contraintes** – Demandez si les valeurs peuvent être négatives ou si les limites sont fixées.
2. **Exposer la complexité tôt** – Afficher le temps "O(n)" et l'espace "O(n)".
3. **Discuss Edge Cases** – Tous les doublons, tous les éléments uniques.
4. **Afficher les échanges** – Hash-map vs computing array.
5. **Réutilisabilité du code des peines** – La même logique peut être adaptée au plus grand nombre qui apparaît exactement k fois.

---

2.8 Lecture et ressources supplémentaires

- Problème de LeetCode : [Plus grand numéro unique](https://leetcode.com/problèmes/plus grand numéro unique/)
- Thème de discussion : Meilleure solution pour LeetCode 1133 – idées évaluées par la communauté.
- HashMap vs HashTable – Comprendre Collections Java.
- C'est un coup de comte. Pourquoi c'est linéaire pour les entiers limités.

---

- Oui. 3. Pensées finales

Solving LeetCode 1133 est un excellent démarreur d'entrevue qui vous apprend à:

- Utilisez des tables de hachage pour compter la fréquence.
- Optimiser avec le tri de comptage lorsque les contraintes le permettent.
- Traduire un algorithme concis en code Java, Python ou C++.

Que vous soyez en train de préparer un pipeline d'embauche dans une grande entreprise de technologie ou une startup, le modèle du filtre → de nombre → maximiser est largement applicable. Gardez le code simple, les commentaires clairs et toujours vérifier les cas de bord. Bonne chance pour votre prochain entretien de codage !

---