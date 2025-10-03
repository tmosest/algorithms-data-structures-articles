---
titre: LeetCode 1567. Longueur maximale de la subarraie avec produit positif -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1567. Longueur maximale de la sous-couche avec un produit positif
### Solutions Java, Python & C++ + SEO-Optimized Blog Post

---

Aperçu du problème
Compte tenu d'un nombre entier, trouver la longueur **maximum** d'un subarray **contitueux** dont le produit est **positif**.
Un sous-réseau est une tranche consécutive du tableau; il peut contenir n'importe quel nombre d'éléments (y compris zéro).

Obstacles
- Oui.
-- -- -- -- -- --
1 ≤ longueur des nums ≤ 105 '

- Oui. Pourquoi ce problème fait-il des ravages?
- **La pertinence du monde réel**: Similaire à la recherche de la plus longue tranche de données de la série chronologique ou financière.
- **Interview mine d'or**: De nombreux intervieweurs demandent des variations pour tester la compréhension de **DP**, **greedy** et **edge-case-management**.
- **LeetCode 1567**: Haute circulation, moyenne difficulté – parfait pour construire un portefeuille.

---

## Ohio Solution Insight – One-Pass O(n), O(1) Espace

- Oui. Principales observations

1. **Zero est une réinitialisation** – le produit devient 0, donc nous commençons à compter à partir de l'élément suivant.
2. **Les chiffres négatifs retournent la parité** – chaque fois que nous voyons un négatif, un produit positif devient négatif et inversement.
3. ** Maintenir deux longueurs**
- `posLen` – longueur de la plus longue sous-couche se terminant à l'indice actuel avec un produit **positif**.
- `negLen` – longueur du plus long subarray se terminant à l'indice actuel avec un produit **négatif**.

Leur mise à jour dépend du signe de l'élément courant.

Règles de transition

Valeur actuelle Effet sur "posLen" Effet sur "negLen"
C'est le cas.
Réinitialiser à "0" Réinitialiser à "0" Réinitialiser à "0"
Positif 1 ''NégLen = négLen > 0 ? negLen + 1 : 0'
Swap `posLen` & `negLen` (après avoir ajouté `1` à chaque)

La réponse est le "posLen" maximum vu pendant le scan.

Complexité

- **Heure**: `O(n)` – passage unique sur le tableau.
- **Espace**: "O(1)" – seulement quelques variables entières.

---

Mise en œuvre du code

####==# Java (style LeetCode)

"Java
solution de classe {
Int public getMaxLen(int[] nums) {
posLen = 0; // longueur de la sous-production positive
la longueur du sous-réseau de produits négatifs
int best = 0; // mondial best

pour (int x : nombres) {
Si (x) 0) {
posLen = 0;
negLen = 0;
} sinon si (x > 0) {
os Len++;
ngLen = ngLen > 0 ? negLen + 1 : 0;
} autres { // x < 0
int oldPos = pos Len;
PosLen = negLen > 0 ? negLen + 1 : 0;
negLen = oldPos + 1;
}
best = Math.max(best, posLen);
}
le meilleur retour;
}
}
«» "

Python (style LeetCode)

'`python
Solution de classe:
def getMaxLen(self, nombres: List[int]) -> Int:
pos_len = 0
_neglen = 0
meilleur = 0

pour x en nombres:
Si x == 0:
= 0, 0
elif x > 0:
Pos_len += 1
neg_len = neg_len + 1 si neg_len > 0 autre 0
Autre: # négatif
pos_len, neg_len = (neg_len + 1 si neg_len > 0 autre 0), pos_len + 1
best = max(best, pos_len)

le meilleur retour
«» "

####3-C++ (style LeetCode)

'`cpp
solution de classe {
public:
Int getMaxLen(vecteur<int>& nums) {
int posLen = 0, negLen = 0, best = 0;

pour (int x : nombres) {
Si (x) 0) {
os Len = negLen = 0;
} sinon si (x > 0) {
posLen += 1;
ngLen = ngLen > 0 ? negLen + 1 : 0;
} autre { // négatif
int oldPos = pos Len;
PosLen = negLen > 0 ? negLen + 1 : 0;
negLen = oldPos + 1;
}
best = max (meilleur, posLen);
}
le meilleur retour;
}
};
«» "

Les trois snippets fonctionnent dans **O(n)** temps et **O(1)** espace, correspondant à la solution optimale sur LeetCode.

---

Le bon, le mauvais et le mauvais de 1567

