---
titre: LeetCode 1601. Nombre maximal de demandes de transfert réalisables -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Voici trois implémentations **ready‐to‐copy** du nombre maximum de demandes de transfert réalisables (Leetcode 1601) – une dans **Java**, une dans **Python** et une dans **C++**.
Les trois utilisent une approche **backtracking + bitmask** qui garantit l'optimalité tout en maintenant l'exécution bien en dessous des limites (le nombre de demandes ≤ 16).

> **Pourquoi Bitmask?**
> Parce que `m ≤ 16`, nous pouvons représenter n'importe quel sous-ensemble de requêtes en entier 16 bits. Le dénombrement de tous les sous-ensembles `2^m` est trivial (65536` au maximum) et beaucoup plus rapide que l'exploration d'un arbre à tailler.
> Pour les plus grands `m`, il serait préférable d'effectuer un retour à l'étape de la taille (première sortie lorsque le déséquilibre net ne peut être corrigé), mais pour ce problème, le bitmask est à la fois plus simple et plus rapide.

---

#### 1.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
***
* Leetcode 1601 – Nombre maximal de demandes de transfert réalisables
* Retraçage avec dénombrement bitmask (O(2^m * n))
*/
public int maximumDemandes(int n, int[][] demandes) {
int m = demandes. longueur;
int best = 0;

// Pré-allouer un tableau pour le changement net de chaque bâtiment
int[] net = nouvelle int[n];

// Énumérer tous les sous-ensembles de demandes (0 ... (1<<m)-1)
pour (int masque = 0; masque < (1 < < m); masque++) {
Tableau.fill(net, 0);
int count = Integer.bitCount(mask); // nombre de requêtes prises
si (compte <= le meilleur) continuer; // ne peut pas battre le meilleur courant

// Appliquer le sous-ensemble
pour (int i = 0; i < m; i++) {
si ((masque & (1 << i)) != 0) {
net[requêtes[i][0]]--; // quitter le bâtiment
net[demandes[i] ][1]]++; // entrer dans le bâtiment
}
}

// Vérifiez si tous les filets sont zéro
booléen ok = vrai;
pour (int val : net) {
si (val != 0) { ok = faux; casse; }
}
si (ok) meilleur = nombre;
}
le meilleur retour;
}
}
«» "

---

#### 1.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
"""
Leetcode 1601 – Nombre maximal de demandes de transfert réalisables
Énumération bitmask (O(2^m * n)), Python 3.11
"""
def maximumDemandes(self, n: int, demandes: List[List[int]]) -> Int:
m = len(demandes)
meilleur = 0
pour masque de portée(1 << m):
net = [0] * n
cnt = masque.bit_count()
si cnt <= meilleur:
poursuivre
pour i dans la plage (m):
si masque >> i & 1:
net[demandes[i][0]] -= 1
net[requêtes[i][1]] += 1
si tous(x) 0 pour x en net):
meilleure = cnt
le meilleur retour
«» "

---

### 1.3 C++ (GNU‐C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// Leetcode 1601 – Nombre maximal de demandes de transfert réalisables
Nombre de bitmasques (O(2^m * n))
int maxDemandes(int n, vector<vector<int>>&demandes) {
int m = requests.size();
int best = 0;

pour (int masque = 0; masque < (1 < < m); ++masque) {
vecteur<int> net(n, 0);
int cnt = __constructin_popcount(masque);
si (cnt <= best) continuer; // taille

pour (int i = 0; i < m; ++i) {
si (masque et (1 << i)) {
net[requêtes[i][0]]--; // congé
net[demandes[i] ][1]]++; // entrer
}
}

bool ok = true;
pour (int x : net) si (x != 0) { ok = faux; casse; }
si (ok) meilleur = cnt;
}
le meilleur retour;
}
};
«» "

> **Conseil:**
> • Les trois codes fonctionnent en **millisecondes** sur le harnais de test Leetcode.
> • Si vous préférez une version de rétro-suivi pure (p. ex. à des fins éducatives), remplacez la boucle bitmask par un DFS récursif qui maintient un `int[] net` et le met à jour à la volée. Le tour de taille ('si (cnt <= best) return;') fonctionne toujours.

---

- Oui. 2. Article du blog

> **Titre:** *Code de cap 1601 – Nombre maximal de demandes de transfert réalisables – Un retour complet + Guide Bitmask pour les entrevues*
> **Meta Description:** Master Leetcode 1601 avec une solution de backtracking propre, une optimisation bitmask et des implémentations Java/Python/C++. Comprendre les pièges, les causes et pourquoi ce problème est important dans le codage des entrevues.

---

2.1 Introduction

