---
titre: LeetCode 719. Trouvez K-th Distance de la paire la plus petite -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Trouvez la plus petite distance de la paire K – LeetCode 719
*Pouvoir* DistancePaire(int[] nombres, int k) "

> **Objectif** – Retourner la plus petite différence absolue entre deux éléments dans le nombre.
> **Input** – «nums» (longueur 2 ≤ n ≤ 104, 0 ≤ nums[i] ≤ 106), «k» (1 ≤ k ≤ n(n‐1)/2).
> **Output** – La plus petite distance de la paire `k`.

Les sections suivantes portent sur:

1. Aperçu du problème
2. L'algorithme optimal (recherche binaire sur la distance + fenêtre coulissante)
3. Mise en œuvre en **Java**, **Python 3**, **C++**
4. Cas de bord et pièges communs
5. Tant mieux. Ugly – une liste de contrôle rapide de révision de code
6. SEO-friendly à emporter pour les chasseurs d'emploi

---

- Oui. 1. Aperçu du problème

La voie de force brute générerait toutes les distances de paires \(\binom{n}{2}\), les trierait et retournerait l'élément \(k\)‐th.
*Time* – \(O(n^2 \log n)\) → beaucoup trop lent pour \(n=104\).
*Espace* – \(O(n^2)\) pour stocker toutes les distances → impossible.

Nous avons besoin d'une solution **\(O(n \log M)\)** où \(M\) est la distance maximale possible (\(\max(nums)-\min(nums)\)).
L'astuce est de ** chercher sur la réponse** (la distance) et compter combien de paires ont une distance ≤ milieu.
Si ce nombre est < k, nous avons besoin d'une plus grande distance; sinon nous pouvons essayer une plus petite.

---

- Oui. 2. Approche optimale – Recherche binaire + Deux-Pointeurs

1. **Trier le tableau – \(O(n \log n)\).
2. Recherche binaire sur la distance `d` dans la plage `[0, max‐min]`.
3. Pour un candidat `mid`, compter les paires `(i, j)` avec `nums[j] - nums[i] ≤ mi` en utilisant une fenêtre coulissante (deux-pointeurs).
* `gauche` commence à 0.
* Pour chaque `droit` de 0 à n‐1, incrément `gauche` alors que la largeur de la fenêtre dépasse `mid`.
* Tous les indices entre `left` et `right-1` forment des paires valides avec `right`. Ajouter `à droite` au compte.
* Ceci est linéaire, \(O(n)\).
4. Ajuster les limites de recherche binaire en fonction du nombre.
5. Retourner la plus petite distance dont le nombre ≥ k.

**Pourquoi ça marche* *
- Oui. Le tableau est trié, de sorte que toute paire valide avec la distance ≤ `mid` est contigu dans l'ordre trié.
- Oui. La fenêtre coulissante compte chaque paire exactement une fois.
- La recherche binaire garantit que nous convergeons à la distance minimale qui satisfait la condition.

---

- Oui. 3. Mise en œuvre du code

#### 3.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
publique DistancePaire(int[] nombres, int k) {
Tableaux.sort(nums); // 1. trier
int low = 0; // distance minimale possible
int high = nombres[nums.longueur - 1] - nombres[0]; // distance maximale possible

pendant que (faible < haut) {
int milieu = faible + (élevé - faible) / 2;
nombre long = nombrePairs(nombres, milieu); // 2. paires de nombre <= mi

si (compte < k) { // besoin d ' une plus grande distance
faible = milieu + 1;
} autre { // mi est suffisant
haute = moyenne;
}
}
retour bas; // distance minimale avec nombre >= k
}

// Compte linéaire à deux points (utilise longtemps pour éviter le débordement)
compte long privéPairs(int[] nombres, limite int) {
longue cnt = 0;
Int gauche = 0;
pour (int droite = 0; droite < nums.longueur; droite++) {
pendant que (nums[right] - nombres[left] > limite) {
gauche++;
}
cnt += droite - gauche; // paires (gauche ... droite-1, droite)
}
retour cnt;
}
}
«» "

> **Pourquoi 64 bits? * *
> Le nombre de paires peut être jusqu'à \(\frac{10^4 \times 999}{2} \approx 5\times10^7\), correspond toujours à `int`.
> Utiliser `long` est un choix défensif lorsqu'il s'étend à `n' plus grand.

---

3.2 Python 3

'`python
Solution de classe:
def le plus petit DistancePair(self, nombres: list[int], k: int) -> Int:
nombres.sort() # 1. En quelque sorte
faible, élevé = 0, nombres[-1] - nombres[0] # plage de recherche

alors que faible < élevé:
milieu = (faible + élevé) // 2
if self.count_pairs(nums, mi) < k: # besoin d'une plus grande distance
faible = milieu + 1
Sinon : # mi-travail
haute = moyenne
retour faible

def count_pairs(self, nombres: list[int], limite: int) -> Int:
"""Nombre linéaire à deux points de paires avec distance <= limite."""
gauche, cnt = 0, 0
pour droite, val in énumérate(nums):
alors que val - nombres[gauche] > limite:
gauche += 1
cnt += droite - gauche
retour cnt
«» "

---

### 3.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int plus petite DistancePaire(vecteur<int>& nums, int k) {
tri(nums.begin(), nums.end()); // 1. tri
= 0;
int high = nums.back() - nums.front(); // 2. limites de recherche