### Titre (SEO-optimisé)
La maîtrise du LeetCode 1567 – Le bon, mauvais et laid de la longueur maximale Subarray avec le produit positif *

> *Mots clés*: LeetCode 1567, subarray de longueur maximale, produit positif, prép d'entrevue, solution Java Python C++, DP, algorithme gourmand, entretien d'emploi.

---

Introduction

Si vous êtes à la chasse pour ce problème d'entretien prochain grand de crack, ne cherchez pas plus loin que **LeetCode 1567**. C'est un puzzle classique *array + parité* qui teste à la fois *la conscience de la complexité du temps* et *la pensée de cas de référence*. Dans ce post, nous allons décomposer le problème, explorer les avantages et les inconvénients des approches communes, et enfin livrer **trois implémentations propres et prêtes à la production**.

---

Pourquoi Ce problème est une Goldmine

Explication
-- -- -- -- -- --
Autres **Entrée simple**= Un seul tableau – aucune structure imbriquée. Autres
**Clear Goal** Autres
Vous pouvez le résoudre avec DP, cupidité, ou même diviser-et-conquer – idéal pour montrer l'ampleur. Autres
**Haute pertinence**= La logique de "reset sur zéro" et "flip sur négatif" apparaît dans de nombreux scénarios du monde réel (traitement des signaux, analyse des stocks, etc.). Autres
**LeetCode Traffic**= Volume de recherche élevé → parfait pour montrer votre portfolio ou GitHub. Autres

---

- Oui. Les mauvaises – pièges communs

1. ** Manque de compréhension du signe du produit**
*De nombreux débutants pensent par erreur qu'un nombre négatif change de longueur *les deux*. *
2. **Ignorer les zéros**
*Passer la réinitialisation conduit à des longueurs inférieures incorrectes. *
3. **Complexité extra-spatiale**
*Certaines solutions DP utilisent deux tableaux (`dpPos`, `dpNeg`) – inutiles lorsqu'une seule passe suffit. *
4. **Délibérations**
* Nombre négatif unique, tous les zéros, ou longueur de tableau 1 – toujours tester ces avant de soumettre. *

---

- Oui. Les approches Ugly – inefficaces ou sur-ingénieuses

L'approche Pourquoi c'est Ugly
-- -- -- -- -- --
**Brute-Force O(n2)** Autres
**Tableaux DP complets**"dpPos[i]", "dpNeg[i]` tableaux → O(n) espace qui peut être évité. Autres
**Récursive Backtracking**.La récursion profonde peut atteindre les limites de la pile sur les grandes entrées. Autres
**Vérification de la signalisation par défaut**= L'utilisation de `abs(x) % 2` au lieu de `x < 0` peut conduire à un dépassement lorsque `x = -109`. Autres

---

Étape par étape (Essayez la course)

Envisagez "nums = [1, -2, -3, 4]":

Valeur d'idx Len-Len-Len-Best-
-- -- -- -- -- -- -- -- -- -- --
C'est vrai.
C'est vrai.
Dénomination des marchandises
Autres

La longueur maximale de subarray du produit positif est **4** – la gamme complète.

---

### Mise en œuvre du code

* (fourni précédemment dans le présent document)*
> Chaque solution utilise un seul passage, ne conserve que trois entiers et fonctionne dans un temps linéaire.

---

Référence A emporter

- **Utilisez les en-têtes avec des mots-clés**: -LeetCode 1567, -longueur maximale subarray, --produit positif.
- **Insert Code Snippets**: Les moteurs de recherche aiment le contenu riche en code.
- **Ajouter la Meta Description** : Solve LeetCode 1567 en Java, Python et C++ avec un algorithme avide O(n). Lire l'article complet au maître DP et des astuces gourmandes pour les entretiens d'emploi. (en milliers de dollars)
- **Lien retour**: Intégrer un lien au problème LeetCode et à votre dépôt GitHub.

---

Pensées de clôture

Maîtrise **LeetCode 1567** démontre:

- Capacité de *détecter et d'exploiter les modèles* (signe flips, réinitialise).
- intuition de l'espace-temps (O(1) vs O(n)).
- Polyvalence entre les langues (Java, Python, C++).

Partagez ces implémentations sur votre portefeuille, discutez des compromis dans votre entrevue, et vous vous démarquez comme un penseur algorithmique ** bien arrondi** prêt pour le prochain emploi technologique.

Bon codage, et bonne chance pour votre voyage d'entrevue! C'est ce qu'il a dit.

---