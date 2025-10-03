---
titre: LeetCode 923. 3Sum avec multiplicité - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3-Sum avec multiplicité – LeetCode 923
**Java / Python / C++ – Solution complète + SEO-Optimized Blog Post**

---

- Oui. Ce que vous apprendrez

Ce que vous découvrirez
- Oui.
Déclaration du problème Le problème du nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de réponses est le nombre de fois où le nombre de fois se trouve le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois qu'est le nombre de fois le nombre de fois où le nombre de fois où le nombre de fois où le nombre de fois où le nombre de jours est plus grand a été exprimé est plus élevé a été plus élevé
Autres Pourquoi ça compte ?Une question d'interview commune qui teste le comptage, la combinatoire et l'optimisation.
Bonne et mauvaise Comment une solution naïve échoue, et l'élégante approche O(1012) qui gagne
Pièges avec débordement entier et modulo arithmétique
Code de produit propre, implémentations prêtes à la production en **Java, Python, C++** Autres
Mots clés, méta-tags et structure pour vous aider à vous classer sur les requêtes de recherche d'emploi

> **Mots clés**: 3Sum Avec Multiplicité, LeetCode 923, algorithme d'entretien, combinatoire, comptage triples, modulo 1e9+7, solution Java, solution Python, solution C++, entretien d'emploi, entretien de codage.

---

- Oui. 1. Exposé des problèmes

> **3Sum avec multiplicité**
> **Moyen**

> ** Signature fonctionnelle**
> ``java
> public int troisSumMulti(int[] arr, int cible)
> `` "

> **Don**:
> - `arr` – tableau entier, `3 <= arr.longueur <= 3000`
> - `0 <= arr[i] <= 100`
> - `0 <= cible <= 300`
>
> **Retour** le nombre de triples de l'indice `i < j < k`
> `arr[i] + arr[j] + arr[k] == cible`.
> Puisque la réponse peut être énorme, retourner le modulo `1_000_000_007`.

> **Exemples**

Entrée Sortie Explication
C'est pas vrai.
"[1,1,2,2,3,3,4,4,5,5]", "cible = 8"
"[1,1,2,2]", "cible = 5"
"[2,1,3]", "cible = 6"

---

- Oui. 2. Pourquoi c'est une bonne question d'entrevue

- ** Aspects multiples** : manipulation de tableau, combinatoire, arithmétique modulaire, compromis temporels.
- **Facile à mal optimiser**: une triple boucle imbriquée est O(n3) – trop lente pour `n = 3000`.
- **Afficher la créativité algorithmique**: l'utilisation du comptage des fréquences et des formules combinatoires réduit la complexité à O(1012).

---

- Oui. 3. Pièges communs (du côté de l'Ugly)

Pourquoi il échoue
C'est quoi ?
**Naïve O(n3) boucles**
**Ne pas manipuler le module**
**Utilisation d'ints 32 bits pour les combinatoires** peut déborder avant la division
**Cas de bords manquants (i == j == k)**
** Ordre de l`Index**

---

- Oui. 4. L'approche "Good" – Fréquence + Combinatorics

Comme chaque élément est dans `[0, 100]`, nous pouvons remplacer le tableau par une table *fréquence* de longueur 101.
Ensuite, nous n'avons besoin d'itérer que sur toutes les paires possibles `(i, j)` avec `i <= j`.
Pour chaque paire, nous calculons `k = cible - i - j` et vérifions si `0 <= k <= 100`.

#### 4.1 Compte de 3 cas

Quantité de triples Formule
- C'est quoi ?
Tous les trois sont égaux.
"i" == j != k"= Les deux premiers sont égaux, le troisième est différent. 2) * cnt[k] = cnt[i] * (cnt[i]-1) / 2 * cnt[k]» Autres
Tous distincts Autres
`i < j == k`=Symmétrique à précédente, manipulée lorsque la boucle atteint `(j, j)`="cnt[i] * C(cnt[j], 2)` – ceci est couvert par le cas `i < j < k` lorsque nous itérerons toutes les combinaisons, mais nous évitons le double comptage en considérant seulement `i <= j <= k` et en appliquant le facteur combinatoire approprié. Autres

Les boucles passent au plus 101 × 101 = 10 201 itérations – négligeables par rapport à la taille d'entrée initiale.

---

- Oui. 5. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Construire une table de fréquence **O(n)**
Autres Double boucle sur les valeurs
**Total******O(n + 1012)

`n` peut être jusqu'à 3000; l'algorithme est confortablement rapide pour toutes les limites.

---

- Oui. 6. Mise en œuvre du code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.
Tous utilisent la même logique basée sur la fréquence et manipulent l'arithmétique modulaire en toute sécurité.

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

public int troisSumMulti(int[] arr, int cible) {
long[] cnt = nouveau long[101]; // table de fréquence
pour (int v : arr) cnt[v]++; // O(n)

résultat long = 0L;

pour (int i = 0; i <= 100; i++) {
si (cnt[i]] 0) poursuivre;
pour (int j = i; j <= 100; j++) {
si (cnt[j]] 0) poursuivre;
int k = cible - i - j;
Si (k < 0.0.0 k > 100.0 cnt[k] == 0) poursuivre;

si (i == j && j == k) { // tous égaux
résultat += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) / 6;
} sinon si (i == j) { // *J !=k
résultat += cnt[i] * (cnt[i] - 1) / 2 * cnt[k];
} sinon si (j == k) { // C'est moi.
résultat += cnt[i] * cnt[j] * (cnt[j] - 1) / 2;
} autres { // tous distincts
résultat += cnt[i] * cnt[j] * cnt[k];
}
résultat %= MOD;
}
}
retour (int) résultat;
}
}
«» "

