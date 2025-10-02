---
titre: LeetCode 2841. Somme maximale de presque unique Subarray -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

**LeetCode 2841 – Maximum Somme d'un sous-array presque unique* *

> Vu un nombre entier et deux nombres entiers positifs `m` et `k`,
> retourner la somme maximale de tout subarray contigu de longueur `k` qui
> contient **au moins `m` valeurs distinctes**.
> S'il n'existe pas de subarray, retourner `0`.

*Contrôles*

«» "
1 ≤ longueur nominale ≤ 20 000
1 ≤ m ≤ k ≤ nums. longueur
1 ≤ nums[i] ≤ 10^9
«» "

---

- Oui. 2. Idée de haut niveau

* La longueur subarray est fixe (`k`), de sorte qu'un classique ** glisse-fenêtre** de la taille `k`
est un ajustement naturel.
* Alors que la fenêtre glisse, nous devons savoir:
* la somme actuelle de ses éléments – un seul total courant,
* le nombre d'éléments **distincts** à l'intérieur – une carte de fréquence (`HashMap` / `unordered_map` / `dict`).

Lorsque la fenêtre atteint la taille requise:

«» "
si (distinctCount ≥ m) // fenêtre est presque unique
best = max(meilleur, courantSum)
«» "

Ensuite, nous décalons la fenêtre d'une étape vers la droite en supprimant l'élément le plus à gauche et
ajouter l'élément suivant, mettre à jour la carte, le compteur distinct et la somme en O(1).

Toute la procédure est linéaire : chaque élément entre et quitte la fenêtre une fois.

---

- Oui. 3. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Autres Glissement de tous les éléments `n`
Mises à jour de la carte (constante moyenne)
Dans l'ensemble **O(n)**

`k ≤ n`, donc l`algorithme est bien dans les limites.

---

- Oui. 4. Mise en œuvre des références

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

---

#### 4.1 Java

"Java
Importer java.util. HashMap;
Importer java.util. Liste;

solution de classe publique {
***
* Renvoie la somme maximale d'un sous-array presque unique de longueur k.
* @param nums Liste des entiers (indices basés sur le nombre autorisé)
* @param m Nombre minimal d'éléments distincts requis
* @param k Longueur de la sous-tribu
* @retour somme maximale possible ou 0 si aucune sous-tribution valide n'existe
*/
public long maxSum(Liste<entier> nombres, int m, int k) {
// Carte de fréquence pour la fenêtre actuelle
HashMap<entier, entier> freq = nouveau HashMap<>();

long best = 0; // meilleure somme trouvée jusqu'à présent
long curSum = 0; // somme des éléments dans la fenêtre actuelle
int distinct = 0; // nombre d'éléments distincts dans la fenêtre

int gauche = 0; // pointeur gauche de la fenêtre coulissante
int droite = 0; // pointeur droit (exclusif)

int n = nombres.size();

pendant que (droite < n) {
// Étendre la fenêtre à droite jusqu'à atteindre la taille k
pendant que (droite < n & & droite - gauche < k) {
int val = nums.get(à droite);
freq.merge(val, 1, entier::sum);
si [freq.get(val)] 1) distinct++; // nouvel élément distinct
curSum += valeur;
droite++;
}

// Fenêtre est maintenant de taille k (sauf si nous avons atteint la fin)
si (droite - gauche) {
best = Math.max (best, curSum);
}

// Retirez-vous de la gauche pour déplacer la fenêtre vers l'avant
int leftVal = nums.get(gauche);
freq.put(leftVal, freq.get(leftVal) - 1);
si (freq.get(leftVal)) 0) {
freq.remove(leftVal);
distincte--;
}
curSum -= gauche Val;
gauche++;
}

le meilleur retour;
}
}
«» "

---

4.2 Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxSum(self, nombres: List[int], m: int, k: int) -> Int:
freq = defaultdict(int)
distinct = 0
cur_sum = 0
meilleur = 0

gauche = 0
n = len(nums)

pour droite à portée(n):
val = nombres[droite]
si freq[val] == 0:
distinct += 1
freq[val] += 1
cur_sum += valeur

# Une fois que la fenêtre atteint la taille k, nous vérifions, puis glissez à gauche
Si droite - gauche + 1 == k:
si distinct >= m:
best = max(best, cur_sum)

# Supprimer l'élément le plus à gauche
gauche_val = nombres[gauche]
freq[left_val] -= 1
si freq[left_val] == 0:
distinct -= 1
cur_sum -= gauche_val
gauche += 1

le meilleur retour
«» "

---

### 4.3 C++

'`cpp
#incluez <vecteur>
#inclut <non-ordonné_map>
#incluez <algorithme>

solution de classe {
public:
long long maxSum(suite std::vector<int>& nums, int m, int k) {
std::unordered_map<int, int> freq; // element -> Nombre
Int distinct = 0;
long curSum = 0, meilleur = 0;

Int gauche = 0;
pour (int right = 0; right < static_cast<int>(nums.size()); ++right) {
int val = nombres[droite];
si (freq[val]] 0) ++ distinct;
++freq[val];
curSum += valeur;

// Lorsque la taille de la fenêtre est k nous pouvons évaluer et glisser
si (droite - gauche + 1 == k) {
si (distinct >= m) mieux = md::max(meilleur, curSum);

// Diapositive gauche
Int gauche Val = nombres[gauche];
--freq[leftVal];
si (freq[leftVal]) 0) --distinct;
curSum -= gauche Val;
+ + gauche;
}
}
le meilleur retour;
}
};
«» "

