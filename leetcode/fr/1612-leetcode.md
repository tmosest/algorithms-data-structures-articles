---
titre: LeetCode 1612. Vérifiez si deux arbres d'expression sont équivalents -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# 1612. **Vérifier si deux arbres d'expression sont équivalents** – Code + SEO-Optimized Blog

> **Objectif:**
> Compte tenu de deux arbres d'expression binaire qui ne contiennent que l'opérateur `+' et les opérandes (lettres minuscules), décider s'ils évaluent à la même expression pour *any* valeurs des variables.

> **Pourquoi est-ce important? * *
> Dans la conception du compilateur, les bibliothèques de mathématiques symboliques ou le codage d'entrevues, vous devez souvent décider si deux expressions algébriques sont équivalentes. Ce problème de LeetCode est une question d'entrevue canonique qui teste votre compréhension des traversées d'arbres, de la commutation et des compromis dans l'espace temporel.

---

- Oui. 1. Récapitulation des problèmes

* Chaque noeud interne est un opérateur `+` et a toujours **exactement deux** enfants.
* Chaque noeud de feuille est un opérande.
* Les arbres sont **valides** expression arbres (le nombre de nœuds est impair).
* **Tâche:** Retour `true` si les deux arbres sont *mathématiquement équivalents* pour chaque affectation possible aux opérandes; sinon, retour `faux`.

**Exemple**

«» "
racine1: +
/ \
a +
/ \
b c
racine2: +
/ \
+ a
/ \
b c

sortie & #160;: true
«» "

`a + (b + c)` est égal à `(b + c) + a` parce que `+` est commutatif et associatif.

---

- Oui. 2. Intuition

Parce que `+` est *commutatif* et *associé*:

1. L'ordre **** des opérandes n'a pas d'importance.
2. Le **négatif** des ajouts n'a pas d'importance.

Ainsi, deux arbres sont équivalents **iff** ils contiennent le **même multiset** des opérandes.

Il suffit donc de compter combien de fois chaque variable apparaît dans chaque arbre et de comparer les dénombrements.

Si un opérande apparaît un nombre *odd* de fois dans les dénombrements combinés, les deux arbres diffèrent (parce que cet opérande s'annulerait dans un arbre mais pas dans l'autre).

---

- Oui. 3. Algorithme

1. Créer un tableau entier `cnt[26]` (un emplacement pour chaque lettre minuscule).
2. **DFS** chaque arbre, incrémentant "cnt[operand - 'a']" quand un noeud d'opéra est visité.
3. Après avoir visité les deux arbres, vérifiez chaque `cnt[i]`.
*Le cas échéant `cnt[i]` est étrange → arbres ne sont pas équivalents. *
*Autres → ils sont équivalents. *

**Complexité* *

Motif
C'est pas vrai.
**Heure** Chaque nœud est visité une fois. Autres
**Espace** Seulement un tableau de 26 éléments; la profondeur de récursion est `O(h)` où `h` est la hauteur des arbres. Autres

---

- Oui. 4. Mise en œuvre des références

> **Note:** Tous les extraits de code sont autonomes.
> La classe `Node` est définie exactement comme dans l'instruction du problème LeetCode.

#### 4.1 Java

"Java
// Définition pour un nœud binaire.
Numéro de classe {
la valeur nominale;
Noeud gauche, droit;
Node() { ce.val = '+'; }
Noeud(char val) { this.val = val; }
Nœuds (val.char, Noeud gauche, Noeud droit) {
ce.val = val; ce.gauche = gauche; ceci. droite = droite;
}
}

solution de classe publique {
contrôle public du booléenEquivalence(Node root1, Node root2) {
int[] cnt = nouveau int[26]; // a.z

dfs(root1, cnt);
dfs(root2, cnt);

pour (int c : cnt) {
si (c % 2 != 0) retourner faux;
}
retour vrai;
}

vide privé dfs(noeud, int[] cnt) {
si (noeud == nul) retour;
si (node.val != '+') { // opérand
cnt[node.val - 'a']++;
}
dfs(node.left, cnt);
dfs(node.right, cnt);
}
}
«» "

4.2 Python

'`python
# Définition d'un noeud d'arbre binaire.
Numéro de classe:
def __init_(self, val='+', gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
Contrôle Équivalence (self, root1: Node, root2: Node) -> bool:
cnt = [0] * 26

def dfs(node):
si ce n'est pas le nœud:
retour
si noeud.val != '+': # opérand
cnt[ord(node.val) - ord('a')] += 1
dfs(node.gauche)
Dfs(node.right)

dfs(root1)
dfs(root2)

retourner tous(c % 2 == 0 pour c in cnt)
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

// Définition pour un nœud binaire.
Numéro de structure {
la valeur nominale;
A gauche;
Noeud* droit;
Node(char v='+', Node* l=nullptr, Node* r=nullptr)
: val(v), gauche(l), droite(r) {}
};

solution de classe {
public:
bool checkEquivalence(Node* root1, Node* root2) {
vecteur <int> cnt(26, 0);
dfs(root1, cnt);
dfs(root2, cnt);
pour (int c : cnt)
si (c % 2 != 0) retourner faux;
retour vrai;
}

particulier:
vide dfs(noeud*, vecteur<int>& cnt) {
si (!node) retour;
si (noeud->val != '+')
++cnt[node->val - 'a'];
dfs(node->gauche, cnt);
dfs(node->right, cnt);
}
};
«» "

---

- Oui. 5. Suivi: Ajouter le `-` Opérateur

Si l'arbre peut également contenir `-`, le problème d'équivalence devient plus difficile:

* `-` est **non** commutatif: `a - b` - - b - a`.
* `-` est également **non** associatif: `a - b) - c` - a - b - c`.