6.2 Python

'`python
Solution de classe:
MOD = 1 000 000 007

def troisSumMulti(self, arr: List[int], cible: int) -> Int:
# fréquence des nombres 0..100
cnt = [0] * 101
pour v in arr:
cnt[v] += 1

Res = 0
pour i dans la plage(101):
si cnt[i] == 0:
poursuivre
pour j dans la plage(i, 101):
si cnt[j]] 0:
poursuivre
k = cible - i - j
si k < 0 ou k > 100 ou cnt[k] == 0:
poursuivre

i == j == k: # tous égaux
Res += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) // 6
Il y a un problème.
res += cnt[i] * (cnt[i] - 1) // 2 * cnt[k]
Il n'y a pas de lien entre les deux.
Rés += cnt[i] * cnt[j] * (cnt[j] - 1) // 2
Autre: # tous distincts
Rés += cnt[i] * cnt[j] * cnt[k]
Res %= soi-même. MOD
retour res
«» "

*### 6.3 C++

'`cpp
solution de classe {
public:
longue MOD = 1'000'000'007LL;

int threeSumMulti(vecteur<int>& arr, cible int) {
long cnt[101] = {0};
pour (int v : arr) ++cnt[v];

long an = 0;
pour (int i = 0; i <= 100; ++i) {
si cnt[i] continue;
pour (int j = i; j <= 100; ++j) {
si (!cnt[j]) continue;
int k = cible - i - j;
si (k < 0) k > 100) cnt[k] continue;

si (i == j && j == k) { // tous égaux
cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) / 6;
} sinon si (i == j) { // *J !=k
cnt[i] * (cnt[i] - 1) / 2 * cnt[k];
} sinon si (j == k) { // C'est moi.
cnt[i] * cnt[j] * (cnt[j] - 1) / 2;
} autres { // tous distincts
cnt[i] * cnt[j] * cnt[k];
}
as %= MOD;
}
}
retourner static_cast<int>(ans);
}
};
«» "

> **Astuce**: En C++, utilisez `long long` pour les calculs intermédiaires afin d'éviter les débordements.

---

- Oui. 7. Marche pas à pas (Java)

"Java
résultat long = 0L;
pour (int i = 0; i <= 100; i++) {
si (cnt[i]] 0) continuer; // sauter les nombres inutilisés
pour (int j = i; j <= 100; j++) {
si (cnt[j]] 0) poursuivre;
int k = cible - i - j;
Si (k < 0.0.0 k > 100.0 cnt[k] == 0) poursuivre;

Si (i == j && j == k) {
// Les trois indices indiquent le même nombre
résultat += cnt[i] * (cnt[i] - 1) * (cnt[i] - 2) / 6;
} sinon si (i) j) {
// i et j sont les mêmes, k est différent
résultat += cnt[i] * (cnt[i] - 1) / 2 * cnt[k];
} sinon si (j) k) {
// j et k sont les mêmes, i est différent
résultat += cnt[i] * cnt[j] * (cnt[j] - 1) / 2;
} autre {
// i, j, k sont tous distincts
résultat += cnt[i] * cnt[j] * cnt[k];
}
résultat %= MOD; // conserver une valeur faible
}
}
«» "

Chaque branche utilise le bon facteur combinatoire :

- "C(n, 3)" quand tous sont égaux,
- "C(n), 2) * m' quand deux sont égaux,
- `n * m * p` quand tout est distinct.

---

- Oui. 8. Validation des cas de bord

> **Test**: `arr = [0, 0, 0]`, `cible = 0`
> **Résultat**: `C(3, 3) = 1` – un seul triple `(0, 0, 0)`.

> **Test**: `arr = [50, 50, 50, 50]`, `cible = 150`
> **Résultat**: `C(4, 3) = 4` – quatre triples `(50,50,50)`.

---

8.1 Que faire si les chiffres étaient plus grands?

Si le domaine était plus grand (par exemple, des valeurs `int` jusqu'à 105), l'approche basée sur la fréquence fonctionne encore, mais nécessite une carte *hash* au lieu d'un tableau de taille fixe.
La complexité deviendrait O(unique2).
Pour les contraintes de LeetCode, le domaine fixe 0–100 est garanti, donc un tableau de 101 longueurs suffit.

---

8.2 Et si on voulait tous les ordres ?

Si l'exigence était *non ordonnée* triple (tout ordre d'indice autorisé), les formules de comptage changent légèrement (pas besoin de "i <= j" restriction).
La solution présentée respecte naturellement " i < j < k " , correspondant à l ' énoncé du problème.

