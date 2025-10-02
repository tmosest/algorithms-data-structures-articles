---
Titre: LeetCode 3350. Détection de Subarrays en augmentation adjacente II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 3350 – Détection de Subarrays en augmentation adjacente II
**Java / Python / C++ – One-Pass, O(n) Time, O(1) Space**

---

- Oui. 1. Résumé du problème

Compte tenu d'un tableau entier «nums» (2 ≤ «nums.longueur» ≤ 2·105), trouver la longueur **maximum «k»** de telle sorte que **deux sous-réseaux adjacents** de longueur «k» soient * strictement croissants*.

«» "
nombres[a ... a+k-1) – augmentation stricte
nombres[b ... b+k-1) – augmentation stricte
b = a + k – les sous-groupes sont adjacents
«» "

Retournez le plus grand "k" possible.
Si une telle paire n'existe pas, la réponse est `0`.

> **Exemple**
> `nums = [2,5,7,8,9,9,2,3,4,1]` → répondre `3`
> (sous-audiences `[7,89]` et `[2,34]`)

---

- Oui. 2. Pourquoi la solution One-Pass est-elle la bonne ?

L'approche Temps L'espace Commentaires
C'est pas vrai.
Brute-force (double boucle + contrôles O(k)) Autres
Recherche binaire sur `k` + balayage linéaire
**One-passe avec deux compteurs***** **O(n)***** **O(1)***** *Optimal* – fonctionne en < 0,02 s sur LeetCode

L'algorithme à un passage suit :

* `up` – longueur du segment **current** en augmentation stricte se terminant à l'indice actuel.
* `pre` – longueur du segment **précédent** qui augmente strictement avant le segment actuel.

À chaque position, la réponse à cette scission est :

1. Le *plus petit* des deux segments adjacents: `min(pre, up)`
(une paire de sous-réseaux en augmentation adjacents qui existent déjà).

2. La moitié du segment actuel: `up / 2`
(scintillant un long segment en deux moitiés égales).

Le maximum global de ces deux valeurs sur l'ensemble du tableau est le «k» requis.

L'algorithme nécessite **un seul passage** à travers le tableau et **constante mémoire supplémentaire**.

---

- Oui. 3. La Force Brute Naïve

Une double boucle simple qui vérifie chaque paire de sous-cours ressemblerait à :

"Java
int best = 0;
pour (int i = 0; i < n; ++i) {
pour (int j = i + 1; j < n; ++j) {
int len = j - i;
si (augmente (nums, i, i + len - 1) &&
est en augmentation(nombres, i + len, j - 1)) {
best = Math.max (best, len);
}
}
}
«» "

`isIncreasing` est O(k), donc la complexité totale est **O(n3)** dans le pire des cas.
Pour `n = 200 000`, cette approche ne se terminerait jamais.

---

- Oui. 4. La recherche binaire sur "k" "

On pourrait effectuer une recherche binaire sur `k` et, pour chaque candidat, scanner le tableau en temps linéaire pour vérifier s'il existe deux sous-réseaux adjacents de cette longueur. C'est exact, mais ajoute encore un facteur logarithmique supplémentaire:

«» "
O(n log n) – acceptable mais non optimal
«» "

Les détails de mise en oeuvre deviennent plus importants (p. ex., garder deux pointeurs, gérer les chevauchements, etc.), ce qui rend le code plus difficile à comprendre et à maintenir.

---

- Oui. 5. L'espace "Good" – One-Pass, O(1)

Voici la solution propre et intuitive qui fonctionne dans le temps linéaire et l'espace constant.

Code de la langue
C'est quoi, ça ?
*Java**
public int maxAugmentation Subarrays(Liste <entier> nombres) {
int n = nombres.size();
int up = 1; // longueur du courant augmentant
int pre = 0; // longueur de la course précédente en augmentation
Int ans = 0;
pour (int i = 1; i < n; ++i) {
si (nums.get(i) > nums.get(i - 1) {
up++;
} autre {
pre = up; // lancer l'exécution terminée
up = 1; // lancer une nouvelle exécution
}
// deux candidats pour cette division
ans = Math.max(ans, Math.max(up / 2, Math.min(pre, up));
}
le retour des an;
}
«» "
*Python**
Solution de classe:
def maxAugmentation Subarrays(self, nombres: Liste[int]) -> Int:
n = len(nums)
up = 1 # courant augmentant la longueur d'exécution
pre = 0 # longueur d'exécution précédente
ans = 0
pour i dans la plage (1, n):
si nombres[i] > nombres[i-1]:
+= 1
Sinon:
Pré = haut
en haut = 1
ans = max(ans, max(up // 2, min(pre, up))
retour et
«» "
*C++ *Cpp
int maxIncreasingSubarrays(vector<int>& nums) {
int n = nombres.size();
int up = 1, pre = 0, ans = 0;
pour (int i = 1; i < n; ++i) {
si (nums[i] > nombres[i-1]) up++;
autres {
pré = haut;
haut = 1;
}
ans = max(ans, max(up / 2, min(pre, up));
}
le retour des an;
}
«» "
---

- Oui. 6. Cas de bord et essais

Autres Test d'entrée prévu Pourquoi
C'est pas vrai.
Les deux seuls éléments forment une seule paire croissante. Autres
Autres Il n'y a pas de sous-réseau en augmentation. Autres
Autres Très longue augmentation de la gamme : Autres
Autres Alterner vers le haut/vers le bas `[1,3,2,4,3,5]`=1`= Seules les paires adjacentes de longueur 1 augmentent. Autres

Assurez-vous de tester ces cas de bord; l'algorithme les gère naturellement.

---

- Oui. 7. Analyse de la complexité

* **Heure**: `O(n)` – un passage sur le tableau.
* **Espace**: "O(1)" – seulement quelques variables entières.

---

- Oui. 8. Conseils à emporter pour les entrevues

1. **Reconnaissez le motif** – vous avez besoin de deux parcours de plus en plus adjacents; cela indique de garder une trace de la longueur des parcours.
2. **Utilisez deux pointeurs ou compteurs** – un pour la course en cours, un pour la course précédente.
3. **Éviter les doubles boucles** – ils sont généralement un drapeau rouge pour `O(n2)` ou pire.
4. **Simplifier les maths** – fractionner une course en deux ('up/2') couvre le cas où une seule course longue peut être divisée en deux sous-arrachages en augmentation égale.

---

- Oui. 9. SEO–Résumé amical

Si vous cherchez à craquer **LeetCode 3350 – Détection de Subarrays en augmentation adjacente II**, cet article vous donne:

* Une solution **Java** – temps "O(n)", espace "O(1)".
* A **Python** implémentation – même efficacité.
* Une version **C++** – parfaite pour une programmation compétitive.
* Une explication claire de pourquoi l'algorithme **one-pass** est l'approche optimale.

Inclure des mots-clés comme *LeetCode 3350*, *Adjacent Augmenting Subarrays*, *O(n) Algorithme*, *Java/Python/C++ solution*, *job interview coding*, *algorithm interview* – qui aideront les recruteurs à trouver ce post lors de la recherche de solutions de codage de haute qualité.

Bon codage et bonne chance pour votre prochaine interview!