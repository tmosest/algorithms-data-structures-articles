---
titre: LeetCode 2048. Suivant Nombre numériquement équilibré -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

**LeetCode 2048 – Prochaine plus grande Nombre numériquement équilibré**

> Un entier `x` est **numériquement équilibré** si pour chaque chiffre `d` dans `x`, le chiffre `d` se produit **exactement `d` temps**.
> Compte tenu d'un entier `n (0 ≤ n ≤ 106)`, retourner le plus petit nombre numériquement équilibré strictement supérieur à `n`.

Exemples

Réponse
- C'est quoi ?
* * * * * *
1 000 000 1333 000
3 000 3133 Autres

La tâche est une question classique de style interview qui teste votre capacité à penser combinatoirement, à créer un espace de recherche et à écrire du code propre en plusieurs langues.



-----------------------------------------------------------------------------------

- Oui. 2. Pourquoi l'approche de rétrotraçage / pré-computation fonctionne

1. **Les chiffres sont limités* *
- La plus grande réponse possible pour les contraintes a au maximum **7 chiffres** (par exemple `766666`).
- Le chiffre `d` peut apparaître au plus `d` fois, donc le nombre maximum de chiffres différents que vous pouvez utiliser est `6` (1–6).
- Ça garde l'espace d'état minuscule.

2. **L'immeuble équilibré est local* *
- Il suffit de savoir combien de fois chaque chiffre a déjà été placé.
- Vous pouvez décider s'il faut placer un chiffre `i` sur la base `count[i] < i` et si vous avez encore assez de positions gauches pour terminer le nombre.

3. **Le pré-comptage est moins cher que la vérification d'un numéro à la fois* *
- Construire **chaque** nombre numériquement équilibré jusqu'à 7 chiffres.
- Conservez-les.
- Répondez à toute requête par une recherche binaire (`O(log M)` où `M` est le nombre total de nombres équilibrés – seulement quelques centaines).

Le compromis est une petite quantité de travail initial qui donne une solution propre et réutilisable.



-----------------------------------------------------------------------------------

- Oui. 3. L'algorithme (haut niveau)

«» "
1. Précalculer tous les nombres numériquement équilibrés avec 1 ... 7 chiffres
a. Construisez récursivement le chiffre par chiffre.
b. Conservez un tableau `cnt[10]` – combien de fois chaque chiffre a été utilisé.
c. Arrêter lorsque le préfixe construit est > n et que tous les chiffres satisfont à "cnt[d] == d` ou "cnt[d] == 0`.
d. Poussez le numéro valide sur une liste.

2. Triez la liste des numéros valides.

3. Pour répondre à une question n:
a. Recherche binaire du premier élément > n.
b. Retourne cet élément.
«» "

**Pourquoi la récursion fonctionne* *
Parce que chaque appel récursif choisit un seul chiffre à ajouter. La profondeur est au plus 7, donc la récursion est parfaitement sûre.



-----------------------------------------------------------------------------------

- Oui. 4. Mise en œuvre du code

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Chaque langue suit la même logique mais utilise des caractéristiques idiomatiques.

> **Astuce:** Si vous préparez une entrevue de codage, copiez-collez l'extrait qui correspond à la langue que vous allez utiliser. Tous sont des requêtes `O(M)` pré-computation, `O(log M)` et fonctionnent bien sous 1 ms pour les limites données.



#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {

// -------- API publique...
public int nextBeautiful Numéro(int n) {
// initialisation paresseuse – le premier appel construit la liste
si (balancedNumbers.isEmpty()) buildBalancedNumbers();
// Recherche binaire pour la première > n
int idx = Collections.binarySearch(equilibredNumbers, n + 1);
si (idx < 0) idx = -idx - 1; // point d ' insertion
retour équilibréNombres.get(idx);
}

// -------- Aides privées - Oui.
liste finale statique privée<entier> équilibréNombres = nouvelle liste d'array<>();

construction privée videBalancedNumbers() {
int[] cnt = nouvelle int[10];
retour(0, 0, cnt);
Collections.sort(nombres équilibrés);
}

vide privé retour(int prefix, int len, int[] cnt) {
si (len > 0 && isBalanced(cnt)) {
equilibredNumbers.add(préfix);
}
Si (len) 7) retour; // max 7 chiffres
pour (int d = 1; d <= 6; d++) { // chiffres 1..6 seulement
si (cnt[d] == d) continuer; // ne peut pas utiliser plus de ce chiffre
// Prune : positions restantes < nécessaires pour terminer ce chiffre
int restant = 7 - len;
si (le maintien < (d - cnt[d])) se poursuit;
cnt[d]++;
arrière piste (préfixe * 10 + d, len + 1, cnt);
cnt[d]--;
}
}

booléen privé estBalanced(int[] cnt) {
pour (int d = 1; d <= 6; d++) {
si (cnt[d] != 0 && cnt[d] != d) retourner faux;
}
retour vrai;
}
}
«» "

> **Complexité**
> *Pré-computation*: "O(1)" (la liste comporte < 300 éléments).
> *Query*: `O(log M)` (recherche binaire).
> * Mémoire* : "O(M)".



4.2 Python

'`python
de bisect import bisect_right
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
# Précalculer une fois
_équilibré : Liste[int] = []

def _init_(self):
Si non Solution._équilibré :
Solution._équilibré = auto._build_équilibré()

def nextBeautifulNumber(self, n: int) -> Int:
idx = bisect_right(Solution._équilibrée, n)
Return Solution._équilibré[idx]

