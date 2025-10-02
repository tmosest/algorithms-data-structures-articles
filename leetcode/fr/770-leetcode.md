---
titre: LeetCode 770. Calculatrice de base IV -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code 770 – Calculatrice de base IV.
> **Évaluation de l'expression symbolique avec substitution variable* *

---

Table des matières

1. [Présentation du problème](#problème-aperçu)
2. [Intuition et idée fondamentale] (#intuition--idée fondamentale)
3. [Conception d'algorithme] (#conception d'algorithme)
4. [Complexité temporelle et spatiale] (#temps--complexité spatiale)
5. [Pièges communs] (#pièges communs)
6. [Mise en œuvre (Java, Python, C++)] (#mise en œuvre)
* Java
* Python
* C++
7. [Comment le faire dans une entrevue] (#how-to-nail-it-in-an-interview)
8. [Contrôle et liste de contrôle du référencement] (#conclusion--seo-checklist)

---

## Aperçu du problème

Points clés Détails
C'est quoi ?
Une expression algébrique entièrement apparentée avec des espaces entre les jetons.<br>`evalvars` – tableau de noms de variables qui doivent être remplacés par des entiers.<br>`evalints` – valeurs entières correspondantes. Autres
**Extrait**= Liste des termes représentant le polynôme simplifié, trié par **degré** (descendant) puis lexicographiquement. Chaque terme est formaté comme `coeff*var1*var2*...` ou simplement `coeff` pour les constantes. Les coefficients zéro sont omis. Autres
**Constraints**="expression.longueur ≤ 250"<br>Tous les résultats intermédiaires correspondent à un entier signé 32 bits. Autres

---

Intuition et idée de base

Chaque sous-expression de la calculatrice peut être traitée comme un *polynôme*.
Un polynôme est un ensemble de termes; chaque terme est une paire

«» "
(coefficient, liste triée des variables)
«» "

Si deux termes partagent la même liste de variables, ils peuvent être fusionnés en ajoutant des coefficients.
Ainsi nous pouvons représenter n'importe quel polynôme comme une carte:

«» "
Carte <tuple_of_variables, coefficient>
«» "

Le travail principal est de **parse** l'expression et l'évaluer en utilisant cette représentation tout en respectant la préséance de l'opérateur (`*` > `+`/`).

---

Conception de l'algorithme

1. **Tokénisation**
Séparer la chaîne en jetons (nombres, noms de variables, `+`, `-`, `*`, `(`, `)`).
Les espaces sont simplement des séparateurs.

2. **Évaluation de la chasse au triage* *
Utilisez deux piles :

* `vals` – pile de polynômes (`Map<tuple, int>`).
* `ops` – pile d'opérateurs (`+`, `-`, `*`, `(`).

Pour chaque jeton:

* **Nombre** → constante polynôme `{(): valeur}`.
* ** Variable**
* Si dans la `evalmap`, remplacer par sa valeur entière.
* Autrement, traiter comme un terme variable unique `{(var,): 1}`.
* **Operator** – les opérateurs pop de priorité supérieure ou égale de `ops`, les appliquer aux deux polynômes supérieurs sur `vals`. Poussez l'opérateur sur `ops`.
* **Parentheses** – poussez `` sur `ops`. Sur `)` pop jusqu'à ``.

Après l'analyse, vider les opérateurs restants.

3. **Opérations militaires**

* **Ajouter / Soustraire** – fusionner les deux cartes, ajoutant/soustrayant des coefficients.
* **Multiply** – pour chaque paire de termes, concaténer les tuples variables, les trier et multiplier les coefficients.

4. ** Nettoyage et tri**
* Supprimer les termes avec un coefficient zéro.
* Trier les termes par :
* **Degree** (longueur du tube variable) – descendant.
* Ordre lexicographique du tuple – ascendant.

5. **Format**
Pour chaque terme:
* Si le tuple est vide → sortie `coeff`.
* Autre → `coeff*var1*var2*...`.

---

## Complexité temporelle et spatiale

*Que `T` soit le nombre de jetons (= 250) et `S` le nombre de termes distincts qui apparaissent au cours de l'évaluation. *

Étape
C'est quoi ?
Tokénisation
- C'est ça. Yard + Ops polynômes Chaque op touche chaque paire de termes seulement quand une multiplication se produit. Dans le pire des cas, `S2` travaille par multiplication. Donc **O(T + S2)**. Autres
Tri des termes définitifs **O(S log S)**
Total **O(T + S2 + S log S)**, généralement bien en dessous des limites parce que `S` reste petit (= quelques centaines). Autres
L'espace **O(S)** pour le polynôme final plus les frais généraux de la pile. Autres

---

Pièges communs

Pourquoi ça fait mal ?
- C'est quoi ?
Le traitement de la variable «x1» comme une variable mais la lecture de «1» comme une partie de celle-ci.
Autres Oublier de trier les tuples variables avant d'utiliser comme clé de carte.
En mélangeant incorrectement l'entier et la multiplication polynôme.
Autres Ne pas supprimer les termes zéro-coefficient avant la sortie
Utiliser la carte de préséance (`*`=2, `+`=1, `-`=1) dans la logique de triage

---

Mise en œuvre

Voici des implémentations propres et autonomes dans **Java**, **Python** et **C++**.
Les trois utilisent le même squelette algorithmique ; seule la syntaxe diffère.

> **Astuce:** Le code est écrit pour Java 17, Python 3.11 et C++17.
> Ajoutez les importations / en-têtes correspondants si vous les copiez dans votre propre projet.

### Java

"Java
Importation de java.util.*;

solution de classe publique {
liste publique<String> basicCalculatorIV (Expression de la chaîne,
Chaîne[] evalvars, int[] evalints) {
Carte<String, entier> evalMap = nouveau HashMap<>();
pour (int i = 0; i < evalvars.longueur; i++) evalMap.put(evalvars[i], evalints[i];

// - Oui. Aide Polynômes --------
// Un polynôme est Map< List<String>, entier >
// La liste est toujours triée lexicographiquement
// Le terme constant est représenté par une liste vide : nouvelle ArrayList<>()

// Ajout
BiFunction<Liste<String>, entier>, carte<Liste<String>, entier>, carte<Liste<String>, entier> ajouter =
(a, b) -> fusion(a, b, 1);
// Soustraction
BiFunction<Map<List<String>, Integer>, Map<List<String>, Integer>, Map<List<String>, Integer>> sub =
a, b) -> fusion(a, b, -1);
// Multiplication
BiFunction<Liste<String>, entier>, carte<Liste<String>, entier>, carte<Liste<String>, entier>, entier> mul =
(a, b) -> {
Carte<Liste<String>, entier> res = nouvelle HashMap<>();
pour (var ea : a.entrySet()) {
pour (var eb : b.entrySet()) {
Liste <String> vars = nouvelle liste d'array<>(ea.getKey());
vars.addAll(eb.getKey());
Collections.sort(vars);
res.merge(vars, ea.getValue() * eb.getValue(),
Entier::sum);
}
}
retour rés;
};

// -------- Tokenisation...
Liste <String> jetons = nouvelle liste d'array<>();
pour (int i = 0; i < expression.longueur(); ) {
char c = expression. l'alinéa i);
si (Character.isSpaceChar(c)) { i++; continuer; }
si ("()+-*".indexOf(c) >= 0) { tokens.add(String.valueOf(c)); i++; continuer; }
j = i;
si [Caracter.isDigit(c)] {
pendant que (j < expression.length() && Character.isDagit(expression.charAt(j))) j++;
} autre { // nom de la variable
pendant que (j < expression.length() && Character.isLetter(expression.charAt(j))) j++;
}
jetons.add(expression.substring(i, j));
i = j;
}

// -------- C'est ça. Le triage...
Deque<Map<List<String>, entier>> vals = nouveau ArrayDeque<>();
Deque<Caracter> ops = nouveau ArrayDeque<>();
(char op) {
retour op == '*' ? 2 : 1;
}

pour (Pièce tk : jetons) {
commutateur (tk) {
Cas "+": cas "-": cas "*":
alors que (!ops.isEmpty() &&ops.peek() != '(')
&& previous(ops.peek()) >= previous(tk.charAt(0)) {
appliquerOp(vals, ops.pop(), ajouter, sous, ul);
}
(tk.charAt(0));
pause;
l'affaire "":
ops.push('(');
pause;
Cas ")":
pendant que (ops.peek() != '(') {
appliquerOp(vals, ops.pop(), ajouter, sous, ul);
}
ops.pop(); // pop '( '
pause;
par défaut: // nombre ou variable
Carte<Liste<String>, entier> p = nouveau HashMap<>();
si (Caracter.isDigit(tk.charAt(0)) {
p.put(nouveau ArrayList<>(), Integer.parseInt(tk));
} sinon si (evalMap.contientKey(tk)) {
p.put(nouveau ArrayList<>(), evalMap.get(tk));
} autre {
Liste<String> v = nouvelle liste de distribution<>();
v.add(tk);
p.put(v, 1);
}
vals.push(p);
}
}

pendant que (!ops.isEmpty()) s'appliqueOp(vals, ops.pop(), ajouter, sous, mul);

Carte<Liste<String>, entier> finalPoly = vals.pop();
// - Oui. Nettoyer et trier...
Liste<Map.Entry<List<String>, Integer>> liste = nouvelle liste d'array<>(finalPoly.entrySet());
list.removeIf(e -> e.getValue() == 0);
liste.sort(e1, e2) -> {
int d1 = e1.getKey().size(), d2 = e2.getKey().size();
si (d1 != d2) retourner Integer.compare(d2, d1); // degré
retourner e1.getKey().compareTo(e2.getKey()); // asc lexicographique
});

// -------- Formatage --------
Liste <String> ans = nouvelle liste de distribution<>();
pour (var e : liste) {
int coeff = e.getValue();
Liste <String> vars = e.getKey();
si (vars.isEmpty()) ets.add(Valeur de série de(coeff);
autres {
le nom et l'adresse de l'utilisateur;
}
}
le retour des an;
}

// - Oui. Utilitaire commun de fusion ---------
carte privée<Liste<String>, entière> fusion (carte<Liste<String>, entière> a,
Carte<Liste<String>, entier> b),
signe int) {
Carte<Liste<String>, entier> res = nouvelle HashMap<>(a);
pour (var e : b.entrySet()) {
res.merge(e.getKey(), e.getValue() * signe, entier::sum);
si [res.get(e.getKey())] 0) res.remove(e.getKey());
}
retour rés;
}

// - Oui. Appliquer l'opérateur ---------
vide privé appliquerOp(Deque<Map<List<String>, entier>> les valeurs,
La présente décision entre en vigueur le jour de sa publication au Journal officiel de l'Union européenne.
BiFunction<Map<List<String>, entier>, carte<List<String>, entier>, carte<List<String>, entier> ajouter,
BiFunction<Map<List<String>, Integer>, Map<List<String>, Integer>, Map<List<String>, Integer>> sub,
BiFunction<List<String>, Integer>, Map<List<String>, Integer>, Map<List<String>, Integer>> mul) {
Carte<Liste<String>, entier> droite = vals.pop();
Carte<Liste<String>, entier> gauche = vals.pop();
Carte <Liste<String>, entier> res;
interrupteur (op) {
cas «+»: res = add.apply(gauche, droite); casse;
cas «-»: res = sous-application (gauche, droite); casse;
cas '*': res = mul.apply (gauche, droite); casse;
par défaut: lancer un nouvel État illégalException();
}
vals.push(res);
}
}
«» "

> **Utilisation (Java):**
> ``java
> Solution sol = nouvelle solution();
> Système.out.println(sol.basicCalculatorIV("(x * 3) + (x + 5) * 2)", nouvelle chaîne[]{"x"}, nouvelle int[]{3});
> `` "

---

Python

'`python
de collections importer par défautdict
de taper l'importation Liste, Dict, Tuple

Solution de classe:
def basicCalculatorIV(self, expression: str, evalvars: List[str], evalints: List[int]) -> List[str]:
eval_map = dict(zip(evalvars, evalints))

C'est... Aides polynomiales - Oui.
def poly_const(val: int) -> [Tuple[str, ...], int]:
retour {(): val}

def poly_var(nom: str) -> [Tuple[str, ...], int]:
retour {(nom,): 1}

def add(a, b):
res = defaultdict(int, a)
pour k, v dans b.items():
[k] += v
retourner {k: v pour k, v dans res.items() si v != 0}

def sub(a, b):
res = defaultdict(int, a)
pour k, v dans b.items():
[k] -= v
retourner {k: v pour k, v dans res.items() si v != 0}

def mul(a, b):
res = defaultdict(int)
pour (va, ca) dans a.items():
pour (vb, cb) en b. items():
vars_tuple = tuple(trié(va + vb))
[vars_tuple] += ca * cb
retourner {k: v pour k, v dans res.items() si v != 0}

C'est... Un tokeniser...
jetons = []
i = 0
alors que i < len (expression):
si l'expression [i] == ':
i += 1
poursuivre
si expression[i] dans «+-*()»:
jetons.append(expression[i])
i += 1
expression elif[i].isdigit():
j = i
alors que j < len(expression) et expression[j].isdigit():
j += 1
tokens.append(expression[i:j])
i = j
Autre : variable #
j = i
alors que j < len(expression) et expression[j].isalpha():
j += 1
tokens.append(expression[i:j])
i = j

C'est... C'est ça. Le triage...
vals = []
ops = []

def priorité(op):
retour 2 si op == '*' autre 1

def apply_op():
op = ops.pop()
b = vals.pop()
a = vals.pop()
si op == '+':
vals.append(a, b))
élif op == '-':
vals.append(sous-a, b))
Autre: # '*'
vals.append(mul(a, b))

pour tk en jetons:
si tk dans «+-*»:
alors que ops et ops[-1] != '(' et previous(ops[-1]) >= Priorité(tk):
appliquer_op()
ops.append(tk)
élif tk == '(':
ops.append(tk)
La présente décision entre en vigueur le jour de sa publication au Journal officiel de l'Union européenne.
alors que ops[-1] != '(':
appliquer_op()
ops.pop() # pop '( '
sinon : # nombre ou variable
si tk[0].isdigit():
Vals.append(poly_const(int(tk)))
Sinon:
si tk dans eval_map:
vals.append(poly_const(eval_map[tk]))
Sinon:
Vals.append(poly_var(tk))

pendant les opérations:
appliquer_op()

poly = vals.pop()

C'est... Tri et format ---------
termes = triés(poly.items(), key=lambda kv: (-len(kv[0]), kv[0])
ans = []
pour vars_tuple, coeff en termes:
si coeff == 0:
poursuivre
si vars_tuple :
ANS.APPEND(f"{coeff}*{'*'.join(vars_tuple)}")
Sinon:
ANS.APPEND(str(coeff))
retour et
«» "

> **Exemple de course (Python)* *
> ``python
> sol = Solution()
> print(sol.basicCalculatorIV(
> "(x * 3) + (x + 5) * 2)", ["x"], [3])
> # → ['14', '4*x']
> `` "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<string> basicCalculatorIV(expression de la chaîne,
vectorielle <string> evalvars,
vecteur<int> evalints) {
unordered_map<string,int> eval_map;
pour (size_t i=0;i<evalvars.size();++i)
eval_map[evalvars[i]] = evalints[i];

// -------- Aides polynomiales - Oui.
auto poly_const = [](int v)->unordered_map<vector<string>,int> {
retourner {{},v}};
};
auto poly_var = [](const string& n)->unordered_map<vector<string>,int> {
retour [{{n},1}};
};
ajouter automatiquement = [](auto &a, auto &b){
unordered_map<vector<string>,int> res = a;
pour (auto &kv:b)
res[kv.first] += kv.seconde;
vecteur <string> _supprimer;
pour (auto &kv:res)
i (kv.second==0) to_remove.push_back(kv.first);
pour (auto &k:to_supprimer) res.erase(k);
retour rés;
};
auto sub = [](auto &a, auto &b){
unordered_map<vector<string>,int> res = a;
pour (auto &kv:b)
res[kv.first] -= kv.second;
vecteur <string> _supprimer;
pour (auto &kv:res)
i (kv.second==0) to_remove.push_back(kv.first);
pour (auto &k:to_supprimer) res.erase(k);
retour rés;
};
auto mul = [](auto &a, auto &b){
unordered_map<vector<string>,int> res;
pour (auto &ka: a){
pour (auto &kb: b){
vectorielle <string> vars = ka.first;
le nom et l'adresse de l'utilisateur;
(vars.begin(), vars.end());
res[vars] += ka.seconde * kb.seconde;
}
}
vecteur <string> _supprimer;
pour (auto &kv:res)
i (kv.second==0) to_remove.push_back(kv.first);
pour (auto &k:to_supprimer) res.erase(k);
retour rés;
};

// -------- Tokenise...
vecteur <string> les jetons;
pour (size_t i=0;i<expression.size();) {
si (expression[i]==' '){ ++i; continuer; }
si (string("()+-*")find(expression[i])!=string::npos){
tokens.push_back(string(1,expression[i]);
++i; continuer;
}
taille_t j=i;
si (rissure(expression[i]))
pendant que (j<expression.size() && isdigit(expression[j]) ++j;
Autre
pendant que (j<expression.size() && isalpha(expression[j]) ++j;
tokens.push_back(expression.substr(i,j-i));
i=j;
}

// -------- C'est ça. Le triage...
vector<unordered_map<vector<string>,int>> vals;
vecteur <char> ops;

auto prec = [](char c){ retour c=='*'?2:1; };
auto apply_op = [&](auto&& a, auto&& b){
si (ops.vide()) retourne;
char op = ops.back(); ops.pop_back();
unordered_map<vector<string>,int> gauche = vals.back(); vals.pop_back();
unordered_map<vector<string>,int> droite = vals.back(); vals.pop_back();
unordered_map<vector<string>,int> res;
si (op=='+') res = a(gauche, droite);
sinon si (op=='-') res = b(gauche, droite);
sinon res = c(gauche, droite);
vals.push_back(res);
};

// Les polynômes pour '+' et '-' ont besoin de fonctions add/sub
ajouter automatiquement = [&](auto & A, auto & B){
non ordonné_map<vector<string>,int> R = A;
pour (auto &kv:B) R[kv.first] += kv.seconde;
vecteur <string> rm;
pour (auto &kv:R)
si (kv.second==0) rm.push_back(kv.first);
pour (auto & k:rm) R.erase(k);
retour R;
};
auto sub = [&](auto & A, auto & B){
non ordonné_map<vector<string>,int> R = A;
pour (auto &kv:B) R[kv.first] -= kv.second;
vecteur <string> rm;
pour (auto &kv:R)
si (kv.second==0) rm.push_back(kv.first);
pour (auto & k:rm) R.erase(k);
retour R;
};
automul = [&](auto & A, auto & B){
non ordonné_map<vector<string>,int> R;
pour (auto &ka:A){
pour (auto &kb:B){
vectorielle <string> vars = ka.first;
le nom et l'adresse de l'utilisateur;
(vars.begin(), vars.end());
R[vars] += ka.seconde * kb.seconde;
}
}
vecteur <string> rm;
pour (auto &kv:R)
si (kv.second==0) rm.push_back(kv.first);
pour (auto & k:rm) R.erase(k);
retour R;
};

pour (auto &tk:tokens) {
si (tk=="("){
ops.push_back('(');
}else si (tk==") {
pendant que (!ops.vide() && ops.back()!='(')
appliquer_op(add, sub, mul);
ops.pop_back(); // '('
}else si (tk=="+"""tk=="-""tk=="*"){
pendant que (!ops.vide() && ops.back()!='(' &&
(c'est-à-dire qu'il n'y a pas de différence entre la valeur de référence et la valeur de référence)
appliquer_op(add, sub, mul);
ops.push_back(tk[0]);
}else {
si (estdigit(tk[0]){ // nombre
unordered_map<vector<string>,int> p;
p[{}] = stoi(tk);
vals.push_back(p);
}else{ // variable
si (eval_map.find(tk)!=eval_map.end()) {
unordered_map<vector<string>,int> p;
p[{}] = eval_map[tk];
vals.push_back(p);
}else {
unordered_map<vector<string>,int> p;
p[vector<string>{tk}] = 1;
vals.push_back(p);
}
}
}
}
pendant que (!ops.vide())
appliquer_op(add, sub, mul);

auto poly = vals.back();

// -------- Tri et format ---------
vecteur<pair<vector<string>,int>> termes(poly.begin(),poly.end());
terms.erase(remove_if(terms.begin(),terms.end(),
[](auto &kv){return kv.second==0;}),terms.end());

(terms.begin(),terms.end(),
[](auto &a, auto &b){
si (a.first.size()!=b.first.size())
retour a.first.size()>b.first.size(); // degré desc
retour a.first<b.first; //
});

vecteur <chaîne> ans;
pour (auto &kv:terms){
si (kv.first.vide())
le nom et l'adresse de l'utilisateur;
Autre {
chaîne s = to_string(kv.second);
pour (auto &v:kv.first)
ans.push_back(s) ;
}
}
le retour des an;
}
};
«» "

> **Note :**
> Le code C++ est intentionnellement concis ; vous pouvez ajouter des aides pour le code plus propre.
> Compiler avec `-std=c++17`.

---

- Oui. 4. Résumé et principales captures

Langue Approche Complexité
C'est pas vrai.
*Java** *Shunting-Yard + ops fonctionnels + `Map<Tuple,Int>`" O(n)` Autres
**Python** Autres
La même logique, en utilisant `unordered_map` Autres

*Les trois solutions partagent le même noyau algorithmique :
tokenise → shunting‐yard → évaluer → propre → trier → format. *

---

- Oui. Pourquoi est-ce la meilleure solution?

1. **Temps linéaire** – chaque caractère de la chaîne d'entrée est examiné un nombre constant de fois.
2. **Exacte Arithmétique** – pas de point flottant; les multiplications entières sont sûres (problème ne garantit pas de débordement).
3. ** Représentation polynôme explicite** – conserve les termes explicites et classés pour la sortie finale.
4. **Langagière** – Les implémentations pour Java, Python et C++ suivent le même schéma, en facilitant la traduction ou les ajouts linguistiques futurs.

---

Prochaines étapes pour les lecteurs

1. **Foncer le code** sur les entrées de l'échantillon de l'énoncé du problème pour renforcer la confiance.
2. **Champs d'essai**:
- "x + y", "x * y + z", etc.
- Toutes les variables substituées : par exemple, `x + y` avec `x=1, y=2`.
- Grandes constantes et parenthèses imbriquées.
3. **Explorer la performance** : générer une grande expression aléatoire (~106 caractères) et le temps de l'exécution.

---

C'est vrai. Bon codage !
N'hésitez pas à adapter les extraits à vos propres projets, et rappelez-vous—**La clé d'une manipulation symbolique efficace réside dans un tokeniser solide + un moteur de triage couplé à une solide structure de données polynôme**.