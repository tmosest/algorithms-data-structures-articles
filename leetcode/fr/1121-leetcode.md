---
titre: LeetCode 1121. Diviser la répartition dans des séquences croissantes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1121 – Diviser les séquences en augmentant
**Java / Python / C++ – Solutions complètes + Blog post**

> Comment résoudre un LeetCode dur en < 5 min et en parler comme un gestionnaire d'embauche.

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Insight clé – la solution de l'avidité] (#insight clé)
3. [Mise en œuvre en Java] (#java)
4. [Mise en œuvre dans Python](#python)
5. [Mise en œuvre en C++](#cpp)
6. [Blog Post – Le bon, le mauvais, et le mauvais] (#blog)
7. [Complexité et choix des entrevues](#analyse)

---

- Oui. 1. Aperçu du problème <un nom="problème-overview"></a>

> **LeetCode 1121 – Diviser les séquences pour augmenter**
> *Difficulté: difficile*

> **Définition**
> *Avec un tableau entier trié `nums` et un entier `k`, retourner `true` si le tableau peut être divisé en un ou plusieurs subséquences croissantes disjointes chacune de la longueur **au moins `k`**; sinon retourner `false`. *

**Exemples**

Résultats
C'est quoi ?
[1,2,2,3,4,4] Autres
"[5,6,6,8]" ""

**Contrôles* *

«» "
1 <= k <= longueur totale <= 10^5
1 <= nombres[i] <= 10^5
nombres triés dans un ordre non décroissant
«» "

---

- Oui. 2. Aperçu clé – La solution de l'avidité <a name="key-insight"></a>

- Oui. Pourquoi est-ce un problème *Hard*?
Le tableau est déjà trié, mais nous devons décider comment *partir* le dans des séquences en augmentation stricte avec une contrainte de longueur minimale.

- Oui. L'observation "Good"
- **Toutes les valeurs égales doivent appartenir aux sous-séquences *différentes*. * *
Étant donné qu'une subséquence doit être en augmentation stricte, des nombres identiques ne peuvent pas apparaître deux fois dans la même subséquence.
- Oui. Par conséquent, le nombre minimum* de sous-séquences que nous avons besoin est égal à la fréquence maximale** de toute valeur unique en «nums».
Appelez cette valeur `maxFreq`.

- Oui. La partie "bad"
- Même si nous avons des sous-séquences `maxFreq`, leurs longueurs peuvent différer.
Le mieux que nous puissions faire est de distribuer les numéros aussi uniformément que possible.
- Oui. La séquence **la plus courte** aura au moins une longueur
\[
\text{floor}\!\Bigl(\frac{n}{maxFreq}\Bigr)
\]
où "n = longueur nums".

- Oui. La prise
- Oui. Nous ne nous soucions que si la longueur *minimum* est au moins `k`.
D'où la condition simplifie:
\[
n \ge k \times max Belgique
\]

### dernier règne gourmand
1. Compter la fréquence de chaque élément.
2. Laisser `maxFreq` être la plus haute fréquence.
3. Retour `true` si `nums.length >= k * maxFreq`, sinon `false`.

Ceci est **O(n)** temps, **O(1)** espace supplémentaire (seulement quelques variables entières).

---

- Oui. 3. Mise en œuvre Java <a name="java"></a>

"Java
***
* 1121. Diviser les séquences en hausse
* Difficulté : difficile
*
* Heure: O(n)
* Espace: O(1)
*/
solution de classe {
publique booléenne canDivideIntoSubsequences(int[] nums, int k) {
int maxFreq = 0;
i = 0;
pendant que (i < longueur nums.) {
j = i;
pendant que (j < nums.longueur && nums[j] == nums[i]) j++;
maxFreq = Math.max(maxFreq, j - i);
i = j;
}
retour nums.longueur >= k * maxFreq;
}
}
«» "

---

- Oui. 4. Mise en oeuvre de Python <un nom="python"></a>

'`python
# 1121. Diviser en séquence croissante
♪ Heure: O(n), espace: O(1)

Solution de classe:
def canDivideIntoSubsequences(self, nombres: List[int], k: int) -> C'est vrai.
max_freq = 0
i = 0
n = len(nums)
alors que i < n:
j = i
alors que j < n et nums[j] == nums[i]:
j += 1
max_freq = max(max_freq, j - i)
i = j
retourner n >= k * max_freq
«» "

---

- Oui. 5. Mise en œuvre C++ <a name="cpp"></a>

'`cpp
// 1121. Diviser en séquence croissante
// Heure: O(n), espace: O(1)

solution de classe {
public:
bool canDivideIntoSubséquences(vecteur<int>& nums, int k) {
int maxFreq = 0;
i = 0, n = nombres.size();
pendant que (i < n) {
j = i;
pendant que (j < n& nums[j] == nums[i]) ++j;
maxFreq = max(maxFreq, j - i);
i = j;
}
retourner n >= k * maxFreq;
}
};
«» "

---

- Oui. 6. Billet de blog – Le Bon, le Mauvais, et l'Ugly

> *Article optimisé par le SEO: 1121 – Diviser les séquences pour augmenter – Une solution de préparation à l'entrevue*

---

Introduction

Si vous vous préparez à une entrevue d'ingénierie logicielle, **LeetCode 1121** est un classique, divisez le tableau en un problème croissant de séquences qui peut faire voyager de nombreux candidats. Dans ce post, nous disséquons le problème, nous traversons une solution cupide propre, nous comparons d'autres approches et nous soulignons comment expliquer votre processus de pensée à un gestionnaire d'embauche.

C'est vrai. Mots clés
- LeetCode 1121
- Diviser les séquences pour augmenter
- Algorithme des subséquences de l'array
- Solution Java / Python / C++
- Problème d'entretien difficile
- Conseils d'entretien de codage

---

- Oui. 1. Récapitulation des problèmes

On vous donne un tableau entier ** trié** `nums` et un entier positif `k`.
Vous devez décider si vous pouvez partitionner `nums` dans un ou plusieurs sous-séquences disjoints ** augmentant de façon stricte**, chacun de longueur **≥ k**.

Pourquoi est-ce difficile ?
Parce que vous devez équilibrer deux contraintes simultanément:
1. Chaque subséquence doit être strictement en augmentation → nombres identiques ne peuvent coexister dans la même subséquence.
2. Chaque subséquence doit être assez longue → vous ne pouvez pas créer trop de séquences courtes.

---

- Oui. 2. Approches naïves (les mauvais)

1. **Suivi / DFS** – Essayez chaque partitionnement.
*Complexité temporelle: Il n'est pas possible d'utiliser `n ≤ 10^5'.
2. **Greedy par élément** – Affecter chaque nombre à une séquence existante ou en lancer une nouvelle.
Cela peut devenir désordonné; vous devez toujours suivre la longueur de chaque séquence.
3. ** Programmation dynamique** – DP sur les positions et les longueurs de séquence actuelles.
L'espace et le temps soufflent de façon exponentielle.

Toutes ces approches dépassent les limites de temps ou sont trop complexes pour être expliquées lors d'une entrevue.

---

- Oui. 3. La tache douce – Greedy par fréquence (La bonne)

**Observation 1 – Questions relatives à la fréquence**
Comme le tableau est trié, les duplicatas sont contigus.
Une sous-séquence augmente strictement, donc ** chaque duplicata doit appartenir à une autre sous-séquence**.
Par conséquent, le nombre *minimum* de sous-séquences dont nous avons besoin est simplement la fréquence **maximum** de toute valeur.

**Observation 2 – Répartition équilibrée**
Avec les sous-séquences `m = maxFreq`, le mieux que vous pouvez faire est de répartir les nombres aussi uniformément que possible.
La sous-séquence la plus courte contiendra alors au moins des numéros `=n / m==`.
Si `=n / m== ≥ k`, la condition est remplie; sinon, il est impossible.

**Simplification mathématique**
''n/m' ≥ k ' , 'n ≥ k * m'.
Il nous suffit donc de vérifier une seule inégalité.

**Étapes d'algorithme**

1. Scanner le tableau trié une fois pour calculer `maxFreq`.
2. Vérifiez si `n >= k * maxFreq`.
3. Retourne le résultat.

**Pourquoi c'est correct* *
- *Nécessité* : Si vous ne pouvez pas attribuer tous les duplicatas à des sous-séquences distinctes (c.-à-d. les sous-séquences `maxFreq`), vous auriez deux valeurs identiques dans la même sous-séquence, en violation de la règle qui augmente strictement.
- *Sufficiency* : Avec exactement les sous-séquences `maxFreq`, les nombres peuvent être assignés rond-robin pour maintenir chaque longueur de subséquence équilibrée. La longueur minimale est `=n / maxFreq==‘. Si cela est au moins `k`, toutes les séquences répondent à la condition.

**Heure et espace**
- Temps: O(n) – une passe linéaire.
- Espace: O(1) – seulement quelques compteurs.

---

- Oui. 4. Échantillons de codes

- **Java** – [voir section 3] (#Java)
- **Python** – [voir section 4] (#python)
- **C++** – [voir rubrique 5] (#cpp)

---

- Oui. 5. Cas de bord et pièges

Pourquoi c'est important Manipulation
- C'est quoi ?
Toute partition fonctionne si les duplicata peuvent être séparés. L'inégalité devient `n ≥ maxFreq`. Toujours vrai depuis `n ≥ maxFreq`. Autres
Autres Tous les éléments sont égaux. Doit renvoyer `faux` à moins que `k = 1`. Autres
`n` trÃ ̈s grand, `k` trÃ ̈s grand. Utilisez des types "long" ou 64 bits. Autres
Des chiffres négatifs ? La garantie de contraintes "nums[i] ≥ 1 %. Autres
* Non autorisé ('num.longueur ≥ 1'). Autres

---

- Oui. 6. Explication de préparation à l'entrevue

> La clé de ce problème est de réaliser que les duplicatas nous obligent à créer au moins autant de subséquences que la valeur la plus fréquente. Une fois que ce minimum est connu, nous devons simplement vérifier que nous pouvons distribuer le reste des éléments afin que chaque subséquence ait au moins des éléments `k`. Parce que le tableau est trié, la distribution est insignifiante : on peut imaginer remplir les subséquences round-robin. La longueur minimale sera `=n / maxFreq==‘. Donc la réponse est simplement `n >= k * maxFreq`. Cela donne une solution O(n) à la fois optimale et facile à expliquer. (en milliers de dollars)

---

- Oui. 7. A emporter pour votre prochaine entrevue de travail

- **Toujours chercher une propriété qui réduit l'espace de recherche** – ici, trié ordre + duplicata.
- **Balance temps/espace contre clarté** – la solution gourmande est courte, rapide et facile à prouver.
- **Expliquez votre raisonnement étape par étape** – les intervieweurs apprécient un récit clair : (en milliers de dollars)
- **Cas de bord de Mention** – montrez que vous avez pensé aux limites (`k = 1`, tous les duplicatas, les grandes entrées).
- **Pratique d'écriture du code** – choisissez votre langue de confort mais soyez prêt à s'adapter.

---

- Oui. 8. Pensées finales

LeetCode 1121 est un excellent problème pour montrer votre capacité à transformer une contrainte apparemment dure en une simple inégalité mathématique. Avec une solution cupide et propre, vous pouvez démontrer des capacités de pensée algorithmique, d'efficacité et de communication d'entrevues, autant de qualités que les employeurs apprécient.

Bon codage, et bonne chance d'atterrir ce travail de rêve!

---

- Oui. 9. Références

- Problème de LeetCode: https://leetcode.com/problèmes/divis-array-in-upering-sequences/
- Solutions discutées :
- Goyal – Solution Java intuitive facile
- Sakshi – Solution Java simple
- Deleted_user – -Solution

---

> **Auteur** – *Votre nom*, ingénieur logiciel et coach d'entrevue de codage.
> *Suivez-moi sur LinkedIn/Twitter pour plus de tutoriels en algorithme. *

---

*(Nombre de mots: ~1400 – optimisé pour le référencement et la lisibilité.) *