Dans **entretiens d'ingénierie logiciel**, *Leetcode 1601 – Nombre maximal de demandes de transfert réalisables* est un agrafe pour tester **optimisation combinée** compétences. Le problème vous oblige à penser à:

1. ** Solde net** par bâtiment (sortie = entrée).
2. **Recherche exhaustive** de sous-ensembles de demandes (=16).
3. **Élagage suffisant** ou **dénombrement bitmask**.

Si vous pouvez résoudre cela proprement, vous impressionnerez les gestionnaires d'embauche dans les entreprises de haute technologie.

---

### 2.2 Énoncé du problème (réécrit)

On vous donne des bâtiments `n` (`0 ... n‐1`).
Chaque bâtiment abrite d'abord des employés, mais nous ne nous soucions que des changements relatifs**.
`requests[i] = [from_i, to_i]` indique qu'un seul employé souhaite passer du bâtiment `from_i` au bâtiment `to_i`.

**Objectif:**
Sélectionnez le plus grand sous-ensemble possible de demandes, comme pour **chaque bâtiment** le nombre d'employés qui quittent le bâtiment correspond au nombre d'employés qui entrent.
Autrement dit, la variation nette par bâtiment est nulle.

**Contrôles* *

- "1 ≤ n ≤ 20"
- `1 ≤ m = longueur des demandes ≤ 16'
- `0 ≤ de_i, à_i < n`

---

2.3 Approche naïve

Une solution de manuel est d'essayer chaque combinaison en utilisant la récursion:

Texte
dfs(idx, net[], nombre)
Si idx == m:
if all(net[i] == 0): best = max(meilleur, nombre)
retour
// Prendre la demande idx
net[from[idx]]--, net[to[idx]]++
dfs(idx + 1, net, nombre + 1)
// Annuler
++, net[to[idx]]--
// Sauter la requête idx
dfs(idx + 1, net, nombre)
«» "

**Pour**

- Intuitif, facile à déboguer.
- Modéliser directement les décisions.

**Cons**

- "O(2^m)" profondeur de récursion (appels "65k" dans le pire des cas) – encore très bien, mais peut être lent dans des délais serrés.
- Oui. Pas de taille sauf si vous ajoutez manuellement des vérifications (par exemple, si les autres demandes ne peuvent pas compenser un déséquilibre actuel).

---

2.4 Optimisation du bitmask (L'approche « Good »)

Parce que `m ≤ 16`, chaque sous-ensemble de requêtes peut être représenté en entier 16 bits. Le dénombrement de tous les sous-ensembles `2^m` en une seule boucle est à la fois **simple** et **fast**:

1. **Couper au-dessus de `mask`** de `0` à `(1 << m) - 1`.
2. ** Calculer** le changement net pour chaque bâtiment en itérant sur les bits définis dans la "masque".
3. **Vérifier** que tous les filets sont nuls (« O(n) » par sous-ensemble.

La complexité totale est de < < O(2^m * n) > > , c ' est-à-dire ≤ < 65k * 20 > 1.3M ' opérations primitives – bien moins de 1 seconde.

> **Pourquoi est-ce mieux? * *
> • Pas de frais généraux.
> • `mask.bit_count()` vous donne le nombre de requêtes instantanément.
> • Vous pouvez établir un sous-ensemble tôt (`si (compte <= le meilleur) continue;`).
> • Le code est presque identique entre les langues.

---

2.5 Les pièges à éviter

Piège Explication
- C'est quoi ?
Autres **Éliminer l'élagage `meilleure`**= Vérification de tous les sous-ensembles indépendamment du temps de gaspillage `compte`.== `si (cnt <=meilleure) continue;'=
**Utiliser `int[]]` pour le net dans le DFS sans réinitialisation**.Le net array doit être fraîchement effacé pour chaque masque; sinon, les sous-ensembles précédents polluent le résultat. "Arrays.fill(net, 0);" Autres
**Si `m` étaient > 20, bitmask exploserait. Utilisez alors DFS + taille. Passez au DFS récursif avec sortie anticipée. Autres
**Ignorer `n` jusqu'à 20**= Si vous utilisez un tableau de taille 20 pour le filet, vous serez bien. Pas de problème de débordement. Autres

---

2.6 Les cas du coin

1. **Toutes les demandes sont identiques** – par exemple, `[0,1],[0,1],[0,1]`.
*Solution:* Le meilleur sous-ensemble sera **even** (chaque bâtiment doit être égal). Bitmask le gère automatiquement.

2. **Chaînes circulaires** – `0→1`, `1→2`, `2→0`.
Toute seule demande ne peut satisfaire l'équilibre ; vous avez besoin de **tous les trois** ensemble.
Bitmask trouvera cela sans logique supplémentaire.

