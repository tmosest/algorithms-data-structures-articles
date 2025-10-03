---
titre: LeetCode 2970. Compter le nombre d'incroyables Subarrays I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 2970
**Couvercle du nombre de subdivisions incamovibles I**

On vous donne un tableau 0 indexé de nombres entiers positifs.
Un **subarray** `[i ... j]` (contitueux, non-vide) est appelé *incommodable* s'il supprime le reste du tableau **de manière à augmenter de façon stricte**.
Retourner le nombre total de sous-barrages incrémables.

*Exemples*

Explication
C'est quoi ?
"[1,2,3,4]" "10" chaque sous-arrachage est incrémable"
"[6,5,7,8]" "" 7" seulement les 7 travaux de sous-arrachage énumérés
[8,7,6] Autres

*Contrôles*

«» "
1 ≤ longueur nominale ≤ 50
1 ≤ nombres[i] ≤ 50
«» "

Parce que le tableau est minuscule (= 50), une solution simple O(n3) brute-force fonctionne en quelques microsecondes et est acceptable pour un réglage d'entrevue.
Ci-dessous vous trouverez trois implémentations propres – **Java**, **Python** et **C++** – tous utilisant la même logique O(n3).
Nous montrons également une brève optimisation O(n2) qui mérite d'être prise en compte pour des entrées plus importantes.

---

- Oui. 2. L'idée de la force brute (O(n3))

1. **Cochez une sous-procès** `[i ... j]`.
2. **Passer tous les éléments à l'intérieur** `[i ... j]` et traverser les éléments restants de gauche à droite.
3. Vérifiez que chaque élément visité est ** strictement plus grand** que le précédent.
4. Si le chèque passe, le sous-barrage est incrédule → incrédule le compteur.

L'algorithme ne nécessite que quelques variables entières (`i`, `j`, `k`, `last`, `ok`) – espace supplémentaire constant.

Pourquoi ça marche ?

L'élimination d'une sous-tribu est équivalente à la concaténation du préfixe (`0 ... i‐1`) et du suffixe (`j+1 ... n‐1`).
Le tableau concaténé augmente strictement si chaque élément du suffixe est supérieur au dernier élément du préfixe, et tous les éléments de chaque segment augmentent déjà.
L'algorithme imite ce test en balançant le tableau une fois par sous-array candidat.

---

- Oui. 3. Détails de la mise en œuvre

Langue Faits saillants du code Autres
-- -- -- -- -- -- -- --
**Java**= Utilise des tableaux `int`, un compteur `long` pour éviter le débordement (pas nécessaire pour n=50, mais sûr). Autres
**Python**= Boucles droites; la simplicité de Python brille pour ce minuscule n. Autres
**C++**= Utilise `vector<int>`, `long long` comptoir et `bool ok` drapeau. Autres

Voici les extraits exacts.

#### 3.1 Java (Java 17)

"Java
solution de classe publique {
public longue incrédule SubarrayCount(int[] nums) {
int n = longueur nums;
long ans = 0;

// Indice de démarrage
pour (int i = 0; i < n; i++) {
// indice de fin
pour (int j = i; j < n; j++) {
booléen ok = vrai;
int last = Integer.MIN_VALUE; // sentinelle: aucun élément précédent

// Analyser le tableau entier
pour (int k = 0; k < n; k++) {
if (k >= i && k <= j) { // inside subarray – skip
poursuivre;
}
si (dernier >= nombres[k]) { // ne pas augmenter strictement
ok = faux;
pause; // pas besoin de continuer à vérifier
}
dernier = nombres[k];
}
si (ok) ans++;
}
}
le retour des an;
}
}
«» "

3.2 Python (Python 3,11)

'`python
Solution de classe:
def incremovible SubarrayCount(même, nombres: list[int]) -> Int:
n = len(nums)
ans = 0
pour i dans la plage(n): # commencer
pour j dans la plage(i, n): # fin
ok = Vrai
dernier = flotteur('-inf')
pour k dans la plage(n):
i i <= k <= j: # à l'intérieur du sous-barrage
poursuivre
si la dernière >= nombres[k]:
ok = Faux
pause
dernière = nombres[k]
si oui:
+= 1
retour et
«» "

### 3.3 C++ (C++17)