Une stratégie commune:

1. **Canonicalize** chaque expression en la convertissant en une chaîne * entièrement entre parenthèses* (ou une autre forme normale).
2. Comparez les cordes canoniques.

En pratique, vous pouvez effectuer une traversée post-commande qui construit une chaîne :

"Java
Chaîne expr(Node n) {
si (n.val != '+') retourner String.valueOf(n.val);
retour "(" + expr(n.left) + n.val + expr(n.right) + ");
}
«» "

Pour la soustraction, vous utilisez simplement `-`.
Deux arbres sont équivalents iff `expr(root1).equals(exr(root2))`.

---

- Oui. 6. Article de blog: -Le Bien, le Mauvais, et le Ugly de l'Expression-Equivalence

> **Audience :** Ingénieurs en logiciels, interviewés, recruteurs et tous ceux qui veulent décrocher un rôle de développeur senior.

---

#### 6.1 Titre (SEO-optimisé)

*Check Si deux arbres d'expression sont équivalents – Java/Python/C++ Solution + Conseils d'entrevue

Pourquoi ? Le mot-clé « l'équivalence de l'arbre d'expression » est recherché par les intervieweurs, les recruteurs et les étudiants. Le jumeler avec le signal «Java/Python/C++» indique une expertise multilingue, ce qui stimule le référencement.

---

Description de la méta

> *Découvrez comment résoudre LeetCode 1612 en Java, Python et C++. Comprendre les mathématiques derrière les arbres commutatifs, voir le code complet, et découvrir des astuces de suivi pour la soustraction. Parfait pour votre prochaine entrevue de codage.

---

6.3 Aperçu

Section Objet
C'est quoi ?
Qu'est-ce qu'un arbre d'expression ? Autres
**Déclaration du problème**
**Simplicité, temps O(n), espace O(1)
**Cas de bord, uniquement pris en charge par `+`
L'extension à "-", pièges potentiels
Code complet Java, Python, C++
**Suivant-Mise en oeuvre**
**Conseils d'entretien**
Récapitulation + appel à l'action

---

### 6.4 Article de blog complet

> *(Le message de blog est formaté dans Markdown; copier-coller dans votre plateforme de blogs ou GitHub README.) *

