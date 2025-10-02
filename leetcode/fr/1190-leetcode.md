---
titre: LeetCode 1190. Des sous-chaînes inversées entre chaque paire de parenthèses -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## 1190. **Reverser les sous-chaînes entre chaque paire de parenthèses* *
*Moyenne de LeetCode*

> **Problème** – Avec une chaîne `s` contenant seulement des lettres minuscules et des parenthèses, inverser les sous-chaînes à l'intérieur de chaque paire de parenthèses correspondante, à partir de la paire la plus interne.
> Retourne la chaîne résultante ** sans** entre parenthèses.

> **Exemples**
> `` "
> Entrée: «(abcd)»
> Produit : "dcba"
>
> Entrée: "(u(lov)i)"
> Produit: "iloveu"
>
> Entrée: "(ed(et(oc))el)"
> Sortie : "code de sortie"
> `` "

> **Constraints**
> • `1 <= longueur <= 2000`
> • `s` ne contient que des lettres anglaises minuscules et des parenthèses équilibrées.

---

- Oui. 1. Pourquoi ce problème est une mine d'or pour les entrevues

* Il vous force à penser à **structures de données nested** (une pile ou une récursion).
* Il teste votre capacité à **muter les chaînes efficacement** (en place vs. tampons supplémentaires).
* Beaucoup d'intervieweurs posent ce problème exact sur un premier tour parce que la réponse est propre, courte, et couvre quelques concepts de base.

**Mots-clés du référencement: **
- entre parenthèses inversées
- leetcode 1190 solution
- java python c++ leetcode entre parenthèses inversées
- manipulation des chaînes d'entretien
- problème de leetcode basé sur la pile
- algorithme de chaîne d'entretien d'emploi

---

- Oui. 2. La solution "Good" – Une pile classique (Python / Java / C++)

Langue Approche Temps Espace
- C'est quoi ?
Python 2-pass: construire un tableau de paires + marcher avec un drapeau de direction (O(n))
Autres Empilement itératif Java (O(n))
Pile itérative (O(n))

Voici deux variantes :

Variante Ce qu'il fait Complexité
- C'est quoi ?
**Pile itérative**=Pile itérative, poussez l'index de chaque `'('`. Lorsqu'un `')'' est trouvé, pop le dernier `'('` index, inverser le segment entre eux, et *skip* les parenthèses. **Espace** O(n) – pile + tampon de sortie. Autres
**Optimal *Jump** * Pré-calculez les paires correspondantes, puis traversez la chaîne une fois pendant que vous sautez à travers les parenthèses correspondantes et la direction de basculement. **Espace** O(n) – tableau de paires + pile. Autres

#### 1.1 Solution de piles itératives (Python)

'`python
def inverseParenthèses: str -> str:
empilé = [] # stocke des indices de '( '
res = [] # caractères finals
cur = 0 # indice courant en s

pendant que cur < len(s):
ch = s[cur]
Si ch == '(':
stack.append(cur) # n'oubliez pas où le '(' est
élif ch == ')':
début = pile.pop() # trouver sa correspondance
# inverser la sous-chaîne entre start+1 et cur-1
res.extend(reversed(s[start+1:cur]))
Sinon:
res.append(ch) # caractère normal
pour 1

retour ''.join(res)
«» "

> **Pourquoi ça marche** –
> *La pile garantit que nous jumelons toujours chaque `')` avec son **dernier** non assorti `'('`.
> En inversant la tranche `[start+1:cur]` nous défaire les parenthèses et inverser la sous-chaîne intérieure au moment exact où nous finissons de la traiter. *

Mise en œuvre de Java

"Java
Importation de java.util.*;

solution de classe publique {
publique Parentheses(String s) {
StringBuilder sb = nouveau StringBuilder();
Deque<Integer> pile = nouvelle ArrayDeque<>();

pour (int i = 0; i < s.longueur(); i++) {
c = s.charAt(i);
si c == '(') {
Le point i) est remplacé par le texte suivant:
} sinon si (c) {
int start = pile.pop(); // index de la correspondance '('
segment de chaîne = sb.substring(démarrage + 1, sb.longueur());
sb.delete(démarrage + 1, sb.longueur()); // supprimer la partie traitée
sb.insert(start + 1, new StringBuilder(segment).reverse());
} autre {
sb.annexe c);
}
}
retour sb.toString();
}
}
«» "

