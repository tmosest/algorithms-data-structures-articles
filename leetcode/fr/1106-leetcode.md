---
titre: LeetCode 1106. Parsing A Boolean Expression -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Parsing a Boolean Expression – 1106 – Maîtrise basée sur la pile (Java / Python / C++)
*(Bon. Mauvais.) – Un guide pratique pour votre prochaine entrevue de codage. *

---

### TL;DR
- **Problème**: Évaluer une expression booléenne entièrement parente avec `t`, `f`, `!`, `&`, `=" et virgules.
- ** Solution optimale** : Algorithme linéaire de la pile d'espace qui *début-breaks* lorsque le résultat est connu.
- **Langues**: solutions prêtes à coller pour **Java**, **Python** et **C++**.
- **Blog focus**: Pourquoi l'approche de pile gagne, pièges communs, et comment en discuter dans une entrevue d'emploi.

> ** Prêt à ajouter ceci à votre portfolio? **
> Copiez le code, lancez-le contre LeetCode, et déposez l'article dans votre GitHub README.

---

- Oui. 1. Récapitulation des problèmes (Code Leet 1106)

> **Input** – Une chaîne `expression` (longueur ≤ 20 000) qui suit la grammaire:
> `` "
> expr → 't'= 'f'= '!' '(' expr ')'='&' '(' expr (',' expr)* ')='' expr (',' expr*) '
> `` "
> **Output** – La valeur booléenne (`true` / `false`) que l'expression évalue.

**Exemples**

expression réponse
C'est pas vrai.
""&(t,!(f))"""""
"(f,t,f)" "(f,t,f)"
(f,f,f))

---

- Oui. 2. Pourquoi une pile est le choix naturel

1. **Depth‐first nature** – Chaque opérateur s'applique à la sous-expression *next* en miroir de l'ordre poussoir/pop de la pile.
2. **Pas de pile de récursion** – La récursion sur une chaîne de 20 000 caractères peut atteindre les limites de récursion JVM / Python.
3. **Désormais terminé** – Pour `&` nous pouvons nous arrêter dès que nous voyons `f`; pour `=` dès que nous voyons `t`.

> **Connaissance clé**: *Il suffit de garder les opérateurs et les valeurs d'opérande sur la pile. *

---

- Oui. 3. L'algorithme des piles optimisé (temps O(n), espace O(n))

«» "
pour chaque char c en expression
si c == ',' ou c == '(' → ignorer
Sinon, si c dans { 't', 'f', '!', '&', '='} → pousser(c)
sinon si c == ')' → évaluer la sous-expression
«» "

**Évaluation de la sous-expression* *

Texte
hasTrue = faux
hasFalse = faux
alors que le dessus de la pile est 't' ou 'f'
-> valeur
a Vrai= (val= 't')
hasFalse= (val= 'f')

op = pop() // opérateur est maintenant en haut

Si op == '!':
push('t' if not hasTrue other 'f') // !x: true seulement si x est faux
élif op == « & » :
push('f' si hasFalse autre 't') // & : false si un opérande est false
Sinon : // op == ' '
push('t' if hasTrue other 'f') //= : vrai si un opérande est vrai
«» "

La valeur finale sur la pile est la réponse.

> **Pourquoi tôt? * *
> Pour `&`, dès que `hasFalse` devient `true` nous pourrions sauter le reste des valeurs, mais la boucle simple le fait déjà dans quelques autres opérations.
> La même idée s'applique pour `="'. Le gain est marginal par rapport à la complexité supplémentaire du code, donc nous le gardons simple.

---

- Oui. 4. Code

Voici des extraits complets et compilables pour Java, Python et C++. Chacun suit la logique exacte décrite ci-dessus.

#### 4.1 Java

"Java
Importer java.util. - ArrayDeque;
Importer java.util. Deque;

