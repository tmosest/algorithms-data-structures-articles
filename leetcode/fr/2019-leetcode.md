---
titre: LeetCode 2019. Le score des étudiants qui résolvent l'expression mathématique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème (récapitulation courte)

> **Note des élèves en résolution de l'expression mathématique**
> On nous donne une expression mathématique simple qui ne contient que des nombres à un seul chiffre, « + » et « * ».
> Chaque élève doit évaluer l'expression ** d'abord toutes les multiplications (de gauche à droite), puis tous les ajouts (de gauche à droite)**.
>
> Le tableau `réponses` contient les réponses (non ordonnées) soumises par les élèves.
>
> * 5 points – réponse correcte.
> * 2 points – réponse qui pourrait survenir si l'étudiant a appliqué les opérateurs dans le mauvais ordre ** mais a toujours fait l'arithmétique correctement**.
> * 0 points – tout le reste.
>
> Retourne le score total.

La longueur de l'expression est ≤ 31, le nombre d'opérateurs ≤ 15 et chaque réponse est en `[0, 1000]`.
L'expression est garantie d'être syntaxiquement correcte.

---

- Oui. 2. Idée de haut niveau

Étape Ce que nous faisons
- C'est quoi ?
Calculer la bonne réponse** – évaluer les « s » avec priorité normale. Il donne la référence en 5 points. Autres
Autres **Générer *tous* résultats possibles** qui peuvent être obtenus par toute parenthèse de l'expression. Autres Si la réponse d'un étudiant est dans cet ensemble mais n'est pas la bonne, nous donnons 2 points. Autres
* ** ≤ 104. Autres

Le noyau de la solution est l'étape 2.
Parce que l'expression ne contient que des nombres à un chiffre et qu'au plus 15 opérateurs, nous pouvons énumérer en toute sécurité chaque groupe en utilisant la récursion + mémorisation (programmation dynamique à intervalles).

---

- Oui. 3. Calcul de la réponse correcte

Le moyen le plus facile est de faire le calcul comme une calculatrice :

Texte
Total = 0
current_product = premier chiffre
pour chaque opérateur et numéro suivant d
Si : '
Total += produit_courant
current_product = d
autres // o == '* '
_produit courant *= d
Total += produit_courant
«» "

complexité temporelle : **O(m)**, *m* = nombre d'opérateurs (15).

---

- Oui. 4. Générer tous les résultats possibles

4.1 Tokenise

«» "
nombres = [int(ch) pour ch en s si ch.isdigit()]
ops = [ch pour ch dans s si ch dans '+*']
«» "

Exemple: `"7+3*1*2"` → `nums = [7,3,1,2]`, `ops = ['+','*','*'']`.

4.2 Récursion des intervalles

`solve(l, r)` → *set* de toutes les valeurs qui peuvent être obtenues à partir de la sous-expression
«nums[l] op[l] nums[l+1] ... op[r] nums[r+1]».

Cas de base
«l > r» → un seul numéro → `{ nums[l]}`.

Étape récursive

«» "
résultat =
pour k dans [l ... r] // scission avant op[k]
gauche = résoudre(l, k-1)
droite = résoudre(k+1, r)
pour x à gauche:
pour y à droite:
si ops[k] == '+': result.add(x + y)
autre: result.add(x * y)
«» "

La mémorisation est essentielle – nous stockons le résultat de chaque paire `(l, r)` dans une carte de hachage.
Le nombre de sous-intervalles est O(ops2) ≤ (15)2 = 225, de sorte que le DP est minuscule.

4.3 Complexité

* Nombre d'intervalles: O(k2) où *k* = nombre d'opérateurs ≤ 15.
* Pour chaque intervalle, nous fusionnons deux ensembles ; chaque ensemble contient au plus quelques centaines d'entiers (la valeur ne dépasse jamais 109 dans l'instruction).
* Temps global: **O(k3)** dans le pire des cas – bien en dessous de 105 opérations.
* Mémoire : **O(k2)** pour la carte de mémoisation.

---

- Oui. 5. Code complet

Ci-dessous sont des solutions propres, prêtes à coller dans **Java**, **Python** et **C++**.

> **Astuce** – les trois versions utilisent l'algorithme *same*; la seule différence est la syntaxe spécifique au langage pour les hash‐maps, les séries de récursion et d'entier.

---

#### 5.1 Java 17

"Java
Importation de java.util.*;
Importer java.util.stream.*;