3. **Demandes avec `de == à`** – requêtes insignifiantes qui ne font rien.
Ils peuvent toujours être pris ; bitmask les inclut automatiquement dans le sous-ensemble optimal.

4. **Large `n` (jusqu ' à 20)** mais petite `m`.
Le tableau net peut être jusqu'à 20 éléments ; il est négligeable.

---

2.7 Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
Chaque appel fait des mises à jour `O(n)` → `O(2^m * n)`"" `O(n)` (réseau net) + pile de récursion `O(m)` Autres
"O(2^m * n)" sans récursion

Avec `m ≤ 16` et `n ≤ 20`, la version bitmask fonctionne en **sub-milliseconde** sur les processeurs modernes.
Si vous voulez passer au-delà de 16 demandes, passez à DFS avec la taille de branche et de lien.

---

### 2.8 Liste de contrôle des meilleures pratiques pour les entrevues

Point de contrôle
C'est pas vrai.
**Lisez attentivement l'invite** – vous n'avez besoin que de l'équilibre relatif, pas du nombre absolu d'employés. Autres
**Confirmer les contraintes** – elles guident le choix algorithmique (bitmask vs DFS). Autres
Autres **Cas de bord de test** – bâtiment unique, demande unique, toutes les demandes s'annulent. Autres
**Write helper functions** – `isBalanced(net)` garde la logique de base rangé. Autres
**Utilisez le nombre de bits intégré** (`_builtin_popcount` / `mask.bit_count()`) pour la vitesse. Autres
**Prune tôt** – skip masques dont "compte <= best".
Autres **Commentaire du code** – les intervieweurs aiment les solutions propres et lisibles. Autres

---

2.9 Harnais d'essai de l'échantillon

"Java
public statique vide principal(String[] args) {
la valeur n = 3;
[] [] req = {{0, 0}, {0, 1}, {1, 2}, {2, 0}};
System.out.println(nouvelle solution().maximumDemandes(n, req)); // → 3
}
«» "

> Lancez le même harnais en Python ou en C++ en traduisant l'extrait.
> Utilisez des énoncés **assert** ou des cadres d'essais unitaires pour couvrir les cas bord énumérés ci-dessus.

---

### 2.10 Takeaway de l'entrevue

Les meilleurs intervieweurs demandent *Leetcode 1601* parce qu'il vérifie:

- **Connaissance conjointe** – reconnaître que chaque sous-ensemble est une solution possible.
- **Échange d'espaces horaires** – choix entre DFS et bitmask en fonction de la taille des entrées.
- ** Style de codage propre** – un algorithme bien structuré avec des commentaires montre du professionnalisme.

Pratiquer ce problème vous aidera à :

- Encoder les contraintes comme *équations d'équilibre*.
- Transformez les choix récursifs en bitmasks.
- Effectuez des dénombrements rapides lorsque l'espace de recherche est petit.
- Discutez des compromis avec les intervieweurs, transformant un simple exemple de code en conversation sur l'évolutivité.

---

2.11 Conclusion et prochaines étapes

- **Clone** les extraits de code pour Java, Python et C++ dans votre IDE local.
- **Ajouter des tests unitaires** couvrant tous les cas bord :
- Pas de demandes → réponse 0.
- Toutes les demandes annulent → répondre m.
- Demandes qui ne peuvent être équilibrées → réponse 0.
- ** Expliquez votre approche** à un ami ou dans un entretien simulé.
- **Ajouter le problème** à votre liste de Leetcodes et l'utiliser comme point de discussion dans votre prochaine interview.

> ** Prêt à décrocher votre rôle d'ingénierie logicielle de rêve? * *
> Maître problèmes comme Leetcode 1601, pratiquez le code propre, et les présenter avec confiance dans les interviews. Bonne chance ! C'est ce qu'il a dit.

---

### 2.12 SEO Mots clés

- `Codage à gauche 1601 "
- `Nombre maximal de demandes de transfert réalisables "
- Algorithme "bitmask" "
- `solution de suivi arrière "
- Entretien avec un ingénieur logiciel "
- `Java 17 solution "
- Solution "Python 3" "
- Solution `C++ "
- "Codage de la pratique des entretiens "
- Problèmes de codage des entretiens d ' emploi "

N'hésitez pas à copier, adapter et publier cet article sur Medium, Dev.to, ou votre blog personnel. Les en-têtes structurés et le contenu riche en mots-clés devraient aider le rang de poste dans les recherches comme la solution Leetcode 1601, les problèmes d'entretien backtracking, ou comment résoudre le problème de demande de transfert.