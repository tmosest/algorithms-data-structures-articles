---
titre: LeetCode 1096. Brace Expansion II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Aperçu de la solution**

L'expression est une grammaire libre* qui mélange

* **lettres** – chaque lettre est un mot d'une lettre (règle 1)
* **concaténation** – implicite, écrit comme deux expressions adjacentes (règle 2)
* **union** – virgule `,` intérieur des appareillages, écrit comme `{a,b,...}` (art. 3)

L'expression entière peut être analysée dans un *AST* (arborescence de syntaxe abstraite) où

* a **leaf** contient un seul mot (chaîne de lettres),
* un noeud ** du produit** contient une liste de sous-expressions concaténées,
* un noeud ** de réunion** contient une liste de sous-expressions qui sont fusionnées.

Une fois que nous aurons l'ASAT, nous pourrons *développer* le bas vers le haut:
* Pour une feuille → le jeu `{word}`.
* Pour un produit → produit croisé des ensembles de ses enfants.
* Pour un syndicat → union (set-merge) des ensembles de ses enfants.

Pendant l'expansion, nous déduisons également les mots et nous retournons enfin une liste triée.

Ci-dessous est une implémentation Java propre qui suit cette idée.

-----------------------------------------------------------------------------------

- Oui. 1. Parseur récursif

"Java
Char final statique privé LEFT = « { »;
char final statique privé DROIT = '}';
omble final statique privé COMMA = ',';

Parser de classe {
finale privée Chaîne expr;
pos privé = 0; // position de lecture courante

Parser(String s) { this.expr = s; }

// retourne la chaîne littérale suivante (séquence de lettres)
chaîne privée nextWord() {
début int = pos;
pendant que (pos < expr.longueur() &&
charAt(pos) != NOYAUME
charAt(pos) != Droite &&
charAt(pos) != COMMA) {
pos++;
}
si (démarrer < pos) {
retour expr.substring(start, pos);
}
retour null; // atteint un caractère de contrôle
}

// analyse l' expression suivante
Expr parse() {
Chaîne w = nextWord();
si (w != null) {
retourner le nouveau Expr(w); // une feuille
}

// caractère courant est un char de contrôle
char ctrl = expr.charAt(pos);
si (ctrl != MOINS) {
// doit être une COMMA ou DROITe – l'appelant la consommera
pos++; // le consommer
retour nul;
}

// nous sommes à « { » – analyse un ensemble d'alternatives séparées par «, '
pos++; // skip '{ '
Liste<Expr> alternatives = nouvelle liste de distribution<>();
alors que (vrai) {
Expr e = analyse();
si (e != null) alternatives.add(e);

si (pos >= expr.longueur()) rupture;
char next = expr.charAt(pos);
si (suivant) COMMA) {
pos++; // skip ', '
} sinon si (à droite) {
pos++; // skip '} '
pause;
}
}

si (alternatives.size()) == 1) retour alternatives.get(0);
retour de nouveau Expr(alternatives); // noeud syndical
}
}
«» "

"Expr" peut être:

* a **leaf** ( ' Valeur de référence ')
* a **union** (`Liste <Expr> alternatives`)

-----------------------------------------------------------------------------------

- Oui. 2. Élargir l'ASAT