solution de classe {

- Oui. 1. réponse correcte
Int correct privé Réponse(String s) {
= 0;
int curProd = s.charAt(0) - '0';
pour (int i = 1; i < s.longueur(); i += 2) {
char op = s.charAt(i);
nombre int = s.charAt(i + 1) - '0';
si (op == '+') {
Total += curProd;
curProd = chiffre;
} autres { // '* '
curProd *= chiffre;
}
}
total de retour + curProd;
}

- Oui. 2. tous les résultats possibles
liste privée <entier> nombres; // nombres
liste privée <caractère> ops; // opérateurs
carte privée<String, définir<entier>> mémo;

set privé<integer> resolve(int l, int r) {
Clé de chaîne = l + ", + r;
si (memo.contientKey(key)) retourne memo.get(key);

Définir <integer> res = nouveau HashSet<>();

si (l > r) { // un seul nombre
res.add(nums.get(l));
} autre {
pour (int k = l; k <= r; k++) { // fraction avant op[k]
Définir <Intégrer> gauche = résoudre(l, k - 1);
Définir <Intégrer> droite = résoudre(k + 1, r);
pour (int x : gauche) {
pour (int y : droite) {
si (ops.get(k) == '+')
res.add(x + y);
Autre
res.add(x * y);
}
}
}
}
mémo.put(key, res);
retour rés;
}

/* ----------- API publique --------- */
score int public Des élèves(String s, réponses int[]) {
/* 1. tokenise l'expression */
nombres = Arrays.stream(s.split("(?=[+*])")).filtre(t -> !t.equals("+") && !t.equals("*")
.map(entier::parseInt).collect(Collectors.toList());
ops = s.chars()
.filter(c -> c == '+'"" c == '*')
.mapToObj(c -> (char) c)
.collecteurs.toList() ;

mémo = nouveau HashMap<>();
Définir <Intégrer> allVals = resolve(0, ops.size() - 1);

int correct = correctRéponse(s);
Total Score = 0;

pour (int ans : réponses) {
si (ans == corriger) total Score += 5;
sinon si (allVals.contient(ans)) totalScore += 2;
}
retour total Note;
}
}
«» "

---

5.2 Python 3.10

'`python
à partir de functools importer lru_cache
de taper l'importation Liste, ensemble

Solution de classe:
Def score DesÉtudiants(s: str, réponses: List[int]) -> Int:
# 1. réponse correcte
Total, cur_prod = 0, int(s[0])
pour i dans la plage (1, len(s), 2):
op, d = s[i], int(s[i+1])
si op == '+':
Total += cur_prod
cur_prod = d
Autre: # '*'
cur_prod *= d
correct = total + cur_prod

# 2. tokenise
nombres = [int(ch) pour ch en s si ch.isdigit()]
ops = [ch pour ch dans s si ch dans '+*']

# 3. Récursion mémorisé
@lru_cache(Aucun)
def resolu(l: int, r: int) -> [int] :
si l > r: # un seul nombre
retour {nums[l]}
res = set()
pour k dans la plage(l, r + 1): # fractionné avant ops[k]
gauche = résoudre(l, k - 1)
droite = résoudre(k + 1, r)
si ops[k] == '+':
res.update(x + y pour x à gauche pour y à droite)
Sinon:
res.update(x * y pour x à gauche pour y à droite)
retour res

all_vals = resolve(0, len(ops) - 1)

# 4. score étudiants
score = 0
pour les réponses :
si ans == corriger:
score += 5
elif et dans all_vals:
score += 2
retour
«» "

---

#### 5.3 C++ (17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

/* ---------------- pour la paire<int,int> -------- */
struct PairHash {
taille_t operator()(paire de const<int,int>&p) const noexception {
retour hash<int>()(p.first) ^ (hash<int>()(p.second) << 1);
}
};

solution de classe {
public:
score int Des élèves(chaîne, vecteur<int>& réponses) {
/* 1. réponse correcte */
Int total = 0, cur = s[0] - '0';
pour (int i = 1; i < (int)s.s.ize(); i += 2) {
char op = s[i];
int d = s[i+1] - '0';
si (op == '+') {
Total += cur;
cur = d;
} autres { // '* '
pour *= d;
}
}
Int correct = total + cur;

/* 2. tokenise */
vecteur<int> num;
vecteur <char> op;
pour (charc : s) {
si (isdigit(c)) num.push_back(c - '0');
sinon op.push_back(c);
}

unordered_map<pair<int,int>, unordered_set<int>, PairHash> mémo;

fonction<unordered_set<int>(int,int)> dfs = [&](int l, int r) -> unordered_set<int> {
couple<int,int> clé = {l,r};
auto it = mémo.find(key);
si (it != memo.end()) retourne->seconde;

unordered_set<int> res;
si (l > r) { // un seul nombre
(num[l]);
} autre {
pour (int k = l; k <= r; ++k) { // fraction avant op[k]
auto gauche = dfs(l, k-1);
auto droite = dfs(k+1, r);
pour (int x : gauche)
pour (int y : droite) {
si (op[k] == '+') res.insert(x + y);
sinon res.insert(x * y);
}
}
}
mémo[key] = res;
retour rés;
};

unordered_set<int> all = dfs(0, (int)op.size()-1);

/* 3. marquer les élèves */
score int = 0;
pour (int ans : réponses) {
si (ans == corriger) score += 5;
sinon si (tous.count(ans)) score += 2;
}
le score de retour;
}
};
«» "

---

- Oui. 6. Qu'est-ce qui rend la solution *bonne* ?

1. **Déterministe** – le PDD énumère *tous* groupes juridiques, donc pas de cas cachés.
2. **Extremement rapide** – même en Python nous terminons le DP en < 1 ms pour l'expression la plus défavorable.
3. **Modulaire** – le code sépare clairement les deux tâches (évaluation normale + intervalle DP).
4. **Interview-friendly** – un candidat peut expliquer l'algorithme en 5-10 minutes, écrire le squelette DP et le tester avec les exemples de cas.

---

- Oui. 7. Pièges potentiels (la partie *mauvaise*)

Que peut-on faire de mal?
- C'est quoi ?
Autres Mauvaise clé de mémo: Deux intervalles différents sont traités comme les mêmes → résultats manquants. Utilisez une clé unique – p. ex., "l,r" ou "pair<int,int>` avec un hachage personnalisé. Autres
Autres Oublier la priorité *exacte* pour la réponse à 5 points La référence à 5 points serait erronée et nous attribuerons 0 points à chaque élève. Calculer la réponse correcte séparément, ne pas réutiliser le jeu DP. Autres
Autres Retournant l'ensemble de *toutes* parenthèses *y compris* la valeur correcte pour le cas à 2 points .Une réponse correcte serait récompensée deux fois (5 + 2). Dépassez explicitement la valeur correcte lors de l'ajout de points à 2 points. Autres
Pour les expressions très longues, la pile peut déborder dans Python. Autres

---

- Oui. 8. La partie de "gugly" (pourquoi la déclaration se sent un peu alternée)

Leetcode demande parfois *tous* des valeurs mathématiquement possibles qui peuvent être obtenues en modifiant l'ordre des opérateurs.
Il s'agit essentiellement de l'énumération *Catalan* d'arbres binaires sur les opérateurs – un DP d'intervalle classique que la plupart des intervieweurs reconnaîtront comme une astuce bien connue pour les différentes façons d'ajouter des problèmes entre parenthèses.

*La prise*: nous devons **pas** traiter l'ordre de mauvaise conduite de -- comme un shuffling arbitraire des opérateurs – seuls les regroupements qui gardent l'ordre relatif des opérandes mais changent la priorité sont valables.
L'intervalle DP couvre exactement cela, mais vous devez faire attention de ne pas doubler ou manquer le résultat correct.

---

- Oui. 9. Récapitulation de la complexité

Sous-étape Complexité
C'est pas vrai.
Réponse correcte
**O(k3)** (k ≤ 15)
Autres Nombre de points **O(n)** (n ≤ 104) Autres

L'ensemble du programme fonctionne bien sous une milliseconde pour le cas de test maximal, ce qui le rend parfait pour les interviews de Leetcode et du monde réel.

---

## 10. Réflexions finales

> **Bien** – une solution propre et linéaire pour l'évaluation normale et un petit PDD pour la parenthèse exhaustive.
> **Bad** – le libellé de l'énoncé (="wrong order=" vs.="any grouping=") peut faire monter les gens; toujours demander des éclaircissements avant de coder.
> **Ugly** – la mise en œuvre de l'intervalle mémorisé DP peut sembler intimidante pour les débutants; un seul liner `@lru_cache` dans Python cache beaucoup de travail, mais il est toujours une excellente technique d'entrevue pour vous montrer comprendre la récursion + mémorisation.

Si vous préparez un entretien technique, ce problème est une vitrine parfaite de:

1. **Décomposition des problèmes** (préoccupations distinctes).
2. ** Patterns algorithmiques classiques** (Catalan DP).
3. ** Polyvalence linguistique** – vous pouvez fournir la même logique en Java, Python ou C++ avec des changements minimes.

Bonne chance, et le codage heureux!

---

*Pour plus d'informations sur les différentes façons d'ajouter entre parenthèses, consultez le Leetcode 224 et le Leetcode 241. Ces problèmes partagent la même structure sous-jacente du PDD. *

---

**Tags** : intervalle DP, récursion, mémoisation, nombres catalans, Leetcode, codage d'entrevue, parenthèse.