solution de classe publique {
public booléen parseBoolExpr(Expression de la chaîne) {
Deque<Caracter> pile = nouvelle ArrayDeque<>();

pour (charc : expression.toCharArray()) {
si (c) continue;
si (c) c) c) c) c))
le point c) est remplacé par le texte suivant:
} sinon si (c) {
le booléen a Vrai = faux;
booléen aFalse = faux;
pendant que (stack.peek() != '!' && stack.peek() != '&' && stack.peek() != ''') {
val char = pile.pop();
si (val == 't') aTrue = true;
sinon si (val == 'f') aFalse = true;
}
char op = pile.pop(); // opérateur
char res;
Si (op) {
res = hasTrue ? 'f' : 't'; // !x
} sinon si (op) {
res = hasFalse ? 'f' : 't'; // &x
} autres { // ' '
res = hasTrue ? 't' : 'f'; //=x
}
empilé.pouss;
}
}
retour pile.peek() == 't';
}
}
«» "

4.2 Python

'`python
à partir de collections import deque

Solution de classe:
def parseBoolExpr(self, expression: str) -> C'est vrai.
m = deque()
pour ch en expression:
si ch dans ',(':
poursuivre
Si ch in ('t', 'f', '!', '&', ''):
Annexe(ch)
élif ch == ')':
has_true = has_false = Faux
tandis que st[-1] ne se trouve pas ('!', '&', ''):
Val = s.pop()
Si la valeur == 't':
a_true = Vrai
Autre: # val == 'f '
has_false = Vrai
op = st.pop()
Si op == '!':
st.append('t' si non a_true autre 'f')
élif op == « & » :
st.append('f' si has_false autre 't')
Autre : # '''
st.append('t' if has_true autre 'f')
retour st[-1] == 't'
«» "

### 4.3 C++

'`cpp
solution de classe {
public:
parseBoolExpr(expression de chaîne) {
vectorielle<char> m; // utiliser vectorielle comme pile pour la vitesse
pour (charc : expression) {
si (c) continue;
Si (c) : "t" : "f" : "c" : "c" : "c" : "c" : "c" :
st.push_back(c);
autres si (c) {
bool hasTrue = false, hasFalse = false;
alors que (!st.vide() && st.back() != '!' && st.back() != '&' && st.back() != ''') {
val de char = st.back(); st.pop_back();
si (val == 't') aTrue = true;
autrement a Faux = vrai;
}
char op = st.back(); st.pop_back();
char res;
si (op == '!') res = hasTrue ? 'f' : 't';
sinon si (op == '&') res = hasFalse ? 'f' : 't';
sinon res = hasTrue ? 't' : 'f'; // ' '
st.push_back(res);
}
}
retour st.back() == 't';
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps (une passe) et **O(n)** espace auxiliaire (la pile).

---

- Oui. 5. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Correctness**= Fonctionne pour toutes les entrées valides, passe linéaire.= Aucune – l'algorithme est simple et robuste. Oublier de sauter des virgules ou entre parenthèses → empiler la corruption. Autres
**Complexité** Aucun. Autres
**Readability**=Push/pop clair, un bloc logique.= Mineur : l'utilisation de drapeaux booléens ('hasTrue', 'hasFalse') peut sembler inconnue. Une solution basée sur des piles peut être plus difficile à saisir pour les novices; la récursion est plus intuitive. Autres
**Cas d'escroquerie** Aucune expression comme `"!(t)"` → doit traiter `!` comme un simple correctement. Autres
**Interview Talk**= Expliquez la terminaison précoce, la métaphore de la pile, pourquoi on ignore les virgules. Éviter d'optimaliser trop les boucles de rupture précoce; cela peut confondre l'intervieweur. Ne **pas** mentionner `ArrayDeque` dans l'interview Java 8; utiliser `Stack` ou `ArrayList` pour la clarté. Autres
**Production Ready**= Nettoyez, testez et compilez.== Aucune.= Ajouter des logs de débogage ou des piles d'impression après chaque opération peut gonfler l'exécution. Autres

---

- Oui. 6. Alternative : Descente récursive (moins optimale pour les entrevues)

Une récursion naïve :

'`python
parse(expr, i):
si expr[i] dans 'tf':
retour expr[i] == 't', i+1
o = expr[i]
i += 2 # sauter '( '
résultats = []
alors que Vrai:
val, i = analyse(expr, i)
résultats.annexe(val)
si expr[i] == ')':
i += 1
pause
i += 1 # sauter ', '
Si op == '!':
retour non résultats[0], i
élif op == « & » :
retourner tous(résultats), i
Autre : # '''
retourner n'importe quel(résultats), i
«» "

> **Pourquoi l'éviter? **
> - Complexité cachée dans la profondeur de récursion ("O(n)" dans le pire des cas.
> - Plus difficile à illustrer.
> - Pour les langues comme Java/Python, la profondeur de récursion > 10 000 peut s'écraser.

---

- Oui. 7. Points de discussion pour votre entrevue de travail

1. **Cadre de problèmes** – reformuler la grammaire, clarifier le cas unique `t`/`f`.
2. **Pourquoi linéaire?** – Big-O : une structure transversale, aucune structure de données supplémentaire au-delà d'une pile.
3. **Exemple de sauvegarde** – montrer comment chaque `(` pousse le contexte, chaque `)` pops contexte.
4. **Termination précoce** – mettre en évidence `&` vs `=".
5. ** Preuve de complexité** – mention que chaque caractère est traité une fois.
6. **Tests** – donner des exemples d'essais aux limites (`"t"`, `"&(t)"`, `"!(t)").
7. **Scalabilité** – 20 k caractères → récursion peut échouer, la pile est sûre.

> **Astuce :** Pratiquez le . . . . avec un tableau blanc ou un débogueur IDE, afin de montrer visuellement l'évolution de la pile.

---

- Oui. 7. Enveloppage

- **Algorithme de positionnement**: La solution la plus rapide, sûre et conviviale pour LeetCode 1106.
- **Code**: Fourni pour **Java**, **Python**, **C++** – copier, coller et exécuter.
- **Article**: Ce billet de blog est SEO-friendly pour le code 1106, l'expression booléenne, l'algorithme d'emplacement, l'O(n), la discussion d'entretien.

Autres ** Prendre des mesures** – Affichez le code dans votre dépôt, ajoutez l'article à votre README et partagez-le sur LinkedIn ou Twitter.

Bonne chance, et que votre pile reste équilibrée!

---

Références

1. Problème de LeetCode 1106 – Expression booléenne*.
2. G. H. Cormen et al., *Algorithmes*, 3e éd., Chapitre 6 (Stacks and Queues).

---

*Si vous avez trouvé cet article utile, mettez la repo en vedette, partagez un commentaire ci-dessous, ou contactez Twitter. Bon codage ! *