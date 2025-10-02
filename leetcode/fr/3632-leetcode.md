---
titre: LeetCode 3632. Subarrays avec XOR au moins K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Description du problème – LeetCode 3632: Les subarrays avec XOR au moins K

**Contrairements**
C'est pas vrai.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Retourner le nombre total de sous-tarifs valides. Autres

> **Exemple**
> `nums = [3,1,2,3]`, `k = 2` → réponse: **6**.

---

Le bien, le mal et le mal de la solution

Aspect du bien
- C'est quoi ?
**Naïve O(n2) double boucle** 1052 opérations → impossible. Autres
**Préfixe XOR + Brute-Force** Toujours O(n2) pour le dénombrement. Toujours TLE. Autres
Autres **Binary Trie + Préfixe XOR**** **O(n · W)** (W = 32) → 3.2 × 106 ops. Facile à détecter (off‐by‐one, débordement). Autres
**L'espace**=O(n · W) pour les nœuds triés (~3 Mo). Acceptable. Autres

L'approche binaire-trie est la solution **golden** qui passe tous les tests, fonctionne assez rapidement pour les entretiens d'emploi, et démontre une compréhension profonde de la manipulation bit et des sommes préfixées.

---

Intuition et algorithme

1. **Préfixer XOR**:
«pref[i] = nombres[0] ─ ... nombres[i-1]».
XOR du sous-appel `l ... r` est égal à `pref[r+1] ' pref[l]`.

2. **Tarifs secondaires**:
Pour chaque `pref[r+1]` nous avons besoin du nombre de préfixes précédents `pref[l]` de telle sorte que
"pref[r+1] φ pref[l] ≥ k".

3. ** Trie binaire** :
Entreposez tous les préfixes précédents dans un tri où chaque noeud représente un peu (0 ou 1).
Chaque noeud garde un `cnt` de combien de nombres passent par ce noeud.
Lors de l'interrogation, nous marchons le trie du bit le plus significatif (31e) jusqu'à 0, en décidant si:
* prendre le bit opposé (assurer XOR ≥ k à ce niveau de bit), ou
* rester sur le même bit (continuer à vérifier les bits inférieurs).

4. **Complexités**:
*Temps* – O(n · 32)
*Space* – O(n · 32) pour les nœuds triés (4 × n octets 4 Mo).

---

Mise en œuvre – 3 langues

- Oui. 1. Java

"Java
importation java.io.*;
Importation de java.util.*;

solution de classe publique {
- Oui. Trie Node --------- */
classe statique privée TrieNode {
TrieNode[] enfant = nouveau TrieNode[2];
nombre int = 0;
}

- Oui. API publique --------- */
compte long publicXorSubarrays(int[] nums, int k) {
TrieNode root = nouveau TrieNode();
insert(root, 0); // préfixe vide
résultat long = 0;
préfixe int = 0;

pour (int num : nombres) {
préfixe ^= num;
résultat += requête(root, préfixe, k);
insérer(racine, préfixe);
}
le résultat du retour;
}

- Oui. Insérer un numéro dans le trie ---------- */
insertion de vide privé(racine TrieNode, int val) {
TrieNode noeud = racine;
pour (int i = 31; i >= 0; i--) {
bit int = (val >> i) & 1;
si (node.child[bit] == null) node.child[bit] = nouveau TrieNode();
noeud = noeud.child[bit];
node.count++;
}
}

- Oui. Demande : combien de préfixes donnent XOR >= k --------- */
requête longue privée(TrieNode root, int prefix, int k) {
TrieNode noeud = racine;
nombre long = 0;
pour (int i = 31; i >= 0 && noeud != Null; i--) {
int pBit = (préfixe >> i) & 1;
int kBit = (k >> i) & 1;

si (kBit == 1) { // besoin de bits opposés pour garder XOR >= k
noeud = noeud.enfant[1 - pBit];
} autre { // si le bit opposé existe, tous sont éligibles
Si (node.child[1 - pBit] != null)
nombre += noeud.child[1 - pBit].compte;
noeud = noeud.child[pBit];
}
}
si (node != null) nombre += node.count; // tous les numéros restants sont valides
le nombre de retours;
}

- Oui. Pilote pour les essais manuels rapides --------- */
public statique vide main(String[] args) lance Exception {
Solution sol = nouvelle solution();
Système.out.println(sol.countXorSubarrays(nouveau int[]{3,12,3}, 2)); // 6
Système.out.println(sol.countXorSubarrays(nouvelle int[]{0,00}, 0)); // 6
}
}
«» "

> **Pourquoi un "long"?**
> Le nombre de sous-cours peut atteindre ~5 × 109, ce qui dépasse `int`.
> Tous les comptes dans le trie sont stockés comme `int` car au plus `n` préfixes passent par un noeud.

---

- Oui. 2. Python

'`python
Classe TrieNode:
__slots__ = ("enfant", "compte")
def _init_(self):
l'enfant = [Aucun, aucun]
total = 0

Solution de classe:
Dénombrement XorSubarrays(self, nombres: list[int], k: int) -> Int:
racine = TrieNode()
_insérer(racine, 0) # préfixe vide
Res = 0
pref = 0