```markdown
♪ Vérifiez si deux arbres d'expression sont équivalents – Java/Python/C++ Solution + Conseils d'entrevue

- Oui. 1. Pourquoi ce problème est votre entrevue

Les arbres d'expression sont l'épine dorsale des compilateurs, des moteurs de mathématiques symboliques et même de la communauté **LeetCode**. Être capable de prouver que deux arbres sont équivalents démontre la maîtrise sur:

- **Travaux d ' arbres** (DFS/BFS)
- **Propriétés algébriques**
- **Optimisation algorithmique** (temps linéaire, espace constant)

Si vous pouvez résoudre ce problème, les recruteurs verront que vous pouvez mélanger les structures de données avec la perspicacité mathématique.

- Oui. 2. Récapitulation des problèmes

On vous donne deux arbres binaires qui représentent des expressions arithmétiques avec seulement l'opérateur `+` et les opérandes minuscules. Retourner `true` si les expressions sont équivalentes pour *chaque* affectation possible aux variables.

**Exemples**

Explication
- C'est quoi ?
"[x]" "[x]" "[x]"
"[+,a,+,null,null,b,c]"" "[+,+,a,b,c]"" "true"" "a + (b + c)"
"[+,a,+,null,null,b,c]"" "[+,+,a,b,d]"" "false"" Différent opérande (`c` vs `d`) Autres

- Oui. 3. Les bonnes

- **O(n) Temps** – Chaque noeud est visité une fois.
- **O(1) Espace supplémentaire** – Un seul tableau de 26 éléments (constante pour les lettres minuscules).
- **Intuitive** – Comte opérandes, comparer la parité.
- **Extensible** – Fonctionne pour un nombre quelconque de variables.

- Oui. 4. Les mauvais

- **Seuls `+`** – La solution repose sur la commutativité et l'associativité. Si la soustraction apparaît, vous êtes hors de chance.
- **Grands Alphabets** – Si vous prenez en charge `A-Z` ou Unicode, la taille du tableau augmente, bien que toujours gérable.

- Oui. 5. L'Ugly

- **Soustraction (`-`)** – Non-commutative, non-associative. Un simple compteur échoue.
- **Parenthèses / Préséance de l'opérateur** – Si vous vous étendez à `*` ou `/`, vous avez besoin d'un analyseur complet ou d'un normalisateur d'expression.
- **Effets secondaires** – Si les opérandes ne sont pas indépendants (p. ex. fonctions ayant des effets secondaires), l'équivalence mathématique n'est plus suffisante.

5.1 Comment s'attaquer `- "

Une approche fiable est de **canonicaliser** chaque expression :

1. **Post-order traversal**: construire une chaîne `("(" + gauche + op + droite + ")")`.
2. Comparez les cordes canoniques.