---

8.3 Analogies du monde réel

- ** Stock de produits**: "cnt` est comme le niveau des stocks; "(i, j, k)" sont trois articles qui se résument à un prix cible.
- **Paradoxe du jour**: Le comptage des combinaisons de valeurs identiques est analogue au regroupement des anniversaires.

---

8.4 Manipulation de très grands nombres

Pour les langues avec des entiers de précision arbitraire (p. ex. Python"s `int`), la division avant le modulo est sûre.
En langues à largeur fixe, effectuez toujours la division *après* en multipliant pour garder les nombres petits.

---

8.5 Questions courantes d'entrevue que vous pourriez poser

1. **Pouvez-vous expliquer les formules combinatoires? * *
*Réponse*: `C(n,3) = n(n-1)(n-2)/6`, `C(n,2) = n(n-1)/2`

2. **Pourquoi itérer `j` de `i` à 100 au lieu de 0? **
*Réponse*: S'assure que nous n'avons pas de paires de doubles comptes et maintient `i <= j`.

3. **Comment modifier cela si les chiffres pouvaient être négatifs? * *
*Réponse*: Déplacez la table de fréquence ou utilisez un `HashMap<entier, Long>`; toujours O(unique2).

4. **Que se passe-t-il si `cible` est énorme ( > 300)? **
*Réponse*: `k` devient négatif → sauté; l'algorithme retourne naturellement 0.

---

8.6 Pensées finales

- **Élégance** : le remplacement des valeurs par des fréquences transforme un problème apparemment intractable O(n3) en une minuscule boucle O(10 k).
- **Évoluable**: Fonctionne pour tout `n` ≤ 3000 sans réglage.
- **Arithmétique modulaire**: Gardez un modulo en cours d'exécution pour éviter le débordement et correspondre à la sortie attendue de LeetCode.

N'hésitez pas à copier-coller le code dans votre IDE préféré et à exécuter les cas de test fournis.

---

# # 8.7 Résumé

Point de vue clé Autres
C'est pas vrai.
**Tableau de fréquence**
**Boucle double** Autres
Calcul du k**
**Manipulation de l'affaire**
**Modulo**

C'est un exemple de manuel de transformation d'une idée de force brute en solution *optimale*.

---

## 8.8 Quoi-si ?

1. **Et si `cible` peut être jusqu'à 300? **
L'algorithme fonctionne toujours parce que `k` peut être négatif ; nous sautons simplement ces cas.

2. ** Pouvons-nous réduire davantage la complexité? * *
Pas vraiment – la double boucle sur les 101 valeurs est déjà *O(1)* par rapport à l'entrée.

3. **Si les nombres étaient jusqu'à 105, pourrions-nous encore utiliser un tableau de fréquence? * *
Oui, mais la table serait grande; une carte de hachage (`unordered_map`) et itérer sur les touches uniques serait encore rapide.

4. **Pourrions-nous utiliser une technique à deux points après tri? * *
Deux-pointeur fonctionne pour *distinct* sommes, mais gérer des nombres égaux combinatoirement est plus simple avec la table de fréquence.

---

## 8.9 Problèmes de pratique

- **LeetCode 1512** – *Ajouter à l'image-forme de l'entier* (utiliser deux-pointer).
- **LeetCode 1675** – *Opérations minimales pour réduire X à zéro* (deux points + fenêtre coulissante).
- **LeetCode 436** – *Trouver l'intervalle droit* (recherche binaire + tri).

---

8.10 Avis de clôture

- **Comprendre le domaine** : Des contraintes comme `0 <= val <= 100` ouvrent la porte aux optimisations basées sur la fréquence.
- **Formules combinatoires master**: `nC2`, `nC3` sont vos amis.
- **Arithmétique modulaire à la main** Utilisez `long`/`long` et appliquez `% MOD` après chaque ajout.

Bonne chance pour cette interview ! C'est ce qu'il a dit.

---

FAQ

**Q** : *Et si le tableau d'entrée contient des nombres négatifs ? *
**A** : La solution actuelle repose sur le domaine `[0,100]`. Pour les négatifs, utilisez un `HashMap<entier, Long>` pour stocker les fréquences et itérer sur toutes les paires de clés. La complexité devient O(unique2).

**Q**: * Pouvons-nous précalculer les facteurs factoriaux pour les combinaisons? *
**A** : Avec de petits comptages fixes, les formules directes sont plus simples et évitent les matrices factorielles.

**Q**: *Pourquoi ne pas utiliser des ints 32 bits en Python? *
**A**: Les ints de Python sont une précision arbitraire, donc le débordement n'est pas un problème, mais nous jetons toujours à `int` pour le retour final.

---

**Profitez du codage, et bonne chance dans votre prochaine interview! * *