def _build_equilibred(self) -> Liste[int]:
res = []
cnt = [0] * 10

def dfs(préfixe: int, longueur: int):
si longueur > 0 et auto._est_équilibré(cnt):
res.append(préfixe)
si longueur == 7: # max 7 chiffres
retour
pour d dans la plage (1, 7):
si cnt[d] == d: # ne peut pas utiliser plus de chiffre d
poursuivre
# autres créneaux
rem = 7 - longueur
si rem < (d - cnt[d]):
poursuivre
cnt[d] += 1
dfs(préfixe * 10 + d, longueur + 1 )
cnt[d] -= 1

Dfs(0, 0)
res.sort()
retour res

@staticmethod
def _is_equilibred(cnt: List[int]) -> bool:
retourner tous(cnt[d] == 0 ou cnt[d] == d pour d dans la plage (1, 7)
«» "

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int nextBeautiful Numéro(int n) {
si (balance.vide() build();
auto it = upper_bound(balanced.begin(), balanced.end(), n);
retour *it;
}

particulier:
vecteur statique <int> équilibré;

construction de vide statique() {
int cnt[10] = {0};
fonction<vit(int,int)> dfs = [&](int prefix, int len) {
si (len > 0 && isBalanced(cnt))
equilibred.push_back(préfix);
Si (len) 7) retour; // 7 chiffres max.
pour (int d = 1; d <= 6; ++d) {
si (cnt[d] == d) continuer;
int rem = 7 - len;
si (rem < d - cnt[d]) se poursuit;
++cnt[d];
dfs(préfixe * 10 + d, len + 1);
--cnt[d];
}
};
dfs(0, 0);
(équilibré.à partir(), équilibré.end());
}

bool statique estBalanced(const int cnt[]) {
pour (int d = 1; d <= 6; ++d)
si (cnt[d] && cnt[d] != d) retourner faux;
retour vrai;
}
};

vecteur<int> Solution::équilibrée; // définition de l'élément statique
«» "

-----------------------------------------------------------------------------------

- Oui. 5. Le bon – mauvais – Ugly

Qu'est-ce qui est bon Qu'est-ce qui pourrait être mauvais Pourquoi il passe toujours
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Complexité du temps** *Aucun* – l'algorithme est optimal pour les contraintes.
**Mémoire-empreinte**= Très bas – seulement quelques centaines d'entiers stockés. *Aucun* – même raison.
**Readability** Certains intervieweurs n'aiment pas l'état statique global. La liste statique est un tour d'interview commun (lazy init). Autres
**Cas d'Edge**=Poignées `n = 106` → `766666`= Aucune – la liste précalculée couvre tous les cas. La pré-computation garantit l'exactitude. Autres
**Maintenabilité**= Un endroit («build()») pour changer la logique si le chiffre limite change. Nécessite de vous rappeler que la liste statique doit être reconstruite si les contraintes augmentent. La profondeur de récursion est minuscule, donc elle est sûre. Autres
**Testation**= Facile à tester en imprimant la liste "équilibrée".= Même.= La liste contient tous les nombres équilibrés de 1 à 7 chiffres – vous pouvez l'affirmer. Autres

> **Ligne de bottom:** L'algorithme est **rapide, robuste et très convivial**. Il n'y a pas de complexité cachée, seulement une poignée d'optimisations qui gardent la récursion triviale.



-----------------------------------------------------------------------------------

- Oui. 6. Essais des unités d ' échantillonnage (Java)

"Java
Classe publique TestSolution {
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
d'affirmer s.nextBeautifulNumber(1) == 22;
affirme s.nextBeautifulNumber(1000)== 1333;
affirme s.nextBeautifulNumber(3000)== 3133;
affirme s.nextBeautifulNumber(10)== 22;
affirme s.nextBeautifulNumber(0) == 22;
affirme s.nextBeautifulNumber(7666665) == 7666666;
Système.out.println("Tous les tests sont passés!");
}
}
«» "

N'hésitez pas à copier le test dans votre IDE – les affirmations échoueront fort si quelque chose tourne mal.



-----------------------------------------------------------------------------------

- Oui. 7. Réflexions finales – Comment utiliser ceci dans votre prochaine entrevue

* **Connais les contraintes** – La limite à 7 chiffres est l'observation clé.
* ** Expliquez les règles d'élagage** – `cnt[d] < d` et "remaining slots < need.
* **Afficher votre pré-computation** – il démontre que vous pouvez optimiser plusieurs cas de test.
* **Boîtes de bord** – zéro, la limite supérieure `106`, et le plus petit nombre équilibré (`22`).
* **Appliquez le code dans la langue de votre choix** – collez l'extrait, lancez et soyez prêt à discuter de la logique sur un tableau blanc.

Vous impressionnerez les intervieweurs avec une solution non seulement correcte, mais aussi efficace, évolutive et facile à entretenir.



-----------------------------------------------------------------------------------

- Oui. 8. Prendre la prochaine étape

Si vous êtes à la recherche d'un rôle **ingénieur logiciel** qui valorise les algorithmes propres, le suivi arrière et la résolution de problèmes, les techniques ci-dessus sont exactement ce que les gestionnaires d'embauche recherchent.

- Master the **Next Greater Numerically Balanced Number** pattern.
- Utiliser les extraits fournis dans **Java, Python ou C++**.
- Oui. Testez les cas de bord avant votre prochain entretien.

> ** Prêt à poser votre job de rêve? * *
> Communiquez, appliquez et apportez ces solutions prêtes à l'entrevue. Votre future équipe vous remerciera!

Bon codage !