> **Pourquoi ça marche** –
> *Le `StringBuilder` nous permet de supprimer et d'insérer dans O(1) amorti par opération.
> La pile garde une trace de l'endroit où commence une nouvelle sous-chaîne de "Inner", de sorte que lorsqu'un `')' est rencontré, nous pouvons isoler le segment, l'inverser et le remettre. *

*## 1.3 C++ Mise en œuvre

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne inversée Parenthèses(chaîne s) {
le résultat de la chaîne;
vecteur<int> pile;
int n = s.size();

pour (int i = 0; i < n; ++i) {
si (s[i] == '(') {
les données suivantes sont disponibles:
} sinon si (s[i] == ')') {
int start = pile.back(); pile.pop_back();
inverse(result.begin() + début + 1, result.end());
} autre {
result.push_back(s[i]);
}
}
le résultat du retour;
}
};
«» "

> **Pourquoi ça marche** –
> *L'appel `inverse` sur la plage `string::iterator` effectue l'inversion interne à externe de manière transparente.
> En ne stockant pas les parenthèses dans `result`, nous garantissons que la chaîne finale ne contient aucune. *

---

- Oui. 2. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Readability**La solution de pile est un code de 40 lignes, facile à lire en entrevue. Autres Une approche naïve qui construit une nouvelle chaîne pour chaque renversement peut être *O(n2)*. L'utilisation de la récursion sans indice global peut prêter à confusion pour les débutants. Autres
**Performance**= O(n) temps, O(n) mémoire – optimal pour les limites données.= L'opération "inverse" à l'intérieur de la boucle pourrait être évitée par la méthode "jump", mais elle coûte peu pour n ≤ 2000. Le renversement de l'ensemble de la chaîne en place est possible, mais ajoute de la complexité avec deux pointeurs. Autres
En Java, `StringBuilder.reverse()` mute le constructeur – rappelez-vous de cloner si vous avez besoin de l'original. Autres

---

- Oui. 3. Solution optimum pour le jump (O(n)) – 2 passes

Cette méthode est un favori parmi les problèmes de LeetCode.

'`python
def inverseParenthèses: str -> str:
n = len(s)
couple = [0] * n
pile = []

# 1er passage – carte d'index des paires de construction
pour i, ch dans le(s) énuméré(s):
Si ch == '(':
pile.annexe(i)
Sinon: # ch == ') '
j = pile.pop()
couple[i] = j
couple[j] = i

res = []
i = 0
étape = 1
alors que i < n:
si s[i] dans "()":
i = paire[i]
Étape = -étape
Sinon:
res.append(s[i])
i += étape
retour ''.join(res)
«» "

**C++**

'`cpp
chaîne inverseParentheses(chaîne s) {
int n = s.size();
le vecteur<int> paire(n);
Pile <int> m;
pour (int i = 0; i < n; ++i) {
si (s[i] == '(') st.push(i);
Sinon si (s[i] == ') {
int j = m. top(); st.pop();
couple[i] = j;
couple[j] = i;
}
}

la chaîne rés;
pour (int i = 0, d = 1; i < n; i += d) {
si (s[i] == '('"s[i] == ') {
i = paire[i];
d = -d;
} autre {
res.push_back(s[i]);
}
}
retour rés;
}
«» "

**Java**

"Java
solution de classe {
publique Parentheses(String s) {
int n = s.longueur();
int[] paire = nouvelle int[n];
Stack<integer> m = nouveau Stack<>();

pour (int i = 0; i < n; i++) {
si (s.charAt(i) == '(') st.push(i);
sinon si (s.charAt(i) == ')') {
int j = st.pop();
couple[i] = j;
couple[j] = i;
}
}

StringBuilder sb = nouveau StringBuilder();
pour (int i = 0, d = 1; i < n; i += d) {
c = s.charAt(i);
si (c) {
i = paire[i];
d = -d;
} autre sb.append(c);
}
retour sb.toString();
}
}
«» "

---

- Oui. 4. Récapitulation de la complexité

Variante Temps Espace
- C'est quoi ?
Empil/builder (première solution)
"Jump" à deux passages (optimal)

Les deux fonctionnent confortablement sous les limites de LeetCode (`n ≤ 2000`). Pour les entrées plus importantes, la méthode de saut est légèrement plus rapide parce qu'elle effectue une traversée linéaire *une* après le passage de prétraitement.

---

- Oui. 5. Comment utiliser cette solution dans votre prochaine entrevue de travail

1. ** Expliquez d'abord l'intuition. **
Parce que les parenthèses sont imbriquées, on peut les considérer comme une pile ou une récursion.
2. **Afficher le code, mais ne pas le remettre. **
*Parcourez l'utilisation de la pile et pourquoi nous supprimons les parenthèses. *
3. ** Mention des compromis.**
*Stack vs. récursion vs. saut à deux passages – chacun a son propre coût de lisibilité. *
4. **Demander une question complémentaire. **
Et si la corde n'était pas équilibrée ? Comment le détecteriez-vous ?

Un candidat fort finira en **moins de 5 minutes**, puis étendra la discussion à des problèmes d'analyse plus génériques.

---

- Oui. 6. Pensée finale

Le problème des parenthèses inverses est une voie d'accès** dans le monde des algorithmes de chaînes de caractères linéaires*. Maîtrisez-le, et vous vous sentirez confiant à l'égard d'un large éventail de questions d'entrevue impliquant ** délimiteurs équilibrés, renversement substring, et deux-pointer tours**.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

**Préparé par**
*Votre assistant de codage ami*

---
**Mots clés pour le référencement**: `solution de pile inverse entre parenthèses, algorithme de saut optimal, manipulation de chaîne d'entretien, algorithme basé sur la pile, problème de chaîne de LeetCode, pratique de codage d'entretien d'emploi'.