pour num in nums:
Préf ^= num
res += self._query(root, pref, k)
auto_insérer(root, pref)

retour res

def _insert(self, root: TrieNode, val: int) -> Aucun:
noeud = racine
pour i dans la plage(31, -1, -1):
bit = (val >> i) & 1
si noeud.child[bit] n'est pas:
noeud.child[bit] = TrieNode()
noeud = noeud.child[bit]
nombre de nœuds += 1

def _query(self, root: TrieNode, pref: int, k: int) -> Int:
noeud = racine
ans = 0
pour i dans la plage(31, -1, -1):
si le nœud n'est pas :
pause
p_bit = (préf >> i) & 1
k_bit = (k >> i) & 1
si k_bit == 1 :
noeud = noeud.child[1 - p_bit] # doit prendre le bit opposé
Sinon:
# tous les nombres avec le bit opposé satisfont déjà >=k
en cas de nœud. enfant[1 - p_bit]:
ans += noeud.child[1 - p_bit].count
noeud = noeud.child[p_bit]
en cas de nœud:
nombre de nœuds
retour et

♪ - Oui. Essai manuel rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.countXorSubarrays([3,1,2,3], 2)) # 6
print(sol.countXorSubarrays([0,00], 0)) # 6
«» "

> **Conseils de python**:
> *Utilisez `__slots__` pour réduire les frais de mémoire de nombreux nœuds triés. *
> *La boucle passe de 31 à 0 – 32 itérations seulement. *

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct TrieNode {
enfant TrieNode*[2];
int cnt;
TrieNode() { enfant[0] = enfant[1] = nulptr; cnt = 0; }
};

solution de classe {
public:
long compte long XorSubarrays(vecteur<int>& nums, int k) {
racine de TrieNode* = nouveau TrieNode();
insert(root, 0); // préfixe vide
longue rés = 0;
Int pref = 0;

pour (int num : nombres) {
ff ^= num;
res += requête(root, pref, k);
insérer(root, pref);
}
retour rés;
}

particulier:
oblique insérer(TrieNode* root, int val) {
TrieNode* noeud = racine;
pour (int i = 31; i >= 0; --i) {
bit int = (val >> i) & 1;
si (!node->child[bit]) node->child[bit] = nouveau TrieNode();
noeud = noeud->enfant[bit];
noeud->cnt++;
}
}

longue requête longue (racine TrieNode*, int pref, int k) {
TrieNode* noeud = racine;
long an = 0;
pour (int i = 31; i >= 0 && noeud; -i) {
i) et 1;
int kBit = (k >> i) & 1;

si (kBit) { // doit prendre un bit opposé
noeud = noeud->enfant[1 - pBit];
} autre { // bit opposé donne >= k
si (noeud->enfant[1 - pBit]) ans += noeud->enfant[1 - pBit]->cnt;
noeud = noeud->enfant[pBit];
}
}
si (noeud) ans += noeud->cnt; // les nœuds restants sont valides
le retour des an;
}
};

// - Oui. Pilote pour un test manuel rapide
Int main() {
Solution s;
Cout << s.countXorSubarrays({3,1,2,3}, 2) << endl; // 6
<< s.countXorSubarrays({0,00}, 0) << endl; // 6
retour 0;
}
«» "