---

- Oui. 5. Billet de blog – Le bon, le mauvais, et le mauvais de LeetCode 2841

### 5.1 Titre & Méta‐Description (SEO)

**Titre**
> LeetCode 2841 : La somme maximale d'un subarray presque unique – Une classe de maître de la fenêtre coulissante

**Méta—Description**
> Débloquez les secrets de LeetCode 2841 avec une solution de fenêtre coulissante étape par étape en Java, Python & C++. Apprenez les compromis, les pièges et comment ce problème peut impressionner les gestionnaires d'embauche.

5.2 Introduction

> **Pourquoi ce problème est important. **
> Beaucoup d'entretiens vous demandent de combiner *deux* techniques classiques: fenêtres coulissantes et comptage de fréquence. Mastering LeetCode 2841 montre non seulement vos côtelettes algorithmiques, mais aussi votre capacité à gérer des compromis entre le temps et l'espace**, une compétence standard pour les ingénieurs logiciels.

5.3 La bonne – Pourquoi la fenêtre coulissante gagne

Caractéristique Explication
C'est pas vrai.
Chaque élément est traité une fois. Autres
**Simple structures de données**= Une somme courante, une carte non ordonnée et un compteur. Pas de cadres lourds. Autres
**Mémoire prédictible**= Au plus `k` touches distinctes, `O(k)` espace. Fonctionne même pour "nums.length = 20 000". Autres

> Dans les interviews, une solution propre de fenêtre coulissante indique que vous pouvez **optimiser** tôt, les recruteurs de caractères aiment.

5.4 Les mauvaises – Pièges communs

Symptômes Correction
C'est pas vrai.
Autres Oublier de rétrécir la fenêtre. Erreur d'exécution ou mauvaise réponse. Autres
Autres Utilisation d'un vecteur pour la fréquence sur une large gamme de fréquences Autres
Défaut de traiter `m > cas distinct`. Autres

> Une petite surveillance sur le compteur distinct ou la taille de la fenêtre peut faire votre solution **O(n2)** ou même **TLE**.

5.5 Les horribles cas que vous ne pouvez ignorer

Un cas d'Edge
- C'est quoi ?
Une seule fenêtre; doit toujours vérifier `m` Pas de boucle; juste évaluer une fois. Autres
- Oui. 1 ''. Toute fenêtre fonctionne. Autres
Autres Très grand `nums[i]` (= 109)= Somme déborde 32 bits== Utiliser un entier 64 bits (=`long`, `long long`, `int64_t`). Autres
Résultat vide Aucun subarray ne rencontre `m`. Autres

> Les intervieweurs injectent souvent ces cas subtils pour tester la robustesse.

#### 5.6 Le départ – Comment réussir l'entrevue

1. **Commencez avec la force brute** (O(n·k)) pour démontrer votre compréhension.
2. **Expliquez l'intuition de la fenêtre coulissante**: longueur fixe.
3. **Afficher le compteur distinct basé sur la carte** et pourquoi `unordered_map` est la clé.
4. **Va à travers la ligne de code par ligne**, en particulier l'étape de rétrécissement de la fenêtre.
5. **Réponse : Par exemple, et si tous les nombres sont les mêmes? (en milliers de dollars)

> Un modèle mental clair et une mise en œuvre soignée vous valent le clin d'œil de l'intervieweur.

5.7 Conclusion

LeetCode 2841 est un **spot sucré**: pas trop dur, mais assez riche pour afficher la maturité algorithmique.
En maîtrisant le motif de la fenêtre coulissante, vous serez équipé pour une foule de problèmes similaires:`Sliding Window Maximum`, `Longest Substring with K Distinct`, `Subarray Sum Equals K`, etc.

> **Conseil :** Gardez les trois implémentations à portée de main. Ils sont parfaits pour une vitrine rapide de portfolio ou un message de codage-blog. Et oui, copiez le code dans votre CV - - Projects si le travail nécessite Java, Python ou C++.

5.8 Réflexions finales

- **Pratique** le modèle sur d'autres problèmes de la taille de la fenêtre.
- **Lire** les solutions éditoriales officielles et comparer les compromis.
- **Partager** vos solutions sur GitHub; inclure des tests unitaires pour les cas de bord.

Bonne chance ! Si vous avez frappé la partie --good-- de ce post, vous allez non seulement résoudre 2841 mais aussi impressionner les gestionnaires d'embauche qui apprécient **efficacité, clarté et résilience**.

---

- Oui. 6. À propos de l'auteur

> *[Votre nom]* – Ingénieur en logiciel, Algorithme Enthousiaste
> 3+ années d'expérience avec Java & Python, interviewé chevronné, et blogueur.

---

**Codage heureux!**