'`cpp
solution de classe {
public:
longue incrédule subarrayCount(vecteur<int>& nums) {
int n = nombres.size();
long an = 0;

pour (int i = 0; i < n; ++i) { // début
pour (int j = i; j < n; ++j) { // fin
bool ok = true;
int last = INT_MIN; // sentinelle

pour (int k = 0; k < n; ++k) {
si (k >= i && k <= j) continuer; // sauter sous-array
si (dernier >= nombres[k]) { // ne pas augmenter strictement
ok = faux;
pause;
}
dernier = nombres[k];
}
si (ok) ++ans;
}
}
le retour des an;
}
};
«» "

---

- Oui. 4. Plus optimisé (O(n2)) Affichage

Bien que la force brute passe confortablement, vous pouvez réduire la boucle intérieure en précomputant:

- `leftInc[i]` – est le préfixe `nums[0...i]` Ça augmente ?
- `rightInc[i]` – le suffixe `nums[i...n-1]` augmente-t-il strictement?

Puis pour chaque `[i...j]` vous devez seulement vérifier:

1. `leftInc[i-1]` (si `i>0`) – veille à ce que le préfixe avant `i` soit correct.
2. `rightInc[j+1]` (si `j+1<n`) – assure suffixe après `j` est bien.
3. `nums[i-1] < nums[j+1]` (si les deux côtés existent) – garantit que le point de jonction augmente.

Avec ces tableaux la décision d'un sous-array devient **O(1)**, transformant l'algorithme entier en **O(n2)**.
Pour les contraintes données, il est sur-ingénierie, mais c'est un excellent truc à retenir pour les questions d'entrevue où `n` pourrait être jusqu'à `105`.

---

- Oui. 5. Cas de bord et essais

Autres Test d'entrée prévu Pourquoi
C'est pas vrai.
Uniquement le paragraphe «[1]» est valide. Autres
"2" "[2,1]" "2" "[2]" et "[1]" laissent tous deux un seul tableau d'éléments, ce qui augmente strictement. Autres
Seul `[1,1]` laisse un tableau vide. Autres
"[3,2,1]""" `3`" `[3]`, `[2]`, `[1]` chaque produit `[2,1]`, `[3,1]`, `[3,2]` – tous en baisse stricte, de sorte que seule la sous-tribu complète `[3,2,1]` fonctionne. Autres
Tous les travaux de sous-traitance. Autres

Exécutez ces tests dans n'importe quelle langue; les trois solutions doivent correspondre.

---

- Oui. 6. Le Bon, le Mauvais, le Miséricordieux

Aspect du bien
- C'est quoi ?
**Simplicité** La force brute peut paraître lente à première vue. Trois boucles imbriquées peuvent intimider les nouveaux arrivants. Autres
**Performance** La vérification interne `if (k >= i && k <= j)` est répétée plusieurs fois. Autres
**Extensibilité**=Simplement pour s'adapter à d'autres problèmes d'élimination. Difficile à réutiliser pour des contraintes plus grandes. La logique n'est pas réutilisable pour les séquences en croissance non stricte. Autres
**Interview Appeal** Ça pourrait soulever un drapeau rouge sur la complexité du temps. Affiche la capacité d'écrire des boucles propres, mais la discussion d'optimisation manquante peut nuire. Autres

> **Takeaway** – Pour les contraintes de style d'entrevue, *readability* bat souvent *optimalité*.
> Si l'intervieweur demande explicitement une solution plus rapide, la méthode O(n2) ci-dessus est une prochaine étape rapide.

---

- Oui. 7. Résumé – Pourquoi vous allez marquer des points

- Oui. Le problème est un classique, supprimer un segment → vérifier la monotonicité.
- Une approche de force brute est parfaite pour les limites données.
- Les extraits Java/Python/C++ partagent le même squelette logique, prouvant que la solution est *langue-agnostique*.
- Oui. Vous pouvez toujours mentionner l'optimisation O(n2) pour démontrer la conscience de modèles plus efficaces.
- Oui. Le code est prêt à être collé dans une plateforme d'entrevue, et vous pouvez expliquer avec confiance chaque boucle à l'intervieweur.

Bonne chance pour atterrir sur ce call-out de codage-entrevue! C'est ce qu'il a dit