Cela garantit que la structure (et l'ordre) est préservée. C'est temps O(n) et espace O(n), mais cela est acceptable pour les scénarios d'entrevue.

- Oui. 6. Passage du code

Voici des solutions propres et prêtes à la production en trois langues.

#### 6.1 Java

"Java
Numéro de classe {
la valeur nominale;
Noeud gauche, droit;
Node() { ce.val = '+'; }
Noeud(char val) { this.val = val; }
Nœuds (val.char, Noeud gauche, Noeud droit) {
ce.val = val; ce.gauche = gauche; ceci. droite = droite;
}
}

solution de classe publique {
contrôle public du booléenEquivalence(Node root1, Node root2) {
int[] cnt = nouveau int[26];
dfs(root1, cnt);
dfs(root2, cnt);
pour (int c : cnt) si (c % 2 != 0) retourner faux;
retour vrai;
}

vide privé dfs(noeud, int[] cnt) {
si (noeud == nul) retour;
si (node.val != '+') cnt[node.val - 'a']++;
dfs(node.left, cnt);
dfs(node.right, cnt);
}
}
«» "

6.2 Python

'`python
Numéro de classe:
def __init_(self, val='+', gauche=Aucun, droite=Aucun):
autoval = val
auto.gauche = gauche
soi.right = droit

Solution de classe:
Contrôle Équivalence (self, root1: Node, root2: Node) -> bool:
cnt = [0] * 26

def dfs(node):
si non noeud: retour
si noeud.val != '+':
cnt[ord(node.val) - ord('a')] += 1
dfs(node.gauche)
Dfs(node.right)

dfs(root1)
dfs(root2)
retourner tous(c % 2 == 0 pour c in cnt)
«» "

*### 6.3 C++

'`cpp
Numéro de structure {
la valeur nominale;
A gauche;
Noeud* droit;
Node(char v='+', Node* l=nullptr, Node* r=nullptr)
: val(v), gauche(l), droite(r) {}
};

solution de classe {
public:
bool checkEquivalence(Node* root1, Node* root2) {
vecteur <int> cnt(26, 0);
dfs(root1, cnt);
dfs(root2, cnt);
pour (int c : cnt) si (c % 2 != 0) retourner faux;
retour vrai;
}

particulier:
vide dfs(noeud*, vecteur<int>& cnt) {
si (!node) retour;
si (node->val != '+') ++cnt[node->val - 'a'];
dfs(node->gauche, cnt);
dfs(node->right, cnt);
}
};
«» "

- Oui. 7. Points d'entrevue

1. ** Expliquez les maths** – Parce que `+` est commutatif, seulement la parité de chaque variable est importante. (en milliers de dollars)
2. **Voir le code** – Partagez d'abord la solution contre-basée; puis demandez si vous pouvez étendre à `-`.
3. **Cas de bord en évidence** – Enfants null, arbres à nœud unique.
4. **Demander des éclaircissements** – Si l'intervieweur permet la soustraction ou d'autres opérateurs, pivotez vers la canonicalisation tôt.

- Oui. 8. A emporter

- **Maîtriser le contre-astuce** pour les arbres `+` purs.
- **Soyez prêts à canoniser** lorsque les contraintes du problème changent.
- **Pratique** écrire la solution à partir de zéro dans chaque langue. Cette maîtrise de la langue est un énorme aimant de recruteur.

> **Prêt à recevoir votre prochaine entrevue de codage?** Pratiquez ce problème sur LeetCode, ajoutez-le à votre portfolio et regardez les portes d'entrevue s'ouvrir.

«» "

«» "

---

6.5 Appel à l'action

- **Dépôt de GitHub** – Stocker les solutions et les cas de test.
- **LeetCode Profile** – Affichez les étiquettes de votre solution (`DFS`, `Hashing`, `Algorithmes`).
- **Liens** – Poster un extrait court avec le tag `#ExpressionTreeEquivalence`.
- **Recruiter Outreach** – Mentionnez le problème lors de l'entretien technique.

---

- Oui. 7. Pensées finales

Solving LeetCode 1612 est une victoire rapide** qui démontre l'élégance algorithmique. En fournissant un code complet en Java, Python et C++, vous montrez la polyvalence du langage. La section "Suivi-Up" enseigne aux recruteurs que vous pensez à l'avenir, prêts à gérer des ensembles d'opérateurs plus complexes.

Maintenant allez code, as l'entrevue, et atterrissez ce poste de procureur senior! *

«» "

---

## 7.1 Liste de contrôle de la publication

- Mots clés dans le titre & méta
- Tags linguistiques
- Blocs de code complets avec mise en évidence syntaxique
- Conseils de suivi et d'entrevue
- CTA (Download the GitHub repo)

---

Mot final

Ce problème est une *mine d'or* pour votre portefeuille d'entrevues. Maîtrisez le contre-tour linéaire, comprenez les limites et soyez prêt à pivoter vers des formes canoniques pour la soustraction. Avec les extraits de code multi-langue ci-dessus, vous n'êtes pas seulement en train de résoudre un défi LeetCode – vous livrez un pack d'entrevue **complet** que les recruteurs aimeront. Bon codage !
«» "

---

- Oui. 7. Remarques finales

Vous avez maintenant :

1. **Code de travail** en trois langues populaires.
2. Une compréhension claire de **quand** la solution fonctionne et **pourquoi**.
3. Un article **blog** prêt pour votre site personnel, LinkedIn, ou un message moyen, avec un titre SEO optimisé et une méta description.
4. Des explications prêtes à l'entrevue qui montrent que les recruteurs peuvent ** expliquer**, **justifier** et **extend** la solution.

** Prochaines étapes :**
- Exécuter les solutions contre une batterie d'essais unitaires.
- Construire une repo GitHub intitulée `leetcode-1612-expr-tree` contenant le code, les tests, et le blog Markdown.
- Publiez l'article.

Bonne chance – et que l'opérateur `+' soit toujours en votre faveur!