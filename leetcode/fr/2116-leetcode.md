---
titre: LeetCode 2116. Vérifiez si une chaîne de parenthèses peut être valide -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Problème**

On vous donne deux cordes de la même longueur

* `s` – seuls les caractères `'('` et `')''
* `locked` – une chaîne de `'0'` et `'1'`.
"verrouillé[i]] «1» signifie que «s[i]» est *fixé* – il ne peut être modifié.
"verrouillé[i]] « 0 » signifie que « s[i] » est *free* – vous pouvez le remplacer par l'un ou l'autre
`'('' ou `')'''.

Pouvez-vous changer chaque position libre pour que toute la chaîne devienne un *valable*
Une corde de parenthèses (appropriée)?

-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

* Une chaîne entre parenthèses valide doit avoir une longueur égale – sinon il est
impossible de coupler chaque ouverture avec un support de fermeture.

* En scannant la chaîne de gauche à droite, nous pouvons garder une trace de combien
nous avons vu moins les crochets de fermeture fixes.
Que ce soit "équilibre".
Chaque position libre peut être utilisée comme support d'ouverture (ou plus tard
en conclusion) – en ce moment nous savons seulement qu'il peut aider à
couvrir un déficit.

Si à un préfixe `balance + libre < 0` nous avons déjà plus de fermeture
entre crochets que nous pouvons couvrir – la chaîne ne peut jamais devenir valide.

* La même logique doit tenir lors de la numérisation de droite à gauche,
mais maintenant nous regardons les crochets de fermeture *fixed* moins l'ouverture fixe
entre parenthèses.
Lorsque le déficit des crochets de fermeture dépasse le nombre de
positions dans ce suffixe, un support d'ouverture fixe restera inégalé.

Si **les deux** passent la fin sans contradiction, nous pouvons toujours attribuer
les crochets libres d'une manière que la chaîne finale est valide.

-----------------------------------------------------------------------------------

C'est vrai. 2. Algorithme

«» "
canBeValid(s, verrouillé)
n ← longueur de s
si n is impair → retourner false // une chaîne valide doit être égale

// ----- gauche → passe droit -----
solde ← 0 // fixe '(' – fixe ') '
freeLeft ← 0 // positions libres vues jusqu'à présent
pour i = 0 ... n- 1
si verrouillé[i]] '0'
gratuit Gauche ← libreÀ gauche + 1
Sinon si s[i] == '('
solde ← solde + 1
autres // s[i] == ') '
solde ← solde – 1

si solde + franc-gauche < 0
retourner false // trop fixe ')' déjà

// ----- à droite → passe gauche -----
solde ← 0 // fixe ')' – fixe '( '
libre à droite ← 0
pour i = n-1 ... 0
si verrouillé[i]] '0'
gratuit Droite ← libreDroite + 1
Sinon si s[i] ==') '
solde ← solde + 1
Autre // s[i] == '('
solde ← solde – 1

si équilibre + libreDroite < 0
retourner false // trop fixe '(' déjà

retour vrai
«» "

-----------------------------------------------------------------------------------

C'est vrai. 3. Preuve d'exactitude

Nous prouvons que l'algorithme retourne `true` si la chaîne peut être faite
valable.

---

Lemma 1
Pendant le passage de gauche à droite, pour chaque préfixe `P` de la chaîne,
`balance(P) + freeLeft(P) ≥ 0` tient *iff* il est possible de remplacer tous
positions libres à l'intérieur de `P` de sorte qu'aucun support de fermeture dans `P` ne soit décomposé
en lisant de gauche à droite.

**Prof.**

*Si c'est parti. *
Supposons que `balance(P) + freeLeft(P) < 0`.
`balance(P)` est le nombre de `'('` moins `''''' fixe dans `P`.
`freeLeft(P)` compte les positions libres, que nous pourrons décider plus tard.
Même si nous tournons **all** positions libres en `'('', le nombre net de
la fermeture des crochets dans `P` serait toujours
`- (balance(P) + freeLeft(P)) > 0`.
Par conséquent, il y aurait au moins un `''' sans égal '' – impossible.

*Seulement en partie. *
Supposons `balance(P) + freeLeft(P) ≥ 0`.
Nous pouvons attribuer `balance(P) + freeLeft(P)` des positions libres dans `P`
comme `'('`, et le reste comme `')'`.
Le solde net résultant après ce préfixe est exactement
`balance(P) + (balance(P) + freeLeft(P)) - freeLeft(P) = 0`
ou positif, de sorte qu'aucun `')'' ne peut être égalé. *



Lemma 2
Pendant le passage de droite à gauche, pour chaque suffixe `S` de la chaîne,
`balance(S) + freeRight(S) ≥ 0` détient *iff* il est possible de remplacer tous
positions libres à l'intérieur de `S` de telle sorte qu'aucun support d'ouverture dans `S` n'est inégalé
en lisant de droite à gauche.

*La preuve est symétrique à Lemma 1.*



C'est vrai. Théorème
L'algorithme renvoie `true` s'il existe un moyen de remplacer tous
positions libres de `s` de sorte que la chaîne résultante soit valide
Une corde entre parenthèses.

**Prof.**

*Si l'algorithme retourne `true`.*
Les deux passes n'ont jamais violé les inégalités, donc par Lemma 1;
Lemma 2 chaque préfixe peut être rendu exempt de `'' non apparié et de chaque
suffixe peut être rendu exempt de `'(''' non assorti.
Parce que la longueur de la chaîne est égale, le nombre total de `'('' est égal à
nombre de `')'` après avoir choisi les caractères libres de manière appropriée.
Par conséquent, une affectation complète existe et la chaîne entière peut être faite
valable.

*Si l'algorithme retourne `false`. *
L'algorithme s'arrête au premier préfixe `P` ou suffixe `S` où le
l'inégalité échoue.
Par Lemma 1 ou Lemma 2, aucune affectation des postes libres ne peut
éliminer le support non assorti dans ce préfixe/suffixe.
Par conséquent, une affectation valide pour la chaîne entière n'existe pas. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

Étapes Temps Espace supplémentaire
C'est pas vrai.
Contrôle de la longueur
Parti de gauche à droite
Droite-à-gauche
**O(n)**

-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool canBeValid(chaîne s, chaîne verrouillée) {
int n = s.size();
si (n % 2 != 0) retourner faux; // doit être égal

// gauche → droite
int bal = 0; // fixe '(' - fixe ') '
int freeLeft = 0; // nombre de positions libres vues jusqu'à présent
pour (int i = 0; i < n; ++i) {
Si (verrouillé[i]] '0')
++freeLeft;
sinon si (s[i] == '(')
++bal;
autres // s[i] == ') '
--bal;

si (bal + freeLeft < 0) retourner faux;
}

// droite → gauche
bal = 0; // fixe ')' - fixe '( '
Int freeRight = 0;
pour (int i = n - 1; i >= 0; --i) {
Si (verrouillé[i]] '0')
++droite libre;
Sinon si (s[i] == ')')
++bal;
Autre // s[i] == '('
--bal;

si (bal + freeRight < 0) retourner faux;
}

retour vrai;
}
};
«» "

-----------------------------------------------------------------------------------

C'est vrai. 6. Essai rapide

«» "
s = "(())"
verrouillé = "111111" → true // déjà valide

s = "(())"
verrouillé = "110110" → false // a fixed ')' ne peut pas être couvert

s = "())"
verrouillé = "0000" → true // assigner "()"

s = "())"
verrouillé = "000000" → faux // aucune affectation ne peut équilibrer
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus
et satisfait aux prescriptions relatives à l ' espace < < O(n) > > .