> **Notes C++**:
> *Pré-allouer les nœuds avec `new` – l'utilisation de la mémoire reste bien en dessous de 10 Mo. *
> *Utilisez `long' pour la réponse. *
> *La boucle 32 bits («pour (int i = 31; i >= 0; --i)») garantit un temps constant par nombre. *

---

Pourquoi est-ce l'entrevue?

1. **Clean, O(1) par numéro** – LeetCode vous demande de penser au-delà de la force brute.
2. **Shows mastery of**:
* Préfixe XOR – une astuce classique pour les problèmes XOR sub-array.
* Binary Trie – une puissante structure de données pour les requêtes bit-wise.
* 64 bits entier arithmétique – gestion correcte du débordement.
3. ** Temps et espace** – Satisfait aux limites strictes (temps « O(n) », espace « O(n) »).
4. **Readability** – Commentaires, nommage cohérent et fonctions d'aide modulaire aide à la compréhension.

---

Article de blog optimisé par le SEO

### Subarrays avec XOR ≥ K – Le Bon, le Mauvais, et l'Ugly
**(Problème #3632 – 2025‐09‐26)**

> **Mots clés**: `leetcode hard`, `subarrays`, `xor`, `prefix XOR`, `biary trie`, `job interview algorithmes`, `efficace algorithme`, `C++ solution`, `Java solution`, `Python solution`.

---

Introduction

Dans le monde du codage des interviews, **LeetCode Hard** problèmes sont la vitrine ultime de brillance algorithmique.
Problème 3632 – *Subarrays avec XOR au moins K* – se trouve au carrefour de la manipulation des bits, des montants préfixés et des structures de données triées.

Si vous voulez décrocher un rôle d'ingénierie logicielle, maîtriser ce problème prouve que vous pouvez :

* Des solutions de conception qui sont à la fois **fast** et **friendly memory**.
* Traduire des idées mathématiques en code propre en plusieurs langues.
* Communiquez clairement des idées complexes, une compétence d'entrevue indispensable.

---

Déclaration du problème

> **Donné** d'un tableau «nums» de «n» entiers (0 ≤ nombres[i] ≤ 231 – 1) et d'un entier «K».
> **Tâche**: Compter tous les sous-groupes `(i ... j)` de sorte que
> `xor(nums[i..j]) ≥ K`.

L'approche naïve examine chaque sous-cours: «O(n2)».
Avec `n` jusqu`à 5 × 105, cela est impossible sur les machines d`entretien typiques.

---

- Oui. Le bon – De la force brute au temps linéaire

L'approche Temps Espace Verdict
C'est pas vrai.
Force brute (double boucle)
Préfixe XOR + hashmap
Autres **Binary Trie + Préfixe XOR**

La partie *bonne* : La solution optimale utilise **préfix XOR** pour transformer le problème en une inégalité *préfixe* qui peut être répondue en temps constant par élément en utilisant un trie **binaire**.

---

C'est pas vrai. Le mauvais – Pourquoi les tricks simples échouent

- ** Approche HashMap** : Vous pouvez compter les sous-arrays avec XOR exactement égal à une cible en stockant le préfixe XOR dans un hashmap.
Cependant, pour *au moins K*, vous devez savoir combien de préfixes donnent une plage ** de valeurs XOR** — les hashmaps ne vous donnent que des correspondances *exacte*.
- **Trier + deux points**: Fonctionne pour des sommes mais échoue pour XOR, parce que XOR n'est pas monotonique en ce qui concerne l'ordre de tableau.

Ces pièges illustrent pourquoi une solution naïve obtiendra une limite de temps dépassée.

---

C'est pas vrai. L'horrible – Pièges communs

Symptômes Correction
C'est pas vrai.
Utiliser `int` pour la réponse.
Autres Oubliant le préfixe vide, il manque des sous-arrachages qui commencent à l'index.
Erreurs de gestion du bit-ordering hors-par-un dans la logique des inégalités
"Érreur d'écoulement" ou "C++" épuisement du tas.

---

##### 6=1 Étape par étape (Java)

"Java
// 1. Insérer le préfixe vide
insérer(root, 0);

// 2. Pour chaque numéro
Préfixe ^= num; // préfixe XOR
ans += requête(root, préfixe, K); // compter les préfixes de qualification
insert(root, préfixe); // ajouter le préfixe courant pour les futures requêtes
«» "

*La fonction `query` navigue bit by bit, décide de prendre le bit opposé (pour rester ≥ K) ou compte tous les nœuds de qualification. *

---

Modèles multilingues

Nous fournissons des extraits complets et compilables dans **Java**, **Python** et **C++**.
N'hésitez pas à les copier, à les coller et à les exécuter sur votre IDE local.

Langue Fichier Complexité
- C'est quoi ?
Autres Java `Solution.java` Autres
"Python" "solution.py" "O(n)" Autres
*C++ *solution.cpp * * O(n) * Autres

---

#### # 8-

1. ** Expliquez l'intuition d'abord**: *préfixe XOR → sub-array XOR peut être exprimé en XOR de deux préfixes. *
2. **Afficher le choix de la structure des données**: *la trie binaire nous donne une recherche logarithmique (constante) sur les bits. *
3. **Parcourez un petit exemple sur le tableau blanc** pour démontrer la logique bit-by-bit.

Rappelez-vous, les intervieweurs aiment voir *penser à la volée*. Si vous frappez un snag, posez des questions claires sur l'étendue de `K` ou la distribution des valeurs d'entrée, elles peuvent suggérer une solution plus simple ou une torsion subtile.

---

Les pensées finales

Subarrays avec XOR ≥ K peut sembler intimidant, mais avec une approche systématique – préfixe XOR + trie binaire – vous le transformez en un algorithme propre, linéaire-temps.

Déposez la solution dans votre portfolio GitHub, utilisez la section discussion pour poser des questions plus approfondies et soyez prêt à en discuter dans un entretien technique.

** Bonne chance, futur ingénieur logiciel! * *

---

TL; RD

- **Problème**: Compter les sous-réseaux avec XOR ≥ K.
- **Approche optimale**: Préfixe XOR + Trie binaire.
- **Complexités**: temps "O(n)", espace "O(n)".
- **Langues**: Java, Python, C++ (code ci-dessus).
- **Valeur d'entrevue**: Démontre le raisonnement avancé au sens bit, le choix de la structure des données et la sensibilisation au rendement.

---

> **Prêt pour le prochain problème difficile? **
> Essayez le problème 3631 – *Somme maximale de subarrays avec longueur égale* – pour une torsion de programmation dynamique.

---

**Codage heureux, et peut-être vos entrevues d'emploi sont-elles sans problème!**

---

* Fin de l'article. *

---

Avec ces extraits et l'article, vous êtes équipé pour impressionner les recruteurs, as le défi dur LeetCode, et briller dans votre prochaine interview. Bonne solution !