---
titre: LeetCode 3205. Score d'arrêt maximal Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code – 3205 Score d'arrêt maximal I

Le problème est un classique **O(n)** problème gourmand.
Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

> **Signature (Code de bord)* *
> ```texte
> int public maxScore(int[] nums); // Java
> int maxScore(vector<int>& nums); // C++
> int maxScore(vector<int> nums); // Python (base classe)
> `` "

---

Java 17
"Java
Importation de java.util.*;

solution de classe publique {
Int public maxScore(int[] nums) {
int res = 0;
int mx = 0; // meilleure valeur vue à droite
pour (int i = longueur nominale - 1; i > 0; i--) {
mx = Math.max(mx, nums[i]); // garder le maximum à droite
res += mx; // sauter de i-1 à i (ou plus loin)
}
retour rés;
}
}
«» "

**Pourquoi ça marche** –
Nous traversons de l'élément le plus droit vers la gauche.
À chaque étape, nous conservons la valeur maximale vue jusqu'à présent (`mx`).
Sauter de l'index précédent au maximum *current* donne le score le plus élevé, donc nous ajoutons simplement `mx` au résultat.

---

Python 3
'`python
Solution de classe:
def maxScore(self, nombres: List[int]) -> Int:
Res = 0
mx = 0
# itérer de la fin au deuxième élément (index 1)
pour i dans la plage (len(nums) - 1, 0, -1):
mx = max(mx, nums[i]) # meilleure valeur à droite de i-1
Res += mx # score pour sauter de i-1 à i (ou plus loin)
retour res
«» "

*Version monoligne* (si vous aimez la brièveté):

'`python
à partir d'import d'itertools
Solution de classe:
def maxScore(self, nombres: List[int]) -> Int:
somme de retour(accumulation(nums[:0:-1), max))
«» "

---

C++ (g++17)
'`cpp
#incluez <vecteur>
#incluez <algorithme>
utilisant l'espace de noms std;

solution de classe {
public:
Int maxScore(vecteur<int>& nums) {
Int res = 0, mx = 0;
pour (int i = nombres.size() - 1; i > 0; --i) {
mx = max(mx, nombres[i]); // maximum à droite de i-1
res += mx; // score pour ce houblon
}
retour rés;
}
};
«» "

---

Article du blog – Le bon, le mauvais, et le mauvais de **Maximum Array Score

> **Mots-clés**: Leetcode, Score maximum d'array, algorithme, cupidité, programmation dynamique, O(n), O(1), interview, interview de codage, Java, Python, C++

Introduction

Lors d'une interview récente, j'ai été écrasé par LeetCode #3205 -Score d'arrêt maximal I-. C'est un problème faussement simple qui cache une clairvoyance avide. Dans ce post, je vais vous guider dans l'intuition, prouver pourquoi le choix avide est optimal, présenter des solutions Java/Python/C++ propres, et pointer des pièges communs. À la fin, vous serez prêt à accepter ce problème (et les mêmes) lors de votre prochaine entrevue de codage.

---