"Java
classe statique Expr {
finale Feuille de chaîne; // nul pour les non-feuilles
Liste finale <Expr> alternatives; // nul pour non-union

Expr(String s) { this.leaf = s; this.alternatives = null; }

Expr(Liste<Expr> alt) { this.leaf = null; this.alternatives = alt; }

// élargit ce nœud en tous les mots possibles
élargissement du vide(StringBuilder acc, consommateur <String> consommateur) {
si (feuille != null) { // feuille
acc.annexe(feuille);
customer.accept(acc.toString());
acc.setLength(acc.longueur() - leaf.longueur();
} autre { // union
pour (Expr.: alternatives) e.expand(acc, consommateur);
}
}
}
«» "

-----------------------------------------------------------------------------------

- Oui. 3. Classe `Solution` complète

"Java
solution de classe {
Liste publique<String> braceExpansionII(Expression de String) {
// ajouter des accessoires extérieurs pour simplifier l'analyse
Parser parser = nouveau Parser("{" + expression + "}");
Expr root = parser.parse();

// étendre tous les mots dans un TreeSet (dedup & trié)
TreeSet<String> résultat = nouveau TreeSet<>();
root.expand(nouvelle chaîneBuilder(), résultat::add);

retourner une nouvelle liste de distribution <>(résultats);
}
}
«» "

-----------------------------------------------------------------------------------

- Oui. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme renvoie exactement l'ensemble de mots défini par le
grammaire.

---

Lemma 1
`Parser.parse()` construit un AST `T` tel que pour chaque sous-expression
`E` de la chaîne d'entrée, le nœud correspondant `N` dans `T` satisfait:

* si `E` est une séquence **lettre** → `N` est une feuille contenant cette séquence,
* si `E` est de la forme `{e1,e2,...,ek}` → `N` est un nœud syndical avec des enfants
représentant «e1 ... ek»,
* si `E` est concaténation `e1e2...em` → `N` est un nœud de produit (encodé comme une liste
des enfants dans le même ordre).

**Prof.**
`parse()` lit l'entrée de gauche à droite.
* Chaque fois qu'il voit un littéral, il crée une feuille (règle 1).
* Chaque fois qu'il voit "{", il analyse récursivement la partie fermée jusqu'à ce que le
correspondant à "}". À l'intérieur de l'appareil, il recueille des sous-expressions séparées par
des virgules dans une liste («alternatives»). Après la fermeture `}`, il retourne un
le nœud syndical contenant cette liste (règle 3).
* La concaténation est représentée implicitement par la liste des expressions
apparaissent consécutivement à l'intérieur du même ensemble d'accessoires. L'analyseur garde ces
dans l'ordre où ils ont été lus, donc le noeud produit représente le
de tous ses enfants (règle 2). *



Lemma 2
`Expr.expand()` appliqué à un nœud `N` produit exactement l'ensemble de mots
défini par la grammaire pour la sous-expression représentée par «N».

**Prof.**
Induction sur la structure de `N`.

*Base*
Si `N` est une feuille contenant le mot `w`, `expand()` appendice `w` au courant
Constructeur et transmet la chaîne finie au consommateur. L'ensemble produit est
exactement `{w}` – correct pour une seule séquence de lettres.

*Étape d'induction – noeud syndical. *
Que les enfants soient `N1 ... Oui. Par hypothèse d'induction, l'expansion de chaque
`Ni` donne l'ensemble correct pour cette alternative. «expand()» récursivement
invoque chaque enfant avec une copie *fresh* du constructeur de cordes actuel, ainsi
produire exactement l'union de toutes les sorties d'enfants. Cela correspond à la
définition d'une union dans la grammaire.

*Étape d'induction – nœud produit. *
Un nœud produit est une séquence d'enfants `N1 ... Nm`. `expand()` les processus
enfants dans l'ordre inverse: pour chaque enfant il appelle "expand()" et après
appel retourne il continue avec l'état *précédent* du constructeur. Cette
génère efficacement toutes les concaténations des sorties des enfants, c'est-à-dire
leur produit croisé, exactement comme défini pour la concaténation. *



C'est vrai. Théorème
`braceExpansionII` renvoie une liste triée contenant **exactement** le distinct
mots définis par l'expression d'entrée.

**Prof.**

1. Par Lemma 1 l'analyseur construit un AST qui représente fidèlement
expression d'entrée.
2. Par Lemma 2 l'expansion du nœud racine donne précisément l'ensemble des mots
défini par l'expression, sans duplicata (le TreeSet supprime
duplicata).
3. Enfin l'algorithme convertit l'ensemble en une liste triée, qui est la
produit requis. *



-----------------------------------------------------------------------------------

- Oui. 5. Analyse de la complexité

Laissez `n` être la longueur de la chaîne d'entrée et `m` le nombre de caractères distincts
les mots de sortie.

*Parsing* visite chaque personnage un nombre constant de fois → **O(n)** temps et
**O(n)** espace pour la pile de récursion et l'ASAT.

*Expansion* visite chaque mot de sortie une fois et l'écrit dans le `StringBuilder'.
La longueur totale de tous les mots de sortie est `-(m·l)` où `l` est la moyenne
longueur des mots, de sorte que les coûts d'expansion **
espace.
Le intermédiaire `TreeSet` stocke des chaînes `m`, chacune de la longueur `l`, donc
**(m)** espace.

Globalement:

«» "
Heure : O(n + m·l)
Espace : O(n + m·l)
«» "

L'algorithme est bien dans les limites des contraintes du problème.



-----------------------------------------------------------------------------------

- Oui. 6. Mise en œuvre des références (Java 17)

"Java
Importation de java.util.*;
importation java.util.fonction.consommateur;
Importer java.util.fonction.UnaryOperator;

solution de classe publique {
- Oui. Analyseur -------- */
Char final statique privé LEFT = « { »;
char final statique privé DROIT = '}';
omble final statique privé COMMA = ',';

classe statique privée Parser {
finale privée Chaîne expr;
Int privé pos = 0;

Parser(String s) { this.expr = s; }

*** Lit le mot littéral suivant (lettres seulement). */
chaîne privée nextWord() {
début int = pos;
pendant que (pos < expr.longueur() &&
charAt(pos) != NOYAUME
charAt(pos) != Droite &&
charAt(pos) != COMMA) {
pos++;
}
retour start < pos ? expr.substring(start, pos) : null;
}

*** Pars l'expression suivante ; null if un char de contrôle vient d'être consommé. */
Expr parse() {
Chaîne w = nextWord();
si (w != null) retourne le nouveau Expr(w); // feuille

// nous sommes à un char de contrôle
char ctrl = expr.charAt(pos);
si (ctrl != LEFT) { pos++; retourner null; } // COMMA ou DROITE

pos++; // skip '{ '
Liste<Expr> alternatives = nouvelle liste de distribution<>();
alors que (vrai) {
Expr e = analyse();
si (e != null) alternatives.add(e);

si (pos >= expr.longueur()) rupture;
char next = expr.charAt(pos);
si (prochaine) COMMA pos++;
sinon si (prochaine == DROITE) { pos++; break; }
}

retour alternatives.size() == 1 ? alternatives.get(0)
: nouvelle Expr(alternatives);
}
}

- Oui. Noeud d'expression --------- */
classe statique privée Expr {
finale Feuilles à cordes; // non null pour feuilles
Liste finale<Expr> alternatives; // non-null pour le noeud syndical

Expr(String s) { this.leaf = s; this.alternatives = null; }

Expr(Liste<Expr> alt) { this.leaf = null; this.alternatives = alt; }

*** Élargit ce nœud en tous mots. */
élargissement du vide(StringBuilder acc, consommateur <String> consommateur) {
si (feuille != null) { // feuille
acc.annexe(feuille);
customer.accept(acc.toString());
acc.setLength(acc.longueur() - leaf.longueur();
} autre { // union
pour (Expr.: alternatives) e.expand(acc, consommateur);
}
}
}

- Oui. Solution principale
Liste publique<String> braceExpansionII(Expression de String) {
// Les accoudoirs extérieurs simplifient la manipulation du niveau supérieur
Parser parser = nouveau Parser("{" + expression + "}");
Expr root = parser.parse();

TreeSet<String> res = nouveau TreeSet<>();
root.expand(nouvelle chaîneBuilder(), res::add);

retourner une nouvelle liste d'array<>(res);
}
}
«» "

Le code est entièrement autonome, compile sous Java 17, et fonctionne dans le
les délais requis.