pendant que (faible < haut) {
int milieu = faible + (élevé - faible) / 2;
long long cnt = nombre Paires(nombres, milieu); // 3. paires de nombre <= milieu

si (cnt < k) {
faible = milieu + 1;
} autre {
haute = moyenne;
}
}
retour faible; // 4. réponse
}

particulier:
// Nombre linéaire à deux points
long comptePairs(vecteur const<int>& nums, limite int) {
long cnt = 0;
Int gauche = 0;
pour (int right = 0; right < (int)nums.size(); ++right) {
pendant que (nums[right] - nombres[left] > limite) {
+ + gauche;
}
cnt += droite - gauche; // tous i dans [gauche, droite-1] forment une paire valide avec droite
}
retour cnt;
}
};
«» "

> Les trois solutions ont la même complexité temps/espace:
> **Heure**: \(O(n \log n + n \log M)\)
> **Espace**: \(O(1)\) outre le tableau d'entrée (le genre est en place).

---

- Oui. 4. Cas de bord et pièges communs

Scénario Qu'est-ce qu'il faut vérifier ?
- C'est quoi ?
Les nombres dupliqués "bas" commencent à 0; comptePairs retournera de nombreuses paires de distance zéro. L'algorithme trouve toujours la plus petite distance non négative. Autres
Autres Très grand `k` (proche de \(n(n-1)/2\)) ► La recherche binaire se termine par `faible=élevée=max-min`. Autres
Le tri est obligatoire, sinon la logique de la fenêtre coulissante échoue. Rappelez-vous d'appeler `Arrays.sort` / `sort(nums)` avant la recherche binaire. Autres
Autres Utiliser `long` / `long long` pour le comptage. Autres
Des chiffres négatifs ? Le problème garantit non-négatif, mais si vous vous étendez aux négatifs, `nums[right] - nums[left]` fonctionne toujours parce que le tableau est trié. Pas besoin de changement. Autres

---

- Oui. 5. Bon, mauvais, mal – Liste de contrôle de l'examen rapide du code

Aspect du bien
- C'est quoi ?
**Traitement**=Utilisez le tri intégré et efficace (`Arrays.sort` / `sort`)=Utiliser pour trier les casses de l'algorithme==Utiliser un énorme flux de données (par exemple, utiliser `Collections.sort` sur une liste d'objets)=
**Binary search limits**= correct `low = 0`, `high = max‐min`== Utiliser `high = max(nums)` au lieu de `max‐min` gonfle l'espace de recherche== Off‐by‐one: `int mid= (low + high)/2` sans empêcher le débordement==
**Fonction de comptage**=Deux-pointeurs linéaires, pas de mémoire supplémentaire==Défaut d'incrémenter la `gauche` ou d'oublier la `gauche-droite'==Paires de comptage deux fois ou deux paires manquantes (par exemple, en utilisant la `gauche-droite+1`) Autres
**Valeur de retour**= `low` après la boucle – distance minimale avec le nombre ≥ k== Retour `high` incorrectement== Retour `mid` à l'intérieur de la boucle (arrêt trop tôt)=
En supposant que `int` est suffisant → nombre entier de conversions "non signées" inutiles (en code C++)

---

- Oui. 6. Alternatives et pourquoi nous choisissons celui-ci

Démarche Complexité
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**K-th order statistic + min-heap** , \(O(n^2 \log k)\) , Fonctionne pour les petits `n` , toujours quadratique
**FFT + tableau de fréquences**.
**Recherche binaire + recherche binaire par élément**

Pour LeetCode 719, la méthode binaire-recherche-sur-réponse est la solution *de facto*.

---

- Oui. 7. SEO-Friendly Take-Away – Ce que les gestionnaires d'embauche aiment

- **Mot-clé**: *K-th plus petite distance de paire LeetCode 719*
- **Méta-Description** (155 caractères)
> Solution de LeetCode 719 – recherche binaire sur la distance + fenêtre coulissante à deux points. Code O(n log M) en Java, Python, C++. Guide de préparation à l'entrevue et de recherche d'emploi. (en milliers de dollars)
- **En-têtes**:
- "# Trouvez la K-th la plus petite distance de paire – LeetCode 719`
- Oui. Algorithme optimal: Recherche binaire + fenêtre coulissante`
- Oui. Java / Python / C++ Code "
- Oui. Bon, mauvais, mauvais – Liste de contrôle du code d'entrevue "

> **Pourquoi c'est important** – Les recruteurs cherchent le code 719 pour trouver des candidats capables de résoudre des problèmes de traitement de réseau dur.
> Inclure les mots-clés ci-dessus dans le titre de votre blog, le premier paragraphe et la méta-description pour classer plus haut dans les requêtes de recherche d'emploi.

---

Mot final

- Le modèle **binary search over reply** est un outil puissant pour résoudre les problèmes de petite taille.
- Gardez votre fonction **count** linéaire; la fenêtre coulissante est à la fois *fast* et *clean*.
- Oui. N'oubliez pas d'utiliser **`long`** pour le nombre de paires.
- Oui. L'algorithme fonctionne confortablement pour les contraintes maximales (104 éléments).

Déposez ce post dans votre portfolio, modifiez les commentaires pour votre style, et appuyez sur "Publier"! Bonne chance pour l'entrevue.