Déclaration de problème (Code de let #3205)

> On vous donne un tableau `nums`. À partir de l'index 0, vous devez sauter vers le dernier index.
> Dans un saut, vous pouvez sauter de l'index `i` à n'importe quel `j > i`.
> Chaque houblon vous décerne une note de `(j - i) * nums[j]`.
> Trouvez le score total maximum que vous pouvez obtenir.

**Contrôles* *

- "2 ≤ longueur nominale ≤ 10^3"
- `1 ≤ nombres[i] ≤ 10^5`

---

Intuition – Pourquoi une solution d'avidité fonctionne

1. **Décision locale, Optimum mondial**
Considérez tout état à l'index "i". Supposons que l'élément maximum à droite de `i` soit à la position `k` avec la valeur `nums[k]`.
*Si vous sautez de `i` à `k` en un seul saut, le score est `(k-i)*nums[k]`.
*Si vous sautez d'abord à un certain `j` (`i < j < k`) et puis à `k`, le score total est `(j-i)*nums[j] + (k-j)*nums[k]`.

2. **Comparer les deux**
«» "
(k-i)*nums[k] versus (j-i)*nums[j] + (k-j)*nums[k)
«» "
Déplacez le `(k-j)*nums[k]` commun à gauche:
«» "
(j-i)*nums[j] < (k-i)*nums[k] - (k-j)*nums[k] = (j-i)*nums[k)
«» "
Puisque `nums[k]` est le *maximum* parmi tous les `nums[j]`, l'inégalité tient toujours.
Par conséquent, le *single* hop à l'élément maximum à droite est strictement meilleur (ou égal si `nums[j] == nums[k]`).

3. **Induction**
En répétant l'argument pour chaque indice, le chemin optimal est :
- Commencez par '0 '
- Sauter à l'élément maximum dans `nums[1 ... n-1]`
- De là, sauter au maximum dans son suffixe, et ainsi de suite, jusqu'au dernier élément

L'algorithme est essentiellement de continuer à sauter au plus grand nombre à votre droite.

---

Mise en œuvre – O(n) / O(1)

Traverser le tableau de droite à gauche :

Étape
- C'est quoi ?
Autres 1= Garder une variable `mx` = valeur maximale vue à ce jour (initialement `0`). Autres
Autres Pour chaque indice `i` de `n-1` jusqu'à `1`:
- Mettre à jour `mx = max(mx, nums[i])` (maintenant `mx` est la meilleure valeur à droite de `i-1`).
- Ajouter `mx` à la réponse courante `res`. Autres

La dernière «res» est la note maximale.

- **Heure** : "O(n)" – laissez-passer unique.
- **Espace**: "O(1)" – mémoire supplémentaire constante.

---

Extraits de code

> **Java**
> ``java
> public int maxScore(int[] nums) {
> int res = 0, mx = 0;
> pour (int i = longueur nominale - 1; i > 0; i--) {
> mx = Math.max(mx, nombres[i]);
> res += mx;
> }
> retour rés;
> }
> `` "

> **Python**
> ``python
> solution de classe:
> def maxScore(self, nombres: List[int]) -> Int:
> res = mx = 0
> pour i dans la plage(len(nums)-1, 0, -1):
> mx = max(mx, nombres[i])
> res += mx
> retour res
> `` "

> **C++**
> ``cpp
> solution de classe {
> public:
> int maxScore(vecteur<int>& nums) {
> int res = 0, mx = 0;
> pour (int i = nombres.size() - 1; i > 0; --i) {
> mx = max(mx, nombres[i]);
> res += mx;
> }
> retour rés;
> }
> };
> `` "

---

Le bien

- **Simplicité** – Une seule boucle inversée et deux variables entières.
- **Performance** – Temps linéaire et mémoire constante.
- **Pro-fondé** – Le choix avide peut être formellement prouvé optimal.
- **Langage brut** – La même logique fonctionne en Java, Python, C++ (et beaucoup d'autres).

---

Le mal

- **Surveillance d'Edge-case** – Oublier de démarrer la boucle de `n-1` et ne pas inclure le dernier élément dans la réponse (certaines solutions naïves ignorent par erreur le saut final).
- **Grande entrée** – Alors que `n ≤ 1000` ici, le même motif fonctionne pour les tableaux énormes; juste assurer 64-bit arithmétique (`long` en Java, `long` en C++) si les valeurs dépassent `2^31-1`.
- **Miscompréhension de la formule** – Penser que le score est `i * nums[j]` au lieu de `(j-i)*nums[j]` conduit à de mauvaises réponses.

---

L'Ugly

- **Redondance à la programmation dynamique** – Certains candidats essaient une table DP complète `dp[i] = max sur j>i de (j-i)*nums[j] + dp[j]`, qui est `O(n^2)` et inutile.
- **Complex Récursion** – La mémorisation récursive avec un argument d'index est exagérée pour une simple solution gourmande.
- **Over‐Optimizing** – Micro‐Optimizing the inside loop with bit-wise tricks or fantasy bibliolars peut nuire à la lisibilité, qui est un critère d'entrevue clé.

---

Conseils d'entrevue

1. ** Expliquez l'idée de Greedy tôt** – Montrez l'intuition avant d'écrire le code.
2. **Statut de l'invariant** – Le terme "mx" est la valeur maximale à droite de l'indice actuel.
3. **Prouvez l'exactitude** – Passez par la comparaison à deux sauts.
4. **Mention Edge Cases** – p.ex., tous les éléments égaux, tableau en baisse stricte.
5. **Complexité temps/espace** – Toujours mentionner `O(n)` / `O(1)`.

---

Conclusion

Score d'arrêt maximal Je suis un exemple parfait d'un problème où une observation cupide *simple* transforme un DP apparemment complexe en un seul-liner. En gardant la valeur de suffixe maximale, nous garantissons le meilleur saut à chaque étape et l'optimisation en temps linéaire.

N'hésitez pas à copier les extraits ci-dessus dans votre IDE préféré, à exécuter les cas de test fournis et à les partager sur votre portfolio ou GitHub. Bonne chance avec votre prochaine entrevue – rappelez-vous : la clarté, la preuve et la brièveté sont vos meilleurs alliés ! C'est ce qu'il a dit.

---

**Tags:** #LeetCode #Algorithme #Greedy #DynamicProgrammation #CodingInterview #Java #Python #C++ #JobInterview #ProgrammationConseils